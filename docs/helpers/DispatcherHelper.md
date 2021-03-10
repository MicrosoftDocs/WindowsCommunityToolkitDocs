---
title: DispatcherHelper
author: nmetulev
description: The DispatcherHelper class enables easy interaction with CoreDispatcher, mainly in the case of executing a block of code on the UI thread from a non-UI thread (outdated docs).
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, DispatcherHelper
dev_langs:
  - csharp
  - vb
---

# DispatcherHelper

> [!WARNING]
> This type has been deprecated and it will be removed from the Windows Community Toolkit, please refer to the [`DispatcherQueueExtensions`](..\extensions\DispatcherQueueExtensions.md) type.

The DispatcherHelper class enables easy interaction with [CoreDispatcher](https://msdn.microsoft.com/library/windows/apps/windows.ui.core.coredispatcher.aspx), mainly in the case of executing a block of code on the UI thread from a non-UI thread.

_What is included in the helper?_

- Extension method with overloads for [CoreDispatcher](https://msdn.microsoft.com/library/windows/apps/windows.ui.core.coredispatcher.aspx) class.

- Extension method with overloads for [CoreApplicationView](https://msdn.microsoft.com/library/windows/apps/windows.applicationmodel.core.coreapplicationview.aspx) (for multi window applications).

- Static helper methods for executing a specific function on the UI thread of the current application's main window.

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://Helpers?sample=DispatcherHelper)

## Syntax

```csharp
DispatcherHelper.ExecuteOnUIThreadAsync<T>(() =>
{
    // Code to execute on main window's UI thread
});

await CoreApplication.MainView.Dispatcher.AwaitableRunAsync<T>( () =>
{
    
});
```

```vb
DispatcherHelper.ExecuteOnUIThreadAsync(Of T)(Function()
    ' Code to execute on main window's UI thread
End Function)

Await CoreApplication.MainView.Dispatcher.AwaitableRunAsync(Of T)(Function()

End Function)
```

## Methods

|                                      Methods                                       | Return Type |                                                                Description                                                                |
|------------------------------------------------------------------------------------|-------------|-------------------------------------------------------------------------------------------------------------------------------------------|
|         AwaitableRunAsync(CoreDispatcher, Action, CoreDispatcherPriority)          |    Task     | Extension method for CoreDispatcher. Offering an actual awaitable Task with optional result that will be executed on the given dispatcher |
|          AwaitableRunAsync(CoreDispatcher, Func, CoreDispatcherPriority)           |    Task     | Extension method for CoreDispatcher. Offering an actual awaitable Task with optional result that will be executed on the given dispatcher |
|      AwaitableRunAsync(CoreDispatcher, Func\<Task\<T>>, CoreDispatcherPriority)      |   Task\<T>   | Extension method for CoreDispatcher. Offering an actual awaitable Task with optional result that will be executed on the given dispatcher |
|          AwaitableRunAsync(CoreDispatcher, Func, CoreDispatcherPriority)           |   Task\<T>   | Extension method for CoreDispatcher. Offering an actual awaitable Task with optional result that will be executed on the given dispatcher |
|               ExecuteOnUIThreadAsync(Action, CoreDispatcherPriority)               |    Task     |                    Execute the given function asynchronously on given view's UI thread. Default view is the main view                     |
|                ExecuteOnUIThreadAsync(Func, CoreDispatcherPriority)                |    Task     |                                  Execute the given function asynchronously on UI thread of the main view                                  |
|    ExecuteOnUIThreadAsync(CoreApplicationView, Action, CoreDispatcherPriority)     |    Task     |                    Execute the given function asynchronously on given view's UI thread. Default view is the main view                     |
|     ExecuteOnUIThreadAsync(CoreApplicationView, Func, CoreDispatcherPriority)      |    Task     |                    Execute the given function asynchronously on given view's UI thread. Default view is the main view                     |
|           ExecuteOnUIThreadAsync(Func<Task\<T>>, CoreDispatcherPriority)            |   Task\<T>   |                                  Execute the given function asynchronously on UI thread of the main view                                  |
|              ExecuteOnUIThreadAsync(Func\<T>, CoreDispatcherPriority)               |   Task\<T>   |                    Execute the given function asynchronously on given view's UI thread. Default view is the main view                     |
| ExecuteOnUIThreadAsync(CoreApplicationView, Func<Task\<T>>, CoreDispatcherPriority) |   Task\<T>   |                    Execute the given function asynchronously on given view's UI thread. Default view is the main view                     |
|     ExecuteOnUIThreadAsync(CoreApplicationView, Func, CoreDispatcherPriority)      |   Task\<T>   |                    Execute the given function asynchronously on given view's UI thread. Default view is the main view                     |

## Example

```csharp
// Executing from a non-UI thread with helper method
int returnedFromUIThread = await DispatcherHelper.ExecuteOnUIThreadAsync<int>(() =>
{
    // Code to execute on main window's UI thread
    NormalTextBlock.Text = "Updated from a random thread!";
    return 1;
});

// returnedFromUIThread now is 1, execution can go on from the non-UI thread

// Or update it manually via the Extension method for CoreDispatcher
returnedFromUIThread = await CoreApplication.MainView.Dispatcher.AwaitableRunAsync<int>(() =>
{
    NormalTextBlock.Text = "Updated from a random thread with extension method!";
    return 1;
});
```

```vb
' Executing from a non-UI thread with helper method
Dim returnedFromUIThread As Integer = Await DispatcherHelper.ExecuteOnUIThreadAsync(Of Integer)(Function()
    ' Code to execute on main window's UI thread
    NormalTextBlock.Text = "Updated from a random thread!"
    Return 1
End Function)

' returnedFromUIThread now is 1, execution can go on from the non-UI thread

' Or update it manually via the Extension method for CoreDispatcher
returnedFromUIThread = Await CoreApplication.MainView.Dispatcher.AwaitableRunAsync(Of Integer)(Function()
    NormalTextBlock.Text = "Updated from a random thread with extension method!"
    Return 1
End Function)
```

## Sample Project

[DispatcherHelper Sample Page Source](https://github.com/Microsoft/WindowsCommunityToolkit//tree/master/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/DispatcherHelper). You can [see this in action](uwpct://Helpers?sample=DispatcherHelper) in the [Windows Community Toolkit Sample App](https://aka.ms/uwptoolkitapp).

## Requirements

| Device family | Universal, 10.0.16299.0 or higher |
| --- | --- |
| Namespace | Microsoft.Toolkit.Uwp |

## API

- [DispatcherHelper source code](https://github.com/Microsoft/WindowsCommunityToolkit//blob/master/Microsoft.Toolkit.Uwp/Helpers/DispatcherHelper.cs)
