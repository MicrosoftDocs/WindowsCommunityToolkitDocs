---
title: ThrowHelper
author: Sergio0694
description: Helper methods to efficiently throw exceptions
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, debug, net core, net standard
dev_langs:
  - csharp
---

# ThrowHelper

The [ThrowHelper](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.diagnostics.ThrowHelper) class is a helper type that can be used to efficiently throw exceptions. It is meant to support the [Guard](Guard.md) APIs, and it should primarily be used in situations where developers need fine-grained controls over the exception types being thrown, or over the exact exception message to include.

## Syntax

The `ThrowHelper` class exposes a series of `ThrowException` APIs that offer a 1:1 mapping to the constructors of all the available exception types. These methods are meant to be used in place of the classic `throw new Exception(...)` statement in code, as it will result in smaller and more efficient code. Put simply:

```csharp
// Replace this...
throw new InvalidOperationException("Some custom message from my library");

// ...with this
ThrowHelper.ThrowInvalidOperationException("Some custom message from my library");
```

> [!NOTE]
> This will also result in a slightly different stack trace, as the exception will be thrown by this helper method instead of directly by the original caller. The practical result is still the same as throwing an exception directly.

The `Guard` APIs provide an easy to use abstraction over many common checks that might need to be performed, so it is recommended to first try to see if there is a `Guard` API that can be used, and only fallback on using `ThrowHelper` if that's not the case. As mentioned before, this might be if your library needs to throw a specific exception type not present in the `Guard` APIs, or if you need full control on the exact arguments being included in the exception being thrown.

There are also generic overloads for all the available APIs, which can be used within expressions that require a return type of a specific type (eg. a switch expression). These overloads never return any value, but the return type is declared to allow the C# compiler to accept the usage of these APIs within expressions that wouldn't work with a method returning `void`. Consider the following example:

```csharp
int result = text switch
{
    "cat" => 0,
    "dog" => 1,
    _ => ThrowHelper.ThrowArgumentException<string>(nameof(text))
};
```

Here we're using `ThrowHelper` within an expression that requires a return type of type `string`, so we can use the generic overload of `ThrowArgumentException` to make this possible. This also works with patterns such as ternary operators (`x ? a : b`), null-coalescing operators (`x = a ?? b`) null-coalescing assignment operators (`x ??= y`), and more.

## Methods

There are lots of different methods and overloads in the `ThrowHelper` class, providing access to the following exceptions (and mapping all their public constructors):

