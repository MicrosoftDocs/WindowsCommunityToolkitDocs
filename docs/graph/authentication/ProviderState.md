---
title: ProviderState
author: shweaver-MSFT
description: ProviderState represents the current authentication state of the session for a given IProvider.
keywords: netstandard, windows, community, toolkit, graph, login, authentication, provider, providers, identity
dev_langs:
  - csharp
---

# ProviderState

ProviderState represents the current authentication state of the session for a given [IProvider](./IProvider.md).

| Name | Description |
| -- | -- |
| Loading | The user's status is not known. |
| SignedOut | The user is signed-out. |
| SignedIn | The user is signed-in. |
