---
title: MsalProvider
author: shweaver-MSFT
description: Authentication provider based on the official Microsoft Authentication Library (MSAL).
keywords: uwp, wpf, netstandard, windows, community, toolkit, graph, login, authentication, provider, providers, identity, msal
dev_langs:
  - csharp
---

# MsalProvider

The MsalPRovider is an [IProvider](../IProvider.md) implementation built on the official Microsoft Authentication Library (MSAL). It is NetStandard 2.0 so it works in both UWP and WPF apps.

> Available in the `CommunityToolkit.Authentication.Msal` package.

```csharp
using CommunityToolkit.Authentication;

string clientId = "YOUR-CLIENT-ID-HERE";
string[] scopes = new string[] { "User.Read" };

ProviderManager.Instance.GlobalProvider = new MsalProvider(clientId, scopes);
```

## Prerequisite Configure Client Id in Partner Center

If your product integrates with Azure AD and calls APIs that request either application permissions or delegated permissions that require administrator consent, you will also need to enter your Azure AD Client ID in Partner Center:

https://partner.microsoft.com/dashboard/products/&lt;YOUR-APP-ID&gt;/administrator-consent

This lets administrators who acquire the app for their organization grant consent for your product to act on behalf of all users in the tenant.

> [!NOTE]
> You only need to specify the client id if you need admin consent for delegated permissions from your AAD app registration. Simple authentication for public accounts does not require a client id or any additional configuration.

> [!IMPORTANT]
> Be sure to Register Client Id in Azure first following the guidance here: [Quickstart: Register an application with the Microsoft identity platform](/azure/active-directory/develop/quickstart-register-app)
>
> After finishing the initial registration page, you will also need to add an additional redirect URI. Click on "Add a Redirect URI" and add the value retrieved from running `WindowsProvider.RedirectUri`.
>
> You'll also want to set the toggle to true for "Allow public client flows".
>
> Then click "Save".

## Properties

| Property | Type | Description |
| -- | -- | -- |
| State | [ProviderState](../IProvider.md) | Gets the current authentication state of the provider. |

## Events

| Event | Type | Description |
| -- | -- | -- |
| StateChanged | EventHandler&lt;[ProviderStateChangedEventArgs](../IProvider.md)&gt; | Event called when the provider state changes. |

## Methods

| Method | Arguments | Returns | Description |
| -- | -- | -- | -- |
| GetTokenAsync | bool silentOnly = true | Task&lt;string&gt; | Retrieve a token for the authenticated user. |
| AuthenticateRequestAsync | HttpRequestMessage | Task | Authenticate an outgoing request. |
| SignInAsync | | Task | Sign in a user. |
| SignOutAsync | | Task | Sign out the current user. |
| TrySilentSignInAsync | | Task&lt;bool&gt; | Try signing in silently, without prompts. |
