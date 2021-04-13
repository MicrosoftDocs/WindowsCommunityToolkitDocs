---
title: Known Issues in WebView control
author: mcleanbyron
description: This guide highlights known limitations with the current release of the WebView control for Windows Forms and WPF applications.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, WebView, Windows Forms, WPF, known issues, release notes
---

# Known Issues of the WebView control for Windows Forms and WPF applications

> [!NOTE]
> **WebView** is now deprecated. Use [WebView2](/microsoft-edge/hosting/webview2) instead.

This document describes issues and limitations in this release of the **WebView** control.

Answers to a number of [*Frequently Asked Questions on WebView*](./WebView.md#frequently-asked-questions-faqs)  for Windows Forms and WPF applications are also available.

## WebView control members

The **WebView** control does not implement these methods of the [IWebViewControl](/uwp/api/windows.web.ui.iwebviewcontrol).

* [NavigateToLocalStreamUri](/uwp/api/windows.web.ui.iwebviewcontrol.navigatetolocalstreamuri). Instead use `NavigateToLocal`.

* [NavigateWithHttpRequestMessage](/uwp/api/windows.web.ui.iwebviewcontrol.navigatewithhttprequestmessage)

* [CapturePreviewToStreamAsync](/uwp/api/windows.web.ui.iwebviewcontrol.capturepreviewtostreamasync)

* [CaptureSelectedContentToDataPackageAsync](/uwp/api/windows.web.ui.iwebviewcontrol.captureselectedcontenttodatapackageasync)

* [BuildLocalStreamUri](/uwp/api/windows.web.ui.iwebviewcontrol.buildlocalstreamuri)

The **WebView** control implements these events of the [IWebViewControl](/uwp/api/windows.web.ui.iwebviewcontrol), but they don't work as expected.

* [LongRunningScriptDetected](/uwp/api/windows.web.ui.iwebviewcontrol.longrunningscriptdetected)

* [UnsafeContentWarningDisplaying](/uwp/api/windows.web.ui.iwebviewcontrol.unsafecontentwarningdisplaying)

* [UnsupportedUriSchemeIdentified](/uwp/api/windows.web.ui.iwebviewcontrol.unsupportedurischemeidentified)

* [UnviewableContentIdentified](/uwp/api/windows.web.ui.iwebviewcontrol.unviewablecontentidentified)

* [NewWindowRequested](/uwp/api/windows.web.ui.iwebviewcontrol.newwindowrequested)

### InvokeScriptAsync

* Contrary to its name, the [WebViewControl.InvokeScriptAsync](/uwp/api/windows.web.ui.interop.webviewcontrol.invokescriptasync) method is not actually asynchrounous, as the Win32 application and WebView share the same input queue.

* [WebViewControl.InvokeScriptAsync](/uwp/api/windows.web.ui.interop.webviewcontrol.invokescriptasync) only returns strings. For example, `WebView.InvokeScriptAsync("eval", "1==1")` returns an empty string rather than *true*, unless you use *toString*:
`WebView.InvokeScriptAsync("eval", "(1==1).toString()")`

## Rendering and layout

* The [Control.Bounds](https://msdn.microsoft.com/library/system.windows.forms.control.bounds.aspx) property is not supported.

* The **WebView** control doesn't appear as expected on some high-resolution displays.

* The **WebView** control doesn't appear at the correct scale when users move the host application between monitors that have different screen resolutions.

  To workaround this issue, see the [Enable the WebView control to appear properly on high DPI displays](WebView.md#high-dpi) section of the [WebView](WebView.md) guide.

## Performance

* **WebView** controls in WPF applications have longer load times than Windows Forms applications.

* If the web view stops responding or stops working, other applications that use the same underlying process (WWAHost) will stop responding or stop working as well.

## Security

* **WebView** controls don't render in XAML Browser Applications (XBAP).

  That's because a browser has partial trust to the system while WebView controls have full-trust.

* Content in the **WebView** can be blocked even if the user responds to a system prompt by providing permission to the control.

  This can happen if the Win32WebViewHost (or "Desktop Web App Viewer" in Insider builds) application is disabled in the location settings of the user's system. To resolve the issue, users can open those settings and enable the Win32WebViewHost (or "Desktop Web App Viewer" in Insider builds) application.

* **WebView** controls won't function as expected in a WPF-based ClickOnce application.

* **WebView** controls function only in applications that use a Single-Threaded Apartment (STA) model. Multithreaded Apartment (MTA) model is not supported.

* **WebView** controls have not been tested for Windows Information Protection. Therefore, the information that moves in and out of the WebView control might not be properly secured even if an  organizational administrator applies a Windows Information Protection policy to the hosting application.  

* **WebView** controls have not been exhaustively tested for security.

## User interaction

* Accelerator keys don't work in **WebView** controls.

* Users can't use the TAB key to put the **WebView** into focus. They'll have to use the mouse or other pointing device to put the **WebView** control into focus.

## Paths and strings

* You can use only absolute URIs to resources in members of the **WebView** control that accept string paths.

* **WebView** controls don't recognize the ms-appx:/// prefix, so they can't read from the package (if you've created a package for your application).

* **WebView** controls don't recognize the File:// prefix. If you want to read a file into a **WebView** control, call the `NavigateToLocal(String)` or the `NavigateToLocalStreamUri(Uri, IUriToStreamResolver)` method, or add code to your application that reads the content of the file. Then, serialize that content into a string, and call the `NavigateToString(String)` method of the **WebView** control.

* **WebView** controls don't support URI's that are not encoded in UTF-8. Characters between UTF-16 and UTF-32 aren't supported.

* **WebView** controls don't support URIs that are greater than 2048 characters.

## Host container

* **WebView** controls can be hosted in a popup window. We recommend that you do not do this because support for that scenario will soon be disabled for security reasons.

* Web applications that run in a **WebView** control can't initiate downloads.

* Service workers can't run in a **WebView** control.

## WebView browser

* The [WebBrower.ObjectForScripting](https://msdn.microsoft.com/library/system.windows.controls.webbrowser.objectforscripting.aspx) property and [WebView.AddWebAllowedObject(String, Object)](/uwp/api/windows.ui.xaml.controls.webview.addweballowedobject) are not supported.

  Instead, use the [WebViewControl.InvokeScriptAsync](/uwp/api/windows.web.ui.interop.webviewcontrol.invokescriptasync) method.

* You can't programmatically navigate by using a new window.

* You can't programmatically navigate to a specific frame.

* You can't programmatically print information from a WebView control.

* There's no way to programmatically refresh content with cache validation. By default, pages refresh without cache validation by sending a "Pragma:no-cache" header to the server.
