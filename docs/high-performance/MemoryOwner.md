---
title: MemoryOwner&lt;T> and SpanOwner&lt;T>
author: Sergio0694
description: Buffer types that rent memory from a shared pool
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, parallel, high performance, net core, net standard
dev_langs:
  - csharp
---

# MemoryOwner&lt;T>

The [MemoryOwner&lt;T>](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.highperformance.buffers.memoryowner-1) is a buffer type implementing `IMemoryOwner<T>`, an embedded length property and a series of performance oriented APIs. It is essentially a lightweight wrapper around the `ArrayPool<T>` type, with some additional helper utilities.

## How it works

`MemoryOwner<T>` has the following main features:

- One of the main issues of arrays returned by the `ArrayPool<T>` APIs and of the `IMemoryOwner<T>` instances returned by the `MemoryPool<T>` APIs is that the size specified by the user is only being used as a _minum_ size: the actual size of the returned buffers might actually be greater. `MemoryOwner<T>` solves this by also storing the original requested size, so that `Memory<T>` and `Span<T>` instances retrieved from it will never need to be manually sliced.
- When using `IMemoryOwner<T>`, getting a `Span<T>` for the underlying buffer requires first to get a `Memory<T>` instance, and then a `Span<T>`. This is fairly expensive, and often unnecessary, as the intermediate `Memory<T>` might actually not be needed at all. `MemoryOwner<T>` instead has an additional `Span` property which is extremely lightweight, as it directly wraps the internal `T[]` array being rented from the pool.
- Buffers rented from the pool are not cleared by default, which means that if they were not cleared when being previous returned to the pool, they might contain garbage data. Normally, users are required to clear these rented buffers manually, which can be verbose especially when done frequently. `MemoryOwner<T>` has a more flexible approach to this, through the `Allocate(int, AllocationMode)` API. This method not only allocates a new instance of exactly the requested size, but can also be used to specify which allocation mode to use: either the same one as `ArrayPool<T>`, or one that automatically clears the rented buffer.
- There are cases where a buffer might be rented with a greater size than what is actually needed, and then resized afterwards. This would normally require users to rent a new buffer and copy the region of interest from the old buffer. Instead, `MemoryOwner<T>` exposes a `Slice(int, int)` API that simply return a new instance wrapping the specified area of interest. This allows to skip renting a new buffer and copying the items entirely.

## Syntax

Here is an example of how to rent a buffer and retrieve a `Memory<T>` instance:

```csharp
// Be sure to include this using at the top of the file:
using Microsoft.Toolkit.HighPerformance.Buffers;

using (MemoryOwner<int> buffer = MemoryOwner<T>.Allocate(42))
{
    // Buffer has exactly 42 items
    Memory<T> memory = buffer.Memory;
    Span<T> span = buffer.Span;
}
```

In this example, we used a `using` block to declare the `MemoryOwner<T>` buffer: this is particularly useful as the underlying array will automatically be returned to the pool at the end of the block. If instead we don't have direct control over the lifetime of a `MemoryOwner<T>` instance, the buffer will simply be returned to the pool when the object is finalized by the garbage collector. In both cases, rented buffers will always be correctly returned to the shared pool.

## Properties

| Property | Return Type | Description |
| -- | -- | -- |
| Length | int | Gets the number of items in the current instance |
| Memory | System.Memory&lt;T> | Gets the memory belonging to this owner |
| Span | System.Span&lt;T> | Gets a span wrapping the memory belonging to the current instance |
| Empty | MemoryOwner&lt;T> | Gets an empty `MemoryOwner<T>` instance |

## Methods

| Method | Return Type | Description |
| -- | -- | -- |
| Allocate(int) | Memory&lt;T> | Creates a new `MemoryOwner<T>` instance with the specified parameters |
| Allocate(int, AllocationMode) | Memory&lt;T> | Creates a new `MemoryOwner<T>` instance with the specified parameters |
| DangerousGetReference() | ref T | Returns a reference to the first element within the current instance, with no bounds check |
| Slice(int, int) | MemoryOwner&lt;T> | Slices the buffer currently in use and returns a new `MemoryOwner<T>` instance |

## Sample Code

You can find more examples in our [unit tests](https://github.com/Microsoft/WindowsCommunityToolkit//blob/master/UnitTests/UnitTests.HighPerformance.Shared/Buffers)

## Requirements

| Device family | Universal, 10.0.16299.0 or higher |
| --- | --- |
| Namespace | Microsoft.Toolkit.HighPerformance |
| NuGet package | [Microsoft.Toolkit.HighPerformance](https://www.nuget.org/packages/Microsoft.Toolkit.HighPerformance/) |

## API

* [MemoryOwner&lt;T> source code](https://github.com/Microsoft/WindowsCommunityToolkit//blob/master/Microsoft.Toolkit.HighPerformance/Buffers)
