---
title: Rotator Tile Control
author: nmetulev
description: The RotatorTile Control is an ItemsControl that rotates through a set of items one-by-one. It enables you to show multiple items of data in a live-tile like way.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, RotatorTile Control, xaml control, xaml
---

# RotatorTile XAML Control

The [Rotator Tile Control](/dotnet/api/microsoft.toolkit.uwp.ui.controls.rotatortile) is an ItemsControl that rotates through a set of items one-by-one. It enables you to show multiple items of data in a live-tile like way.

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://Controls?sample=RotatorTile)

## Syntax

```xaml
<Page ...
    xmlns:controls="using:Microsoft.Toolkit.Uwp.UI.Controls"/>

<controls:RotatorTile x:Name="Tile1"
    Background="LightGray"
    Direction="Up"
    Width="400"
    Height="200"
    Margin="20"/>
```

## Example Image

![RotatorTile animation](../resources/images/Controls/RotatorTile.gif)

## Properties

| Property | Type | Description |
| -- | -- | -- |
| CurrentItem | object | Gets or sets the currently selected visible item |
| Direction | [RotateDirection](/dotnet/api/microsoft.toolkit.uwp.ui.controls.rotatortile.rotatedirection) | Gets or sets the direction the tile slides in |
| ExtraRandomDuration | TimeSpan | Gets or sets the extra randomized duration to be added to the `RotationDelay` property. A value between zero and this value in seconds will be added to the `RotationDelay` |
| ItemsSource | object | Gets or sets the ItemsSource |
| ItemTemplate | DataTemplate | Gets or sets the item template |
| RotationDelay | TimeSpan | Gets or sets the duration for tile rotation |

## Sample Project

[RotatorTile Sample Page Source](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.1.0/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/RotatorTile). You can [see this in action](uwpct://Controls?sample=RotatorTile) in the [Windows Community Toolkit Sample App](https://aka.ms/windowstoolkitapp).

## Default Template

[RotatorTile XAML File](https://github.com/CommunityToolkit/WindowsCommunityToolkit/blob/rel/7.1.0/Microsoft.Toolkit.Uwp.UI.Controls.Core/RotatorTile/RotatorTile.xaml) is the XAML template used in the toolkit for the default styling.

## Requirements

| Device family | Universal, 10.0.16299.0 or higher |
| -- | -- |
| Namespace | Microsoft.Toolkit.Uwp.UI.Controls |
| NuGet package | [Microsoft.Toolkit.Uwp.UI.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI.Controls/) |

## API

* [RotatorTile source code](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.1.0/Microsoft.Toolkit.Uwp.UI.Controls.Core/RotatorTile)
