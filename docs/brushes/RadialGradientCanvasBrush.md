---
title: RadialGradientCanvasBrush
author: ratishphilip
description: XAML equivalent of Win2d's CanvasRadialGradientBrush class which paints in radial gradient.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, brush, Win2D, composition
---

# RadialGradientCanvasBrush

The [RadialGradientCanvasBrush](/dotnet/api/microsoft.toolkit.uwp.ui.media.radialgradientcanvasbrush) is the XAML equivalent of Win2d's CanvasRadialGradientBrush class which paints in radial gradient. This brush is primarily used by the Render Surface Brushes.

> [!div class="nextstepaction"]

## Properties

| Property               | Type                   | Description                                                                                          |
| ---------------------- | ---------------------- | ---------------------------------------------------------------------------------------------------- |
| AlphaMode              | CanvasAphaMode         | Gets or sets the way in which the Alpha channel affects color channels.                              |
| BufferPrecision        | CanvasBufferPrecision  | Gets or sets the precision used for computation.                                                     |
| Center                 | Point                  | Gets or sets the center of the brush's radial gradient.                                              |
| EdgeBehavior           | CanvasEdgeBehavior     | Gets or sets the behavior of the pixels which fall outside of the gradient's typical rendering area. |
| EndPoint               | Point                  | Gets or sets the point on the Canvas where the gradient stops.                                       |
| OriginOffset           | Point                  | Gets or sets the displacement from Center, used to form the brush's radial gradient.                 |
| PostInterpolationSpace | CanvasColorSpace       | Gets or sets the the color space to be used after interpolation.                                     |
| PreInterpolationSpace  | CanvasColorSpace       | Gets or sets the the color space to be used before interpolation.                                    |
| StartPoint             | Point                  | Gets or sets the point on the Canvas where the gradient starts.                                      |
| RadiusX                | double                 | Gets or sets the horizontal radius of the brush's radial gradient.                                   |
| RadiusY                | double                 | Gets or sets the vertical radius of the brush's radial gradient.                                     |
| Stops                  | GradientStopCollection | Gets or sets the gradient stops that comprise the brush.                                             |
