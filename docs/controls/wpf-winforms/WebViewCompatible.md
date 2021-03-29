---
title: WebViewCompatible control for Windows Forms and WPF
author: mcleanbyron
description: The Windows Community Toolkit provides a version of the UWP web view control that can be used in WPF and Windows Forms applications. This control embeds a view into your application that renders web content in one of two ways. For client environments that support the WebViewControl (Windows 10), that implementation is used. For legacy systems, System.Windows.Controls.WebBrowser implements the view.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, WebView, Windows Forms, WPF
dev_langs:
  - csharp
  - vb
---

# WebViewCompatible control for Windows Forms and WPF

The **WebViewCompatible** control shows web content in your Windows Forms or WPF desktop application. This is one of several wrapped Universal Windows Platform controls that are available for Windows Forms and WPF applications. For more information, see [UWP controls in desktop applications](/windows/uwp/xaml-platform/xaml-host-controls).

![WebViewCompatible example](../../resources/images/Controls/WebView/web-view-samples.png)

Unlike [WebView](WebView.md), **WebViewCompatible** uses one of two rendering engines to support a broader set of Windows clients:

* On Windows 10 devices, the newer Microsoft Edge rendering engine is used to embed a view that renders richly formatted HTML content from a remote web server, dynamically generated code, or content files.
* On devices running older versions of Windows, the [System.Windows.Controls.WebBrowser](/dotnet/api/system.windows.controls.webbrowser) is used, which provides Internet Explorer engine-based rendering.

> [!NOTE]
> The Edge runtime does not at the moment work when the process is elevated as an administrator. Therefore **WebViewCompatible** will fall back to use the [System.Windows.Controls.WebBrowser](/dotnet/api/system.windows.controls.webbrowser) when it detects that the process is running as administrator.

