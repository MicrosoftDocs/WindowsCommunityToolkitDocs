---
title: RadialProgressBar
author: nmetulev
description: The Radial Progress Bar Control displays a value in a certain range using a cicular sector that grows clockwise until it becomes a full ring.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, Radial Progress Bar, RadialProgressBar, xaml control, xaml
---

# RadialProgressBar

The [RadialProgressBar](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.uwp.ui.controls.radialprogressbar) control displays a value in a certain range using a circular sector that grows clockwise until it becomes a full ring.

The control uses the same dependency properties as the standard Progress Bar, with the addition of:

- A Thickness parameter, which sets the thickness of the circular sector and the outline it's drawn on
- An Outline property, which sets the brush of the circular outline

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://Controls?sample=RadialProgressBar)

## Syntax

```xaml
<Page ...
     xmlns:controls="using:Microsoft.Toolkit.Uwp.UI.Controls"/>

<controls:RadialProgressBar x:Name="RadialProgressBarControl"
	Value="70" Minimum="0" Maximum="180"
	Thickness="4" Outline="Gray" Foreground="Red">
</controls:RadialProgressBar>
```

## Sample Output

![RadialProgressBar image](../resources/images/Controls/RadialProgressBar.png)

## Properties

| Property | Type | Description |
| -- | -- | -- |
| Outline | Brush | Gets or sets the color of the circular outline on which the segment is drawn |
| Thickness | double | Gets or sets the thickness of the circular outline and segment |

## Sample Project

[RadialProgressBar Sample Page Source](https://github.com/Microsoft/WindowsCommunityToolkit//tree/master/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/RadialProgressBar). You can [see this in action](uwpct://Controls?sample=RadialProgressBar) in the [Windows Community Toolkit Sample App](https://aka.ms/uwptoolkitapp).

## Default Template

[RadialProgressBar XAML File](https://github.com/Microsoft/WindowsCommunityToolkit//blob/master/Microsoft.Toolkit.Uwp.UI.Controls/RadialProgressBar/RadialProgressBar.xaml) is the XAML template used in the toolkit for the default styling.

## Requirements

| Device family | Universal, 10.0.16299.0 or higher |
| -- | -- |
| Namespace | Microsoft.Toolkit.Uwp.UI.Controls |
| NuGet package | [Microsoft.Toolkit.Uwp.UI.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI.Controls/) |

## API

* [RadialProgressBar source code](https://github.com/Microsoft/WindowsCommunityToolkit//tree/master/Microsoft.Toolkit.Uwp.UI.Controls/RadialProgressBar)
