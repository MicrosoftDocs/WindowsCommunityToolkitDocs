---
title: BackdropGammaTransferBrush
author: michael-hawker
description: The BackdropBlurBrush is a Brush that blurs whatever is behind it in the application.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, brush, backdrop, gamma, color
---

# BackdropGammaTransferBrush

The [BackdropGammaTransferBrush](/dotnet/api/microsoft.toolkit.uwp.ui.media.backdropgammatransferbrush) is a [Brush](/uwp/api/windows.ui.xaml.media.brush) which modifies the color values of whatever is behind it in the application.

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://Brushes?sample=BackdropGammaTransferBrush)

## Syntax

To apply a red hue:

```xml
<Border BorderBrush="Black" BorderThickness="1" VerticalAlignment="Center" HorizontalAlignment="Center" Width="400" Height="400">
  <Border.Background>
    <media:BackdropGammaTransferBrush RedAmplitude="1.25" />
  </Border.Background>
</Border>
```

## Example Image

![Backdrop Gamma](../resources/images/Brushes/BackdropGamma.jpg "Backdrop Gamma")

## Properties

See the property reference for the [GammaTransferEffect](http://microsoft.github.io/Win2D/html/T_Microsoft_Graphics_Canvas_Effects_GammaTransferEffect.htm).  

All Amplitude, Disable, Exponent, and Offset properties are available for the Alpha, Red, Green, and Blue channels.

## Sample Code

[BackdropGammaTransferBrush sample page Source](https://github.com/Microsoft/WindowsCommunityToolkit//tree/master/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/BackdropGammaTransferBrush). You can [see this in action](uwpct://Brushes?sample=BackdropGammaTransferBrush) in the [Windows Community Toolkit Sample App](http://aka.ms/uwptoolkitapp).

## Requirements

| Device family | Universal, 10.0.16299.0 or higher |
| --- | --- |
| Namespace | Microsoft.Toolkit.Uwp.UI.Media |
| NuGet package | [Microsoft.Toolkit.Uwp.UI.Media](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI.Media/)

## API

* [BackdropGammaTransferBrush source code](https://github.com/windows-toolkit/WindowsCommunityToolkit/blob/master/Microsoft.Toolkit.Uwp.UI.Media/Brushes/BackdropGammaTransferBrush.cs)

## Related Topics

* [Win2D GammaTransferEffect reference](http://microsoft.github.io/Win2D/html/T_Microsoft_Graphics_Canvas_Effects_GammaTransferEffect.htm)