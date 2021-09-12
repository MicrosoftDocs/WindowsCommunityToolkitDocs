---
title: LinearGradientCanvasBrush
author: ratishphilip
description: XAML equivalent of Win2d's CanvasLinearGradientBrush class which paints in linear gradient.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, brush, Win2D, composition
---

# LinearGradientCanvasBrush

The [LinearGradientCanvasBrush](/dotnet/api/microsoft.toolkit.uwp.ui.media.lineargradientcanvasbrush) is the XAML equivalent of Win2d's CanvasLinearGradientBrush class which paints in linear gradient. This brush is primarily used by the Render Surface Brushes.

> [!div class="nextstepaction"]

## Properties

| Property               | Type                   | Description                                                                                          |
| ---------------------- | ---------------------- | ---------------------------------------------------------------------------------------------------- |
| AlphaMode              | CanvasAphaMode         | Gets or sets the way in which the Alpha channel affects color channels.                              |
| BufferPrecision        | CanvasBufferPrecision  | Gets or sets the precision used for computation.                                                     |
| EdgeBehavior           | CanvasEdgeBehavior     | Gets or sets the behavior of the pixels which fall outside of the gradient's typical rendering area. |
| EndPoint               | Point                  | Gets or sets the point on the Canvas where the gradient stops.                                       |
| PostInterpolationSpace | CanvasColorSpace       | Gets or sets the the color space to be used after interpolation.                                     |
| PreInterpolationSpace  | CanvasColorSpace       | Gets or sets the the color space to be used before interpolation.                                    |
| StartPoint             | Point                  | Gets or sets the point on the Canvas where the gradient starts.                                      |
| Stops                  | GradientStopCollection | Gets or sets the gradient stops that comprise the brush.                                             |
