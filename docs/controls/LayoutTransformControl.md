---
title: LayoutTransformControl
author: odonno
description: The LayoutTransformControl is a control that support transformations on FrameworkElement as if applied by LayoutTransform.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, LayoutTransformControl, RenderTransform, RotateTransform, ScaleTransform, SkewTransform 
---

# LayoutTransformControl

The [LayoutTransformControl](/dotnet/api/microsoft.toolkit.uwp.ui.controls.layouttransformcontrol) is a control that applies Matrix transformations on any `FrameworkElement` of your application.

The transformations that can be applied are one of the following:

* [RotateTransform](/uwp/api/windows.ui.xaml.media.rotatetransform)
* [ScaleTransform](/uwp/api/windows.ui.xaml.media.scaletransform)
* [SkewTransform](/uwp/api/windows.ui.xaml.media.skewtransform)
* [MatrixTransform](/uwp/api/windows.ui.xaml.media.matrixtransform)
* [TransformGroup](/uwp/api/windows.ui.xaml.media.transformgroup)

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://Controls?sample=LayoutTransformControl)

## Syntax

```xaml
<controls:LayoutTransformControl Background="Black" 
                                 HorizontalAlignment="Center" 
                                 VerticalAlignment="Center"
                                 RenderTransformOrigin="0.5,0.5">
    <controls:LayoutTransformControl.Transform>
        <RotateTransform Angle="90" />
    </controls:LayoutTransformControl.Transform>

    <Border HorizontalAlignment="Center" 
            VerticalAlignment="Center"
            BorderBrush="Red"
            BorderThickness="5">
        <Grid>
            <TextBlock Padding="10" Foreground="White" Text="This is a test message." />
        </Grid>
    </Border>
</controls:LayoutTransformControl>
```

## Properties

| Property | Type | Description |
| -- | -- | -- |
| Child | FrameworkElement | The content of the control that will receive matrix transformations |
| Transform | Transform | The transformations to apply on the `Content`. It can be a single transformation like `RotateTransform`, `ScaleTransform` or `SkewTransform` or it can be a combo of multiple transformations using `TransformGroup` |

## Sample Project

[LayoutTransformControl Sample Page](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.0.0/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/LayoutTransformControl). You can [see this in action](uwpct://Controls?sample=LayoutTransformControl) in the [Windows Community Toolkit Sample App](https://aka.ms/windowstoolkitapp).

## Requirements

| [Device family](/windows/uwp/get-started/universal-application-platform-guide#device-families) | Universal, 10.0.16299.0 or higher   |
| -- | -- |
| Namespace | Microsoft.Toolkit.Uwp.UI.Controls |
| NuGet package | [Microsoft.Toolkit.Uwp.UI.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI.Controls/) |

## API

*-* [LayoutTransformControl](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.0.0/Microsoft.Toolkit.Uwp.UI.Controls.Layout/LayoutTransformControl)

## Related Topics

* [Expander](Expander.md)
* [MatrixTransform](/uwp/api/windows.ui.xaml.media.matrixtransform)
* [TransformGroup](/uwp/api/windows.ui.xaml.media.transformgroup)
* [RotateTransform](/uwp/api/windows.ui.xaml.media.rotatetransform)
* [ScaleTransform](/uwp/api/windows.ui.xaml.media.scaletransform)
* [SkewTransform](/uwp/api/windows.ui.xaml.media.skewtransform)
