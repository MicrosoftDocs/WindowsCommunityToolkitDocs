---
title: ImageSurfaceOptions
author: ratishphilip
description: A class encapsulating a set of properties which influence the rendering of the image on an ImageSurface or ImageSurfaceBrush.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, brush, Win2D, composition
---

# ImageSurfaceOptions

The [ImageSurfaceOptions](/dotnet/api/microsoft.toolkit.uwp.ui.media.imagesurfaceoptions) class encapsulates a set of properties which influence the rendering of the image on the ImageSurface.

## Properties

| Property               | Type                     | Description                                                                                                                                                                                    | Possible Values                                                                  |
| ---------------------- | ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| AutoResize             | bool                     | Specifies whether the surface should resize itself automatically to match the loaded image size. When set to true, the Stretch, HorizontalAlignment and VerticalAlignment options are ignored. | false                                                                            |
| BlurRadius             | double                   | The radius of the Gaussian blur to be applied to the IImageMaskSurface. This property is not used by IImageSurface.                                                                            | Any positive double value.                                                       |
| HorizontalAlignment    | AlignmentX               | Describes how image is positioned horizontally in the ImageSurface.                                                                                                                            | Left, Center, Right                                                              |
| Interpolation          | CanvasImageInterpolation | Specifies the interpolation used to render the image on the ImageSurface.                                                                                                                      | NearestNeighbor, Linear, Cubic, MultiSampleLinear, Anisotropic, HighQualityCubic |
| Opacity                | float                    | Specifies the opacity of the rendered image.                                                                                                                                                   | 0 - 1f inclusive                                                                 |
| Stretch                | Stretch                  | Describes how image is resized to fill its allocated space.                                                                                                                                    | None, Uniform, Fill, UniformToFill                                               |
| SurfaceBackgroundColor | Color                    | Specifies the color which will be used to fill the ImageSurface before rendering the image.                                                                                                    | All possible values that can be created.                                         |
| VerticalAlignment      | AlignmentY               | Describes how image is positioned vertically in the ImageSurface.                                                                                                                              | Top, Center, Bottom                                                              |

Here is how the image is aligned on the Visual based on the **HorizontalAlignment** and **VerticalAlignment** properties

![Image Alignment](../resources/images/Surface/ImageSurfaceOptions_Alignment.png 'Alignment of image on the Image Surface')

## Requirements

| Device family | Universal, 10.0.17134.0 or higher                                                                |
| ------------- | ------------------------------------------------------------------------------------------------ |
| Namespace     | Microsoft.Toolkit.Uwp.UI.Media                                                                   |
| NuGet package | [Microsoft.Toolkit.Uwp.UI.Media](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI.Media/) |

## API

- [ImageSurfaceOptions source code](https://github.com/windows-toolkit/WindowsCommunityToolkit/blob/rel/7.0.0/Microsoft.Toolkit.Uwp.UI.Media/Surface/ImageSurfaceOptions.cs)
