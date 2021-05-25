---
title: Windows Community Toolkit - Graph Helpers and Controls
author: shweaver-MSFT
description: Authentication providers and Graph powered helpers that make it easy to work with Microsoft Graph APIs.
keywords: uwp, wpf, netstandard, windows, community, toolkit, graph, login, authentication, provider, providers, identity
dev_langs:
  - csharp
---

# Windows Community Toolkit - Graph Helpers and Controls

Welcome to the Windows Graph Toolkit! A sub-project of the [Windows Community Toolkit](https://aka.ms/wct) focused on [Microsoft Graph](https://developer.microsoft.com/en-us/graph/) and providing a set of Authentication providers and Graph powered Helpers/Controls that make it easy to work with Microsoft Graph APIs.

Note: This new library replaces the `Microsoft.Toolkit.Uwp.UI.Controls.Graph` package; however, it is not backwards compatible nor does it provide all the same features at this time.

If you need similar controls for the Web, please use the [Microsoft Graph Toolkit](https://aka.ms/mgt).

## What's new?

We've overhauled our approach and introduced some big improvements:

- The new WindowsProvider enables basic consumer login without AAD configuration 🎊
- Authentication packages are now split per provider 🎉
- Access to the GraphServiceClient now lives in a separate package. This means no dependency on the Graph SDK for simple auth scenarios and apps that perform Graph requests manually (sans SDK) 🥳
- Removed Beta Graph SDK, but enabled access with V1 SDK types. This is so our controls and helpers can be based on the stable Graph endpoint, while also allowing for requests to the beta endpoint in some circumstances (Such as retrieving a user's photo) 🎈

For more info on our roadmap, check out the current [Release Plan](https://github.com/windows-toolkit/Graph-Controls/issues/81)

## <a name="supported"></a> Supported SDKs

| Package | Min Supported |
|--|--|
| `CommunityToolkit.Authentication` | NetStandard 2.0 |
| `CommunityToolkit.Authentication.Msal` | NetStandard 2.0 |
| `CommunityToolkit.Authentication.Uwp` | UWP Windows 10 17134 |
| `CommunityTookit.Graph` | NetStandard 2.0 |
| `CommunityToolkit.Graph.Uwp` | UWP Windows 10 17763 |

## <a name="documentation"></a> Getting Started

To get started using Graph data in your application, you'll first need to enable authentication.

The nuget packages metioned below are not yet released, and can be accessed from using our dedicated Nuget feed: [WindowsCommunityToolkit-MainLatest](https://pkgs.dev.azure.com/dotnet/WindowsCommunityToolkit/_packaging/WindowsCommunityToolkit-MainLatest/nuget/v3/index.json):

### 1A. Setup authentication with MSAL

Leverage the official Microsoft Authentication Library (MSAL) to enable authentication in any NetStandard application.

1. Register your app in Azure AAD
    
    Before requesting data from [Microsoft Graph](https://graph.microsoft.com), you will need to [register your application](https://docs.microsoft.com/azure/active-directory/develop/quickstart-register-app) to get a **ClientID**.

    > After finishing the initial registration page, you will also need to add an additional redirect URI. Click on "Add a Redirect URI", then "Add a platform", and then on "Mobile and desktop applications". Check the `https://login.microsoftonline.com/common/oauth2/nativeclient` checkbox on that page. Then click "Configure".

3. Install the `CommunityToolkit.Authentication.Msal` package.
4. Set the [ProviderManager](./authentication/ProviderManager.md).GlobalProvider to a new instance of [MsalProvider](./authentication/msal/MsalProvider.md) with clientId and pre-configured scopes:
    
    ```csharp
    using CommunityToolkit.Authentication;

    string clientId = "YOUR-CLIENT-ID-HERE";
    string[] scopes = new string[] { "User.Read" };

    ProviderManager.Instance.GlobalProvider = new MsalProvider(clientId, scopes);
    ```

> Note: You can use the `Scopes` property to preemptively request permissions from the user of your app for data your app needs to access from Microsoft Graph.

### 1B. Setup authentication with WindowsProvider

Try out the [WindowsProvider](./authentication/uwp/WindowsProvider.md) to enable authentication based on the native Windows Account Manager (WAM) APIs in your UWP apps, without requiring a dependency on MSAL.

1. Associate your app with the Microsoft Store. The app association will act as our minimal app registration for authenticating consumer MSAs. See the [WindowsProvider docs](https://github.com/windows-toolkit/Graph-Controls/edit/main/Docs/WindowsProvider.md) for more details.
1. Install the `CommunityToolkit.Authentication.Uwp` package
1. Set the [ProviderManager](./authentication/ProviderManager.md).GlobalProvider to a new instance of [WindowsProvider](./authentication/uwp/WindowsProvider.md) with pre-configured scopes:

    ```csharp
    using CommunityToolkit.Authentication;

    string[] scopes = new string[] { "User.Read" };

    ProviderManager.Instance.GlobalProvider = new WindowsProvider(scopes);
    ```

### 2. Make a Graph call

Once you are authenticated, you can then make requests to the Graph using the GraphServiceClient instance via [ProviderExtensions](./helpers/ProviderExtensions.md).

> Install the `CommunityToolkit.Graph` package.

```
using CommunityToolkit.Authentication;
using CommunityToolkit.Graph.Extensions;

var provider = ProviderManager.Instance.GlobalProvider;

if (provider != null && provider.State == ProviderState.SignedIn)
{
    var graphClient = provider.GetClient();
    var me = await graphClient.Me.Request().GetAsync();
}
```

**That's all you need to get started!**

You can use the `ProviderManager.Instance` to listen to changes in authentication status with the `ProviderUpdated` event or get direct access to the [.NET Graph Beta API](https://github.com/microsoftgraph/msgraph-beta-sdk-dotnet) through `ProviderManager.Instance.GlobalProvider.GetBetaClient()`, just be sure to check if the `GlobalProvider` has been set first and its `State` is `SignedIn`:

```csharp
using CommunityToolkit.Authentication;
using CommunityToolkit.Graph.Extensions;

public ImageSource GetMyPhoto()
{
    IProvider provider = ProviderManager.Instance.GlobalProvider;
    
    if (provider?.State == ProviderState.SignedIn)
    {
        // Get the beta client
        GraphServiceClient betaGraphClient = provider.GetBetaClient();

        try
        {
            // Make a request to the beta endpoint for the current user's photo.
            var photoStream = await betaGraphClient.Me.Photo.Content.Request().GetAsync();

            using var ras = photoStream.AsRandomAccessStream();
            var bitmap = new BitmapImage();
            await bitmap.SetSourceAsync(ras);

            return bitmap;
        }
        catch
        {
            return null;
        }
    }
}
```
