---
title: Authentication Providers Overview
author: shweaver-MSFT
description: Authentication providers that enable easy access to Microsoft Graph APIs.
keywords: uwp, wpf, netstandard, windows, community, toolkit, graph, login, authentication, provider, providers, identity, msa, wam
dev_langs:
  - csharp
---

# Authentication Providers Overview

Authentication is always the first step to working with Microsoft Graph. The toolkit providers enable your application to authenticate with Microsoft Identity and access Microsoft Graph in only few lines of code. Each provider handles user authentication and acquiring access tokens to call Microsoft Graph APIs, so that you don't have to write this code yourself.

You can use the providers on their own, without components, to quickly implement authentication for your app and make calls to Microsoft Graph via the Microsoft Graph .NET SDK.

The providers are required when using the Microsoft Graph Toolkit helpers and controls so they can access Microsoft Graph APIs. If you already have your own authentication and want to use the helpers and controls, you can use a [custom provider](./custom.md) instead.

The toolkit includes the following providers:

| Providers | Description |
| -- | -- |
| [Msal](./msal.md) | Uses MSAL for .NET to sign in users and acquire tokens to use with Microsoft Graph in NetStandard 2.0 applications. |
| [Windows](./windows.md) | Uses native WebAccountManager (WAM) APIs to sign in users and acquire tokens to use with Microsoft Graph in UWP applications. |
| [Custom](./custom.md) | Create a custom provider to enable authentication and access to Microsoft Graph with your application's existing authentication code. |

## Initializing the GlobalProvider

To use an authentication provider in your app, you need to set it as the global provider. The [ProviderManager](./ProviderManager.md) is the singleton that stores the globally accessible [IProvider](./custom.md) implementation and signals events in response to authentication state changes.
Set the `GlobalProvider` property at app startup and any other Graph based code will respond to any changes as users sign in and out.

```csharp
using CommunityToolkit.Authentication;

// Set the GlobalProvider to an IProvider implementation.
ProviderManager.Instance.GlobalProvider = new WindowsProvider();
```

### Permission scopes

We recommend adding all the permission scopes your application may need when initializing your provider. This is optional, but will improve your user experience by presenting a single consent screen to the user with an aggregated list of permissions requested by all components in your app, rather than presenting separate prompts per scope as requested by the helpers and controls. The following example shows how to do this with the WindowsProvider.

```csharp

using CommunityToolkit.Authentication;

string[] scopes = new string[] { "User.Read", "People.Read" };

ProviderManager.Instance.GlobalProvider = new WindowsProvider(scopes);
```

### ProviderState

The providers keeps track of the user's authentication state and communicate it outwards. For example, when a user successfully signs in, the `ProviderState` is updated to `SignedIn`, signaling to the application that it is now able to make calls to Microsoft Graph.

```csharp
public enum ProviderState
{
    // The user's status is not known.
    Loading,

    // The user is signed-out.
    SignedOut,

    // The user is signed-in.
    SignedIn,
}
```

## Respond to changes in the GlobalProvider state

In some scenarios, you will want to show certain functionality or perform an action only after a user has successfully signed in. You can access and check the provider state as shown in the following example:

```csharp
using CommunityToolkit.Authentication;

if (ProviderManager.Instance.GlobalProvider?.State === ProviderState.SignedIn) {
  // your code here
}
```

Use the `ProviderUpdated` and `ProviderStateChanged` events to get notified whenever provider is set or changes state.

```csharp
using CommunityToolkit.Authentication;

ProviderManager.Instance.ProviderUpdated += OnProviderUpdated;
ProviderManager.Instance.ProviderStateChanged += OnProviderStateChanged;

void OnProviderUpdated(object sender, IProvider provider)
{
    // The global provider has been set.
}

void OnProviderStateChanged(object sender, ProviderUpdatedEventArgs args)
{
    // The state of the global provider has changed.
}
```

### ProviderStateTrigger

To respond to provider state changes from XAML, try out the `ProviderStateTrigger` state trigger.

Available in the `CommunityToolkit.Graph.Uwp` package.

```xml
<VisualStateManager.VisualStateGroups xmlns:uwp="using:CommunityToolkit.Graph.Uwp">
    <VisualStateGroup>
        <VisualState>
            <VisualState.StateTriggers>
                <uwp:ProviderStateTrigger State="SignedIn" />
            </VisualState.StateTriggers>
            <VisualState.Setters>
                <Setter Target="ContentPivot.Visibility" Value="Visible" />
            </VisualState.Setters>
        </VisualState>
    </VisualStateGroup>
</VisualStateManager.VisualStateGroups>

<Pivot Name="ContentPivot" Visibility="Collapsed">
    <!-- The pivot will only be visible when the global provider is in a signed in state, and otherwise collapsed. -->
</Pivot>
```

### FrameworkElement.IsVisibleWhen

The `FrameworkElement.IsVisibleWhen` attached property makes it easy to toggle visibility for any `FrameworkElement`.

Available in the `CommunityToolkit.Graph.Uwp` package.

```xml
<Pivot Name="ContentPivot" uwp:ElementExtensions.IsVisibleWhen="SignedIn">
    <!-- The pivot will only be visible when the global provider is in a signed in state, and otherwise collapsed. -->
</Pivot>
```

## Getting an access token

Each provider exposes a function called `getTokenAsync` that can retrieve the current access token or retrieve a new access token for the provided scopes. The following example shows how to get a new access token or the currently signed in user:

```csharp
using CommunityToolkit.Authentication;

// Assuming a provider has already been initialized
IProvider provider = ProviderManager.Instance.GlobalProvider;

string token = await provider.GetTokenAsync(silentOnly: false);
```

## Call Microsoft Graph APIs

Once authenticated, you can now make API calls to Microsoft Graph using the Graph SDK or without. See the [Extensions](../helpers/extensions.md) page for an example of how to authenticate an outbound request directly.

### Use the Graph SDK

Access APIs using the Graph SDK through a preconfigured `GraphServiceClient` available through an extension method on `IProvider` called `GetClient()` and `GetBetaClient()`.
See [Microsoft Graph Extensions](../helpers/extensions.md) for more details.

It's possible to authenticate and make all Graph requests manually, without the Graph SDK. This can reduce package size significantly. However, using the Graph SDK is certainly the easiest way to work with Graph in .NET because the `GraphServiceClient` offers a convenient way of building requests and includes all of the object types ready to use.

Available in the `CommunityToolkit.Graph` package.

```csharp
using CommunityToolkit.Authentication;
using CommunityToolkit.Graph.Extensions;

IProvider provider = ProviderManager.Instance.GlobalProvider;
GraphServiceClient graphClient = provider.GetClient();

var me = await graphClient.Me.Request().GetAsync();
```
