---
title: TabbedCommandBar XAML Control
author: yoshiask
description: TabbedCommandBar is a control for displaying multiple CommandBars in the same space, like Microsoft Office's ribbon.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, TabbedCommandBar, CommandBar, ribbon
dev_langs:
  - csharp
---

# TabbedCommandBar XAML Control
The [TabbedCommandBar](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.uwp.ui.controls.tabbedcommandbar) displays a set of [TabbedCommandBarItem](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.uwp.ui.controls.tabbedcommandbaritem) in a shared container, like Microsoft Office's ribbon.

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://Controls?sample=TabbedCommandBar)

## Syntax

```xaml
<controls:TabbedCommandBar>
  <controls:TabbedCommandBar.PaneFooter>
    <CommandBar Background="Transparent" DefaultLabelPosition="Right">
      <AppBarButton Label="Share" Icon="Share"/>
      <AppBarButton Label="Comments" Icon="Message"/>
    </CommandBar>
  </controls:TabbedCommandBar.PaneFooter>
  <controls:TabbedCommandBar.MenuItems>
    <controls:TabbedCommandBarItem Header="Home">
      <AppBarButton Icon="Undo" Label="Undo"/>
      <AppBarButton Icon="Redo" Label="Redo"/>
      <AppBarButton Icon="Paste" Label="Paste"/>
      <AppBarSeparator />
      <AppBarElementContainer>
        <SplitButton>
          <FontIcon FontFamily="{ThemeResource SymbolThemeFontFamily}" Glyph="&#xE790;" />
          <SplitButton.Flyout>
            <Flyout>
              <controls:ColorPicker Margin="-10" Color="{ThemeResource Brand-Color}"/>
            </Flyout>
          </SplitButton.Flyout>
        </SplitButton>
      </AppBarElementContainer>
      <AppBarElementContainer>
        <ComboBox SelectedIndex="0" MinWidth="175">
          <ComboBoxItem Content="Arial" />
          <ComboBoxItem Content="Calibri" />
          <ComboBoxItem Content="JetBrains Mono" />
          <ComboBoxItem Content="Roboto" />
          <ComboBoxItem Content="Sergio UI" />
          <ComboBoxItem Content="Sergio UI Semibold" />
        </ComboBox>
      </AppBarElementContainer>
      <AppBarElementContainer>
        <TextBox PlaceholderText="Size"/>
      </AppBarElementContainer>
      <AppBarToggleButton Icon="Bold" Label="Bold" />
      <AppBarToggleButton Icon="Italic" Label="Italic" />
      <AppBarToggleButton Icon="Underline" Label="Underline" />
    </controls:TabbedCommandBarItem>
    <controls:TabbedCommandBarItem Header="Insert">
      <AppBarButton Icon="Pictures" Label="Pictures">
        <AppBarButton.Flyout>
          <MenuFlyout Placement="BottomEdgeAlignedLeft">
            <MenuFlyoutItem Text="This Device">
              <MenuFlyoutItem.Icon>
                <FontIcon FontFamily="Segoe MDL2 Assets" Glyph="&#xEC4E;" />
              </MenuFlyoutItem.Icon>
            </MenuFlyoutItem>
            <MenuFlyoutItem Text="Stock Images">
              <MenuFlyoutItem.Icon>
                <FontIcon FontFamily="Segoe MDL2 Assets" Glyph="&#xE721;" />
              </MenuFlyoutItem.Icon>
            </MenuFlyoutItem>
            <MenuFlyoutItem Icon="Globe" Text="Online Pictures" />
          </MenuFlyout>
        </AppBarButton.Flyout>
      </AppBarButton>
      <AppBarButton Label="Shapes">
        <AppBarButton.Icon>
          <FontIcon FontFamily="Segoe UI Symbol" Glyph="&#x25A1;" />
        </AppBarButton.Icon>
      </AppBarButton>
      <AppBarButton Label="Icons">
        <AppBarButton.Icon>
          <FontIcon FontFamily="Segoe MDL2 Assets" Glyph="&#xED58;" />
        </AppBarButton.Icon>
      </AppBarButton>
      <AppBarButton Label="3D Models">
        <AppBarButton.Icon>
          <FontIcon FontFamily="Segoe MDL2 Assets" Glyph="&#xF158;" />
        </AppBarButton.Icon>
      </AppBarButton>
      <AppBarSeparator/>
      <AppBarButton Label="Add-ins">
        <AppBarButton.Icon>
          <FontIcon FontFamily="Segoe MDL2 Assets" Glyph="&#xECAA;" />
        </AppBarButton.Icon>
      </AppBarButton>
      <controls:TabbedCommandBarItem.SecondaryCommands>
        <AppBarButton Icon="Add" Label="New item" />
      </controls:TabbedCommandBarItem.SecondaryCommands>
    </controls:TabbedCommandBarItem>
    <controls:TabbedCommandBarItem Header="Shape Format" IsContextual="True" Visibility="{Binding ElementName=ContextualToggle, Path=IsOn}">
      <AppBarButton Label="Shape Fill">
        <AppBarButton.Icon>
          <FontIcon FontFamily="{ThemeResource SymbolThemeFontFamily}" Glyph="&#xE771;" />
        </AppBarButton.Icon>
      </AppBarButton>
      <AppBarButton Label="Shape Outline">
        <AppBarButton.Icon>
          <FontIcon FontFamily="{ThemeResource SymbolThemeFontFamily}" Glyph="&#xE76D;" />
        </AppBarButton.Icon>
      </AppBarButton>
    </controls:TabbedCommandBarItem>
  </controls:TabbedCommandBar.MenuItems>
</controls:TabbedCommandBar>
```

