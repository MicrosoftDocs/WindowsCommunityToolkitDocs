---
title: ImageSurfaceBrush
author: ratishphilip
description: A composition brush that paints an area using the provided image.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, brush, Win2D, composition
---

# ImageSurfaceBrush

The [ImageSurfaceBrush](/dotnet/api/microsoft.toolkit.uwp.ui.media.imagesurfacebrush) is a [Brush](/uwp/api/windows.ui.xaml.media.brush) that uses a image to paint an area.

> [!div class="nextstepaction"] > [Try it in the sample app](uwpct://Brushes?sample=ImageSurfaceBrush)

## Syntax

```xaml
<Grid>
    <Grid.Background>
        <media:ImageSurfaceBrush Source="ms-appx:///Assets/Photos/SpeedTripleAtristsPoint.jpg"
                                  SurfaceHeight="500"
                                  SurfaceWidth="900">
            <media:ImageSurfaceBrush.ImageOptions>
                <media:ImageSurfaceOptions x:Name="ImageOptions"
                                            HorizontalAlignment="Center"
                                            VerticalAlignment="Center"
                                            Stretch="None" />
            </media:ImageSurfaceBrush.ImageOptions>
        </media:ImageSurfaceBrush>
    </Grid.Background>
</Grid>
```

## Example Image

![Image Surface  brush](../resources/images/Brushes/ImageSurfaceBrush.jpg 'Image Surface Brush')

## Properties

| Property     | Type                                                                                  | Description                                                                                                |
| ------------ | ------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| Background   | Color                                                                                 | The color that is rendered in the transparent areas of the Image. The default value is Colors.Transparent. |
| Source       | object                                                                                | The object representing the image source.                                                                  |
| ImageOptions | [ImageSurfaceOptions](/dotnet/api/microsoft.toolkit.uwp.ui.media.imagesurfaceoptions) | Additional options to configure the image used to create the brush.                                        |

## Code behind support

## Sample Project

[ImageSurfaceBrush sample page Source](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.1.0/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/ImageSurfaceBrush). You can [see this in action](uwpct://Brushes?sample=ImageSurfaceBrush) in the [Windows Community Toolkit Sample App](https://aka.ms/windowstoolkitapp).

## Requirements

| Device family | Universal, 10.0.17134.0 or higher                                                                |
| ------------- | ------------------------------------------------------------------------------------------------ |
| Namespace     | Microsoft.Toolkit.Uwp.UI.Media                                                                   |
| NuGet package | [Microsoft.Toolkit.Uwp.UI.Media](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI.Media/) |

## API

- [ImageSurfaceBrush source code](https://github.com/windows-toolkit/WindowsCommunityToolkit/blob/rel/7.0.0/Microsoft.Toolkit.Uwp.UI.Media/Brushes/ImageSurfaceBrush.cs)

## Related Topics

- [Render Surfaces](RenderSurfaces.md)
- [XamlCompositionBrushBase Examples](/uwp/api/windows.ui.xaml.media.xamlcompositionbrushbase#examples)
