---
title: IProvider
author: shweaver-MSFT
description: IProvider interface defines the basic functions of an authentication provider in the Graph toolkit.
keywords: uwp, wpf, netstandard, windows, community, toolkit, graph, login, authentication, provider, providers, identity
dev_langs:
  - csharp
---

# Custom provider

If you have existing authentication code in your application, you can create a custom provider to enable authentication and access to Microsoft Graph for the toolkit's Graph based controls and helpers. To bring your own authentication provider logic, start by extending `IProvider`.

## IProvider

`IProvider` is the base interface for creating authentication providers that work with the various controls and helpers in the toolkit. Handle authenticaiton with one of our premade `IProvider` implementations or create your own.

> Available in the `CommunityToolkit.Authentication` package.

> [!IMPORTANT]
> Windows Community Toolkit - Graph Controls and Helpers packages are in preview. To get started using WCT preview packages visit the [WCT Preview Packages wiki page](https://aka.ms/wct/wiki/previewpackages).

```csharp
using CommunityToolkit.Authentication;

// Create an instance of your custom IProvider implementation.
IProvider customProvider = new CustomProvider(); 

// Set the global provider using the custom instance.
ProviderManager.Instance.GlobalProvider = customProvider;
```

### Properties

| Property | Type | Description |
| -- | -- | -- |
| State | ProviderState | Gets the current authentication state of the provider. |

### Events

| Event | Type | Description |
| -- | -- | -- |
| StateChanged | EventHandler&lt;ProviderStateChangedEventArgs&gt; | An event that is called whenever the login state changes.

### Methods

| Method | Arguments | Returns | Description |
| -- | -- | -- | -- |
| AuthenticateRequestAsync | HttpRequestMessage | Task | Authenticate an outgoing request. |
| GetTokenAsync | bool silentOnly = false | Task&lt;string&gt; | Retrieve a token for the authenticated user. |
| SignInAsync | | Task | Sign in a user. |
| SignOutAsync | | Task | Sign out the current user. |
| TrySilentSignInAsync | | Task&lt;bool&gt; | Try signing in silently, without prompts. |
