---
title: RichSuggestBox
author: huynhsontung
description: A rich text input control that auto-suggests and stores token items in a document.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, RichSuggestBox
dev_langs:
  - csharp
---

# RichSuggestBox

The [RichSuggestBox](/dotnet/api/microsoft.toolkit.uwp.ui.controls.richsuggestbox) is a combination of AutoSuggestBox and RichEditBox which provides suggestions when the user types certain customizable prefixes and stores suggested items as tokens in the document.

RichSuggestBox can operate in Rich Text Format (RTF) mode or plain-text mode. In RTF mode, the user can insert rich text documents that contain formatted text, hyperlinks, and images. In plain-text mode, the user can only insert plain-text as the only formatted texts in the document are tokens.

RichSuggestBox is inspired by text controls commonly found in social applications where you type "@" and the control starts suggesting different people to be included in the text box.
<!-- Your API link will be in a form like: /dotnet/api/microsoft.toolkit.uwp.helpers.printhelper 
with the namespace and the class name. Without any country/region 'en-us' identifiers, the root domain, or query string views.
-->



<!-- Use below format to display note
> [!NOTE]
> Some note

> [!IMPORTANT]
> Some important note

> [!WARNING]
> Some warning note
-->

> **Platform APIs:** [`RichSuggestBox`](/dotnet/api/microsoft.toolkit.uwp.ui.controls.richsuggestbox)

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://Controls?sample=RichSuggestBox)

## Syntax

```xaml
<controls:RichSuggestBox
  PlaceholderText="Leave a comment"
  ItemTemplate="{StaticResource EmailTemplate}"
  Prefixes="@#" />
```

## Example Output

![RichSuggestBox Example](../resources/images/Controls/RichSuggestBox.gif)

## Properties

| Property | Type | Description |
| -- | -- | -- |
| ClipboardCopyFormat | RichEditClipboardFormat | Gets or sets a value that specifies whether text is copied with all formats, or as plain text only. |
| ClipboardPasteFormat | RichEditClipboardFormat | Gets or sets a value that specifies whether pasted text preserves all formats, or as plain text only. |
| Description | object | Gets or sets content that is shown below the control. The content should provide guidance about the input expected by the control. |
| DisabledFormattingAccelerators | DisabledFormattingAccelerators | Gets or sets a value that indicates which keyboard shortcuts for formatting are disabled. |
| Header | object | Gets or sets the content for the control's header. |
| HeaderTemplate | DataTemplate | Gets or sets the `DataTemplate` used to display the content of the control's header. |
| HorizontalOffset | double | Gets the distance the content has been scrolled horizontally from the underlying `ScrollViewer`. |
| PlaceholderText | string | Gets or sets the text that is displayed in the control until the value is changed by a user action or some other operation. |
| PopupCornerRadius | CornerRadius | Gets or sets the radius for the corners of the popup control's border. |
| PopupFooter | object | Gets or sets the content for the suggestion popup control's footer. |
| PopupFooterTemplate | DataTemplate | Gets or sets the `DataTemplate` used to display the content of the suggestion popup control's footer. |
| PopupHeader | object | Gets or sets the content for the suggestion popup control's header. |
| PopupHeaderTemplate | DataTemplate | Gets or sets the `DataTemplate` used to display the content of the suggestion popup control's header. |
| PopupPlacement | SuggestionPopupPlacementMode | Gets or sets suggestion popup placement to either `Floating` or `Attached` to the text box. |
| Prefixes | string | Gets or sets prefix characters to start a query.<br />Prefix characters must be punctuations (must satisfy [IsPunctuation(Char)](https://docs.microsoft.com/dotnet/api/system.char.ispunctuation) method). |
| RichEditBoxStyle | Style | Gets or sets the style of the underlying `RichEditBox`. |
| TextDocument | RichEditTextDocument | Gets an object that enables access to the text object model for the text contained in a `RichEditBox`. |
| TokenBackground | SolidColorBrush | Gets or sets the default brush used to color the suggestion token background. |
| TokenForeground | SolidColorBrush | Gets or sets the default brush used to color the suggestion token foreground. |
| Tokens | ReadOnlyObservableCollection\<RichSuggestToken\> | Gets a collection of suggestion tokens that are present in the document. |
| VerticalOffset | double | Gets the distance the content has been scrolled vertically from the underlying `ScrollViewer`. |

## Methods

| Methods | Return Type | Description |
| -- | -- | -- |
| AddTokens(IEnumerable\<RichSuggestToken\>) | void | Add tokens to be tracked against the document. Duplicate tokens will not be updated. |
| Clear() | void | Clear the document and token list. This will also clear the undo/redo history. |
| ClearUndoRedoSuggestionHistory() | void | Clear unused tokens and undo/redo history. |
| GetRectFromRange(ITextRange) | Rect | Retrieves the bounding rectangle that encompasses the text range with position measured from the top left of the `RichSuggestBox` control. |
| Load(string, IEnumerable\<RichSuggestToken\>) | void | Populate the `RichSuggestBox` with an existing Rich Text Format (RTF) document and a collection of tokens.<br />This method replaces the current document and token list. |
| TryGetTokenFromRange(ITextRange, out RichSuggestToken) | bool | Try getting the token associated with a text range. |

## Events

| Events | Description |
| -- | -- |
| Paste | Event raised when text is pasted into the control. |
| SelectionChanged | Event raised when the text selection has changed. |
| SuggestionChosen | Event raised when user click on a suggestion.<br />This event lets you customize the token appearance in the document. |
| SuggestionRequested | Event raised when the control needs to show suggestions. |
| TextChanged | Event raised when text is changed, either by user or by internal formatting. |
| TokenPointerOver | Event raised when a pointer is hovering over a token. |
| TokenSelected | Event raised when a token is fully highlighted. |


## Sample Project

[RichSuggestBox sample page Source](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.1.0/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/RichSuggestBox). You can [see this in action](uwpct://Controls?sample=RichSuggestBox) in [Windows Community Toolkit Sample App](https://aka.ms/windowstoolkitapp).

## Requirements

| Device family | Universal, 10.0.17763.0 or higher |
| -- | -- |
| Namespace | Microsoft.Toolkit.Uwp.UI.Controls |
| NuGet package | [Microsoft.Toolkit.Uwp.UI.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI.Controls/) |

## Source Code

- [RichSuggestBox source code](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.1.0/Microsoft.Toolkit.Uwp.UI.Controls.Input/RichSuggestBox)

## Related Topics

- [AutoSuggestBox](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.autosuggestbox)
- [RichEditBox](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.richeditbox)
- [TokenizingTextBox](TokenizingTextBox.md)