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


| Property              | Type            | Description                                                  |
| --------------------- | --------------- | ------------------------------------------------------------ |
| MinCroppedPixelLength | double          | Gets or sets the minimum cropped length(in pixel).           |
| MinSelectedLength     | double          | Gets or sets the minimum selectable length.                  |
| Source                | WriteableBitmap | Gets or sets the source of the cropped image.                |
| AspectRatio           | double?         | Gets or sets the aspect ratio of the cropped image，the default value is null. |
| CropShape             | CropShape       | Gets or sets the shape to use when cropping.                 |
| Mask                  | Brush           | Gets or sets the mask on the cropped image.                  |
| PrimaryThumbStyle     | Style           | Gets or sets a value for the style to use for the primary thumbs of the ImageCropper. |
| SecondaryThumbStyle   | Style           | Gets or sets a value for the style to use for the secondary thumbs of the ImageCropper. |
| ThumbPlacement        | ThumbPlacement  | Gets or sets a value for thumb placement.                    |


## Methods

| Methods                                         | Return Type           | Description                                                  |
| ----------------------------------------------- | --------------------- | ------------------------------------------------------------ |
| LoadImageFromFile(StorageFile)                  | Task                  | Load an image from a file.                                   |
| GetCroppedImageAsync()                          | Task<WriteableBitmap> | Gets the cropped image.                                      |
| SaveAsync(StorageFile,BitmapFileFormat)         | Task                  | Saves the cropped image to a file with the specified format. |
| SaveAsync(IRandomAccessStream,BitmapFileFormat) | Task                  | Saves the cropped image to a stream with the specified format. |
| Reset()                                         | void                  | Reset the cropped area.                                      |


## Examples

### Use ImageCropper
You can set the cropped image source by using the `LoadImageFromFile(StorageFile)` method or setting the `Source` property.

```csharp
//Load image.
await ImageCropper.LoadImageFromFile(file);
//Another way.
ImageCropper.Source = writeableBitmap;
//Gets the cropped image.
var writeableBitmap = await ImageCropper.GetCroppedImageAsync();
//Saves the cropped image to a file.
await ImageCropper.SaveAsync(imageFile, BitmapFileFormat.Png)
```

### Circular ImageCropper
You can set `CropShape` property to use a circular ImageCropper.

```csharp
ImageCropper.CropShape = CropShape.Circular;
```

### Image aspect ratio
You can set `AspectRatio` property to change the aspect ratio of the cropped image.

```csharp
ImageCropper.AspectRatio = 16d / 9d;
```
Or you can crop image without aspect ratio.

```csharp
ImageCropper.AspectRatio = null;
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