## Sample Output

 ![TabbedCommandBar Overview](../resources/images/Controls/TabbedCommandBar/Overview.gif)

## Properties

### TabView Properties

| Property | Type | Description |
| -- | -- | -- |
| CanCloseTabs | bool | Default value for if the TabViewItem doesn't specify a IsClosable value. |
| IsCloseButtonOverlay | bool | Changes the behavior of how the Close button effects layout.  If True, the close button will overlay itself on top of content if the tab is a fixed size. |
| ItemHeaderTemplate | DataTemplate | Default Template for the TabViewItem Header if no template is specified. |
| SelectedTabWidth | double | Size to set the Selected Tab Header.  Defaults to Auto. |
| TabActionHeader | object | Area to the Right of Tab Strip before Padding. |
| TabActionHeaderTemplate | DataTemplate | Template for the TabActionHeader. |
| TabEndHeader | object | Area to the Right of the Tab Strip after Padding. |
| TabEndHeaderTemplate | DataTemplate | Template for the TabEndHeader. |
| TabStartHeader | object | Description Area to the Left of the Tab Strip. |
| TabStartHeaderTemplate | DataTemplate | Template for the TabStartHeader. |
| TabWidthBehavior | TabWidthMode | Actual, Equal, or Compact values specify how Tab Headers should be sized.  Defaults to Actual. |

> [!IMPORTANT]
> Do not use `ItemsStackPanel` if you override the ItemsPanel.  It is suggested to keep the `TabWidthBehavior` to `Actual` when using a custom panel.

### TabViewItem Properties

| Property | Type | Description |
| -- | -- | -- |
| Content | object | Main Tab Content. |
| Header | object | Header Content of the Tab. |
| HeaderTemplate | DataTemplate | Template for the Header object. |
| Icon | IconElement | Icon of the Tab. |
| IsClosable | bool | Set to true for the TabViewItem to show a close button. |

## Events

### TabView Events

| Events | Description |
| -- | -- |
| TabClosing | Fires when a Tab is about to be closed, can be intercepted to prevent closure. |
| TabDraggedOutside | Fires when a Tab is dragged outside of the Tab bar. |

### TabViewItem Events
| Events | Description |
| -- | -- |
| TabClosing | Fires when a Tab's closed button is clicked. |

## Examples

If you want to replicate the behavior of Microsoft Edge with the TabView, you can use the following setup:

```xaml
<controls:TabView TabWidthBehavior="Equal"
                  CanCloseTabs="True"
                  IsCloseButtonOverlay="True"
                  CanDragItems="True"
                  CanReorderItems="True"
                  AllowDrop="True">
  <controls:TabView.Resources>
    <x:Double x:Key="TabViewItemHeaderMinHeight">32</x:Double>
    <x:Double x:Key="TabViewItemHeaderMinWidth">90</x:Double>
    <x:Double x:Key="TabViewItemHeaderMaxWidth">200</x:Double>
  </controls:TabView.Resources>
  ...
</controls:TabView>
```

The TabView supports data binding as well.  The following example shows binding the TabView to a collection of 'DataItems' which have both 'Value' and 'MyText' properties:

```xaml
<controls:TabView x:Name="TabItems"
                  ItemsSource="{Binding TabItemCollection}">
  <controls:TabView.ItemHeaderTemplate>
    <DataTemplate>
      <TextBlock>
        <Run Text="{Binding Value}"/>
        <Run Text=": "/>
        <Run Text="{Binding MyText}"/>
      </TextBlock>
    </DataTemplate>
  </controls:TabView.ItemHeaderTemplate>
  <controls:TabView.ItemTemplate>
    <DataTemplate>
      <StackPanel>
        <TextBlock Margin="8">
          <Run Text="Tab Value: "/>
          <Run Text="{Binding Value}" />
        </TextBlock>
        <TextBlock Margin="8,0,0,0" Text="Some other shared content..." />
      </StackPanel>
    </DataTemplate>
  </controls:TabView.ItemTemplate>
</controls:TabView>
```

> [!NOTE]
> It's recommended to use an [ObservableCollection](https://docs.microsoft.com/dotnet/api/system.collections.objectmodel.observablecollection-1) when working with the TabbedCommandBar.

## Sample Project

[TabView Sample Page Source](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/master/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/TabbedCommandBar). You can [see this in action](uwpct://Controls?sample=TabbedCommandBar) in the [Windows Community Toolkit Sample App](http://aka.ms/uwptoolkitapp).

## Default Template

[TabbedCommandBar XAML File](https://github.com/windows-toolkit/WindowsCommunityToolkit/blob/master/Microsoft.Toolkit.Uwp.UI.Controls/TabbedCommandBar/TabbedCommandBar.xaml) is the XAML template used in the toolkit for the default styling.

## Requirements

| Device family | Universal, 10.0.16299.0 or higher  |
| -- | -- |
| Namespace | Microsoft.Toolkit.Uwp.UI.Controls |
| NuGet package | [Microsoft.Toolkit.Uwp.UI.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI.Controls/) |

## API

- [TabbedCommandBar source code](https://github.com/Microsoft/WindowsCommunityToolkit/tree/master/Microsoft.Toolkit.Uwp.UI.Controls/TabbedCommandBar)

## Related Topics

- [ObservableCollection](https://docs.microsoft.com/dotnet/api/system.collections.objectmodel.observablecollection-1)
- [IconElement](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.IconElement)
- [Ribbon (WPF)](https://docs.microsoft.com/dotnet/api/system.windows.controls.ribbon.ribbon)
