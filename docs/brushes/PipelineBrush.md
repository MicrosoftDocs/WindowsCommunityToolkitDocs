---
title: PipelineBrush
author: Sergio0694
description: A composition brush which can render any custom Win2D/Composition effects chain.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, brush, backdrop, blur, win2d, composition
---

# PipelineBrush

The [PipelineBrush](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.uwp.ui.media.pipelinebrush) is a [Brush](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.brush) which can render any custom Win2D/Composition effects chain.

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://Brushes?sample=PipelineBrush)

## Syntax

```xml
<Border BorderBrush="Black" BorderThickness="1" VerticalAlignment="Center" HorizontalAlignment="Center" Width="400" Height="400">
  <Border.Background>
    <brushes:PipelineBrush>
        <brushes:PipelineBrush.Effects>
            <effects:BackdropEffect Source="Backdrop"/>
            <effects:LuminanceToAlphaEffect/>
            <effects:OpacityEffect Value="0.4"/>
            <effects:BlendEffect Mode="Multiply">
            <effects:BlendEffect.Input>
                <effects:BackdropEffect Source="Backdrop"/>
            </effects:BlendEffect.Input>
            </effects:BlendEffect>
            <effects:BlurEffect Value="16"/>
            <effects:ShadeEffect Color="#FF222222" Intensity="0.2"/>
            <effects:BlendEffect Mode="Overlay" Placement="Background">
            <effects:BlendEffect.Input>
                <effects:TileEffect Uri="ms-appx:///Assets/BrushAssets/NoiseTexture.png"/>
            </effects:BlendEffect.Input>
            </effects:BlendEffect>
        </brushes:PipelineBrush.Effects>
    </brushes:PipelineBrush>
  </Border.Background>
</Border>
```

## Example Image

![Pipeline brush](../resources/images/Brushes/PipelineBrush.jpg "Pipeline brush")

## Properties

| Property | Type | Description |
| -- | -- | -- |
| Effects | IList<IPipelineEffect> | The collection of effects to use in the current pipeline. |

## Code behind support

The pipelines of effects that can be built from XAML through the `PipelineBrush` type can also be created directly from code behind through the `PipelineBuilder` class.

```csharp
Brush brush =
  PipelineBuilder
    .FromBackdrop()
    .LuminanceToAlpha()
    .Opacity(0.4f)
    .Blend(
      PipelineBuilder.FromBackdrop(),
      BlendEffectMode.Multiply)
    .Blur(16)
    .Shade("#FF222222".ToColor(), 0.4f)
    .Blend(
      PipelineBuilder.FromTiles("/Assets/BrushAssets/NoiseTexture.png"),
      BlendEffectMode.Overlay,
      Placement.Background)
    .AsBrush();
```

## Sample Project

[PipelineBrush sample page Source](https://github.com/Microsoft/WindowsCommunityToolkit//tree/master/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/PipelineBrush). You can [see this in action](uwpct://Brushes?sample=PipelineBrush) in the [Windows Community Toolkit Sample App](http://aka.ms/uwptoolkitapp).

## Requirements

| Device family | Universal, 10.0.17134.0 or higher |
| --- | --- |
| Namespace | Microsoft.Toolkit.Uwp.UI.Media |
| NuGet package | [Microsoft.Toolkit.Uwp.UI.Media](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI.Media/) |

## API

* [PipelineBrush source code](https://github.com/windows-toolkit/WindowsCommunityToolkit/blob/master/Microsoft.Toolkit.Uwp.UI.Media/Brushes/PipelineBrush.cs)
* [PipelineBuilder source code](https://github.com/windows-toolkit/WindowsCommunityToolkit/blob/master/Microsoft.Toolkit.Uwp.UI.Media/Pipelines/PipelineBuilder.cs)

## Related Topics

* [Win2D GaussianBlurEffect reference](http://microsoft.github.io/Win2D/html/T_Microsoft_Graphics_Canvas_Effects_GaussianBlurEffect.htm)
* [XamlCompositionBrushBase Examples](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.xamlcompositionbrushbase#examples)
