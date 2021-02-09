---
title: MemoryOwner&lt;T>
author: Sergio0694
description: A buffer type implementing `IMemoryOwner<T>` that rents memory from a shared pool
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, parallel, high performance, net core, net standard
dev_langs:
  - csharp
---

# MemoryOwner&lt;T>

The [MemoryOwner&lt;T>](/dotnet/api/microsoft.toolkit.highperformance.buffers.memoryowner-1) is a buffer type implementing [`IMemoryOwner<T>`](/dotnet/api/system.buffers.imemoryowner-1), an embedded length property and a series of performance oriented APIs. It is essentially a lightweight wrapper around the [`ArrayPool<T>`](/dotnet/api/system.buffers.arraypool-1) type, with some additional helper utilities.

## How it works

`MemoryOwner<T>` has the following main features:

- One of the main issues of arrays returned by the `ArrayPool<T>` APIs and of the `IMemoryOwner<T>` instances returned by the `MemoryPool<T>` APIs is that the size specified by the user is only being used as a _minum_ size: the actual size of the returned buffers might actually be greater. `MemoryOwner<T>` solves this by also storing the original requested size, so that [`Memory<T>`](/dotnet/api/system.memory-1) and [`Span<T>`](/dotnet/api/system.span-1) instances retrieved from it will never need to be manually sliced.
- When using `IMemoryOwner<T>`, getting a `Span<T>` for the underlying buffer requires first to get a `Memory<T>` instance, and then a `Span<T>`. This is fairly expensive, and often unnecessary, as the intermediate `Memory<T>` might actually not be needed at all. `MemoryOwner<T>` instead has an additional `Span` property which is extremely lightweight, as it directly wraps the internal `T[]` array being rented from the pool.
- Buffers rented from the pool are not cleared by default, which means that if they were not cleared when being previous returned to the pool, they might contain garbage data. Normally, users are required to clear these rented buffers manually, which can be verbose especially when done frequently. `MemoryOwner<T>` has a more flexible approach to this, through the `Allocate(int, AllocationMode)` API. This method not only allocates a new instance of exactly the requested size, but can also be used to specify which allocation mode to use: either the same one as `ArrayPool<T>`, or one that automatically clears the rented buffer.
- There are cases where a buffer might be rented with a greater size than what is actually needed, and then resized afterwards. This would normally require users to rent a new buffer and copy the region of interest from the old buffer. Instead, `MemoryOwner<T>` exposes a `Slice(int, int)` API that simply return a new instance wrapping the specified area of interest. This allows to skip renting a new buffer and copying the items entirely.

## Syntax

Here is an example of how to rent a buffer and retrieve a `Memory<T>` instance:

```csharp
// Be sure to include this using at the top of the file:
using Microsoft.Toolkit.HighPerformance.Buffers;

using (MemoryOwner<int> buffer = MemoryOwner<int>.Allocate(42))
{
    // Both memory and span have exactly 42 items
    Memory<int> memory = buffer.Memory;
    Span<int> span = buffer.Span;

    // Writing to the span modifies the underlying buffer
    span[0] = 42;
}
```

In this example, we used a `using` block to declare the `MemoryOwner<T>` buffer: this is particularly useful as the underlying array will automatically be returned to the pool at the end of the block. If instead we don't have direct control over the lifetime of a `MemoryOwner<T>` instance, the buffer will simply be returned to the pool when the object is finalized by the garbage collector. In both cases, rented buffers will always be correctly returned to the shared pool.

## When should this be used?

`MemoryOwner<T>` can be used as a general purpose buffer type, which has the advantage of minimizing the number of allocations done over time, as it internally reuses the same arrays from a shared pool. A common use case is to replace `new T[]` array allocations, especially when doing repeated operations that either require a temporary buffer to work on, or that produce a buffer as a result.

Suppose we have a dataset consisting of a series of binary files, and that we need to read all these files and process them in some way. To properly separate our code, we might end up writing a method that simply reads one binary file, which might look like this:

```csharp
public static byte[] GetBytesFromFile(string path)
{
    using Stream stream = File.OpenRead(path);

    byte[] buffer = new byte[(int)stream.Length];

    stream.Read(buffer, 0, buffer.Length);

    return buffer;
}
```

Note that `new byte[]` expression. If we read a large number of files, we'll end up allocating a lot of new arrays, which will put a lot of pressure over the garbage collector. We might want to refactor this code using buffers rented from a pool, like so:

```csharp
public static (byte[] Buffer, int Length) GetBytesFromFile(string path)
{
    using Stream stream = File.OpenRead(path);

    byte[] buffer = ArrayPool<T>.Shared.Rent((int)stream.Length);

    stream.Read(buffer, 0, (int)stream.Length);

    return (buffer, (int)stream.Length);
}
```

Using this approach, buffers are now rented from a pool, which means that in most cases we're able to skip an allocation. Additionally, since rented buffers are not cleared by default, we can also save the time needed to fill them with zeros, which gives us another small performance improvement. In the example above, loading 1000 files would bring the total allocation size from around 1MB down to just 1024 bytes - just a single buffer would effectively be allocated, and then reused automatically.

There are two main issues with the code above:
- `ArrayPool<T>` might return buffers that have a size greater than the requested one. To work around this issue, we need to return a tuple which also indicates the actual used size into our rented buffer.
- By simply returning an array, we need to be extra careful to properly track its lifetime and to return it to the appropriate pool. We might work around this issue by using [`MemoryPool<T>`](/dotnet/api/system.buffers.memorypool-1) instead and by returning an `IMemoryOwner<T>` instance, but we still have the problem of rented buffers having a greater size than what we need. Additionally, `IMemoryOwner<T>` has some overhead when retrieving a `Span<T>` to work on, due to it being an interface, and the fact that we always need to get a `Memory<T>` instance first, and then a `Span<T>`.

To solve both these issues, we can refactor this code again by using `MemoryOwner<T>`:

```csharp
public static MemoryOwner<byte> GetBytesFromFile(string path)
{
    using Stream stream = File.OpenRead(path);

    MemoryOwner<byte> buffer = MemoryOwner<byte>.Allocate((int)stream.Length);

    stream.Read(buffer.Span);

    return buffer;
}
```

The returned `IMemoryOwner<byte>` instance will take care of disposing the underlying buffer and returning it to the pool when its [`IDisposable.Dispose`](/dotnet/api/system.idisposable.dispose) method is invoked. We can use it to get a `Memory<T>` or `Span<T>` instance to interact with the loaded data, and then dispose the instance when we no longer need it. Additionally, all the `MemoryOwner<T>` properties (like `MemoryOwner<T>.Span`) respect the initial requested size we used, so we no longer need to manually keep track of the effective size within the rented buffer.

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