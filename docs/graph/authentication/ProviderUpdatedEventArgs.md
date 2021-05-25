---
title: ProviderUpdatedEventArgs
author: shweaver-MSFT
description: EventsArgs class for the ProviderManager ProviderUpdated event.
keywords: netstandard, windows, community, toolkit, graph, login, authentication, provider, providers, identity
dev_langs:
  - csharp
---

# ProviderUpdatedEventArgs

EventsArgs class for the [ProviderManager](./ProviderManager.md).ProviderUpdated event.

## Properties

| Property | Type | Description |
| -- | -- | -- |
| Reason | ProviderManagerChangedState | Gets the reason for the provider update. |

## Enums

### ProviderManagerChangedState

Enumeration of potential reasons for a provider state change.

| Name | Description |
| -- | -- |
| ProviderStateChanged | The [IProvider](./IProvider.md) state has changed.|
| ProviderUpdated | The [IProvider](./IProvider.md) itself has changed. |
