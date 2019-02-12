---
title: Getting Started with Lottie-Windows
author: sohchatt
description: Lottie-Windows renders AfterEffects animations natively in Windows applications.
keywords: lottie, lottie-windows, animatedvisualplayer, bodymovin, aftereffects, windows 10, uwp, uwp community toolkit
---

# Getting Started with Lottie-Windows

You probably have a JSON file, `LottieLogo1.json` in this example, that was exported from [Adobe AfterEffects](https://www.adobe.com/products/aftereffects.html) using the [BodyMovin](https://aescripts.com/bodymovin/) plugin. If not, you can find many from the [fantastic community](https://lottiefiles.com/) of Lottie designers and creators. Let’s bring these animations to your Windows applications with the following steps:

1. _(Optional but Recommended)_ Install the [LottieViewer app](https://www.microsoft.com/p/lottie-viewer/9p7x9k692tmw) from the Store and validate that the JSON file works as expected. If there are any known issues due to unsupported AfterEffects features, the warning icon may light up and provide more context.  

2. Install the [`Microsoft.UI.Xaml` nuget package](https://www.nuget.org/packages/Microsoft.UI.Xaml/) which contains the [`AnimatedVisualPlayer`](https://docs.microsoft.com/en-us/uwp/api/microsoft.ui.xaml.controls.animatedvisualplayer) element. In your VisualStudio project:
    * Go to the Nuget Package Manager by navigating to Project > Manage Nuget Packages.
    * Check the _Include prerelease_ box and search for “Microsoft.UI.Xaml” in nuget.org.
    * Install the latest prerelease version of the nuget package available.

    Modify your `Page.xaml` to include the `Microsoft.UI.Xaml.Controls` namespace:

    ```xaml
    xmlns:controls="using:Microsoft.UI.Xaml.Controls"
    ```

3. Install the latest [`Microsoft.Toolkit.Uwp.UI.Lottie` nuget package](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI.Lottie/) by following steps similar to those listed above. Modify your `Page.xaml` to include the namespace:

    ```xaml
    xmlns:lottie="using:Microsoft.Toolkit.Uwp.UI.Lottie"
    ```

4. Add the JSON file to your project: create a new  `/AnimatedVisuals` folder and include `LottieLogo1.json` in the Project Solution by right clicking > Add > Existing Item. Set its [Build Action](https://docs.microsoft.com/visualstudio/ide/build-actions) to **Content** in the Properties window.

    <img src="../../resources/images/Animations/Lottie/LottieDocs_BuildAction.png" alt="BuildAction" width="150"/>

5. Instantiate the `AnimatedVisualPlayer` element and configure its `Source` as follows:

    ```xaml
        <Border Style="{StaticResource LottiePlayer}">
            <!--AnimatedVisualPlayer with AutoPlay-->
            <controls:AnimatedVisualPlayer x:Name="LottiePlayer">
                <!--LottieVisualSource with JSON UriSource-->
                <lottie:LottieVisualSource x:Name="LottieJsonSource" UriSource="ms-appx:///AnimatedVisuals/LottieLogo1.json"/>
            </controls:AnimatedVisualPlayer>
        </Border>
    ```

Since the `AutoPlay` property is set to `True` by default, the result will be a looping animation:

![Autoplay Gif](../../resources/images/Animations/Lottie/LottieDocs_Autoplay.gif)

## Resources

* [Source code](https://github.com/windows-toolkit/Lottie-Windows/blob/master/samples/LottieSamples/Scenarios/JsonPage.xaml) for sample: getting started with a JSON file
* The resulting page in the [Lottie Samples application](http://aka.ms/lottiesamples)
* [LottieVisualSource](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.uwp.ui.lottie.lottievisualsource) API reference
* [Lottie Viewer application](https://www.microsoft.com/p/lottie-viewer/9p7x9k692tmw) for previewing JSON files
* [Help + feedback](https://github.com/windows-toolkit/Lottie-Windows/issues)