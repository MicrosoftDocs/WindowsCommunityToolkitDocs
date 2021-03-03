---
title: Introduction to the High Performance package
author: Sergio0694
description: An overview of how to get started with High Performance package and to the APIs it contains
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, get started, visual studio, high performance, net core, net standard
---

# Introduction to the High Performance package

This package can be installed through NuGet, and it has the following multi-targets:

- .NET Standard 1.4
- .NET Standard 2.0
- .NET Standard 2.1
- .NET Core 2.1
- .NET Core 3.1

This means that you can use it from anything from UWP or legacy .NET Framework applications, games written in Unity, cross-platform mobile applications using Xamarin, to .NET Standard libraries and modern .NET Core 2.1 or .NET Core 3.1 applications. The API surface is almost identical in all cases, and lots of work has been put into backporting as many features as possible to older targets like .NET Standard 1.4 and .NET Standard 2.0. Except for some minor differences, you can expect the same APIs to be available on all target frameworks.

The reason why multi-targeting has been used is to allow the package to leverage all the latest APIs on modern runtimes (like .NET Core 3.1) whenever possible, while still offering most of its functionalities to all target platforms. It also makes it possible for .NET Core 2.1 to use all the APIs that it has in common with .NET Standard 2.1, even though the runtime itself doesn't fully implement .NET Standard 2.1. All of this would not have been possible without multi-targeting to both .NET Standard as well as individual runtimes.

Follow these steps to install the High Performance package:

1. Open an existing project in Visual studio, targeting any of the following:
    - UWP (>= 10.0)
    - .NET Standard (>= 1.4)
    - .NET Core (>= 1.0)
    - Any other framework supporting .NET Standard 1.4 and up

2. In Solution Explorer panel, right click on your project name and select **Manage NuGet Packages**. Search for **Microsoft.Toolkit.HighPerformance** and install it.

    ![NuGet Packages](../resources/images/ManageNugetPackages.png "Manage NuGet Packages Image")

3. Add a using directive in your C# files to use the new APIs:

    ```csharp
    using Microsoft.Toolkit.HighPerformance;
    ```

4. If you want so see some code samples, you can either read through the other docs pages for the High Performance package, or have a look at the various [unit tests](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/master/UnitTests/UnitTests.HighPerformance.Shared) for the project.

## When should I use this package?

As the name suggests, the High Performance package contains a set of APIs that are heavily focused on optimization. All the new APIs have been carefully crafted to achieve the best possible performance when using them, either through reduced memory allocation, micro-optimizations at the assembly level, or by structuring the APIs in a way that facilitates writing performance oriented code in general.

This package makes heavy use of APIs such as:

- [System.Buffers.ArrayPool<T>](https://docs.microsoft.com/dotnet/api/system.buffers.arraypool-1)
- [System.Runtime.CompilerServices.Unsafe](https://docs.microsoft.com/dotnet/api/system.runtime.compilerservices.unsafe)
- [System.Runtime.InteropServices.MemoryMarshal](https://docs.microsoft.com/dotnet/api/system.runtime.interopservices.memorymarshal)
- [System.Threading.Tasks.Parallel](https://docs.microsoft.com/dotnet/api/system.threading.tasks.parallel)

If you are already familiar with these APIs or even if you're just getting started with writing high performance code in C# and want a set of well tested helpers to use in your own projects, have a look at what's included in this package to see how you can use it in your own projects!

## Where to start?

Here are some APIs you could look at first, if you were already using one of those types mentioned above:
- [MemoryOwner<T>](MemoryOwner.md) and [SpanOwner<T>](SpanOwner.md), if you were using `System.Buffers.ArrayPool<T>`.
- [ParallelHelper](ParallelHelper.md), if you were using `System.Threading.Tasks.Parallel`.
