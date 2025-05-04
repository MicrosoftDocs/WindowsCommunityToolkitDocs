---
title: GeometryMaskSurfaceBrush
author: ratishphilip
description: A composition brush that paints an area by creating a mask defined by the provided geometry.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, brush, Win2D, composition
---

# GeometryMaskSurfaceBrush

The [GeometryMaskSurfaceBrush](/dotnet/api/microsoft.toolkit.uwp.ui.media.geometrymasksurfacebrush) is a [Brush](/uwp/api/windows.ui.xaml.media.brush) that uses a [CanvasCoreGeometry](/dotnet/api/microsoft.toolkit.uwp.ui.media.geometry.canvascoregeometry) to paint an area.

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://Brushes?sample=GeometryMaskSurfaceBrush)

## Syntax

```xaml
<Grid>
    <Grid.Background>
        <media:GeometryMaskSurfaceBrush BlurRadius="0"
                                        OffsetX="0"
                                        OffsetY="0"
                                        SurfaceHeight="600"
                                        SurfaceWidth="899.25">
            <media:GeometryMaskSurfaceBrush.Target>
                <media:ImageSurfaceBrush Source="ms-appx:///Assets/Photos/SpeedTripleAtristsPoint.jpg"
                                            SurfaceHeight="600"
                                            SurfaceWidth="899.25" />
            </media:GeometryMaskSurfaceBrush.Target>
            <media:GeometryMaskSurfaceBrush.Mask>
                <geometry:CanvasRoundedRectangleGeometry Width="200"
                                                            Height="200"
                                                            RadiusX="30"
                                                            RadiusY="30" />
            </media:GeometryMaskSurfaceBrush.Mask>
        </media:GeometryMaskSurfaceBrush>
    </Grid.Background>
</Grid>
```

## Example Image

![Geometry Mask Surface brush](../resources/images/Brushes/GeometryMaskSurfaceBrush.jpg 'Geometry Mask Surface Brush')

## Properties

| Property   | Type                                                                                         | Description                                                                                            |
| ---------- | -------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| Target     | [RenderCanvasBrushBase](/dotnet/api/microsoft.toolkit.uwp.ui.media.rendercanvasbrushbase)    | The Render Surface Brush on which the mask is applied.                                                 |
| Mask       | [CanvasCoreGeometry](/dotnet/api/microsoft.toolkit.uwp.ui.media.geometry.canvascoregeometry) | The geometry that is used to create the mask.                                                          |
| OffsetX    | double                                                                                       | The offset on the x-axis from the top left corner of the Brush Surface where the Geometry is rendered. |
| OffsetY    | double                                                                                       | The offset on the y-axis from the top left corner of the Brush Surface where the Geometry is rendered. |
| BlurRadius | double                                                                                       | The radius of the Gaussian blur to be applied on the mask.                                             |

## Sample Project

[GeometryMaskSurfaceBrush sample page Source](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.1.0/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/GeometryMaskSurfaceBrush). You can [see this in action](uwpct://Brushes?sample=GeometryMaskSurfaceBrush) in the [Windows Community Toolkit Sample App](https://aka.ms/windowstoolkitapp).

## Requirements

| Device family | Universal, 10.0.17134.0 or higher                                                                |
| ------------- | ------------------------------------------------------------------------------------------------ |
| Namespace     | Microsoft.Toolkit.Uwp.UI.Media                                                                   |
| NuGet package | [Microsoft.Toolkit.Uwp.UI.Media](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI.Media/) |

## API

- [GeometryMaskSurfaceBrush source code](https://github.com/windows-toolkit/WindowsCommunityToolkit/blob/rel/7.0.0/Microsoft.Toolkit.Uwp.UI.Media/Brushes/GeometryMaskSurfaceBrush.cs)

## Related Topics

- [Render Surfaces](RenderSurfaces.md)
- [XamlCompositionBrushBase Examples](/uwp/api/windows.ui.xaml.media.xamlcompositionbrushbase#examples)
