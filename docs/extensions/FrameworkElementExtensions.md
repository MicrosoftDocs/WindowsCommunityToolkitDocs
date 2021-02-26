---
title: FrameworkElement Extensions
author: ST-Apps
description: Provides attached dependency properties and extensions for the FrameworkElement type.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, FrameworkElement, extensions
dev_langs:
  - csharp
  - vb
---

# FrameworkElement Extensions

[`FrameworkElementExtensions`](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.uwp.ui.frameworkelementextensions) provides a collection of attached dependency properties, helpers and extension methods to work with [`FrameworkElement`](https://docs.microsoft.com/uwp/api/windows.ui.xaml.frameworkelement) objects. In particular, it also includes a series of extension methods to explore the logical tree from a given UI element and find child or parent objects.

> **Platform APIs:** [`FrameworkElementExtensions`](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.uwp.ui.frameworkelementextensions), [`DependencyObjectExtensions`](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.uwp.ui.DependencyObjectExtensions)

## Logical tree extensions

The `FindChild` and `FindParent` methods (and their overloads) provide an easy way to explore the logical tree starting from a given `FrameworkElement` instance and find other controls connected to it.

These APIs differ from the *visual tree* extensions (in the [`DependencyObjectExtensions`](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.uwp.ui.DependencyObjectExtensions) class) where extra containers and styles can wrap other elements. The logical tree instead defines how controls are directly connected through construction. These methods can also be used on controls that aren't yet connected or rendered in the visual tree.

Here are some examples of how these extensions can be used:

```csharp
// Include the namespace to access the extensions
using Microsoft.Toolkit.Uwp.UI;

// Find a logical child control using its name
var control = uiElement.FindChild("MyTextBox");

// Find the first logical child control of a specified type
control = uiElement.FindChild<ListView>();

// Find all logical child controls of the specified type.
// The FindChildren extension will iterate through all the existing
// child nodes of the starting control, so here we also use the
// OfType<T>() LINQ extension (from System.Linq) to filter to a type.
foreach (var child in uiElement.FindChildren().OfType<ListViewItem>())
{
    // ...
}

// Find the first logical parent using its name
control = uiElement.FindParent("MyGrid");

// Find the first logical parent control of a specified type
control = uiElement.FindParent<Grid>();

// Retrieves the Content for the specified control from whatever its "Content" property may be
var content = uiElement.GetContentControl();
```
```vb
' Include the namespace to access the extensions
Imports Microsoft.Toolkit.Uwp.UI

' Find a logical child control using its name
Dim control = uiElement.FindChild("MyTextBox")

' Find the first logical child control of a specified type
control = uiElement.FindChild(Of ListView)()

' Find all the child nodes of a specified type. Like in the C# example,
' here we are also using a LINQ extension to filter the returned items.
For Each child In uiElement.FindChildren().OfType(Of ListViewItem)()
    ' ...
Next

' Find the first logical parent using its name
control = uiElement.FindParent("MyGrid")

' Find the first logical parent control of a specified type
control = uiElement.FindParent(Of Grid)()

' Retrieves the Content for the specified control from whatever its "Content" property may be
Dim content = uiElement.GetContentControl()
```

## EnableActualSizeBinding

The `EnableActualSizeBinding` property allows you to enable/disable the binding for the `ActualHeight` and `ActualWidth` extensions. The `ActualHeight` and `ActualWidth` properties then make it possible to bind to the `ActualHeight` and `ActualWidth` properties of a given object.

Here is an example of how the `ActualWidth` attached property can be used in a binding:

```xml
<Rectangle
    x:Name="TargetObject"
    ui:FrameworkElementExtensions.EnableActualSizeBinding="true"/>
...
<TextBlock Text="{Binding ElementName=TargetObject, Path=(ui:FrameworkElementExtensions.ActualHeight)}" />
```

## AncestorType

The `AncestorType` attached property will walk the visual tree from the attached element for another element of the specified type.  That value will be stored in the attached element's `Ancestor` property.  This can then be used for binding to properties on the parent element.  This is similar to the [`FindAncestor`](https://docs.microsoft.com/en-us/dotnet/api/system.windows.data.relativesourcemode) mode to [`RelativeSource`](https://docs.microsoft.com/dotnet/desktop/wpf/advanced/relativesource-markupextension) data binding in WPF.

Here is an example of how this can be used:

```xml
<Button
    ui:FrameworkElementExtensions.AncestorType="Grid"
    Visibility="{Binding (ui:FrameworkElementExtensions.Ancestor).Visibility,RelativeSource={RelativeSource Self}}"/>
```

## Examples

You can find more examples in the [unit tests](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/master/UnitTests).