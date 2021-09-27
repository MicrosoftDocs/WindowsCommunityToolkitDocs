---
title: GraphPresenter XAML Control
author: shweaver
description: The GraphPresenter control enables adhoc visualization of any Graph API.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, presenter, graphpresenter, graph
dev_langs:
  - csharp
---

# (Experimental) GraphPresenter XAML Control

The GraphPresenter is a flexible XAML control for visualizing Graph API data. Provide an `IBaseRequestBuilder` implementation and the GraphPresenter will automatically fetch the data from the proper Graph endpoint, ready for visualization. Because every Graph entity is different, this control has no default of UI of it's own. It is up to the developer to decide how the data should be presented by setting the control's `ContentTemplate`. This control is great for prototyping and experimentation purposes, but we suggest creating your own user controls for production scenarios.

Available in the `CommunityToolkit.Graph.Uwp` package.

## Syntax

### XAML

```xml
<!-- Display my recent OneDrive files. -->
<Grid xmlns:controls="using:CommunityToolkit.Graph.Uwp.Controls">
    <controls:GraphPresenter 
            RequestBuilder="{x:Bind RecentDriveItemsRequestBuilder, Mode=OneWay}"
            ResponseType="graph:DriveItem"
            IsCollection="True">
        <controls:GraphPresenter.ContentTemplate>
            <DataTemplate>
                <!-- Return result is a collection of DriveItem's as we used 'IsCollection', so bind that first. -->
                <ItemsControl ItemsSource="{Binding}">
                    <ItemsControl.ItemTemplate>
                        <DataTemplate x:DataType="graph:DriveItem">
                            <TextBlock Text="{Binding Name}" />
                        </DataTemplate>
                    </ItemsControl.ItemTemplate>
                </ItemsControl>
            </DataTemplate>
        </controls:GraphPresenter.ContentTemplate>
    </controls:GraphPresenter>
</Grid>
```

### Code-behind

```csharp
public IBaseRequestBuilder RecentDriveItemsRequestBuilder { get; set; }

public GraphPresenterSamplePage()
{
    InitializeComponent();

    ProviderManager.Instance.ProviderStateChanged += (s, e) => UpdateRequestBuilder();
    UpdateRequestBuilder();
}

private void UpdateRequestBuilder()
{
    var provider = ProviderManager.Instance.GlobalProvider;
    switch (provider?.State)
    {
        case ProviderState.SignedIn:
            RecentDriveItemsRequestBuilder = provider.GetClient().Me.Drive.Recent();
            break;

        default:
            RecentDriveItemsRequestBuilder = null;
            break;
    }
}
```

## Properties

| Property | Type | Description |
| -- | -- | -- |
| RequestBuilder | IBaseRequestBuilder | Used to make a request to the graph. The results will be automatically populated to the `ContentPresenter.ContentTemplate` property. Use a `ContentPresenter.ContentTemplate` to change the presentation of the data. |
| ResponseType | Type | The type of item returned by the `RequestBuilder`. |
| IsCollection | bool | A value indicating whether the returned data from the `RequestBuilder` is a collection. |
| QueryOptions | List&lt;QueryOption&gt; | A list of `QueryOption` values to pass into the request built by the `RequestBuilder`. |
| OrderBy | string | A string to indicate a sorting order for the `RequestBuilder`. This is a helper to add this specific request option to the `QueryOptions`.

## Requirements

* **Namespace:** CommunityToolkit.Graph.Uwp.Controls
* **NuGet package:** [CommunityToolkit.Graph.Uwp](https://www.nuget.org/packages/CommunityToolkit.Graph.Uwp)

## API

* [GraphPresenter source code](https://github.com/windows-toolkit/Graph-Controls/tree/main/CommunityToolkit.Graph.Uwp/Controls/GraphPresenter)

## Related Topics

* [MGT Get Component](/graph/toolkit/components/get)
