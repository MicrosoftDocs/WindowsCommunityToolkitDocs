---
title: Handling Failure and Down-level
author: sohchatt
description: Lottie-Windows renders AfterEffects animations natively in Windows applications.
keywords: lottie, lottie-windows, animatedvisualplayer, bodymovin, aftereffects, windows 10, uwp, uwp community toolkit
---

# Handling Failure and Down-level

The AnimatedVisualPlayer has a [FallbackContent](https://docs.microsoft.com/uwp/api/microsoft.ui.xaml.controls.animatedvisualplayer.fallbackcontent) property that allows you to provide custom XAML to be displayed in cases where Lottie-Windows is unable to render the animation, such as:

* a Lottie source that fails to load due to a malformed JSON file, incorrect URI, etc.
* your application running on a Windows 10 OS version **prior to 1809** (10.0.17763).

The FallbackContent is of type [DataTemplate](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.DataTemplate) — this ensures that your custom XAML tree is only instantiated when the AnimatedVisualPlayer needs to fallback.
In the example below, we use an Image as fallback for the Lottie animation:

```xaml
    <!-- AnimatedVisualPlayer -->
    <controls:AnimatedVisualPlayer x:Name="player">
        <!-- LottieVisualSource with invalid UriSource to cause fallback -->
        <lottie:LottieVisualSource x:Name="JsonSource "
                                    UriSource="http://notarealuri.microsoft.com/notarealfile.json" />
        <!-- Fallback Content: Custom XAML content that is rendered if Source fails to load, or if app runs on Windows 10 verion < 1809. -->
        <controls:AnimatedVisualPlayer.FallbackContent>
            <DataTemplate>
                <!-- Static Image for Fallback.
                     Because this is in a DataTemplate, the Image is only instantiated when in the fallback case. -->
                <Image Source="/Assets/LottieLogo1.png" />
            </DataTemplate>
        </controls:AnimatedVisualPlayer.FallbackContent>
    </controls:AnimatedVisualPlayer>

```

## Resources

* [Source code](https://github.com/windows-toolkit/Lottie-Windows/blob/master/samples/LottieSamples/Scenarios/FallbackPage.xaml) for sample: handling failure and down-level
* The resulting page in the [Lottie Samples application](https://aka.ms/lottiesamples)
* [FallbackContent](https://docs.microsoft.com/uwp/api/microsoft.ui.xaml.controls.animatedvisualplayer.fallbackcontent) property
* [Help + feedback](https://github.com/windows-toolkit/Lottie-Windows/issues)
