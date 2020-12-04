---
title: PersonView XAML Control
author: michael-hawker
description: The PersonView control displays a person or contact's photo, name, and/or email address.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, personview, person, user, contact, graph
dev_langs:
  - csharp
---

# PersonView XAML Control

The [PersonView](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.graph.controls.personview) is used to display a person or contact by using their photo, name, and/or email address.

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

[PersonView sample page Source](https://github.com/Microsoft/WindowsCommunityToolkit//tree/master/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/PersonView). You can [see this in action](uwpct://Controls?sample=PersonView) in [Windows Community Toolkit Sample App](http://aka.ms/uwptoolkitapp).

## Requirements

| Device family | Universal, MinVersion or higher |
| -- | -- |
| Namespace | Microsoft.Toolkit.Graph.Controls |
| NuGet package | [Microsoft.Toolkit.Graph.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Graph.Controls) |

## API

* [PersonView source code](https://github.com/windows-toolkit/Graph-Controls/tree/master/Microsoft.Toolkit.Graph.Controls/Controls/PersonView)

## Related Topics

* [Person Graph API](https://docs.microsoft.com/en-us/graph/api/resources/person?view=graph-rest-beta)
* [MGT Person Component](https://docs.microsoft.com/graph/toolkit/components/person)
