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

## IProvider extension methods

The following extension methods are available on `IProvider` via the `CommunityToolkit.Graph.Extensions` namespace.

| Method | Arguments | Returns | Description |
| -- | -- | -- | -- |
| GetClient | | GraphServiceClient | Retrieve pre-configured GraphServiceClient instance for making authenticated Graph calls, using the v1 endpoint. |
| GetBetaClient | | GraphServiceClient | Retrieve pre-configured GraphServiceClient instance for making authenticated Graph calls, using the beta endpoint. |

## Handle Graph requests manually

Access APIs by managing requests to Microsoft Graph yourself. This is helpful for projects with existing systems for managing web requests, or for keeping package sizes minimal by excluding the Graph SDK.

To make Graph API calls manually, use the `HttpRequestMessage.AuthenticateAsync()` extension method to authenticate any outgoing requests.

```csharp
using CommunityToolkit.Authentication;
using CommunityToolkit.Authentication.Extensions;
using Newtonsoft.Json;
using Newtonsoft.Json.Linq;

private async Task<IList<TodoTask>> GetDefaultTaskListAsync()
{
    return await GetResponseAsync<List<TodoTask>>("https://graph.microsoft.com/v1.0/me/todo/lists/tasks/tasks");
}

private async Task<T> GetResponseAsync<T>(string requestUri)
{
    // Build the request
    var getRequest = new HttpRequestMessage(HttpMethod.Get, requestUri);

    // Authenticate the request using an extension on HttpRequestMessage.
    await getRequest.AuthenticateAsync();

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

## HttpRequestMessage extension methods

The extension methods are available on `HttpRequestMessage` via the `CommunityToolkit.Authenticaiton.Extensions` namespace.

| Method | Arguments | Returns | Description |
| -- | -- | -- | -- |
| AuthenticateAsync | | HttpRequestMessage | Authenticate an http request using the current GlobalProvider instance. |
