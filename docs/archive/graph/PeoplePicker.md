---
title: PeoplePicker Control
author: OGcanviz
description: The PeoplePicker Control is a simple control that allows for selection of one or more users from an organizational AD (outdated docs).
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, PeoplePicker Control
---

# PeoplePicker Control

> [!WARNING]
> (This API has been removed. For the latest guidance on using the Microsoft Graph see the new [PeoplePicker](../../graph/controls/PeoplePicker.md) control.)

The [PeoplePicker Control](/dotnet/api/microsoft.toolkit.uwp.ui.controls.graph.peoplepicker) is a simple control that allows for selection of one or more users from an organizational AD, see more details [here](/graph/people-example), it relies on the [MicrosoftGraphService](../../services/MicrosoftGraph.md) for authentication.

## Syntax

```xaml
<Page ...
    xmlns:controls="using:Microsoft.Toolkit.Uwp.UI.Controls.Graph"/>

<controls:PeoplePicker x:Name="PeoplePicker1"
    AllowMultiple="True" />
```

## Example Image

![PeoplePicker animation](../../resources/images/Graph/PeoplePicker.png)

## Properties

|           Property           |             Type             |                                    Description                                    |
|------------------------------|------------------------------|-----------------------------------------------------------------------------------|
| RequiredDelegatedPermissions |           String[]           |             Gets required delegated permissions for Graph API access              |
|           GroupId            |            String            | Search people in this group if specified, otherwise, search the organizational AD |
|        AllowMultiple         |           Boolean            |                      Whether multiple people can be selected                      |
|      SearchResultLimit       |             Int              |                     Max person returned in the search results                     |
|       PlaceholderText        |            String            |                   Text to be displayed when no user is selected                   |
|          Selections          | ObservableCollection\<Person> |                             The selected person list                              |

## Sample Code

First of all, initialize the [MicrosoftGraphService](../../services/MicrosoftGraph.md) with your [Azure AD v2.0 app](/azure/active-directory/develop/active-directory-v2-app-registration), this should be done globally with the combined and unique [delegate permissions](/azure/active-directory/develop/active-directory-v2-scopes) required by all Graph controls and services used in your app.

```csharp
MicrosoftGraphService.Instance.AuthenticationModel = MicrosoftGraphEnums.AuthenticationModel.V2;

MicrosoftGraphService.Instance.Initialize(
    "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    MicrosoftGraphEnums.ServicesToInitialize.UserProfile,
    PeoplePicker.RequiredDelegatedPermissions
);
```

The sign in will be processed by the [AadLogin](AadLogin.md) control, however, you could do sign in with the following alternatively.

```csharp
await MicrosoftGraphService.Instance.LoginAsync();
```

[PeoplePicker Sample Page Source](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.1.0/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/PeoplePicker). You can [see this in action](uwpct://Controls?sample=PeoplePicker) in the [Windows Community Toolkit Sample App](https://aka.ms/windowstoolkitapp).

## Default Template

[PeoplePicker XAML File](https://github.com/windows-toolkit/WindowsCommunityToolkit/blob/rel/7.1.0/Microsoft.Toolkit.Uwp.UI.Controls.Graph/PeoplePicker/PeoplePicker.xaml) is the XAML template used in the toolkit for the default styling.

## Requirements

| Device family | Universal, 10.0.16299.0 or higher |
| -- | -- |
| Namespace | Microsoft.Toolkit.Uwp.UI.Controls.Graph |
| NuGet package | [Microsoft.Toolkit.Uwp.UI.Controls.Graph](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI.Controls.Graph/) |
