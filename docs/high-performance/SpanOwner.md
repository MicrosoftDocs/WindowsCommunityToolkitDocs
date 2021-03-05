---
title: SpanOwner&lt;T>
author: Sergio0694
description: A stack-only buffer type renting memory from a shared pool
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, parallel, high performance, net core, net standard
dev_langs:
  - csharp
---

# SpanOwner&lt;T>

The [`SpanOwner<T>`](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.highperformance.buffers.spanowner-1) is a stack-only buffer type that rents buffers from a shared memory pool. It essentially mirrors the functionality of [`MemoryOwner<T>`](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.highperformance.buffers.memoryowner-1), but as a `ref struct` type. This is particularly useful for short-lived buffers that are only used in synchronous code (that don't require [`Memory<T>`](https://docs.microsoft.com/dotnet/api/system.memory-1) instances), as well as code running in a tight loop, as creating `SpanOwner<T>` values will not require memory allocations at all.

> **Platform APIs:** [`SpanOwner<T>`](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.highperformance.buffers.spanowner-1), [`MemoryOwner<T>`](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.highperformance.buffers.memoryowner-1)

## Syntax

The same core features of `MemoryOwner<T>` apply to this type as well, with the exception of it being a stack-only `struct`, and the fact that it lacks the [`IMemoryOwner<T>`](https://docs.microsoft.com/dotnet/api/system.buffers.imemoryowner-1) `interface` implementation, as well as the `Memory<T>` property. The syntax is virtually identical to that used with `MemoryOwner<T>` as well, except for the differences mentioned above.

As an example, suppose we have a method where we need to allocate a temporary buffer of a specified size (let's call this value `length`), and then use it to perform some work. A first, inefficient version might look like this:

```csharp
byte[] buffer = new byte[length];

// Use buffer here
```

This is not ideal, as we're allocating a new buffer every time this code is used, and then throwing it away immediately (as mentioned in the `MemoryOwner<T>` docs as well), which puts more pressure on the garbage collector. We can optimize the code above by using [`ArrayPool<T>`](https://docs.microsoft.com/dotnet/api/system.buffers.arraypool-1):

```csharp
// Using directive to access the ArrayPool<T> type
using System.Buffers;

int[] buffer = ArrayPool<int>.Shared.Rent(length);

try
{
    // Slice the span, as it might be larger than the requested size
    Span<int> span = buffer.AsSpan(0, length);

    // Use the span here
}
finally
{
    ArrayPool<int>.Shared.Return(buffer);
}
```

The code above rents a buffer from an array pool, but it's more verbose and error-prone: we need to be careful with the `try/finally` block to make sure to always return the rented buffer to the pool. We can rewrite it by using the `SpanOwner<T>` type, like so:

```csharp
// Be sure to include this using at the top of the file:
using Microsoft.Toolkit.HighPerformance.Buffers;

using SpanOwner<int> buffer = SpanOwner<int>.Allocate(length);

Span<int> span = buffer.Span;

// Use the span here, no slicing necessary
```

The `SpanOwner<T>` instance will internally rent an array, and will take care of returning it to the pool when it goes out of scope. We no longer need to use a `try/finally` block either, as the C# compiler will add that automatically when expanding that `using` statement. As such, the `SpanOwner<T>` type can be seen as a lightweight wrapper around the `ArrayPool<T>` APIs, which makes them both more compact and easier to use, reducing the amount of code that needs to be written to properly rent and dispose short lived buffers. You can see how using `SpanOwner<T>` makes the code much shorter and more straightforward.

> [!NOTE]
> As this is a stack-only type, it relies on the duck-typed `IDisposable` pattern introduced with C# 8. That is shown in the sample above: the `SpanOwner<T>` type is being used within a `using` block despite the fact that the type doesn't implement the `IDisposable` interface at all, and it's also never boxed. The functionality is just the same: as soon as the buffer goes out of scope, it is automatically disposed. The APIs in `SpanOwner{T}` rely on this pattern for extra performance: they assume that the underlying buffer will never be disposed as long as the `SpanOwner<T>` type is in scope, and they don't perform the additional checks that are done in `MemoryOwner<T>` to ensure that the buffer is in fact still available before returning a `Memory<T>` or `Span<T>` instance from it. As such, this type should always be used with a `using` block or expression. Not doing so will cause the underlying buffer not to be returned to the shared pool. Technically the same can also be achieved by manually calling `Dispose` on the `SpanOwner<T>` type (which doesn't require C# 8), but that is error prone and hence not recommended.

## Examples

You can find more examples in the [unit tests](https://github.com/Microsoft/WindowsCommunityToolkit//blob/master/UnitTests/UnitTests.HighPerformance.Shared/Buffers).