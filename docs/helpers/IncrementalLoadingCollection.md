---
title: Incremental Loading Collection Helpers
author: nmetulev
description: The IncrementalLoadingCollection helpers greatly simplify the definition and usage of collections whose items can be loaded incrementally only when needed by the view
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, IncrementalLoadingCollection
dev_langs:
  - csharp
  - vb
---

# Incremental Loading Collection Helpers

The **IncrementalLoadingCollection** helpers greatly simplify the definition and usage of collections whose items can be loaded incrementally only when needed by the view, i.e., when user scrolls a [ListView](/uwp/api/Windows.UI.Xaml.Controls.ListView) or a [GridView](/uwp/api/Windows.UI.Xaml.Controls.GridView).

| Helper | Purpose |
| --- | --- |
|[IIncrementalSource](/dotnet/api/microsoft.toolkit.collections.iincrementalsource-1) | An interface that represents a data source whose items can be loaded incrementally. |
|[IncrementalLoadingCollection](/dotnet/api/microsoft.toolkit.uwp.incrementalloadingcollection-2) | An extension of [ObservableCollection](/dotnet/api/system.collections.objectmodel.observablecollection-1) such that its items are loaded only when needed. |

> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://Helpers?sample=Incremental%20Loading%20Collection)

## IncrementalLoadingCollection Properties

|     Property     |                                   Type                                    |                                                          Description                                                           |
|------------------|---------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------|
| CurrentPageIndex |                                    int                                    |                         Gets or sets a value indicating The zero-based index of the current items page                         |
|   HasMoreItems   |                                   bool                                    |                         Gets a value indicating whether the collection contains more items to retrieve                         |
|    IsLoading     |                                   bool                                    |                                   Gets a value indicating whether new items are being loaded                                   |
|   ItemsPerPage   |                                    int                                    |                    Gets a value indicating how many items that must be retrieved for each incremental call                     |
|   OnEndLoading   | [Action](/dotnet/api/system.action) |                             Gets or sets an Action that is called when a retrieval operation ends                              |
|     OnError      |                             Action\<Exception>                             | Gets or sets an Action that is called if an error occours during data retrieval. The actual Exception is passed as an argument |
|  OnStartLoading  |                                  Action                                   |                            Gets or sets an Action that is called when a retrieval operation begins                             |

## IncrementalLoadingCollection Methods

|             Methods              |             Return Type              |                                             Description                                              |
|----------------------------------|--------------------------------------|------------------------------------------------------------------------------------------------------|
| LoadDataAsync(CancellationToken) |       Task<IEnumerable\<IType>>       |                              Actually performs the incremental loading                               |
|    LoadMoreItemsAsync(UInt32)    | IAsyncOperation\<LoadMoreItemsResult> |                            Initializes incremental loading from the view                             |
|            Refresh()             |                 void                 | Clears the collection and resets the page index which triggers an automatic reload of the first page |
|          RefreshAsync()          |                 Task                 |                        Clears the collection and reloads data from the source                        |

## Example

`IIncrementalSource` allows to define the data source:

```csharp
// Be sure to include the using at the top of the file:
//using Microsoft.Toolkit.Uwp;

public class Person
{
    public string Name { get; set; }
}

public class PeopleSource : IIncrementalSource<Person>
{
    private readonly List<Person> people;

    public PeopleSource()
    {
        // Creates an example collection.
        people = new List<Person>();

        for (int i = 1; i <= 200; i++)
        {
            var p = new Person { Name = "Person " + i };
            people.Add(p);
        }
    }

    public async Task<IEnumerable<Person>> GetPagedItemsAsync(int pageIndex, int pageSize)
    {
        // Gets items from the collection according to pageIndex and pageSize parameters.
        var result = (from p in people
                        select p).Skip(pageIndex * pageSize).Take(pageSize);

        // Simulates a longer request...
        await Task.Delay(1000);

        return result;
    }
}
```

```vb
' Be sure to include the using at the top of the file:
'Imports Microsoft.Toolkit.Uwp

Public Class Person

    Public Property Name As String
End Class

Public Class PeopleSource
    Implements IIncrementalSource(Of Person)

    Private ReadOnly people As List(Of Person)

    Public Sub New()
        ' Creates an example collection.
        people = New List(Of Person)()
        For i As Integer = 1 To 200
            Dim p = New Person With {.Name = "Person " & i}
            people.Add(p)
        Next
    End Sub

    Public Async Function GetPagedItemsAsync(pageIndex As Integer, pageSize As Integer, Optional cancellationToken As CancellationToken = Nothing) As Task(Of IEnumerable(Of Person)) Implements Microsoft.Toolkit.Collections.IIncrementalSource(Of Person).GetPagedItemsAsync
        ' Gets items from the collection according to pageIndex and pageSize parameters.
        Dim result = (From p In people Select p).Skip(pageIndex * pageSize).Take(pageSize)

        ' Simulates a longer request...
        Await Task.Delay(1000)
        Return result
    End Function
End Class
```

The *GetPagedItemsAsync* method is invoked every time the view need to show more items.

`IncrementalLoadingCollection` can then be bound to a [ListView](/uwp/api/Windows.UI.Xaml.Controls.ListView) or a [GridView-like](/uwp/api/Windows.UI.Xaml.Controls.GridView) control:

```csharp
var collection = new IncrementalLoadingCollection<PeopleSource, Person>();
PeopleListView.ItemsSource = collection;
```

```vb
Dim collection = New IncrementalLoadingCollection(Of PeopleSource, Person)()
PeopleListView.ItemsSource = collection
```

## Sample Project

[Incremental Loading Collection Sample Page Source](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.1.0/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/Incremental%20Loading%20Collection). You can [see this in action](uwpct://Helpers?sample=Incremental%20Loading%20Collection) in the [Windows Community Toolkit Sample App](https://aka.ms/windowstoolkitapp).

## Requirements

| Device family | Universal, 10.0.16299.0 or higher |
| --- | --- |
| Namespace | Microsoft.Toolkit.Uwp |
| NuGet package | [Microsoft.Toolkit.Uwp](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp/) |

## API

* [IncrementalLoadingCollection source code](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.1.0/Microsoft.Toolkit.Uwp/IncrementalLoadingCollection)
