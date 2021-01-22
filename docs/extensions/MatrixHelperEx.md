---
title: MatrixHelperEx
author: michael-hawker
description: Learn about the MatrixHelperEx extension. This extension provides extra UWP MatrixHelper-like methods.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, Extensions, matrix, MatrixHelper, Multiply, round, Rect, Transform
dev_langs:
  - csharp
---

# MatrixHelperEx
[MatrixHelperEx](/dotnet/api/microsoft.toolkit.uwp.ui.extensions.matrixhelperex) provides extra methods for various matrix operations.

## Methods

| Methods | Return Type | Description |
| -- | -- | -- |
| Multiply(Matrix, Matrix) | Matrix | Multiply the two matrices and return the result. |
| Round(Matrix, double) | Matrix | Rounds the non-offset elements of a matrix to avoid issues due to floating point imprecision and returns the result. |
| RectTransform(Rect, Matrix) | Rect | Returns the rectangle that results from applying the specified matrix to the specified rectangle. |

## Requirements (Windows 10 Device Family)

| [Device family](/windows/uwp/get-started/universal-application-platform-guide) | Universal, 10.0.16299.0 or higher |
| --- | --- |
| Namespace | Microsoft.Toolkit.Uwp.UI |
| NuGet package | [Microsoft.Toolkit.Uwp.UI](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI/) |

## API Source Code

- [MatrixHelperEx source code](https://github.com/Microsoft/WindowsCommunityToolkit//blob/master/Microsoft.Toolkit/Extensions/Media/MatrixHelperEx.cs)

## Related Topics

- [Windows.UI.Xaml.Media.Matrix](/uwp/api/Windows.UI.Xaml.Media.Matrix)
- [Windows.Foundation.Rect](/uwp/api/Windows.Foundation.Rect)
- [System.Windows.Media.Matrix](/dotnet/api/system.windows.media.matrix)
- [System.Windows.Rect](/dotnet/api/system.windows.rect)