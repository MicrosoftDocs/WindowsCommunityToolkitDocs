---
title: UIElement Extensions
author: vgromfeld
description: UIElementExtensions provides a simple way to extend the UIElement
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, UIElement, extensions
---

# UIElement Extensions

`UIElementExtensions` provides helpers for `UIElement`.

## ClipToBounds

The `ClipToBounds` property allows you to indicate whether to clip the content of this element (or content coming from the child elements of this element) to fit into the size of the containing element.

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://Extensions?sample=ClipToBounds)

### Example

```xaml
<Grid
    BorderBrush="White"
    BorderThickness="1"
    Width="148"
    Height="148"
    extensions:UIElementExtensions.ClipToBounds="True">
    <!-- We translate the inner rectangles outside of the bounds of the container. -->
    <Rectangle Fill="Blue" Width="100" Height="100">
        <Rectangle.RenderTransform>
            <TranslateTransform X="-50" Y="-50" />
        </Rectangle.RenderTransform>
    </Rectangle>
    <Rectangle Fill="Green" Width="100" Height="100">
        <Rectangle.RenderTransform>
            <TranslateTransform X="50" Y="50" />
        </Rectangle.RenderTransform>
    </Rectangle>
</Grid>

```

## Requirements (Windows 10 Device Family)

| [Device family](http://go.microsoft.com/fwlink/p/?LinkID=526370) | Universal, 10.0.16299.0 or higher |
| --- | --- |
| Namespace | Microsoft.Toolkit.Uwp.UI.Extensions |
| NuGet package | [Microsoft.Toolkit.Uwp.UI](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI/) |

## API

- [UIElementExtensions source code](https://github.com/Microsoft/WindowsCommunityToolkit//blob/master/Microsoft.Toolkit.Uwp.UI/Extensions/UIElement)

## Related Topics

- [UIElement.ClipToBounds Property (WPF)](https://docs.microsoft.com/en-us/dotnet/api/system.windows.uielement.cliptobounds?view=netframework-4.8)
