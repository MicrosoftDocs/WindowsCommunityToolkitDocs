---
title: TokenizingTextBox
author: michael-hawker
description: A text input control that auto-suggests and displays token items.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, TokenizingTextBox
dev_langs:
  - csharp
---

# TokenizingTextBox

The [TokenizingTextBox](/dotnet/api/microsoft.toolkit.uwp.ui.controls.tokenizingtextbox) is an advanced [AutoSuggestBox](/uwp/api/Windows.UI.Xaml.Controls.AutoSuggestBox) which will display selected items as tokens within the textbox. A user can easily see the picked items or remove them easily.

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://Controls?sample=TokenizingTextBox)

## Syntax

```xaml
  <controls:TokenizingTextBox
    QueryIcon="Tag"
    PlaceholderText="Add Tags"
    TokenDelimiter=","/>
```

## Sample Output

  ![TokenizingTextBox Example](../resources/images/Controls/TokenizingTextBox.png)

## Properties

| Property | Type | Description |
| -- | -- | -- |
| AutoSuggestBoxStyle | Style | Inner AutoSuggestBox style |
| AutoSuggestBoxTextBoxStyle | Style | Inner TextBox style of the AutoSuggestBox |
| PlaceholderText | string | Placeholder text to display when there's no text in the textbox |
| QueryIcon | IconSource |
| QueryText | string | Gets or sets the text query of the AutoSuggestBox |
| SelectedItems | IList&lt;object&gt; | Collection of items selected by the user |
| SelectedTokenText | string | Complete set of text for any selection in the control |
| SuggestedItemsSource | object | List of suggested items |
| SuggestedItemTemplate | DataTemplate | Template for suggested items |
| SuggestedItemTemplateSelector | DataTemplateSelector | Template selector for suggested items |
| SuggestedItemContainerStyle | Style for suggested item's container |
| TabNavigateBackOnArrow | bool | Value indicating whether the control will move focus to the previous control when an arrow key is pressed and selection is at one of the limits in the control. |
| Text | string | Text of currently focused text box part |
| TextMemberPath | string | Path of property for item display |
| TokenDelimiter | string | Character delimiter for recognizing a token |
| TokenItemTemplate | DataTemplate | Template for a token item |
| TokenItemTemplateSelector | DataTemplateSelector | Template selector for token items |
| TokenItemStyle | Style | Style for a token item |
| TokenSpacing | double | Amount of spacing between tokens |

## Methods

| Methods | Return Type | Description |
| -- | -- | -- |
| AddTokenItem(data, bool) | void | Used in special cases where you want to add a token manually to the control |
| ClearAsync() | Task | Clears everything from the control, tokens and text. |
| GetUntokenizedText(string) | string | Returns the string representation of each token item, concatenated and delimited. |

## Events

| Events | Description |
| -- | -- |
| QuerySubmitted | Event raised when the user submits the text query. |
| SuggestionChosen | Event raised when a suggested item is chosen by the user. |
| TextChanged | Event raised when the text input value has changed. |
| TokenItemAdding | Event raised before a new token item has been added. Can be used to transform user text into an object. |
| TokenItemRemoving | Event raised before a token item is removed (cancelable). |
| TokenItemRemoved | Event raised after a token item has been removed. |

## Sample Project

[TokenizingTextBox sample page Source](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.1.0/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/TokenizingTextBox). You can [see this in action](uwpct://Controls?sample=TokenizingTextBox) in [Windows Community Toolkit Sample App](https://aka.ms/windowstoolkitapp).

## Requirements

| Device family | Universal, 10.0.17763.0 or higher |
| -- | -- |
| Namespace | Microsoft.Toolkit.Uwp.UI.Controls |
| NuGet package | [Microsoft.Toolkit.Uwp.UI.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI.Controls/) |

## API

* [TokenizingTextBox source code](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.1.0/Microsoft.Toolkit.Uwp.UI.Controls.Input/TokenizingTextBox)

## Related Topics

* [AutoSuggestBox](/uwp/api/Windows.UI.Xaml.Controls.AutoSuggestBox)
* [IconSource](/uwp/api/windows.ui.xaml.controls.iconsource)
