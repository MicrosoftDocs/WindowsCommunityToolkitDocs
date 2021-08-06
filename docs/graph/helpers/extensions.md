---
title: Microsoft Graph Extensions
author: shweaver-MSFT
description: Extension methods that enable Graph API calls using the global authentication provider.
keywords: uwp, wpf, netstandard, windows, community, toolkit, graph, provider, providers, extensions
dev_langs:
  - csharp
---

# Microsoft Graph Extensions

Use toolkit extensions to help you make calls to Graph APIs using the global authentication provider. Available in the `CommunityToolkit.Graph` package, `CommunityToolkit.Graph.Extensions` namespace.

> [!IMPORTANT]
> Windows Community Toolkit - Graph Controls and Helpers packages are in preview. To get started using WCT preview packages visit the [WCT Preview Packages wiki page](https://aka.ms/wct/wiki/previewpackages).

## Call Microsoft Graph APIs

Once authenticated, you can make API calls to Microsoft Graph using a preconfigured `GraphServiceClient` instance. Access to the client is enabled through an extension method on [IProvider](../authentication/custom.md) called, `GetClient()`.

```csharp
using CommunityToolkit.Authentication;
using CommunityToolkit.Graph.Extensions;

IProvider provider = ProviderManager.Instance.GlobalProvider;

if (provider?.State == ProviderState.SignedIn)
{
    // Get the Graph client
    GraphServiceClient graphClient = provider.GetClient();

    // Make a request for the current user.
    var me = await graphClient.Me.Request().GetAsync();
}
```

## Make Beta API calls

You can also get access to a beta version of the client by calling `GetBetaClient()`.
It won't return types from the Beta SDK, but it does enable access to some beta-only content like user photos.

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

## Extension methods

The following extension methods are available on `IProvider` via the `CommunityToolkit.Graph.Extensions` namespace.

| Method | Arguments | Returns | Description |
| -- | -- | -- | -- |
| GetClient | | GraphServiceClient | Retrieve pre-configured GraphServiceClient instance for making authenticated Graph calls, using the v1 endpoint. |
| GetBetaClient | | GraphServiceClient | Retrieve pre-configured GraphServiceClient instance for making authenticated Graph calls, using the beta endpoint. |
