---
title: Win2D Path Mini Language
author: ratishphilip
description: The Win2D Path Mini Language is a powerful language based on the SVG Path language specification.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, Win2D, Win2D path mini language
dev_langs:
  - csharp
---

# Win2D Path Mini Language

The _Win2D Path Mini Language_ is a powerful and sophisticated language based on the [SVG Path language](https://www.w3.org/TR/SVG11/paths.html) specification. It facilitates specifying complex geometries, color, brushes, strokes and stroke styles in a more compact manner.

Using the Win2D Path Mini Language, the geometry from the initial [CanvasPathGeometry](CanvasPathGeometry.md) example can be created in the following way:

```cs
string pathData = “M 1 1 300 300 1 300 Z”;
CanvasGeometry triangleGeometry = CanvasPathGeometry.CreateGeometry(device, pathData);
```

## Requirements

| Device family | Universal, MinVersion or higher                                                                  |
| ------------- | ------------------------------------------------------------------------------------------------ |
| Namespace     | Microsoft.Toolkit.Uwp.UI.Media.Geometry                                                          |
| NuGet package | [Microsoft.Toolkit.Uwp.UI.Media](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI.Media/) |

## Table of Contents

- [Introduction](#win2d-path-mini-language)
  - [Requirements](#requirements)
- [Win2D Path Mini Language](#win2d-path-mini-language-overview)
- [Path Mini Language](#path-mini-language)
  - [Fill Behavior](#fill-behavior)
  - [MoveTo](#moveto)
  - [LineTo](#lineto)
  - [Horizontal LineTo](#horizontal-lineto)
  - [Vertical LineTo](#vertical-lineto)
  - [Cubic Bézier](#cubic-bézier)
  - [Smooth Cubic Bézier](#smooth-cubic-bézier)
  - [Quadratic Bézier](#quadratic-bézier)
  - [Smooth Quadratic Bézier](#smooth-quadratic-bézier)
  - [Arc](#arc)
  - [Close Path](#close-path)
  - [Ellipse Figure](#ellipse-figure)
  - [Polygon Figure](#polygon-figure)
  - [Rectangle Figure](#rectangle-figure)
  - [RoundedRectangle Figure](#roundedrectangle-figure)
- [CanvasBrush Mini Language](#canvasbrush-mini-language)
  - [ICanvasBrush Attribute Commands](#icanvasbrush-attribute-commands)
    - [Start Point](#start-point)
    - [End Point](#end-point)
    - [Opacity](#opacity)
    - [Alpha Mode](#alpha-mode)
    - [Buffer Precision](#buffer-precision)
    - [Edge Behavior](#edge-behavior)
    - [Pre Interpolation Color Space](#pre-interpolation-color-space)
    - [Post Interpolation Color Space](#post-interpolation-color-space)
    - [Origin Offset](#origin-offset)
    - [GradientStop](#gradientstop)
    - [GradientStopHdr](#gradientstophdr)
  - [SolidColorBrush](#solidcolorbrush)
  - [LinearGradientBrush](#lineargradientbrush)
  - [LinearGradientBrush with GradientStopHdr](#lineargradientbrush-with-gradientstophdr)
  - [RadialGradientBrush](#radialgradientbrush)
  - [RadialGradientBrush with GradientStopHdr](#radialgradientbrush-with-gradientstophdr)
- [CanvasStrokeStyle Mini Language](#canvasstrokestyle-mini-language)
  - [CanvasStrokeStyle Attributes](#canvasstrokestyle-attributes)
    - [Dash Style](#dash-style)
    - [Line Join](#line-join)
    - [Miter Limit](#miter-limit)
    - [Dash Offset](#dash-offset)
    - [Start Cap](#start-cap)
    - [End Cap](#end-cap)
    - [Dash Cap](#dash-cap)
    - [Transform Behavior](#transform-behavior)
    - [Custom Dash Style](#custom-dash-style)
  - [Defining the CanvasStrokeStyle](#defining-the-canvasstrokestyle)
- [CanvasStroke Mini Language](#canvasstroke-mini-language)
  - [ICanvasStroke interface and CanvasStroke class](#icanvasstroke-interface-and-canvasstroke-class)
- [Creating Geometries, Brushes, Strokes and StrokeStyles](#creating-geometries-brushes-strokes-and-strokestyles)

## Win2D Path Mini Language Overview

Win2D Path Mini Language syntax derives from the SVG path syntax. It is a prefix notation (i.e., commands followed by parameters). In order to ensure that the data, specified in Win2D Path Mini Language, is concise the following rules must be followed

- The commands are can be expressed as `one` , `two` or `three` characters (e.g., a `Move` command is expressed as an `M` , a LinearGradientBrush command is expressed as `LG` ).
- Superfluous white space and separators such as commas can be eliminated (e.g., `M 100 100 L 200` `200` contains unnecessary spaces and could be expressed more compactly as `M100 100L200 200` ).
- The command letter can be eliminated on subsequent commands if the same command is used multiple times in a row (e.g., you can drop the second "L" in "M 100 200 L 200 100 L - 100 -200" and use "M 100 200 L 200 100 -100 -200" instead).
- Relative versions of all commands are available (uppercase means absolute coordinates, lowercase means relative coordinates).
- Most of the parameters are either integer or floating-point values. The only allowable decimal point is a Unicode U+0046 FULL STOP (".") character (also referred to in Unicode as PERIOD, dot, and decimal point) and no other delimiter characters are allowed [UNICODE]. (For example, the following is an invalid numeric value in a path data stream: "13,000.56". Instead, say: "13000.56".)
- For the relative versions of the commands, all coordinate values are relative to the current point at the start of the command.

In the following sections, the following notation is used:

- `()` indicates the grouping of parameters.
- `+` indicates one or more of the given parameter(s) is required.
- `[]` indicates any one of the values specified within the square brackets. For e.g. [01] means either 0 or 1.
- `?` denotes an optional parameter

## Path Mini Language

Paths represent the outline of a shape, which can be filled, stroked, used as a clipping path, or any combination of the three.

A path is described using the concept of a current point. In an analogy with drawing on paper, the current
point can be thought of as the location of the pen. The position of the pen can be changed, and the outline
of a shape (open or closed) can be traced by dragging the pen in either straight lines or curves.

A path can be defined using the following commands

### Fill Behavior

| Format |            |
| ------ | ---------- |
| F [01] | _Absolute_ |
| f [01] | _Relative_ |

`Fill Behavior` specifies how the intersecting areas of geometries or figures are combined to form the area of the composite geometry. It represents the `CanvasFilledRegionDetermination` enumeration which is based on `D2D1_FILL_MODE` enumeration. The Fill Behavior parameter can be either `0` or `1`.

The parameter value `0` indicates `CanvasFilledRegionDetermination.Alternate` which determines whether a point is in the fill region by drawing a ray from that point to infinity in any direction, and then counting the number of path segments within the given shape that the ray crosses. If this number is odd, the point is in the fill region; if even, the point is outside the fill region.

The parameter value `1` indicates `CanvasFilledRegionDetermination.Winding` which determines whether a point is in the fill region of the path by drawing a ray from that point to infinity in any direction, and then examining the places where a segment of the shape crosses the ray. Starting with a count of zero, add one each time a segment crosses the ray from left to right and subtract one each time a path segment crosses the ray from right to left, as long as left and right are seen from the perspective of the ray. After counting the crossings, if the result is zero, then the point is outside the path. Otherwise, it is inside the path.

> Each Path data should have only one Fill Behavior specified. Otherwise, an exception will be raised.

`CanvasPathGeometry` invokes the `CanvasPathBuilder.SetFilledRegionDetermination()` API for this command.

### MoveTo

| Format     |            |
| ---------- | ---------- |
| `M` (x y)+ | _Absolute_ |
| `m` (x y)+ | _Relative_ |

The `MoveTo` command establishes a new current point. The effect is as if the "pen" were lifted and moved to a new location. A path data segment must begin with a Move command. Subsequent "moveto" commands (i.e., when the Move is not the first command) represent the start of a new subpath.

`M` (uppercase) indicates that absolute coordinates will follow whereas `m` (lowercase) indicates that relative coordinates will follow.

If a `MoveTo` command is followed by multiple pairs of coordinates, the subsequent pairs are
treated as implicit `LineTo` commands. Hence, implicit `LineTo` commands will be relative if the `MoveTo` command is relative and absolute if the `MoveTo` command is absolute.

> If a relative `MoveTo` (`m`) command appears as the first element of the path, then its parameters are treated as a pair of absolute coordinates.
>
> In this case, subsequent pairs of coordinates are treated as relative even though the initial `MoveTo` is interpreted as an absolute `MoveTo`.

`CanvasPathGeometry` invokes the `CanvasPathBuilder.BeginFigure()` API for this command.

### LineTo

| Format     |            |
| ---------- | ---------- |
| `L` (x y)+ | _Absolute_ |
| `l` (x y)+ | _Relative_ |

Draws a line from the current point to the specified (`x`,`y`) coordinate. (`x`,`y`) becomes the new current point.

`L` (uppercase) indicates that absolute coordinates will follow whereas `l` (lowercase) indicates that relative coordinates will follow.

> A number of coordinates pairs may be specified to draw a polyline. At the end of the command, the new current point is set to the final set of coordinates provided.

`CanvasPathGeometry` invokes the `CanvasPathBuilder.AddLine()` API for this command.

### Horizontal LineTo

| Format |            |
| ------ | ---------- |
| `H` x+ | _Absolute_ |
| `h` x+ | _Relative_ |

Draws a horizontal line from the current point (`cpx`, `cpy`) to (`x`, `cpy`).

`H` (uppercase) indicates that absolute coordinates will follow whereas `h` (lowercase) indicates that relative coordinates will follow.

> Multiple `x` values can be provided (although usually this doesn't make sense). At the end of the command, the new current point becomes ( `x`, `cpy` ) for the final value of `x`.

`CanvasPathGeometry` invokes the `CanvasPathBuilder.AddLine()` API for this command.

### Vertical LineTo

| Format |            |
| ------ | ---------- |
| `V` y+ | _Absolute_ |
| `v` y+ | _Relative_ |

Draws a vertical line from the current point (`cpx`, `cpy`) to (`cpx`, `y`).

`V` (uppercase) indicates that absolute coordinates will follow whereas `v` (lowercase) indicates that relative coordinates will follow.

> Multiple `y` values can be provided (although usually this doesn't make sense). At the end of the command, the new current point becomes (`cpx`, `y`) for the final value of `y`.

`CanvasPathGeometry` invokes the `CanvasPathBuilder.AddLine()` API for this command.

### Cubic Bézier

| Format                 |            |
| ---------------------- | ---------- |
| `C` (x1 y1 x2 y2 x y)+ | _Absolute_ |
| `c` (x1 y1 x2 y2 x y)+ | _Relative_ |

Draws a cubic Bézier curve from the current point to (`x`,`y`) using (`x1`,`y1`) as the control point at the beginning of the curve and (`x2`,`y2`) as the control point at the end of the curve.

`C` (uppercase) indicates that absolute coordinates will follow whereas `c` (lowercase) indicates that relative coordinates will follow.

> Multiple sets of coordinates may be specified to draw a polybézier. At the end of the command, the new current point becomes the final (`x`,`y`) coordinate pair used in the polybézier.

`CanvasPathGeometry` invokes the `CanvasPathBuilder.AddCubicBezier()` API for this command.

### Smooth Cubic Bézier

| Format           |            |
| ---------------- | ---------- |
| `S` (x2 y2 x y)+ | _Absolute_ |
| `s` (x2 y2 x y)+ | _Relative_ |

Draws a cubic Bézier curve from the current point to (`x`,`y`). The first control point is assumed to be the reflection of the second control point on the previous command relative to the current point. (_If there is no previous command or if the previous command was not a `C`, `c`, `S` or `s` , assume the first control point is coincident with the current point._)

(`x2`,`y2`) is the second control point (i.e., the control point at the end of the curve).

`S` (uppercase) indicates that absolute coordinates will whereas `s` (lowercase) indicates that relative coordinates will follow.

> Multiple sets of coordinates may be specified to draw a polybézier. At the end of the command,
> the new current point becomes the final (`x`,`y`) coordinate pair used in the polybézier.

`CanvasPathGeometry` invokes the `CanvasPathBuilder.AddCubicBezier()` API for this command.

### Quadratic Bézier

| Format           |            |
| ---------------- | ---------- |
| `Q` (x1 y1 x y)+ | _Absolute_ |
| `q` (x1 y1 x y)+ | _Relative_ |

Draws a quadratic Bézier curve from the current point to (`x`,`y`) using (`x1`,`y1`) as the control point.

`Q` (uppercase) indicates that absolute coordinates will whereas `q` (lowercase) indicates that relative coordinates will follow.

> Multiple sets of coordinates may be specified to draw a polybézier. At the end of the command, the new current point becomes the final (`x`,`y`) coordinate pair used in the polybézier.

`CanvasPathGeometry` invokes the `CanvasPathBuilder.AddQuadraticBezier()` API for this command.

### Smooth Quadratic Bézier

| Format     |            |
| ---------- | ---------- |
| `T` (x y)+ | _Absolute_ |
| `t` (x y)+ | _Relative_ |

Draws a quadratic Bézier curve from the current point to (x,y). The control point is assumed to be the reflection of the control point on the previous command relative to the current point. (If there is no previous command or if the previous command was not a `Q`, `q`, `T` or `t` , assume the control point is coincident with the current
point.)

`T` (uppercase) indicates that absolute coordinates will whereas `t` (lowercase) indicates that relative coordinates will follow.

> Multiple sets of coordinates may be specified to draw a polybézier. At the end of the command the new current point becomes the final (`x`,`y`) coordinate pair used in the polybézier.

`CanvasPathGeometry` invokes the `CanvasPathBuilder.AddQuadraticBezier()` API for this command.

### Arc

| Format                                                     |            |
| ---------------------------------------------------------- | ---------- |
| `A` (radius radiusY angle IsLargeFlag SweepDirection x y)+ | _Absolute_ |
| `a` (radius radiusY angle IsLargeFlag SweepDirection x y)+ | _Relative_ |

Draws an elliptical arc from the current point to ( `x` , `y` ). The size and orientation of the ellipse are defined by two radii ( `rx` , `ry` ) and an `x-axis-rotation` , which indicates how the ellipse as a whole is rotated relative to the current coordinate system. The center ( `cx` , `cy` ) of the ellipse is calculated automatically to satisfy the constraints
imposed by the other parameters.

`IsLargeFlag` specifies whether an arc should take the longer or shorter way, around the ellipse to join its start and end points (`0` denotes the arc’s sweep should be π or less whereas `1` denotes the arc’s sweep should be π or more).

`SweepDirection` specifies the direction that an elliptical arc is drawn (`0` means
CounterClockwise and `1` means Clockwise).

`CanvasPathGeometry` invokes the `CanvasPathBuilder.AddArc()` API for this command.

### Close Path

| Format |
| ------ |
| `Z`    |
| `z`    |

Closes the current subpath by drawing a straight line from the current point to current subpath's initial point. _Since the `Z` and `z` commands take no parameters, they have an identical effect._

`CanvasPathGeometry` invokes the `CanvasPathBuilder.EndFigure()` API for this command.

### Ellipse Figure

| Format                     |            |
| -------------------------- | ---------- |
| `O` (radiusX radiusY x y)+ | _Absolute_ |
| `o` (radiusX radiusY x y)+ | _Relative_ |

Adds an Ellipse Figure to the path. The `radiusX` and `radiusY` parameters denote the elliptical radii on the x-axis and y-axis respectively. ( `x y` ) denotes the center of the Ellipse. _The current point remains unchanged._

`CanvasPathGeometry` internally invokes the `CanvasPathBuilder.AddEllipseFigure()` extension method for this command.

### Polygon Figure

| Format                     |            |
| -------------------------- | ---------- |
| `P` (numSides radius x y)+ | _Absolute_ |
| `p` (numSides radius x y)+ | _Relative_ |

Adds an n-sided Polygon to the path. The `radius` parameter denotes the radius of the circle circumscribing the polygon vertices. ( `x y` ) denotes the center of the polygon. _The current point remains unchanged._

This command internally invokes the `CanvasPathBuilder.AddPolygonFigure()` extension method.

### Rectangle Figure

| Format                  |            |
| ----------------------- | ---------- |
| `R` (x y width height)+ | _Absolute_ |
| `r` (x y width height)+ | _Relative_ |

Adds a Rectangle to the path. ( `x y` ) denotes the top left corner of the Rectangle. The current point remains unchanged.

`CanvasPathGeometry` internally invokes the `CanvasPathBuilder.AddRectangleFigure()` extension method for this command.

### RoundedRectangle Figure

| Format                                  |            |
| --------------------------------------- | ---------- |
| `U` (x y width height radiusX radiusY)+ | _Absolute_ |
| `u` (x y width height radiusX radiusY)+ | _Relative_ |

Adds a RoundedRectangle to the path. ( `x y` ) denotes the top left corner of the RoundedRectangle. `radiusX` and `radiusY` denote the radii of the corner curves on the x-axis and y-axis respectively. _The current point remains unchanged._

`CanvasPathGeometry` internally invokes the `CanvasPathBuilder.AddRoundedRectangleFigure()` extension method for this command.

## CanvasBrush Mini Language

This section describes in detail how a Win2D brush can be defined as a string and an instance created from it. Using the CanvasBrush Mini Language the following Win2D brushes can be created (they all implement the `ICanvasBrush` interface)

- `SolidColorBrush`
- `CanvasLinearGradientBrush`
- `CanvasRadialGradientBrush`

The Win2D Path Mini Language uses the following syntax to define a brush and its attributes

| Format                                                                     |
| -------------------------------------------------------------------------- |
| `<BrushTypeCommand> (<BrushAttributeCommand> <BrushAttributeParameters>)`+ |

Some of the attributes are optional while the others are mandatory. The order in which the attributes are specified should be maintained.

### ICanvasBrush Attribute Commands

This section describes the various brush attributes that will be used to define and construct an ICanvasBrush.

#### Start Point

| Format    |
| --------- |
| `M` (x y) |

Denotes the point on the canvas where the gradient starts.

#### End Point

| Format    |
| --------- |
| `Z` (x y) |

Denotes the point on the canvas where the gradient ends.

#### Opacity

| Format      |
| ----------- |
| `O` opacity |

Denotes the opacity of the brush. The `opacity` parameter should have a value in the range [0, 1].

#### Alpha Mode

| Format    |
| --------- |
| `A` [012] |

Specifies the way in which an alpha channel affects color channels. This attribute corresponds to the [CanvasAlphaMode](https://microsoft.github.io/Win2D/WinUI3/html/T_Microsoft_Graphics_Canvas_CanvasAlphaMode.htm) enumeration. Default is `0` ( `Premultiplied` ).

| Member          |     | Description                                                                                                                                                                                                                                                     |
| --------------- | --- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Premultiplied` | 0   | The alpha value has been premultiplied. In blending, each color is scaled by the alpha value. Note that the alpha value itself is the same in both straight and premultiplied alpha. Typically, no color channel value is greater than the alpha channel value. |
| `Straight`      | 1   | The alpha channel indicates the transparency of the color.                                                                                                                                                                                                      |
| `Ignore`        | 2   | The alpha value is ignored.                                                                                                                                                                                                                                     |

#### Buffer Precision

| Format      |
| ----------- |
| `B` [01234] |

Specifies the bit depth used for graphical computations. This attribute corresponds to the
[CanvasBufferPrecision](https://microsoft.github.io/Win2D/WinUI3/html/T_Microsoft_Graphics_Canvas_CanvasBufferPrecision.htm) | enumeration |. Default is `0` ( |`Precision8UIntNormalized` ).

| Value                          | Member | Description                                                 |
| ------------------------------ | ------ | ----------------------------------------------------------- |
| `Precision8UIntNormalized`     | 0      | Use 8-bit normalized integer per channel.                   |
| `Precision8UIntNormalizedSrgb` | 1      | Use 8-bit normalized integer standard RGB data per channel. |
| `Precision16UIntNormalized`    | 2      | Use 16-bit normalized integer per channel.                  |
| `Precision16Float`             | 3      | Use 16-bit floats per channel.                              |
| `Precision32Float`             | 4      | Use 32-bit floats per channel.                              |

#### Edge Behavior

| Format    |
| --------- |
| `E` [012] |

Specifies the behavior for pixels which fall outside of the gradient's typical rendering area. This attribute corresponds to the [CanvasEdgeBehavior](https://microsoft.github.io/Win2D/WinUI3/html/T_Microsoft_Graphics_Canvas_CanvasEdgeBehavior.htm) enumeration. Default is `0` ( `Clamp` ).

| Member | Value | Description                                                 |
| ------ | ----- | ----------------------------------------------------------- |
| Clamp  | 0     | Repeat the edge pixels of the brush's content.              |
| Wrap   | 1     | Tile the brush's content.                                   |
| Mirror | 2     | Tile the brush's content, and flip each alternate tile. |

#### Pre Interpolation Color Space

| Format    |
| --------- |
| `P` [012] |

Specifies the color space to be used before interpolation. This attribute corresponds to the CanvasColorSpace
enumeration. Default value is `1` ( `Srgb` ).

| Member | Value | Description                                             |
| ------ | ----- | ------------------------------------------------------- |
| Custom | 0     | The color space is a custom ICC ColorManagementProfile. |
| Srgb   | 1     | The color space is sRGB.                                |
| ScRgb  | 2     | The color space is scRGB.                               |

#### Post Interpolation Color Space

| Format    |
| --------- |
| `R` [012] |

Specifies the color space to be used after interpolation. This attribute corresponds to the CanvasColorSpace
enumeration. Default value is `1` ( `Srgb` ).

| Member | Value | Description                                             |
| ------ | ----- | ------------------------------------------------------- |
| Custom | 0     | The color space is a custom ICC ColorManagementProfile. |
| Srgb   | 1     | The color space is sRGB.                                |
| ScRgb  | 2     | The color space is scRGB.                               |

#### Origin Offset

| Format    |
| --------- |
| `F` (x y) |

Specifies a displacement from Center, used to form the brush's radial gradient.

#### GradientStop

| Format                 |
| ---------------------- |
| `S` (offset hexColor)+ |

Specifies one or more gradient stops (using Hexadecimal Color) in a gradient brush.

The parameter `offset` refers to the position of the gradient stop and should be a floating-point number between 0 and 1, inclusive.

The parameter `hexColor` denotes the color specified in `#RRGGBB` or `#AARRGGBB` format.

Example:

```
“S 0.2 FF112233”
“S 0.1 #FF0000 0.4 #00FF00 0.9 #0000FF”
```

#### GradientStopHdr

| Format                |
| --------------------- |
| `S` (offset x y z w)+ |

Specifies one or more high dynamic range gradient stops in a gradient brush.

The parameter `offset` refers to the position of the gradient stop and it should be a floating-point number between 0 and 1, inclusive.

The parameters `x, y, z` and `w` denote the components of the high dynamic range color.

Example:

```
“S 0.2 0.2 .5 .75 1”
“S 0.1 0.3 0.4 0.5 1.0 0.4 .3 .2 .1 0.9”
```

### SolidColorBrush

| Format                       |
| ---------------------------- |
| `SC` hexColor (`O` opacity)? |
| `SC` x y z w (`O` opacity)?  |

The SolidColorBrush is defined by the `SC` command. It has two attributes - `Color` and `Opacity`.

The `Color` attribute is specified as either a Hexadecimal Color or a High Dynamic Range Color.

The `Opacity` attribute is optional and can be specified with the `O` attribute command and an opacity value in the range [0, 1].

Example:

```
“SC #FFAABBCC”
“SC #FF1233AA O .75”
“SC 0.1 0.3 0.4 0.5”
“SC 0.1 0.3 0.4 0.5 O 0.9”
```

### LinearGradientBrush

| Format                                                                                                             |
| ------------------------------------------------------------------------------------------------------------------ |
| `LG` `M` x0 y0 `Z` x1 y1 (`O` opacity `A` [012] `B` [01234] `E` [012] `P` [012] `R` [012])? `S` (offset hexColor)+ |

The LinearGradientBrush is defined by the `LG` command. It has the following mandatory attributes

- StartPoint ( `M` )
- EndPoint ( `Z` )
- GradientStops ( `S` )

It also has the following optional attributes

- Opacity ( `O` )
- Alpha Mode ( `A` )
- Buffer Precision ( `B` )
- Edge Behavior ( `E` )
- Pre Interpolation Color Space ( `P` )
- Post Interpolation Color Space ( `R` )

Example:

```
“LG M 0 80 Z0 0 S 0.00 #ffee5124, 0.18 #fff05627, 0.26 #fff15b29, 0.6 #fff58535, 1.00 #fff9af41”
“LG M 0 80 Z0 0 O 0.75 A 1 E 2 S 0.00 #ffee5124, 0.3 #fff05627, 0.7 #fff58535, 1.00 #fff9af41”
```

### LinearGradientBrush with GradientStopHdr

| Format                                                                                                          |
| --------------------------------------------------------------------------------------------------------------- |
| `LH M` x0 y0 `Z` x1 y1 (`O` opacity `A` [012] `B` [01234] `E` [012] `P` [012] `R` [012])? `S` (offset x y z w)+ |

The LinearGradientBrush with GradientStopHdr is defined by the `LH` command. It has the following mandatory attributes

- StartPoint ( `M` )
- EndPoint ( `Z` )
- GradientStopHdrs ( `S` )

It also has the following optional attributes

- Opacity ( `O` )
- Alpha Mode ( `A` )
- Buffer Precision ( `B` )
- Edge Behavior ( `E` )
- Pre Interpolation Color Space ( `P` )
- Post Interpolation Color Space ( `R` )

Example:

```
“LH M 0 80 Z0 0 P 1 R 1 S 0.00 0.9333333, 0.3176471, 0.1411765, 1, 0.14 0.9411765, 0.3372549, 0.1529412, 1, 0.26 0.945098, 0.3568628, 0.1607843, 1, 0.72 0.9607843, 0.5215687, 0.2078431, 1, 1.00 0.9764706, 0.6862745, 0.254902, 1”
```

### RadialGradientBrush

| Format                                                                                                                 |
| ---------------------------------------------------------------------------------------------------------------------- |
| `RG` radX radY x y (`O` opacity `A` [012] `B` [01234] `E` [012] `F` x1 y1 `P` [012] `R` [012])? `S` (offset hexColor)+ |

The RadialGradientBrush is defined by the `RG` command. It has the following mandatory attributes

- RadiusX
- RadiusY
- CenterX ( `x` )
- CenterY ( `y` )
- GradientStops ( `S` )

It also has the following optional attributes

- Opacity ( `O` )
- Alpha Mode ( `A` )
- Buffer Precision ( `B` )
- Edge Behavior ( `E` )
- Origin Offset ( `F` )
- Pre Interpolation Color Space ( `P` )
- Post Interpolation Color Space ( `R` )

Example:

```
“RG 40 6 0 32 0 4 00 S 0.00 #ffee5124, 0.18 #fff05627, 0.26 #fff15b29, 0.7 #fff58535, 1.00 #fff9af41”
“RG 40 60 320 40 0 A 1 B 2 E 2 S 0.00 #ffee5124, 0.3 #fff05627, 0.7 #fff58535, 1.00 #fff9af41”
```

### RadialGradientBrush with GradientStopHdr

| Format                                                                                                                |
| --------------------------------------------------------------------------------------------------------------------- |
| `RH` radX radY x y (`O` opacity `A` [012] `B` [01234] `E` [012] `F` x1 y1 `P` [012] `R` [012])? `S` (offset x y z w)+ |

Command Parameter

The RadialGradientBrush is defined by the `RG` command. It has the following mandatory attributes

- RadiusX
- RadiusY
- CenterX ( `x` )
- CenterY ( `y` )
- GradientStopHdrs ( `S` )

It also has the following optional attributes

- Opacity ( `O` )
- Alpha Mode ( `A` )
- Buffer Precision ( `B` )
- Edge Behavior ( `E` )
- Origin Offset ( `F` )
- Pre Interpolation Color Space ( `P` )
- Post Interpolation Color Space ( `R` )

Example:

```
“RH 400 400 32 0 3 20 O 0.94 A 1 E 2 S 0.00 0.9333333, 0.3176471, 0.1411765, 1, 0.18 0.9411765, 0.3372549, 0.1529412, 1, 0.26 0.945098, 0.3568628, 0.1607843, 1, 0.72 0.9607843, 0.5215687, 0.2078431, 1, 1.00 0.9764706, 0.6862745, 0.254902, 1”
```

## CanvasStrokeStyle Mini Language

The `Microsoft.Graphics.Canvas.Geometry.CanvasStrokeStyle` class defines a stroke style for drawing lines.
The stroke style describes whether the line comprises of dashes, dots, or solid line, how to join line segments, how to cap the ends, etc.

This section describes in detail how a `CanvasStrokeStyle` can be defined as a string and a `CanvasStrokeStyle` instance created from it.

The Win2D Path Mini Language uses the following format to define a CanvasStrokeStyle and its attributes

| Format                                                                     |
| -------------------------------------------------------------------------- |
| `CSS` (`<StrokeStyleAttributeCommand>` `<StrokeStyleAttributeParameter>`)+ |

Some of the attributes are optional while the others are mandatory. The order in which the attributes are
specified should be maintained.

### CanvasStrokeStyle Attributes

This section describes the various stroke attributes that are used to define and construct a CanvasStrokeStyle object.

#### Dash Style

| Format       |
| ------------ |
| `DS` [01234] |

Describes the sequence of dashes, dots, and gaps in a stroke style. This attribute is ignored if the
`CustomDashStyle` attribute is set. This attribute corresponds to the [CanvasDashStyle](https://microsoft.github.io/Win2D/WinUI2/html/T_Microsoft_Graphics_Canvas_Geometry_CanvasDashStyle.htm) enumeration. Default
value is `0` ( `Solid` ).

| Member     | Value | Description                                                                                                                                                                      |
| ---------- | ----- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Solid      | 0     | A solid line with no breaks.                                                                                                                                                     |
| Dash       | 1     | A dash followed by a gap of equal length. The dash and the gap are each twice as long as the stroke thickness. The equivalent custom dash style is {2, 2}.                       |
| Dot        | 2     | A dot followed by a longer gap. The equivalent custom dash style is {0, 2}.                                                                                                      |
| DashDot    | 3     | A dash, followed by a gap, followed by a dot, followed by another gap. The equivalent custom dash style is {2, 2, 0, 2}.                                                         |
| DashDotDot | 4     | A dash, followed by a gap, followed by a dot, followed by another gap, followed by another dot, followed by another gap. The equivalent custom dash style is {2, 2, 0, 2, 0, 2}. |

#### Line Join

| Format      |
| ----------- |
| `LJ` [0123] |

Describes the shape that joins two lines or segments. This attribute corresponds to the [CanvasLineJoin](https://microsoft.github.io/Win2D/WinUI2/html/T_Microsoft_Graphics_Canvas_Geometry_CanvasLineJoin.htm)
enumeration. Default value is `0` (`Miter`).

| Member       | Value | Description                                                                                                |
| ------------ | ----- | ---------------------------------------------------------------------------------------------------------- |
| Miter        | 0     | Regular angular vertices.                                                                                  |
| Bevel        | 1     | Beveled vertices.                                                                                          |
| Round        | 2     | Rounded vertices.                                                                                          |
| MiterOrBevel | 3     | Regular angular vertices unless the join would extend beyond the miter limit; otherwise, beveled vertices. |

#### Miter Limit

| Format     |
| ---------- |
| `ML` limit |

Describes the limit on the ratio of the miter length to half the stroke's thickness.

#### Dash Offset

| Format      |
| ----------- |
| `DO` offset |

Describes how far into the dash sequence the stroke will start.

#### Start Cap

| Format      |
| ----------- |
| `SC` [0123] |

Describes the type of shape used at the beginning of a stroke. This attribute corresponds to the
[CanvasCapStyle](https://microsoft.github.io/Win2D/WinUI2/html/T_Microsoft_Graphics_Canvas_Geometry_CanvasCapStyle.htm) enumeration. Default value is `0` (`Flat`).

| Member   | Value | Description                                                                                   |
| -------- | ----- | --------------------------------------------------------------------------------------------- |
| Flat     | 0     | A cap that does not extend past the last point of the line.                                   |
| Square   | 1     | Half of a square that has a length equal to the line thickness.                               |
| Round    | 2     | A semicircle that has a diameter equal to the line thickness.                                 |
| Triangle | 3     | An isosceles right triangle whose hypotenuse is equal in length to the thickness of the line. |

#### End Cap

| Format      |
| ----------- |
| `EC` [0123] |

Describes the type of shape used at the beginning of a stroke. This attribute corresponds to the
[CanvasCapStyle](https://microsoft.github.io/Win2D/WinUI2/html/T_Microsoft_Graphics_Canvas_Geometry_CanvasCapStyle.htm) enumeration. Default value is `0` (`Flat`).

| Member   | Value | Description                                                                                   |
| -------- | ----- | --------------------------------------------------------------------------------------------- |
| Flat     | 0     | A cap that does not extend past the last point of the line.                                   |
| Square   | 1     | Half of a square that has a length equal to the line thickness.                               |
| Round    | 2     | A semicircle that has a diameter equal to the line thickness.                                 |
| Triangle | 3     | An isosceles right triangle whose hypotenuse is equal in length to the thickness of the line. |

#### Dash Cap

| Format      |
| ----------- |
| `DC` [0123] |

Describes the type of shape used at the beginning of a stroke. This attribute corresponds to the
[CanvasCapStyle](https://microsoft.github.io/Win2D/WinUI2/html/T_Microsoft_Graphics_Canvas_Geometry_CanvasCapStyle.htm) enumeration. Default value is `0` ( `Flat` ).

| Member   | Value | Description                                                                                                                                    |
| -------- | ----- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| Flat     | 0     | A cap that does not extend past the last point of the line. If `Dash Cap` is set to Flat, dots will have zero size so only dashes are visible. |
| Square   | 1     | Half of a square that has a length equal to the line thickness.                                                                                |
| Round    | 2     | A semicircle that has a diameter equal to the line thickness.                                                                                  |
| Triangle | 3     | An isosceles right triangle whose hypotenuse is equal in length to the thickness of the line.                                                  |

#### Transform Behavior

| Format     |
| ---------- |
| `TB` [012] |

Describes how the world transforms, dots per inch (DPI), and stroke width affect the shape of the pen. This attribute corresponds to the [CanvasStrokeTransformBehavior](https://microsoft.github.io/Win2D/WinUI2/html/T_Microsoft_Graphics_Canvas_Geometry_CanvasStrokeTransformBehavior.htm) enumeration. Default value is `0` (`Normal`).

| Member   | Value | Description                                                                                                                   |
| -------- | ----- | ----------------------------------------------------------------------------------------------------------------------------- |
| Normal   | 0     | The stroke respects the width. currently set world transform, the DPI, and the stroke                                         |
| Fixed    | 1     | The stroke does not respect the world transform but it does respect the DPI and stroke width.                                 |
| Hairline | 2     | The stroke is forced to 1 pixel wide (in device space) and does not respect the world transform, the DPI, or the stroke width. |

#### Custom Dash Style

| Format                      |
| --------------------------- |
| `CDS` (dashSize spaceSize)+ |

Describes an array describing a custom dash pattern. The array elements specify the length of each dash and space in the pattern. The first element sets the length of a dash, the second element sets the length of a space, and the third element sets the length of a dash, and so on. The length of each dash and space in the dash pattern is the product of the element value in the array and the stroke width.

> [!NOTE]
> This overrides the `DashStyle` property, which is only used when `CustomDashStyle` is set to null.

**This array must contain an even number of elements.**

Example:

```
“CDS 2 2 0 2 1 3”
```

### Defining the CanvasStrokeStyle

Using the attributes defined in the previous section the CanvasStrokeStyle can be defined in the following way

| Format                                                                                                                               |
| ------------------------------------------------------------------------------------------------------------------------------------ |
| `CSS` (`DS` [01234] `LJ` [0123] `ML` limit `DO` offset `SC` [0123] `EC` [0123] `DC` [0123] `TB` [012] `CDS` (dashSize spaceSize)+ )? |

All the attributes of `CanvasStrokeStyle` are optional. If none of the attributes is specified in the `CanvasStrokeStyle` definition string, then the default `CanvasStrokeStyle` object is created.

> [!NOTE]
> While specifying the attributes, the order of the attributes must be maintained.

Example:

```
“CSS CDS 2 2 0 2 1 3”
“CSS”
“CSS DS 2 DO 2 SC 1 EC 2 ”
```

## CanvasStroke Mini Language

### ICanvasStroke interface and CanvasStroke class

In Win2D, the stroke, that is used to render an outline to a CanvasGeometry, is comprised of three components

- Stroke Width – defines the width of the stroke.
- Stroke Brush – defines the `ICanvasBrush` that will be used to render the stroke.
- Stroke Style – defines the `CanvasStrokeStyle` for the stroke.
- Transform - defines the Transform property of the stroke brush.

`ICanvasStroke` interface, defined in the `Microsoft.Toolkit.Uwp.UI.Media.Geometry` namespace, encapsulates these three components and the `CanvasStroke` class implements this interface.

```cs
public interface ICanvasStroke
{
    ICanvasBrush Brush { get; }
    float Width { get; }
    CanvasStrokeStyle Style { get; }
    Matrix3x2 Transform { get; set; }
}

public sealed class CanvasStroke : ICanvasStroke
{
    public ICanvasBrush Brush { get; }
    public float Width { get; }
    public CanvasStrokeStyle Style { get; }
    public Matrix3x2 Transform { get; set; }

    public CanvasStroke(ICanvasBrush brush, float strokeWidth = 1f);
    public CanvasStroke(ICanvasBrush brush, float strokeWidth, CanvasStrokeStyle strokeStyle);
    public CanvasStroke(ICanvasResourceCreator device, Color strokeColor, float strokeWidth = 1f);
    public CanvasStroke(ICanvasResourceCreator device, Color strokeColor, float strokeWidth, CanvasStrokeStyle strokeStyle);
}
```

In order to define a CanvasStroke using the Mini Language, the `ST` command is used in the following way

| Format                                                     |
| ---------------------------------------------------------- |
| `ST` strokeWidth `<CanvasBrushML>` `<CanvasStrokeStyleML>` |

In this command string, `strokeWidth` is a positive floating point number, `CanvasBrushML` denotes the CanvasBrush Mini Language and the `CanvasStrokeStyleML` denotes the CanvasStrokeStyle Mini Language.

Example:

```
“ST 4.5 LG M 0 0 Z80 80 S 0.00 #ffff0000, 0.5 #ff00ff00, 0.99 #ff0000ff CSS DS 2 Do 2 SC 1 EC 2 CDS 2 2 0 2 1 3”
“ST 2 SC #ff0000”
```

## Creating Geometries, Brushes, Strokes and StrokeStyles

To create instances of CanvasGeomety, Brushes, CanvasStrokes, and CanvasStrokeStyles you can use the `CanvasPathGeometry` class in the `Microsoft.Toolkit.Uwp.UI.Media.Geometry` namespace.

## Related Topics

- [More details about `CanvasPathGeometry` class here.](CanvasPathGeometry.md)
