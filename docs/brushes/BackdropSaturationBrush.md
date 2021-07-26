---
title: BackdropSaturationBrush
author: michael-hawker
description: The BackdropSaturationBrush is a Brush that applies a Saturation effect to whatever is behind it in the application.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, brush, backdrop, saturation
---

# BackdropSaturationBrush

The [BackdropSaturationBrush](/dotnet/api/microsoft.toolkit.uwp.ui.media.backdropsaturationbrush) is a [Brush](/uwp/api/windows.ui.xaml.media.brush) that blurs whatever is behind it in the application.

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://Brushes?sample=BackdropSaturationBrush)

## Syntax

```xaml
<Border BorderBrush="Black" BorderThickness="1" VerticalAlignment="Center" HorizontalAlignment="Center" Width="400" Height="400">
  <Border.Background>
    <media:BackdropSaturationBrush Saturation="0.25" />
  </Border.Background>
</Border>
```

## Example Image

![Backdrop Saturation](../resources/images/Brushes/BackdropSaturation.jpg "Backdrop Saturation")

## Properties

| Property | Type | Description |
| -- | -- | -- |
| Saturation | double | The `Saturation` property specifies a double value for the amount of Saturation to apply from 0.0 - 1.0.  Zero being monochrome, and one being fully saturated.  The default is 0.5. |

## Sample Project

[BackdropSaturationBrush sample page Source](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.0.0/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/BackdropSaturationBrush). You can [see this in action](uwpct://Brushes?sample=BackdropSaturationBrush) in the [Windows Community Toolkit Sample App](https://aka.ms/windowstoolkitapp).

## Requirements

| Device family | Universal, 10.0.16299.0 or higher |
| --- | --- |
| Namespace | Microsoft.Toolkit.Uwp.UI.Media |
| NuGet package | [Microsoft.Toolkit.Uwp.UI.Media](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI.Media/)

## API

* [BackdropSaturationBrush source code](https://github.com/windows-toolkit/WindowsCommunityToolkit/blob/rel/7.0.0/Microsoft.Toolkit.Uwp.UI.Media/Brushes/BackdropSaturationBrush.cs)

## Related Topics

* [Win2D SaturationEffect reference](https://microsoft.github.io/Win2D/html/T_Microsoft_Graphics_Canvas_Effects_SaturationEffect.htm)
