---
title: Focus Behaviors
author: michael-hawker
description: Behaviors for helping focus controls in different scenarios.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, textbox, behaviors, interactivity, focus, auto focus
dev_langs:
  - csharp
---

# Focus Behaviors

The `FocusBehavior` and `AutoFocusBehavior` help control focus flow within your application.

> **Platform APIs:** [`AutoFocusBehavior`](/dotnet/api/microsoft.toolkit.uwp.ui.behaviors.autofocusbehavior), [`FocusBehavior`](/dotnet/api/microsoft.toolkit.uwp.ui.behaviors.focusbehavior)

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://Helpers?sample=AutoFocusBehavior)

## Example

In this example using the `AutoFocusBehavior` the button will automatically receive focus when it is loaded:

```xaml
  <Button Content="I receive the focus when loaded">
    <interactivity:Interaction.Behaviors>
      <behaviors:AutoFocusBehavior />
    </interactivity:Interaction.Behaviors>
  </Button>
```

## Sample Project

[Focus behavior sample page Source](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.1.0/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/FocusBehavior). You can [see this in action](uwpct://Helpers?sample=FocusBehavior) in [Windows Community Toolkit Sample App](https://aka.ms/windowstoolkitapp).

## Source Code

- [Focus behaviors source code](https://github.com/windows-toolkit/WindowsCommunityToolkit/blob/rel/7.1.0/Microsoft.Toolkit.Uwp.UI.Behaviors/Focus)

## Related Topics

- [XAML Behaviors](https://github.com/microsoft/XamlBehaviors/wiki)
