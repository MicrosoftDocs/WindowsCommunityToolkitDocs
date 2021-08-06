---
title: PlannerTaskList Control
author: OGcanviz
description: The PlannerTaskList Control displays a simple list of Planner tasks (outdated docs).
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, PlannerTaskList Control
---

# PlannerTaskList Control

> [!WARNING]
> (This API has been removed. For the latest guidance on using the Microsoft Graph check out the [Windows Community Toolkit - Graph Helpers and Controls](../../graph/overview.md).)

The [PlannerTaskList Control](/dotnet/api/microsoft.toolkit.uwp.ui.controls.graph.plannertasklist) displays a simple list of Planner tasks, it relies on the [MicrosoftGraphService](../../services/MicrosoftGraph.md) for authentication.

## Syntax

```xaml
<Page ...
    xmlns:controls="using:Microsoft.Toolkit.Uwp.UI.Controls.Graph"/>

<controls:PlannerTaskList x:Name="PlannerTaskList1" />
```

## Example Image

![PlannerTaskList animation](../../resources/images/Graph/PlannerTaskList.png)

## Properties

| Property | Type | Description |
| -- | -- | -- |
| RequiredDelegatedPermissions | String[] | Gets required delegated permissions for Graph API access |
| PlanId | String | Gets or sets Id of Planner Plan to Display, this is optional. |
| DisplayPlanList | Boolean | Gets or sets a value indicating whether show plan list or not |
| DisplayBucketList | Boolean | Gets or sets a value indicating whether show bucket list or not |
| AllTasksLabel | String | Gets or sets label of all tasks |
| ClosedTasksLabel | String | Gets or sets label of closed tasks |

## Sample Code

First of all, initialize the [MicrosoftGraphService](../../services/MicrosoftGraph.md) with your [Azure AD v2.0 app](/azure/active-directory/develop/active-directory-v2-app-registration), this should be done globally with the combined and unique [delegate permissions](/azure/active-directory/develop/active-directory-v2-scopes) required by all Graph controls and services used in your app.

> Note: The permission `Group.ReadWrite.All` used in this control requires [admin consent](/azure/active-directory/develop/active-directory-v2-scopes#request-the-permissions-from-a-directory-admin), which could be done by opening a URL like this in the browser and sign in with your organization's admin.
> `https://login.microsoftonline.com/common/adminconsent?client_id=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx&state=12345`

```csharp
MicrosoftGraphService.Instance.AuthenticationModel = MicrosoftGraphEnums.AuthenticationModel.V2;

MicrosoftGraphService.Instance.Initialize(
    "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    MicrosoftGraphEnums.ServicesToInitialize.UserProfile,
    PlannerTaskList.RequiredDelegatedPermissions
);
```

The sign in will be processed by the [AadLogin](AadLogin.md) control, however, you could do sign in with the following alternatively.

```csharp
await MicrosoftGraphService.Instance.LoginAsync();
```

[PlannerTaskList Sample Page Source](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.0.0/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/PlannerTaskList). You can [see this in action](uwpct://Controls?sample=PlannerTaskList) in the [Windows Community Toolkit Sample App](https://aka.ms/windowstoolkitapp).

## Default Template

[PlannerTaskList XAML File](https://github.com/windows-toolkit/WindowsCommunityToolkit/blob/rel/7.0.0/Microsoft.Toolkit.Uwp.UI.Controls.Graph/PlannerTaskList/PlannerTaskList.xaml) is the XAML template used in the toolkit for the default styling.

## Requirements

| Device family | Universal, 10.0.16299.0 or higher |
| -- | -- |
| Namespace | Microsoft.Toolkit.Uwp.UI.Controls.Graph |
| NuGet package | [Microsoft.Toolkit.Uwp.UI.Controls.Graph](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI.Controls.Graph/) |
