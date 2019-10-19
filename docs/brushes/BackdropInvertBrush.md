---
title: BackdropInvertBrush
author: michael-hawker
description: The BackdropInvertBrush is a Brush that inverts whatever is behind it in the application.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, brush, backdrop, invert
---

# BackdropInvertBrush

The [BackdropInvertBrush](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.uwp.ui.media.backdropinvertbrush) is a [Brush](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.brush) that inverts whatever is behind it in the application.

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://Brushes?sample=BackdropInvertBrush)

## Syntax

```xaml
<Border BorderBrush="Black" BorderThickness="1" VerticalAlignment="Center" HorizontalAlignment="Center" Width="400" Height="400">
  <Border.Background>
    <media:BackdropInvertBrush />
  </Border.Background>
</Border>
```

## Example Image

![Backdrop Invert](../resources/images/Brushes/BackdropInvert.jpg "Backdrop Invert")

## Sample Project

[BackdropInvertBrush sample page Source](https://github.com/Microsoft/WindowsCommunityToolkit//tree/master/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/BackdropInvertBrush). You can [see this in action](uwpct://Brushes?sample=BackdropInvertBrush) in the [Windows Community Toolkit Sample App](http://aka.ms/uwptoolkitapp).

## Requirements

| Device family | Universal, 10.0.16299.0 or higher |
| --- | --- |
| Namespace | Microsoft.Toolkit.Uwp.UI.Media |
| NuGet package | [Microsoft.Toolkit.Uwp.UI](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI/) |

## API

* [BackdropInvertBrush source code](https://github.com/Microsoft/WindowsCommunityToolkit//blob/master/Microsoft.Toolkit.Uwp.UI/Media/BackdropInvertBrush.cs)

## Related Topics

* [Win2D InvertEffect reference](http://microsoft.github.io/Win2D/html/T_Microsoft_Graphics_Canvas_Effects_InvertEffect.htm)
* [Working with Brushes and Content – XAML and Visual Layer Interop, Part One](https://blogs.windows.com/buildingapps/2017/07/18/working-brushes-content-xaml-visual-layer-interop-part-one/#c57zf3bW4ylLlSvJ.97)
