---
title: WebView control for Windows Forms and WPF
author: mcleanbyron
description: The Windows Community Toolkit provides a version of the UWP web view control that can be used in WPF and Windows Forms applications. This control embeds a view into your application that renders web content using the Microsoft Edge rendering engine.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, WebView, Windows Forms, WPF
dev_langs:
  - csharp
  - vb
---

# WebView control for Windows Forms and WPF

> [!NOTE]
> WebView will eventually be replaced by [WebView2](/microsoft-edge/hosting/webview2) (currently in preview). Thus, the WebView has been deprecated within the Toolkit, but we are working on conveying requirements to the WebView2 team. If you would like to give feedback directly for WebView2, you can do so [here on the Edge repository](https://github.com/MicrosoftEdge/WebViewFeedback).

The **WebView** control shows web content in your Windows Forms or WPF desktop application. This is one of several wrapped Universal Windows Platform controls that are available for Windows Forms and WPF applications. For more information, see [UWP controls in desktop applications](/windows/uwp/xaml-platform/xaml-host-controls).

![WebView example](../../resources/images/Controls/WebView/web-view-samples.png)

This control uses the Microsoft Edge rendering engine (EdgeHTML) to embed a view that renders richly formatted HTML5 content from a remote web server, dynamically generated code, or content files.

> [!NOTE]
> If you have feedback about this control, create a new issue in the [Microsoft.Toolkit.Win32 repo](https://github.com/windows-toolkit/Microsoft.Toolkit.Win32/issues) and leave your comments there. If you prefer to submit your feedback privately, you can send it to XamlIslandsFeedback@microsoft.com. Your insights and scenarios are critically important to us.

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://WPFandWinFormsControls?sample=WebView)

## About WebView controls

Here's where to find the *Windows Forms* and *Windows Presentation Foundation* (WPF) versions of the Microsoft Edge WebView control:

| | NuGet Package | Namespace |
|--------|--------| ---------|
| Windows Forms | Microsoft.Toolkit.Forms.UI.Controls.WebView | Microsoft.Toolkit.Forms.UI.Controls |
| WPF | Microsoft.Toolkit.Wpf.UI.Controls.WebView | Microsoft.Toolkit.Wpf.UI.Controls

(You can find additional related types (such as event args classes) in the **Microsoft.Toolkit.Win32.UI.Controls.Interop.WinRT** namespace.)

These controls wrap an instance of the [WebViewControl](/uwp/api/windows.web.ui.interop.webviewcontrol) class, and they provide a subset of members from that class. The [WebViewControl](/uwp/api/windows.web.ui.interop.webviewcontrol) is similar to the [WebView](/uwp/api/windows.ui.xaml.controls.webview) class, but it is designed to run out of process in a desktop application (such as a WPF or Windows Forms application) and it supports a smaller set of members.

Unless specified otherwise in this article, the documentation for the [WebViewControl](/uwp/api/windows.web.ui.interop.webviewcontrol) class applies to the WPF and Windows Forms **WebView** controls. This article links to reference pages for the UWP [WebViewControl](/uwp/api/windows.web.ui.interop.webviewcontrol) class for more information about most members.

## Prerequisites

:heavy_check_mark: Visual Studio 2017.

:heavy_check_mark: Windows 10 Insider Preview Build 17110 or a later release.

:heavy_check_mark: .NET Framework 4.6.2 or a later release.

:heavy_check_mark: Configure your application for high DPI support. To learn how, see [this section](#high-dpi) of the guide.

## Feature limitations

When compared to the UWP **WebView** control, the current release of the WPF and Windows Forms **WebView** control has some limitations. For the complete list of these limitations, see [Known Issues of the WebView control for Windows Forms and WPF applications](WebView-known-issues.md).

See also the [FAQs](#frequently-asked-questions-faqs) section below for answers to common questions when WebView for Windows Forms and WPF applications.

## Add the WebView control to the Visual Studio Toolbox for Windows Forms applications

For Visual Studio 15.8 and later:

1. Install the [Microsoft.Toolkit.Forms.UI.Controls.WebView](https://www.nuget.org/packages/Microsoft.Toolkit.Forms.UI.Controls.WebView) NuGet package.

2. Open the **Toolbox** in Visual Studio. The **WebView** control appears in the **General** section of the **Toolbox** and you can drag it directly the designer.

For earlier versions of Visual Studio:

1. Install the [Microsoft.Toolkit.Forms.UI.Controls.WebView](https://www.nuget.org/packages/Microsoft.Toolkit.Forms.UI.Controls.WebView) NuGet package.

2. Open the **Toolbox** in Visual Studio, right-click anywhere in the toolbox, and select the **Choose Items** option.

3. In the **.NET Framework Components** tab of the **Choose Toolbox Items** dialog box, click **Browse** to locate the **Microsoft.Toolkit.Forms.UI.Controls.WebView.dll** in your [NuGet package folder](/nuget/consume-packages/managing-the-global-packages-and-cache-folders).

4. Add **Microsoft.Toolkit.Forms.UI.Controls.WebView.dll** to the list of Toolbox controls, and then close the **Choose Toolbox Items** dialog box.

   The **WebView** control appears in the **General** section of the **Toolbox**.

   In **Solution Explorer**, the **Microsoft.Toolkit.Forms.UI.Controls.WebView** assembly appears in the **References** list.

## Add the WebView control to the Visual Studio Toolbox for WPF applications

1. Install the [Microsoft.Toolkit.Wpf.UI.Controls.WebView](https://www.nuget.org/packages/Microsoft.Toolkit.Wpf.UI.Controls.WebView) NuGet package.

2. Open the **Toolbox** in Visual Studio or Blend. The **WebView** control appears in the **Windows Community Toolkit** section of the **Toolbox** and you can drag it directly the designer. You can also create an instance of the **WebView** control in code, but we recommend that you do not add **WebView** controls to popup windows because support for that scenario will soon be disabled for security reasons.

<a id="high-dpi" />

## Enable the WebView control to appear properly on high DPI displays

If users open your application on displays that have a high Dots Per Inch (DPI) displays, your WebView won't appear at the proper scale unless you configure your application first.

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

## Modify the appearance of a WebView

To constrain the display area, set the `Width` and `Height` properties.

This table contains links to each of these members.

| Member | Windows Forms WebView | WPF WebView |
|-------|-------------|---|
|Width property |[Width](/dotnet/api/system.windows.forms.control.width)|[Width](/dotnet/api/system.windows.frameworkelement.width)|
|Height property|[Height](/dotnet/api/system.windows.forms.control.height)|[Height](/dotnet/api/system.windows.frameworkelement.height)|

## Get the web page title

You can get the title of the HTML document currently displayed in the **WebView** by using the [DocumentTitle](/uwp/api/windows.web.ui.interop.webviewcontrol.documenttitle) property.

## Input events and tab order

You can use the [InvokeScriptAsync](/uwp/api/windows.web.ui.interop.webviewcontrol.invokescriptasync) method with the JavaScript **eval** function to use the HTML event handlers, and use **window.external.notify** from the HTML event handlers to notify the application using the [ScriptNotify](/uwp/api/windows.web.ui.interop.webviewcontrol.scriptnotify) event.

## Navigate to content

The **WebView** control has several APIs for basic navigation:  [GoBack](/uwp/api/windows.web.ui.interop.webviewcontrol.goback), [GoForward](/uwp/api/windows.web.ui.interop.webviewcontrol.goforward), [Stop](/uwp/api/windows.web.ui.interop.webviewcontrol.stop), [Refresh](/uwp/api/windows.web.ui.interop.webviewcontrol.refresh), [CanGoBack](/uwp/api/windows.web.ui.interop.webviewcontrol.cangoback), and [CanGoForward](/uwp/api/windows.web.ui.interop.webviewcontrol.cangoforward). You can use these to add typical web browsing capabilities to your app.

To set the initial content of the the **WebView** control, you can set the [Source](/uwp/api/windows.web.ui.interop.webviewcontrol.source) property in code, XAML, or in the **Properties** window. You can also use the **Navigate** methods to load content in code. Here's an example.

```csharp
private void WebView_Loaded(object sender, RoutedEventArgs e)
{
    webView1.Navigate("https://www.contoso.com");
}
```

```vb
webView1.Navigate("https://www.contoso.com")
```

> [!IMPORTANT]
> If calling `Navigate()` in code, you must wait until the control has loaded for the operation to complete successfully.

## Respond to navigation events

The **WebView** control provides several events that you can use to respond to navigation and content loading states. The events occur in the following order for the root web view content:

1. [NavigationStarting](/uwp/api/windows.web.ui.interop.webviewcontrol.navigationstarting)

2. [ContentLoading](/uwp/api/windows.web.ui.interop.webviewcontrol.contentloading)

3. [DOMContentLoaded](/uwp/api/windows.web.ui.interop.webviewcontrol.domcontentloaded)

4. [NavigationCompleted](/uwp/api/windows.web.ui.interop.webviewcontrol.navigationcompleted)

The **NavigationStarting** event is raised before the web view navigates to new content. You can cancel navigation in a handler for this event by setting the ``WebViewNavigationStartingEventArgs.Cancel`` property to true.

```csharp
webView1.NavigationStarting += webView1_NavigationStarting;

private void webView1_NavigationStarting(object sender, WebViewControlNavigationStartingEventArgs args)
{
    // Cancel navigation if URL is not allowed. (Implemetation of IsAllowedUri not shown.)
    if (!IsAllowedUri(args.Uri))
        args.Cancel = true;
}
```

```vb
Imports Microsoft.Toolkit.Win32.UI.Controls.Interop.WinRT

AddHandler webView1.NavigationStarting, AddressOf webView1_NavigationStarting

Private Sub webView1_NavigationStarting(ByVal sender As Object, ByVal args As WebViewControlNavigationStartingEventArgs)
    ' Cancel navigation if URL is not allowed. (Implemetation of IsAllowedUri not shown.)
    If Not IsAllowedUri(args.Uri) Then args.Cancel = True
End Sub
```

The **ContentLoading** is raised when the web view has started loading new content.

```csharp
webView1.ContentLoading += webView1_ContentLoading;

private void webView1_ContentLoading(WebView sender, WebViewControlContentLoadingEventArgs args)
{
    // Show status.
    if (args.Uri != null)
    {
        statusTextBlock.Text = "Loading content for " + args.Uri.ToString();
    }
}
```

```vb
Imports Microsoft.Toolkit.Wpf.UI.Controls

AddHandler webView1.ContentLoading, AddressOf webView1_ContentLoading

Private Sub webView1_ContentLoading(ByVal sender As WebView, ByVal args As WebViewControlContentLoadingEventArgs)
    If args.Uri IsNot Nothing Then
        statusTextBlock.Text = "Loading content for " & args.Uri.ToString()
    End If
End Sub
```

The **DOMContentLoaded** event is raised when the web view has finished parsing the current HTML content.

```csharp
webView1.DOMContentLoaded += webView1_DOMContentLoaded;

private void webView1_DOMContentLoaded(WebView sender, WebViewControlDOMContentLoadedEventArgs args)
{
    // Show status.
    if (args.Uri != null)
    {
        statusTextBlock.Text = "Content for " + args.Uri.ToString() + " has finished loading";
    }
}
```

```vb
AddHandler webView1.DOMContentLoaded, AddressOf webView1_DOMContentLoaded

Private Sub webView1_DOMContentLoaded(ByVal sender As WebView, ByVal args As WebViewControlDOMContentLoadedEventArgs)
    If args.Uri IsNot Nothing Then
        statusTextBlock.Text = "Content for " & args.Uri.ToString() & " has finished loading"
    End If
End Sub
```

The **NavigationCompleted** event is raised when the web view has finished loading the current content or if navigation has failed. To determine whether navigation has failed, check the **IsSuccess** and **WebErrorStatus** properties of the event args.

```csharp
webView1.NavigationCompleted += webView1_NavigationCompleted;

private void webView1_NavigationCompleted(WebView sender, WebViewControlNavigationCompletedEventArgs args)
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
AddHandler webView1.NavigationCompleted, AddressOf webView1_NavigationCompleted

Private Sub webView1_NavigationCompleted(ByVal sender As WebView, ByVal args As WebViewControlNavigationCompletedEventArgs)
    If args.IsSuccess = True Then
        statusTextBlock.Text = "Navigation to " & args.Uri.ToString() & " completed successfully."
    Else
        statusTextBlock.Text = "Navigation to: " & args.Uri.ToString() & " failed with error " + args.WebErrorStatus.ToString()
    End If
End Sub
```

Similar events occur in the same order for each **iframe** in the web view content:

1. The [FrameNavigationStarting](/uwp/api/windows.web.ui.interop.webviewcontrol.framenavigationstarting) event is raised before a frame in the web view navigates to new content.

2. The [FrameContentLoading](/uwp/api/windows.web.ui.interop.webviewcontrol.framecontentloading) event is raised when a frame in the web view has started loading new content.

3. The [FrameDOMContentLoaded](/uwp/api/windows.web.ui.interop.webviewcontrol.framedomcontentloaded) event is raised when a frame in the web view has finished parsing its current HTML content.

4. The [FrameNavigationCompleted](/uwp/api/windows.web.ui.interop.webviewcontrol.framenavigationcompleted) event is raised when a frame in the web view has finished loading its content.

## Respond to potential problems

You can respond to potential problems with the content such as long running scripts, content that the **WebView** control can't load, and warnings of unsafe content.

Your app might appear unresponsive while scripts are running. The [LongRunningScriptDetected](/uwp/api/windows.web.ui.interop.webviewcontrol.longrunningscriptdetected) event is raised periodically while the web view executes JavaScript. This provides you with an opportunity to interrupt the script. To determine how long the script has been running, check the [ExecutionTime](/uwp/api/windows.web.ui.webviewcontrollongrunningscriptdetectedeventargs.executiontime) property of the [WebViewControlLongRunningScriptDetectedEventArgs](/uwp/api/windows.web.ui.webviewcontrollongrunningscriptdetectedeventargs). To halt the script, set the event args [StopPageScriptExecution](/uwp/api/windows.web.ui.webviewcontrollongrunningscriptdetectedeventargs.stoppagescriptexecution) property to **true**. The halted script will not execute again unless it is reloaded during a subsequent web view navigation.
<!-- Not able to get the event to fire without causing the application to go unresponsive -->

The web view control cannot host arbitrary file types. When an attempt is made to load content that the web view can't host, the [UnviewableContentIdentified](/uwp/api/windows.web.ui.interop.webviewcontrol.unviewablecontentidentified) event occurs. You can handle this event and notify the user.

Similarly, the [UnsupportedUriSchemeIdentified](/uwp/api/windows.web.ui.interop.webviewcontrol.unsupportedurischemeidentified) event occurs when a URI scheme that's not supported is invoked in the web content, such as fbconnect:// or mailto://. You can handle this event to provide custom behavior instead of allowing the default system launcher to launch the URI.

The [UnsafeContentWarningDisplayingEvent](/uwp/api/windows.web.ui.interop.webviewcontrol.unsafecontentwarningdisplaying) event occurs when the web view shows a warning page for content that was reported as unsafe by the SmartScreen Filter. If the user chooses to continue the navigation, subsequent navigation to the page will not display the warning nor fire the event.

## Handle special cases for web view content

You can use the [ContainsFullScreenElement](/uwp/api/windows.web.ui.interop.webviewcontrol.containsfullscreenelement) property and [ContainsFullScreenElementChanged](/uwp/api/windows.web.ui.interop.webviewcontrol.containsfullscreenelementchanged) event to detect, respond to, and enable full-screen experiences in web content, such as full-screen video playback.

For example, you might use the **ContainsFullScreenElementChanged** event to resize the web view to occupy the entire app view, or, as the following example illustrates, put a windowed app in full screen mode.

```csharp
// Assume webView is defined in XAML
webView.ContainsFullScreenElementChanged += webView_ContainsFullScreenElementChanged;

private void webView_ContainsFullScreenElementChanged(object sender, object args)
{
    var webview = sender as WebView;
    var applicationView = ApplicationView.GetForCurrentView();

    if (webview.ContainsFullScreenElement)
    {
        applicationView.TryEnterFullScreenMode();
    }
    else if (applicationView.IsFullScreenMode)
    {
        applicationView.ExitFullScreenMode();
    }
}
```

```vb
' Assume webView1 is defined in XAML
AddHandler webView1.ContainsFullScreenElementChanged, AddressOf webView1_ContainsFullScreenElementChanged

Private Sub webView_ContainsFullScreenElementChanged(ByVal sender As Object, ByVal args As Object)
    Dim webview = TryCast(sender, WebView)
    Dim applicationView = ApplicationView.GetForCurrentView()

    If webview.ContainsFullScreenElement Then
        applicationView.TryEnterFullScreenMode()
    ElseIf applicationView.IsFullScreenMode Then
        applicationView.ExitFullScreenMode()
    End If
End Sub
```

You can use the [NewWindowRequested](/uwp/api/windows.web.ui.interop.webviewcontrol.newwindowrequested) event to handle cases where hosted web content requests a new window, such as a popup window. You can use another **WebView** control to display the contents of the requested window.
<!-- Cannot get this event to fire -->

Handle the [PermissionRequested](/uwp/api/windows.web.ui.interop.webviewcontrol.permissionrequested) event to enable web features that require special capabilities. These currently include geolocation, IndexedDB storage, and user audio and video (for example, from a microphone or webcam).

<!-- This behaves differently than UWP: The sandbox process Win32WebViewHost.exe is a system application and has all capabilities listed in its manifest. Since WinForms/WPF do not have their own identities, they use the identity and permissions of the sandbox application.
The PermissionRequested event is fired when a permission is reqested each time. If the application is the first to request permissions from the sandbox, the user will receive two prompts: one from the application, one from the system for the sandbox. -->

In addition to the app handling the [PermissionRequested](/uwp/api/windows.web.ui.interop.webviewcontrol.permissionrequested) event, the user will have to approve standard system dialogs for apps requesting location or media capabilities in order for these features to be enabled.

Here is an example of how an app would enable geolocation in a map from Bing:

```csharp
// Assume webView is defined in XAML
webView.PermissionRequested += webView_PermissionRequested;

private void webView_PermissionRequested(WebView sender, WebViewControlPermissionRequestedEventArgs args)
{
    if (args.PermissionRequest.PermissionType == WebViewControlPermissionType.Geolocation &&
        args.PermissionRequest.Uri.Host == "www.bing.com")
    {
        args.PermissionRequest.Allow();
    }
}
```

```vb
AddHandler webView1.PermissionRequested, AddressOf webView1_PermissionRequested

Private Sub webView1_PermissionRequested(ByVal sender As WebView, ByVal args As WebViewControlPermissionRequestedEventArgs)
    If args.PermissionRequest.PermissionType = WebViewControlPermissionType.Geolocation AndAlso args.PermissionRequest.Uri.Host = "www.bing.com" Then
        args.PermissionRequest.Allow()
    End If
End Sub
```

If your app requires user input or other asynchronous operations to respond to a permission request, use the [Defer](/uwp/api/windows.web.ui.webviewcontrolpermissionrequest.defer) method of [WebViewControlPermissionRequest](/uwp/api/windows.web.ui.webviewcontrolpermissionrequest) to create a [WebViewControlDeferredPermissionRequest](/uwp/api/windows.web.ui.webviewcontroldeferredpermissionrequest) that can be acted upon at a later time.

## Interact with web view content

You can interact with the content of the web view by using the [InvokeScriptAsync](/uwp/api/windows.web.ui.interop.webviewcontrol.invokescriptasync) method to invoke or inject script into the web view content, and the [ScriptNotify](/uwp/api/windows.web.ui.interop.webviewcontrol.scriptnotify) event to get information back from the web view content.

To invoke JavaScript inside the web view content, use the [InvokeScriptAsync](/uwp/api/windows.web.ui.interop.webviewcontrol.invokescriptasync) method. The invoked script can return only string values.

For example, if the content of a web view named `webView1` contains a function named `setDate` that takes 3 parameters, you can invoke it like this.

```csharp
string[] args = {"January", "1", "2000"};
string returnValue = await webView1.InvokeScriptAsync("setDate", args);
```

```vb
Dim args As String() = {"January", "1", "2000"}
Dim returnValue As String = Await webView1.InvokeScriptAsync("setDate", args)
```

You can use **InvokeScriptAsync** with the JavaScript **eval** function to inject content into the web page.

Here, the text of a XAML text box (`nameTextBox.Text`) is written to a div in an HTML page hosted in `webView1`.

```csharp
private async void Button_Click(object sender, RoutedEventArgs e)
{
    string functionString = String.Format("document.getElementById('nameDiv').innerText = 'Hello, {0}';", nameTextBox.Text);
    await webView1.InvokeScriptAsync("eval", new string[] { functionString });
}
```

```vb
Private Async Sub Button_Click(sender As Object, e As RoutedEventArgs)
    Dim functionString As String = String.Format("document.getElementById('nameDiv').innerText = 'Hello, {0}';", nameTextBox.Text)
    Await webView1.InvokeScriptAsync("eval", New String() {functionString})
End Sub
```

Scripts in the web view content can use **window.external.notify** with a string parameter to send information back to your app. To receive these messages, handle the [ScriptNotify](/uwp/api/windows.web.ui.interop.webviewcontrol.scriptnotify) event.

## Options for web content hosting

You can use the [Settings](/uwp/api/windows.web.ui.webviewcontrolsettings) property (of type [WebViewControlSettings](/uwp/api/windows.web.ui.webviewcontrolsettings) to control whether JavaScript and IndexedDB are enabled. For example, if you use a web view to display strictly static content, you might want to disable JavaScript for best performance.

## Creating multiple web views in the same process

By default, the **WebView** is hosted outside of your application's process in a process called WWAHost. When using the designer or default constructor, each new **WebView** is created in a new WWAHost instance, with its own copy of state. To share session cookies and state, consider using the same WWAHost process to host your **WebView**.

### For Windows Forms Applications

For example, if through the designer a **WebView** named `webView1` is on `Form1`, you can create a new **WebView** that shares the same process and state with `webView1` like this.

```csharp
public partial class Form1 : Form
{
    private WebView webView2;

    public Form1()
    {
        InitializeComponent();

        // Assume webView1 created through the designer
        webView2 = new WebView(webView1.Process);
        ((ISupportInitialize)webView).BeginInit();
        // ... other initialization code
        ((ISupportInitialize)webView).EndInit();
    }
}
```

```vb
Private Class Form1

    Private webView2 As WebView

    Public Sub New()
        InitializeComponent()

        ' Assume webView1 created through the designer
        webView2 = New WebView(webView1.Process)
        (CType(webView, ISupportInitialize)).BeginInit()
        ' ... other initialization code
        (CType(webView, ISupportInitialize)).EndInit()
    End Sub
End Class
```

### For WPF Applications

Similar to the Windows Forms example, if through the designer a **WebView** is created named `WebView1` on the `Window`, you can create a new **WebView** that shares the same process and state with `WebView1` like this.

MainWindow.xaml

```xaml
<Window
    xmlns="https://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="https://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:d="https://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="https://schemas.openxmlformats.org/markup-compatibility/2006"
    xmlns:WPF="clr-namespace:Microsoft.Toolkit.Wpf.UI.Controls;assembly=Microsoft.Toolkit.Wpf.UI.Controls.WebView"
    Title="MainWindow"
    Width="800"
    Height="450"
    mc:Ignorable="d">
    <Grid x:Name="Grid1" Grid.Row="1">
        <Grid.ColumnDefinitions>
            <ColumnDefinition />
            <ColumnDefinition />
        </Grid.ColumnDefinitions>

         <WPF:WebView x:Name="WebView1"
                      Grid.Row="0"
                      Grid.Column="0"
                      Loaded="WebView_Loaded" />
    </Grid>
</Window>
```

MainWindow.xaml.cs

```csharp
public partial class MainWindow : Window
{
    public MainWindow()
    {
        InitializeComponent();
    }

    private void WebView_Loaded(object sender, RoutedEventArgs e)
    {
        var webView2 = new WebView(WebView1.Process);
        webView2.BeginInit();
        webView2.EndInit();

        Grid.SetRow(webView2, 0);
        Grid.SetColumn(webView2, 1);

        Grid1.Children.Add(webView2);
    }
}
```

MainWindow.xaml.vb

```vb
Class MainWindow
    Private Sub WebView_Loaded(sender As Object, e As RoutedEventArgs)
        Dim webView2 = New WebView(webView1.Process)
        webView2.BeginInit()
        webView2.EndInit()

        Grid.SetRow(webView2, 0)
        Grid.SetColumn(webView2, 1)

        Grid1.Children.Add(webView2)
    End Sub
End Class
```

## Frequently Asked Questions (FAQs)

### There’s *WebBrowser*, *WebView*, and *WebViewControl*. What’s the difference?

When people refer to a “web view” they either refer to the [WebBrowser](/dotnet/api/system.windows.controls.webbrowser) control in .NET, which uses the legacy Internet Explorer "Trident" (MSHTML) engine, the Universal Windows Platform (UWP) [WebView](/uwp/api/windows.ui.xaml.controls.webview ) which uses the Microsoft Edge (EdgeHTML) engine on some versions of Windows and Trident on others, or the [WebViewControl](/uwp/api/windows.web.ui.interop.webviewcontrol), which is a subset of the UWP WebView available for use in Windows Forms, WPF and other desktop (Win32) applications.

### Is *WebViewControl* available on Windows Server?

No. [Long-Term Servicing Channel (LTSC)](/windows/deployment/update/waas-overview#long-term-servicing-channel) versions of Windows, including *Windows Server*, don't include Microsoft Edge or many other UWP applications. These apps and their required services are frequently updated with new functionality and cannot be supported on systems running a LTSC operating system.

A future workaround might be to use [Windows Virtual Desktop](https://azure.microsoft.com/services/virtual-desktop/) to run your WebViewControl application through a virtualized desktop on Windows 7, Windows 10 LTSC versions, and other environments where Microsoft Edge (and the WebViewControl) wouldn't otherwise be supported.

### Are there samples?

Yes! Samples are available for Windows Forms, Windows Presentation Foundation, and C++ here:
<https://github.com/rjmurillo/webview-samples>

### Can I simply swap out the Internet Explorer *WebBrowser* for Microsoft Edge *WebViewControl* in my application?

No, the APIs differ significantly, as the *WebViewControl* represents several generations of browser development since the IE *WebBrowser* control was released.

### Can I inject native objects into my WebViewControl content?

No. Neither the WebBrower (Internet Explorer) [ObjectForScripting](https://msdn.microsoft.com/library/system.windows.controls.webbrowser.objectforscripting.aspx) property nor the WebView (UWP) [AddWebAllowedObject](/uwp/api/windows.ui.xaml.controls.webview.addweballowedobject) method are supported in WebViewControl. As a workaround, you can use `window.external.notify`/ `ScriptNotify` and JavaScript execution to communicate between the layers, for example: <https://github.com/rjmurillo/WebView_AddAllowedWebObjectWorkaround>

### Can I host the UWP WebView in WPF or Windows Forms using XAML islands?

No. It is not possible to host the (full-featured) UWP WebView using XAML islands due to architectural and security constraints. The WebViewControl provided by Windows Community Toolkit is the recommended way of hosting a modern WebView control in desktop applications.

### How do I debug WebViewControl?

To debug WebViewControl, download and install the standalone [Microsoft Edge DevTools Preview](https://www.microsoft.com/store/productId/9MZBFRMZ0MNJ) app from the Microsoft Store. Once launched, the [*Local*](/microsoft-edge/devtools-guide#microsoft-store-app) panel of the chooser will display all active EdgeHTML content processes, including open Edge browser tabs, Windows 10 web apps (WWAHost.exe processes), and webview controls.

## Sample Project

You can [see this in action](uwpct://WPFandWinFormsControls?sample=WebView) in the [Windows Community Toolkit Sample App](https://aka.ms/windowstoolkitapp).

## Requirements

| Requirement   |  Value      |
|--------|--------|
| Device family | .NET 4.6.2, Windows 10 (introduced v10.0.17110.0) |
| Namespace | Windows Forms: Microsoft.Toolkit.Forms.UI.Controls <br/> WPF: Microsoft.Toolkit.Wpf.UI.Controls |
| NuGet package | Windows Forms: [Microsoft.Toolkit.Forms.UI.Controls.WebView](https://www.nuget.org/packages/Microsoft.Toolkit.Forms.UI.Controls.WebView) <br/> WPF: [Microsoft.Toolkit.Wpf.UI.Controls.WebView](https://www.nuget.org/packages/Microsoft.Toolkit.Wpf.UI.Controls.WebView) |

## API

- [WebView (Windows Forms)](https://github.com/windows-toolkit/Microsoft.Toolkit.Win32/tree/rel/6.1.2/Microsoft.Toolkit.Forms.UI.Controls.WebView)
- [WebView (WPF)](https://github.com/windows-toolkit/Microsoft.Toolkit.Win32/tree/rel/6.1.2/Microsoft.Toolkit.Wpf.UI.Controls.WebView)
