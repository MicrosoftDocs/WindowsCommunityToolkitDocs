---
title: Guard
author: Sergio0694
description: Helper methods to verify conditions when running code
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, debug, net core, net standard
dev_langs:
  - csharp
---

# Guard

The [Guard](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.diagnostics.guard) can be used to validate method arguments in a streamlined manner, which is also faster, less verbose, more expressive and less error prone than manually writing checks and throwing exceptions.

## How it works

These `Guard` APIs are built with three core principles in mind:

- Being **fast**. To achieve that, all the APIs have been designed to produce as little code as possible in the caller, and each single Guard API will (almost always) be inlined. Furthermore, specialized methods are generated with T4 templates to achieve the most efficient assembly code possible when working with common types (eg. primitive numeric types).
- Being **helpful**. Each `Guard` API produces a detailed exception message that clearly specifies what went wrong, along with additional info (eg. current variable values), when applicable.
- Being **intuitive**. To achieve this, all the `Guard` APIs have expressive and self-explanatory names that make it immediately clear what each API is supposed to do. This shifts the burden of writing checks away from the developers, letting them express conditions using natural language.

## Syntax

Here is a sample method, with some checks being done with explicit checks and manual throw statements:

```csharp
public static void SampleMethod(int[] array, int index, Span<int> span, string text)
{
    if (array is null)
    {
        throw new ArgumentNullException(nameof(array), "The array must not be null");
    }

    if (array.Length >= 10)
    {
        throw new ArgumentException($"The array must have less than 10 items, had a size of {array.Length}", nameof(array));
    }

    if (index < 0 || index >= array.Length)
    {
        throw new ArgumentOutOfRangeException(nameof(index), $"The index must be in the [0, {array.Length}) range, was {index}");
    }

    if (span.Length < array.Length)
    {
        throw new ArgumentException($"The target span is shorter than the input array, had a length of {span.Length}", nameof(span));
    }

    if (string.IsNullOrEmpty(text))
    {
        throw new ArgumentException("The input text can't be null or empty", nameof(text));
    }
}
```

And here is the same method, but using the new `Guard.APIs` to validate the input arguments:

```csharp
public static void SampleMethod(int[] array, int index, Span<int> span, string text)
{
    Guard.IsNotNull(array, nameof(array));
    Guard.HasSizeAtLeast(array, 10, nameof(array));
    Guard.IsInRangeFor(index, array, nameof(index));
    Guard.HasSizeLessThanOrEqualTo(array, span, nameof(span));
    Guard.IsNotNullOrEmpty(text, nameof(text));
}
```

The `Guard` APIs will perform the required checks in the fastest way possible, and will throw the appropriate exception with a well formated message if they fail.

## Methods

There are dozens of different APIs and overloads in the `Guard` class, here are a few of them:

### General

| Methods | Return Type | Description |
| -- | -- | -- |
| IsNotNull<T>(T, string) | void | Asserts that the input value is not null |
| IsOfType<T>(object, string) | void | Asserts that the input value is of a specific type |
| IsAssignableToType<T>(object, string) | void | Asserts that the input value can be assigned to a specified type |
| IsReferenceEqualTo<T>(T, T, string) | void | Asserts that the input value must be the same instance as the target value |
| IsTrue(bool, string) | void | Asserts that the input value must be true |

### Comparisons

| Methods | Return Type | Description |
| -- | -- | -- |
| IsEqualTo<T>(T, T, string) | void | Asserts that the input value must be equal to a specified value |
| IsBitwiseEqualTo<T>(T, T, string) | void | Asserts that the input value must be a bitwise match with a specified value |
| IsLessThan<T>(T, T, string) | void | Asserts that the input value must be less than a specified value |
| IsLessThanOrEqualTo<T>(T, T, string) | void | Asserts that the input value must be less than or equal to a specified value |
| IsInRange<T>(T, T, T, string) | void | Asserts that the input value must be in a given range |
| IsBetween<T>(T, T, T, string name) | void | Asserts that the input value must be in a given interval |

### Strings

| Methods | Return Type | Description |
| -- | -- | -- |
| IsNotNullOrEmpty(string, string) | void | Asserts that the input string instance must not be null or empty |
| IsNotNullOrWhitespace(string, string) | void | Asserts that the input string instance must not be null or whitespace |

### Collections

| Methods | Return Type | Description |
| -- | -- | -- |
| IsNotEmpty<T>(T[], string) | void | Asserts that the input array instance must not be empty |
| HasSizeEqualTo<T>(T[], int, string) | void | Asserts that the input array instance must have a size of a specified value |
| HasSizeAtLeast<T>(T[], int, string) | void | Asserts that the input array must have a size of at least or equal to a specified value |
| IsInRangeFor<T>(int, T[], string) | void | Asserts that the input index is valid for a given array |
| HasSizeLessThanOrEqualTo<T>(T[], T[], string) | void | Asserts that the source array must have a size of less than or equal to that of the destination array |

### Tasks

| Methods | Return Type | Description |
| -- | -- | -- |
| IsCompleted(Task, string) | void | Asserts that the input task is in a completed state |
| IsNotCanceled(Task, string) | void | Asserts that the input task is not canceled |

## Sample Code

You can find more examples in our [unit tests](https://github.com/Microsoft/WindowsCommunityToolkit//blob/master/UnitTests/Diagnostics/Test_Guard.cs)

## Requirements

| Device family | Universal, 10.0.16299.0 or higher |
| --- | --- |
| Namespace | Microsoft.Toolkit.Diagnostics |
| NuGet package | [Microsoft.Toolkit](https://www.nuget.org/packages/Microsoft.Toolkit/) |

The Guard class supports .NET Standard

## API

* [Guard source code](https://github.com/Microsoft/WindowsCommunityToolkit//blob/master/Microsoft.Toolkit/Diagnostics)
