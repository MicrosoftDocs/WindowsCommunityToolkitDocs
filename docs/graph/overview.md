---
title: Windows Community Toolkit - Graph Helpers and Controls
author: shweaver-MSFT
description: Authentication providers and Graph powered helpers that make it easy to work with Microsoft Graph APIs.
keywords: uwp, wpf, netstandard, windows, community, toolkit, graph, login, authentication, provider, providers, identity
dev_langs:
  - csharp
---

# Windows Community Toolkit - Graph Helpers and Controls

The Graph helpers and controls are a sub-project of the [Windows Community Toolkit](https://aka.ms/wct) focused on [Microsoft Graph](https://developer.microsoft.com/en-us/graph/) and providing a set of Authentication providers and Graph powered Helpers/Controls that make it easy to work with Microsoft Graph APIs.

Note: This new library replaces the `Microsoft.Toolkit.Uwp.UI.Controls.Graph` package; however, it is not backwards compatible nor does it provide all the same features at this time.

If you need similar controls for the Web, please use the [Microsoft Graph Toolkit](https://aka.ms/mgt).

## What's new?

We've overhauled our approach and introduced some big improvements:

- The new WindowsProvider enables basic consumer login without AAD configuration 🎊
- Authentication packages are now split per provider 🎉
- Access to the GraphServiceClient now lives in a separate package. This means no dependency on the Graph SDK for simple auth scenarios and apps that perform Graph requests manually (sans SDK) 🥳
- Removed Beta Graph SDK, but enabled access with V1 SDK types. This is so our controls and helpers can be based on the stable Graph endpoint, while also allowing for requests to the beta endpoint in some circumstances (Such as retrieving a user's photo) 🎈

For more info on our roadmap, check out the current [Release Plan](https://github.com/windows-toolkit/Graph-Controls/issues/81)

## <a name="supported"></a> Supported SDKs

| Package | Min Supported |
|--|--|
| `CommunityToolkit.Authentication` | NetStandard 2.0 |
| `CommunityToolkit.Authentication.Msal` | NetStandard 2.0 |
| `CommunityToolkit.Authentication.Uwp` | UWP Windows 10 17134 |
| `CommunityTookit.Graph` | NetStandard 2.0 |
| `CommunityToolkit.Graph.Uwp` | UWP Windows 10 17763 |

## Getting Started

Check out the [Getting Started](./getting-started.md) guide for details on how to get authenticated and start calling Graph APIs.

## Learn More

**Authentication Providers**

Hook into a lightweight framework for authenticating users and responding to login state changes: [Authentication Providers Overview](./authentication/overview.md)

**Graph Helpers**

See [ProviderExtensions](./helpers/ProviderExtensions.md) to learn how to get access to a preconfigured GraphServiceClient and make adhoc API calls using the Graph SDK.

**Graph Controls**

Build Graph experiences with XAML controls and helpers made for UWP, such as [LoginButton](./controls/LoginButton.md) or [PersonView](./controls/PersonView.md).
