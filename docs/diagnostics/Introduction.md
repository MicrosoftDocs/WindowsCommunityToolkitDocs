---
title: Introduction to the Diagnostics package
author: Sergio0694
description: An overview of how to get started with the Diagnostics package and to the APIs it contains
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, get started, visual studio, diagnostics, exceptions, contract, net core, net standard
---

# Introduction to the Diagnostics package

The Diagnostics package contains APIs to efficiently validate method parameters and to throw exceptions in faulting code paths. It is meant to be used to help simplify all argument checks and to make them more expressive and easier to read, while at the same time improving codegen quality and performance.

This package can be installed through NuGet, and it has the following multi-targets:

- .NET Standard 1.4
- .NET Standard 2.0
- .NET Standard 2.1
- .NET 5

This means the package can be used on any available runtime (including .NET Framework, .NET Core, UWP, Unity, Xamarin, Uno, Blazor, etc.). The API surface is almost identical in all cases, while the internal implementation can be optimized when newer APIs are available. The Diagnostics package as a whole is meant to be self-contained and extremely small in scope and binary size.

Follow these steps to install the Diagnostics package:

1. Open an existing project in Visual studio, targeting any of the following:
    - UWP (>= 10.0)
    - .NET Standard (>= 1.4)
    - .NET Core (>= 1.0)
    - Any other framework supporting .NET Standard 1.4 and up

2. In Solution Explorer panel, right click on your project name and select **Manage NuGet Packages**. Search for **Microsoft.Toolkit.HighPerformance** and install it.

    ![NuGet Packages](../resources/images/ManageNugetPackages.png "Manage NuGet Packages Image")

3. Add a using directive in your C# files to use the new APIs:

    ```csharp
    using Microsoft.Toolkit.Diagnostics;
    ```

4. If you want so see some code samples, you can either read through the other docs pages for the Diagnostics package, or have a look at the various [unit tests](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.0.0/UnitTests/UnitTests.Shared/Diagnostics) for the project.
