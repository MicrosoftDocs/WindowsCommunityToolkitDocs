---
title: Attached Shadows
author: michael-hawker
description: Attached Shadows allow you to easily create a shadow effects on elements.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, your control name
dev_langs:
  - csharp
---

# Attached Shadows

Attached Shadows allow you to more easily create beautiful shadow effects within your app with little to no modification of the visual tree required, unlike our previous [`DropShadowPanel`](../controls/DropShadowPanel.md) control.

> **Platform APIs:** [`AttachedCardShadow`](/dotnet/api/microsoft.toolkit.uwp.ui.media.attachedcardshadow), [`AttachedDropShadow`](/dotnet/api/microsoft.toolkit.uwp.ui.attacheddropshadow)

## Introduction

There are two types of attached shadows available today, the `AttachedCardShadow` and the `AttachedDropShadow`. It is recommended to use the `AttachedCardShadow` where possible, if you don't mind the dependency on Win2D. The `AttachedCardShadow` provides an easier to use experience that is more performant and easier to apply across an entire set of elements, assuming those elements are rounded-rectangular in shape.

The following table outlines the various capabilities of each shadow type in addition to comparing to the previous `DropShadowPanel` implementation:

| Capability                    | AttachedCardShadow                                                 | AttachedDropShadow                                              | DropShadowPanel (deprecated)                                                              |
|-------------------------------|--------------------------------------------------------------------|-----------------------------------------------------------------|-----------------------------------------------------------------------------------------|
| Dependency/NuGet Package      | 🟡 Win2D via<br>`Microsoft.Toolkit.Uwp.UI.Media`                       | ✅ UWP Only (Composition Effect)<br>`Microsoft.Toolkit.Uwp.UI`  | ✅ UWP Only (Composition Effect)<br>`Microsoft.Toolkit.Uwp.UI`                              |
| Layer                         | Inline Composition +<br>Win2D Clip Geometry                           | Composition via<br>Target Element Backdrop                         | Composition via<br>`ContentControl` Container                                                |
| Modify Visual Tree            | ✅ No                                                              | 🟡 Usually requires single target element, even for multiple shadows    | ❌ Individually wrap each element needing shadow                                         |
| Extra Visual Tree Depth       | ✅ 0                                                               | 🟡 1 per sibling element to cast one or more shadows to          | ❌ _**4** per Shadowed Element_                                                                |
| Masking/Geometry              | 🟡 Rectangular/Rounded-Rectangles only                               | ✅ Can mask images, text, and shapes (performance penalty)     | ✅ Can mask images, text, and shapes (performance penalty)                                 |
| Performance                   | ✅ Fast, applies rectangular clipped geometry                       | 🟡 Slower, especially when masking (default);<br>can use rounded-rectangles optimization                  | ❌ Slowest, no optimization for rounded-rectangles                                                     |
| ResourceDictionary Support    | ✅ Yes                                                              | ✅ Yes                                                           | ❌ Limited, via complete custom control style +<br>still need to wrap each element to apply |
| Usable in Styles              | ✅ Yes, anywhere, including app-level                               | 🟡 Yes, but limited to page-scope due to element target | ❌ No                                                                                    |
| Supports Transparent Elements | ✅ Yes, shadow is clipped and not visible                           | ❌ No, shadow shows through transparent element                  | ❌ No, shadow shows through transparent element                                          |
| Animation Support             | ✅ Yes, in XAML via [`AnimationSet`](../animations/AnimationSet.md) | 🟡 Partial, translating/moving element may desync shadow         | ❌ No                                                                                    |

## AttachedCardShadow (Win2D)

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://controls?sample=attachedcardshadowwin2d) <!-- TODO: Don't know what magic we need here, probably () throwing it -->

## AttachedDropShadow (Composition)

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://controls?sample=attacheddropshadowcomposition)

## Example

```xaml
     <Rectangle RadiusX="32" RadiusY="32"
                Height="100" Width="100"
                Stroke="Blue" StrokeThickness="1">
        <Rectangle.Fill>
            <ImageBrush ImageSource="ms-appx:///Assets/Photos/Owl.jpg"/>
        </Rectangle.Fill>
        <ui:Effects.Shadow>
            <media:AttachedCardShadow BlurRadius="8"
                                      CornerRadius="32"
                                      Color="Black"
                                      Offset="4,4"
                                      Opacity="1"/>
        </ui:Effects.Shadow>
    </Rectangle>
```

## Example Output

![Alt Text of Image (not same as filename)](../resources/images/filename.png)

## Sample Project

[control/helper name sample page Source](sample-page-link). You can [see this in action](uwpct://CategoryName?sample=pageName) in [Windows Community Toolkit Sample App](https://aka.ms/windowstoolkitapp).

## Source Code

- [control/helper name source code](source-code-link)

## Related Topics

- [Topic 1](link)
- [Topic 2](link)
