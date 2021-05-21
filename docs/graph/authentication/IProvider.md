---
title: IProvider
author: shweaver-MSFT
description: IProvider interface defines the basic functions of an authentication provider in the Graph toolkit.
keywords: uwp, wpf, netstandard, windows, community, toolkit, graph, login, authentication, provider, providers, identity
dev_langs:
  - csharp
---

# IProvider

The IProvider is the base interface for creating authentication providers that work with the various controls and helpers in the toolkit. 

```csharp
using CommunityToolkit.Authentication;

IProvider provider = ProviderManager.Instance.GlobalProvider; 

if (provider?.State == ProviderState.SignedIn)
{
    // You are now signed in and can request access tokens.
}
```

## Properties

| Property | Type | Description |
| -- | -- | -- |
| State | [ProviderState](./ProviderState.md) | Gets the current authentication state of the provider. |

## Events

| Event | Type | Description |
| -- | -- | -- |
| StateChanged | EventHandler&lt;[ProviderStateChangedEventArgs](./ProviderStateChangedEventArgs.md)&gt; | An event that is called whenever the login state changes. 

## Methods

| Method | Arguments | Returns | Description |
| -- | -- | -- | -- |
| AuthenticateRequestAsync | HttpRequestMessage | Task | Authenticate an outgoing request. |
| GetTokenAsync | bool silentOnly = true | Task&lt;string&gt; | Retrieve a token for the authenticated user. |
| SignInAsync | | Task | Sign in a user. |
| SignOutAsync | | Task | Sign out the current user. |
| TrySilentSignInAsync | | Task&lt;bool&gt; | Try signing in silently, without prompts. |