---
title: ProviderManager
author: shweaver-MSFT
description: ProviderManager manages access to the globally configured IProvider instance and any state change events as users sign in and out.
keywords: uwp, wpf, netstandard, windows, community, toolkit, graph, login, authentication, provider, providers, identity
dev_langs:
  - csharp
---

# ProviderManager

The ProviderManager manages access to the globally configured [IProvider](./IProvider.md) instance and any state change events as users sign in and out.

> Available in the `CommunityToolkit.Authentication` package.

> [!IMPORTANT]
> Windows Community Toolkit - Graph Controls and Helpers packages are in preview. To get started using WCT preview packages visit the [WCT Preview Packages wiki page](https://aka.ms/wct/wiki/previewpackages).

## Set the GlobalProvider

```csharp
using CommunityToolkit.Authentication;

ProviderManager.Instance.GlobalProvider = new WindowsProvider();
```

## Listen for changes to the GlobalProvider

```csharp
using CommunityToolkit.Authentication;

ProviderManager.Instance.ProviderUpdated += OnProviderUpdated;

void OnProviderUpdated(object sender, ProviderUpdatedEventArgs e)
{
    if (e.Reason == ProviderManagerChangedState.ProviderUpdated)
    {
        // The GlobalProvider has been set.
    }

    if (e.Reason == ProviderManagerChangedState.ProviderStateChanged)
    {
        // The GlobalProvider state has changed.
    }
}
```

## Properties

| Property | Type | Description |
| -- | -- | -- |
| State | ProviderState | Gets the current authentication state of the provider. |

## Events

| Event | Type | Description |
| -- | -- | -- |
| ProviderUpdated | EventHandler&lt;ProviderUpdatedEventArgs&gt; | Event called when the IProvider changes. |

## ProviderUpdatedEventArgs Object

| Property | Type | Description |
| -- | -- | -- |
| Reason | ProviderManagerChangedState | Gets the reason for the provider update. |

## ProviderManagerChangedState Enum

| Name | Description |
| -- | -- |
| ProviderStateChanged | The [IProvider](./IProvider.md) state has changed.|
| ProviderUpdated | The [IProvider](./IProvider.md) itself has changed. |
