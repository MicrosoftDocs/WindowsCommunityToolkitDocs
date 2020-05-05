---
title: Introduction to the High Performance package
author: Sergio0694
description: An overview of how to get started with High Performance package and to the APIs it contains
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, get started, visual studio, high performance, net core, net standard
---

# Introduction to the High Performance package

This package can be installed through NuGet, and it multi-targets .NET Standard 2.0 and .NET Standard 2.1. This means that you can use it from both UWP apps, as well as modern .NET Core 3.0 applications. The API surface is almost identical in both cases, and lots of work has been put into backporting as many features as possible to .NET Standard 2.0 as well. Except for some minor differences, you can expect the same APIs to be available on both target frameworks.

Follow these steps to install the High Performance package:

1. Open an existing project in Visual studio, targeting any of the following:
    - UWP (SDK >= 16299)
    - .NET Standard (>= 2.0)
    - .NET Core (>= 2.1)
    - Any other framework supporting .NET Standard 2.0 and up

2. In Solution Explorer panel, right click on your project name and select **Manage NuGet Packages**. Search for **Microsoft.Toolkit.HighPerformance** and install it.

    ![NuGet Packages](../resources/images/ManageNugetPackages.png "Manage NuGet Packages Image")

3. Add a using directive in your C# files to use the new APIs:

    ```c#
    using Microsoft.Toolkit.HighPerformance;
    ```

4. If you want so see some code samples, you can either read through the other docs pages for the High Performance package, or have a look at the various [unit tests](https://github.com/Microsoft/WindowsCommunityToolkit//blob/master/UnitTests/UnitTests.HighPerformance.Shared/Helpers) for the project.

## When should I use this package?

As the name suggests, the High Performance package contains a set of APIs that are heavily focused on optimization. All the new APIs have been carefully crafted to achieve the best possible performance when using them, either through reduced memory allocation, micro-optimizations at the assembly level, or by structuring the APIs in a way that facilitates writing performance oriented code in general.

This package makes heavy use of APIs such as [`System.Buffers.ArrayPool<T>`](https://docs.microsoft.com/en-us/dotnet/api/system.buffers.arraypool-1), helpers from the [`System.Runtime.CompilerServices.Unsafe`](https://docs.microsoft.com/en-us/dotnet/api/system.runtime.compilerservices.unsafe) and [`System.Runtime.InteropServices.MemoryMarshal`](https://docs.microsoft.com/en-us/dotnet/api/system.runtime.interopservices.memorymarshal) classes, APIs from the [`System.Threading.Tasks.Parallel`](https://docs.microsoft.com/en-us/dotnet/api/system.threading.tasks.parallel) class, and more.

If you are already familiar with these APIs or even if you're just getting started with writing high performance code in C# and want a set of well tested helpers to use in your own projects, have a look at what's included in this package to see how you can use it in your own projects!

