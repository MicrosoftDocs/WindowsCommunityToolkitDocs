---
title: Key Down Trigger Behavior
author: 
description: Add a new behavior that listens to a key press event on the associated UIElement and triggers the set of actions.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, textbox, behaviors, interactivity, KeyDownTrigger, key down trigger
dev_langs:
  - csharp
---

# Key Down Trigger Behavior

Add a new behavior that listens to a key press event on the associated UIElement and triggers the set of actions.

> **Platform APIs:** [`Behaviors`](/dotnet/api/microsoft.toolkit.uwp.ui.behaviors)

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://Helpers?sample=KeyDownTriggerBehavior)

## Example

In this example setting up the `KeyDownTriggerBehavior` to start the animation:

```xaml
  <TextBox
    PlaceholderText="Set the focus to this TextBox and press enter to trigger the animation"
    Width="500">
        <interactivity:Interaction.Behaviors>
            <behaviors:KeyDownTriggerBehavior
                Key="Enter">
                <behaviors:StartAnimationAction Animation="{Binding ElementName=MoveAnimation}" />
            </behaviors:KeyDownTriggerBehavior>
        </interactivity:Interaction.Behaviors>
    </TextBox>
```

## Sample Project

[Key Down Trigger behavior sample page Source](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/main/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/KeyDownTriggerBehavior). You can [see this in action](uwpct://Helpers?sample=KeyDownTriggerBehavior) in [Windows Community Toolkit Sample App](https://aka.ms/windowstoolkitapp).

## Source Code

- [Key Down Trigger behavior source code](https://github.com/windows-toolkit/WindowsCommunityToolkit/blob/rel/7.0.0/Microsoft.Toolkit.Uwp.UI.Behaviors/Keyboard)

## Related Topics

- [XAML Behaviors](https://github.com/microsoft/XamlBehaviors/wiki)