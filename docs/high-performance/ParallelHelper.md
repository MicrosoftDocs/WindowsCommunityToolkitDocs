---
title: ParallelHelper
author: Sergio0694
description: Helpers to work with parallel code in a highly optimized manner
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, parallel, high performance, net core, net standard
dev_langs:
  - csharp
---

# ParallelHelper

The [ParallelHelper](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.highperformance.helpers.parallelhelper) contains high performance APIs to work with parallel code. It contains performance oriented methods that can be used to quickly setup and execute paralell operations over a given data set or iteration range or area.

## How it works

`ParallelHelper` is built around three main concepts:

- It performs automatic batching over the target iteration range. This means that it automatically schedules the right number of working units based on the number of available CPU cores. This is done to reduce the overhead of invoking the parallel callback once for every single parallel iteration.
- It heavily leverages the way generic types are implemented in C#, and uses `struct` types implementing specific interfaces instead of delegates like `Action<T>`. This is done so that the JIT compiler will be able to "see" each individual callback type being used, which allows it to inline the callback entirely, when possible. This can greatly reduce the overhead of each parallel iteration, especially when using very small callbacks, which would have a trivial cost with respect to the delegate invocation alone. Additionally, using a `struct` type as callback requires developers to manually handle variables that are being captured in the closure, which prevents accidental captures of the `this` pointer from instance methods and other values that could considerably slowdown each callback invocation. This is the same approach that is used in other performance-oriented libraries such as `ImageSharp`.
- It exposes 4 types of APIs that represent 4 different types of iterations: 1D and 2D loops, items iteration with side effect and items iteration without side effect. Each type of action has a corresponding `interface` type that needs to be applied to the `struct` callbacks being passed to the `ParallelHelper` APIs: these are `IAction`, `IAction2D`, `IRefAction<T>` and `IInAction<T>`. This helps developers to write code that is clearer regarding its intent, and allows the APIs to perform further optimizations internally.

## Syntax

Let's say we're interested in processing all the items in some `float[]` array, and to multiply each of them by `2`. In this case we don't need to capture any variables: we can just use the `IRefAction<T>` `interface` and `ParallelHelper` will load each item to feed to our callback automatically. All that's needed is to define our callback, that will receive a `ref float` argument and perform the necessary operation:

```csharp
// Be sure to include this using at the top of the file:
using Microsoft.Toolkit.HighPerformance.Helpers;

// First declare the struct callback
public readonly struct ByTwoMultiplier : IRefAction<float>
{
    public void Invoke(ref float x) => x *= 2;
}

// Create an array and run the callback
float[] array = new float[10000];

ParallelHelper.ForEach<float, ByTwoMultiplier>(array);
```

With the `ForEach` API, we don't need to specify the iteration ranges: `ParallelHelper` will batch the collection and process each input item automatically. Furthermore, in this specific example we didn't even have to pass our `struct` as an argument: since it didn't contain any fields we needed to initialize, we could just specify its type as a type argument when invoking `ParallelHelper.ForEach`: that API will then create a new instance of that `struct` on its own, and use that to process the various items.

To introduce the concept of closures, suppose we want to multiply the array elements by a value that is specified at runtime. To do so, we need to "capture" that value in our callback `struct` type. We can do that like so:

```csharp
public readonly struct ItemsMultiplier : IRefAction<float>
{
    private readonly float factor;
    
    public ItemsMultiplier(float factor)
    {
        this.factor = factor;
    }

    public void Invoke(ref float x) => x *= this.factor;
}

// ...

ParallelHelper.ForEach(array, new ItemsMultiplier(3.14f));
```

We can see that the `struct` now contains a field that represents the factor we want to use to multiply elements, instead of using a constant. And when invoking `ForEach`, we're explicitly creating an instance of our callback type, with the factor we're interested in. Furthermore, in this case the C# compiler is also able to automatically recognize the type arguments we're using, so we can omit them together from the method invocation.

This approach of creating fields for values we need to access from a callback lets us explicitly declare what values we want to capture, which helps makes the code more expressive. This is exactly the same thing that the C# compiler does behind the scenes when we declare a lambda function or local function that accesses some local variable as well.

Here is another example, this time using the `For` API to initialize all the items of an array in parallel. Note how this time we're capturing the target array directly, and we're using the `IAction` `interface` for our callback, which gives our method the current parallel iteration index as argument:

```csharp
public readonly struct ArrayInitializer : IAction
{
    private int[] array;
    
    public ArrayInitializer(int[] array)
    {
        this.array = array;
    }
    
    public void Invoke(int i)
    {
    	this.array[i] = i;
    }
}

// ...

ParallelHelper.For(0, array.Length, new ArrayInitializer(array));
```

**NOTE:** since the callback types are `struct`-s, they're passed _by copy_ to each thread running parallel, not by reference. This means that value types being stored as fields in a callback types will be copied as well. A good practice to remember that detail and avoid errors is to mark the callback `struct` as `readonly`, so that the C# compiler will not let us modify the values of its fields. This only applies to _instance_ fields of a value type: if a callback `struct` has a `static` field of any type, or a reference field, then that value will correctly be shared between parallel threads.

## Methods

These are the 4 main APIs exposed by `ParallelHelper`, corresponding to the `IAction`, `IAction2D`, `IRefAction<T>` and `IInAction<T>` interfaces. The `ParallelHelper` type also exposes a number of overloads for these methods, that offer a number of ways to specify the iteration range(s), or the type of input callback.

| Method | Return Type | Description |
| -- | -- | -- |
| For&lt;TAction>(int, int, in TAction) | void | Executes a specified action in an optimized parallel loop |
| For2D&lt;TAction>(int, int, int, int, in TAction) | void | Executes a specified action in an optimized parallel loop |
| ForEach&lt;TItem,TAction>(Memory<TItem>, in TAction) | void | Executes a specified action in an optimized parallel loop over the input data |
| ForEach&lt;TItem,TAction>(ReadOnlyMemory<TItem>, in TAction) | void | Executes a specified action in an optimized parallel loop over the input data |

## Sample Code

You can find more examples in our [unit tests](https://github.com/Microsoft/WindowsCommunityToolkit//blob/master/UnitTests/UnitTests.HighPerformance.Shared/Helpers)

## Requirements

| Device family | Universal, 10.0.16299.0 or higher |
| --- | --- |
| Namespace | Microsoft.Toolkit.HighPerformance |
| NuGet package | [Microsoft.Toolkit.HighPerformance](https://www.nuget.org/packages/Microsoft.Toolkit.HighPerformance/) |

## API

* [ParallelHelper source code](https://github.com/Microsoft/WindowsCommunityToolkit//blob/master/Microsoft.Toolkit.HighPerformance/Helpers)
