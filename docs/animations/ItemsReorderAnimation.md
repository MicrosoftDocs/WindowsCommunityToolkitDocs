---
title: ItemsReorderAnimation
author: nmetulev
description: Provides the ability to assign a reorder animation to a items in any ListViewBase container.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, ItemsReorderAnimation
dev_langs:
  - csharp
---

# ItemsReorderAnimation

The [`ItemsReorderAnimation`](/dotnet/api/microsoft.toolkit.uwp.ui.animations.ItemsReorderAnimation) type allows your [`ListViewBase`](/uwp/api/windows.ui.xaml.controls.listviewbase) controls (such as [`ListView`](/uwp/api/windows.ui.xaml.controls.ListView) and [`GridView`](/uwp/api/windows.ui.xaml.controls.GridView)) to animate items into position when the size of the container changes.

> **Platform APIs:** [`ItemsReorderAnimation`](/dotnet/api/microsoft.toolkit.uwp.ui.animations.ItemsReorderAnimation)

## Syntax

The `ItemsReorderAnimation` type can be used directly from XAML like other attached properties:

```xaml
<Page ...
    xmlns:animations="using:Microsoft.Toolkit.Uwp.UI.Animations"/>
<GridView x:Name="MyGridView"
          animations:ItemsReorderAnimation.Duration="0:0:0.2"/>
```

This will add an animation with a duration of 200ms to all items in the target `GridView` control.

The `ItemsReorderAnimation` type can also be used directly from code behind, if necessary:

```csharp
ItemsReorderAnimation.SetValue(MyGridView, TimeSpan.FromMilliseconds(200));
```

Here is the visual result when using a `GridView` to display some images in a window being resized:

![ItemsReorderAnimation](../resources/images/Animations/ReorderGridAnimation/Sample-Output.gif)

## Examples

You can find more examples in the [sample app](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.1.0/Microsoft.Toolkit.Uwp.SampleApp).
