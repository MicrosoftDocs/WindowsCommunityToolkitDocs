---
title: RemoteDevicePicker Control
author: avknaidu
description: The RemoteDevicePicker control helps you to pick a device that you can use to Remote Launch Apps, Services.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, RemoteDevicePicker, picker
dev_langs:
  - csharp
---

# RemoteDevicePicker Control

The [RemoteDevicePicker](/dotnet/api/microsoft.toolkit.uwp.ui.controls.remotedevicepicker) gives you a list of Remote Systems. All the systems must be signed in with the same Microsoft Account (MSA)

> [!IMPORTANT]
> Make sure you enable the [RemoteSystem capability](/windows/uwp/packaging/app-capability-declarations#general-use-capabilities) in your app's `package.appxmanifest` to access remote system information.

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://Controls?sample=RemoteDevicePicker)

## Syntax

```csharp
RemoteDevicePicker remoteDevicePicker = new RemoteDevicePicker()
{
    Title = "Pick Remote Device",
    SelectionMode = RemoteDevicesSelectionMode.Multiple
};
var result = await remoteDevicePicker.PickDeviceAsync();
await new MessageDialog($"You picked {result.Count.ToString()} Device(s)" + Environment.NewLine + string.Join(",", result.Select(x => x.DisplayName.ToString()).ToList())).ShowAsync();
```

You can also use default filter types for initializing. Like Below.

```csharp
RemoteDevicePicker remoteDevicePicker = new RemoteDevicePicker(RemoteSystemDiscoveryType.Proximal, RemoteSystemAuthorizationKind.Anonymous, RemoteSystemStatusType.Any)
{
    Title = "Pick Remote Device",
    SelectionMode = RemoteDevicesSelectionMode.Multiple
};

var remoteSystems = await remoteDevicePicker.PickDeviceAsync();
await new MessageDialog($"You picked {remoteSystems.Count().ToString()} Device(s)" + Environment.NewLine + string.Join(",", remoteSystems.Select(x => x.DisplayName.ToString()).ToList())).ShowAsync();
```

## Properties

| Property | Type | Description |
| -- | -- | -- |
| SelectionMode | RemoteDevicesSelectionMode | Gets or sets the DeviceList Selection Mode. Defaults to RemoteDevicesSelectionMode.Single |
| ShowAdvancedFilters | Boolean | Gets or sets a value indicating whether Advanced Filters are visible or not. Defaults to false |

## Sample Project

[RemoteDevicePicker Sample Page Source](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.0.0/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/RemoteDevicePicker). You can [see this in action](uwpct://Controls?sample=RemoteDevicePicker) in the [Windows Community Toolkit Sample App](https://aka.ms/windowstoolkitapp).

## Default Template

[RemoteDevicePicker XAML File](https://github.com/windows-toolkit/WindowsCommunityToolkit/blob/rel/7.0.0/Microsoft.Toolkit.Uwp.UI.Controls/RemoteDevicePicker/RemoteDevicePicker.xaml) is the XAML template used in the toolkit for the default styling.

## Requirements

| Device family | Universal, 10.0.16299.0 or higher |
| --- | --- |
| Namespace | Microsoft.Toolkit.Uwp.UI.Controls |
| NuGet package | [Microsoft.Toolkit.Uwp.UI.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI.Controls/) |

## API

* [RemoteDevicePicker source code](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.0.0/Microsoft.Toolkit.Uwp.UI.Controls.Input/RemoteDevicePicker)

## Related Topics

* [Project Rome](https://developer.microsoft.com/windows/project-rome)
* [Remote Systems Sample](https://github.com/Microsoft/Windows-universal-samples/tree/rel/7.0.0/Samples/RemoteSystems)
* [Connected apps and devices (Project Rome)](/windows/uwp/launch-resume/connected-apps-and-devices)
* [Communicate with a remote app service](/windows/uwp/launch-resume/communicate-with-a-remote-app-service)
* [AppServices Sample](https://github.com/Microsoft/Windows-universal-samples/tree/rel/7.0.0/Samples/AppServices)
