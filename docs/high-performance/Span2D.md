---
title: Span2D&lt;T> and ReadOnlySpan2D&lt;T>
author: Sergio0694
description: A stack-only type that mirrors the behavior of Span&lt;T> and ReadOnlySpan&lt;T>, but supporting arbitrary 2D memory locations
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, parallel, high performance, net core, net standard
dev_langs:
  - csharp
---

# Span2D&lt;T>

The [`Span2D<T>`](/dotnet/api/microsoft.toolkit.highperformance.span2d-1) is a type that mirrors the functionality of the [`Span<T>`](/dotnet/api/system.span-1) type, but it supports 2D memory regions. Just like [`Memory2D<T>`](/dotnet/api/microsoft.toolkit.highperformance.memory2d-1), it is extremely flexible and can wrap a number of different objects, as well as native pointers or GC references.

The internal layout is similar to that used by the [`Memory2D<T>`](/dotnet/api/microsoft.toolkit.highperformance.Memory2D-1) type, including a pitch parameter that is used to enable support for discontiguous memory buffers. You can read more info on this in the `Memory2D<T>` docs.

> **Platform APIs:** [`Span2D<T>`](/dotnet/api/microsoft.toolkit.highperformance.span2d-1), [`Memory2D<T>`](/dotnet/api/microsoft.toolkit.highperformance.Memory2D-1), [`ReadOnlySpan2D<T>`](/dotnet/api/microsoft.toolkit.highperformance.readonlyspan2d-1)

## Syntax

Here's how you can create a `Span2D<T>` instance from a 2D array:

```csharp
int[,] array =
{
    { 1, 2, 3 },
    { 4, 5, 6 }
};

Span2D<int> span = array;

// The memory directly maps the 2*3 array here

span[0, 0] = 10;
span[2, 1] = 20;

// The array is now:
// { 10, 2, 3 },
// { 4, 20, 6 }

// We can also use indices, on supported runtimes
int x = span[0, ^1];

// We can also get references to items, like with arrays
ref int reference = ref span[1, 1];

Span2D<int> slice = span.Slice(0, 1, 2, 2);

// Or alternatively, on supported runtimes

slice = span[.., 1..];

int[,] copy = slice.ToArray();

// The resulting array is:
// { 2, 3 },
// { 20, 6 }
```

We can also directly create a 2D view over native memory:

```csharp
int* p = stackalloc int[9];

Span2D<int> span = new Span2D<int>(p, 3, 3);
```

The `Span2D<T>` type also includes custom enumerator types to easily traverse a given row, column or the entire memory area using the standard `foreach` syntax in C#, as well as performing bulk operations in a single call:

```csharp
int[,] array =
{
    { 1, 2, 3 },
    { 4, 5, 6 },
    { 7, 8, 9 }
};

Span2D<int> span = array;

foreach (int i in span.GetColumn(1))
{
    // 2, 5, 8
}

// We can also iterate by reference
foreach (ref int i in span.GetRow(2))
{
    // 7, 8, 9
}

foreach (int i in span)
{
    // 1, 2, 3, 4, 5...
}

// Set all items in a column to 0
span.GetColumn(0).Clear();

// Set the value of all items in a row
span.GetRow(1).Fill(42);

Span<int> copy = stackalloc int[3];

// Copy all items from a column
span.GetColumn(2).CopyTo(copy);

// Get a copy of a row as an array
int[] array = span.GetRow(1).ToArray();
```

## ReadOnlySpan2D&lt;T>

The [`ReadOnlySpan2D<T>`](/dotnet/api/microsoft.toolkit.highperformance.readonlyspan2d-1) is to the `Span2D<T>` type what `ReadOnlySpan<T>` is to `Span<T>`. It exposes a similar set of APIs but provides no way to directly modify the contents of the underlying memory area.

## Sample Code

You can find more examples in the [unit tests](https://github.com/windows-toolkit/WindowsCommunityToolkit/blob/rel/7.1.0/UnitTests/UnitTests.HighPerformance.Shared).
