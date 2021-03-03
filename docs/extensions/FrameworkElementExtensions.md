---
title: FrameworkElement Extensions
author: ST-Apps
description: FrameworkElementExtensions provides a simple way to bind to actual size for any FrameworkElement
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, FrameworkElement, extensions
---

# FrameworkElement Extensions

FrameworkElementExtensions provide helpers to bind to the actual size for any FrameworkElement or to bind to a parent value (to replace [RelativeSourceMode.FindAncestor](https://docs.microsoft.com/dotnet/api/system.windows.data.relativesourcemode)).

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://Extensions?sample=FrameworkElementExtensions)

## EnableActualSizeBinding

The EnableActualSizeBinding property allows you to enable/disable the binding for the ActualHeight and ActualWidth extensions.

## ActualHeight

The ActualHeight property allows to bind to TargetObject's ActualHeight.

### Example

```xaml
<Rectangle x:Name="TargetObject"
            extensions:FrameworkElementExtensions.EnableActualSizeBinding="true"/>
...
<TextBlock Text="{Binding ElementName=TargetObject, Path=(extensions:FrameworkElementExtensions.ActualHeight)}" />
```

## ActualWidth

The ActualWidth property allows to bind to TargetObject's ActualWidth.

## AncestorType

The `AncestorType` attached property will walk the VisualTree from the attached element for another element of the specified type.  That value will be stored in the attached element's `Ancestor` property.  This can then be used for binding to properties on the parent element.  This is similar to the [FindAncestor](https://docs.microsoft.com/dotnet/api/system.windows.data.relativesourcemode) mode to RelativeSource data binding in WPF.

### Example

```xaml
<Button ex:FrameworkElementExtensions.AncestorType="Grid"
        Visibility="{Binding (ex:FrameworkElementExtensions.Ancestor).Visibility,RelativeSource={RelativeSource Self}}"/>
```

## Ancestor

The `Ancestor` attached property stores the value discovered from the `AncestorType` result.

## Requirements (Windows 10 Device Family)

| [Device family](https://go.microsoft.com/fwlink/p/?LinkID=526370) | Universal, 10.0.16299.0 or higher |
| --- | --- |
| Namespace | Microsoft.Toolkit.Uwp.UI.Extensions |

## API

- [FrameworkElementEx source code](https://github.com/Microsoft/WindowsCommunityToolkit//blob/master/Microsoft.Toolkit.Uwp.UI/Extensions/FrameworkElement)

## Related Topics

- [RelativeSource.AncestorType (WPF)](https://docs.microsoft.com/dotnet/api/system.windows.data.relativesource.ancestortype)
- [RelativeSourceMode (WPF)](https://docs.microsoft.com/dotnet/api/system.windows.data.relativesourcemode)