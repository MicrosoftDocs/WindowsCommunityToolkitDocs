---
title: MapControl for Windows Forms and WPF
author: granitestatehacker
description: This control is a wrapper to enable use of the UWP MapControl class in Windows Forms or WPF.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, MapControl, Windows Forms, WPF
---

# MapControl for Windows Forms and WPF

> [!NOTE]
> This control is currently available as a developer preview. Although we encourage you to try out this control in your own prototype code now, we do not recommend that you use it in production code at this time. This control will continue to mature and stabilize in future toolkit releases.

The **MapControl** class enables you to display a symbolic or photorealistic map in your Windows Forms or WPF desktop application. This control shows rich and customizable map data including road maps, aerial, 3D, views, directions, search results, and traffic. You can also display the user's location, directions, and points of interest.

![MapControl example](../../resources/images/Controls/MapControl.png)

## About MapControl

The WPF version of this control is located in the **Microsoft.Toolkit.Wpf.UI.Controls** namespace. The Windows Forms version is located in the **Microsoft.Toolkit.Forms.UI.Controls** namespace. You can find additional related types (such as enums and event args classes) in the **Microsoft.Toolkit.Win32.UI.Controls.Interop.WinRT** namespace.

This control wraps an internal instance of the UWP [Windows.UI.Xaml.Controls.Maps.MapControl](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl) class.

## Known Limitations

<!-- TBD  -->

## Syntax
```xaml
<Window x:Class="TestSample.MainWindow" ...
  xmlns:controls="clr-namespace:Microsoft.Toolkit.Wpf.UI.Controls;assembly=Microsoft.Toolkit.Wpf.UI.Controls"
...>


<controls:MapControl x:Name="mapControl" DockPanel.Dock="Top" ZoomInteractionMode="GestureAndControl"
    TiltInteractionMode="GestureAndControl" MapServiceToken="EnterYourAuthenticationKeyHere" />
```

## Properties

