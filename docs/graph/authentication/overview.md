---
title: Authentication Providers Overview
author: shweaver-MSFT
description: Authentication providers that enable easy access to Microsoft Graph APIs.
keywords: uwp, wpf, netstandard, windows, community, toolkit, graph, login, authentication, provider, providers, identity, msa, wam
dev_langs:
  - csharp
---

# Authentication Providers Overview

Authentication is always the first step to working with Microsoft Graph. 
The toolkit offers a lightweight system for authenticating users, managing access tokens, and making Graph calls. 

## ProviderManager and the GlobalProvider

The `ProviderManager` is the singleton that stores the globally accessible `IProvider` implementation and signals events in response to authentication state changes. 
Set the `GlobalProvider` property at app startup and any other Graph based code will respond to any changes as users login and logout.

```csharp
using CommunityToolkit.Net.Authentication;

// Set the GlobalProvider to an IProvider implementation.
ProviderManager.Instance.GlobalProvider = new MockProvider();
```

Invoke the ProviderManager anywhere you need to make Graph calls. 
Listen for State changes on the GlobalProvider using the `ProviderChanged` event.  

```csharp
using CommunityToolkit.Net.Authentication;

ProviderManager.Instance.GlobalProvider.ProviderChanged += OnProviderChanged;

void OnProviderChanged (object sender, ProviderUpdatedEventArgs args) 
{
    // Check the State property of the GlobalProvider to determine if a user is signed in or not. 
    if (ProviderManager.Instance.GlobalProvider?.State == ProviderState.SignedIn)
    {
        // Signed in.
        // You can now make Graph calls.
    }
    else
    {
        // Signed out or loading.
        // Graph calls will fail.
    }
}
```

### MsalProvider
An `IProvider` implementation built on the official Microsoft Authentication Library (MSAL). 
The `MsalProvider` is NetStandard and supports any NetStandard 2.0 applications.

Available in the `CommunityToolkit.Net.Authentication.Msal` package.

### WindowsProvider
A lightweight `IProvider` implementation built directly on the native Windows Account Manager (WAM) APIs.
This provider enables authentication of consumer MSA accounts without any Azure AAD config and only requires a Microsoft Store App registration to use.

Available in the `CommunityToolkit.Uwp.Authentication` package.

## Call Microsoft Graph APIs
Once authenticated, you can now make API calls to Microsoft Graph using a preconfigured GraphServiceClient. Access to the client is enabled through an extension method on IProvider called, `GetClient()`.

See [ProviderExtensions]() for more details. 

```csharp
using CommunityToolkit.Net.Authentication;
using CommunityToolkit.Net.Graph.Extensions;

IProvider provider = ProviderManager.Instance.GlobalProvider;
GraphServiceClient graphClient = provider.GetClient();

var me = await graphClient.Me.Request().GetAsync();
```
