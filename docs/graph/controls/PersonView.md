---
title: PersonView XAML Control
author: michael-hawker
description: The PersonView control displays a person or contact's photo, name, and/or email address.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, personview, person, user, contact, graph
dev_langs:
  - csharp
---

# (Preview) PersonView XAML Control

The PersonView control is used to display a person or contact by using their photo, name, and/or email address.

Available in the `CommunityToolkit.Graph.Uwp` package.

## Syntax

```xml
<Grid xmlns:controls="using:CommunityToolkit.Graph.Uwp.Controls">
    <controls:PersonView PersonQuery="me" PersonViewType="OneLine" />
</Grid>
```

## Sample Output

![PersonView Control](../../resources/images/Graph/Controls/PersonView.png)

## Properties

| Property | Type | Description |
| -- | -- | -- |
| Initials | string | Gets the generated initials for the person. |
| IsLargeImage | bool | Value indicating if the image/circle size should be larger. |
| PersonDetails | Person | Details about this person retrieved from the graph or provided by the developer. |
| PersonQuery | string | Automatically retrieve data on the specified query from the graph.  Use 'me' to retrieve info about the current user.  Otherwise, it's best to use an e-mail address as a query. |
| PersonViewType | PersonViewType | Value indicating what type of details should be displayed: `Avatar`, `OneLine`, `TwoLine` |
| UserId | string | Gets or sets the UserId of the displayed person. |
| UserPhoto | BitmapImage | Gets or sets the displayed photo. |

## Requirements

* **Namespace:** CommunityToolkit.Graph.Uwp.Controls
* **NuGet package:** [CommunityToolkit.Graph.Uwp](https://www.nuget.org/packages/CommunityToolkit.Graph.Uwp)

## API

* [PersonView source code](https://github.com/windows-toolkit/Graph-Controls/tree/dev/7.1.0/CommunityToolkit.Graph.Uwp/Controls/PersonView)

## Related Topics

* [Person Graph API](/graph/api/resources/person)
* [MGT Person Component](/graph/toolkit/components/person)
