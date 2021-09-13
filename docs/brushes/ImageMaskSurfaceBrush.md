---
title: ImageMaskSurfaceBrush
author: ratishphilip
description: A composition brush that paints an area by creating a mask defined by the provided geometry.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, brush, Win2D, composition
---

# ImageMaskSurfaceBrush

The [ImageMaskSurfaceBrush](/dotnet/api/microsoft.toolkit.uwp.ui.media.imagemasksurfacebrush) is a [Brush](/uwp/api/windows.ui.xaml.media.brush) that uses an Image to create a mask to be applied on a [RenderSurfaceBrushBase](/dotnet/api/microsoft.toolkit.uwp.ui.media.rendersurfacebrushbase) derivative.

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://Brushes?sample=ImageMaskSurfaceBrush)

## Syntax

```xaml
<Grid x:Name="MaskGrid"
        Grid.Row="1">
    <Grid.Background>
        <media:ImageSurfaceBrush x:Name="MaskImageBrush"
                                    Source="ms-appx:///SamplePages/ImageMaskSurfaceBrush/MaskImage1.png"
                                    SurfaceHeight="600"
                                    SurfaceWidth="600">
            <media:ImageSurfaceBrush.ImageOptions>
                <media:ImageSurfaceOptions HorizontalAlignment="Center"
                                            VerticalAlignment="Center"
                                            Stretch="Uniform" />
            </media:ImageSurfaceBrush.ImageOptions>
        </media:ImageSurfaceBrush>
    </Grid.Background>
</Grid>
<Grid x:Name="TargetGrid"
        Grid.Row="1"
        Grid.Column="1">
    <Grid.Background>
        <media:ImageSurfaceBrush x:Name="TargetImageBrush"
                                    Source="ms-appx:///Assets/Photos/PaintedHillsPathway.jpg"
                                    SurfaceHeight="600"
                                    SurfaceWidth="600">
            <media:ImageSurfaceBrush.ImageOptions>
                <media:ImageSurfaceOptions HorizontalAlignment="Center"
                                            VerticalAlignment="Center"
                                            Stretch="Uniform" />
            </media:ImageSurfaceBrush.ImageOptions>
        </media:ImageSurfaceBrush>
    </Grid.Background>
</Grid>
<Grid Grid.Row="2"
        Grid.ColumnSpan="2">
    <Grid.Background>
        <media:ImageMaskSurfaceBrush x:Name="ImageMaskBrush"
                                        Padding="30"
                                        Mask="{Binding ElementName=MaskImageBrush, Path=Source}"
                                        SurfaceHeight="600"
                                        SurfaceWidth="600">
            <media:ImageMaskSurfaceBrush.ImageOptions>
                <media:ImageSurfaceOptions x:Name="MaskImageOptions"
                                            BlurRadius="5" />
            </media:ImageMaskSurfaceBrush.ImageOptions>
            <media:ImageMaskSurfaceBrush.Target>
                <media:ImageSurfaceBrush x:Name="MaskTargetImageBrush"
                                            Source="{Binding ElementName=TargetImageBrush, Path=Source}"
                                            SurfaceHeight="800"
                                            SurfaceWidth="800" />
            </media:ImageMaskSurfaceBrush.Target>
        </media:ImageMaskSurfaceBrush>
    </Grid.Background>
</Grid>
```

## Example Image

![Image Mask Surface brush](../resources/images/Brushes/ImageMaskSurfaceBrush.jpg 'Image Mask Surface Brush')

## Properties

| Property     | Type                                                                                      | Description                                                                                                                                                    |
| ------------ | ----------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Target       | [RenderCanvasBrushBase](/dotnet/api/microsoft.toolkit.uwp.ui.media.rendercanvasbrushbase) | The Render Surface Brush on which the mask is applied.                                                                                                         |
| Mask         | [RenderCanvasBrushBase](/dotnet/api/microsoft.toolkit.uwp.ui.media.rendercanvasbrushbase) | URI of the image (in string format) which is used to create the mask.                                                                                          |
| ImageOptions | [ImageSurfaceOptions](/dotnet/api/microsoft.toolkit.uwp.ui.media.imagesurfaceoptions)     | Additional options to configure the image used to create the mask for the brush.                                                                               |
| Padding      | Thickness                                                                                 | The padding between the outer bounds of the brush and the bounds of the area where the mask, created from the loaded image's alpha values, should be rendered. |

## Sample Project

[ImageMaskSurfaceBrush sample page Source](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.1.0/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/ImageMaskSurfaceBrush). You can [see this in action](uwpct://Brushes?sample=ImageMaskSurfaceBrush) in the [Windows Community Toolkit Sample App](https://aka.ms/windowstoolkitapp).

## Requirements

| Device family | Universal, 10.0.17134.0 or higher                                                                |
| ------------- | ------------------------------------------------------------------------------------------------ |
| Namespace     | Microsoft.Toolkit.Uwp.UI.Media                                                                   |
| NuGet package | [Microsoft.Toolkit.Uwp.UI.Media](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI.Media/) |

## API

- [ImageMaskSurfaceBrush source code](https://github.com/windows-toolkit/WindowsCommunityToolkit/blob/rel/7.0.0/Microsoft.Toolkit.Uwp.UI.Media/Brushes/ImageMaskSurfaceBrush.cs)

## Related Topics

- [Render Surfaces](RenderSurfaces.md)
- [XamlCompositionBrushBase Examples](/uwp/api/windows.ui.xaml.media.xamlcompositionbrushbase#examples)
