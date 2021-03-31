---
title: WindowsXAMLHost control
author: mcleanbyron
description: This guide helps you add UWP XAML controls to your WPF.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, host controls, xaml islands, WPF, Windows Forms
dev_langs:
  - csharp
  - vb
---

# WindowsXamlHost control for Windows Forms and WPF

You can use the **WindowsXamlHost** control to add any Universal Windows Platform (UWP) control to your WPF or Windows Forms desktop application, including:

* Any first-party UWP control provided by the Windows SDK or WinUI library.
* Any custom UWP control. You must have the source code for the custom control so you can compile it with your application.
    > [!IMPORTANT]
    > Using the WindowsXamlHost control to host custom UWP controls is supported only in apps that target .NET Core 3. This scenario is not supported in apps that target the .NET Framework.

This is a general-purpose control for hosting *XAML Islands* in your WPF or Windows Forms application. For certain features such as Ink, maps, and playing media content, you might prefer to use other wrapped controls provided by the Windows Community Toolkit that have a simpler development experience. For more information, see [Host UWP XAML controls in desktop apps (XAML Islands)](/windows/apps/desktop/modernize/xaml-islands).

> [!NOTE]
> This control is currently available as a developer preview for Windows 10, version 1903, and later. Although we encourage you to try out this control in your own prototype code now, we do not recommend that you use it in production code at this time. For more information, see the [XAML Islands feature roadmap](/windows/uwp/xaml-platform/xaml-host-controls#feature-roadmap). If you have feedback about this control, create a new issue in the [Microsoft.Toolkit.Win32 repo](https://github.com/windows-toolkit/Microsoft.Toolkit.Win32/issues) and leave your comments there. If you prefer to submit your feedback privately, you can send it to XamlIslandsFeedback@microsoft.com.

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://WPFandWinFormsControls?sample=WindowsXamlHost)

## Known issues and limitations

See our list of [known issues](https://github.com/windows-toolkit/Microsoft.Toolkit.Win32/issues) for WPF and Windows Forms controls in the Windows Community Toolkit repo.

## Host a custom UWP control

You can use the **WindowsXamlHost** control to host any custom UWP control. To do this, you must have the source code for the custom control so you can compile it with your application, and you must make several updates to your project. For a walkthrough that demonstrates how to do this, see [Host a custom UWP control in a WPF app using XAML Islands](/windows/apps/desktop/modernize/host-custom-control-with-xaml-islands).

## Host a first-party UWP control

The **WindowsXamlHost** control provides several ways to host a first-party control provided by the Windows SDK or WinUI library. You can configure the controls at design time or dynamically at run time.

The following sections provide general instructions. For a walkthrough that demonstrates how to use the **WindowsXamlHost** control to host a UWP [CalendarView](/windows/uwp/design/controls-and-patterns/calendar-view) control in a WPF app, see [Host a standard UWP control in a WPF app](/windows/apps/desktop/modernize/host-standard-control-with-xaml-islands).

### Set up your project

Before getting started, follow these instructions to install the necessary NuGet package in your WPF or Windows Forms project.

1. Make sure [package references](/nuget/consume-packages/package-references-in-project-files) are enabled:

    1. In Visual Studio, click **Tools -> NuGet Package Manager -> Package Manager Settings**.
    2. Make sure **PackageReference** is selected for **Default package management format**.

2. With your project open in Visual Studio, right-click your project in **Solution Explorer** and choose **Manage NuGet Packages**.

3. In the **NuGet Package Manager** window, make sure that **Include prerelease** is selected.

4. Select the **Browse** tab and search for one of the following NuGet packages depending on your application type. This package provides everything you need to use the **WindowsXamlHost** control to host a UWP control, including other related NuGet packages.

    * For a WPF application, install the [Microsoft.Toolkit.Wpf.UI.XamlHost](https://www.nuget.org/packages/Microsoft.Toolkit.Wpf.UI.XamlHost) package (version v6.0.0-preview7 or later).
    * For a Windows Forms application, install the [Microsoft.Toolkit.Forms.UI.XamlHost](https://www.nuget.org/packages/Microsoft.Toolkit.Forms.UI.XamlHost) package (version v6.0.0-preview7 or later).

### Create and host UWP controls at design time

1. In your WPF or Windows Forms project, open the window or form in which you want to host a UWP control.
2. From the **Windows Community Toolkit** section of the **Toolbox**, drag a **WindowsXamlHost** control onto the designer.
3. In the **Properties** window, set the **InitialTypeName** property of the **WindowsXamlHost** control to the fully qualified name of the UWP control that you want to host. You'll find the **InitialTypeName** property in the **XAML** section of the **Properties** window.

    **WPF**

    ![InitialTypeName property in Properties WPF](../../resources/images/Controls/WindowsXAMLHost/type-name-property-wpf.png)

    **Windows Forms**

    ![InitialTypeName property in Properties Window](../../resources/images/Controls/WindowsXAMLHost/type-name-property-windows-forms.png)

4. In the **Properties** window, double-click the **ChildChanged** field to generate an event handler.

    **WPF**

    ![WindowsXamlHost control in the toolbox - WPF](../../resources/images/Controls/WindowsXAMLHost/xaml-content-updated-event-wpf.png)

    **Windows Forms**

    ![WindowsXamlHost control in the toolbox](../../resources/images/Controls/WindowsXAMLHost/xaml-content-updated-event-windows-forms.png)

5. Initialize your UWP control by adding code to this handler. Your code can set properties and handle the events of the UWP control. Here's a basic example that sets a property and handles an event of a UWP **Button** class.

    ```csharp
    private void MyWindowsXAMLHost_ChildChanged(object sender, EventArgs e)
    {
        WindowsXamlHost windowsXamlHost = (WindowsXamlHost)sender;

        Windows.UI.Xaml.Controls.Button button =
            (Windows.UI.Xaml.Controls.Button)windowsXamlHost.Child;

        button.Content = "My UWP button";
        button.Click += Button_Click;
    }

    private void Button_Click(object sender, Windows.UI.Xaml.RoutedEventArgs e)
    {
        MessageBox.Show("My UWP button works");
    }
    ```

    ```vb
    Private Sub MyWindowsXAMLHost_ChildChanged(sender As Object, e As EventArgs)
        Dim windowsXamlHost As WindowsXamlHost = CType(sender, WindowsXamlHost)
        Dim button As Windows.UI.Xaml.Controls.Button = CType(windowsXamlHost.Child, Windows.UI.Xaml.Controls.Button)
        button.Content = "My UWP button"
        AddHandler button.Click, AddressOf Button_Click
    End Sub

    Private Sub Button_Click(sender As Object, e As Windows.UI.Xaml.RoutedEventArgs)
        MessageBox.Show("My UWP button works")
    End Sub
    ```

### Create and host UWP controls dynamically at run time

If you don't want to create and host UWP controls at design time, you can create instances of UWP controls by using the **CreateXamlContentByType** convenience method. Before you show that control in the UI of your application, you'll have to associate it with a **WindowsXamlHost** control.

Here's an example that demonstrates how to do this. This example assumes that the code is run in the context of a **Window** that contains a **StackPanel** named **MyStackPanel**.

```csharp
private void UseHelperMethod()
{
    Microsoft.Toolkit.Wpf.UI.XamlHost.WindowsXamlHost myHostControl =
        new Microsoft.Toolkit.Wpf.UI.XamlHost.WindowsXamlHost();

    // Use helper method to create a UWP control instance.
    Windows.UI.Xaml.Controls.Button myButton =
        Microsoft.Toolkit.Win32.UI.XamlHost.UWPTypeFactory.CreateXamlContentByType(
            "Windows.UI.Xaml.Controls.Button") as Windows.UI.Xaml.Controls.Button;

    // Initialize UWP control.
    myButton.Name = "button1";
    myButton.Width = 75;
    myButton.Height = 40;
    myButton.TabIndex = 0;
    myButton.Content = "button1";
    myButton.Click += MyButton_Click;

    // initialize the Windows XAML host control.
    myHostControl.Name = "myWindowsXamlHostControl";

    // Associate the Windows XAML host control with the UWP control.
    // For Windows Forms applications, you might use this.Controls.Add(myHostControl);
    myHostControl.Child = myButton;

    // Make the UWP control appear in the UI.
    this.MyStackPanel.Children.Add(myHostControl);
}

private void MyButton_Click(object sender, Windows.UI.Xaml.RoutedEventArgs e)
{
    MessageBox.Show("This is a UWP button.");
}
```

```vb
Private Sub UseHelperMethod()
    Dim myHostControl As Microsoft.Toolkit.Wpf.UI.XamlHost.WindowsXamlHost = New Microsoft.Toolkit.Wpf.UI.XamlHost.WindowsXamlHost()

    ' Use helper method to create a UWP control instance.
    Dim myButton As Windows.UI.Xaml.Controls.Button = TryCast(Microsoft.Toolkit.Win32.UI.XamlHost.UWPTypeFactory.CreateXamlContentByType("Windows.UI.Xaml.Controls.Button"), Windows.UI.Xaml.Controls.Button)

    ' Initialize UWP control.
    myButton.Name = "button1"
    myButton.Width = 75
    myButton.Height = 40
    myButton.TabIndex = 0
    myButton.Content = "button1"
    AddHandler myButton.Click, AddressOf MyButton_Click

    ' initialize the Windows XAML host control.
    myHostControl.Name = "myWindowsXamlHostControl"

    ' Associate the Windows XAML host control with the UWP control.
    ' For Windows Forms applications, you might use this.Controls.Add(myHostControl);
    myHostControl.Child = myButton

    ' Make the UWP control appear in the UI.
    Me.MyStackPanel.Children.Add(myHostControl)
End Sub

Private Sub MyButton_Click(sender As Object, e As Windows.UI.Xaml.RoutedEventArgs)
    MessageBox.Show("My UWP button works")
End Sub
```

### Initialize UWP controls first, and then assign them to WindowsXamlHost controls

In some situations, you might want to create instances of UWP controls without having to first create **WindowsXamlHost** controls.

If you choose to do this, make sure to first call the [InitializeForCurrentThread](/uwp/api/windows.ui.xaml.hosting.windowsxamlmanager.initializeforcurrentthread) method of the [WindowsXamlManager](/uwp/api/windows.ui.xaml.hosting.windowsxamlmanager) class. This initializes the UWP hosting environment so that you can create and initialize UWP controls. You can create a Windows XAML host control when you are ready to show any of those UWP controls in a UI.

The following example initializes the UWP hosting environment, creates a UWP button and then creates a Windows XAML host control only for the purpose of showing the UWP control in the UI.

```csharp
private void CreateUWPControlsFirst()
{
    // Initialize the UWP hosting environment.
    Windows.UI.Xaml.Hosting.WindowsXamlManager.InitializeForCurrentThread();

    // Create a UWP control.
    Windows.UI.Xaml.Controls.Button myButton = new Windows.UI.Xaml.Controls.Button();

    // Initialize UWP control.
    myButton.Name = "button1";
    myButton.Width = 75;
    myButton.Height = 40;
    myButton.TabIndex = 0;
    myButton.Content = "button1";
    myButton.Click += MyButton_Click;

    // Create a Windows XAML host control.
    Microsoft.Toolkit.Wpf.UI.XamlHost.WindowsXamlHost myHostControl = 
       new Microsoft.Toolkit.Wpf.UI.XamlHost.WindowsXamlHost();

    // initialize the Windows XAML host control.
    myHostControl.Name = "myWindowsXamlHostControl";

    // Associate the Windows XAML host control with the UWP control.
    myHostControl.Child = myButton;

    // Make the UWP control appear in the UI.
    // For Windows Forms applications, you might use this.Controls.Add(myHostControl);
    this.MyStackPanel.Children.Add(myHostControl);
}

private void MyButton_Click(object sender, Windows.UI.Xaml.RoutedEventArgs e)
{
    MessageBox.Show("This is a UWP button.");
}
```

```vb
Private Sub CreateUWPControlsFirst()
    ' Initialize the UWP hosting environment.
    Windows.UI.Xaml.Hosting.WindowsXamlManager.InitializeForCurrentThread()

    ' Create a UWP control.
    Dim myButton As Windows.UI.Xaml.Controls.Button = New Windows.UI.Xaml.Controls.Button()

    ' Initialize UWP control.
    myButton.Name = "button1"
    myButton.Width = 75
    myButton.Height = 40
    myButton.TabIndex = 0
    myButton.Content = "button1"
    AddHandler myButton.Click, AddressOf MyButton_Click

    ' Create a Windows XAML host control.
    Dim myHostControl As Microsoft.Toolkit.Wpf.UI.XamlHost.WindowsXamlHost = New Microsoft.Toolkit.Wpf.UI.XamlHost.WindowsXamlHost()

    ' initialize the Windows XAML host control.
    myHostControl.Name = "myWindowsXamlHostControl"

    ' Associate the Windows XAML host control with the UWP control.
    myHostControl.Child = myButton

    ' Make the UWP control appear in the UI.
    ' For Windows Forms applications, you might use this.Controls.Add(myHostControl);
    Me.MyStackPanel.Children.Add(myHostControl)
End Sub

Private Sub MyButton_Click(sender As Object, e As Windows.UI.Xaml.RoutedEventArgs)
    MessageBox.Show("My UWP button works")
End Sub
```

## Sample Project

You can [see this in action](uwpct://WPFandWinFormsControls?sample=WindowsXamlHost) in the [Windows Community Toolkit Sample App](https://aka.ms/windowstoolkitapp).

## Requirements

| Device family | .NET 4.6.2, Windows 10 (introduced v10.0.17709.0) |
|--------|--------|
| Namespace | Windows Forms: Microsoft.Toolkit.Forms.UI.XamlHost <br/> WPF: Microsoft.Toolkit.Wpf.UI.XamlHost |
| NuGet package | Windows Forms: [Microsoft.Toolkit.Forms.UI.XamlHost](https://www.nuget.org/packages/Microsoft.Toolkit.Forms.UI.XamlHost)  <br/> WPF: [Microsoft.Toolkit.Wpf.UI.XamlHost](https://www.nuget.org/packages/Microsoft.Toolkit.Wpf.UI.XamlHost) |

## API source code

* [WindowsXamlHost (Windows Forms)](https://github.com/windows-toolkit/Microsoft.Toolkit.Win32/tree/rel/6.1.2/Microsoft.Toolkit.Forms.UI.XamlHost)
* [WindowsXamlHost (WPF)](https://github.com/windows-toolkit/Microsoft.Toolkit.Win32/tree/rel/6.1.2/Microsoft.Toolkit.Wpf.UI.XamlHost)
