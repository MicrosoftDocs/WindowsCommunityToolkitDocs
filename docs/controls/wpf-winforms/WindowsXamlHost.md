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
    > Using the [WindowsXamlHost](/windows/communitytoolkit/controls/wpf-winforms/windowsxamlhost) control to host custom UWP controls is supported only in apps that target .NET Core 3. This scenario is not supported in apps that target the .NET Framework.

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

For a walkthrough that demonstrates how to use the **WindowsXamlHost** control to host a UWP control in a WPF app, see [Host a standard UWP control in a WPF app](/windows/apps/desktop/modernize/host-standard-control-with-xaml-islands).

### Set up your project

Before getting started, follow these instructions to install the necessary NuGet package in your WPF or Windows Forms project.

1. Make sure [package references](/nuget/consume-packages/package-references-in-project-files) are enabled:

    1. In Visual Studio, click **Tools -> NuGet Package Manager -> Package Manager Settings**.
    2. Make sure **PackageReference** is selected for **Default package management format**.

2. With your project open in Visual Studio, right-click your project in **Solution Explorer** and choose **Manage NuGet Packages**.

3. Select the **Browse** tab and search for one of the following NuGet packages depending on your application type. This package provides everything you need to use the **WindowsXamlHost** control to host a UWP control, including other related NuGet packages.

    * For a WPF application, install the [Microsoft.Toolkit.Wpf.UI.XamlHost](https://www.nuget.org/packages/Microsoft.Toolkit.Wpf.UI.XamlHost) package (latest stable version).
    * For a Windows Forms application, install the [Microsoft.Toolkit.Forms.UI.XamlHost](https://www.nuget.org/packages/Microsoft.Toolkit.Forms.UI.XamlHost) package (latest stable version).

### Create and host UWP controls at design time

To create and host a first-party UWP control at design time, you must add a **WindowsXamlHost** control to a parent UI element (for example, a grid) in the XAML editor. Dragging a **WindowsXamlHost** from the **Toolbox** to the designer is not supported.

For a walkthrough that demonstrates how to use the **WindowsXamlHost** control to host a UWP control in a WPF app, see [Host a standard UWP control in a WPF app](/windows/apps/desktop/modernize/host-standard-control-with-xaml-islands).

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

## Sample project

You can see this in action in the [Windows Community Toolkit Sample App](https://aka.ms/windowstoolkitapp).

## Requirements

|        |        |
|--------|--------|
| Device family | .NET 4.6.2, Windows 10 (introduced v10.0.17709.0) |
| Namespace | Windows Forms: Microsoft.Toolkit.Forms.UI.XamlHost <br/> WPF: Microsoft.Toolkit.Wpf.UI.XamlHost |
| NuGet package | Windows Forms: [Microsoft.Toolkit.Forms.UI.XamlHost](https://www.nuget.org/packages/Microsoft.Toolkit.Forms.UI.XamlHost)  <br/> WPF: [Microsoft.Toolkit.Wpf.UI.XamlHost](https://www.nuget.org/packages/Microsoft.Toolkit.Wpf.UI.XamlHost) |

## API source code

* [WindowsXamlHost (Windows Forms)](https://github.com/windows-toolkit/Microsoft.Toolkit.Win32/tree/rel/6.1.2/Microsoft.Toolkit.Forms.UI.XamlHost)
* [WindowsXamlHost (WPF)](https://github.com/windows-toolkit/Microsoft.Toolkit.Win32/tree/rel/6.1.2/Microsoft.Toolkit.Wpf.UI.XamlHost)
