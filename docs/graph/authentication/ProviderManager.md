---
title: ProviderManager
author: shweaver-MSFT
description: ProviderManager manages access to the globally configured IProvider instance and any state change events as users sign in and out.
keywords: uwp, wpf, netstandard, windows, community, toolkit, graph, login, authentication, provider, providers, identity
dev_langs:
  - csharp
---

# ProviderManager

The ProviderManager manages access to the globally configured [IProvider](./custom.md) instance and any state change events as users sign in and out.

> Available in the `CommunityToolkit.Authentication` package.

> [!IMPORTANT]
> Windows Community Toolkit - Graph Controls and Helpers packages are in preview. To get started using WCT preview packages visit the [WCT Preview Packages wiki page](https://aka.ms/wct/wiki/previewpackages).

## Properties

| Property | Type | Description |
| -- | -- | -- |
| State | ProviderState | Gets the current authentication state of the provider. |

## Events

| Event | Type | Description |
| -- | -- | -- |
| ProviderUpdated | EventHandler&lt;IProvider&gt; | Event called when the IProvider changes. |
| ProviderStateChanged | EventHandler&lt;ProviderStateChangedEventArgs&gt; | Event called when the IProvider changes. |

## ProviderStateChangedEventArgs Object

| Property | Type | Description |
| -- | -- | -- |
| OldState | ProviderState | Gets the previous state of the IProvider.
| NewState | ProviderState | Gets the new state of the IProvider.

## ProviderState Enum

| Name | Description |
| -- | -- |
| Loading | The user's status is not known. |
| SignedOut | The user is signed-out. |
| SignedIn | The user is signed-in. |
