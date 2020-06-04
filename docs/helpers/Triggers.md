---
title: State Triggers
author: dotMorten
description: A collection of custom visual State Triggers
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, CompareStateTrigger, FullScreenModeStateTrigger, IsEqualStateTrigger, IsNotEqualStateTrigger, IsNullOrEmptyStateTriggers, NetworkConnectionStateTrigger, RegexStateTrigger, UserHandPreferenceStateTrigger, UserInteractionModeStateTrigger
dev_langs:
  - csharp
---

# State Triggers

<!-- Describe your control -->
A collection of custom visual [State Triggers](https://docs.microsoft.com/dotnet/api/Microsoft.Toolkit.Uwp.UI.Triggers)

<!-- Use below format to display note
> [!NOTE]
> Some note

> [!IMPORTANT]
> Some important note

> [!WARNING]
> Some warning note
-->

| Trigger | Purpose |
| --- | --- |
| [CompareStateTrigger](https://docs.microsoft.com/dotnet/api/Microsoft.Toolkit.Uwp.UI.Triggers.CompareStateTrigger) | Enables a state if the value is equal to, greater than, or less than another value |
| [FullScreenModeStateTrigger](https://docs.microsoft.com/dotnet/api/Microsoft.Toolkit.Uwp.UI.Triggers.FullScreenModeStateTrigger) | Trigger for switching when in full screen mode |
| [IsEqualStateTrigger](https://docs.microsoft.com/dotnet/api/Microsoft.Toolkit.Uwp.UI.Triggers.IsEqualStateTrigger) | Enables a state if the value is equal to another value |
| [IsNotEqualStateTrigger](https://docs.microsoft.com/dotnet/api/Microsoft.Toolkit.Uwp.UI.Triggers.IsNotEqualStateTrigger) | Enables a state if the value is not equal to another value |
| [IsNullOrEmptyStateTriggers](https://docs.microsoft.com/dotnet/api/Microsoft.Toolkit.Uwp.UI.Triggers.IsNullOrEmptyStateTriggers) | Enables a state if an Object is null or a String/IEnumerable is empty |
| [NetworkConnectionStateTrigger](https://docs.microsoft.com/dotnet/api/Microsoft.Toolkit.Uwp.UI.Triggers.NetworkConnectionStateTrigger) | Trigger for switching when the network availability changes |
| [RegexStateTrigger](https://docs.microsoft.com/dotnet/api/Microsoft.Toolkit.Uwp.UI.Triggers.RegexStateTrigger) | Enables a state if the regex expression is true for a given string value |
| [UserHandPreferenceStateTrigger](https://docs.microsoft.com/dotnet/api/Microsoft.Toolkit.Uwp.UI.Triggers.UserHandPreferenceStateTrigger) | Trigger for switching UI based on whether the user favors their left or right hand |
| [UserInteractionModeStateTrigger](https://docs.microsoft.com/dotnet/api/Microsoft.Toolkit.Uwp.UI.Triggers.UserInteractionModeStateTrigger) | Trigger for switching when the User interaction mode changes (tablet mode) |

## CompareStateTrigger Example
```
<VisualState.StateTriggers>
    <triggers:CompareStateTrigger Value="{Binding Value,ElementName=Slider, Mode=OneWay}" To="3" Comparison="LessThan" />
</VisualState.StateTriggers>
```
## FullScreenModeStateTrigger Example 
```
<VisualState.StateTriggers>
    <triggers:FullScreenModeStateTrigger IsFullScreen="true" />
</VisualState.StateTriggers>
```                    
## IsEqualStateTrigger Example
```
<VisualState.StateTriggers>
    <triggers:IsEqualStateTrigger Value="{Binding IsChecked, ElementName=checkbox, Mode=OneWay}" To="{x:Null}" />
</VisualState.StateTriggers>
```
## IsNotEqualStateTrigger Example
```
<VisualState.StateTriggers>
    <triggers:IsNotEqualStateTrigger Value="{Binding IsChecked, ElementName=checkbox, Mode=OneWay}" To="{x:Null}" />
</VisualState.StateTriggers>
```
## IsNullOrEmptyStateTriggers Example
```
<VisualState.StateTriggers>
    <triggers:IsNullOrEmptyStateTrigger Value="{Binding Text, ElementName=OurTextBox, Mode=OneWay}"/>
</VisualState.StateTriggers>
```              
## NetworkConnectionStateTrigger Example
```
<VisualState.StateTriggers>
    <triggers:NetworkConnectionStateTrigger ConnectionState="Connected" />
</VisualState.StateTriggers>
```
## RegexStateTrigger Example
```
<VisualState.StateTriggers>
    <triggers:RegexStateTrigger Value="{Binding Text, ElementName=emailTextBox, Mode=OneWay}"
		                    Expression="^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,4}$"
				    Options="IgnoreCase" />
</VisualState.StateTriggers>
```
## UserHandPreferenceStateTrigger Example
```
<VisualState.StateTriggers>
    <triggers:UserHandPreferenceStateTrigger HandPreference="LeftHanded" />
</VisualState.StateTriggers>
```
## UserInteractionModeStateTrigger Example
```
<VisualState.StateTriggers>
    <triggers:UserInteractionModeStateTrigger InteractionMode="Mouse" />
</VisualState.StateTriggers>
```

## Sample Project

<!-- Link to the sample page in the Windows Community Toolkit Sample App -->
[Triggers sample page Source](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/master/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/Triggers). You can [see this in action](uwpct://CategoryName?sample=pageName) in [Windows Community Toolkit Sample App](http://aka.ms/uwptoolkitapp).

## Requirements

| Device family | Universal, 10.0.16299.0 or higher   |
| -- | -- |
| Namespace | Microsoft.Toolkit.Uwp.UI.Triggers |
| NuGet package | [Microsoft.Toolkit.Uwp](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI/) |


## API

* [Triggers source code](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/master/Microsoft.Toolkit.Uwp.UI/Triggers)
