---
title: AutoSelect Behavior
author: jbrianceau
description: Behavior to automatically select the entire content of a TextBox control when it loads.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, textbox, behaviors, interactivity, selection
dev_langs:
  - csharp
---

# AutoSelect Behavior

The `AutoSelectBehavior` automatically selects the entire content of its associated TextBox when it is loaded.

> **Platform APIs:** [`AutoSelectBehavior`](/dotnet/api/microsoft.toolkit.uwp.ui.behaviors.autoselectbehavior)

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://Helpers?sample=AutoSelectBehavior)

## Example

In this example using the `AutoSelectBehavior` the textbox content will be automatically selected when it is loaded:

```xaml
  <TextBox Text="My content is selected when loaded">
    <interactivity:Interaction.Behaviors>
      <behaviors:AutoSelectBehavior />
    </interactivity:Interaction.Behaviors>
  </TextBox>
```

## Sample Project

[AutoSelect behavior sample page Source](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.0.1/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/AutoSelectBehavior). You can [see this in action](uwpct://Helpers?sample=AutoSelectBehavior) in [Windows Community Toolkit Sample App](https://aka.ms/windowstoolkitapp).

## Source Code

- [AutoSelect behavior source code](https://github.com/windows-toolkit/WindowsCommunityToolkit/blob/rel/7.0.1/Microsoft.Toolkit.Uwp.UI.Behaviors/Select/AutoSelectBehavior.cs)

## Related Topics

- [XAML Behaviors](https://github.com/microsoft/XamlBehaviors/wiki)
