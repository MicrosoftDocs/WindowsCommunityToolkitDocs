---
title: SharePointFileList Control
author: OGcanviz
description: The SharePointFileList Control displays a simple list of SharePoint Files (outdated docs).
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, SharePointFileList Control
---

# SharePointFileList Control

> [!WARNING]
> (This API has been removed. For the latest guidance on using the Microsoft Graph check out the [Windows Community Toolkit - Graph Helpers and Controls](../../graph/overview.md).)

The [SharePointFileList Control](/dotnet/api/microsoft.toolkit.uwp.ui.controls.graph.sharepointfilelist) displays a simple list of SharePoint Files, it relies on the [MicrosoftGraphService](../../services/MicrosoftGraph.md) for authentication.

## Syntax

```xaml
<Page ...
    xmlns:controls="using:Microsoft.Toolkit.Uwp.UI.Controls.Graph"/>

<controls:SharePointFileList x:Name="SharePointFileList1"
    DetailPane="Side"
    DriveUrl="https://contoso.sharepoint.com/sites/DemoSite/DemoLib" />
```

## Example Image

![SharePointFileList animation](../../resources/images/Graph/SharePointFileList.png)

## Properties

| Property | Type | Description |
| -- | -- | -- |
| RequiredDelegatedPermissions | String[] | Gets required delegated permissions for Graph API access |
| DriveUrl | String | Full URL of the Drive being displayed |
| DetailPane | [DetailPaneDisplayMode](https://github.com/windows-toolkit/WindowsCommunityToolkit/blob/rel/7.1.0/Microsoft.Toolkit.Uwp.UI.Controls.Graph/SharePointFileList/DetailPaneDisplayMode.cs) | Determines whether file details are displayed, when a file is selected |
| PageSize | Int | Page size of each request |
| ShareLinkCopiedMessage | String | The message when share link copied |
| AllFilesMessage | String | The label of All Files |
| DeleteConfirmMessage | String | The message of delete confirm dialog |
| DeleteConfirmOkMessage | String | The caption of ok button in delete confirm dialog |
| DeleteConfirmCancelMessage | String | The caption of cancel button in delete confirm dialog |
| UploadingFilesMessageTemplate | String | The template of uploading files |

## Methods

| Method | Return Type | Description |
| -- | -- | -- |
| GetDriveUrlFromSharePointUrlAsync | String | Retrieves an appropriate Drive URL from a SharePoint document library root URL |

## Events

| Event | Return Type | Description |
| -- | -- | -- |
| FileSelected | EventHandler&lt;FileSelectedEventArgs&gt; | Occurs when one of the menu items in the control is clicked |

## Sample Code

First of all, initialize the [MicrosoftGraphService](../../services/MicrosoftGraph.md) with your [Azure AD v2.0 app](/azure/active-directory/develop/active-directory-v2-app-registration), this should be done globally with the combined and unique [delegate permissions](/azure/active-directory/develop/active-directory-v2-scopes) required by all Graph controls and services used in your app.

```csharp
MicrosoftGraphService.Instance.AuthenticationModel = MicrosoftGraphEnums.AuthenticationModel.V2;

MicrosoftGraphService.Instance.Initialize(
    "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    MicrosoftGraphEnums.ServicesToInitialize.UserProfile,
    SharePointFileList.RequiredDelegatedPermissions
);
```

The sign in will be processed by the [AadLogin](AadLogin.md) control, however, you could do sign in with the following alternatively.

```csharp
await MicrosoftGraphService.Instance.LoginAsync();
```

[SharePointFileList Sample Page Source](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.1.0/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/SharePointFileList). You can [see this in action](uwpct://Controls?sample=SharePointFileList) in the [Windows Community Toolkit Sample App](https://aka.ms/windowstoolkitapp).

## Default Template

[SharePointFileList XAML File](https://github.com/windows-toolkit/WindowsCommunityToolkit/blob/rel/7.1.0/Microsoft.Toolkit.Uwp.UI.Controls.Graph/SharePointFileList/SharePointFileList.xaml) is the XAML template used in the toolkit for the default styling.

## Requirements

| Device family | Universal, 10.0.16299.0 or higher |
| -- | -- |
| Namespace | Microsoft.Toolkit.Uwp.UI.Controls.Graph |
| NuGet package | [Microsoft.Toolkit.Uwp.UI.Controls.Graph](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI.Controls.Graph/) |
