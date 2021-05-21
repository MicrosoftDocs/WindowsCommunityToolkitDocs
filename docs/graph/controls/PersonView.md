---
title: PersonView XAML Control
author: michael-hawker
description: The PersonView control displays a person or contact's photo, name, and/or email address.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, personview, person, user, contact, graph
dev_langs:
  - csharp
---

# (Preview) PersonView XAML Control

The [PersonView](/dotnet/api/microsoft.toolkit.graph.controls.personview) is used to display a person or contact by using their photo, name, and/or email address.

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://controls?sample=PersonView)

## Syntax

```xaml
  <wgt:PersonView PersonQuery="me" ShowEmail="True"/>
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
| ShowEmail | bool | Value indicating whether the user's email address should be displayed. |
| ShowName | bool | Value indicating whether the user's name should be displayed. |
| UserId | string | Gets or sets the UserId of the displayed person. |
| UserPhoto | BitmapImage | Gets or sets the displayed photo. |

## Sample Project

[PersonView sample page Source](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.0.0/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/PersonView). You can [see this in action](uwpct://Controls?sample=PersonView) in [Windows Community Toolkit Sample App](https://aka.ms/windowstoolkitapp).

## Requirements

| Device family | Universal, MinVersion or higher |
| -- | -- |
| Namespace | Microsoft.Toolkit.Graph.Controls |
| NuGet package | [Microsoft.Toolkit.Graph.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Graph.Controls) |

## API

* [PersonView source code](https://github.com/windows-toolkit/Graph-Controls/tree/rel/7.0.0/Microsoft.Toolkit.Graph.Controls/Controls/PersonView)

## Related Topics

* [Person Graph API](/graph/api/resources/person)
* [MGT Person Component](/graph/toolkit/components/person)
