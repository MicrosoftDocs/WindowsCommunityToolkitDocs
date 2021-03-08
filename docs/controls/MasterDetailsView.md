---
title: MasterDetailsView XAML Control
author: nmetulev
description: The MasterDetailsView Control presents items in a master/details pattern.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, MasterDetailsView, XAML Control, xaml
---

# MasterDetailsView XAML Control 

The [MasterDetailsView Control](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.uwp.ui.controls.masterdetailsview) presents items in a master/details pattern. It shows a collection of items within the "master panel" and the details for that item within the "details panel". The MasterDetailsView reacts to the width it is given to determine if it should show both the master and details or just one of the two. There is a dependency property `ViewState` or an event `ViewStateChanged` that can be used to track which state the control is in.

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://Controls?sample=MasterDetailsView)

## Syntax

```xaml
<controls:MasterDetailsView
          ItemsSource="{Binding Items}"
          ItemTemplate="{StaticResource ListTemplate}"
          DetailsTemplate="{StaticResource DetailsTemplate}"
          NoSelectionContentTemplate="{StaticResource NoSelectionContentTemplate}"
          CompactModeThresholdWidth="720">
</controls:MasterDetailsView>
```

## Sample Output

![MasterDetailsView animation](../resources/images/Controls/MasterDetailsView.gif)

## BackButtonBehavior

When in compact mode, the MasterDetailsView will either show the Master or the Details view, not both. If an item is selected, the control will *navigate* forward to the Details view. If the CurrentItem is set to `null`, the control will navigate *back* to the Master view. 

If there is a Frame in the parent visual tree, the MasterDetailsView control will use the Frame navigation events to transition from the Details view to the Master view. If the host Frame is attempting back navigation while the Details view state is active, the MasterDetailsView will transition to the the Master view and cancel the back navigation.

To help with back navigation, The MasterDetailsView can handle back button visibility of the SystemNavigationManager back button, a parent NavigationView back button, or an inline back button. Use the `BackButtonehavior` property to control the behaviour:

- `Automatic` will let the control decide which back button to make visible/enabled.
  - If the system back button is visible the control won't use any other buttons
  - Else, if the control parent tree contains a Frame hosted in a NavigationView, the NavigationView back button will be used
  - Otherwise, an inline button will be used
- `System` will use the system back button controlled by the SystemNavigationManager. The control will make the button visible (if not already visible) when in the Details view and restore the visibility when transitioning to the Master view. This is the default value.
- `Inline` will use a back button built into the control
- `Manual` will not enable any back buttons (if using a custom button).

## Properties

| Property | Type | Description |
| -- | -- | -- |
| BackButtonBehavior | BackButtonBehavior | Gets or sets the behavior to use for the back button. |
| CompactModeThresholdWidth | double | If width of control is less than CompactModeThresholdWidth, the control will only display the master or details view - otherwise it will show both views. |
| DetailsCommandBar | CommandBar | Gets or sets the Windows.UI.Xaml.Controls.CommandBar for the details section |
| DetailsTemplate | DataTemplate | Gets or sets the DataTemplate used to display the details |
| DetailsHeader | object | Gets or sets the content for the details pane's header | 
| DetailsHeaderTemplate | DataTemplate | Gets or sets the DataTemplate used to display the content of the details pane's header |
| MapDetails | Func<object,object> | Gets or sets a function for mapping the selected item to a different model. This new model will be the DataContext of the Details area |
| MasterCommandBar | CommandBar | Gets or sets the Windows.UI.Xaml.Controls.CommandBar for the master section |
| MasterHeader | object | Gets or sets the content for the master pane's header |
| MasterHeaderTemplate | DataTemplate | Gets or sets the DataTemplate used to display the content of the master pane's header |
| MasterPaneBackground | Brush | Gets or sets the Brush to apply to the background of the list area of the control |
| MasterPaneWidth | double | Gets or sets the width of the master pane when the view is expanded |
| NoSelectionContent | object | Gets or sets the content to dsiplay when there is no item selected in the master list |
| NoSelectionContentTemplate | DataTemplate | Gets or sets the DataTemplate used to display the content when there is no selection |
| SelectedIndex | int | Gets or sets the selected index (-1 if nothing is selected) |
| SelectedItem | object | Gets or sets the selected item |
| ViewState | [MasterDetailsViewState](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.uwp.ui.controls.masterdetailsviewstate) | Gets the current visual state of the control |

## Events

| Events | Description |
| -- | -- |
| SelectionChanged | Occurs when the currently selected item changes |
| ViewStateChanged | Occurs when the view state changes |

## Sample Project

[MasterDetailsView Sample Page Source](https://github.com/Microsoft/WindowsCommunityToolkit//tree/master/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/MasterDetailsView). You can [see this in action](uwpct://Controls?sample=MasterDetailsView) in the [Windows Community Toolkit Sample App](https://aka.ms/uwptoolkitapp).

## Default Template 

[MasterDetailsView XAML File](https://github.com/Microsoft/WindowsCommunityToolkit//blob/master/Microsoft.Toolkit.Uwp.UI.Controls/MasterDetailsView/MasterDetailsView.xaml) is the XAML template used in the toolkit for the default styling.

## Requirements

| Device family | Universal, 10.0.16299.0 or higher |
| -- | -- |
| Namespace | Microsoft.Toolkit.Uwp.UI.Controls |
| NuGet package | [Microsoft.Toolkit.Uwp.UI.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI.Controls/) |

## API

- [MasterDetailsView source code](https://github.com/Microsoft/WindowsCommunityToolkit//tree/master/Microsoft.Toolkit.Uwp.UI.Controls/MasterDetailsView)
