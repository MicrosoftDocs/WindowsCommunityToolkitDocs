---
title: DropShadowPanel
author: nmetulev
description: The DropShadowPanel Control allows the creation of a drop shadow effect for any Xaml FrameworkElement in the markup.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, DropShadowPanel, DropShadow, xaml Control, xaml
dev_langs:
  - csharp
  - vb
---

# DropShadowPanel

> [!WARNING]
> This control has been deprecated in the Windows Community Toolkit and will be removed in a future release. Please use the new [Attached Shadow](../Helpers/AttachedShadows.md) helpers instead.

The [DropShadowPanel](/dotnet/api/microsoft.toolkit.uwp.ui.controls.dropshadowpanel) control allows the creation of a drop shadow effect for any Xaml FrameworkElement in the markup.

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://Controls?sample=DropShadowPanel)

## Syntax

```xaml
<Page ...
     xmlns:controls="using:Microsoft.Toolkit.Uwp.UI.Controls"/>

<controls:DropShadowPanel BlurRadius="4.0" ShadowOpacity="0.70"
                          OffsetX="5.0" OffsetY="5.0" Color="Black">
    <Image Width="200" Source="Unicorn.png" Stretch="Uniform"/>
</controls:DropShadowPanel>
```

## Sample Output

![DropShadowPanel animation](../resources/images/Controls/DropShadowPanel.png)

## Properties

| Property | Type | Description |
| -- | -- | -- |
| BlurRadius | double | Gets or sets the blur radius of the drop shadow |
| Color | Color | Gets or sets the color of the drop shadow |
| IsSupported | bool | Gets a value indicating whether the platform supports drop shadows |
| OffsetX | double | Gets or sets the x offset of the drop shadow |
| OffsetY | double | Gets or sets the y offset of the drop shadow |
| OffsetZ | double | Gets or sets the z offset of the drop shadow |
| ShadowOpacity | double | Gets or sets the opacity of the drop shadow |

## Examples

- Use IsSupported property to verify the availability of drop shadow and take necessary action if not available

    ```csharp
    if(!DropShadowPanel.IsSupported)
    {
        // Change something to counter the lack of drop shadow
    }
    ```

    ```vb
    If Not DropShadowPanel.IsSupported Then
        ' Change something to counter the lack of drop shadow
    End If
    ```

## Sample Project

[DropShadowPanel Sample Page Source](https://github.com/CommunityToolkit/WindowsCommunityToolkit/tree/rel/7.1.0/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/Shadows). You can [see this in action](uwpct://Controls?sample=DropShadowPanel) in the [Windows Community Toolkit Sample App](https://aka.ms/windowstoolkitapp).

## Default Template

[DropShadowPanel XAML File](https://github.com/CommunityToolkit/WindowsCommunityToolkit/blob/rel/7.1.0/Microsoft.Toolkit.Uwp.UI.Controls.Core/DropShadowPanel/DropShadowPanel.xaml) is the XAML template used in the toolkit for the default styling.

## Requirements

| Device family | Universal, 10.0.16299.0 or higher |
| -- | -- |
| Namespace | Microsoft.Toolkit.Uwp.UI.Controls |
| NuGet package | [Microsoft.Toolkit.Uwp.UI.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI.Controls/) |

## API

- [DropShadowPanel source code](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.1.0/Microsoft.Toolkit.Uwp.UI.Controls.Core/DropShadowPanel)
