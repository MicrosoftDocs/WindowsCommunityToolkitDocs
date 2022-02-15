---
title: MsalProvider
author: shweaver-MSFT
description: Authentication provider based on the official Microsoft Authentication Library (MSAL).
keywords: uwp, wpf, netstandard, windows, community, toolkit, graph, login, authentication, provider, providers, identity, msal
dev_langs:
  - csharp
---

# MsalProvider

The MsalProvider is an [IProvider](./custom.md) implementation built on the official Microsoft Authentication Library (MSAL). It is NetStandard 2.0 so it works in both UWP and WPF apps.

Available in the `CommunityToolkit.Authentication.Msal` package.

```csharp
using CommunityToolkit.Authentication;

string clientId = "YOUR-CLIENT-ID-HERE";
string[] scopes = new string[] { "User.Read" };

ProviderManager.Instance.GlobalProvider = new MsalProvider(clientId, scopes);
```

## Prerequisite Configure Client Id in Partner Center

> [!IMPORTANT]
> To obtain a Client Id, first register your app in Azure following the guidance here: [Quickstart: Register an application with the Microsoft identity platform](/azure/active-directory/develop/quickstart-register-app)
>
> After finishing the initial registration, you will also need to add an additional redirect URI. Click on "Authentication -> Add a Platform", select "Mobile and desktop applications", and check the "https://login.microsoftonline.com/common/oauth2/nativeclient" checkbox on that page. Then click "Configure".

## Constructor

| Parameter | Type | Default | Description |
| -- | -- | -- | -- |
| clientId | string | | Registered client id. |
| scopes | string[] | null | Listof scopes to initially request. |
| redirectUri | string | `https://login.microsoftonline.com/common/oauth2/nativeclient` | Redirect URI for authentication response. |
| autoSignIn | bool | true | Determines whether the provider attempts to silently log in upon instantiation. |

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
| GetTokenAsync | bool silentOnly = false | Task&lt;string&gt; | Retrieve a token for the authenticated user. |
| AuthenticateRequestAsync | HttpRequestMessage | Task | Authenticate an outgoing request. |
| SignInAsync | | Task | Sign in a user. |
| SignOutAsync | | Task | Sign out the current user. |
| TrySilentSignInAsync | | Task&lt;bool&gt; | Try signing in silently, without prompts. |
