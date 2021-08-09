---
title: AlignmentGrid XAML Control 
author: nmetulev
description: The AlignmentGrid Control can be used to display a grid to help aligning controls.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, AlignmentGrid, XAML Control, xaml
---

# AlignmentGrid XAML Control

The [AlignmentGrid Control](/dotnet/api/microsoft.toolkit.uwp.developertools.alignmentgrid) can be used to display a grid to help with aligning controls.

You can control the grid's steps with `HorizontalStep` and `VerticalStep` properties. Line color can be defined with `LineBrush` property.

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://Controls?sample=AlignmentGrid)

## Syntax

```xaml
<developerTools:AlignmentGrid Opacity="1" LineBrush="Black"
                    HorizontalStep="20" VerticalStep="20"/>
```

## Sample Output

![AlignmentGrid image](../resources/images/DeveloperTools/AlignmentGrid.jpg)

## Properties

| Property | Type | Description |
| -- | -- | -- |
| HorizontalStep | double | Gets or sets the step to use horizontally |
| LineBrush | Brush | Gets or sets line Brush |
| VerticalStep | double | Gets or sets the step to use vertically |

## Sample Project

[AlignmentGrid Sample Page Source](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.0.0/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/AlignmentGrid). You can [see this in action](uwpct://Controls?sample=AlignmentGrid) in the [Windows Community Toolkit Sample App](https://aka.ms/windowstoolkitapp).

## Requirements

| Device family | Universal, 10.0.16299.0 or higher |
| --- | --- |
| Namespace | Microsoft.Toolkit.Uwp.DeveloperTools |
| NuGet package | [Microsoft.Toolkit.Uwp.DeveloperTools](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.DeveloperTools/) |

## API

* [AlignmentGrid source code](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.0.0/Microsoft.Toolkit.Uwp.DeveloperTools/AlignmentGrid)
