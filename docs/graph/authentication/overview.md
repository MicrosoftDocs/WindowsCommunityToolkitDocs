---
title: Authentication Providers Overview
author: shweaver-MSFT
description: Authentication providers that enable easy access to Microsoft Graph APIs.
keywords: uwp, wpf, netstandard, windows, community, toolkit, graph, login, authentication, provider, providers, identity, msa, wam
dev_langs:
  - csharp
---

# Authentication Providers Overview

> [!IMPORTANT]
> Windows Community Toolkit - Graph Controls and Helpers packages are in preview. To get started using WCT preview packages visit the [WCT Preview Packages wiki page](https://aka.ms/wct/wiki/previewpackages).

Authentication is always the first step to working with Microsoft Graph. The toolkit providers enable your application to authenticate with Microsoft Identity and access Microsoft Graph in only few lines of code. Each provider handles user authentication and acquiring access tokens to call Microsoft Graph APIs, so that you don't have to write this code yourself.

You can use the providers on their own, without components, to quickly implement authentication for your app and make calls to Microsoft Graph via the Microsoft Graph .NET SDK.

The providers are required when using the Microsoft Graph Toolkit helpers and controls so they can access Microsoft Graph APIs. If you already have your own authentication and want to use the helpers and controls, you can use a [custom provider](./custom.md) instead.

The toolkit includes the following providers:

| Providers | Description |
| -- | -- |
| [Msal](./msal.md) | Uses MSAL for .NET to sign in users and acquire tokens to use with Microsoft Graph in a NetStandard 2.0 application. |
| [Windows](./windows.md) | Uses native WebAccountManager (WAM) APIs to sign in users and acquire tokens to use with Microsoft Graph in a UWP application. |
| [Custom](./custom.md)Custom | Create a custom provider to enable authentication and access to Microsoft Graph with your application's existing authentication code. |

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

In some scenarios, you will want to show certain functionality or perform an action only after a user has successfully signed in. You can access and check the provider state as shown in the following example:

```csharp
using CommunityToolkit.Authentication;

if (ProviderManager.Instance.GlobalProvider?.State === ProviderState.SignedIn) {
  // your code here
}
```

You can also use the `ProviderUpdated` event to get notified whenever the state of the provider changes.

```csharp
using CommunityToolkit.Authentication;

ProviderManager.Instance.ProviderUpdated += OnProviderUpdated;

void OnProviderUpdated(object sender, ProviderUpdatedEventArgs e)
{
    if (e.Reason == ProviderManagerChangedState.ProviderUpdated)
    {
        // The GlobalProvider has been set or unset.
    }

    if (e.Reason == ProviderManagerChangedState.ProviderStateChanged)
    {
        // The GlobalProvider state has changed.
    }
}
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

Once authenticated, you can now make API calls to Microsoft Graph using the Graph SDK or without.

### Use the Graph SDK

Access APIs using the Graph SDK through a preconfigured `GraphServiceClient` available through an extension method on `IProvider` called, `GetClient()`.
See [Microsoft Graph Extensions](../helpers/extensions.md) for more details.

This is the easiest way to get started because all of the Graph types are available and the `GraphServiceClient` offers a convenient way of building requests.

Available in the `CommunityToolkit.Graph` package.

```csharp
using CommunityToolkit.Authentication;
using CommunityToolkit.Graph.Extensions;

IProvider provider = ProviderManager.Instance.GlobalProvider;
GraphServiceClient graphClient = provider.GetClient();

var me = await graphClient.Me.Request().GetAsync();
```

### Handle Graph requests manually

Access APIs by managing requests to Microsoft Graph yourself. This is helpful for projects with existing systems for managing web requests, or for keeping package sizes minimal by excluding the Graph SDK.

To make Graph API calls manually, use the `IProvider.AuthenticateRequestAsync(HttpRequestMessage)` method to authenticate an outgoing request.

```csharp
using CommunityToolkit.Authentication;
using Newtonsoft.Json;
using Newtonsoft.Json.Linq;

private async Task<IList<TodoTask>> GetDefaultTaskListAsync()
{
    return await GetResponseAsync<List<TodoTask>>("https://graph.microsoft.com/v1.0/me/todo/lists/tasks/tasks");
}

private async Task<T> GetResponseAsync<T>(string requestUri)
{
    // Build the request
    HttpRequestMessage getRequest = new HttpRequestMessage(HttpMethod.Get, requestUri);

    // Authenticate the request
    await ProviderManager.Instance.GlobalProvider.AuthenticateRequestAsync(getRequest);

    var httpClient = new HttpClient();
    using (httpClient)
    {
        // Send the request
        var response = await httpClient.SendAsync(getRequest);

        if (response.IsSuccessStatusCode)
        {
            // Handle the request response
            var jsonResponse = await response.Content.ReadAsStringAsync();
            var jObject = JObject.Parse(jsonResponse);
            if (jObject.ContainsKey("value"))
            {
                var result = JsonConvert.DeserializeObject<T>(jObject["value"].ToString());
                return result;
            }
        }
    }

    return default;
}
```
