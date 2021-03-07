---
title: FontIcon, FontIconSource, BitmapIcon markup extensions
author: sergio0694
description: The FontIcon, FontIconSource and BitmapIcon markup extensions allow developers to easily declare these types of icons directly from XAML in a compact manner.
keywords: windows 10, uwp, uwp community toolkit, uwp toolkit, nullable bool, dependency property, markup extension, XAML, markup 
---

# IconMarkupExtensions

The icon extensions are a group of markup extensions meant to simplify the creation of various icon types (specifically [`BitmapIcon`](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.BitmapIcon), [`BitmapIconSource`](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.BitmapIconSource), [`FontIcon`](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.FontIcon), [`FontIconSource`](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.FontIconSource), [`SymbolIcon`](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.SymbolIcon), and [`SymbolIconSource`](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.SymbolIconSource)) used across a variety of XAML controls. Using these extensions doesn't enable new capabilities per se, but it greatly simplifies the XAML syntax needed to create instances of these icon types. There are six such extensions available at the moment: `BitmapIconExtension`, `BitmapIconSourceExtension`, `FontIconExtension`, `FontIconSourceExtension`, `SymbolIconExtension` and `SymbolIconSourceExtension`.

## BitmapIcon

The [BitmapIcon markup extension](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.uwp.ui.extensions.bitmapiconextension) is similar in structure to the two previous extensions, but it produces `BitmapIcon` instances instead of font-based icons.

### Syntax

**XAML**

```xaml
<MenuFlyout>

    <!--Before-->
    <MenuFlyoutItem Text="Click me!">
        <MenuFlyoutItem.Icon>
            <BitmapIcon Source="/Assets/myicon.png"/>
        </MenuFlyoutItem.Icon>
    </MenuFlyoutItem>

    <!--After-->
    <MenuFlyoutItem
        Text="No, click me!"
        Icon="{ex:BitmapIcon Source=/Assets/myicon.png}" />
</MenuFlyout>
```

### Properties

| Property | Type | Description |
| -- | -- | -- |
| Source | Uri | The `Uri` representing the image to display. |
| ShowAsMonochrome | bool | Indicates whether to display the icon as monochrome. |

## BitmapIconSource

