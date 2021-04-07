---
title: RangeSelector
author: nmetulev
description: The RangeSelector Control is a Double Slider control that allows the user to select a sub-range of values from a larger range of possible values.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, RangeSelector, XAML Control, xaml, double slider
dev_langs:
  - csharp
  - vb
---

# RangeSelector

The [RangeSelector](/dotnet/api/microsoft.toolkit.uwp.ui.controls.rangeselector) control is a Double Slider control that allows the user to select a sub-range of values from a larger range of possible values.  The user can slide from the left or right of the range.

> **Platform APIs:** [`RangeSelector`](dotnet/api/microsoft.toolkit.uwp.ui.controls.rangeselector)

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://Controls?sample=RangeSelector)

## Syntax

```xaml
<Page ...
    xmlns:controls="using:Microsoft.Toolkit.Uwp.UI.Controls"/>

<controls:RangeSelector x:Name="RangeSelectorControl"
    Minimum="10"
    Maximum="100"
    StepFrequency="2">
</controls:RangeSelector>
```

## Example Output

![RangeSelector animation](../resources/images/Controls/RangeSelector.gif)

## Example

> [!NOTE]
> If you are using a RangeSelector within a ScrollViewer you'll need to add some codes. This is because by default, the ScrollViewer will block the thumbs of the RangeSelector to capture the pointer.

Here is an example of using RangeSelector within a ScrollViewer

```xaml
<controls:RangeSelector x:Name="Selector" ThumbDragStarted="Selector_OnDragStarted" ThumbDragCompleted="Selector_OnDragCompleted"/>
```

```csharp
private void Selector_OnDragStarted(object sender, DragStartedEventArgs e)
{
 ScrollViewer.HorizontalScrollMode = ScrollMode.Disabled;
 ScrollViewer.VerticalScrollMode = ScrollMode.Disabled;
}

private void Selector_OnDragCompleted(object sender, DragCompletedEventArgs e)
{
 ScrollViewer.HorizontalScrollMode = ScrollMode.Auto;
 ScrollViewer.VerticalScrollMode = ScrollMode.Auto;
}
```

```vb
Private Sub Selector_OnDragStarted(ByVal sender As Object, ByVal e As DragStartedEventArgs)
 ScrollViewer.HorizontalScrollMode = ScrollMode.Disabled
 ScrollViewer.VerticalScrollMode = ScrollMode.Disabled
End Sub

Private Sub Selector_OnDragCompleted(ByVal sender As Object, ByVal e As DragCompletedEventArgs)
 ScrollViewer.HorizontalScrollMode = ScrollMode.Auto
 ScrollViewer.VerticalScrollMode = ScrollMode.Auto
End Sub
```

## Sample Project

[RangeSelector Sample Page Source](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.0.0/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/RangeSelector). You can [see this in action](uwpct://Controls?sample=RangeSelector) in the [Windows Community Toolkit Sample App](https://aka.ms/windowstoolkitapp).

## Default Template

[RangeSelector XAML File](https://github.com/windows-toolkit/WindowsCommunityToolkit/blob/rel/7.0.0/Microsoft.Toolkit.Uwp.UI.Controls/RangeSelector/RangeSelector.xaml) is the XAML template used in the toolkit for the default styling.

## Source code

* [RangeSelector source code](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.0.0/Microsoft.Toolkit.Uwp.UI.Controls.Input/RangeSelector)
