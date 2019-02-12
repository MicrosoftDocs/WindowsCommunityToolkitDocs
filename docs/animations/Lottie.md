---
title: Lottie
author: sohchatt
description: Lottie-Windows renders AfterEffects animations natively in Windows applications.
keywords: lottie, lottie-windows, animatedvisualplayer, bodymovin, aftereffects, windows 10, uwp, uwp community toolkit
---

# Lottie

Lottie-Windows, is a library that renders [Adobe AfterEffects](https://www.adobe.com/products/aftereffects.html) animations natively in your application. This project adds Windows to the [Lottie](http://airbnb.io/lottie/) family of cross-platform tools also targeting [Android](https://github.com/airbnb/lottie-android), [iOS](https://github.com/airbnb/lottie-ios), and [Web](https://github.com/airbnb/lottie-web).

Lottie simplifies the design-to-code workflow for bringing engaging, interactive vector animations to your Windows applications, with significant improvements in terms of performance, quality, and engineering efficiency over traditional approaches such as gifs, manually coded animations, etc. Lottie-Windows uses the [`Windows.UI.Composition` APIs](https://docs.microsoft.com/windows/uwp/composition/visual-layer) to provide smooth 60fps animations and resolution-independent vector graphics.

![Lottie Gif](../resources/images/Animations/Lottie/LottieDocs_Intro.gif)

## Key Concepts

* **AnimatedVisualPlayer**, a XAML element that plays the Lottie animation.
* **Lottie-Windows**, a library for parsing [Bodymovin](https://aescripts.com/bodymovin/) JSON files; provides the **LottieVisualSource** that is consumed by the AnimatedVisualPlayer.
* **Lottie Viewer**, a Store app for previewing Lottie animations to test their visual correctness and to codegen C# or C++ classes.
* **LottieGen**, a command line tool for generating C# or C++ classes in lieu of using real-time JSON parsing.
* **Lottie Samples**, a Store app that provides simple code examples for common Lottie animation scenarios.

## Tutorials

The following documents help you get started with Lottie-Windows and provide simple code examples for common scenarios of usage:

* [Getting Started with Lottie-Windows](lottie-scenarios/getting_started_json.md)
* [Using Codegen](lottie-scenarios/getting_started_codegen.md)
* [JSON versus Codegen](lottie-scenarios/json_codegen.md)
* [Configuring Animation Playback](lottie-scenarios/playback.md)
* [Interactive Segments on an Animation Timeline](lottie-scenarios/segments.md)
* [The Asynchronous Play Method](lottie-scenarios/async_play.md)
* [Handling Failure and Down-level](lottie-scenarios/fallback.md)

## Sample Code

* [Code Samples for Lottie-Windows](https://github.com/windows-toolkit/Lottie-Windows/tree/master/samples)
* [Lottie Samples application](http://aka.ms/lottiesamples)

## Requirements

| Device family | Universal, 10.0.17763.0 or higher |
| -- | -- |
| Namespace | Microsoft.Toolkit.Uwp.UI.Lottie |
| NuGet package | [Microsoft.Toolkit.Uwp.UI.Lottie](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI.Lottie/) |

## API

* [AnimatedVisualPlayer](https://docs.microsoft.com/uwp/api/microsoft.ui.xaml.controls.animatedvisualplayer)
* [LottieVisualSource](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.uwp.ui.lottie.lottievisualsource)

## Resources

* [Lottie-Windows library](https://github.com/windows-toolkit/Lottie-Windows) on github
* [Lottie Viewer application](https://www.microsoft.com/p/lottie-viewer/9p7x9k692tmw) in the Store
* [Lottie by Airbnb](http://airbnb.io/lottie/)
* [Bodymovin exporter](https://aescripts.com/bodymovin/) for Adobe AfterEffects
* [Help + feedback](https://github.com/windows-toolkit/Lottie-Windows/issues)