- [ArrayTypeMismatchException](https://docs.microsoft.com/dotnet/api/system.ArrayTypeMismatchException)
- [ArgumentException](https://docs.microsoft.com/dotnet/api/system.ArgumentException)
- [ArgumentNullException](https://docs.microsoft.com/dotnet/api/system.ArgumentNullException)
- [ArgumentOutOfRangeException](https://docs.microsoft.com/dotnet/api/system.ArgumentOutOfRangeException)
- [COMException](https://docs.microsoft.com/dotnet/api/system.runtime.interopservices.COMException)
- [ExternalException](https://docs.microsoft.com/dotnet/api/system.runtime.interopservices.ExternalException)
- [FormatException](https://docs.microsoft.com/dotnet/api/system.FormatException)
- [InsufficientMemoryException](https://docs.microsoft.com/dotnet/api/system.InsufficientMemoryException)
- [InvalidDataException](https://docs.microsoft.com/dotnet/api/system.io.InvalidDataException)
- [InvalidOperationException](https://docs.microsoft.com/dotnet/api/system.InvalidOperationException)
- [LockRecursionException](https://docs.microsoft.com/dotnet/api/system.threading.LockRecursionException)
- [MissingFieldException](https://docs.microsoft.com/dotnet/api/system.MissingFieldException)
- [MissingMemberException](https://docs.microsoft.com/dotnet/api/system.MissingMemberException)
- [MissingMethodException](https://docs.microsoft.com/dotnet/api/system.MissingMethodException)
- [NotSupportedException](https://docs.microsoft.com/dotnet/api/system.NotSupportedException)
- [ObjectDisposedException](https://docs.microsoft.com/dotnet/api/system.ObjectDisposedException)
- [OperationCanceledException](https://docs.microsoft.com/dotnet/api/system.OperationCanceledException)
- [PlatformNotSupportedException](https://docs.microsoft.com/dotnet/api/system.PlatformNotSupportedException)
- [SynchronizationLockException](https://docs.microsoft.com/dotnet/api/system.threading.SynchronizationLockException)
- [TimeoutException](https://docs.microsoft.com/dotnet/api/system.TimeoutException)
- [UnauthorizedAccessException](https://docs.microsoft.com/dotnet/api/system.UnauthorizedAccessException)
- [Win32Exception](https://docs.microsoft.com/dotnet/api/system.componentmodel.Win32Exception)

You can see the available constructors for each of these exception types from the linked docs - the respective `ThrowHelper` APIs will simply offer a series of overloads corresponding to the existing constructors for that specified type. Each API is simply named "Throw" + the exception type.

## Technical Details

The following section describes the impact of switching to `ThrowHelper` APIs over the standard `throw new Expression` statements with respect to the codegen. As mentioned above, knowing these details is not necessary in order to use these APIs, but for developers familiar with how the runtime works or with how the JIT processes code during execution, this will provide a clearer explanation of why using the `ThrowHelper` pattern results in more compact and faster code. In order to do so, we will need to have a peek at the code that the JIT compiler is actually producing in these situations. We will use the code generated on .NET Core 3.1 x64 as a reference, but the same concept applies to other runtimes and architectures as well.

Let's consider this simple type:

```csharp
public struct ExceptionTest
{
    private int number;
    
    public int GetValueIfNotZeroOrThrow()
    {
        if (number == 0)
        {
            throw new InvalidOperationException("The value must be != 0");
        }
        
        return number;
    }
}
```

This type is only meant to showcase the use of `ThrowHelper` APIs. Here we're simply checking the value of the `number` field, and throwing if it's 0. Let's check the generated asm code:

```x86asm
ExceptionTest.GetValueIfNotZeroOrThrow()
    mov eax, [rcx]              ; read number
    test eax, eax               ; if (number != 0)
    je short L0011              ; jump to faulting path (if == 0)
    ret                         ; return (number is already in eax)
    mov rcx, 0x7ff95cbaca80     ; exception setup...
    call 0x00007ff9bc6178f0
    mov rsi, rax
    mov ecx, 1
    mov rdx, 0x7ff96590c080
    call 0x00007ff9bc7403e0
    mov rdx, rax
    mov rcx, rsi
    call System.InvalidOperationException..ctor(System.String)
    mov rcx, rsi
    call 0x00007ff9bc5db3a0
    int3 ; finally throw the exception
```

We can see the code contains a lot of lines just dedicated to creating the exception being thrown. This can cause a large increase in the code size whenever we have many of these checks because it will reduce the efficiency of the instruction cache, etc. In general, we'd like the size of our methods to be as small as possible.

The above snippet, rewritten using the `ThrowHelper` APIs, would like like this:

```csharp
public int GetValueIfNotZeroOrThrow()
{
    if (number == 0)
    {
        ThrowHelper.ThrowInvalidOperationException("The value must be != 0");
    }

    return number;
}
```

Which results in the following assembly:

```x86asm
ExceptionTest.GetValueIfNotZeroOrThrow2()
    mov eax, [rcx]          ; load number
    test eax, eax           ; if (number != 0)
    je short L000f          ; faulting path (if == 0)
    ret                     ; return number (already in eax)
    mov rcx, 0x23435d85b98  ; load the exception message
    mov rcx, [rcx]
    call ThrowHelper.ThrowInvalidOperationException(System.String) ; ThrowHelper call!
    int3 ; return with fault
```

We can see that the resulting assembly is much smaller than before. We basically moved all the code to create the exception out of the method, which also means we can just always reuse the same code from the `ThrowHelper` APIs, with different arguments, instead of inlining the exception throw in every single one of our methods. Here we only have those two `mov` instructions to load the `string` with our exception type, and then we jump to the `ThrowHelper.ThrowInvalidOperationException` method. The JIT compiler is able to see that that method will always throw, so it will never inline that call, and it will make sure to rewrite our conditional branches in the best way possible (specifically, knowing what is the branch that is supposed to be executed, without faulting).

## Requirements

| Implementation | .NET Standard 2.0 |
| --- | --- |
| Namespace | Microsoft.Toolkit.Diagnostics |
| NuGet package | [Microsoft.Toolkit](https://www.nuget.org/packages/Microsoft.Toolkit/) |

The ThrowHelper class supports .NET Standard

## API

- [ThrowHelper source code](https://github.com/Microsoft/WindowsCommunityToolkit/blob/master/Microsoft.Toolkit/Diagnostics/ThrowHelper.ThrowExceptions.cs)

## Related Topics

- [Guard](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.diagnostics.guard)
