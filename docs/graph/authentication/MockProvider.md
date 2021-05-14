---
title: MockProvider
author: shweaver-MSFT
description: Mock authentication provider that enables access to dummy Graph data.
keywords: uwp, wpf, netstandard, windows, community, toolkit, graph, login, authentication, provider, providers, identity, mock
dev_langs:
  - csharp
---

# MockProvider

An `IProvider` implementation built on a set of readonly, fake Graph data. 
Used for prototyping and demonstration purposes.

```csharp
using CommunityToolkit.Net.Authentication;

ProviderManager.Instance.GlobalProvider = new MockProvider();
```

## Properties

| Property | Type | Description |
| -- | -- | -- |
| State | ProviderState | Gets the current authentication state of the provider. |

## Events

| Event | Type | Description |
| -- | -- | -- |
| StateChanged | EventHandler&lt;ProviderStateChangedEventArgs&gt; | Event called when the provider state changes. |

## Methods

| Method | Arguments | Returns | Description |
| -- | -- | -- | -- |
| AuthenticateRequestAsync | HttpRequestMessage | Task | Authenticate an outgoing request. |
| SignInAsync | | Task | Sign in a user. |
| SignOutAsync | | Task | Sign out the current user. |
| TrySilentSignInAsync | | Task&lt;bool&gt; | Try signing in silently, without prompts. |