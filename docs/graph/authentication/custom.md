---
title: IProvider
author: shweaver-MSFT
description: IProvider interface defines the basic functions of an authentication provider in the Graph toolkit.
keywords: uwp, wpf, netstandard, windows, community, toolkit, graph, login, authentication, provider, providers, identity
dev_langs:
  - csharp
---

# IProvider

The `IProvider` is the base interface for creating authentication providers that work with the various controls and helpers in the toolkit. Handle authenticaiton with one of our premade `IProvider` implementations or create your own.

> Available in the `CommunityToolkit.Authentication` package.

> [!IMPORTANT]
> Windows Community Toolkit - Graph Controls and Helpers packages are in preview. To get started using WCT preview packages visit the [WCT Preview Packages wiki page](https://aka.ms/wct/wiki/previewpackages).

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
| State | ProviderState | Gets the current authentication state of the provider. |

## Events

| Event | Type | Description |
| -- | -- | -- |
| StateChanged | EventHandler&lt;ProviderStateChangedEventArgs&gt; | An event that is called whenever the login state changes.

## Methods

| Method | Arguments | Returns | Description |
| -- | -- | -- | -- |
| AuthenticateRequestAsync | HttpRequestMessage | Task | Authenticate an outgoing request. |
| GetTokenAsync | bool silentOnly = true | Task&lt;string&gt; | Retrieve a token for the authenticated user. |
| SignInAsync | | Task | Sign in a user. |
| SignOutAsync | | Task | Sign out the current user. |
| TrySilentSignInAsync | | Task&lt;bool&gt; | Try signing in silently, without prompts. |

## ProviderStateChangedEventArgs Object

| Property | Type | Description |
| -- | -- | -- |
| OldState | ProviderState | Gets the previous state of the IProvider.
| NewState | ProviderState | Gets the new state of the IProvider.

## ProviderState Enum

| Name | Description |
| -- | -- |
| Loading | The user's status is not known. |
| SignedOut | The user is signed-out. |
| SignedIn | The user is signed-in. |
