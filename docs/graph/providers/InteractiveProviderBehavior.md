---
title: InteractiveProviderBehavior XAML Behavior
author: michael-hawker
description: The InteractiveProviderBehavior provides an easy way in XAML to connect to Microsoft Graph.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, graph, login, authentication, interactive, provider, identity, xaml islands
dev_langs:
  - csharp
---

# InteractiveProviderBehavior XAML Behavior

> [!WARNING]
> (This API has been removed. Please use the official [Microsoft Graph SDK](https://github.com/microsoftgraph/msgraph-sdk-dotnet) directly. For the latest guidance on using the Microsoft Graph in the Toolkit check out the [Windows Community Toolkit - Graph Helpers and Controls](../overview.md).)

The [InteractiveProviderBehavior](/dotnet/api/microsoft.toolkit.graph.providers.interactiveproviderbehavior) provides a quick and easy way to connect to the Microsoft Identity platform and Microsoft Graph.  It is built on top of the Graph SDK's authentication providers, but allows usage from XAML.

Add this behavior to your application's main page. It only needs to be added to a single page to bootstrap all the other Graph enabled XAML controls.

> [!IMPORTANT]
> Be sure to Register Client Id in Azure first following the guidance here: <https://docs.microsoft.com/azure/active-directory/develop/quickstart-register-app>
>
> After finishing the initial registration page, you will also need to add an additional redirect URI. Click on "Add a Redirect URI" and check the "https://login.microsoftonline.com/common/oauth2/nativeclient" checkbox on that page. Then click "Save".

## Syntax

```xaml
  <Interactivity:Interaction.Behaviors>
      <providers:InteractiveProviderBehavior ClientId="YOUR_CLIENT_ID_HERE" Scopes="User.Read,User.ReadBasic.All,People.Read,Calendars.Read"/>
  </Interactivity:Interaction.Behaviors>
```

## WPF

> [!IMPORTANT]
> This provider must be initialized in your WPF app when using the XAML Graph controls from [XAML Islands](/windows/apps/desktop/modernize/xaml-islands). The same syntax above is used; however, you must include the [Microsoft.Toolkit.Wpf.Graph.Providers](https://www.nuget.org/packages/Microsoft.Toolkit.Wpf.Graph.Providers) NuGet package instead.

## Properties

| Property | Type | Description |
| -- | -- | -- |
| ClientId | string | Client Id obtained from Azure registration. |
| RedirectUri | string | Client's authentication uri redirect as configured in Azure. |
| Scopes | ScopeSet | Comma-delimited list of scopes to pre-authorize from user during authentication. |

## Requirements

| Device family | Universal, MinVersion or higher   |
| -- | -- |
| Namespace | Microsoft.Toolkit.Graph.Providers |
| NuGet package | [Microsoft.Toolkit.Graph.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Graph.Controls) |

## API

* [InteractiveProviderBehavior source code](https://github.com/windows-toolkit/Graph-Controls/blob/rel/7.0.0/Microsoft.Toolkit.Graph.Controls/Providers/InteractiveProviderBehavior.cs)
* [InteractiveProviderBehavior usage in XAML Islands Sample](https://github.com/windows-toolkit/Graph-Controls/blob/rel/7.0.0/Samples/XAML%20Islands/WPF-Core-GraphApp/MainWindow.xaml)

## Related Topics

* [Graph SDK Authentication Providers](https://github.com/microsoftgraph/msgraph-sdk-dotnet-auth)
* [App Registration Quick-Start for Client Id](/azure/active-directory/develop/quickstart-register-app)