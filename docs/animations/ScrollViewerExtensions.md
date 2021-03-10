---
title: ScrollViewerExtensions (animations)
author: Sergio0694
description: The ScrollViewerExtensions type provides helper methods to handle expression animations on ScrollViewer controls.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, ScrollViewer, extentions
---

# ScrollViewerExtensions (animations)

The [`ScrollViewerExtensions`](/dotnet/api/microsoft.toolkit.uwp.ui.animations.scrollviewerextensions) type from the `Microsoft.Toolkit.Uwp.UI.Animations` package provides helper methods to handle expression animations on [`ScrollViewer`](/uwp/api/windows.ui.xaml.controls.scrollviewer) controls.

> **Platform APIs:** [`ScrollViewerExtensions`](/dotnet/api/microsoft.toolkit.uwp.ui.animations.scrollviewerextensions)

## Expression animations

The `StartExpressionAnimation` methods provide a way to easily start a composition expression animation to sync a `ScrollViewer` instance with another control. This binds the manipulation status on a `ScrollViewer` property set with either the translation or the offset of another visual element, to follow or mirror the motion in the source `ScrollViewer`.

### Example

```xaml
<Grid>

    <!--This is a ListView we can use to display a series of items. It will
        contain the ScrollViewer that will be targeted by the expression animation.-->
    <ListView Name="listView">
      <ListView.ItemTemplate>
        <DataTemplate>
            <Image Width="100"
                   Height="100"
                   Source="ms-appx:///Assets/ToolkitLogo.png" />
        </DataTemplate>
      </ListView.ItemTemplate>
    </ListView>

    <!--This is the panel that will be animated in sync with the main ScrollViewer control
        inside the ListView in the page, using the ScrollViewerExtensions leveraging composition
        ExpressionAnimations. Note how the panel is not inside the ListView, but it's just
        rendering "fixed" items right on top of the ListView. We can use the expression animation
        to "bind" the scrolling of the ListView and keep the panel "in sync" with it.-->
    <StackPanel x:Name="shapesPanel">
      <Polygon Height="100"
               Width="100"
               Points="0,0 0,72 44,36"
               Stroke="DarkGreen"
               Fill="Green"
               VerticalAlignment="Center"
               HorizontalAlignment="Center"/>
    </StackPanel>
  </Grid>
```

```csharp
using Microsoft.Toolkit.Uwp.UI.Animations;

ScrollViewer scrollViewer = listView.FindDescendant<ScrollViewer>();

// Binds the Y scroll axis of the ScrollViewer to the Y translation axis of the target
listScrollViewer.StartExpressionAnimation(shapesPanel, Axis.Y);

// It is also possible to synchronize different axes, as well as targeting
// different Visual properties. By default, the expression works with the
// Visual.Translate property, but Visual.Offset can be used as well.
listScrollViewer.StartExpressionAnimation(shapesPanel, Axis.X, Axis.Y, VisualProperty.Offset);
```

### Sample output

![Expression Animations](../resources/images/Extensions/ScrollViewerExpressionAnimation.gif)

## Examples

You can find more examples in the [unit tests](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.0.0/UnitTests).