The [BitmapIconSource markup extension](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.uwp.ui.extensions.bitmapiconsourceextension) mirrors the `BitmapIconExtension` type, with the only difference being that it returns a [`BitmapIconSource`](https://docs.microsoft.com/uwp/api/microsoft.ui.xaml.controls.bitmapiconsource) instance..

### Syntax

**XAML**

```xaml
<SwipeItems Mode="Reveal">
    <SwipeItem Text="Send" IconSource="{ex:BitmapIconSource Source=/Assets/myicon.png}"/>
</SwipeItems>
```

### Properties

| Property | Type | Description |
| -- | -- | -- |
| Source | Uri | The `Uri` representing the image to display. |
| ShowAsMonochrome | bool | Indicates whether to display the icon as monochrome. |

## FontIcon

The [FontIcon markup extension](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.uwp.ui.extensions.fonticonextension) provides the ability to create `FontIcon` instances from XAML with a more compact representation than by explicitly creating a new `FontIcon` object to assign to the target property. The property also maps all the available `FontIcon` properties, so the two APIs expose the same set of customization options, just through a different XAML syntax.

### Syntax

**XAML**

```xaml
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

### Properties

| Property | Type | Description |
| -- | -- | -- |
| Glyph | string | The `string` representing the icon to display. |
| FontSize | double | The size of the icon to display. |
| FontFamily | FontFamily | The font family to use to display the icon. If `null`, "Segoe MDL2 Assets" will be used. |
| FontWeight | FontWeight | The thickness of the icon glyph. |
| FontStyle | FontStyle | The font style for the icon glyph. |
| IsTextScaleFactorEnabled | bool | Indicates whether automatic text enlargement, to reflect the system text size setting, is enabled. |
| MirroredWhenRightToLeft | bool | Indicates whether the icon is mirrored when the flow direction is right to left. |

## FontIconSource

The [FontIconSource markup extension](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.uwp.ui.extensions.fonticonsourceextension) mirrors the `FontIconExtension` type, but producing `FontIconSource` instances instead of `FontIcon`.

### Syntax

**XAML**

```xaml
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

### Properties

| Property | Type | Description |
| -- | -- | -- |
| Glyph | string | The `string` representing the icon to display. |
| FontSize | double | The size of the icon to display. |
| FontFamily | FontFamily | The font family to use to display the icon. If `null`, "Segoe MDL2 Assets" will be used. |
| FontWeight | FontWeight | The thickness of the icon glyph. |
| FontStyle | FontStyle | The font style for the icon glyph. |
| IsTextScaleFactorEnabled | bool | Indicates whether automatic text enlargement, to reflect the system text size setting, is enabled. |
| MirroredWhenRightToLeft | bool | Indicates whether the icon is mirrored when the flow direction is right to left. |

## SymbolIcon

The [SymbolIcon markup extension](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.uwp.ui.extensions.symboliconextension) mirrors the `FontIcon` markup extension, with the main difference being that it uses a [`Symbol`](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.symbol) value to specify the icon. All the other properties from `FontIconExtension` are available, with the exception of the font family, which is always set to "Segoe MDL2 Assets".

### Syntax

**XAML**

```xaml
<CommandBar>

    <!--Before-->
    <AppBarButton>
        <AppBarButton.Icon>
            <SymbolIcon Symbol="Play"/>
        </AppBarButton.Icon>
    </AppBarButton>

    <!--After-->
    <AppBarButton Icon="{ex:SymbolIcon Symbol=Play}"/>
</CommandBar>
```

### Properties

| Property | Type | Description |
| -- | -- | -- |
| Symbol | Symbol | The `Symbol` representing the icon to display. |
| FontSize | double | The size of the icon to display. |
| FontWeight | FontWeight | The thickness of the icon glyph. |
| FontStyle | FontStyle | The font style for the icon glyph. |
| IsTextScaleFactorEnabled | bool | Indicates whether automatic text enlargement, to reflect the system text size setting, is enabled. |
| MirroredWhenRightToLeft | bool | Indicates whether the icon is mirrored when the flow direction is right to left. |

> [!NOTE]
> The `SymbolIconExtension` actually returns a `FontIcon` value instead of a `SymbolIcon` one. This is done to include the additional properties (eg. `FontSize`, `FontWeight`, etc.) that would otherwise not have been available. When those are not modified, the look of the resulting icon will still be the same as the one that would've resulted from the use of a `SymbolIcon` instance.

## SymbolIconSource

The [SymbolIconSource markup extension](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.uwp.ui.extensions.symboliconsourceextension) is an alternative for `FontIconSourceExtension` that takes a `Symbol` value instead of a text, and displays the icon with the "Segoe MDL2 Assets". It's equivalent to the `SymbolIconExtension` type, except for the fact that it returns a [`FontIconSource`](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.fonticonsource) instance.

### Syntax

**XAML**

```xaml
<SwipeItems Mode="Reveal">
    <SwipeItem Text="Play" IconSource="{ex:SymbolIconSource Symbol=Play}"/>
</SwipeItems>
```

### Properties

| Property | Type | Description |
| -- | -- | -- |
| Symbol | Symbol | The `Symbol` representing the icon to display. |
| FontSize | double | The size of the icon to display. |
| FontWeight | FontWeight | The thickness of the icon glyph. |
| FontStyle | FontStyle | The font style for the icon glyph. |
| IsTextScaleFactorEnabled | bool | Indicates whether automatic text enlargement, to reflect the system text size setting, is enabled. |
| MirroredWhenRightToLeft | bool | Indicates whether the icon is mirrored when the flow direction is right to left. |

## Remarks

All the values returned by these markup extensions belong to the `Windows.UI.Xaml.*` namespace. This means that they will only work properly when used with controls from that namespace, and not from `Microsoft.UI.Xaml.*` (the WinUI namespace). For instance, trying to use the `FontIconSourceExtension` to set the `IconSource` property on the `Microsoft.UI.Xaml.Controls.SwipeItems` will not work correctly, as the extension will produce a `Windows.UI.Xaml.Controls.FontIconSource` value instead of a `Microsoft.UI.Xaml.Controls.FontIconSource` one. When working with WinUI controls, you'll need to manually declare the icons you need with the explicit XAML syntax.

## Requirements

| Device family | Universal, 10.0.16299.0 or higher   |
| -- | -- |
| Namespace | Microsoft.Toolkit.Uwp.UI.Extensions |
| NuGet package | [Microsoft.Toolkit.Uwp.UI](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI/) |

## API Source Code

- [BitmapIconExtension source code](https://github.com/Microsoft/WindowsCommunityToolkit//blob/master/Microsoft.Toolkit.Uwp.UI/Extensions/Markup/BitmapIconExtension.cs)
- [BitmapIconSourceExtension source code](https://github.com/Microsoft/WindowsCommunityToolkit//blob/master/Microsoft.Toolkit.Uwp.UI/Extensions/Markup/BitmapIconSourceExtension.cs)
- [FontIconExtension source code](https://github.com/Microsoft/WindowsCommunityToolkit//blob/master/Microsoft.Toolkit.Uwp.UI/Extensions/Markup/FontIconExtension.cs)
- [FontIconSourceExtension source code](https://github.com/Microsoft/WindowsCommunityToolkit//blob/master/Microsoft.Toolkit.Uwp.UI/Extensions/Markup/FontIconSourceExtension.cs)
- [SymbolIconExtension source code](https://github.com/Microsoft/WindowsCommunityToolkit//blob/master/Microsoft.Toolkit.Uwp.UI/Extensions/Markup/SymbolIconExtension.cs)
- [SymbolIconSourceExtension source code](https://github.com/Microsoft/WindowsCommunityToolkit//blob/master/Microsoft.Toolkit.Uwp.UI/Extensions/Markup/SymbolIconSourceExtension.cs)

## Related Topics

- [MarkupExtension Class](https://docs.microsoft.com/uwp/api/windows.ui.xaml.markup.markupextension)
