---
title: GeometrySurfaceBrush
author: ratishphilip
description: A composition brush that paints an area defined by the provided geometry.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, brush, Win2D, composition
---

# GeometrySurfaceBrush

The [GeometrySurfaceBrush](/dotnet/api/microsoft.toolkit.uwp.ui.media.geometrysurfacebrush) is a [Brush](/uwp/api/windows.ui.xaml.media.brush) that uses a [CanvasCoreGeometry](/dotnet/api/microsoft.toolkit.uwp.ui.media.geometry.canvascoregeometry) to paint an area.

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://Brushes?sample=GeometrySurfaceBrush)

## Syntax

```xaml
<Grid>
      <Grid.Background>
          <media:GeometrySurfaceBrush x:Name="surfaceBrush"
                                      StrokeThickness="15"
                                      SurfaceHeight="800"
                                      SurfaceWidth="800">
              <media:GeometrySurfaceBrush.RenderStrokeStyle>
                  <geometry:StrokeStyle />
              </media:GeometrySurfaceBrush.RenderStrokeStyle>
              <media:GeometrySurfaceBrush.Stroke>
                  <media:SolidColorCanvasBrush Color="Blue" />
              </media:GeometrySurfaceBrush.Stroke>
              <media:GeometrySurfaceBrush.FillBrush>
                  <media:SolidColorCanvasBrush Color="Yellow" />
              </media:GeometrySurfaceBrush.FillBrush>
              <media:GeometrySurfaceBrush.Geometry>
                  <geometry:CanvasCombinedGeometry GeometryCombineMode="Exclude">
                      <geometry:CanvasCombinedGeometry.Geometry1>
                          <geometry:CanvasPathGeometry Data="F1 M 417.661,109.978 L 508.676,294.396 L 751.683,329.707 L 575.842,501.110 L 610.607,703.805 C 613.366,719.893 596.479,732.162 582.031,724.566 L 400.000,628.867 L 217.969,724.566 C 203.521,732.162 186.634,719.893 189.393,703.805 L 224.158,501.110 L 48.317,329.707 L 291.324,294.396 L 382.339,109.978 C 389.564,95.341 410.436,95.341 417.661,109.978 Z" />
                      </geometry:CanvasCombinedGeometry.Geometry1>
                      <geometry:CanvasCombinedGeometry.Geometry2>
                          <geometry:CanvasRoundedRectangleGeometry x:Name="MaskGeometry2"
                                                                   Width="200"
                                                                   Height="200"
                                                                   RadiusX="30"
                                                                   RadiusY="30"
                                                                   X="300"
                                                                   Y="350" />
                      </geometry:CanvasCombinedGeometry.Geometry2>
                  </geometry:CanvasCombinedGeometry>
              </media:GeometrySurfaceBrush.Geometry>
          </media:GeometrySurfaceBrush>
      </Grid.Background>
  </Grid>
```

## Example Image

![Geometry Surface brush](../resources/images/Brushes/GeometrySurfaceBrush.jpg 'Geometry Surface Brush')

## Properties

| Property          | Type                                                                                         | Description                                                                       |
| ----------------- | -------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| BackgroundBrush   | [RenderCanvasBrushBase](/dotnet/api/microsoft.toolkit.uwp.ui.media.rendercanvasbrushbase)    | The Canvas brush with which the background of the brush surface will be rendered. |
| FillBrush         | [RenderCanvasBrushBase](/dotnet/api/microsoft.toolkit.uwp.ui.media.rendercanvasbrushbase)    | The Canvas brush that is used to fill the Geometry.                               |
| Geometry          | [CanvasCoreGeometry](/dotnet/api/microsoft.toolkit.uwp.ui.media.geometry.canvascoregeometry) | The geometry that is used to paint the surface of the brush.                      |
| Stroke            | [RenderCanvasBrushBase](/dotnet/api/microsoft.toolkit.uwp.ui.media.rendercanvasbrushbase)    | The Canvas brush that is used to render the outlining stroke of the Geometry.     |
| RenderStrokeStyle | [StrokeStyle](/dotnet/api/microsoft.toolkit.uwp.ui.media.geometry.strokestyle)]              | The style of the outline of the geometry.                                         |
| StrokeThickness   | double                                                                                       | The thickness of the outline of the geometry.                                     |

## Sample Project

[GeometrySurfaceBrush sample page Source](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.1.0/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/GeometrySurfaceBrush). You can [see this in action](uwpct://Brushes?sample=GeometrySurfaceBrush) in the [Windows Community Toolkit Sample App](https://aka.ms/windowstoolkitapp).

## Requirements

| Device family | Universal, 10.0.17134.0 or higher                                                                |
| ------------- | ------------------------------------------------------------------------------------------------ |
| Namespace     | Microsoft.Toolkit.Uwp.UI.Media                                                                   |
| NuGet package | [Microsoft.Toolkit.Uwp.UI.Media](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI.Media/) |

## API

- [GeometrySurfaceBrush source code](https://github.com/windows-toolkit/WindowsCommunityToolkit/blob/rel/7.0.0/Microsoft.Toolkit.Uwp.UI.Media/Brushes/GeometrySurfaceBrush.cs)

## Related Topics

- [Render Surfaces](RenderSurfaces.md)
- [XamlCompositionBrushBase Examples](/uwp/api/windows.ui.xaml.media.xamlcompositionbrushbase#examples)
