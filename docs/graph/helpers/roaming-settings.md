---
title: Roaming settings
author: shweaver-MSFT
description: Roam user settings across experiences using WCT's Graph powered storage helpers.
keywords: uwp, wpf, netstandard, windows, community, toolkit, graph, roaming, settings, storage, files
dev_langs:
  - csharp
---

# Roaming settings

Store and roam user settings/files across experiences and devices using Microsoft Graph powered storage helpers. These Graph storage helpers implement the `Microsoft.Toolkit.Helpers.IFileStorageHelper` and `Microsoft.Toolkit.Helpers.ISettingsStorageHelper` interfaces and work well in conjunction with the `Microsoft.Toolkit.Uwp.Helpers.ApplicationDataStorageHelper` for migrating local data to roaming storage locations.

## OneDriveStorageHelper

The `OneDriveStorageHelper` is a storage helper for handling files and folders in a user's OneDrive AppSpecial folder. This helper is purposed for storing app specific values and does not support freely navigating the user's OneDrive root folder or other app's settings folders.

Available in the `CommunityToolkit.Uwp.Graph` package.

```csharp
var filePath = "TestFile.txt";
var fileContents = "this is a test";
var fileContents2 = "this is also a test";
var storageHelper = await OneDriveStorageHelper.CreateForCurrentUserAsync();

// Create a file
await storageHelper.CreateFileAsync(filePath, fileContents);

// Read a file
var readContents = await storageHelper.ReadFileAsync<string>(filePath);
Assert.AreEqual(fileContents, readContents);

// Update a file
await storageHelper.CreateFileAsync(filePath, fileContents2);
var readContents2 = await storageHelper.ReadFileAsync<string>(filePath);
Assert.AreEqual(fileContents2, readContents2);

// Delete a file
var itemDeleted = await storageHelper.TryDeleteItemAsync(filePath);
Assert.IsTrue(itemDeleted);
```

Sub-folders are also supported:

```csharp
var folderName = "TestFolder";
var subfolderName = "TestSubFolder";
var subfolderPath = $"{folderName}/{subfolderName}";
var fileName = "TestFile.txt";
var filePath = $"{folderName}/{fileName}";
var fileContents = "this is a test";
var storageHelper = await OneDriveStorageHelper.CreateForCurrentUserAsync();

// Test preparation
await storageHelper.TryDeleteItemAsync(folderName);
await storageHelper.CreateFolderAsync(folderName);

// Create a subfolder
await storageHelper.CreateFolderAsync(subfolderName, folderName);

// Create a file in a folder
await storageHelper.CreateFileAsync(filePath, fileContents);

// Read a file from a folder
var readContents = await storageHelper.ReadFileAsync<string>(filePath);
Assert.AreEqual(fileContents, readContents);

// List folder contents
var folderItems = await storageHelper.ReadFolderAsync(folderName);
var folderItemsList = folderItems.ToList();
Assert.AreEqual(2, folderItemsList.Count());
Assert.AreEqual(subfolderName, folderItemsList[0].Name);
Assert.AreEqual(DirectoryItemType.Folder, folderItemsList[0].ItemType);
Assert.AreEqual(fileName, folderItemsList[1].Name);
Assert.AreEqual(DirectoryItemType.File, folderItemsList[1].ItemType);

// Delete a subfolder
var itemDeleted = await storageHelper.TryDeleteItemAsync(subfolderPath);
Assert.IsTrue(itemDeleted);
```

## UserExtensionStorageHelper

The `UserExtensionStorageHelper` is a storage helper that leverages open extensions on the Graph User entity to store data. Use this helper for storing user specific settings as key-value-pairs.

Available in the `CommunityToolkit.Uwp.Graph` package.

```csharp
// Create a new storage helper for the current user.
var storageHelper = await UserExtensionStorageHelper.CreateForCurrentUserAsync("my-storage-extension-id");

// Save a value
storageHelper["PreferredTheme"] = "Dark";

// Sync with Graph to update the remote.
await storageHelper.Sync();
```

### Syncing with Graph

The `UserExtensionStorageHelper` uses synchronous methods to interop and does not automatically sync data back to Graph. Use the `Sync()` method to push changes up to Graph and retrieve any new settings.

Common sync opportunities:

1. On application startup, when ready to fetch values and hydrate the cache.
1. On application suspend/resume.
1. After changing one or more settings values.

There is a known limitation with open extensions that does not allow deletion of a specific key. We suggest using a unique value to represent when a key has been deleted. To truly remove keys, the entire extension must be cleared and synced to delete the extension, then rehydrated with values and synced again.

**Sample 1. Set a default value**

```csharp
// Create a new storage helper for the current user.
var storageHelper = await UserExtensionStorageHelper.CreateForCurrentUserAsync("my-storage-extension-id");

// Individual key deletion is not supported by open extensions.
// As a workaround, save a unique value like "KEY_DELETED" on deleted keys to pseudo remove them. 
storageHelper["PreferredTheme"] = "KEY_DELETED";

// Check for a preferred theme, if not set the default.
if (!storageHelper.TryRead<string>("PreferredTheme", out string preferredTheme) || preferredTheme == "KEY_DELETED")
{
    // Set the default theme.
    preferredTheme = "Light";

    // Save a value to the storage helper cache.
    // Changes must be explicitly synced.
    storageHelper["preferredTheme"] = preferredTheme;

    // Sync with Graph push changes back up.
    await storageHelper.Sync();
}
```

**Sample 2. Delete a key**

```csharp
// Create a new storage helper for the current user.
var storageHelper = await UserExtensionStorageHelper.CreateForCurrentUserAsync("my-storage-extension-id");

// Sync to hydrate.
await storageHelper.Sync();

// Get the cache and remove the target item.
Dictionary<string, object> cache = storageHelper.Cache.ToDictionary(kvp => kvp.Key, kvp => kvp.Value);
cache.Remove("PreferredTheme");

// Call clear to mark the extension ready for deletion/recreation
storageHelper.Clear();

// Reapply the cached values
foreach (var setting in cache)
{
  storageHelper[setting.Key] = setting.Value;
}

// Sync deletion to Graph and preserve other settings values.
await storageHelper.Sync();
```

## Related Topics

* [Add custom data to users using open extensions](/graph/extensibility-open-users)