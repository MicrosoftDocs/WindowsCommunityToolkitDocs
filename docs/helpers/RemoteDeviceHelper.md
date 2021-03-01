---
title: RemoteDeviceHelper
author: avknaidu
description: The RemoteDeviceHelper is a Helper to get a List Remote Devices that are accessible.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, RemoteDeviceHelper, helper
dev_langs:
  - csharp
---

# RemoteDeviceHelper

The [RemoteDeviceHelper](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.uwp.helpers.remotedevicehelper) gives you a list of Remote Systems. All the systems must be signed in with the same Microsoft Account (MSA)

> [!IMPORTANT]
> Make sure you enable the [RemoteSystem capability](https://docs.microsoft.com/windows/uwp/packaging/app-capability-declarations#general-use-capabilities) in your app's `package.appxmanifest` to access remote system information.

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://Helpers?sample=RemoteDeviceHelper)

## Syntax

```csharp

RemoteDeviceHelper _remoteDeviceHelper = new RemoteDeviceHelper();

```

You can also use default filter types for initializing. Like Below.

```csharp

var filters = new List<IRemoteSystemFilter>
{
    new RemoteSystemDiscoveryTypeFilter(RemoteSystemDiscoveryType.Cloud),
    new RemoteSystemAuthorizationKindFilter(RemoteSystemAuthorizationKind.SameUser),
    new RemoteSystemStatusTypeFilter(RemoteSystemStatusType.Available)
};

RemoteDeviceHelper _remoteDeviceHelper = new RemoteDeviceHelper(filters);
```

## Example

```csharp
// without filters

RemoteDeviceHelper _remoteDeviceHelper = new RemoteDeviceHelper();
DevicesList.DataContext = _remoteDeviceHelper;


// with filters

var filters = new List<IRemoteSystemFilter>
{
    new RemoteSystemDiscoveryTypeFilter(RemoteSystemDiscoveryType.Cloud),
    new RemoteSystemAuthorizationKindFilter(RemoteSystemAuthorizationKind.SameUser),
    new RemoteSystemStatusTypeFilter(RemoteSystemStatusType.Available)
};

RemoteDeviceHelper _remoteDeviceHelper = new RemoteDeviceHelper(filters);
DevicesList.DataContext = _remoteDeviceHelper;

```

```xaml

<ListView ItemsSource="{Binding RemoteSystems}" x:Name="DevicesList">
  <ListView.ItemTemplate>
    <DataTemplate>
	  <Grid>
		<Grid.RowDefinitions>
		  <RowDefinition Height="*"/>
		  <RowDefinition Height="*"/>
		</Grid.RowDefinitions>
		<TextBlock Text="{Binding DisplayName}" Tag="{Binding }" Grid.Row="0" />
		<TextBlock Text="{Binding ModelDisplayName}" Tag="{Binding }" Grid.Row="1" />
	  </Grid>
    </DataTemplate>
  </ListView.ItemTemplate>
</ListView>

```

## Sample Project

[RemoteDeviceHelper Sample Page Source](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/master/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/RemoteDeviceHelper). You can [see this in action](uwpct://Helpers?sample=RemoteDeviceHelper) in the [Windows Community Toolkit Sample App](https://aka.ms/uwptoolkitapp).

## Requirements

| Device family | Universal, 10.0.16299.0 or higher |
| --- | --- |
| Namespace | Microsoft.Toolkit.Uwp.Helpers |
| NuGet package | [Microsoft.Toolkit.Uwp](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp/) |

## API

* [RemoteDeviceHelper source code](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/master/Microsoft.Toolkit.Uwp/Helpers/RemoteDeviceHelper)

## Related Topics

* [Project Rome](https://developer.microsoft.com/en-us/windows/project-rome)
* [Remote Systems Sample](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/RemoteSystems)
* [Connected apps and devices (Project Rome)](https://docs.microsoft.com/windows/uwp/launch-resume/connected-apps-and-devices)
* [Communicate with a remote app service](https://docs.microsoft.com/windows/uwp/launch-resume/communicate-with-a-remote-app-service)
* [AppServices Sample](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/AppServices)
