---
title: MapControl for Windows Forms and WPF
author: mcleanbyron
description: This control is a wrapper to enable use of the UWP MapControl class in Windows Forms or WPF.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, MapControl, Windows Forms, WPF
dev_langs:
  - csharp
  - vb
---

# MapControl for Windows Forms and WPF

The **MapControl** class enables you to display a symbolic or photorealistic map in your Windows Forms or WPF desktop application. This is one of several wrapped Universal Windows Platform controls that are available for Windows Forms and WPF applications as part of a feature called *XAML Islands*. For more information, see [UWP controls in desktop applications (XAML Islands)](/windows/uwp/xaml-platform/xaml-host-controls).

This control shows rich and customizable map data including road maps, aerial, 3D, views, directions, search results, and traffic. You can also display the user's location, directions, and points of interest.

![MapControl example](../../resources/images/Controls/MapControl.png)

> [!NOTE]
> If you have feedback about this control, create a new issue in the [Microsoft.Toolkit.Win32 repo](https://github.com/windows-toolkit/Microsoft.Toolkit.Win32/issues) and leave your comments there. If you prefer to submit your feedback privately, you can send it to XamlIslandsFeedback@microsoft.com.

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://WPFandWinFormsControls?sample=MapControl)

## About MapControl

This control wraps an instance of the UWP [Windows.UI.Xaml.Controls.Maps.MapControl](/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl) class. The WPF version of this control is located in the **Microsoft.Toolkit.Wpf.UI.Controls** namespace. The Windows Forms version is located in the **Microsoft.Toolkit.Forms.UI.Controls** namespace. You can find additional related types (such as enums and event args classes) in the **Microsoft.Toolkit.Win32.UI.Controls.Interop.WinRT** namespace.

## Prerequisites

Before you can use this control, you must follow [these instructions](/windows/apps/desktop/modernize/xaml-islands#requirements) to configure your project to support XAML Islands.

## Known issues and limitations

See our list of [known issues](https://github.com/windows-toolkit/Microsoft.Toolkit.Win32/issues) for WPF and Windows Forms controls in the Windows Community Toolkit repo.

## Syntax

```xaml
<Window x:Class="TestSample.MainWindow" ...
  xmlns:controls="clr-namespace:Microsoft.Toolkit.Wpf.UI.Controls;assembly=Microsoft.Toolkit.Wpf.UI.Controls"
...>


<controls:MapControl x:Name="mapControl" DockPanel.Dock="Top" ZoomInteractionMode="GestureAndControl"
    TiltInteractionMode="GestureAndControl" MapServiceToken="EnterYourAuthenticationKeyHere" />
```

## Code example

```csharp
private async void MapControl_Loaded(object sender, RoutedEventArgs e)
{
    // Specify a known location.
    BasicGeoposition cityPosition = new BasicGeoposition() { Latitude = 47.604, Longitude = -122.329 };
    var cityCenter = new Geopoint(cityPosition);

    // Set the map location.
    await (sender as MapControl).TrySetViewAsync(cityCenter, 12);
}
```

```vb
Private Async Sub MapControl_Loaded(sender As Object, e As RoutedEventArgs)
    Dim cityPosition As BasicGeoposition = New BasicGeoposition() With {
        .Latitude = 47.604,
        .Longitude = -122.329
    }
    Dim cityCenter = New Geopoint(cityPosition)
    Await (TryCast(sender, MapControl)).TrySetViewAsync(cityCenter, 12)
End Sub
```

## Properties

The following properties wrap corresponding [properties](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol#properties) of the wrapped UWP [Windows.UI.Xaml.Controls.Maps.MapControl](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol) object. See the links in this table for more information about each property.

| Property | Type | Description |
| -- | -- | -- |
| ActualCamera | MapCamera  | Wraps the [ActualCamera](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.actualcamera) property. |
| BusinessLandmarksEnabled | bool  | Wraps the [BusinessLandmarksEnabled](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.businesslandmarksenabled) property. |
| BusinessLandmarksVisible  | bool  | Wraps the [BusinessLandmarksVisible](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.businesslandmarksvisible) property. |
| Center | Geopoint  | Wraps the [Center](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.center) property. |
| CustomExperience | MapCustomExperience  | Wraps the [CustomExperience](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.customexperience) property. |
| DesiredPitch | double  | Wraps the [DesiredPitch](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.desiredpitch) property. |
| Heading | double  | Wraps the [Heading](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.heading) property. |
| Is3DSupported | bool  | Wraps the [Is3DSupported](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.is3dsupported) property. |
| IsStreetsideSupported | bool  | Wraps the [IsStreetsideSupported](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.isstreetsidesupported) property. |
| LandmarksVisible | bool | Wraps the [LandmarksVisible](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.landmarksvisible) property. |
| Layers | IList&lt;MapLayer&gt; | Wraps the [Layers](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.layers) property. |
| LoadingStatus | MapLoadingStatus  | Wraps the [LoadingStatus](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.loadingstatus) property. |
| MapColorScheme  |  ColorScheme| Wraps the [MapColorScheme](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.colorscheme) property. |
| MapElements  | IList&lt;MapElement&gt; | Wraps the [MapElements](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.mapelements) property. |
| MapProjection | MapProjection | Wraps the [MapProjection](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.mapprojection) property. |
| MapServiceToken | string | Wraps the [MapServiceToken](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.mapservicetoken) property. |
| MaxZoomLevel | double  | Wraps the [MaxZoomLevel](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.maxzoomlevel) property. |
| MinZoomLevel | double | Wraps the [MinZoomLevel](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.minzoomlevel) property. |
| PanInteractionMode | MapPanInteractionMode  | Wraps the [PanInteractionMode](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.paninteractionmode) property. |
| PedestrianFeaturesVisible | bool  | Wraps the [PedestrianFeaturesVisible](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.pedestrianfeaturesvisible) property. |
| Pitch | double | Wraps the [Pitch](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.pitch) property. |
| Region | string | Wraps the [Region](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.region) property. |
| RotateInteractionMode | MapInteractionMode  | Wraps the [RotateInteractionMode](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.rotateinteractionmode) property. |
| Routes | IList&lt;MapRouteView&gt; | Wraps the [Routes](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.routes) property. |
| Scene | MapScene  | Wraps the [Scene](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.scene) property. |
| Style | MapStyle  | Wraps the [Style](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.style) property. |
| StyleSheet | MapStyleSheet  | Wraps the [StyleSheet](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.stylesheet) property. |
| TargetCamera | MapCamera  | Wraps the [TargetCamera](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.targetcamera) property. |
| TileSources | IList&lt;MapTileSource&gt; | Wraps the [TileSources](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.tilesources) property. |
| TiltInteractionMode | MapInteractionMode  | Wraps the [TiltInteractionMode](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.tiltinteractionmode) property. |
| TrafficFlowVisible | bool  | Wraps the [TrafficFlowVisible](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.trafficflowvisible) property. |
| TransitFeaturesEnabled | bool  | Wraps the [TransitFeaturesEnabled](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.transitfeaturesenabled) property. |
| TransitFeaturesVisible | bool  | Wraps the [TransitFeaturesVisible](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.transitfeaturesvisible) property. |
| TransformOrigin | Point | Wraps the [TransformOrigin](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.transformorigin) property. |
| WatermarkMode | MapWatermarkMode | Wraps the [WatermarkMode](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.watermarkmode) property. |
| ZoomInteractionMode | MapInteractionMode  | Wraps the [ZoomInteractionMode](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.zoominteractionmode) property. |
| ZoomLevel | double | Wraps the [ZoomLevel](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.zoomlevel) property.  |

## Methods

The following methods wrap corresponding [methods](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol#methods) of the wrapped UWP [Windows.UI.Xaml.Controls.Maps.MapControl](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol) object. See the links in this table for more information about each method.

| Method | Return Type | Description |
| -- | -- | -- |
| FindMapElementsAtOffset(Point) | IReadOnlyList&lt;MapElement&gt; | Wraps the [FindMapElementsAtOffset(Point)](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.findmapelementsatoffset#Windows_UI_Xaml_Controls_Maps_MapControl_FindMapElementsAtOffset_Windows_Foundation_Point_) method. |
| FindMapElementsAtOffset(Point, double) | IReadOnlyList&lt;MapElement&gt; | Wraps the [FindMapElementsAtOffset(Point, double)](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.findmapelementsatoffset#Windows_UI_Xaml_Controls_Maps_MapControl_FindMapElementsAtOffset_Windows_Foundation_Point_System_Double_) method. |
| GetLocationFromOffset(Point, Geopoint) | void   | Wraps the [GetLocationFromOffset(Point, Geopoint)](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.getlocationfromoffset#Windows_UI_Xaml_Controls_Maps_MapControl_GetLocationFromOffset_Windows_Foundation_Point_Windows_Devices_Geolocation_Geopoint__) method. |
| GetLocationFromOffset(Point, AltitudeReferenceSystem, Geopoint) | void | Wraps the [GetLocationFromOffset(Point, AltitudeReferenceSystem, Geopoint)](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.getlocationfromoffset#Windows_UI_Xaml_Controls_Maps_MapControl_GetLocationFromOffset_Windows_Foundation_Point_Windows_Devices_Geolocation_AltitudeReferenceSystem_Windows_Devices_Geolocation_Geopoint__) method. |
| GetOffsetFromLocation | void  | Wraps the [GetOffsetFromLocation](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.getoffsetfromlocation) method. |
| GetVisibleRegion | Geopath | Wraps the [GetVisibleRegion](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.getvisibleregion) method. |
| IsLocationInView | void  | Wraps the [IsLocationInView](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.islocationinview) method. |
| StartContinuousPan | void  | Wraps the [StartContinuousPan](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.startcontinuouspan) method.  |
| StartContinuousRotate | void  | Wraps the [StartContinuousRotate](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.startcontinuousrotate) method. |
| StartContinuousTilt | void  | Wraps the [StartContinuousTilt](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.startcontinuoustilt) method. |
| StartContinuousZoom | void  | Wraps the [StartContinuousZoom](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.startcontinuouszoom) method. |
| StopContinuousPan | void  | Wraps the [StopContinuousPan](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.stopcontinuouspan) method. |
| StopContinuousRotate | void  | Wraps the [StopContinuousRotate](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.stopcontinuousrotate) method. |
| StopContinuousTilt | void  | Wraps the [StopContinuousTilt](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.stopcontinuoustilt) method. |
| StopContinuousZoom | void  | Wraps the [StopContinuousZoom](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.stopcontinuouszoom) method. |
| TryGetLocationFromOffset(Point, Geopoint) | bool |  Wraps the [TryGetLocationFromOffset(Point, Geopoint)](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.trygetlocationfromoffset#Windows_UI_Xaml_Controls_Maps_MapControl_TryGetLocationFromOffset_Windows_Foundation_Point_Windows_Devices_Geolocation_Geopoint__) method. |
| TryGetLocationFromOffset(Point, AltitudeReferenceSystem, Geopoint) | bool | Wraps the [TryGetLocationFromOffset(Point, AltitudeReferenceSystem, Geopoint)](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.trygetlocationfromoffset#Windows_UI_Xaml_Controls_Maps_MapControl_TryGetLocationFromOffset_Windows_Foundation_Point_Windows_Devices_Geolocation_AltitudeReferenceSystem_Windows_Devices_Geolocation_Geopoint__) method. |
| TryPanAsync | bool | Wraps the [TryPanAsync](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.trypanasync) method. |
| TryPanToAsync | bool | Wraps the [TryPanToAsync](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.trypantoasync) method. |
| TryRotateAsync | bool | Wraps the [TryRotateAsync](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.tryrotateasync) method. |
| TryRotateToAsync | bool | Wraps the [TryRotateToAsync](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.tryrotatetoasync) method. |
| TrySetSceneAsync(MapScene) | bool | Wraps the [TrySetSceneAsync(MapScene)](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.trysetsceneasync#Windows_UI_Xaml_Controls_Maps_MapControl_TrySetSceneAsync_Windows_UI_Xaml_Controls_Maps_MapScene_) method. |
| TrySetSceneAsync(MapScene, MapAnimationKind) | bool | Wraps the [TrySetSceneAsync(MapScene, MapAnimationKind)](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.trysetsceneasync#Windows_UI_Xaml_Controls_Maps_MapControl_TrySetSceneAsync_Windows_UI_Xaml_Controls_Maps_MapScene_Windows_UI_Xaml_Controls_Maps_MapAnimationKind_) method. |
| TrySetViewAsync(Geopoint) | bool | Wraps the [TrySetViewAsync(Geopoint)](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.trysetviewasync#Windows_UI_Xaml_Controls_Maps_MapControl_TrySetViewAsync_Windows_Devices_Geolocation_Geopoint_) method. |
| TrySetViewAsync(Geopoint, Nullable&lt;double&gt;) | bool | Wraps the [TrySetViewAsync(Geopoint, Nullable&lt;double&gt;)](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.trysetviewasync#Windows_UI_Xaml_Controls_Maps_MapControl_TrySetViewAsync_Windows_Devices_Geolocation_Geopoint_Windows_Foundation_IReference_System_Double__) method. |
| TrySetViewAsync(Geopoint, Nullable&lt;double&gt;, Nullable&lt;double&gt;, Nullable&lt;double&gt;) | bool | Wraps the [TrySetViewAsync(Geopoint, Nullable&lt;double&gt;, Nullable&lt;double&gt;, Nullable&lt;double&gt;)](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.trysetviewasync#Windows_UI_Xaml_Controls_Maps_MapControl_TrySetViewAsync_Windows_Devices_Geolocation_Geopoint_Windows_Foundation_IReference_System_Double__Windows_Foundation_IReference_System_Double__Windows_Foundation_IReference_System_Double__) method. |
| TrySetViewAsync(Geopoint, Nullable&lt;double&gt;, Nullable&lt;double&gt;, Nullable&lt;double&gt;, MapAnimationKind) | bool | Wraps the [TrySetViewAsync(Geopoint, Nullable&lt;double&gt;, Nullable&lt;double&gt;, Nullable&lt;double&gt;, MapAnimationKind)](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.trysetviewasync#Windows_UI_Xaml_Controls_Maps_MapControl_TrySetViewAsync_Windows_Devices_Geolocation_Geopoint_Windows_Foundation_IReference_System_Double__Windows_Foundation_IReference_System_Double__Windows_Foundation_IReference_System_Double__Windows_UI_Xaml_Controls_Maps_MapAnimationKind_) method. |
| TryTiltAsync | bool | Wraps the [TryTiltAsync](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.trytiltasync) method. |
| TryTiltToAsync | bool | Wraps the [TryTiltToAsync](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.trytilttoasync) method. |
| TryZoomInAsync | bool | Wraps the [TryZoomInAsync](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.tryzoominasync) method. |
| TryZoomOutAsync | bool | Wraps the [TryZoomOutAsync](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.tryzoomoutasync) method. |
| TryZoomToAsync | bool | Wraps the [TryZoomToAsync](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.tryzoomtoasync) method. |

## Events

The following events wrap corresponding [events](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol#events) of the wrapped UWP [Windows.UI.Xaml.Controls.Maps.MapControl](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol) object. See the links in this table for more information about each event.

| Event | Description |
| -- | -- |
| ActualCameraChanged  | Wraps the [ActualCameraChanged](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.actualcamerachanged) event. |
| ActualCameraChanging   | Wraps the [ActualCameraChanging](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.actualcamerachanging) event. |
| CenterChanged  | Wraps the [CenterChanged](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.centerchanged) event. |
| CustomExperienceChanged   | Wraps the [CustomExperienceChanged](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.customexperiencechanged) event. |
| HeadingChanged  | Wraps the [HeadingChanged](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.headingchanged) event. |
| LoadingStatusChanged  | Wraps the [LoadingStatusChanged](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.loadingstatuschanged) event. |
| MapContextRequested  | Wraps the [MapContextRequested](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.mapcontextrequested) event. |
| MapDoubleTapped  | Wraps the [MapDoubleTapped](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.mapdoubletapped) event |
| MapElementClick  | Wraps the [MapElementClick](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.mapelementclick) event. |
| MapElementPointerEntered  | Wraps the [MapElementPointerEntered](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.mapelementpointerentered) event. |
| MapElementPointerExited  | Wraps the [MapElementPointerExited](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.mapelementpointerexited) event. |
| MapHolding  | Wraps the [MapHolding](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.mapholding) event. |
| MapRightTapped  | Wraps the [MapRightTapped](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.maprighttapped) event. |
| MapTapped  | Wraps the [MapTapped](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.maptapped) event. |
| PitchChanged  | Wraps the [PitchChanged](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.pitchchanged) event. |
| TargetCameraChanged  | Wraps the [TargetCameraChanged](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.targetcamerachanged) event. |
| TransformOriginChanged  | Wraps the [TransformOriginChanged](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.transformoriginchanged) event. |
| ZoomLevelChanged  | Wraps the [ZoomLevelChanged](/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.zoomlevelchanged) event. |

## Requirements

| Requirement   |  Value      |
|--------|--------|
| Device family | .NET 4.6.2, Windows 10 (introduced v10.0.17709.0) |
| Namespace | Windows Forms: Microsoft.Toolkit.Forms.UI.Controls <br/> WPF: Microsoft.Toolkit.Wpf.UI.Controls |
| NuGet package | Windows Forms: [Microsoft.Toolkit.Forms.UI.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Forms.UI.Controls)  <br/> WPF: [Microsoft.Toolkit.Wpf.UI.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Wpf.UI.Controls) |

## API

- [MapControl (Windows Forms)](https://github.com/windows-toolkit/Microsoft.Toolkit.Win32/tree/rel/6.1.2/Microsoft.Toolkit.Forms.UI.Controls/MapControl)
- [MapControl (WPF)](https://github.com/windows-toolkit/Microsoft.Toolkit.Win32/tree/rel/6.1.2/Microsoft.Toolkit.Wpf.UI.Controls/MapControl)

## Related topics

- [Windows.UI.Xaml.Controls.Maps.MapControl](/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl)
- [Display maps](/windows/uwp/maps-and-location/display-maps)
