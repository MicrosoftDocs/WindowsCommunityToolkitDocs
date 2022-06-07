---
title: Carousel
author: nmetulev
description: The Carousel control inherits from ItemsControl, representing a nice and smooth carousel.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, carousel, xaml control, xaml
dev_langs:
  - csharp
  - vb
---

# Carousel

The [Carousel](/dotnet/api/microsoft.toolkit.uwp.ui.controls.carousel) control provides a new control, inherited from the [ItemsControl](/uwp/api/Windows.UI.Xaml.Controls.ItemsControl), representing a nice and smooth carousel.  
This control lets you specify a lot of properties for a flexible layouting.  
The `Carousel` control works fine with mouse, touch, mouse and keyboard as well.

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://Controls?sample=Carousel)

## Syntax

```xaml
<Page ...
    xmlns:controls="using:Microsoft.Toolkit.Uwp.UI.Controls"/>

<controls:Carousel InvertPositive="True" ItemDepth="300"
                   ItemMargin="0" ItemRotationX="0"
                   ItemRotationY="45" ItemRotationZ="0"
                   Orientation="Horizontal">
    <controls:Carousel.EasingFunction>
        <CubicEase EasingMode="EaseOut" />
    </controls:Carousel.EasingFunction>

    <controls:Carousel.ItemTemplate>
        <DataTemplate>
            <!-- Carousel content -->
        </DataTemplate>
    </controls:Carousel.ItemTemplate>
</controls:Carousel>
```

## Sample Output

![Carousel Overview](../resources/images/Controls/Carousel-Overview.gif)  

## Properties

| Property | Type | Description |
| -- | -- | -- |
| EasingFunction | EasingFunctionBase | Gets or sets easing function to apply for each Transition |
| InvertPositive | bool | Gets or sets a value indicating whether the items rendered transformations should be opposite compared to the selected item If false, all the items (except the selected item) will have the exact same transformations If true, all the items where index > selected index will have an opposite tranformation (Rotation X Y and Z will be multiply by -1) |
| ItemDepth | int | Gets or sets depth of non Selected Index Items |
| ItemMargin | int | Gets or sets the item margin |
| ItemRotationX | double | Gets or sets rotation angle on X |
| ItemRotationY | double | Gets or sets rotation angle on Y |
| ItemRotationZ | double | Gets or sets rotation angle on Z |
| Orientation | Orientation | Gets or sets the Carousel orientation. Horizontal or Vertical |
| SelectedIndex | int | Gets or sets selected Index |
| SelectedItem | object | Gets or sets the selected Item |
| TransitionDuration | int | Gets or sets duration of the easing function animation in ms |

## Events

| Events | Description |
| -- | -- |
| SelectionChanged | Occurs when the selected item has changed |

## Sample Project

[Carousel Sample Page Source](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.1.0/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/Carousel). You can [see this in action](uwpct://Controls?sample=Carousel) in the [Windows Community Toolkit Sample App](https://aka.ms/windowstoolkitapp).

## Default Template

[Carousel XAML File](https://github.com/CommunityToolkit/WindowsCommunityToolkit/blob/rel/7.1.0/Microsoft.Toolkit.Uwp.UI.Controls.Layout/Carousel/Carousel.xaml) is the XAML template used in the toolkit for the default styling.

## Requirements

| Device family | Universal, 10.0.16299.0 or higher |
| -- | -- |
| Namespace | Microsoft.Toolkit.Uwp.UI.Controls |
| NuGet package | [Microsoft.Toolkit.Uwp.UI.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI.Controls/) |

## API

* [Carousel source code](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.1.0/Microsoft.Toolkit.Uwp.UI.Controls.Layout/Carousel)
