---
title: ImageEx
author: nmetulev
description: The ImageEx Control and downloads images asynchronously, while showing a loading indicator.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, ImageEx, xaml control, xaml
---

# ImageEx

The [ImageEx](/dotnet/api/microsoft.toolkit.uwp.ui.controls.imageex) control downloads images asynchronously, while showing a loading indicator. Source images are then stored in the application's local cache to preserve resources and load time. ImageEx also extends the default *Image* and *ImageBrush* Platform controls respectively to improve performance through caching. You can also use a placeholder image that will be displayed while loading the main image.

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://Controls?sample=ImageEx)

## Syntax

```xaml
<controls:ImageEx Name="ImageExControl" IsCacheEnabled="True"
    PlaceholderSource="/assets/thumbnails/thumbnails.png"
    Source="/assets/bigPicture.png" CornerRadius="20"/>
```

## Sample Output

![ImageEx animation](../resources/images/Controls/ImageEx.gif)

## ImageEx Properties

| Property | Type | Description |
| -- | -- | -- |
| NineGrid | Thickness | Gets or sets the nine-grid used by the image |
| IsCacheEnabled | bool | Gets or sets a value indicating whether gets or sets cache state |
| ImageExCachingStrategy | enum | Gets or sets a value indicating how the Image will be cached |
| CornerRadius | double | Get or set the radius of image corner |
| EnableLazyLoading | bool | Gets or sets a value indicating is lazy loading enabled. |
| LazyLoadingThreshold | double | Gets or sets a value indicating the threshold for triggering lazy loading. Default value is 300 px. |

## Sample Project

[ImageExControl Sample Page Source](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.0.0/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/ImageEx). You can [see this in action](uwpct://Controls?sample=ImageEx) in the [Windows Community Toolkit Sample App](https://aka.ms/windowstoolkitapp).

## Default Template

ImageEx control supports use of Progress Indicator. This can be enabled by adding ImageEx template from previous release of the control.

- [ImageEx Control with Progress Indicator XAML File](https://github.com/windows-toolkit/WindowsCommunityToolkit/blob/rel/2.2.0/Microsoft.Toolkit.Uwp.UI.Controls/ImageEx/ImageEx.xaml) is the XAML template used in v.2.2.0 of toolkit.

- [ImageEx Control XAML File](https://github.com/windows-toolkit/WindowsCommunityToolkit/blob/main/Microsoft.Toolkit.Uwp.UI.Controls.Core/ImageEx/ImageEx.xaml) is the XAML template used in the toolkit for the default styling.

## Requirements

| Device family | Universal, 10.0.16299.0 or higher |
| -- | -- |
| Namespace | Microsoft.Toolkit.Uwp.UI.Controls |
| NuGet package | [Microsoft.Toolkit.Uwp.UI.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI.Controls/) |

## API

- [ImageEx source code](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.0.0/Microsoft.Toolkit.Uwp.UI.Controls.Core/ImageEx)
