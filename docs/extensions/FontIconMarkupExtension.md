---
title: FontIcon, FontIconSource, BitmapIcon markup extensions
author: sergio0694
description: The FontIcon, FontIconSource and BitmapIcon markup extensions allow developers to easily declare these types of icons directly from XAML in a compact manner.
keywords: windows 10, uwp, uwp community toolkit, uwp toolkit, nullable bool, dependency property, markup extension, XAML, markup 
---

# FontIcon markup extension
The [FontIcon markup extension](https://docs.microsoft.com/en-us/dotnet/api/microsoft.toolkit.uwp.ui.extensions.fonticonextension) provides the ability to create `FontIcon` instances from XAML with a more compact representation than by explicitly creating a new `FontIcon` object to assign to the target property. The property also mapps all the available `FontIcon` properties, so the two APIs expose the same set of customization options, just through a different XAML syntax.

## Syntax

**XAML**

```xml
<CommandBar>

    <!--Before-->
    <AppBarButton>
        <AppBarButton.Icon>
            <FontIcon Glyph="&#xE102;" FontFamily="Segoe MDL2 Assets"/>
        </AppBarButton.Icon>
    </AppBarButton>

    <!--After-->
    <AppBarButton Icon="{ex:FontIcon Glyph=&#xE102;}"/>
</CommandBar>
```

## Properties

| Property | Type | Description |
| -- | -- | -- |
| Glyph | string | The `string` representing the icon to display. |
| FontSize | double | The size of the icon to display. |
| FontFamily | FontFamily | The font family to use to display the icon. If `null`, "Segoe MDL2 Assets" will be used. |
| FontWeight | FontWeight | The thickness of the icon glyph. |
| FontStyle | FontStyle | The font style for the icon glyph. |
| IsTextScaleFactorEnabled | bool | Indicates whether automatic text enlargement, to reflect the system text size setting, is enabled. |
| MirroredWhenRightToLeft | bool | Indicates whether the icon is mirrored when the flow direction is right to left. |

# FontIconSource markup extension
The [FontIconSource markup extension](https://docs.microsoft.com/en-us/dotnet/api/microsoft.toolkit.uwp.ui.extensions.fonticonsourceextension) mirrors the `FontIconExtension` type, but producing `FontIconSource` instances instead of `FontIcon`.

## Syntax

**XAML**

```xml
<SwipeItems Mode="Reveal">

    <!--Before-->
    <SwipeItem Text="Accept">
        <SwipeItem.IconSource>
            <FontIconSource Glyph="&#xE10B;"/>
        </SwipeItem.IconSource>
    </SwipeItem>
    
    <!--After-->
    <SwipeItem Text="Accept" IconSource="{ex:FontIconSource Glyph=&#xE10B;}"/>
</SwipeItems>
```

## Properties

| Property | Type | Description |
| -- | -- | -- |
| Glyph | string | The `string` representing the icon to display. |
| FontSize | double | The size of the icon to display. |
| FontFamily | FontFamily | The font family to use to display the icon. If `null`, "Segoe MDL2 Assets" will be used. |
| FontWeight | FontWeight | The thickness of the icon glyph. |
| FontStyle | FontStyle | The font style for the icon glyph. |
| IsTextScaleFactorEnabled | bool | Indicates whether automatic text enlargement, to reflect the system text size setting, is enabled. |
| MirroredWhenRightToLeft | bool | Indicates whether the icon is mirrored when the flow direction is right to left. |

## Requirements

| Device family | Universal, 10.0.16299.0 or higher   |
| -- | -- |
| Namespace | Microsoft.Toolkit.Uwp.UI.Extensions |
| NuGet package | [Microsoft.Toolkit.Uwp.UI](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI/) |

## API Source Code

- [FontIconExtension source code](https://github.com/Microsoft/WindowsCommunityToolkit//blob/master/Microsoft.Toolkit.Uwp.UI/Extensions/Markup/FontIconExtension.cs)

## Related Topics

- [MarkupExtension Class](https://docs.microsoft.com/en-us/uwp/api/windows.ui.xaml.markup.markupextension)
