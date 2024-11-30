---
title: BackdropBlurBrush
author: michael-hawker
description: The BackdropBlurBrush is a Brush that blurs whatever is behind it in the application.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, brush, backdrop, blur
---

# BackdropBlurBrush

The [BackdropBlurBrush](/dotnet/api/microsoft.toolkit.uwp.ui.media.backdropblurbrush) is a [Brush](/uwp/api/windows.ui.xaml.media.brush) that blurs whatever is behind it in the application.

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://Brushes?sample=BackdropBlurBrush)

## Syntax

```xaml
<Border BorderBrush="Black" BorderThickness="1" VerticalAlignment="Center" HorizontalAlignment="Center" Width="400" Height="400">
  <Border.Background>
    <media:BackdropBlurBrush Amount="3.0" />
  </Border.Background>
</Border>
```

## Example Image

![Backdrop Blur](../resources/images/Brushes/BackdropBlur.jpg "Backdrop Blur")

## Properties

| Property | Type | Description |
| -- | -- | -- |
| Amount | double | The `Amount` property specifies a double value for the amount of Gaussian blur to apply. |

## Sample Project

[BackdropBlurBrush sample page Source](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.1.0/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/BackdropBlurBrush). You can [see this in action](uwpct://Brushes?sample=BackdropBlurBrush) in the [Windows Community Toolkit Sample App](https://aka.ms/windowstoolkitapp).

## Requirements

| Device family | Universal, 10.0.16299.0 or higher |
| --- | --- |
| Namespace | Microsoft.Toolkit.Uwp.UI.Media |
| NuGet package | [Microsoft.Toolkit.Uwp.UI.Media](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI.Media/) |

## API

* [BackdropBlurBrush source code](https://github.com/windows-toolkit/WindowsCommunityToolkit/blob/rel/7.1.0/Microsoft.Toolkit.Uwp.UI.Media/Brushes/BackdropBlurBrush.cs)

## Related Topics

* [Win2D GaussianBlurEffect reference](https://microsoft.github.io/Win2D/WinUI2/html/T_Microsoft_Graphics_Canvas_Effects_GaussianBlurEffect.htm)
* [XamlCompositionBrushBase Examples](/uwp/api/windows.ui.xaml.media.xamlcompositionbrushbase#examples)
