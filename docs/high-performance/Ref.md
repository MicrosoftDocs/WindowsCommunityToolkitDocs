---
title: Ref&lt;T> and ReadOnlyRef&lt;T>
author: Sergio0694
description: Two stack-only types that can store a reference to a value of a specified type
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, parallel, high performance, net core, net standard
dev_langs:
  - csharp
---

# Ref&lt;T>

The [Ref&lt;T>](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.highperformance.ref-1) is a stack-only type that can store a reference to a value of a specified type. It is semantically equivalent to a `ref T` value, with the difference that it can also be used as a type of field in another stack-only `struct` type. It can be used in place of proper `ref T` fields, which are currently not supported in C#.

## How it works

> [!NOTE]
> Due to how it's implemented on different .NET Standard contracts, the `Ref<T>` has some minor differences on .NET Standard 1.4 and .NET Standard 2.1 (and equivalent .NET Core runtimes). In particular, on .NET Standard 1.4 it can only be used to reference fields _within an object_, instead of arbitrary values pointed by a managed reference. This is because the underlying APIs being used on .NET Standard 1.4 don't have built-in support for the `Span<T>` type.

### `Ref<T>` on .NET Standard 1.4

As mentioned before, on .NET Standard 1.4, `Ref<T>` can only point to locations within a given `object`. Consider the following code:

```csharp
// Be sure to include this using at the top of the file:
using Microsoft.Toolkit.HighPerformance;

// Define a sample model
class MyModel
{
    public int Number = 42;
}

var model = new MyModel();

// Create a Ref<T> pointing to the MyModel.Number field
Ref<int> byRef = new Ref<T>(model, ref model.Number);

// Modify the field indirectly
byRef.Value++;

Console.WriteLine(model.Number); // Prints 43!
```

> [!WARNING]
> The `Ref<T>` constructor doesn't validate the input arguments, meaning that it is your responsability to pass a valid `object` and a reference to a field within that object. Failing to do so might cause the `Ref<T>.Value` property to return an invalid reference.

### `Ref<T>` on .NET Standard 2.1

On .NET Standard 2.1, `Ref<T>` can point to any `ref T` value:

```csharp
int number = 42;

// Create a Ref<int> pointing to 'number'
Ref<int> byRef1 = new Ref<int>(ref number);

// Modify 'number'
byRef1.Value++;

Console.WriteLine(number); // Prints 43!
```

> [!WARNING]
> This type comes with a few caveats and should be used very carefully. On .NET Core runtimes, any use of `Ref<T>` may cause intermittent crashes or data corruptions, as `Ref<T>` is using internal implementation details of the .NET runtime in an unsupported way. Also, using this type can lead to runtime crashes if a `Ref<T>` instance is created with an invalid reference. In particular, you should only create a `Ref<T>` instance pointing to values that have a lifetime that is greater than that of the `Ref<T>` in use. Consider the following snippet:

```csharp
public static ref int GetDummyReference()
{
    int number = 42;

    Ref<int> byRef = new Ref<T>(ref number);
        
    return ref byRef.Value;        
}
```

This will compile and run fine, but the returned `ref int` will be invalid (as in, it will not point to a valid location) and could cause crashes if it's dereferenced. It is your responsability to track the lifetime of values being referenced by new `Ref<T>` values.

> [!NOTE]
> Although it is possible to create a `Ref<T>` value wrapping a `null` reference, by using the `default(Ref<T>)` expression, the `Ref<T>` type is not designed to be used with nullable references and does not include proper features to validate the internal reference. If you need to return a reference that can be set to `null`, use the `NullableRef<T>` and `NullableReadOnlyRef<T>` types.

## Properties

| Property | Return Type | Description |
| -- | -- | -- |
| Value | ref T | Gets the `T` reference represented by the current `Ref{T}` instance |

# ReadOnlyRef&lt;T>

The [ReadOnlyRef&lt;T>](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.highperformance.readonlyref-1) is a stack-only type that mirrors `Ref<T>`, with the exception that its constructor takes an `in T` parameter (a readonly reference), instead of a `ref T` one. Similarly, its `Value` property has a `ref readonly T` return type instead of `ref T`. 

## Properties

| Property | Return Type | Description |
| -- | -- | -- |
| Value | ref readonly T | Gets the `T` reference represented by the current `ReadOnlyRef{T}` instance |

## Sample Code

You can find more examples in our [unit tests](https://github.com/Microsoft/WindowsCommunityToolkit//blob/master/UnitTests/UnitTests.HighPerformance.Shared)

## Requirements

| Device family | Universal, 10.0 or higher |
| --- | --- |
| Namespace | Microsoft.Toolkit.HighPerformance |
| NuGet package | [Microsoft.Toolkit.HighPerformance](https://www.nuget.org/packages/Microsoft.Toolkit.HighPerformance/) |

## API

* [Ref&lt;T> source code](https://github.com/Microsoft/WindowsCommunityToolkit//blob/master/Microsoft.Toolkit.HighPerformance)
* [ReadOnlyRef&lt;T> source code](https://github.com/Microsoft/WindowsCommunityToolkit//blob/master/Microsoft.Toolkit.HighPerformance)
