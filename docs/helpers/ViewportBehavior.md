---
title: ViewportBehavior class
author: h82258652
description: This behavior allows you to listen an element enter or exit the ScrollViewer viewport
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, your control name
dev_langs:
  - csharp
---

# ViewportBehavior

This behavior allows you to listen an element enter or exit the ScrollViewer viewport.

## Syntax

```xaml
<Page 
    xmlns:interactivity="using:Microsoft.Xaml.Interactivity"
    xmlns:behaviors="using:Microsoft.Toolkit.Uwp.UI.Animations.Behaviors" />

<ScrollViewer>
    <StackPanel Orientation="Vertical"
                Height="3000">
        <Border Width="100"
                Height="100">
            <interactivity:Interaction.Behaviors>
                <behaviors:ViewportBehavior x:Name="ViewportBehavior"
                                            EnteringViewport="Border_EnteringViewport"
                                            EnteredViewport="Border_EnteredViewport"
                                            ExitingViewport="Border_ExitingViewport"
                                            ExitedViewport="Border_ExitedViewport" />
            </interactivity:Interaction.Behaviors>
        </Border>
    </StackPanel>
</ScrollViewer>
```

## Properties

| Property | Type | Description |
| -- | -- | -- |
| IsInViewport | bool | Gets a value indicating whether associated element is in the ScrollViewer viewport |
| IsFullyInViewport | bool | Gets a value indicating whether associated element is fully in the ScrollViewer viewport |
| IsRemoveBehaviorAfterEnteredViewport | bool | Gets or sets a value indicating whether remove this behavior after associated element entered viewport |

## Events

| Event | Description |
| -- | -- |
| EnteringViewport | Associated element enter the ScrollViewer viewport event |
| EnteredViewport | Associated element fully enter the ScrollViewer viewport event |
| ExitingViewport | Associated element exit the ScrollViewer viewport event |
| ExitedViewport | Associated element fully exit the ScrollViewer viewport event |

## Sample Code

[ViewportBehavior Sample Page Source](https://github.com/Microsoft/WindowsCommunityToolkit//tree/master/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/ViewportBehavior). You can see this in action in [Windows Community Toolkit Sample App](https://www.microsoft.com/store/apps/9NBLGGH4TLCQ).

## Requirements

| Device family | Universal, 10.0.16299.0 or higher   |
| ---------------------------------------------------------------- | ----------------------------------- |
| Namespace                                                        | Microsoft.Toolkit.Uwp.UI.Animations |
| NuGet package | [Microsoft.Toolkit.Uwp.UI.Animations](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI.Animations/) |

## API

* [ViewportBehavior source code](https://github.com/Microsoft/WindowsCommunityToolkit/tree/master/Microsoft.Toolkit.Uwp.UI.Animations/Behaviors/ViewportBehavior.cs)

