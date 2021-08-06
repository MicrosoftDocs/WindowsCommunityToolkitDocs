---
title: Object Serializer
author: simop
description: IObjectSerializer is an interface that you can implement to provide a serializer of your choice to ObjectStorageHelper.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, serialization
dev_langs:
  - csharp
  - vb
---

# ObjectSerializer

You should implement IObjectSerializer when you need to write data using this toolkit's helpers with a custom serializer. If you don't, a default JSON serializer will be used otherwise.

## Methods

| Methods | Return Type | Description |
|---------|-------------|-------------|
| Serialize\<T>(T)        | object | Serialize an object of type T into a object. |
| Deserialize\<T>(object) | T      | Deserialize a object to an object of type T. |

## Examples

### System.Text.Json

```cs
using Microsoft.Toolkit.Uwp.Helpers;
using System.Text.Json;

namespace Contoso.Helpers
{
    public class SystemTextJsonObjectSerializer : IObjectSerializer
    {
        public object Serialize<T>(T value) => JsonSerializer.Serialize(value);

        public T Deserialize<T>(object value) => JsonSerializer.Deserialize<T>((string)value);
    }
}
```

### Json.NET

```csharp
using Microsoft.Toolkit.Uwp.Helpers;
using Newtonsoft.Json;

namespace Contoso.Helpers
{
    public class JsonNetObjectSerializer : IObjectSerializer
    {
        // Specify your serialization settings
        private readonly JsonSerializerSettings settings = new JsonSerializerSettings();

        public object Serialize<T>(T value) => JsonConvert.SerializeObject(value, typeof(T), Formatting.Indented , settings);

        public T Deserialize<T>(object value) => JsonConvert.DeserializeObject<T>((string)value, settings);
    }
}
```

### DataContract

```csharp
using Microsoft.Toolkit.Uwp.Helpers;
using System.IO;
using System.Runtime.Serialization;
using System.Xml;

namespace Contoso.Helpers
{
    public class DataContractObjectSerializer : IObjectSerializer
    {
        // Specify your serialization settings
        private readonly DataContractSerializerSettings settings = new DataContractSerializerSettings();

        public object Serialize<T>(T value)
        {
            var serializer = new DataContractSerializer(typeof(T), settings);

            using (var stringWriter = new StringWriter())
            using (var xmlWriter = XmlWriter.Create(stringWriter))
            {
                serializer.WriteObject(xmlWriter, value);
                return stringWriter.ToString();
            }
        }

        public T Deserialize<T>(object value)
        {
            var serializer = new DataContractSerializer(typeof(T), settings);

            using (var stringReader = new StringReader((string)value))
            using (var xmlReader = XmlReader.Create(stringReader))
            {
                return (T)serializer.ReadObject(xmlReader);
            }
        }
    }
}
```

## Requirements

| Device family | Universal, 10.0.16299.0 or higher |
| --- | --- |
| Namespace | Microsoft.Toolkit.Uwp |
| NuGet package | [Microsoft.Toolkit.Uwp](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp/) |

## API

* [IObjectSerializer source code](https://github.com/windows-toolkit/WindowsCommunityToolkit/blob/rel/7.0.0/Microsoft.Toolkit.Uwp/Helpers/ObjectStorage/IObjectSerializer.cs)

## Related topics

* [ObjectStorage](./objectstorage.md)
