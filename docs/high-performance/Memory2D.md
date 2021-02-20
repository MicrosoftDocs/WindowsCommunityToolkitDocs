---
title: Memory2D&lt;T> and ReadOnlyMemory2D&lt;T>
author: Sergio0694
description: A value type that mirrors the behavior of Memory&lt;T> and ReadOnlyMemory&lt;T> with the addition of supporting arbitrary 2D memory locations
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, parallel, high performance, net core, net standard
dev_langs:
  - csharp
---

# Memory2D&lt;T>

The [`Memory2D<T>`](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.highperformance.memory.memory2d-1) is a type that mirrors the functionality of the [`Memory<T>`](https://docs.microsoft.com/dotnet/api/system.memory-1) type, with the difference being that it can be used to represent 2D memory locations. It is extremely flexible and is capable of wrapping a number of different types, including ND arrays (with explicit support for 1D, 2D, and 3D arrays) or `Memory<T>` instances. This type is meant to be used together with the [`Span2D<T>`](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.highperformance.memory.span2d-1) type, in the same way that `Memory<T>` is used along with [`Span<T>`](https://docs.microsoft.com/dotnet/api/system.span-1). For more info on the key differences and use case scenarios of these two types, you can read [this docs page](https://docs.microsoft.com/dotnet/standard/memory-and-spans/memory-t-usage-guidelines).

> **Platform APIs:** [`Memory2D<T>`](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.highperformance.memory.memory2d-1), [`Span2D<T>`](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.highperformance.memory.span2d-1), [`ReadOnlyMemory2D<T>`](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.highperformance.memory.readonlymemory2d-1)

## How it works

The `Memory2D<T>` type internally tracks the mapped 2D memory area through a reference to the wrapped object, the height and width parameters, and a special pitch parameter. The height and width indicate the length of the rows and columns in the 2D memory area, while the pitch indicates the offset between the end of each row and the start of the following one. 

Here's a simple diagram that illustrates this configuration (the "XX" cells in the grid represent items belonging to the target 2D memory area):

```csharp
//                _____________________stride_____...
//  reference__  /________width_________  ________...
//             \/                       \/
// | -- | -- | |- | -- | -- | -- | -- | -- | -- | -- |_
// | -- | -- | XX | XX | XX | XX | XX | XX | -- | -- | |
// | -- | -- | XX | XX | XX | XX | XX | XX | -- | -- | |
// | -- | -- | XX | XX | XX | XX | XX | XX | -- | -- | |_height
// | -- | -- | XX | XX | XX | XX | XX | XX | -- | -- |_|
// | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- |
// | -- | -- | -- | -- | -- | -- | -- | -- | -- | -- |
// ...__pitch__/
// ...________/
```

This configuration allows `Memory2D<T>` to be extremely flexible in the way it maps existing buffers to 2D memory areas, as it makes it possible to also represent discontiguous buffers as a "virtual" 2D memory location. For instance, here's a few examples of buffer types that a `Memory2D` instance can map to:
- A 1D `T[]` array which is mapped as a 2D memory area in row-major order.
- A 2D `T[,]` array, mapped directly to a `Memory2D<T>` instance.
- A 3D `T[,,]` array, with a `Memory2D<T>` instance representing a given depth slice (a layer).

The `Memory<T>` type also exposes a number of utility methods, including most of the same API surface that the standard `Memory<T>` implements. For instance, it includes a `Slice(int, int)` method that makes it easy to do 2D slicing operations directly on the virtual 2D memory location, with the `Memory2D<T>` instance automatically adjusting the necessary parameters internally to shift its mapping on the right memory area(s) corresponding to the requested result.

## Syntax

Here's how you can create a `Memory2D<T>` instance from a 2D array:

```csharp
int[,] array =
{
    { 1, 2, 3 },
    { 4, 5, 6 },
    { 7, 8, 9 }
};

Memory2D<int> memory = array;

// The memory directly maps the 2*3 array here

Memory2D<int> slice = memory.Slice(0, 1, 2, 2);

// We create a slice from row 0 and column 1, of size 2*2

int[,] copy = slice.ToArray();

// { 2, 3 }
// { 5, 6 }

// If on a supported runtime, we can also slice using a range

Memory2D<int> test = memory[.., ..2];

// { 1, 2 }
// { 4, 5 }
// { 7, 8 }

Span2D<int> span = memory.Span;

// We can use the span to perform operations on the underlying
// data for the memory instance. All the available APIs are
// documented in the docs about the Span2D<T> type.

```

## ReadOnlyMemory2D&lt;T>

The [`ReadOnlyMemory2D<T>`](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.highperformance.memory.readonlymemory2d-1) is to the `Memory2D<T>` type what `ReadOnlyMemory<T>` is to `Memory<T>`. It exposes the same exact functionalities (minus the APIs that involve modifying the contents of the wrapped memory area) and provides a read-only view to arbitrary 2D memory locations. For more info on how this type works, you can refer to the paragraph on the `Memory2D<T>` type above.

## Examples

You can find more examples in the [unit tests](https://github.com/Microsoft/WindowsCommunityToolkit//blob/master/UnitTests/UnitTests.HighPerformance.Shared).