---
title: Windows Community Toolkit NuGet Packages
author: nmetulev
description: The Windows Community Toolkit is updated regularly with new controls, services, APIs, and more importantly, bug fixes. Make sure to regularly update your nuget packages
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, nuget, visual studio
---

# Community Toolkit NuGet Packages

NuGet is a standard package manager for .Net applications that is built into Visual Studio. From your open solution choose the *Tools* menu, *NuGet Package Manager*, *Manage NuGet packages for solution...* to open the UI.  Enter one of the package names below to search for it online.

| NuGet Package Name | Description |
| --- | --- |
| CommunityToolkit.Common | .NET Standard NuGet package containing common code |
| CommunityToolkit.Diagnostics | .NET Standard code helpers |
| CommunityToolkit.HighPerformance | .NET Standard and .NET Core NuGet package with performance oriented helpers, extensions, etc. |
| CommunityToolkit.Mvvm | [MVVM Toolkit](/dotnet/communitytoolkit/mvvm/) a modern, fast, and modular MVVM library for .NET Standard, platform and runtime agnostic |
| CommunityToolkit.Maui | [MAUI Community Toolkit](/dotnet/communitytoolkit/maui) for .NET MAUI |
| CommunityToolkit.WinUI.* | [WindowsAppSDK](/windows/apps/windows-app-sdk)/[WinUI 3](/windows/apps/winui/winui3) versions of the toolkit packages below. |
| Microsoft.Toolkit.Uwp | Includes code only helpers such as Colors conversion tool, Storage file handling, a Stream helper class, etc. |
| Microsoft.Toolkit.Uwp.UI | UI Packages - XAML converters, Visual tree extensions, and other extensions and helpers for your XAML UI |
| Microsoft.Toolkit.Uwp.UI.Animations | Animations and Composition behaviors such as Blur, Fade, Rotate, etc. |
| Microsoft.Toolkit.Uwp.UI.Behaviors | Extra behaviors built on top of the [XAML Behaviors](https://github.com/microsoft/XamlBehaviors/wiki) library. |
| Microsoft.Toolkit.Uwp.UI.Controls | Wrapping package of all controls, for best disk footprint, use individual packages. |
| Microsoft.Toolkit.Uwp.UI.Controls.Core | Common controls useful for a variety of applications. |
| Microsoft.Toolkit.Uwp.UI.Controls.DataGrid | XAML DataGrid control |
| Microsoft.Toolkit.Uwp.UI.Controls.Input | Controls related to retrieving information or values. |
| Microsoft.Toolkit.Uwp.UI.Controls.Layout | Controls for various application layout scenarios. |
| Microsoft.Toolkit.Uwp.UI.Controls.Markdown | Markdown renderer control. |
| Microsoft.Toolkit.Uwp.UI.Controls.Media | Controls that depend on Win2D. |
| Microsoft.Toolkit.Uwp.UI.Controls.Primitives | Panels and simple layout controls without stlyes |
| Microsoft.Toolkit.Uwp.UI.Lottie | Library for rendering Adobe AfterEffects animations natively in Windows apps |
| Microsoft.Toolkit.Uwp.UI.Media | Brushes, Win2D/Composition effects, and helpers to create visual effects  |
| Microsoft.Toolkit.Uwp.Connectivity | API helpers such as BluetoothLEHelper and Networking |
| Microsoft.Toolkit.Uwp.DeveloperTools | XAML user controls and services to help developer building their app |

## Search in Visual Studio

Searching in Visual Studio package manager you should see a list similar to the one below (version numbers may be different, but names should be the same).

![NuGet packages](resources/images/NugetPackages.png "Nuget Packages")

## Update NuGet Packages

The Windows Community Toolkit is updated regularly with new controls, services, APIs, and more importantly, bug fixes. To make sure you are on the latest version, open your project in Visual Studio, choose the **Tools** menu, select **NuGet Package Manager** -> **Manage NuGet Packages for Solution...** and select the *Updates* tab. Select the package you want to update and click Install to update to the latest version.

## Getting Started

Read the [getting Started with the Windows Community Toolkit](getting-started.md) for more instructions on using these NuGet Packages in your own projects.

## Windows 10 Store App

Want to see the controls and animations in action before jumping into the code?  We have published the [Windows Community Toolkit Sample App](https://aka.ms/windowstoolkitapp) to the Windows 10 store.  Download the app and play with the controls live to see what they do before ever writing a line of code.

## GitHub Repository

Visit the [Windows Community Toolkit Github Repository](https://aka.ms/uwptoolkit) to see the current source code, what is coming next, and to clone the repository.  Community contributions are welcome!
