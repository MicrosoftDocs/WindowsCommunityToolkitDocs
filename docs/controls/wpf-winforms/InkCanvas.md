---
title: InkCanvas control for Windows Forms and WPF
author: mcleanbyron
description: This control is a wrapper to enable use of the UWP InkCanvas control in Windows Forms or WPF.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, InkCanvas, Windows Forms, WPF
---

# InkCanvas control for Windows Forms and WPF

The **InkCanvas** control provides a surface for Windows Ink-based user interaction in your Windows Forms or WPF desktop application. This control embeds a panel that receives and displays all pen input as either an ink stroke or an erase stroke. This is one of several wrapped Universal Windows Platform controls that are available for Windows Forms and WPF applications as part of a feature called *XAML Islands*. For more information, see [UWP controls in desktop applications (XAML Islands)](https://docs.microsoft.com/windows/uwp/xaml-platform/xaml-host-controls).

![InkCanvas example](../../resources/images/Controls/InkCanvas.png)

> [!NOTE]
> If you have feedback about this control, create a new issue in the [Microsoft.Toolkit.Win32 repo](https://github.com/windows-toolkit/Microsoft.Toolkit.Win32/issues) and leave your comments there. If you prefer to submit your feedback privately, you can send it to XamlIslandsFeedback@microsoft.com.

## About InkCanvas control

This control wraps an instance of the UWP [Windows.UI.Xaml.Controls.InkCanvas](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas) control. The WPF version of this control is located in the **Microsoft.Toolkit.Wpf.UI.Controls** namespace. The Windows Forms version is located in the **Microsoft.Toolkit.Forms.UI.Controls** namespace. You can find additional related types (such as enums and event args classes) in the **Microsoft.Toolkit.Win32.UI.Controls.Interop.WinRT** namespace.

For a walkthrough that demonstrates how to host an **InkCanvas** wrapped control in a WPF app, see [Host a standard UWP control in a WPF app using XAML Islands](https://docs.microsoft.com/windows/apps/desktop/modernize/host-standard-control-with-xaml-islands).

## Requirements

Before you can use this control, you must follow [these instructions](https://docs.microsoft.com/windows/uwp/xaml-platform/xaml-host-controls#requirements) to configure your project to support XAML Islands.

## Requirements

This control is currently available as a developer preview for Windows 10, version 1903, and later. Although we encourage you to try out this control in your own prototype code now, we do not recommend that you use it in production code at this time. For more information, see [XAML Islands feature roadmap](https://docs.microsoft.com/windows/uwp/xaml-platform/xaml-host-controls#xaml-islands-feature-roadmap).

Before you can use this control, you must follow [these instructions](https://docs.microsoft.com/windows/uwp/xaml-platform/xaml-host-controls#requirements) to configure your project to support XAML Islands.

## Known issues and limitations

This control, like the UWP **Windows.UI.Xaml.Controls.InkCanvas** control, provides no interaction without an associated [InkToolbar](InkToolbar.md) with the interaction mode set. You'll also find it may not show ink properly while running on a device that uses the Windows 10 dark theme.

See also our list of [known issues](https://github.com/windows-toolkit/Microsoft.Toolkit.Win32/issues) for WPF and Windows Forms controls in the Windows Community Toolkit repo.

## Syntax
```xaml
<Window x:Class="TestSample.MainWindow" ...
  xmlns:controls="clr-namespace:Microsoft.Toolkit.Wpf.UI.Controls;assembly=Microsoft.Toolkit.Wpf.UI.Controls"
...>


<controls:InkCanvas x:Name="inkCanvas" DockPanel.Dock="Top" Loaded="inkCanvas_Loaded"/>
```

## Properties

| Property | Type | Description |
| -- | -- | -- |
| InkPresenter | InkPresenter | Wraps the [InkPresenter](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.inkcanvas.inkpresenter) property of the wrapped UWP [Windows.UI.Xaml.Controls.InkToolbar](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkToolbar) object. |


## Requirements

|        |        |
|--------|--------|
| Device family | .NET 4.6.2, Windows 10 (introduced v10.0.17709.0) |
| Namespace | Windows Forms: Microsoft.Toolkit.Forms.UI.Controls <br/> WPF: Microsoft.Toolkit.Wpf.UI.Controls |
| NuGet package | Windows Forms: [Microsoft.Toolkit.Forms.UI.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Forms.UI.Controls)  <br/> WPF: [Microsoft.Toolkit.Wpf.UI.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Wpf.UI.Controls) |

## API source code

- [InkCanvas (Windows Forms)](https://github.com/windows-toolkit/Microsoft.Toolkit.Win32/tree/master/Microsoft.Toolkit.Forms.UI.Controls/InkCanvas)
- [InkCanvas (WPF)](https://github.com/windows-toolkit/Microsoft.Toolkit.Win32/tree/master/Microsoft.Toolkit.Wpf.UI.Controls/InkCanvas)


## Related topics

- [InkCanvas (UWP)](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.InkCanvas)
- [Pen and Windows Ink](https://docs.microsoft.com/windows/uwp/design/input/pen-and-stylus-interactions)
