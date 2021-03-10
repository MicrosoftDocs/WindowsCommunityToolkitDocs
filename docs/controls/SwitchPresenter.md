---
title: SwitchPresenter XAML Control
author: michael-hawker
description: A XAML ContentPresenter which can act like a switch statement for showing different UI based on a condition.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, switchpresenter, contentpresenter, visibility
dev_langs:
  - csharp
---

# SwitchPresenter XAML Control

<!-- Describe your control -->
The [SwitchPresenter](/dotnet/api/microsoft.toolkit.uwp.ui.controls.switchpresenter) control acts like a switch statement for XAML. It allows a developer to display certain content based on the condition of another value as an alternative to managing multiple Visibility values or complex visual states.

Unlike traditional approaches of showing/hiding components within a page, the `SwitchPresenter` will only load and attach the matching Case's content to the Visual Tree.

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://controls?sample=SwitchPresenter)

## Example

```xaml
    <controls:SwitchPresenter Value="{Binding SelectedItem, ElementName=Lookup}">
      <controls:Case Value="Confirmation Code">
        <StackPanel>
          <TextBox Name="ConfirmationCodeValidator"
                   ui:TextBoxExtensions.Regex="^[a-zA-Z]{6}$"
                   Header="Confirmation code"
                   PlaceholderText="6 letters" />
          <TextBlock Visibility="{Binding (ui:TextBoxExtensions.IsValid), ElementName=ConfirmationCodeValidator}" Text="Thanks for entering a valid code!" />
        </StackPanel>
      </controls:Case>
      <controls:Case Value="E-ticket number">
        <StackPanel>
          <TextBox Name="TicketValidator"
                   ui:TextBoxExtensions.Regex="(^\d{10}$)|(^\d{13}$)"
                   Header="E-ticket number"
                   PlaceholderText="10 or 13 numbers" />
          <TextBlock Visibility="{Binding (ui:TextBoxExtensions.IsValid), ElementName=TicketValidator}" Text="Thanks for entering a valid code!" />
        </StackPanel>
      </controls:Case>
      <controls:Case Value="Mileage Plan number">
        <TextBox Name="PlanValidator"
                 Header="Mileage Plan #"
                 PlaceholderText="Mileage Plan #" />
      </controls:Case>
      <!-- You can also provide a default case if no match is found -->
      <controls:Case IsDefault="True">
        <TextBlock Text="Please select a way to lookup your reservation above..." />
      </controls:Case>
    </controls:SwitchPresenter>
```

## Sample Project

<!-- Link to the sample page in the Windows Community Toolkit Sample App -->
[SwitchPresenter sample page Source](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.0.0/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/Primitives/SwitchPresenter.bind). You can [see this in action](uwpct://Controls?sample=SwitchPresenter) in [Windows Community Toolkit Sample App](https://aka.ms/windowstoolkitapp).

## Requirements

| Device family | Universal, MinVersion 10.0.17763 or higher   |
| -- | -- |
| Namespace | Microsoft.Toolkit.Uwp.UI.Controls |
| NuGet package | [Microsoft.Toolkit.Uwp.UI.Controls.Primitives](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI.Controls.Primitives/) |

## API

* [SwitchPresenter source code](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.0.0/Microsoft.Toolkit.Uwp.UI.Controls.Primitives/SwitchPresenter)

## Related Topics

* [ContentPresenter](/uwp/api/Windows.UI.Xaml.Controls.ContentPresenter)
* [VisualStateManager](/uwp/api/Windows.UI.Xaml.VisualStateManager)
* [Visibility](/uwp/api/windows.ui.xaml.uielement.visibility)
