---
title: Configuring Animation Playback
author: sohchatt
description: Sample of configuring animation playback in Lottie-Windows.
keywords: lottie, lottie-windows, animatedvisualplayer, bodymovin, aftereffects, windows 10, uwp, uwp community toolkit
---

# Configuring Animation Playback

The [AnimatedVisualPlayer](/uwp/api/microsoft.ui.xaml.controls.animatedvisualplayer) XAML element is responsible for controlling the playback of its Lottie animation source through the following properties and methods:

* [AutoPlay](/uwp/api/microsoft.ui.xaml.controls.animatedvisualplayer.autoplay) plays a Lottie animation as soon as it is loaded.
* [IsPlaying](/uwp/api/microsoft.ui.xaml.controls.animatedvisualplayer.isplaying) indicates whether a play is currently underway.
* [PlaybackRate](/uwp/api/microsoft.ui.xaml.controls.animatedvisualplayer.playbackrate) is a live property that modifies the rate of the animation; negative values change the direction of playback.
* [PlayAsync(Double, Double, Boolean)](/uwp/api/microsoft.ui.xaml.controls.animatedvisualplayer.playasync) plays a Lottie animation asynchronously between two specified progress values, looping or once.
* [Pause()](/uwp/api/microsoft.ui.xaml.controls.animatedvisualplayer.pause) pauses the animation.
* [Resume()](/uwp/api/microsoft.ui.xaml.controls.animatedvisualplayer.resume) resumes a paused animation.
* [Stop()](/uwp/api/microsoft.ui.xaml.controls.animatedvisualplayer.stop) stops and completes the current play.
* [SetProgress(Double)](/uwp/api/microsoft.ui.xaml.controls.animatedvisualplayer.setprogress) moves the animation to the specified progress value.

Let’s set up a Lottie animation that plays in response to an event, for instance on ButtonClicked. Load the AnimatedVisualPlayer and configure its Source as before, but disable AutoPlay:

```xaml
    <Border Style="{StaticResource LottiePlayer}">
        <!--AnimatedVisualPlayer with AutoPlay disabled-->
        <controls:AnimatedVisualPlayer x:Name="player" AutoPlay="False">
            <!--Codegen class AnimatedVisuals/LottieLogo1.cs-->
            <animatedvisuals:LottieLogo1/>
        </controls:AnimatedVisualPlayer>
    </Border>
```

Next, let’s configure the PlayAsync method with the from and to progress values and no looping enabled. We won’t `await` the PlayAsync because we don’t want to wait until the animation has finished playing. Since we’re intentionally ignoring the IAsyncAction returned from PlayAsync in this case, we assign the result to a [C# 7 discard](/dotnet/csharp/discards#a-standalone-discard) to avoid a CS1998 compiler warning.

```csharp
    private void PlayButton_Click(object sender, RoutedEventArgs e)
    {
        _ = player.PlayAsync(fromProgress: 0, toProgress: 1, looped: false);
    }

```

Now, let's introduce Pause, Stop, and Reverse Buttons and update the method above to account for these other states. Our desired end result is as follows:

![Playback Gif](../../resources/images/Animations/Lottie/LottieDocs_Playback.gif)

```csharp
    private void PlayButton_Click(object sender, RoutedEventArgs e)
    {
        // Set forward playback rate.
        // NOTE: This property is live -- it takes effect even if the animation is playing.
        player.PlaybackRate = 1;
        EnsurePlaying();
    }

    private void PauseButton_Checked(object sender, RoutedEventArgs e)
    {
        // Pause the animation, if playing.
        player.Pause();
    }

    private void PauseButton_Unchecked(object sender, RoutedEventArgs e)
    {
        // Resume playing current animation.
        player.Resume();
    }

    private void StopButton_Click(object sender, RoutedEventArgs e)
    {
        // Stop the animation, which completes PlayAsync and resets to initial frame.
        player.Stop();
        PauseButton.IsChecked = false;
    }

    private void ReverseButton_Click(object sender, RoutedEventArgs e)
    {
        // Set negative playback rate in order to change the animation's direction.
        player.PlaybackRate = -1;
        EnsurePlaying();
    }

    private void EnsurePlaying()
    {
        if (PauseButton.IsChecked.Value)
        {
            // Resume playing the animation, if paused.
            PauseButton.IsChecked = false;
        }
        else
        {
            if (!player.IsPlaying)
            {
                // Play the animation at the currently specified playback rate.
                _ = player.PlayAsync(fromProgress: 0, toProgress: 1, looped: false);
            }
        }
    }

```

## Resources

* [Source code](https://github.com/windows-toolkit/Lottie-Windows/blob/rel/7.0.0/samples/LottieSamples/Scenarios/PlaybackPage.xaml.cs) for sample: configuring animation playback
* The resulting page in the [Lottie Samples application](https://aka.ms/lottiesamples)
* [AnimatedVisualPlayer](/uwp/api/microsoft.ui.xaml.controls.animatedvisualplayer) API reference
* [Help + feedback](https://github.com/windows-toolkit/Lottie-Windows/issues)
