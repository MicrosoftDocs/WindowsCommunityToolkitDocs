---
title: Observable groups
author: vgromfeld
description: A set of helper classes to manage grouping from toolkit
keywords: windows 10, uwp, uwp community toolkit, uwp toolkit, observable, grouping, group, observablecollection
---

# Observable Groups

Provides helper class to easily create grouped collections that can be used in [ListView](https://docs.microsoft.com/en-us/uwp/api/Windows.UI.Xaml.Controls.ListView) or [GridView](https://docs.microsoft.com/en-us/uwp/api/Windows.UI.Xaml.Controls.GridView) controls to display grouped items.

## ObservableGroup<TKey, TValue>

A group of `TValue` objects with a key of type `TKey`.

It is an implementation of [IGrouping<Tkey, TValue>](https://docs.microsoft.com/en-us/dotnet/api/system.linq.igrouping-2?view=netstandard-2.0) based on [ObservableCollection<TValue>](https://docs.microsoft.com/en-us/dotnet/api/system.collections.objectmodel.observablecollection-1?view=netstandard-2.0).
It is used by `ObservableGroupedCollection<TKey, TValue>` to represent the groups.


| Property | Type | Description |
| -- | -- | -- |
| Key | TKey | The key of the group. |

## ObservableGroupedCollection<TKey, TValue>

A list of groups that can be used by a [CollectionViewSource](https://docs.microsoft.com/en-us/uwp/api/Windows.UI.Xaml.Data.CollectionViewSource) to display groups in a `ListView` or `GridView`.
Each group inside the collection has an observable `TKey` key and contains `TValue` values.

It is an `ObservableCollection<ObservableGroup<TKey, TValue>>` so groups can be added to the collection using the regular methods of [ObservableCollection<T>](https://docs.microsoft.com/en-us/dotnet/api/system.collections.objectmodel.observablecollection-1?view=netstandard-2.0).


```csharp
// Grab a sample type
public class Person
{
    public string Name { get; set; }
}

// Set up the original list with a few sample items
var contacts = new[]
{
    new Person { Name = "Staff" },
    new Person { Name = "Swan" },
    new Person { Name = "Orchid" },
    new Person { Name = "Flame" },
    new Person { Name = "Arrow" },
    new Person { Name = "Tempest" },
    new Person { Name = "Pearl" },
    new Person { Name = "Hydra" },
    new Person { Name = "Lamp Post" },
    new Person { Name = "Looking Glass" },
};

// Group the contacts by first letter
var grouped = contacts.GroupBy(GetGroupName).OrderBy(g => g.Key);

// Create an observable grouped collection
var contactsSource = new ObservableGroupedCollection<string, Person>(grouped);

// Set up the CollectionViewSource
var cvs = new CollectionViewSource
{
    IsSourceGrouped = True,
    Source = contactsSource,
};

// Bind the CollectionViewSource to anything that supports grouped collections.
ContactsList.ItemsSource = cvs.View;
```

## ReadOnlyObservableGroup<TKey, TValue>

Represents a read-only `ObservableGroup<TKey, TValue>`.
This class is a read-only wrapper around an `ObservableGroup<TKey, TValue>`.
If changes are made to the underlying collection, the `ReadOnlyObservableGroup<TKey, TValue>` reflects those changes.

## ReadOnlyObservableGroupedCollection<TKey, TValue>

Represents a read-only `ObservableGroupedCollection<TKey, TValue>`.
This class is a read-only wrapper around an `ObservableGroupedCollection<TKey, TValue>`.
If changes are made to the underlying collection, the `ReadOnlyObservableGroupedCollection<TKey, TValue>` reflects those changes.


## IReadOnlyObservableGroup

This interface allows us to use `x:Bind` with `ObservableGroup{TKey, TValue}` and `ReadOnlyObservableGroup{TKey, TValue}` by providing
a non-generic type that we can declare using `x:DataType`.
It extends [INotifyPropertyChanged](https://docs.microsoft.com/en-us/dotnet/api/system.componentmodel.inotifypropertychanged?view=netstandard-2.0).

```xaml
<DataTemplate x:Key="GroupDataTemplate"
              x:DataType="collections:IReadOnlyObservableGroup">
    <StackPanel Orientation="Horizontal">
        <TextBlock Style="{StaticResource SubtitleTextBlockStyle}"
                   Text="{x:Bind (x:String)Key}" />
        <TextBlock Margin="8,0,0,0"
                   VerticalAlignment="Bottom"
                   Opacity="0.8"
                   Style="{StaticResource CaptionTextBlockStyle}"
                   Text="{x:Bind system:String.Format('{0} item(s)', Count), Mode=OneWay}" />
    </StackPanel>
</DataTemplate>
```

| Property | Type | Description |
| -- | -- | -- |
| Key | object | The key of the group. It is immutable. |
| Count | int | The number of items currently in the grouped collection. | 

## Sample Project

[Observable group Sample Page](https://github.com/Microsoft/WindowsCommunityToolkit//tree/master/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/ObservableGroup).

You can [see this in action](uwpct://Helpers?sample=ObservableGroup) in the [Windows Community Toolkit Sample App](http://aka.ms/uwptoolkitapp).

## Requirements

| Implementation | .NET Standard 2.0. |
| --- | --- |
| Namespace | Microsoft.Toolkit |
| NuGet package | [Microsoft.Toolkit](https://www.nuget.org/packages/Microsoft.Toolkit/) |

## API

* [Observable group source code](https://github.com/Microsoft/WindowsCommunityToolkit//blob/master/Microsoft.Toolkit/Collections)

## Related Topics

* [CollectionViewSource](https://docs.microsoft.com/en-us/uwp/api/Windows.UI.Xaml.Data.CollectionViewSource)
* [ListView and GridView](https://docs.microsoft.com/en-us/windows/uwp/design/controls-and-patterns/listview-and-gridview)
* [ObservableCollection\<T\>](https://docs.microsoft.com/en-us/dotnet/api/system.collections.objectmodel.observablecollection-1?view=netstandard-2.0)
* [ReadOnlyObservableCollection\<T\>](https://docs.microsoft.com/en-us/dotnet/api/system.collections.objectmodel.readonlyobservablecollection-1?view=netstandard-2.0)
* [IGrouping\<TKey,TElement\>](https://docs.microsoft.com/en-us/dotnet/api/system.linq.igrouping-2?view=netstandard-2.0)
