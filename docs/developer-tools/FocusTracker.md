---
title: FocusTracker XAML Control 
author: nmetulev
description: The FocusTracker Control can be used to display information about the current focused XAML element (if any).
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, FocusTracker, XAML Control, xaml 
---

# FocusTracker XAML Control

The [FocusTracker Control](/dotnet/api/microsoft.toolkit.uwp.developertools.focustracker) can be used to display information about the current focused XAML element (if any).

FocusTracker will display the following information (when available) about the current focused XAML element:

- Name
- Type
- AutomationProperties.Name
- Name of the first parent in hierarchy with a name

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://Controls?sample=FocusTracker)

## Syntax

```xaml
<developerTools:FocusTracker IsActive="True"/>
```

## Sample Output

![FocusTracker image](../resources/images/DeveloperTools/FocusTracker.jpg)

## Properties

| Property | Type | Description |
| -- | -- | -- |
| IsActive | bool | Gets or sets a boolean indicating whether the tracker is running or not |

## Sample Project

[FocusTracker Sample Page Source](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.1.0/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/FocusTracker). You can [see this in action](uwpct://Controls?sample=FocusTracker) in the [Windows Community Toolkit Sample App](https://aka.ms/windowstoolkitapp).

## Requirements

| Device family | Universal, 10.0.16299.0 or higher |
| --- | --- |
| Namespace | Microsoft.Toolkit.Uwp.DeveloperTools |
| NuGet package | [Microsoft.Toolkit.Uwp.DeveloperTools](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.DeveloperTools/) |

## API

- [FocusTracker source code](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.1.0/Microsoft.Toolkit.Uwp.DeveloperTools/FocusTracker)
