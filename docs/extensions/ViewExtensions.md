---
title: View extensions
author: nmetulev
description: The ApplicationViewExtensions and TitleBarExtensions types provide a declarative way of setting ApplicationView, CoreApplicationView and ApplicationViewTitleBar properties from XAML.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, ViewExtensions, ApplicationViewExtensions, StatusBarExtensions, TitleBarExtensions, statusbar, titlebar, xaml
---

# View extensions

The [`ApplicationViewExtensions`](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.uwp.ui.applicationviewextensions) and [`TitleBarExtensions`](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.uwp.ui.titlebarextensions) provide a declarative way of setting [`ApplicationView`](https://docs.microsoft.com/uwp/api/windows.ui.viewmanagement.applicationview), [`CoreApplicationView`](https://docs.microsoft.com/uwp/api/windows.applicationmodel.core.coreapplicationview) and [`ApplicationViewTitleBar`](https://docs.microsoft.com/uwp/api/windows.ui.viewmanagement.applicationviewtitlebar) properties from XAML.

> **Platform APIs:** [`ApplicationViewExtensions`](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.uwp.ui.applicationviewextensions), [`TitleBarExtensions`](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.uwp.ui.titlebarextensions)

## Example

These attached properties all target a [`Page`](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.page) element, so they can be used directly from XAML when declaring a control of this type in an application:

```xml
<Page x:Class="Microsoft.Toolkit.Uwp.SampleApp.SamplePages.ViewExtensionsPage"
      xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
      xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
      xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
      xmlns:local="using:Microsoft.Toolkit.Uwp.SampleApp.SamplePages"
      xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
      xmlns:ui="using:Microsoft.Toolkit.Uwp.UI"
      ui:ApplicationViewExtensions.Title="View Extensions"
      ui:ApplicationViewExtensions.ExtendViewIntoTitleBar="True"
      ui:TitleBarExtensions.BackgroundColor="Gray"
      ui:TitleBarExtensions.ButtonBackgroundColor="Orange"
      ui:TitleBarExtensions.ButtonForegroundColor="Black"
      ui:TitleBarExtensions.ButtonHoverBackgroundColor="DarkOrange"
      ui:TitleBarExtensions.ButtonHoverForegroundColor="Gray"
      ui:TitleBarExtensions.ButtonPressedForegroundColor="DarkGray"
      mc:Ignorable="d">

    <!-- Page content here -->
</Page>
```

## Examples

You can find more examples in the [unit tests](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/master/UnitTests).