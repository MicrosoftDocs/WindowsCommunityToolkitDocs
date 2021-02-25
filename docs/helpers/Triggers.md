---
title: State Triggers
author: dotMorten
description: A collection of custom visual State Triggers
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, CompareStateTrigger, FullScreenModeStateTrigger, IsEqualStateTrigger, IsNotEqualStateTrigger, IsNullOrEmptyStateTriggers, NetworkConnectionStateTrigger, RegexStateTrigger, UserHandPreferenceStateTrigger, UserInteractionModeStateTrigger

---

# State Triggers

<!-- Describe your control -->
A collection of custom visual [State Triggers](/uwp/api/windows.ui.xaml.statetrigger).

| Trigger | Purpose |
| --- | --- |
| [CompareStateTrigger](/dotnet/api/Microsoft.Toolkit.Uwp.UI.Triggers.CompareStateTrigger) | Enables a state if the value is equal to, greater than, or less than another value |
| [FullScreenModeStateTrigger](/dotnet/api/Microsoft.Toolkit.Uwp.UI.Triggers.FullScreenModeStateTrigger) | Trigger for switching when in full screen mode |
| [IsEqualStateTrigger](/dotnet/api/Microsoft.Toolkit.Uwp.UI.Triggers.IsEqualStateTrigger) | Enables a state if the value is equal to another value |
| [IsNotEqualStateTrigger](/dotnet/api/Microsoft.Toolkit.Uwp.UI.Triggers.IsNotEqualStateTrigger) | Enables a state if the value is not equal to another value |
| [IsNullOrEmptyStateTrigger](/dotnet/api/Microsoft.Toolkit.Uwp.UI.Triggers.IsNullOrEmptyStateTrigger) | Enables a state if an Object is null or a String/IEnumerable is empty |
| [NetworkConnectionStateTrigger](/dotnet/api/Microsoft.Toolkit.Uwp.UI.Triggers.NetworkConnectionStateTrigger) | Trigger for switching when the network availability changes |
| [RegexStateTrigger](/dotnet/api/Microsoft.Toolkit.Uwp.UI.Triggers.RegexStateTrigger) | Enables a state if the regex expression is true for a given string value |
| [UserHandPreferenceStateTrigger](/dotnet/api/Microsoft.Toolkit.Uwp.UI.Triggers.UserHandPreferenceStateTrigger) | Trigger for switching UI based on whether the user favors their left or right hand |
| [UserInteractionModeStateTrigger](/dotnet/api/Microsoft.Toolkit.Uwp.UI.Triggers.UserInteractionModeStateTrigger) | Trigger for switching when the User interaction mode changes (tablet mode) |

## CompareStateTrigger Example
```xml
<VisualState.StateTriggers>
    <triggers:CompareStateTrigger Value="{Binding Value,ElementName=Slider, Mode=OneWay}" Comparison="LessThanOrEqual" To="3"/>
</VisualState.StateTriggers>
```
## FullScreenModeStateTrigger Example 
```xml
<VisualState.StateTriggers>
    <triggers:FullScreenModeStateTrigger IsFullScreen="true" />
</VisualState.StateTriggers>
```                    
## IsEqualStateTrigger Example
```xml
<VisualState.StateTriggers>
    <triggers:IsEqualStateTrigger Value="{Binding IsChecked, ElementName=checkbox, Mode=OneWay}" To="{x:Null}" />
</VisualState.StateTriggers>
```
## IsNotEqualStateTrigger Example
```xml
<VisualState.StateTriggers>
    <triggers:IsNotEqualStateTrigger Value="{Binding IsChecked, ElementName=checkbox, Mode=OneWay}" To="{x:Null}" />
</VisualState.StateTriggers>
```
## IsNullOrEmptyStateTrigger Example
```xml
<VisualState.StateTriggers>
    <triggers:IsNullOrEmptyStateTrigger Value="{Binding Text, ElementName=OurTextBox, Mode=OneWay}"/>
</VisualState.StateTriggers>
```              
## NetworkConnectionStateTrigger Example
```xml
<VisualState.StateTriggers>
    <triggers:NetworkConnectionStateTrigger ConnectionState="Connected" />
</VisualState.StateTriggers>
```
## RegexStateTrigger Example
```xml
<VisualState.StateTriggers>
    <triggers:RegexStateTrigger Value="{Binding Text, ElementName=emailTextBox, Mode=OneWay}"
                                                  Expression="^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,4}$"
                                                  Options="IgnoreCase" />
</VisualState.StateTriggers>
```
## UserHandPreferenceStateTrigger Example
```xml
<VisualState.StateTriggers>
    <triggers:UserHandPreferenceStateTrigger HandPreference="LeftHanded" />
</VisualState.StateTriggers>
```
## UserInteractionModeStateTrigger Example
```xml
<VisualState.StateTriggers>
    <triggers:UserInteractionModeStateTrigger InteractionMode="Mouse" />
</VisualState.StateTriggers>
```

## Sample Project

<!-- Link to the sample page in the Windows Community Toolkit Sample App -->
[Triggers sample page Source](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/master/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/Triggers). You can see this in action in the [Windows Community Toolkit Sample App](http://aka.ms/uwptoolkitapp).

## Requirements

| Device family | Universal, 10.0.16299.0 or higher   |
| -- | -- |
| Namespace | Microsoft.Toolkit.Uwp.UI.Triggers |
| NuGet package | [Microsoft.Toolkit.Uwp.UI](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI/) |


## API

* [Triggers source code](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/master/Microsoft.Toolkit.Uwp.UI/Triggers)