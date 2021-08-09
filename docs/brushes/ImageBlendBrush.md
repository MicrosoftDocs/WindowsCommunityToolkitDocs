---
title: ImageBlendBrush
author: michael-hawker
description: The ImageBlendBrush is a Brush that inverts whatever is behind it in the application.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, brush, backdrop, image, blend
---

# ImageBlendBrush

The [ImageBlendBrush](/dotnet/api/microsoft.toolkit.uwp.ui.media.imageblendbrush) is a [Brush](/uwp/api/windows.ui.xaml.media.brush) that blends the provided image with whatever is behind it in the application with the provided blend mode.

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://Brushes?sample=ImageBlendBrush)

## Syntax

```xaml
<Border Grid.Column="0">
  <Border.Background>
    <media:ImageBlendBrush
      Source="/SamplePages/DropShadowPanel/Unicorn.png"
      Stretch="None"
      Mode="ColorBurn"/>
  </Border.Background>
</Border>
```

## Example Image

![Image Blend](../resources/images/Brushes/ImageBlend.jpg "Image Blend")

## Properties

| Property | Type | Description |
| -- | -- | -- |
| Source | Windows.UI.Xaml.Media.ImageSource | The `ImageSource` property specifies which image to use for the effect.  It is assumed it will resolve to a [BitmapImage](/uwp/api/windows.ui.xaml.media.imaging.bitmapimage). |
| Stretch | Windows.UI.Xaml.Media.Stretch | The `Stretch` property specifies how the image should stretch to its container.  Requires 10.0.16299 or higher for modes other than None (default). |
| Mode | [ImageBlendMode](/dotnet/api/microsoft.toolkit.uwp.ui.media.imageblendmode) | The `ImageBlendMode` property specifies how the image should be blended with the backdrop.  See the [BlendEffectMode](https://microsoft.github.io/Win2D/html/T_Microsoft_Graphics_Canvas_Effects_BlendEffectMode.htm) reference. |

## Sample Project

[ImageBlendBrush sample page Source](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.0.0/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/ImageBlendBrush). You can [see this in action](uwpct://Brushes?sample=ImageBlendBrush) in the [Windows Community Toolkit Sample App](https://aka.ms/windowstoolkitapp).

## Requirements

| Device family | Universal, 10.0.16299.0 or higher |
| --- | --- |
| Namespace | Microsoft.Toolkit.Uwp.UI.Media |
| NuGet package | [Microsoft.Toolkit.Uwp.UI.Media](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI.Media/)

## API

* [ImageBlendBrush source code](https://github.com/windows-toolkit/WindowsCommunityToolkit/blob/rel/7.0.0/Microsoft.Toolkit.Uwp.UI.Media/Brushes/ImageBlendBrush.cs)

## Related Topics

* [BitmapImage](/uwp/api/windows.ui.xaml.media.imaging.bitmapimage)
* [Win2D BlendEffect reference](https://microsoft.github.io/Win2D/html/T_Microsoft_Graphics_Canvas_Effects_BlendEffect.htm)
* [BlendEffectMode reference](https://microsoft.github.io/Win2D/html/T_Microsoft_Graphics_Canvas_Effects_BlendEffectMode.htm)
* [Working with Brushes and Content – XAML and Visual Layer Interop, Part One](https://blogs.windows.com/buildingapps/2017/07/18/working-brushes-content-xaml-visual-layer-interop-part-one/#c57zf3bW4ylLlSvJ.97)
