---
title: StringPool
author: Sergio0694
description: A type implementing a configurable pool for string instances
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, parallel, high performance, net core, net standard
dev_langs:
  - csharp
---

# StringPool

The [StringPool](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.highperformance.buffers.stringpool) type implements a configurable pool for `string` instances. This can be used to minimize allocations when creating multiple `string` instances from buffers of `char` or `byte` values. It provides a mechanism that is somewhat similar to [`string` interning](https://docs.microsoft.com/dotnet/api/system.string.intern), with the main differences being that the pool is configurable, can be reset, is implemented with a best-effort policy and doesn't require to pre-instantiate `string` objects, so it can save the initial allocations as well when working on temporary buffers.

## Syntax

The main entry point for `StringPool` is its `GetOrAdd(ReadOnlySpan<char>)` API, which returns a `string` instance matching the contents of the input `ReadOnlySpan>char>`, possibly getting the returned object from the internal pool.

As an example, imagine we have an input `string` representing the URL of a given web request, and we want to also retrieve a `string` with just the host name. If we get a large number of requests possibly for a small number of hosts, we might want to cache those `string` instances, we can do so by using the `StringPool` type as follows:

```csharp
public static string GetHost(string url)
{
    // We assume the input might start either with eg. https:// (or other prefix),
    // or directly with the host name. Furthermore, we also assume that the input
    // URL will always have a '/' character right after the host name.
    // For instance: "https://docs.microsoft.com/dotnet/api/system.string.intern".
    int
        prefixOffset = url.AsSpan().IndexOf(stackalloc char[] { ':', '/', '/' }),
        startIndex = prefixOffset == -1 ? 0 : prefixOffset + 3,
        endIndex = url.AsSpan(startIndex).IndexOf('/');

    // In this example, it would be "docs.microsoft.com"
    ReadOnlySpan<char> span = url.AsSpan(startIndex, endIndex);

    return StringPool.Shared.GetOrAdd(span);
}
```

The method above does no allocations at all if the requested `string` is already present in the cache, as the lookup is done with just a `ReadOnlySpan<char>` as input, representing a view on the input URL `string`.

The `StringPool` type can also be useful when parsing raw requests using a different encoding, for instance UTF8. There is a `GetOrAdd` overload that takes an input `ReadOnlySpan<byte>` and an `Encoding` instance, which uses a temporary buffer rented from the pool to retrieve a `ReadOnlySpan<char>` value to use for the lookup. This again can greatly reduce the number of allocations depending on the specific use case scenario.

## Properties

| Property | Return Type | Description |
| -- | -- | -- |
| Shared | StringPool | Gets the shared `StringPool` instance |
| Size | int | Gets the total number of `string`-s that can be stored in the current instance. |

## Methods

| Method | Return Type | Description |
| -- | -- | -- |
| Add(string) | void | Stores a `string` instance in the internal cache. |
| GetOrAdd(string) | string | Gets a cached `string` instance matching the input content, or stores the input one |
| GetOrAdd(ReadOnlySpan&lt;char&gt;) | string | Gets a cached `string` instance matching the input content, or creates a new one |
| GetOrAdd(ReadOnlySpan&lt;byte&gt;, Encoding) | string | Gets a cached `string` instance matching the input content (converted to Unicode), or creates a new one. |
| TryGet(ReadOnlySpan&lt;char&gt;, out string?) | bool | Tries to get a cached `string` instance matching the input content, if present |
| Reset() | void | Resets the current instance and its associated buckets |

## Sample Code

You can find more examples in our [unit tests](https://github.com/Microsoft/WindowsCommunityToolkit//blob/master/UnitTests/UnitTests.HighPerformance.Shared/Buffers)

## Requirements

| Device family | Universal, 10.0.16299.0 or higher |
| --- | --- |
| Namespace | Microsoft.Toolkit.HighPerformance |
| NuGet package | [Microsoft.Toolkit.HighPerformance](https://www.nuget.org/packages/Microsoft.Toolkit.HighPerformance/) |

## API

* [StringPool source code](https://github.com/Microsoft/WindowsCommunityToolkit//blob/master/Microsoft.Toolkit.HighPerformance/Buffers/StringPool.cs)