The following properties wrap corresponding [properties](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol#properties) of the internal UWP [Windows.UI.Xaml.Controls.Maps.MapControl](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol) object. See the links in this table for more information about each property.

| Property | Type | Description |
| -- | -- | -- |
| ActualCamera | MapCamera  | Wraps the [ActualCamera](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.actualcamera) property. |
| BusinessLandmarksEnabled | bool  | Wraps the [BusinessLandmarksEnabled](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.businesslandmarksenabled) property. |
| BusinessLandmarksVisible  | bool  | Wraps the [BusinessLandmarksVisible](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.businesslandmarksvisible) property. |
| Center | Geopoint  | Wraps the [Center](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.center) property. |
| CustomExperience | MapCustomExperience  | Wraps the [CustomExperience](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.customexperience) property. |
| DesiredPitch | double  | Wraps the [DesiredPitch](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.desiredpitch) property. |
| Heading | double  | Wraps the [Heading](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.heading) property. |
| Is3DSupported | bool  | Wraps the [Is3DSupported](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.is3dsupported) property. |
| IsStreetsideSupported | bool  | Wraps the [IsStreetsideSupported](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.isstreetsidesupported) property. |
| LandmarksVisible | bool | Wraps the [LandmarksVisible](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.landmarksvisible) property. |
| Layers | IList&lt;MapLayer&gt; | Wraps the [Layers](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.layers) property. |
| LoadingStatus | MapLoadingStatus  | Wraps the [LoadingStatus](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.loadingstatus) property. |
| MapColorScheme  |  ColorScheme| Wraps the [MapColorScheme](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.mapcolorscheme) property. |
| MapElements  | IList&lt;MapElement&gt; | Wraps the [MapElements](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.mapelements) property. |
| MapProjection | MapProjection | Wraps the [MapProjection](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.mapprojection) property. |
| MapServiceToken | string | Wraps the [MapServiceToken](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.mapservicetoken) property. |
| MaxZoomLevel | double  | Wraps the [MaxZoomLevel](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.maxzoomlevel) property. |
| MinZoomLevel | double | Wraps the [MinZoomLevel](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.minzoomlevel) property. |
| PanInteractionMode | MapPanInteractionMode  | Wraps the [PanInteractionMode](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.paninteractionmode) property. |
| PedestrianFeaturesVisible | bool  | Wraps the [PedestrianFeaturesVisible](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.pedestrianfeaturesvisible) property. |
| Pitch | double | Wraps the [Pitch](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.pitch) property. |
| Region | string | Wraps the [Region](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.region) property. |
| RotateInteractionMode | MapInteractionMode  | Wraps the [RotateInteractionMode](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.rotateinteractionmode) property. |
| Routes | IList&lt;MapRouteView&gt; | Wraps the [Routes](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.routes) property. |
| Scene | MapScene  | Wraps the [Scene](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.scene) property. |
| Style | MapStyle  | Wraps the [Style](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.style) property. |
| StyleSheet | MapStyleSheet  | Wraps the [StyleSheet](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.stylesheet) property. |
| TargetCamera | MapCamera  | Wraps the [TargetCamera](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.targetcamera) property. |
| TileSources | IList&lt;MapTileSource&gt; | Wraps the [TileSources](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.tilesources) property. |
| TiltInteractionMode | MapInteractionMode  | Wraps the [TiltInteractionMode](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.tiltinteractionmode) property. |
| TrafficFlowVisible | bool  | Wraps the [TrafficFlowVisible](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.trafficflowvisible) property. |
| TransitFeaturesEnabled | bool  | Wraps the [TransitFeaturesEnabled](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.transitfeaturesenabled) property. |
| TransitFeaturesVisible | bool  | Wraps the [TransitFeaturesVisible](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.transitfeaturesvisible) property. |
| TransformOrigin | Point | Wraps the [TransformOrigin](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.transformorigin) property. |
| WatermarkMode | MapWatermarkMode | Wraps the [WatermarkMode](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.watermarkmode) property. |
| ZoomInteractionMode | MapInteractionMode  | Wraps the [ZoomInteractionMode](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.zoominteractionmode) property. |
| ZoomLevel | double | Wraps the [ZoomLevel](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.zoomlevel) property.  |

## Methods

The following methods wrap corresponding [methods](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol#methods) of the internal UWP [Windows.UI.Xaml.Controls.Maps.MapControl](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol) object. See the links in this table for more information about each method.

| Method | Return Type | Description |
| -- | -- | -- |
| FindMapElementsAtOffset(Point) | IReadOnlyList&lt;MapElement&gt; | Wraps the [FindMapElementsAtOffset(Point)](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.findmapelementsatoffset#Windows_UI_Xaml_Controls_Maps_MapControl_FindMapElementsAtOffset_Windows_Foundation_Point_) method. |
| FindMapElementsAtOffset(Point, double) | IReadOnlyList&lt;MapElement&gt; | Wraps the [FindMapElementsAtOffset(Point, double)](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.findmapelementsatoffset#Windows_UI_Xaml_Controls_Maps_MapControl_FindMapElementsAtOffset_Windows_Foundation_Point_System_Double_) method. |
| GetLocationFromOffset(Point, Geopoint) | void   | Wraps the [GetLocationFromOffset(Point, Geopoint)](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.getlocationfromoffset#Windows_UI_Xaml_Controls_Maps_MapControl_GetLocationFromOffset_Windows_Foundation_Point_Windows_Devices_Geolocation_Geopoint__) method. |
| GetLocationFromOffset(Point, AltitudeReferenceSystem, Geopoint) | void | Wraps the [GetLocationFromOffset(Point, AltitudeReferenceSystem, Geopoint)](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.getlocationfromoffset#Windows_UI_Xaml_Controls_Maps_MapControl_GetLocationFromOffset_Windows_Foundation_Point_Windows_Devices_Geolocation_AltitudeReferenceSystem_Windows_Devices_Geolocation_Geopoint__) method. |
| GetOffsetFromLocation | void  | Wraps the [GetOffsetFromLocation](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.getoffsetfromlocation) method. |
| GetVisibleRegion | Geopath | Wraps the [GetVisibleRegion](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.getvisibleregion) method. |
| IsLocationInView | void  | Wraps the [IsLocationInView](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.islocationinview) method. |
| StartContinuousPan | void  | Wraps the [StartContinuousPan](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.startcontinuouspan) method.  |
| StartContinuousRotate | void  | Wraps the [StartContinuousRotate](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.startcontinuousrotate) method. |
| StartContinuousTilt | void  | Wraps the [StartContinuousTilt](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.startcontinuoustilt) method. |
| StartContinuousZoom | void  | Wraps the [StartContinuousZoom](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.startcontinuouszoom) method. |
| StopContinuousPan | void  | Wraps the [StopContinuousPan](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.stopcontinuouspan) method. |
| StopContinuousRotate | void  | Wraps the [StopContinuousRotate](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.stopcontinuousrotate) method. |
| StopContinuousTilt | void  | Wraps the [StopContinuousTilt](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.stopcontinuoustilt) method. |
| StopContinuousZoom | void  | Wraps the [StopContinuousZoom](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.stopcontinuouszoom) method. |
| TryGetLocationFromOffset(Point, Geopoint) | bool |  Wraps the [TryGetLocationFromOffset(Point, Geopoint)](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.trygetlocationfromoffset#Windows_UI_Xaml_Controls_Maps_MapControl_TryGetLocationFromOffset_Windows_Foundation_Point_Windows_Devices_Geolocation_Geopoint__) method. |
| TryGetLocationFromOffset(Point, AltitudeReferenceSystem, Geopoint) | bool | Wraps the [TryGetLocationFromOffset(Point, AltitudeReferenceSystem, Geopoint)](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.trygetlocationfromoffset#Windows_UI_Xaml_Controls_Maps_MapControl_TryGetLocationFromOffset_Windows_Foundation_Point_Windows_Devices_Geolocation_AltitudeReferenceSystem_Windows_Devices_Geolocation_Geopoint__) method. |
| TryPanAsync | bool | Wraps the [TryPanAsync](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.trypanasync) method. |
| TryPanToAsync | bool | Wraps the [TryPanToAsync](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.trypantoasync) method. |
| TryRotateAsync | bool | Wraps the [TryRotateAsync](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.tryrotateasync) method. |
| TryRotateToAsync | bool | Wraps the [TryRotateToAsync](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.tryrotatetoasync) method. |
| TrySetSceneAsync(MapScene) | bool | Wraps the [TrySetSceneAsync(MapScene)](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.trysetsceneasync#Windows_UI_Xaml_Controls_Maps_MapControl_TrySetSceneAsync_Windows_UI_Xaml_Controls_Maps_MapScene_) method. |
| TrySetSceneAsync(MapScene, MapAnimationKind) | bool | Wraps the [TrySetSceneAsync(MapScene, MapAnimationKind)](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.trysetsceneasync#Windows_UI_Xaml_Controls_Maps_MapControl_TrySetSceneAsync_Windows_UI_Xaml_Controls_Maps_MapScene_Windows_UI_Xaml_Controls_Maps_MapAnimationKind_) method. |
| TrySetViewAsync(Geopoint) | bool | Wraps the [TrySetViewAsync(Geopoint)](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.trysetviewasync#Windows_UI_Xaml_Controls_Maps_MapControl_TrySetViewAsync_Windows_Devices_Geolocation_Geopoint_) method. |
| TrySetViewAsync(Geopoint, Nullable&lt;double&gt;) | bool | Wraps the [TrySetViewAsync(Geopoint, Nullable&lt;double&gt;)](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.trysetviewasync#Windows_UI_Xaml_Controls_Maps_MapControl_TrySetViewAsync_Windows_Devices_Geolocation_Geopoint_Windows_Foundation_IReference_System_Double__) method. |
| TrySetViewAsync(Geopoint, Nullable&lt;double&gt;, Nullable&lt;double&gt;, Nullable&lt;double&gt;) | bool | Wraps the [TrySetViewAsync(Geopoint, Nullable&lt;double&gt;, Nullable&lt;double&gt;, Nullable&lt;double&gt;)](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.trysetviewasync#Windows_UI_Xaml_Controls_Maps_MapControl_TrySetViewAsync_Windows_Devices_Geolocation_Geopoint_Windows_Foundation_IReference_System_Double__Windows_Foundation_IReference_System_Double__Windows_Foundation_IReference_System_Double__) method. |
| TrySetViewAsync(Geopoint, Nullable&lt;double&gt;, Nullable&lt;double&gt;, Nullable&lt;double&gt;, MapAnimationKind) | bool | Wraps the [TrySetViewAsync(Geopoint, Nullable&lt;double&gt;, Nullable&lt;double&gt;, Nullable&lt;double&gt;, MapAnimationKind)](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.trysetviewasync#Windows_UI_Xaml_Controls_Maps_MapControl_TrySetViewAsync_Windows_Devices_Geolocation_Geopoint_Windows_Foundation_IReference_System_Double__Windows_Foundation_IReference_System_Double__Windows_Foundation_IReference_System_Double__Windows_UI_Xaml_Controls_Maps_MapAnimationKind_) method. |
| TryTiltAsync | bool | Wraps the [TryTiltAsync](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.trytiltasync) method. |
| TryTiltToAsync | bool | Wraps the [TryTiltToAsync](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.trytilttoasync) method. |
| TryZoomInAsync | bool | Wraps the [TryZoomInAsync](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.tryzoominasync) method. |
| TryZoomOutAsync | bool | Wraps the [TryZoomOutAsync](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.tryzoomoutasync) method. |
| TryZoomToAsync | bool | Wraps the [TryZoomToAsync](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.tryzoomtoasync) method. |

## Events

The following events wrap corresponding [events](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol#events) of the internal UWP [Windows.UI.Xaml.Controls.Maps.MapControl](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol) object. See the links in this table for more information about each event.

| Event | Description |
| -- | -- |
| ActualCameraChanged  | Wraps the [ActualCameraChanged](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.actualcamerachanged) event. |
| ActualCameraChanging   | Wraps the [ActualCameraChanging](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.actualcamerachanging) event. |
| CenterChanged  | Wraps the [CenterChanged](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.centerchanged) event. |
| CustomExperienceChanged   | Wraps the [CustomExperienceChanged](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.customexperiencechanged) event. |
| HeadingChanged  | Wraps the [HeadingChanged](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.headingchanged) event. |
| LoadingStatusChanged  | Wraps the [LoadingStatusChanged](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.loadingstatuschanged) event. |
| MapContextRequested  | Wraps the [MapContextRequested](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.mapcontextrequested) event. |
| MapDoubleTapped  | Wraps the [MapDoubleTapped](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.mapdoubletapped) event |
| MapElementClick  | Wraps the [MapElementClick](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.mapelementclick) event. |
| MapElementPointerEntered  | Wraps the [MapElementPointerEntered](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.mapelementpointerentered) event. |
| MapElementPointerExited  | Wraps the [MapElementPointerExited](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.mapelementpointerexited) event. |
| MapHolding  | Wraps the [MapHolding](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.mapholding) event. |
| MapRightTapped  | Wraps the [MapRightTapped](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.maprighttapped) event. |
| MapTapped  | Wraps the [MapTapped](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.maptapped) event. |
| PitchChanged  | Wraps the [PitchChanged](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.pitchchanged) event. |
| TargetCameraChanged  | Wraps the [TargetCameraChanged](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.targetcamerachanged) event. |
| TransformOriginChanged  | Wraps the [TransformOriginChanged](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.transformoriginchanged) event. |
| ZoomLevelChanged  | Wraps the [ZoomLevelChanged](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.maps.mapcontrol.zoomlevelchanged) event. |


## Requirements

|        |        |
|--------|--------|
| Device family | .NET 4.6.2, Windows 10 (introduced v10.0.17709.0) |
| Namespace | Windows Forms: Microsoft.Toolkit.Forms.UI.Controls <br/> WPF: Microsoft.Toolkit.Wpf.UI.Controls |
| NuGet package | Windows Forms: [Microsoft.Toolkit.Forms.UI.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Forms.UI.Controls)  <br/> WPF: [Microsoft.Toolkit.Wpf.UI.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Wpf.UI.Controls) |

## API Source Code

- [MapControl (Windows Forms)](https://github.com/Microsoft/WindowsCommunityToolkit/tree/master/Microsoft.Toolkit.Win32/Microsoft.Toolkit.Forms.UI.Controls/MapControl)
- [MapControl (WPF)](https://github.com/Microsoft/WindowsCommunityToolkit/tree/master/Microsoft.Toolkit.Win32/Microsoft.Toolkit.Wpf.UI.Controls/MapControl)


## Related Topics

- [Windows.UI.Xaml.Controls.Maps.MapControl](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Maps.MapControl)
- [Display maps](https://docs.microsoft.com/windows/uwp/maps-and-location/display-maps)
