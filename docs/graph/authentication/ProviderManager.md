---
title: ProviderManager
author: shweaver-MSFT
description: ProviderManager manages access to the globally configured IProvider instance and any state change events as users sign in and out.
keywords: uwp, wpf, netstandard, windows, community, toolkit, graph, login, authentication, provider, providers, identity
dev_langs:
  - csharp
---

# ProviderManager

The ProviderManager manages access to the globally configured [IProvider](./IProvider.md) instance and any state change events as users sign in and out.

### Set the GlobalProvider

```csharp
using CommunityToolkit.Authentication;

ProviderManager.Instance.GlobalProvider = new WindowsProvider();
```

### Listen for changes to the GlobalProvider

```csharp
using CommunityToolkit.Authentication;

ProviderManager.Instance.ProviderUpdated += OnProviderUpdated;

void OnProviderUpdated(object sender, ProviderUpdatedEventArgs e)
{
    if (e.Reason == ProviderManagerChangedState.ProviderUpdated)
    {
        // The GlobalProvider has been set.
    }

    if (e.Reason == ProviderManagerChangedState.ProviderStateChanged)
    {
        // The GlobalProvider state has changed.
    }
}
```

## Properties

| Property | Type | Description |
| -- | -- | -- |
| State | ProviderState | Gets the current authentication state of the provider. |

## Events

| Event | Type | Description |
| -- | -- | -- |
| ProviderUpdated | EventHandler&lt;[ProviderUpdatedEventArgs](./ProviderUpdatedEventArgs.md)&gt; | Event called when the IProvider changes. |

## Methods

| Method | Arguments | Returns | Description |
| -- | -- | -- | -- |
| AuthenticateRequestAsync | HttpRequestMessage | Task | Authenticate an outgoing request. |
| GetTokenAsync | bool silentOnly = true | Task&lt;string&gt; | Retrieve a token for the authenticated user. |
| SignInAsync | | Task | Sign in a user. |
| SignOutAsync | | Task | Sign out the current user. |
| TrySilentSignInAsync | | Task&lt;bool&gt; | Try signing in silently, without prompts. |