> [!NOTE]
> If you have feedback about this control, create a new issue in the [Microsoft.Toolkit.Win32 repo](https://github.com/windows-toolkit/Microsoft.Toolkit.Win32/issues) and leave your comments there.

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://WPFandWinFormsControls?sample=WebViewCompatible)

## About WebViewCompatible control

The WPF version of this control is located in the **Microsoft.Toolkit.Wpf.UI.Controls** namespace. The Windows Forms version is coming soon, and it will be located in the **Microsoft.Toolkit.Forms.UI.Controls** namespace. You can find additional related types (such as event args classes) in the **Microsoft.Toolkit.Win32.UI.Controls.Interop.WinRT** namespace.

These controls wrap an instance of the [WebViewControl](/uwp/api/windows.web.ui.interop.webviewcontrol) class, and they provide a subset of members from that class. The [WebViewControl](/uwp/api/windows.web.ui.interop.webviewcontrol) is similar to the [WebView](/uwp/api/windows.ui.xaml.controls.webview) class, but it is designed to run out of process in a desktop application (such as a WPF or Windows Forms application) and it supports a smaller set of members.  Because **WebViewCompatible** wraps [WebViewControl](/uwp/api/windows.web.ui.interop.webviewcontrol) (on Windows 10) and [WebBrowser](/dotnet/api/system.windows.controls.webbrowser) (on older versions of Windows), it provides a simpler subset of common functionality.

Unless specified otherwise in this article, the documentation for the [WebViewControl](/uwp/api/windows.web.ui.interop.webviewcontrol) class applies to the WPF and Windows Forms **WebView** controls. This article links to reference pages for the UWP [WebViewControl](/uwp/api/windows.web.ui.interop.webviewcontrol) class for more information about most members.

## Prerequisites

:heavy_check_mark: Visual Studio 2017.

:heavy_check_mark: Windows 10 Insider Preview Build 17110 or a later release for WebViewControl-based underlying implementation.

:heavy_check_mark: .NET Framework 4.6.2 or a later release.

:heavy_check_mark: Configure your application for high DPI support. To learn how, see [this section](#high-dpi) of the guide.

## Feature limitations

When compared to the UWP **WebView** control, the current release of the WPF and Windows Forms [WebView](WebView.md) controls have some limitations. For the complete list of these limitations, see [Known Issues of the WebView control for Windows Forms and WPF applications](WebView-known-issues.md).

The **WebViewCompatible** control has further limitations because it exposes a common interface that is a subset of common functionality across the two underlying implementations. On a Windows 10 computer that supports [WebViewControl](/uwp/api/windows.web.ui.interop.webviewcontrol), **WebViewCompatible** has the same limitations as [WebView](WebView.md) as well as further exclusions to the exposed functionality. On a computer running an earlier version of Windows, **WebViewCompatible** will use [WebBrowser](/dotnet/api/system.windows.controls.webbrowser) and have the same additional interface limitations.

## Add the WebViewCompatible control to the Visual Studio Toolbox for Windows Forms applications

For Visual Studio 15.8 and later:

1. Install the [Microsoft.Toolkit.Forms.UI.Controls.WebView](https://www.nuget.org/packages/Microsoft.Toolkit.Forms.UI.Controls.WebView) NuGet package.

2. Open the **Toolbox** in Visual Studio. The **WebViewCompatible** control appears in the **General** section of the **Toolbox** and you can drag it directly the designer.

For earlier versions of Visual Studio:

1. Install the [Microsoft.Toolkit.Forms.UI.Controls.WebView](https://www.nuget.org/packages/Microsoft.Toolkit.Forms.UI.Controls.WebView) NuGet package.

2. Open the **Toolbox** in Visual Studio, right-click anywhere in the toolbox, and select the **Choose Items** option.

3. In the **.NET Framework Components** tab of the **Choose Toolbox Items** dialog box, click **Browse** to locate the **Microsoft.Toolkit.Forms.UI.Controls.WebView.dll** in your [NuGet package folder](/nuget/consume-packages/managing-the-global-packages-and-cache-folders).

4. Add **Microsoft.Toolkit.Forms.UI.Controls.WebView.dll** to the list of Toolbox controls, and then close the **Choose Toolbox Items** dialog box.

   The **WebViewCompatible** control appears in the **General** section of the **Toolbox**.

   In **Solution Explorer**, the **Microsoft.Toolkit.Forms.UI.Controls.WebView** assembly appears in the **References** list.

## Add the WebViewCompatible control to the Visual Studio Toolbox for WPF applications

1. Install the [Microsoft.Toolkit.Wpf.UI.Controls.WebView](https://www.nuget.org/packages/Microsoft.Toolkit.Wpf.UI.Controls.WebView) NuGet package.

2. Open the **Toolbox** in Visual Studio or Blend. The **WebViewCompatible** control appears in the **Windows Community Toolkit** section of the **Toolbox** and you can drag it directly the designer. You can also create an instance of the **WebViewCompatible** control in code, but we recommend that you do not add **WebViewCompatible** controls to popup windows because support for that scenario will soon be disabled for security reasons.

<a id="high-dpi" />

## Enable the WebViewCompatible control to appear properly on high DPI displays

If users open your application on displays that have a high DPI displays, your **WebViewCompatible** won't appear at the proper scale unless you configure your application first.

### Configure a Windows Forms application

For guidance, see [Configuring your Windows Forms app for high DPI support](/dotnet/framework/winforms/high-dpi-support-in-windows-forms#configuring-your-windows-forms-app-for-high-dpi-support).

### Configure a WPF application

Add the following XML to your application manifest file:

```xaml
<compatibility xmlns="urn:schemas-microsoft-com:compatibility.v1">
    <application>
      <!-- Windows 10 -->
      <supportedOS Id="{8e0f7a12-bfb3-4fe8-b9a5-48fd50a15a9a}" />
    </application>
  </compatibility>
```

Add the following XML to your application configuration file:

```xaml
<application xmlns="urn:schemas-microsoft-com:asm.v3">
   <windowsSettings>
     <!-- The combination of below two tags have the following effect :
     1) Per-Monitor for >= Windows 10 Anniversary Update
     2) System < Windows 10 Anniversary Update -->
     <dpiAwareness xmlns="https://schemas.microsoft.com/SMI/2016/WindowsSettings">PerMonitor</dpiAwareness>
     <dpiAware xmlns="https://schemas.microsoft.com/SMI/2005/WindowsSettings">true/PM</dpiAware>
   </windowsSettings>
 </application>
```

## Modify the appearance of a WebViewCompatible instance

To constrain the display area, set the `Width` and `Height` properties.

This table contains links to each of these members.

| Member | Windows Forms WebView | WPF WebView |
|-------|-------------|---|
|Width property |[Width](/dotnet/api/system.windows.forms.control.width)|[Width](/dotnet/api/system.windows.frameworkelement.width)|
|Height property|[Height](/dotnet/api/system.windows.forms.control.height)|[Height](/dotnet/api/system.windows.frameworkelement.height)|

## Navigate to content

The **WebViewCompatible** control has several APIs for basic navigation:  [GoBack](/uwp/api/windows.web.ui.interop.webviewcontrol.goback), [GoForward](/uwp/api/windows.web.ui.interop.webviewcontrol.goforward), [Stop](/uwp/api/windows.web.ui.interop.webviewcontrol.stop), [Refresh](/uwp/api/windows.web.ui.interop.webviewcontrol.refresh), [CanGoBack](/uwp/api/windows.web.ui.interop.webviewcontrol.cangoback), and [CanGoForward](/uwp/api/windows.web.ui.interop.webviewcontrol.cangoforward). You can use these to add typical web browsing capabilities to your app.

To set the initial content of the **WebViewCompatible** control, you can set the [Source](/uwp/api/windows.web.ui.interop.webviewcontrol.source) property in code, XAML, or in the **Properties** window. You can also use the **Navigate** methods to load content in code. Here's an example.

```csharp
webViewCompatible1.Navigate("https://www.contoso.com");
```

```vb
webViewCompatible1.Navigate("https://www.contoso.com")
```

## Respond to navigation events

The **WebView** control provides several events that you can use to respond to navigation and content loading states. The events occur in the following order for the root web view content:

1. [NavigationStarting](/uwp/api/windows.web.ui.interop.webviewcontrol.navigationstarting)

2. [ContentLoading](/uwp/api/windows.web.ui.interop.webviewcontrol.contentloading)

3. [NavigationCompleted](/uwp/api/windows.web.ui.interop.webviewcontrol.navigationcompleted)

The **NavigationStarting** event is raised before the web view navigates to new content. You can cancel navigation in a handler for this event by setting the ``WebViewNavigationStartingEventArgs.Cancel`` property to true.

```csharp
webViewCompatible1.NavigationStarting += webViewCompatible1_NavigationStarting;

private void webViewCompatible1_NavigationStarting(object sender, WebViewNavigationStartingEventArgs args)
{
    // Cancel navigation if URL is not allowed. (Implemetation of IsAllowedUri not shown.)
    if (!IsAllowedUri(args.Uri))
        args.Cancel = true;
}
```

```vb
AddHandler webViewCompatible1.NavigationStarting, AddressOf webViewCompatible1_NavigationStarting

Private Sub webViewCompatible1_NavigationStarting(sender As Object, args As WebViewControlNavigationStartingEventArgs)
    If Not IsAllowedUri(args.Uri) Then args.Cancel = True
End Sub
```

The **ContentLoading** is raised when the web view has started loading new content.

```csharp
webViewCompatible1.ContentLoading += webViewCompatible1_ContentLoading;

private void webViewCompatible1_ContentLoading(WebView sender, WebViewControlContentLoadingEventArgs args)
{
    // Show status.
    if (args.Uri != null)
    {
        statusTextBlock.Text = "Loading content for " + args.Uri.ToString();
    }
}
```

```vb
AddHandler webViewCompatible1.ContentLoading, AddressOf webViewCompatible1_ContentLoading

Private Sub webViewCompatible1_ContentLoading(sender As WebView, args As WebViewControlContentLoadingEventArgs)
    ' Show status.
    If args.Uri IsNot Nothing Then
        statusTextBlock.Text = "Loading content for " & args.Uri.ToString()
    End If
End Sub
```

The **NavigationCompleted** event is raised when the web view has finished loading the current content or if navigation has failed. To determine whether navigation has failed, check the **IsSuccess** and **WebErrorStatus** properties of the event args.

```csharp
webViewCompatible1.NavigationCompleted += webViewCompatible1_NavigationCompleted;

private void webViewCompatible1_NavigationCompleted(WebView sender, WebViewControlNavigationCompletedEventArgs args)
{
    if (args.IsSuccess == true)
    {
        statusTextBlock.Text = "Navigation to " + args.Uri.ToString() + " completed successfully.";
    }
    else
    {
        statusTextBlock.Text = "Navigation to: " + args.Uri.ToString() +
                               " failed with error " + args.WebErrorStatus.ToString();
    }
}
```

```vb
AddHandler webViewCompatible1.NavigationCompleted, AddressOf webViewCompatible1_NavigationCompleted

Private Sub webViewCompatible1_NavigationCompleted(sender As WebView, args As WebViewControlNavigationCompletedEventArgs)
    If args.IsSuccess = True Then
        statusTextBlock.Text = "Navigation to " & args.Uri.ToString() & " completed successfully."
    Else
        statusTextBlock.Text = "Navigation to: " & args.Uri.ToString() & " failed with error " + args.WebErrorStatus.ToString()
    End If
End Sub
```

## Interact with web view content

To invoke JavaScript inside the web view content, use the **InvokeScript** method. The invoked script can return only string values.

For example, if the content of a web view named `webViewCompatible1` contains a function named `myScript`, you can invoke it like this.

```csharp
string returnValue = await webViewCompatible1.InvokeScript("myScript");
```

```vb
Dim returnValue As String = Await webViewCompatible1.InvokeScript("myScript")
```

> [!NOTE]
> Unlike [WebView](WebView.md), **WebViewCompatible** does not provide an **InvokeScript** method that supports script arguments, an **InvokeScriptAsync** method, or a **ScriptNotify** event. This is because **WebViewCompatible** only provides a common subset of features that are supported on both Windows 10 and earlier versions. For more information, see [Feature limitations](#feature-limitations).

## Requirements

| Requirement   |  Value      |
|--------|--------|
| Device family | .NET 4.6.2, Windows 10 (introduced v10.0.17110.0) |
| Namespace | Windows Forms: Microsoft.Toolkit.Forms.UI.Controls <br/> WPF: Microsoft.Toolkit.Wpf.UI.Controls |
| NuGet package | Windows Forms: [Microsoft.Toolkit.Forms.UI.Controls.WebView](https://www.nuget.org/packages/Microsoft.Toolkit.Forms.UI.Controls.WebView) <br/> WPF: [Microsoft.Toolkit.Wpf.UI.Controls.WebView](https://www.nuget.org/packages/Microsoft.Toolkit.Wpf.UI.Controls.WebView) |

## API

* [WebViewCompatible (Windows Forms)](https://github.com/windows-toolkit/Microsoft.Toolkit.Win32/tree/rel/6.1.2/Microsoft.Toolkit.Forms.UI.Controls.WebView)
* [WebViewCompatible (WPF)](https://github.com/windows-toolkit/Microsoft.Toolkit.Win32/tree/rel/6.1.2/Microsoft.Toolkit.Wpf.UI.Controls.WebView)
