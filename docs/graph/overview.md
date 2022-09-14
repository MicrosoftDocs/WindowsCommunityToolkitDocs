---
title: Windows Community Toolkit - Authentication and Graph
author: shweaver-MSFT
description: Authentication providers and Graph powered helpers that make it easy to work with Microsoft Graph APIs.
keywords: uwp, wpf, netstandard, windows, community, toolkit, graph, login, authentication, provider, providers, identity
dev_langs:
  - csharp
---

# Windows Community Toolkit - Authentication and Graph

The authentication and Graph helpers and controls are a part of the [Windows Community Toolkit](https://aka.ms/wct), focused on enabling quick and easy Windows authentication and [Microsoft Graph](https://developer.microsoft.com/en-us/graph/) powered experiences. These controls and helpers make it easy to get users authenticated and start calling Microsoft Graph APIs!

> Note: This new library replaces the `Microsoft.Toolkit.Uwp.UI.Controls.Graph` package; however, it is not backwards compatible nor does it provide all the same features at this time.

If you need similar controls for the web, check out the [Microsoft Graph Toolkit](https://aka.ms/mgt).

## <a name="supported"></a> Supported SDKs

| Package | Min Supported |
|--|--|
| `CommunityToolkit.Authentication` | NetStandard 2.0 |
| `CommunityToolkit.Authentication.Msal` | NetStandard 2.0 |
| `CommunityToolkit.Authentication.Uwp` | UWP Windows 10 17134 |
| `CommunityToolkit.Graph` | NetStandard 2.0 |
| `CommunityToolkit.Graph.Uwp` | UWP Windows 10 17763 |

## Getting started

Check out the [Getting Started](./getting-started.md) guide for details on how to get authenticated and start calling Graph APIs.

## Learn More

### Authentication providers

Hook into a lightweight framework for authenticating users and responding to login state changes: [Authentication Providers Overview](./authentication/overview.md)

### Extensions

See [Microsoft Graph Extensions](./helpers/extensions.md) to learn how to get access to a preconfigured GraphServiceClient and make adhoc API calls using the Graph SDK.

### Roaming settings

Roam settings across experiences with the Graph using [Graph powered storage helpers](./helpers/roaming-settings.md). Store simple settings with open extensions on the Graph User or try the `OneDriveStorageHelper` for roaming files via OneDrive.

### XAML controls

Build Graph experiences with XAML controls made for UWP, such as [LoginButton](./controls/LoginButton.md) or [PersonView](./controls/PersonView.md).
