---
title: MapControl for Windows Forms and WPF
author: granitestatehacker
description: This control is a wrapper to enable use of the UWP MapControl class in Windows Forms or WPF.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, MapControl, Windows Forms, WPF
---

# MapControl for Windows Forms and WPF

> [!NOTE]
> This control is currently available as a developer preview. Although we encourage you to try out this control in your own prototype code now, we do not recommend that you use it in production code at this time. This control will continue to mature and stabilize in future toolkit releases.

The **MapControl** class enables you to display a symbolic or photorealistic map in your Windows Forms or WPF desktop application. This control shows rich and customizable map data including road maps, aerial, 3D, views, directions, search results, and traffic. You can also display the user's location, directions, and points of interest.

![MapControl example](../../resources/images/Controls/MapControl.png)

## About MapControl

The WPF version of this control is located in the **Microsoft.Toolkit.Wpf.UI.Controls** namespace. The Windows Forms version is located in the **Microsoft.Toolkit.Forms.UI.Controls** namespace. You can find additional related types (such as enums and event args classes) in the **Microsoft.Toolkit.Win32.UI.Controls.Interop.WinRT** namespace.

Internally, this control wraps the UWP [Windows.UI.Xaml.Controls.Maps.MapControl](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl) class.

## Known Limitations

<!-- TBD  -->

## Syntax
```xaml
<Window x:Class="TestSample.MainWindow" ...
  xmlns:controls="clr-namespace:Microsoft.Toolkit.Wpf.UI.Controls;assembly=Microsoft.Toolkit.Wpf.UI.Controls"
...>


<controls:MapControl x:Name="mapControl" DockPanel.Dock="Top" ZoomInteractionMode="GestureAndControl"
    TiltInteractionMode="GestureAndControl" MapServiceToken="EnterYourAuthenticationKeyHere" />
```

## Properties

| Property | Type | Description |
| -- | -- | -- |
|  |  |

## Methods

| Method | Type | Description |
| -- | -- | -- |
|  |  |

## Events

| Event | Type | Description |
| -- | -- | -- |
|  |  |


## Requirements

|        |        |
|--------|--------|
| Device family | .NET 4.6.2, Windows 10 (introduced v10.0.17709.0) |
| Namespace | Windows Forms: Microsoft.Toolkit.Forms.UI.Controls <br/> WPF: Microsoft.Toolkit.Wpf.UI.Controls |
| NuGet package | Windows Forms: [Microsoft.Toolkit.Forms.UI.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Forms.UI.Controls)  <br/> WPF: [Microsoft.Toolkit.Wpf.UI.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Wpf.UI.Controls) |

## API Source Code

- [MapControl (Windows Forms)](https://github.com/Microsoft/WindowsCommunityToolkit/tree/master/Microsoft.Toolkit.Win32/Microsoft.Toolkit.Forms.UI.Controls/MapControl)
- [MapControl (WPF)](https://github.com/Microsoft/WindowsCommunityToolkit/tree/master/Microsoft.Toolkit.Win32/Microsoft.Toolkit.Wpf.UI.Controls/MapControl)


## Related Topics

- [Windows.UI.Xaml.Controls.Maps.MapControl](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl)
- [Display maps](https://docs.microsoft.com/windows/uwp/maps-and-location/display-maps)
