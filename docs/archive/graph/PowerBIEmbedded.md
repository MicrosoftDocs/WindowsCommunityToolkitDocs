---
title: PowerBIEmbedded Control
author: OGcanviz
description: The PowerBIEmbedded control is a simple wrapper to an IFRAME for a PowerBI embed (outdated docs).
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, PowerBIEmbedded Control
---

# PowerBIEmbedded Control

> [!WARNING]
> (This API has been removed. For the latest guidance on using the Microsoft Graph see the [InteractiveProviderBehavior](../../graph/providers/InteractiveProviderBehavior.md).)

The [PowerBIEmbedded Control](/dotnet/api/microsoft.toolkit.uwp.ui.controls.graph.powerbiembedded) is a simple wrapper to an IFRAME for a PowerBI embed.

## Syntax

```xaml
<Page ...
    xmlns:controls="using:Microsoft.Toolkit.Uwp.UI.Controls.Graph"/>

<controls:PowerBIEmbedded x:Name="PowerBIEmbedded1"
    ClientId="xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
    GroupId="xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx" />
```

## Example Image

![PowerBIEmbedded animation](../../resources/images/Graph/PowerBIEmbedded.png)

## Properties

| Property | Type | Description |
| -- | -- | -- |
| ClientId | String | Gets or sets the client id of Azure AD app registration (v1) |
| GroupId | String | Gets or sets the identifier of a Group. Optional when EmbedUrl is specified, if this is used, a dropdown will appear that lets users select amongst different reports in a Group |
| EmbedUrl | String | Gets or sets the Url of the embed, optional when GroupId is specified |
| ShowFilter | Boolean | Gets or sets a value indicating whether show the filter pane |

## Integration

1. Follow the
[MicrosoftGraphService](../../services/MicrosoftGraph.md#register-the-app-to-use-azure-ad-v1-endpoint) to create Azure AD app registration (v1), and grant the permissions below.

   * Microsoft Graph
      * Sign in and read user profile
      * Read all users' basic profiles
      * Sign users in

   * Windows Azure Active Directory
      * Sign in and read user profile

   * Power BI Service (Microsoft.Azure.AnalysisServices)

      * View all datapools
      * View users Groups
      * View all Groups
      * View all Reports
      * View all Datasets
      * View all Dashboards
      * View all workspaces

      ![PowerBIEmbedded Permissions](../../resources/images/Graph/PowerBIEmbedded-Permissions.png)

2. Follow this [article](/power-bi/developer/embedding-content) to do the primary tasks below.

   * Create Power BI Pro user account
   * Create app workspaces
   * Create Power BI Embedded capacity
   * Create and publish reports

3. For better report experience in mobile, that's recommended to [design phone layout for mobile portrait view in PowerBI desktop](/power-bi/desktop-create-phone-report).

## Sample Project

[PowerBIEmbedded Sample Page Source](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.0.0/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/PowerBIEmbedded). You can [see this in action](uwpct://Controls?sample=PowerBIEmbedded) in the [Windows Community Toolkit Sample App](https://aka.ms/windowstoolkitapp).

## Default Template

[PowerBIEmbedded XAML File](https://github.com/windows-toolkit/WindowsCommunityToolkit/blob/rel/7.0.0/Microsoft.Toolkit.Uwp.UI.Controls.Graph/PowerBIEmbedded/PowerBIEmbedded.xaml) is the XAML template used in the toolkit for the default styling.

## Requirements

| Device family | Universal, 10.0.16299.0 or higher |
| -- | -- |
| Namespace | Microsoft.Toolkit.Uwp.UI.Controls.Graph |
| NuGet package | [Microsoft.Toolkit.Uwp.UI.Controls.Graph](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI.Controls.Graph/) |
