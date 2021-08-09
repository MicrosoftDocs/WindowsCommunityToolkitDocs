---
title: HttpHelperResponse
author: nmetulev
description: HttpHelperResponse is a Windows Community Toolkit helper class used with the HttpHelper class to read http responses (outdated docs).
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, HttpHelperResponse
dev_langs:
  - csharp
  - vb
---

# HttpHelperResponse

> [!WARNING]
> (This API is obsolete and has been removed. Please use [System.Net.Http.HttpResponseMessage](/dotnet/api/system.net.http.httpresponsemessage)
> or [Windows.Web.Http.HttpResponseMessage](/uwp/api/Windows.Web.Http.HttpResponseMessage) directly)

[HttpHelperResponse](/dotnet/api/microsoft.toolkit.uwp.httphelperresponse) represents an HTTP response message including headers.

## Sample

```csharp
using (HttpHelperResponse response = await HttpHelper.Instance.SendRequestAsync(request))
{
    await response.GetTextResultAsync();
}
```

```vb
Using response = Await HttpHelper.Instance.SendRequestAsync(request)
    Await response.GetTextResultAsync()
End Using
```

## Constructors

The **HttpHelperResponse** class has these constructors.

| Constructor | Description |
| ----------  | ----------- |
| HttpHelperResponse([HttpResponseMessage](/uwp/api/Windows.Web.Http.HttpResponseMessage))  | Initializes an instance of the HttpHelperRequest class with supplied HttpHelperResponse. |

## Properties

| Property | Type | Description |
| -------- | ----------- | ----------- |
| Content | IHttpContent | Gets the HTTP content return from the server |
| Headers | HttpResponseHeaderCollection | Gets the collection of HTTP response headers associated with the response that were sent by the server |
| StatusCode | HttpStatusCode | Gets the status code of the response |
| Success | bool | Gets a value that indicates whether the response was successful |

## Methods

|        Methods         |    Return Type     |                                     Description                                     |
|------------------------|--------------------|-------------------------------------------------------------------------------------|
|       Dispose()        |        void        | Performs tasks associated with freeing, releasing, or resetting unmanaged resources |
| GetStreamResultAsync() | Task\<IInputStream> |              Reads the Content as stream and returns it to the caller               |
|  GetTextResultAsync()  |    Task\<string>    |         Serialize the HTTP content to a String as an asynchronous operation         |
|       ToString()       |       string       |       Returns a string that represents the current HttpHelperResponse object        |

## Remarks

The **HttpHelperResponse** class contains headers and potentially data.
An app receives an instance of **HttpHelperResponse** when it creates an instance of **HttpHelperRequest** and passes it to the **HttpHelper.SendRequestAsync** method.

## Example

```csharp
using (var request = new HttpHelperRequest(new Uri(twitterUrl), HttpMethod.Post))
{
    using (var response = await HttpHelper.Instance.SendRequestAsync(request))
    {
        return await response.GetTextResultAsync();
    }
}
```

```vb
Using request = New HttpHelperRequest(New Uri(twitterUrl), HttpMethod.Post)
    Using response = Await HttpHelper.Instance.SendRequestAsync(request)
        Return Await response.GetTextResultAsync()
    End Using
End Using
```

## Requirements

| [Device family | Universal, 10.0.16299.0 or higher |
| --- | --- |
| Namespace | Microsoft.Toolkit.Uwp |
| NuGet package | [Microsoft.Toolkit.Uwp](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp/) |

## API

* [HttpHelperResponse source code](https://github.com/windows-toolkit/WindowsCommunityToolkit/blob/rel/7.0.0/Microsoft.Toolkit.Uwp/Helpers/HttpHelper/HttpHelperResponse.cs)
