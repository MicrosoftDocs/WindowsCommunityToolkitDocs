---
title:  ScrollHeader
author: nmetulev
description: The ScrollHeader Control provides a header for ListViews or GridViews that adds the ability to keep its content visible or fade it out while scrolling down.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, ScrollHeader, XAML Control, xaml
---

# ScrollHeader

> [!WARNING]
> This control has been removed from the Windows Community Toolkit. Please use the behavior directly instead, either [`FadeHeaderBehavior`](/dotnet/api/microsoft.toolkit.uwp.ui.behaviors.fadeheaderbehavior), [`QuickReturnHeaderBehavior`](/dotnet/api/microsoft.toolkit.uwp.ui.behaviors.quickreturnheaderbehavior), or [`StickyHeaderBehavior`](/dotnet/api/microsoft.toolkit.uwp.ui.behaviors.stickyheaderbehavior).

The [ScrollHeader](/dotnet/api/microsoft.toolkit.uwp.ui.controls.scrollheader) control provides a header for ListViews or GridViews that adds the ability to keep its content visible or fade it out while scrolling down. It also has a quick return mode where the header hides when the ListView is scrolled down and reappears immediately as soon as the ListView is scrolled up again.

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://Controls?sample=ScrollHeader)

## Syntax

```xaml
<Page xmlns:controls="using:Microsoft.Toolkit.Uwp.UI.Controls" .../>

<ListView Name="listView" ItemsSource="{x:Bind _items, Mode=OneWay}">
    <ListView.Header>
        <controls:ScrollHeader Mode="Sticky">
            <TextBlock Text="Scroll Header" />
        </controls:ScrollHeader>
    </ListView.Header>
</ListView>

<!-- or -->

<GridView Name="gridView" ItemsSource="{x:Bind _items, Mode=OneWay}">
    <GridView.Header>
        <controls:ScrollHeader Mode="Sticky">
            <TextBlock Text="Scroll Header" />
        </controls:ScrollHeader>
    </GridView.Header>
</GridView>
```

## Sample Output

![ScrollHeader animation](../resources/images/Controls/ScrollHeader.gif)

## Properties

| Property | Type | Description |
| -- | -- | -- |
| Mode | [ScrollHeaderMode](/dotnet/api/microsoft.toolkit.uwp.ui.controls.scrollheadermode) | Gets or sets a value indicating whether the current mode. Default is none |
| TargetListViewBase | ListViewBase | Gets or sets the container this header belongs to |

## Sample Project

[ScrollHeader Sample Page Source](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.0.0/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/ScrollHeader). You can [see this in action](uwpct://Controls?sample=ScrollHeader) in the [Windows Community Toolkit Sample App](https://aka.ms/windowstoolkitapp).

## Default Template

[ScrollHeader XAML File](https://github.com/windows-toolkit/WindowsCommunityToolkit/blob/rel/7.0.0/Microsoft.Toolkit.Uwp.UI.Controls/ScrollHeader/ScrollHeader.xaml) is the XAML template used in the toolkit for the default styling.

## Requirements

| Device family | Universal, 10.0.16299.0 or higher |
| -- | -- |
| Namespace | Microsoft.Toolkit.Uwp.UI.Controls |
| NuGet package | [Microsoft.Toolkit.Uwp.UI.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI.Controls/) |

## API

* [ScrollHeader source code](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.0.0/Microsoft.Toolkit.Uwp.UI.Controls/ScrollHeader)
