---
title: PeoplePicker XAML Control
author: michael-hawker
description: The PeoplePicker control searches for people and renders the list of results from Microsoft Graph.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, people, peoplepicker, picker, graph
dev_langs:
  - csharp
---

# (Preview) PeoplePicker XAML Control

The [PeoplePicker](/dotnet/api/microsoft.toolkit.graph.controls.peoplepicker) searches for people and renders the list of results from Microsoft Graph. By default, the component will search across all people.

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://controls?sample=PeoplePicker)

## Syntax

```xaml
  <wgt:PeoplePicker/>
```

## Sample Output

![PeoplePicker Control](../../resources/images/Graph/Controls/PeoplePicker.png)

## Properties

| Property | Type | Description |
| -- | -- | -- |
| PickedPeople | ObservableCollection\<Person> | Gets the set of Person objects chosen by the user. |
| SuggestedPeople | ObservableCollection\<Person> | Gets or sets collection of people suggested by the graph from the user's query. |

## Sample Project

[PeoplePicker sample page Source](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.0.0/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/PeoplePicker). You can [see this in action](uwpct://Controls?sample=PeoplePicker) in [Windows Community Toolkit Sample App](https://aka.ms/windowstoolkitapp).

## Requirements

| Device family | Universal, MinVersion or higher |
| -- | -- |
| Namespace | Microsoft.Toolkit.Graph.Controls |
| NuGet package | [Microsoft.Toolkit.Graph.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Graph.Controls) |

## API

* [PeoplePicker source code](https://github.com/windows-toolkit/Graph-Controls/tree/rel/7.0.0/Microsoft.Toolkit.Graph.Controls/Controls/PeoplePicker)

## Related Topics

* [Person Graph API](/graph/api/resources/person)
* [MGT PeoplePicker Component](/graph/toolkit/components/people-picker)
