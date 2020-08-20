---
title: RSS Parser
author: michael-hawker
description: The RSS Parser allows you to parse an RSS content String into an RSS Schema.
keywords: windows community toolkit, uwp community toolkit, uwp toolkit, microsoft community toolkit, microsoft toolkit, rss, rss parsing, parser
dev_langs:
  - csharp
  - vb
---

# RSS Parser

The Toolkit RssParser has been removed. Code should be migrated to use the [System.ServiceModel.Syndication](https://docs.microsoft.com/dotnet/api/system.servicemodel.syndication) API instead.

This document will show you how to migrate over to the .NET Standard library API.

## Migration Steps

1. Remove the `Microsoft.Toolkit.Parsers` package.
2. Add the `System.ServiceModel.Syndication` package.
3. Replace `HttpClient` + `GetStringAsync` with `XmlReader.Create`.
4. Replace `RssParser` + `Parse` with `SyndicationFeed.Load`.
5. Append `.Text` to any element properties retrieved.

## Toolkit Example

```csharp
public async void ParseRSS()
{
    string feed = null;

    using (var client = new HttpClient())
    {
        try
        {
            feed = await client.GetStringAsync("https://visualstudiomagazine.com/rss-feeds/news.aspx");
        }
        catch { } // TODO: Deal with unavailable resource.
    }

    if (feed != null)
    {
        var parser = new RssParser();
        var rss = parser.Parse(feed);

        foreach (var element in rss)
        {
            Console.WriteLine($"Title: {element.Title}");
            Console.WriteLine($"Summary: {element.Summary}");
        }
    }
}
```
```vb
Public Async Sub ParseRSS()
    Dim feed As String = Nothing
    Using client = New HttpClient()
        Try
            feed = Await client.GetStringAsync("https://visualstudiomagazine.com/rss-feeds/news.aspx")
        Catch
        End Try
    End Using

    If feed IsNot Nothing Then
        Dim parser = New RssParser()
        Dim rss = parser.Parse(feed)
        For Each element In rss
            Console.WriteLine($"Title: {element.Title}")
            Console.WriteLine($"Summary: {element.Summary}")
        Next
    End If
End Sub
```

## .NET Example

```cs
public void ParseRSSdotnet()
{
    SyndicationFeed feed = null;

    try
    {
        using (var reader = XmlReader.Create("https://visualstudiomagazine.com/rss-feeds/news.aspx"))
        {
            feed = SyndicationFeed.Load(reader);
        }
    }
    catch { } // TODO: Deal with unavailable resource.

    if (feed != null)
    {
        foreach (var element in feed.Items)
        {
            Console.WriteLine($"Title: {element.Title.Text}");
            Console.WriteLine($"Summary: {element.Summary.Text}");
        }
    }
}
```
```vb
Public Sub ParseRSSdotnet()
    Dim feed As SyndicationFeed = Nothing
    Try
        Using reader = XmlReader.Create("https://visualstudiomagazine.com/rss-feeds/news.aspx")
            feed = SyndicationFeed.Load(reader)
        End Using
    Catch
    End Try
    
    If feed IsNot Nothing Then
        For Each element In feed.Items
            Console.WriteLine($"Title: {element.Title.Text}")
            Console.WriteLine($"Summary: {element.Summary.Text}")
        Next
    End If
End Sub
```

## Related Topics

* [SyndicationFeed Class](https://docs.microsoft.com/dotnet/api/system.servicemodel.syndication.syndicationfeed)
