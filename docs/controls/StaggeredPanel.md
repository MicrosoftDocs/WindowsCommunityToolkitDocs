---
title: StaggeredPanel
author: skendrot
description: Learn about the StaggeredPanel control. This control arranges child elements into a staggered grid pattern.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, StaggeredPanel 
---

# StaggeredPanel

The [StaggeredPanel](/dotnet/api/microsoft.toolkit.uwp.ui.controls.staggeredpanel) allows for layout of items in a column approach where an item will be added to whichever column has used the least amount of space.

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://Controls?sample=StaggeredPanel)

## Syntax

**XAML**

```xaml
<ItemsControl>
    <ItemsControl.ItemTemplate>
        <DataTemplate>
            <Image Source="{Binding Thumbnail}"/>
        </DataTemplate>
    </ItemsControl.ItemTemplate>
    <ItemsControl.ItemsPanel>
        <ItemsPanelTemplate>
            <controls:StaggeredPanel/>
        </ItemsPanelTemplate>
    </ItemsControl.ItemsPanel>
</ItemsControl>
```

## Sample Output

![StaggeredPanel](../resources/images/Controls-StaggeredPanel.jpg "StaggeredPanel")

## Properties

| Property | Type | Description |
| -- | -- | -- |
| ColumnSpacing | double  | Gets or sets the distance between columns |
| DesiredColumnWidth | double | The desired width of each column. The width of columns can exceed the DesiredColumnWidth if the HorizontalAlignment is set to Stretch. |
| Padding | Thickness | The dimensions of the space between the edge and its child as a Thickness value. Thickness is a structure that stores dimension values using pixel measures. |
| RowSpacing | double  | Gets or sets the vertical distance between items |

## Sample Project

[StaggeredPanel Sample Page](https://github.com/Microsoft/WindowsCommunityToolkit//tree/master/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/StaggeredPanel). You can [see this in action](uwpct://Controls?sample=StaggeredPanel) in the [Windows Community Toolkit Sample App](http://aka.ms/uwptoolkitapp).

## Default Template

[StaggeredPanel XAML File](https://github.com/Microsoft/WindowsCommunityToolkit//blob/master/Microsoft.Toolkit.Uwp.UI.Controls/StaggeredPanel/StaggeredPanel.xaml) is the XAML template used in the toolkit for the default styling.

## Requirements

| [Device family](/windows/uwp/get-started/universal-application-platform-guide#device-families) | Universal, 10.0.16299.0 or higher   |
| -- | -- |
| Namespace | Microsoft.Toolkit.Uwp.UI.Controls |
| NuGet package | [Microsoft.Toolkit.Uwp.UI.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI.Controls/) |

## API

- [StaggeredPanel](https://github.com/Microsoft/WindowsCommunityToolkit//tree/master/Microsoft.Toolkit.Uwp.UI.Controls/StaggeredPanel)