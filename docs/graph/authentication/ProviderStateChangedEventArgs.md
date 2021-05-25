---
title: ProviderStateChangedEventArgs
author: shweaver-MSFT
description: EventArgs for the IProvider.StateChanged event.
keywords: netstandard, windows, community, toolkit, graph, login, authentication, provider, providers, identity
dev_langs:
  - csharp
---

# ProviderStateChangedEventArgs

EventArgs for the [IProvider](./IProvider.md).StateChanged event.

| Property | Type | Description |
| -- | -- | -- |
| OldState | [ProviderState](./IProvider.md) | Gets the previous state of the [IProvider](./IProvider.md).
| NewState | [ProviderState](./IProvider.md) | Gets the new state of the [IProvider](./IProvider.md).
