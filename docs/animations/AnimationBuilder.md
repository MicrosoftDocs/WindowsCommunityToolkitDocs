---
title: AnimationBuilder
author: Sergio0694
description: A class that allows to build custom animations targeting both the XAML and composition layers.
keywords: windows 10, uwp, windows community toolkit, uwp toolkit, animations, xaml, visual, composition
dev_langs:
  - csharp
---

# AnimationBuilder

The [`AnimationBuilder`](/dotnet/api/microsoft.toolkit.uwp.ui.animations.AnimationBuilder) class is a powerful and extensible type that can be used to construct complex animation schedules and to execute them on existing UI elements. Each `AnimationBuilder` instance is also fully reusable, so the same animations schedule can be stored and then used to start the same animations on different UI elements. One of the key features of this type is its ability to abstract over both the [XAML and the Composition layer](/windows/uwp/composition/visual-layer), allowing consumers to easily create schedules that include animations that can work on both layers.

> **Platform APIs:** [AnimationBuilder](/dotnet/api/microsoft.toolkit.uwp.ui.animations.AnimationBuilder), [`CompositorExtensions`](/dotnet/api/microsoft.toolkit.uwp.ui.animations.CompositorExtensions), [`DependencyObjectExtensions`](/dotnet/api/microsoft.toolkit.uwp.ui.animations.DependencyObjectExtensions), [`EasingTypeExtensions`](/dotnet/api/microsoft.toolkit.uwp.ui.animations.EasingTypeExtensions)

## Default animations

These are "ready to use" APIs that create specific animations for commonly used properties. They require little setup on the user side, with no need to deal with explicit property paths to animate. Examples of these are animations such as `Opacity`, `Offset` and `Translation`. Each of these default animation APIs also expose a number of overloads that can be used to easily customize how the animation is constructed. For instance by specifying a single translation axis to animate only using a single `double` value to indicate the initial and ending value for the animation:

```csharp
// Here we're creating a schedule with 3 different default animations.
// By default, all animations target the Composition layer, but users
// can opt in to target the XAML layer instead for supported animations.
AnimationBuilder.Create()
    .Opacity(from: 0, to: 1)
    .Translation(Axis.X, from: -20, to: 0)
    .RotationInDegrees(from: -30, to: 0)
    .Start(MyButton);
```

The `AnimationBuilder` type will take care of executing the right initialization depending on the target framework layer, including picking the right property path, converting the animation values, etc.

```csharp
// Each animation has a standard duration of 400ms and uses the default
// easing mode for both the Composition and XAML layers respectively.
// All these parameters can be fully customized as well, like so:
AnimationBuilder.Create().Opacity(
    from: 1,
    to: 0,
    delay: TimeSpan.FromSeconds(1),
    duration: TimeSpan.FromMilliseconds(600),
    easingType: EasingType.Sine,
    easingMode: EasingMode.EaseIn,
    layer: FrameworkLayer.Xaml).Start(MyButton);
```

## Default keyframe animations

These are keyframed animations that similar to the default ones, in that they are built-in and don't require users to manually specify property paths to animate or to select the correct animation type. The same standard animation targets are available here as well, and additionally it is possible to setup each keyframe animation using either normalized or timed keyframes, for either framework layer being animated. The `AnimationBuilder` class will automatically convert the custom keyframes to the right format depending on the animation being created.

```csharp
// Default keyframe animations using normalized keyframes
AnimationBuilder.Create()
    .Opacity().NormalizedKeyFrames(b => b
        .KeyFrame(0.0, 0)
        .KeyFrame(0.5, 1)
        .KeyFrame(0.75, 0.8)
        .KeyFrame(1.0, 1))
    .Translation(Axis.Y).TimedKeyFrames(b => b
        .KeyFrame(TimeSpan.Zero, -20)
        .KeyFrame(TimeSpan.FromMilliseconds(400), 20)
        .KeyFrame(TimeSpan.FromMilliseconds(600), 0))
    .Scale().NormalizedKeyFrames(b => b
        .KeyFrame(0.0, new(1))
        .KeyFrame(0.5, new(1.2f))
        .KeyFrame(1.0, new(1)))
    .Start(this);

// It is also possible to customize the easing type and mode
// for each individual keyframe, as well as using expression
// keyframes as well (only supported for Composition animations).
AnimationBuilder.Create()
    .Opacity().NormalizedKeyFrames(b => b
        .KeyFrame(0.0, 0)
        .KeyFrame(1.0, 1, easingType: EasingType.Back, easingMode: EasingMode.EaseOut))
    .Translation(Axis.Y).NormalizedKeyFrames(b => b
        .KeyFrame(0.0, -20)
        .ExpressionKeyFrame(0.5, "this.Target.Opacity * 100")
        .KeyFrame(1.0, 0))
    .Start(this);
```

## Custom keyframe animations

These are advanced keyframe animations that offer full control on the animation parameters. It is possible to manually set the property path, the target framework layer and the animation type. As with previous APIs, the `AnimationBuilder` type will take care of abstracting over the underlying APIs and converting the strongly typed APIs into the right implementation. These APIs are especially helpful in combination with the XAML target layer, as they allow combining custom [`Storyboard`](/uwp/api/windows.ui.xaml.media.animation.storyboard)-based animations with existing animation schedules.

