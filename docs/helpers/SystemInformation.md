---
title: SystemInformation
author: nmetulev
description: The SystemInformation class is a utility class that provides properties with some system, application and device information.

keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, SystemInformation
---

# SystemInformation

The [SystemInformation](/dotnet/api/microsoft.toolkit.uwp.helpers.systeminformation?view=uwp-toolkit-dotnet) class is a utility class that provides properties with some system, application and device information.

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://Helpers?sample=SystemInformation)

## Properties

| Property | Type | Description |
| -- | -- | -- |
| ApplicationName | string | Gets the application's name as a `string` |
| ApplicationVersion | [PackageVersion](/uwp/api/Windows.ApplicationModel.PackageVersion) | Gets the application's version as a [PackageVersion](/uwp/api/Windows.ApplicationModel.PackageVersion) |
| AppUptime | TimeSpan | Gets the length of time this instance of the app has been running. |
| AvailableMemory | float | Gets the available memory in _MB_ as a `float` |
| Culture | CultureInfo | Gets the most preferred language by the user as a [CultureInfo](/dotnet/api/system.globalization.cultureinfo) |
| DeviceFamily | string | Gets the family of used device as a `string`. Common `DeviceFamily` values include: Windows.Desktop, Windows.Mobile, Windows.Xbox, Windows.Holographic, Windows.Team, Windows.IoT. Prepare your code for other values |
| DeviceManufacturer | string | Gets the name of device manufacturer as a `string`. The value will be empty if the device manufacturer couldn't be determined (ex: when running in a virtual machine). |
| DeviceModel | string | Gets the model of the device as a `string`. The value will be empty if the device model couldn't be determined (ex: when running in a virtual machine). |
| FirstUseTime | DateTime | Gets the DateTime (in UTC) that the app as first used. |
| FirstVersionInstalled | [PackageVersion](/uwp/api/Windows.ApplicationModel.PackageVersion) | Gets the first version of the app that was installed. |
| PreviousVersionInstalled | [PackageVersion](/uwp/api/Windows.ApplicationModel.PackageVersion) | Gets the previous version of the app that was installed. |
| Instance | SystemInformation | Gets public singleton property. |
| IsFirstRun | bool | Gets a value indicating whether the app is being used for the first time since it was installed. |
| IsAppUpdated | bool | Gets a value indicating whether the app is being used for the first time since being upgraded from an older version. |
| LastLaunchTime | DateTime | Gets the DateTime (in UTC) that this was previously launched. |
| LastResetTime | DateTime | Gets the DateTime (in UTC) when the launch count was previously reset. |
| LaunchCount | long | Gets the number of times the app has been launched since the last reset. |
| LaunchTime | DateTime | Gets the DateTime (in UTC) that this instance of the app was launched. |
| OperatingSystem | string | Gets the operating system as a `string` |
| OperatingSystemArchitecture | [ProcessorArchitecture](/uwp/api/Windows.System.ProcessorArchitecture) | Gets used processor architecture as `ProcessorArchitecture` |
| OperatingSystemVersion | [OSVersion](/dotnet/api/microsoft.toolkit.uwp.helpers.osversion) | Gets the operating system version (for example 10.0.10586.0) as `OSVersion` structure |
| TotalLaunchCount | long | Gets the number of times the app has been launched. |

## Methods

| Method | Return Type | Description |
| ------ | ----------- | -- |
| AddToAppUptime(TimeSpan) | void | Add to the record of how long the app has been running. Use this to optionally include time spent in background tasks or extended execution |
| LaunchStoreForReviewAsync() | Task | Launch the store app so the user can leave a review. |
| ResetLaunchCount() | void | Reset launch count so you can get launch count from a new perspective |
| TrackAppUse() | void | Track app launch time and count. |

## Sample Project

[System Information Sample Page Source](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.0.0/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/SystemInformation). You can [see this in action](uwpct://Helpers?sample=SystemInformation) in the [Windows Community Toolkit Sample App](https://aka.ms/windowstoolkitapp).

## Requirements

| Device family | Universal, 10.0.16299.0 or higher |
| --- | --- |
| Namespace | Microsoft.Toolkit.Uwp |
| NuGet package | [Microsoft.Toolkit.Uwp](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp/) |

## API

* [SystemInformation source code](https://github.com/windows-toolkit/WindowsCommunityToolkit/blob/rel/7.0.0/Microsoft.Toolkit.Uwp/Helpers/SystemInformation.cs)
