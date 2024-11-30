---
title: Fade animation behavior
author: nmetulev
description: The Fade animation behavior fades objects, in and out, over time and delay. It can be used along side other animations directly through XAML or code (outdated docs).
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, fade, fade animation
dev_langs:
  - csharp
  - vb
---

# Fade

> [!WARNING]
> This behavior is no longer available in the Windows Community Toolkit. Please use the effects from the `Microsoft.Toolkit.Uwp.UI.Media` package and the helpers such as the [`PipelineVisualFactory`](/dotnet/api/microsoft.toolkit.uwp.ui.media.PipelineVisualFactory) type.

The [Fade animation](/dotnet/api/microsoft.toolkit.uwp.ui.animations.animationextensions.fade) fades objects, in and out, over time. Fade animation is applied to all the XAML elements in its parent control/panel. Fade animation doesn't affect the functionality of the control.

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://Animations?sample=Fade)

## Syntax

```xaml
<Page ...
    xmlns:interactivity="using:Microsoft.Xaml.Interactivity"  
    xmlns:behaviors="using:Microsoft.Toolkit.Uwp.UI.Animations.Behaviors"/>

<interactivity:Interaction.Behaviors>
    <behaviors:Fade x:Name="FadeBehavior" 
            Value="0.5" 
            Duration="2500" 
            Delay="250"
            EasingType="Linear"
            AutomaticallyStart="True"/>
</interactivity:Interaction.Behaviors>
```

```csharp
MyUIElement.Fade(value: 0.5f, duration: 2500, delay: 250, easingType: EasingType.Default).Start();
await MyUIElement.Fade(value: 0.5f, duration: 2500, delay: 250, easingType: EasingType.Default).StartAsync();  //Fade animation can be awaited
```

```vb
MyUIElement.Fade(value:=0.5F, duration:=2500, delay:=250, easingType:=EasingType.[Default]).Start()
Await MyUIElement.Fade(value:=0.5F, duration:=2500, delay:=250, easingType:=EasingType.[Default]).StartAsync()  ' Fade animation can be awaited
```

## Sample Output

![Fade Behavior animation](../resources/images/Animations/Fade/Sample-Output.gif)

## Properties

| Property | Type | Description |
| -- | -- | -- |
| Value | float | The fade value, between 0 and 1 |
| Duration | double | The duration in milliseconds |
| Delay | double | The delay for the animation to begin |
| EasingType | EasingType | Used to describe how the animation interpolates between keyframes |

### EasingType

You can change the way how the animation interpolates between keyframes by defining the EasingType.

| EasingType | Explanation                                                                                                | Graphical Explanation                      |
| ---------- | ---------------------------------------------------------------------------------------------------------- | ------------------------------------------ |
| Default    | Creates an animation that accelerates with the default EasingType which is specified in AnimationExtensions.DefaultEasingType which is by default Cubic |                                                                                                                           |
| Linear     | Creates an animation that accelerates or decelerates linear                                                                                             |                                                                                                                           |
| Back       | Retracts the motion of an animation slightly before it begins to animate in the path indicated                                                          | ![BackEase](/dotnet/framework/wpf/graphics-multimedia/media/backease-graph.png)           |
| Bounce     | Creates a bouncing effect                                                                                                                               | ![BounceEase](/dotnet/framework/wpf/graphics-multimedia/media/bounceease-graph.png)       |
| Circle     | Creates an animation that accelerates or decelerates using a circular function                                                                          | ![CircleEase](/dotnet/framework/wpf/graphics-multimedia/media/circleease-graph.png)       |
| Cubic      | Creates an animation that accelerates or decelerates using the formula f(t) = t3                                                                        | ![CubicEase](/dotnet/framework/wpf/graphics-multimedia/media/cubicease-graph.png)         |
| Elastic    | Creates an animation that resembles a spring oscillating back and forth until it comes to rest                                                          | ![ElasticEase](/dotnet/framework/wpf/graphics-multimedia/media/elasticease-graph.png)     |
| Quadratic  | Creates an animation that accelerates or decelerates using the formula f(t) = t2                                                                        | ![QuadraticEase](/dotnet/framework/wpf/graphics-multimedia/media/quadraticease-graph.png) |
| Quartic    | Creates an animation that accelerates or decelerates using the formula f(t) = t4                                                                        | ![QuarticEase](/dotnet/framework/wpf/graphics-multimedia/media/quarticease-graph.png)     |
| Quintic    | Create an animation that accelerates or decelerates using the formula f(t) = t5                                                                         | ![QuinticEase](/dotnet/framework/wpf/graphics-multimedia/media/quinticease-graph.png)     |
| Sine       | Creates an animation that accelerates or decelerates using a sine formula                                                                               | ![SineEase](/dotnet/framework/wpf/graphics-multimedia/media/sineease-graph.png)           |

## Methods

| Methods | Return Type | Description |
| -- | -- | -- |
| Fade(AnimationSet, Single, Double, Double, EasingType) | AnimationSet | Animates the opacity of the UIElement |
| Fade(UIElement, Single, Double, Double, EasingType) | AnimationSet | Animates the opacity of the UIElement |

## Examples

- Use this to create chaining animations with other animations. Visit the [AnimationSet](AnimationSet.md) documentation for more information.

    **Sample Code**

    ```csharp
    var anim = MyUIElement.Fade(0.5f).Blur(5).Rotate(30);
    anim.SetDurationForAll(2500);
    anim.SetDelay(250);
    anim.Completed += animation_completed;
    anim.Start();
    ```

    ```vb
    Dim anim = MyUIElement.Fade(0.5F).Blur(5).Rotate(30)
    anim.SetDurationForAll(2500)
    anim.SetDelay(250)
    AddHandler anim.Completed, AddressOf animation_completed
    anim.Start()
    ```

    **Sample Output**

    ![Use Case 1 Output](../resources/images/Animations/Chaining-Animations-Blur-Fade-Rotate.gif)

## Sample Project

[Fade Behavior Sample Page Source](https://github.com/CommunityToolkit/WindowsCommunityToolkit/tree/rel/7.1.2/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/Animations/Effects). You can [see this in action](uwpct://Animations?sample=Fade) in the [Windows Community Toolkit Sample App](https://aka.ms/windowstoolkitapp).

## Requirements

| Device family | Universal, 10.0.16299.0 or higher   |
| ---------------------------------------------------------------- | ----------------------------------- |
| Namespace                                                        | Microsoft.Toolkit.Uwp.UI.Animations |
| NuGet package | [Microsoft.Toolkit.Uwp.UI.Animations](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI.Animations/) |

## API

- [Fade source code](https://github.com/CommunityToolkit/WindowsCommunityToolkit/blob/rel/7.1.2/Microsoft.Toolkit.Uwp.UI.Animations/Xaml/Default/OpacityAnimation.cs)

## Related Topics

- [AnimationSet Class](./animationset.md)
- [Storyboard Class](/uwp/api/Windows.UI.Xaml.Media.Animation.Storyboard)
