---
title: Windows Community Toolkit Known Issues
author: nmetulev
description: The Windows Community Toolkit is a collection of helper functions, custom controls, and app services. It simplifies and demonstrates common developer tasks building UWP apps for Windows 10. 
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, known issues
---

# Windows Community Toolkit Known Issues

> [!NOTE]
> For an accurate list of known bugs and issues, take a look at the [issues on GitHub](https://github.com/windows-toolkit/WindowsCommunityToolkit/issues)

## Controls

### InfiniteCanvas

* InfiniteCanvas is not supported on Creators Update - [see issue for details](https://github.com/windows-toolkit/WindowsCommunityToolkit/issues/2162)

### ScrollHeader

* ScrollHeader with `Mode="Sticky"` inside a ListView with grouped items causes the groups' headers to be displayed in front of the header - [see issue for details](https://github.com/windows-toolkit/WindowsCommunityToolkit/issues/1446)

### WebView

For the complete list of issues and limitations in this release of the **WebView** control, see [Known Issues of the WebView control for Windows Forms and WPF applications](controls/wpf-winforms/WebView-known-issues.md).

## Extensions

### TextBoxRegEx

* Some phone number formats are not supported - [see issue for details](https://github.com/windows-toolkit/WindowsCommunityToolkit/issues/1821)

## Xaml Islands

### WindowsXamlHost (Windows Forms)

* Windows Forms app using WindowsXamlHost crashes when focus is changed away and back to the app - [see issue for details](https://github.com/windows-toolkit/WindowsCommunityToolkit/issues/2491)
