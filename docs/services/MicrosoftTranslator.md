---
title: Microsoft Translator Service
author: nmetulev
description: The Microsoft Translator Service allows you to translate text to various supported languages.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, MicrosoftTranslator
dev_langs:
  - csharp
  - vb
---

# Microsoft Translator Service

> [!WARNING]
> (This API has been removed and the Microsoft Translator Service is no longer available in the Windows Community Toolkit. Please refer to the [Microsoft Translator](/azure/cognitive-services/translator/) documentation instead.)

The **Microsoft Translator Service** allows you to translate text to various supported languages.

## Set up Microsoft Translator Service

[Signup for Microsoft Translator Service](https://ms.portal.azure.com/#create/Microsoft.CognitiveServicesTextTranslation) using your Microsoft Azure subscription account. There is a free trial option that allows you to translate up to 2,000,000 characters per month.

## Example Syntax

```csharp
// using Microsoft.Toolkit.Uwp.Services.MicrosoftTranslator;

await TranslatorService.Instance.InitializeAsync("<translator service key");

// Retrieves codes and friendly names for the languages available for text translation.
var languages = await TranslatorService.Instance.GetLanguageNamesAsync("en");

// Detects the language of a text.
var detectResult = await TranslatorService.Instance.DetectLanguageWithResponseAsync("Hello everyone!");
var detectedLanguage = detectResult.Language;
var detectedLanguageConfidence = detectResult.Score;

// Translates the text to Italian.
var translationResult = await TranslatorService.Instance.TranslateWithResponseAsync("Hello everyone!", "it");
var translatedText = translationResult.Translation.Text;
```

```vb
' Imports Microsoft.Toolkit.Uwp.Services.MicrosoftTranslator

Await TranslatorService.Instance.InitializeAsync("<translator service key")

' Retrieves codes and friendly names for the languages available for text translation.
Dim languages = Await TranslatorService.Instance.GetLanguageNamesAsync("en")

' Detects the language of a text.
Dim detectResult = Await TranslatorService.Instance.DetectLanguageWithResponseAsync("Hello everyone!")
Dim detectedLanguage = detectResult.Language
Dim detectedLanguageConfidence = detectResult.Score

' Translates the text to Italian.
Dim translationResult = Await TranslatorService.Instance.TranslateWithResponseAsync("Hello everyone!", "it")
Dim translatedText = translationResult.Translation.Text
```
