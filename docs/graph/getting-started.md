---
title: Getting started with WCT Graph helpers and controls
author: shweaver-MSFT
description: Get started using authentication providers and Graph powered controls and helpers from the Windows Community Toolkit.
keywords: uwp, wpf, netstandard, windows, community, toolkit, graph, login, authentication, provider, providers, identity
dev_langs:
  - csharp
---

# Getting started

To get started using Graph data in your application, you'll first need to enable authentication.

## Set the global authentication provider

### Authenticate with MSAL

Leverage the official Microsoft Authentication Library (MSAL) to enable authentication in NetStandard 2.0 applications using [MsalProvider](./authentication/msal.md).

1. Register your app in Azure AAD

    Before requesting data from [Microsoft Graph](https://graph.microsoft.com), you will need to [register your application](/azure/active-directory/develop/quickstart-register-app) to get a **ClientID**.

    > After finishing the initial registration page, you will also need to add an additional redirect URI. Click on "Add a Redirect URI", then "Add a platform", and then on "Mobile and desktop applications". Check the `https://login.microsoftonline.com/common/oauth2/nativeclient` checkbox on that page. Then click "Configure".
1. Install the `CommunityToolkit.Authentication.Msal` package.
1. Set the [ProviderManager](./authentication/ProviderManager.md).GlobalProvider to a new instance of [MsalProvider](./authentication/msal.md) with clientId and pre-configured scopes:

    ```csharp
    using CommunityToolkit.Authentication;

    string clientId = "YOUR-CLIENT-ID-HERE";
    string[] scopes = new string[] { "User.Read" };

    ProviderManager.Instance.GlobalProvider = new MsalProvider(clientId, scopes);
    ```

> Note: Use the `Scopes` property to preemptively request permissions from the user of your app for data your app needs to access from Microsoft Graph.

### Authenticate with WindowsProvider

Try out the [WindowsProvider](./authentication/windows.md) to enable authentication based on the native Windows Account Manager (WAM) APIs in your UWP apps, without requiring a dependency on MSAL.

1. Associate your app with the Microsoft Store. The app association will act as our minimal app registration for authenticating consumer MSAs. See [WindowsProvider](./authentication/windows.md) for more details.
1. Install the `CommunityToolkit.Authentication.Uwp` package
1. Set the [ProviderManager](./authentication/ProviderManager.md).GlobalProvider to a new instance of [WindowsProvider](./authentication/windows.md) with pre-configured scopes:

    ```csharp
    using CommunityToolkit.Authentication;

    string[] scopes = new string[] { "User.Read" };

    ProviderManager.Instance.GlobalProvider = new WindowsProvider(scopes);
    ```

## Sign in a user

Call `SignInAsync` to initiate the login process. This will prompt the user to specify an account or provide credentials.

  ```csharp
using CommunityToolkit.Authentication;

await ProviderManager.Instance.GlobalProvider.SignInAsync();
```

You can also use the [LoginButton](./controls/LoginButton.md) control in UWP XAML apps to support the full sign in/out lifecycle and even display the user's photo and name when signed in.

```xml
<Grid xmlns:controls="using:CommunityToolkit.Graph.Uwp.Controls">
    <controls:LoginButton />
</Grid>
```

## Make a Graph call

Once you are authenticated, you can then make requests to the Graph using the GraphServiceClient instance via [extensions](./helpers/extensions.md).

> Install the `CommunityToolkit.Graph` package.

```csharp
using CommunityToolkit.Authentication;
using CommunityToolkit.Graph.Extensions;

ProviderManager.Instance.ProviderStateChanged += (s, e)
{
    IProvider provider = ProviderManager.Instance.GlobalProvider;
    if (provider?.State == ProviderState.SignedIn)
    {
        var graphClient = provider.GetClient();
        var me = await graphClient.Me.Request().GetAsync();
    }
}
```
