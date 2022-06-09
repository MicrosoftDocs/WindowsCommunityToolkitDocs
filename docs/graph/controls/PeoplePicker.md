---
title: PeoplePicker XAML Control
author: michael-hawker
description: The PeoplePicker control searches for people and renders the list of results from Microsoft Graph.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, people, peoplepicker, picker, graph
dev_langs:
  - csharp
---

# PeoplePicker XAML Control

The PeoplePicker searches for people and renders the list of results from Microsoft Graph. By default, the component will search across all people.

Available in the `CommunityToolkit.Graph.Uwp` package.

## Syntax

```xml
<Grid xmlns:controls="using:CommunityToolkit.Graph.Uwp.Controls">
    <controls:PeoplePicker />
</Grid>
```

## Sample Output

![PeoplePicker Control](../../resources/images/Graph/Controls/PeoplePicker.png)

## Properties

| Property | Type | Description |
| -- | -- | -- |
| PickedPeople | ObservableCollection&lt;Person&gt; | Gets the set of Person objects chosen by the user. |
| SuggestedPeople | ObservableCollection&lt;Person&gt; | Gets or sets collection of people suggested by the graph from the user's query. |

## Requirements

* **Namespace:** CommunityToolkit.Graph.Uwp.Controls
* **NuGet package:** [CommunityToolkit.Graph.Uwp](https://www.nuget.org/packages/CommunityToolkit.Graph.Uwp)

## API

* PeoplePicker source code `(https://github.com/windows-toolkit/Graph-Controls/tree/dev/7.1.0/CommunityToolkit.Graph.Uwp/Controls/PeoplePicker)`

## Related Topics

* [Person Graph API](/graph/api/resources/person)
* [MGT PeoplePicker Component](/graph/toolkit/components/people-picker)