```csharp
AnimationBuilder.Create()
    .NormalizedKeyFrames<Color>(
        property: "(TextBlock.Foreground).(SolidColorBrush.Color)",
        delay: TimeSpan.FromMilliseconds(200),
        duration: TimeSpan.FromMilliseconds(600),
        layer: FrameworkLayer.Xaml,
        build: b => b
        .KeyFrame(0.0, Colors.White)
        .KeyFrame(0.4, Colors.Orange)
        .KeyFrame(0.8, Colors.Blue)
        .KeyFrame(1.0, Colors.White))
    .TimedKeyFrames<Vector2>(
        property: "Scale.XY",
        layer: FrameworkLayer.Composition,
        build: b => b
        .KeyFrame(TimeSpan.Zero, new(1))
        .KeyFrame(TimeSpan.FromMilliseconds(200), new(1.2f))
        .KeyFrame(TimeSpan.FromMilliseconds(800), new(1)))
    .Start(MyTextBlock);
```

## External animations

These are animations targeting either the XAML or Composition layer that can be created outside of an `AnimationBuilder` instance and then inserted into an existing schedule. One key feature for these APIs is that they enable inserting animations targeting different UI elements into a given schedule. For instance, this is also used internally by the `Clip` default animation, which creates a Composition [`InsetClip`](/uwp/api/windows.ui.composition.insetclip) behind the scenes and then inserts an external animation targeting it into the current schedule.

It is also how the new effect animations from the `Microsoft.Toolkit.Uwp.UI.Media` package work, as they leverage these APIs to insert external animations targeting a [`CompositionBrush`](/uwp/api/windows.ui.composition.compositionbrush) object into the target schedule. External animation APIs are especially useful in combination with the new extension methods introduced in the package, as they make manually creating animations easier compared to manually doing so using the standard APIs for either the XAML or Composition layer.

```csharp
// First use an extension to create a custom brush animation
var blurAnimation = myBrush.Compositor.CreateScalarKeyFrameAnimation(
    target: "BlurEffect.BlurAmount",
    from: 32,
    to: 0,
    delay: TimeSpan.FromMilliseconds(500),
    duration: TimeSpan.FromSeconds(1),
    delayBehavior: AnimationDelayBehavior.SetInitialValueBeforeDelay);

// Then create and start an animation schedule with this external animation.
// We also indicate the external target for this Composition animation, as it's
// different than the UI element targeted by the whole schedule. There is also
// an overload accepting a Timeline instance, which doesn't require an external
// target since it can internally store the target DependencyObject already.
AnimationBuilder.Create()
    .Scale(1.1)
    .Opacity(0.0)
    .ExternalAnimation(myBrush, blurAnimation)
    .Start(MyButton);
```

### Extension methods

As mentioned above, the new versions of the `.Animations` and `.Media` packages also includes a number of extension methods that can be useful in a number of situations, such as:

- **Creating custom animations**: the [`CompositorExtensions`](/dotnet/api/microsoft.toolkit.uwp.ui.animations.CompositorExtensions) and [`DependencyObjectExtensions`](/dotnet/api/microsoft.toolkit.uwp.ui.animations.DependencyObjectExtensions) include extension methods to easily create custom [`CompositionAnimation`](/windows/uwp/composition/composition-animation) and [`Timeline`](/uwp/api/windows.ui.xaml.media.animation.timeline) instances in a single method call while still allowing to customize their behavior where necessary. They'll rely on the same suggested default values used elsewhere in the package (eg. the standard duration of 400ms for animations).
- **Creating easing functions**: the `CompositorExtensions` and [`EasingTypeExtensions`](/dotnet/api/microsoft.toolkit.uwp.ui.animations.EasingTypeExtensions) classes include extension methods that offer a uniform factory interface to create [`CompositionEasingFunction`](/uwp/api/windows.ui.composition.compositioneasingfunction) and [`EasingFunctionBase`](/uwp/api/windows.ui.xaml.media.animation.easingfunctionbase) instances respectively through the same abstraction of the EasingType and EasingMode values used in the rest of the toolkit. These helpers will automatically create the right easing types according to the input parameters.
- **And more**: there are other extension methods to help creating [`ScrollViewer`](/uwp/api/windows.ui.xaml.controls.scrollviewer) expression animations, start `Storyboard` elements and await for their completion, and to help interoperate with other types in the other modules of the package. Refer to the .NET API browser for a full list of the available APIs in each Toolkit package.

## Dispatch and cancellation

Lastly, the `AnimationBuilder` type also exposes a number of different overloads to start a schedule. They are available both in synchronous and asynchronous versions which can be awaited. A [`CancellationToken`](/dotnet/api/system.threading.cancellationtoken) can also be provided to stop animations after they are started. The fact that each executed timeline has its own `CancellationToken` is also how it is possible to re-use `AnimationBuilder` instances for different UI elements, while being able to stop each individual schedule.

```csharp
var schedule = AnimationBuilder.Create().Scale(1.1).Opacity(0.0);

// Starts an animation directly, with no awaiting/cancellation support.
// This is the simplest overload and the one with less overhead.
schedule.Start(MyButton);

// Starts the animation with a cancellation token. Cancelling
// it will stop all running animations (including external ones).
schedule.Start(MyButton, token);

// Asynchronous overloads are available as well which can be used to 
// suspend the current method's execution until the animation has
// completed or cancelled.
await schedule.StartAsync(MyButton);
await schedule.StartAsync(MyButton, token);
```

The standard way to create tokens is to use the [`CancellationTokenSource`](/dotnet/api/system.threading.cancellationtokensource) class, which exposes a linked token that will be cancelled when the source is cancelled as well. Here is a simple example demonstrating how to combine these different APIs to cancel an animation after some time:

```csharp
CancellationTokenSource tokenSource = new();

// Start the animation with the token, without awaiting it
animation.Start(MyButton, tokenSource.Token);

// Simulate some asynchronous work taking some time
await Task.Delay(1000);

// Send a request for cancellation. This will propagate the
// request to the token that has been passed to the animation,
// causing it to stop all animations still running in the schedule.
tokenSource.Cancel();
```

## Examples

You can find more examples in the [sample app](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.0.0/Microsoft.Toolkit.Uwp.SampleApp).
