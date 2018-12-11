---
title: ImageCropper
author: HHChaos
description: ImageCropper control allows user to crop image freely.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, ImageCropper
dev_langs:
  - csharp
---

# ImageCropper XAML Control

The [ImageCropper Control](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.uwp.ui.controls.imagecropper) allows user to crop image freely.

## Syntax

```xaml
<Page ...
     xmlns:controls="using:Microsoft.Toolkit.Uwp.UI.Controls"/>
    <controls:ImageCropper x:Name="ImageCropper" />
</controls:DropShadowPanel>
```

## Sample Output

![ImageCropper animation](../resources/images/Controls/ImageCropper.gif)

## Properties


| Property | Type | Description |
| -- | -- | -- |
| MinCroppedPixelLength | double | Gets or sets the minimum cropped length(in pixel). |
| MinSelectedLength | double | Gets or sets the minimum selectable length. |
| Source | WriteableBitmap |  Gets or sets the source of the cropped image. |
| AspectRatio | double | Gets or sets the aspect ratio of the cropped image，the default value is -1. |
| CircularCrop | bool | Gets or sets a value indicating whether gets or sets whether to use a circular ImageCropper. |
| Mask | Brush | Gets or sets the mask on the cropped image. |
| PrimaryThumbStyle | Style | Gets or sets a value for the style to use for the primary thumbs of the ImageCropper. |
| SecondaryThumbStyle | Style | Gets or sets a value for the style to use for the secondary thumbs of the ImageCropper. |
| IsSecondaryThumbVisible | bool | Gets or sets a value indicating whether secondary thumbs is displayed. |


## Methods

| Methods | Return Type | Description |
| -- | -- | -- |
| LoadImageFromFile(StorageFile)| Task | Load an image from a file. |
| GetCroppedBitmapAsync() | Task<WriteableBitmap> | The cropped image. |


## Examples

### Circular ImageCropper
You can set `CircularCrop` property to use a circular ImageCropper.
```csharp
ImageCropper.CircularCrop = true;
```
### Image aspect ratio
You can set `AspectRatio` property to change the aspect ratio of the cropped image.

```csharp
ImageCropper.AspectRatio = 16d / 9d;
```
Or you can crop image without aspect ratio.

```csharp
ImageCropper.AspectRatio = -1;
```
### SecondaryControlButton
You can set `IsSecondaryThumbVisible` property to display the secondary control buttons, can also set `IsSecondaryThumbVisible` property to change the style of the secondary control buttons.

```csharp
ImageCropper.IsSecondaryThumbVisible = true;
```

## Sample Code

[ImageCropper Sample Page Source](https://github.com/Microsoft/WindowsCommunityToolkit//tree/master/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/ImageCropper). You can see this in action in [Windows Community Toolkit Sample App](https://www.microsoft.com/store/apps/9NBLGGH4TLCQ).

## Default Template 

[ImageCropper XAML File](https://github.com/Microsoft/WindowsCommunityToolkit//blob/master/Microsoft.Toolkit.Uwp.UI.Controls/ImageCropper/ImageCropper.xaml) is the XAML template used in the toolkit for the default styling.

## Requirements

| Device family | Universal, MinVersion or higher   |
| -- | -- |
| Namespace | Microsoft.Toolkit.Uwp.UI.Controls |
| NuGet package | [NuGet package](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI.Controls/) |
## API Source Code

- [ImageCropper source code](https://github.com/Microsoft/WindowsCommunityToolkit//tree/master/Microsoft.Toolkit.Uwp.UI.Controls/ImageCropper)
