---
title: ListViewExtensions
author: nmetulev
description: ListViewExtensions extensions provide a lightweight way to extend every control that inherits the ListViewBase class with attached properties.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, ListViewBase, extensions
---

# ListViewExtensions

The [`ListViewExtensions`](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.uwp.ui.listviewextensions) class provide a lightweight way to extend every control that inherits the [`ListViewBase`](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.ListViewBase) class with attached properties. This means that all the extensions in this class can apply to both [`ListView`](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.listview), [`GridView`](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.gridview) and other controls.

> **Platform APIs:** [`ListViewExtensions`](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.uwp.ui.listviewextensions), [`ItemContainerStretchDirection`](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.uwp.ui.ItemContainerStretchDirection)

## AlternateColor

The `AlternateColor` property provides a way to assign a background color to every other item.

> [!WARNING]
> The [`ContainerContentChanging`](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.listviewbase#Windows_UI_Xaml_Controls_ListViewBase_ContainerContentChanging) event used for this extension to work, will not be raised when the [`ItemsPanel`](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemscontrol.itemspanel) is replaced with another type of panel than [`ItemsStackPanel`](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemsstackpanel) or [`ItemsWrapGrid`](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemswrapgrid).

Here is how this property can be used in XAML:

```xaml
<Page ...
     xmlns:ui="using:Microsoft.Toolkit.Uwp.UI">

<ListView
    ui:ListViewExtensions.AlternateColor="Silver"
    ItemsSource="{x:Bind MainViewModel.Items, Mode=OneWay}" />
```

## AlternateItemTemplate

The `AlternateItemTemplate` property provides a way to assign an alternate [`DataTemplate`](https://docs.microsoft.com/uwp/api/windows.ui.xaml.datatemplate) to every other item. It is also possible to combine with the `AlternateColor` property.

> [!WARNING]
> The [`ContainerContentChanging`](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.listviewbase#Windows_UI_Xaml_Controls_ListViewBase_ContainerContentChanging) event used for this extension to work, will not be raised when the [`ItemsPanel`](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemscontrol.itemspanel) is replaced with another type of panel than [`ItemsStackPanel`](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemsstackpanel) or [`ItemsWrapGrid`](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemswrapgrid).

Here is how this property can be used in XAML:

```xaml
<Page ...
     xmlns:ui="using:Microsoft.Toolkit.Uwp.UI">

<Page.Resources>
    <DataTemplate x:Name="NormalTemplate">
        <TextBlock Text="{Binding " Foreground="Green"></TextBlock>
    </DataTemplate>
    
    <DataTemplate x:Name="AlternateTemplate">
        <TextBlock Text="{Binding}" Foreground="Orange"></TextBlock>
    </DataTemplate>
</Page.Resources>

<ListView
    ItemTemplate="{StaticResource NormalTemplate}"
    ui:ListViewExtensions.AlternateItemTemplate="{StaticResource AlternateTemplate}"
    ItemsSource="{x:Bind MainViewModel.Items, Mode=OneWay}" />
```

## Command

`ListViewExtensions` provides extension method that allow attaching an [`ICommand`](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Input.ICommand) to handle `ListViewBase` item interaction by means of [`ItemClick`](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.listviewbase#Windows_UI_Xaml_Controls_ListViewBase_ItemClick) event.

> [!IMPORTANT]
> ListViewBase [`IsItemClickEnabled`](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.listviewbase#Windows_UI_Xaml_Controls_ListViewBase_IsItemClickEnabled) must be set to `true`.

Here is how this property can be used in XAML:

```xaml
<Page ...
     xmlns:ui="using:Microsoft.Toolkit.Uwp.UI">
     
<ListView
    ui:ListViewExtensions.Command="{x:Bind MainViewModel.ItemSelectedCommand, Mode=OneWay}"
    IsItemClickEnabled="True"
    ItemsSource="{x:Bind MainViewModel.Items, Mode=OneWay}"
    SelectionMode="None" />
```

## StretchItemContainerDirection

The `ItemContainerStretchDirection` property provides a way to stretch the `ItemContainer` in horizontal, vertical or both ways. The allowed values are items from the `ItemContainerStretchDirection` type.

> [!WARNING]
> The [`ContainerContentChanging`](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.listviewbase#Windows_UI_Xaml_Controls_ListViewBase_ContainerContentChanging) event used for this extension to work, will not be raised when the [`ItemsPanel`](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemscontrol.itemspanel) is replaced with another type of panel than [`ItemsStackPanel`](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemsstackpanel) or [`ItemsWrapGrid`](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.itemswrapgrid).

Here is how this property can be used from XAML:

```xaml
<Page ...
     xmlns:ui="using:Microsoft.Toolkit.Uwp.UI">

<ListView
    ui:ListViewExtensions.StretchItemContainerDirection="Horizontal"
    ItemsSource="{x:Bind MainViewModel.Items, Mode=OneWay}" />
```

## Examples

You can find more examples in the [unit tests](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/master/UnitTests).
