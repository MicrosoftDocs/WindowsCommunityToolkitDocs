---
title: ProviderState
author: shweaver-MSFT
description: ProviderState represents the current authentication state of the session for a given IProvider.
keywords: netstandard, windows, community, toolkit, graph, login, authentication, provider, providers, identity
dev_langs:
  - csharp
---

### WebAccountProviderConfig

Configuration values for what type of authentication providers to  enable via the [WindowsProvider](./WindowsProvider.md).

| Property | Type | Description |
| -- | -- | -- |
| ClientId | string | Client Id obtained from Azure registration. |
| WebAccountsProviderType | WebAccountsProviderType | The types of accounts providers that should be available to the user. |
