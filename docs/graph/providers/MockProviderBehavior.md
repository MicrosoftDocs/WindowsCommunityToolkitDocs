---
title: MockProviderBehavior XAML Behavior
author: michael-hawker
description: The MockProviderBehavior provides sample data from Microsoft Graph.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, graph, login, authentication, interactive, provider, identity, mock, sample
dev_langs:
  - csharp
---

# MockProviderBehavior XAML Behavior

> [!WARNING]
> (This API has been removed. Please use the official [Microsoft Graph SDK](https://github.com/microsoftgraph/msgraph-sdk-dotnet) directly. For the latest guidance on using the Microsoft Graph in the Toolkit check out the [Windows Community Toolkit - Graph Helpers and Controls](../overview.md).)

<!-- Describe your control -->
The [MockProviderBehavior](/dotnet/api/microsoft.toolkit.graph.providers.mockproviderbehavior) provides sample data from the Microsoft Graph for demonstration and learning purposes only.

Add this behavior to your application's main page. It only needs to be added to a single page to bootstrap all the other Graph enabled XAML controls.

## Syntax

```xaml
  <Interactivity:Interaction.Behaviors>
      <providers:MockProviderBehavior/>
  </Interactivity:Interaction.Behaviors>
```

## Properties

| Property | Type | Description |
| -- | -- | -- |
| SignedIn | bool | Value to indicate if the provider should be in the signed-in state at initialization. |

## Requirements

| Device family | Universal, MinVersion or higher   |
| -- | -- |
| Namespace | Microsoft.Toolkit.Graph.Providers |
| NuGet package | [Microsoft.Toolkit.Graph.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Graph.Controls) |

## API

* [MockProviderBehavior source code](https://github.com/windows-toolkit/Graph-Controls/blob/rel/7.0.0/Microsoft.Toolkit.Graph.Controls/Providers/MockProviderBehavior.cs)