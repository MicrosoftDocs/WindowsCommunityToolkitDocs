---
title: SwapChainPanel control for Windows Forms and WPF
author: mcleanbyron
description: This control is a wrapper to enable use of the UWP SwapChainPanel control in Windows Forms or WPF.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, SwapChainPanel, Windows Forms, WPF
---

# SwapChainPanel control for Windows Forms and WPF

> [!NOTE]
> This control is currently available as a developer preview. Although we encourage you to try out this control in your own prototype code now, we do not recommend that you use it in production code at this time. This control will continue to mature and stabilize in future toolkit releases.

The **SwapChainPanel** control provides a hosting surface in your Windows Forms or WPF desktop application where you can manage Microsoft DirectX swap chains to render content in a XAML-based UI.

<!-- Need an image... do we want one from somewhere?
![SwapChainPanel example](../../resources/images/Controls/SwapChainPanel.png)
-->

## About SwapChainPanel control

The WPF version of this control is located in the **Microsoft.Toolkit.Wpf.UI.Controls** namespace. The Windows Forms version is located in the **Microsoft.Toolkit.Forms.UI.Controls** namespace. You can find additional related types (such as enums and event args classes) in the **Microsoft.Toolkit.Win32.UI.Controls.Interop.WinRT** namespace.

This control wraps an internal instance of the UWP [Windows.UI.Xaml.Controls.SwapChainPanel](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.SwapChainPanel) control.

## Known issues and limitations

See our list of [known issues](https://github.com/windows-toolkit/WindowsCommunityToolkit/issues?utf8=%E2%9C%93&q=is:issue+is:open+label:XamlIslands+label:bug).

## Syntax

```xaml
<Window x:Class="TestSample.MainWindow" ...
  xmlns:controls="clr-namespace:Microsoft.Toolkit.Wpf.UI.Controls;assembly=Microsoft.Toolkit.Wpf.UI.Controls"
...>


<controls:SwapChainPanel x:Name="swapChainPanel" DockPanel.Dock="Top" />
```

## Properties

| Property | Type | Description |
| -- | -- | -- |
| CompositionScaleX | float  | Wraps the [CompositionScaleX](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.swapchainpanel.compositionscalex) property of the internal UWP [SwapChainPanel](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.SwapChainPanel) object. |
| CompositionScaleY | float  |  Wraps the [CompositionScaleY](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.swapchainpanel.compositionscaley) property of the internal UWP [SwapChainPanel](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.SwapChainPanel) object. |

## Methods

| Method | Description |
| -- | -- |
| CreateCoreIndependentInputSource | Wraps the [CreateCoreIndependentInputSource](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.swapchainpanel.createcoreindependentinputsource) method of the internal UWP [SwapChainPanel](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.SwapChainPanel) object. |

## Events

| Event | Description |
| -- | -- |
| CompositionScaleChanged  | Wraps the [CompositionScaleChanged](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.swapchainpanel.compositionscalechanged) event of the internal UWP [SwapChainPanel](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.SwapChainPanel) object. |


## Requirements

|        |        |
|--------|--------|
| Device family | .NET 4.6.2, Windows 10 (introduced v10.0.17709.0) |
| Namespace | Windows Forms: Microsoft.Toolkit.Forms.UI.Controls <br/> WPF: Microsoft.Toolkit.Wpf.UI.Controls |
| NuGet package | Windows Forms: [Microsoft.Toolkit.Forms.UI.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Forms.UI.Controls)  <br/> WPF: [Microsoft.Toolkit.Wpf.UI.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Wpf.UI.Controls) |

## API source code

- [SwapChainPanel (Windows Forms)](https://github.com/Microsoft/WindowsCommunityToolkit/tree/master/Microsoft.Toolkit.Win32/Microsoft.Toolkit.Forms.UI.Controls/SwapChainPanel)
- [SwapChainPanel (WPF)](https://github.com/Microsoft/WindowsCommunityToolkit/tree/master/Microsoft.Toolkit.Win32/Microsoft.Toolkit.Wpf.UI.Controls/SwapChainPanel)


## Related topics

- [SwapChainPanel (UWP)](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.SwapChainPanel)
- [SwapChainPanel and gaming](https://docs.microsoft.com/windows/uwp/gaming/directx-and-xaml-interop#swapchainpanel-and-gaming)
