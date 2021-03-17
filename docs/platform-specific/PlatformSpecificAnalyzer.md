---
title: UWP Platform Specific Analyzer
author: hermitdave
description: Platform Specific Analyzer is a Roslyn analyzer that analyzes and suggests code fixes to ensure that any version / platform specific API are guarded by correct runtime checks (outdated docs).
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, platform specific, platform specific analyzer, roslyn analyzer
dev_langs:
  - csharp
  - visualbasic
---

# Platform Specific Analyzer

> [!WARNING]
> This docs page is outdated and the Platform Specific Analyzers have been removed. Improvements are continually being made to the Visual Studio development experience, so please ensure you are on the latest version.

When writing [version](/windows/uwp/debug-test-perf/version-adaptive-code) or platform adaptive code, the developers should ensure that code checks for presence of API before calling it.
The platform specific analyzer is a Roslyn Analyzer that can parse through code and suggest fixes where appropriate.

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://Helpers?sample=PlatformSpecificAnalyzer)

## Installation

The analyzer is available both as a nuget package

* References > Manage NuGet References > install [Microsoft.Toolkit.Uwp.PlatformSpecificAnalyzer](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.PlatformSpecificAnalyzer)

## Sample Output

The analyzer automatically kicks in when code is opened in Visual Studio and supports both C# and Visual Basic

C#
![Code Analysis Underlined](../resources/images/CodeAnalysis.png)

![Code Analysis Suggestion](../resources/images/CodeFixSuggestion.png)

Visual Basic
![Code Analysis Underlined in VB](../resources/images/CodeAnalysisVB.png)

![Code Analysis Suggestion in VB](../resources/images/CodeFixSuggestionVB.png)

## Sample Project

You can [see this in action](uwpct://Helpers?sample=PlatformSpecificAnalyzer) in the [Windows Community Toolkit Sample App](https://aka.ms/windowstoolkitapp).

## Requirements

| Device family | Universal, 10.0.16299.0 or higher   |
| ---------------------------------------------------------------- | ----------------------------------- |
| Namespace                                                        | Microsoft.Toolkit.Uwp.PlatformSpecificAnalyzer |
| NuGet package | [Microsoft.Toolkit.Uwp.PlatformSpecificAnalyzer](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.PlatformSpecificAnalyzer/) |

## API

* [Platform Specific Analyzer](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.0.0/Microsoft.Toolkit.Uwp.PlatformSpecificAnalyzer)

## Related Topics

* [Platform Specific Differences Generator](./platformspecificdifferencesgenerator.md)
