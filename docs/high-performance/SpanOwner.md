---
title: Spanowner&lt;T>
author: Sergio0694
description: A stack-only buffer type renting memory from a shared pool
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, parallel, high performance, net core, net standard
dev_langs:
  - csharp
---

# SpanOwner&lt;T>

The [SpanOwner&lt;T>](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.highperformance.buffers.spanowner-1) is a stack-only buffer type that rents buffers from a shared memory pool. It essentially mirrors the functionality of `MemoryOwner<T>`, but as a `ref struct` type. This is particularly useful for short-lived buffers that are only used in synchronous code (that don't require `Memory<T>` instances), as well as code running in a tight loop, as creating `SpanOwner<T>` values will not require memory allocations at all.

## Syntax

The same core features of `MemoryOwner<T>` apply to this type as well, with the exception of it being a stack-only `struct`, and the fact that it lacks the `IMemoryOwner<T>` `interface` implementation, as well as the `Memory<T>` property. The syntax is virtually identical to that used with `MemoryOwner<T>` as well:

```csharp
// Be sure to include this using at the top of the file:
using Microsoft.Toolkit.HighPerformance.Buffers;

using (SpanOwner<int> buffer = SpanOwner<int>.Allocate(42))
{
    // Buffer has exactly 42 items
    Span<int> span = buffer.Span;
}
```

**NOTE:** as this is a stack-only type, it relies on the duck-typed `IDisposable` pattern introduced with C# 8. That is shown in the sample above: the `SpanOwner<T>` type is being used within a `using` block despite the fact that the type doesn't implement the `IDisposable` interface at all, and it's also never boxed. The functionality is just the same: as soon as the buffer goes out of scope, it is automatically disposed. The APIs in `SpanOwner{T}` rely on this pattern for extra performance: they assume that the underlying buffer will never be disposed as long as the `SpanOwner<T>` type is in scope, and they don't perform the additional checks that are done in `MemoryOwner<T>` to ensure that the buffer is in fact still available before returning a `Memory<T>` or `Span<T>` instance from it. As such, this type should always be used with a `using` block or expression. Not doing so will cause the underlying buffer not to be returned to the shared pool. Technically the same can also be achieved by manually calling `Dispose` on the `SpanOwner<T>` type (which doesn't require C# 8), but that is error prone and hence not recommended.

The `SpanOwner<T>` type can also be seen as a lightweight wrapper around the `ArrayPool<T>` APIs, which makes them both more compact and easier to use, reducing the amount of code that needs to be written to properly rent and dispose short lived buffers. For reference, the previous code sample is conceptually equivalent to this snippet:

```csharp
// Using directive to access the ArrayPool<T> type
using System.Buffers;

int[] buffer = ArrayPool<int>.Shared.Rent(42);

try
{
    // The span needs to manually be sliced to have the right length
    Span<int> span = buffer.AsSpan(0, 42);
}
finally
{
    ArrayPool<int>.Shared.Return(buffer);
}
```

You can see how using `SpanOwner<T>` makes the code much shorter and more straightforward.

## Properties

| Property | Return Type | Description |
| -- | -- | -- |
| Length | int | Gets the number of items in the current instance |
| Span | System.Span&lt;T> | Gets a span wrapping the memory belonging to the current instance |
| Empty | SpanOwner&lt;T> | Gets an empty `SpanOwner<T>` instance |

## Methods

| Method | Return Type | Description |
| -- | -- | -- |
| Allocate(int) | Memory&lt;T> | Creates a new `SpanOwner<T>` instance with the specified parameters |
| Allocate(int, AllocationMode) | Memory&lt;T> | Creates a new `SpanOwner<T>` instance with the specified parameters |
| DangerousGetReference() | ref T | Returns a reference to the first element within the current instance, with no bounds check |

## Sample Code

You can find more examples in our [unit tests](https://github.com/Microsoft/WindowsCommunityToolkit//blob/master/UnitTests/UnitTests.HighPerformance.Shared/Buffers)

## Requirements

| Device family | Universal, 10.0.16299.0 or higher |
| --- | --- |
| Namespace | Microsoft.Toolkit.HighPerformance |
| NuGet package | [Microsoft.Toolkit.HighPerformance](https://www.nuget.org/packages/Microsoft.Toolkit.HighPerformance/) |

## API

* [SpanOwner&lt;T> source code](https://github.com/Microsoft/WindowsCommunityToolkit//blob/master/Microsoft.Toolkit.HighPerformance/Buffers)
