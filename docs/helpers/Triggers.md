---
title: State Triggers
author: dotMorten
description: A collection of custom visual State Triggers
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, CompareStateTrigger, FullScreenModeStateTrigger, IsEqualStateTrigger, IsNotEqualStateTrigger, IsNullOrEmptyStateTriggers, NetworkConnectionStateTrigger, RegexStateTrigger, UserHandPreferenceStateTrigger, UserInteractionModeStateTrigger
dev_langs:
  - csharp
---

<!-- To know about all the available Markdown syntax, Check out https://docs.microsoft.com/contribute/contribute/how-to-write-use-markdown -->
<!-- Ensure you remove all comments before submission, to ensure that there are no formatting issues when displaying this page.  -->
<!-- It is recommended to check how the Documentation will look in the sample app, before Merging a PR -->

# State Triggers

<!-- Describe your control -->
A collection of custom visual [State Triggers](https://docs.microsoft.com/dotnet/api/Microsoft.Toolkit.Uwp.UI.Triggers)
<!-- You can get your API link from https://docs.microsoft.com/dotnet/api/?term=Microsoft.Toolkit. Make sure you remove the "?view=uwp-toolkit-x.x.x" from the end and country/region specific keyword like "en-us" of the URL eg: https://docs.microsoft.com/dotnet/api/microsoft.toolkit.uwp.helpers.printhelper -->

<!-- Use below format to display note
> [!NOTE]
> Some note

> [!IMPORTANT]
> Some important note

> [!WARNING]
> Some warning note
-->

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://categoryName?sample=pageName)

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

## Properties

<!-- Explain all properties in a table format -->

| Property | Type | Description |
| -- | -- | -- |
| A | bool | Description |
| B | int | Description |

<!-- Use <remarks> tag in C# to give more info about a propertie. For more info - https://docs.microsoft.com/dotnet/csharp/programming-guide/xmldoc/remarks -->

## Methods

<!-- Explain all methods in a table format -->

| Methods | Return Type | Description |
| -- | -- | -- |
| A(int) | bool | Description |
| B(float, string) | int | Description |

<!-- Use <remarks> tag in C# to give more info about a method. For more info - https://docs.microsoft.com/dotnet/csharp/programming-guide/xmldoc/remarks -->

## Events

<!-- Explain all events in a table format -->

| Events | Description |
| -- | -- |
| A | Description |
| B | Description |

<!-- Use <remarks> tag in C# to give more info about a event. For more info - https://docs.microsoft.com/dotnet/csharp/programming-guide/xmldoc/remarks -->

## Examples

<!-- All control/helper must at least have an example to show the use of Properties and Methods in your control/helper with the output -->
<!-- Use <example> and <code> tags in C# to create a Propertie/method specific examples. For more info - https://docs.microsoft.com/dotnet/csharp/programming-guide/xmldoc/example -->
<!-- Optional: Codes to achieve real-world use case with the output. For eg: Check https://docs.microsoft.com/windows/communitytoolkit/animations/animationset#examples  -->

## Sample Project

<!-- Link to the sample page in the Windows Community Toolkit Sample App -->
[CompareStateTrigger sample page Source](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/master/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/Triggers). You can [see this in action](uwpct://CategoryName?sample=pageName) in [Windows Community Toolkit Sample App](http://aka.ms/uwptoolkitapp).

## Requirements

| Device family | Universal, MinVersion or higher   |
| -- | -- |
| Namespace | Microsoft.Toolkit.Uwp |
| NuGet package | [Microsoft.Toolkit.Uwp](https://github.com/MicrosoftDocs/WindowsCommunityToolkitDocs/blob/master/docs/helpers/ImageCache.md) |

<!-- If your control supports .NET Standard then uncomment the below line -->
<!-- The Control Name supports .NET Standard -->

<!-- Copy paste for the NuGet package links
[Microsoft.Toolkit](https://www.nuget.org/packages/Microsoft.Toolkit/)
[Microsoft.Toolkit.Services](https://www.nuget.org/packages/Microsoft.Toolkit.Services/)
[Microsoft.Toolkit.Parsers](https://www.nuget.org/packages/Microsoft.Toolkit.Parsers/)
[Microsoft.Toolkit.Uwp](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp/)
[Microsoft.Toolkit.Uwp.Notifications](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Notifications/)
[Microsoft.Toolkit.Uwp.Notifications.JavaScript](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Notifications.JavaScript/)
[Microsoft.Toolkit.Uwp.Services](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Services/)
[Microsoft.Toolkit.Uwp.UI](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI/)
[Microsoft.Toolkit.Uwp.UI.Animations](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI.Animations/)
[Microsoft.Toolkit.Uwp.UI.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI.Controls/)
[Microsoft.Toolkit.Uwp.Connectivity](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Connectivity/)
[Microsoft.Toolkit.Uwp.DeveloperTools](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.DeveloperTools/)
 -->

## API

* [CompareStateTrigger source code](https://github.com/windows-toolkit/WindowsCommunityToolkit/blob/master/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/Triggers/CompareStateTriggerPage.xaml.cs)
