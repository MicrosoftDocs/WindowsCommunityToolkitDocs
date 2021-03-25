---
title: MediaPlayerElement control for Windows Forms and WPF
author: granitestatehacker
description: This control is a wrapper to enable use of the UWP MediaPlayerElement control in Windows Forms or WPF.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, MediaPlayerElement, Windows Forms, WPF
---

# MediaPlayerElement control for Windows Forms and WPF

The **MediaPlayerElement** control embeds a view that streams and renders media content such as video in your Windows Forms or WPF desktop application. This is one of several wrapped Universal Windows Platform controls that are available for Windows Forms and WPF applications as part of a feature called *XAML Islands*. For more information, see [UWP controls in desktop applications (XAML Islands)](/windows/uwp/xaml-platform/xaml-host-controls).

![MediaPlayterElement example](../../resources/images/Controls/MediaPlayerElement.png)

> [!NOTE]
> If you have feedback about this control, create a new issue in the [Microsoft.Toolkit.Win32 repo](/windows-toolkit/Microsoft.Toolkit.Win32/issues) and leave your comments there. If you prefer to submit your feedback privately, you can send it to XamlIslandsFeedback@microsoft.com.

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://WPFandWinFormsControls?sample=MediaPlayerElement)

## About MediaPlayerElement control

This control wraps an instance of the UWP [Windows.UI.Xaml.Controls.MediaPlayerElement](/uwp/api/Windows.UI.Xaml.Controls.MediaPlayerElement) control. The WPF version of this control is located in the **Microsoft.Toolkit.Wpf.UI.Controls** namespace. The Windows Forms version is located in the **Microsoft.Toolkit.Forms.UI.Controls** namespace. You can find additional related types (such as enums and event args classes) in the **Microsoft.Toolkit.Win32.UI.Controls.Interop.WinRT** namespace.

## Prerequisites

Before you can use this control, you must follow [these instructions](/windows/apps/desktop/modernize/xaml-islands#requirements) to configure your project to support XAML Islands.

## Known issues and limitations

* This controls does not currently support full screen video.
* The **Source** property is exposed as a string, which is interpreted as a URL and bound to the **Source** property of the wrapped UWP control as a UWP-implemented **IMediaPlaybackSource**.
* See also our list of [known issues](https://github.com/windows-toolkit/Microsoft.Toolkit.Win32/issues) for WPF and Windows Forms controls in the Windows Community Toolkit repo.

## Syntax

```xaml
<Window x:Class="TestSample.MainWindow" ...
  xmlns:controls="clr-namespace:Microsoft.Toolkit.Wpf.UI.Controls;assembly=Microsoft.Toolkit.Wpf.UI.Controls"
...>

<controls:MediaPlayerElement x:Name="mediaPlayerElement"
    Source="https://mediaplatstorage1.blob.core.windows.net/windows-universal-samples-media/elephantsdream-clip-h264_sd-aac_eng-aac_spa-aac_eng_commentary-srt_eng-srt_por-srt_swe.mkv"
    AutoPlay="True" Margin="5" HorizontalAlignment="Stretch"  VerticalAlignment="Stretch" AreTransportControlsEnabled="True" />
```

## Properties

The following properties wrap corresponding [properties](/uwp/api/Windows.UI.Xaml.Controls.MediaPlayerElement#properties) of the wrapped UWP [Windows.UI.Xaml.Controls.MediaPlayerElement](/uwp/api/Windows.UI.Xaml.Controls.MediaPlayerElement) object. See the links in this table for more information about each property.

| Property | Type | Description |
| -- | -- | -- |
| AreTransportControlsEnabled | bool | Wraps the [AreTransportControlsEnabled](/uwp/api/windows.ui.xaml.controls.mediaplayerelement.aretransportcontrolsenabled) property. |
| AreTransportControlsEnabledProperty | DependencyProperty | Dependency property for the **AreTransportControlsEnabled** property. |
| AutoPlay | bool | Wraps the [AutoPlay](/uwp/api/windows.ui.xaml.controls.mediaplayerelement.autoplay) property. |
| AutoPlayProperty | DependencyProperty | Dependency property for the **ActiAutoPlayveTool** property. |
| IsFullWindow | bool | Wraps the [IsFullWindow](/uwp/api/windows.ui.xaml.controls.mediaplayerelement.isfullwindow) property. |
| IsFullWindowProperty | DependencyProperty | Dependency property for the **IsFullWindow** property. |
| MediaPlayer | MediaPlayer | Wraps the [MediaPlayer](/uwp/api/windows.ui.xaml.controls.mediaplayerelement.mediaplayer) property. |
| MediaPlayerProperty | DependencyProperty | Dependency property for the **MediaPlayer** property. |
| PosterSource | ImageSource | Wraps the [PosterSource](/uwp/api/windows.ui.xaml.controls.mediaplayerelement.postersource) property. |
| PosterSourceProperty | DependencyProperty | Dependency property for the **PosterSource** property. |
| Source | string | Wraps the [Source](/uwp/api/windows.ui.xaml.controls.mediaplayerelement.source) property. The **Source** property of this wrapped control is exposed as a string, which is interpreted as a URL and bound to the **Source** property of the wrapped UWP control as a UWP-implemented **IMediaPlaybackSource**.|
| SourceProperty | DependencyProperty | Dependency property for the **Source** property. |
| Stretch | Stretch | Wraps the [Stretch](/uwp/api/windows.ui.xaml.controls.mediaplayerelement.stretch) property. |
| StretchProperty | DependencyProperty | Dependency property for the **Stretch** property. |
| TransportControls | MediaTransportControls | Wraps the [TransportControls](/uwp/api/windows.ui.xaml.controls.mediaplayerelement.transportcontrols) property. |

## Methods

| Methods | Return Type | Description |
| -- | -- | -- |
| SetMediaPlayer(MediaPlayer) | void | Wraps the [SetMediaPlayer](/uwp/api/windows.ui.xaml.controls.mediaplayerelement.setmediaplayer) method of the wrapped UWP **MediaPlayerElement** control. |

## Requirements

| Requirement   |  Value      |
|--------|--------|
| Device family | .NET 4.6.2, Windows 10 (introduced v10.0.17709.0) |
| Namespace | Windows Forms: Microsoft.Toolkit.Forms.UI.Controls <br/> WPF: Microsoft.Toolkit.Wpf.UI.Controls |
| NuGet package | Windows Forms: [Microsoft.Toolkit.Forms.UI.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Forms.UI.Controls)  <br/> WPF: [Microsoft.Toolkit.Wpf.UI.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Wpf.UI.Controls) |

## API

* [MediaPlayerElement (Windows Forms)](https://github.com/windows-toolkit/Microsoft.Toolkit.Win32/tree/rel/6.1.2/Microsoft.Toolkit.Forms.UI.Controls/MediaPlayerElement)
* [MediaPlayerElement (WPF)](https://github.com/windows-toolkit/Microsoft.Toolkit.Win32/tree/rel/6.1.2/Microsoft.Toolkit.Wpf.UI.Controls/MediaPlayerElement)

## Related topics

* [MediaPlayerElement (UWP)](/uwp/api/Windows.UI.Xaml.Controls.MediaPlayerElement)
* [Media playback](/windows/uwp/design/controls-and-patterns/media-playback)
