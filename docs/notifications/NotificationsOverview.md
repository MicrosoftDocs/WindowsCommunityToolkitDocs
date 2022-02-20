---
title: Notifications Overview 
author: andrewleader
description: Instead of having to deal with XML, you can now use Windows Community toolkit and its notification extensions to work with Tiles and notifications using a complete object model.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, adaptive live tiles, interactive toast, tiles, notifications
---

# Notifications Overview

Adaptive Live Tiles and interactive Toasts are key engagement components of a UWP Application on Windows 10.
Instead of having to deal with XML, you can now use Windows Community toolkit and its notification extensions to work with Tiles and notifications using a complete object model.

## Tiles

| Documentation |
| --- |
| [Create Adaptive Tile](/windows/uwp/design/shell/tiles-and-notifications/create-adaptive-tiles) |
| [Sending a local Tile notification](/windows/uwp/design/shell/tiles-and-notifications/sending-a-local-tile-notification) |

### Sample Output

![LiveTile Image](../resources/images/Notifications/LiveTile.gif)

## Toasts

| Documentation |
| --- |
| [Interactive Toast Notifications](/windows/uwp/design/shell/tiles-and-notifications/adaptive-interactive-toasts) |
| [Send a local toast](/windows/uwp/design/shell/tiles-and-notifications/send-local-toast)

### Sample Output

![Toast](../resources/images/Notifications/PopToast.gif "Toast")

### Sending toasts from desktop C# apps

If you're developing a non-UWP C# app for Windows, the Windows Community Toolkit makes it easier to send an interactive toast notification from your desktop C# app. To learn more, see [Send a local toast notification from C# apps](/windows/uwp/design/shell/tiles-and-notifications/send-local-toast).

## Requirements

| Device family | Universal, 10.0.10240.0 or higher |
| --- | --- |
| Namespace for C# | Microsoft.Toolkit.Uwp.Notifications |
| Namespace for JavaScript | Microsoft.Toolkit.Uwp.Notifications.Javascript |

## API

* [Notifications source code](https://github.com/CommunityToolkit/WindowsCommunityToolkit/tree/rel/7.1.0/Microsoft.Toolkit.Uwp.Notifications)

## Related Topics

* [Toast Notification UX Guidance](/windows/uwp/design/shell/tiles-and-notifications/toast-ux-guidance)
