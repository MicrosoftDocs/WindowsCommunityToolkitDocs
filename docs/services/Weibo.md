---
title: Weibo service
author: validvoid
description: Learn about the Weibo Service, which allows users to retrieve or publish data to Weibo. See app setup instructions, syntax examples, and requirements.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, Weibo
dev_langs:
  - csharp
  - vb
---

# Weibo Service

> [!WARNING]
> The API has been removed and the Weibo Service is no longer available in the Windows Community Toolkit.

The **Weibo Service** allows users to retrieve or publish data to Weibo. Visit [https://open.weibo.com](https://open.weibo.com) to create a new app or manage existing apps.

## App Setup

Go to [我的应用(my apps)](https://open.weibo.com/apps) and select your app. Then click the *应用信息*(app info) tab on the left sidebar you will be able to find the following fields:

**App Key**
Copy this from the *应用基本信息*(basic information) section on your application page.

**App Secret**
Copy this from the *应用基本信息*(basic information) section on your application page.

**Secure Domains**
Due to the restriction by Weibo API, a status you post must include a url which starts with "http"/"https". You can add a url to the list of secure domains in the *应用基本信息*(basic information) section on your application page.

**Redirect URI** Enter a unique URI for your application.  This must match the *Redirect URL* field in the *OAuth2.0 授权设置*(OAuth 2.0 Authorization Settings) section on the *高级信息*(advanced Info) page. You can visit the page by clicking on the left sidebar.
*Example*: `https://myapp.company.com` - (this does not have to be a working URL)

## Example Syntax

```csharp
// Initialize service
WeiboService.Instance.Initialize(AppKey, AppSecret, RedirectUri);

// Login to Weibo
if (!await WeiboService.Instance.LoginAsync())
{
    return;
}

// Get current user info
var user = await WeiboService.Instance.GetUserAsync();

// Get user timeline
ListView.ItemsSource = await WeiboService.Instance.GetUserTimeLineAsync(user.ScreenName, 50);

// Post a status
await WeiboService.Instance.PostStatusAsync(StatusText.Text);

// Post a status with a picture
await WeiboService.Instance.PostStatusAsync(StatusText.Text, stream);

```

```vb

' Initialize service
WeiboService.Instance.Initialize(AppKey, AppSecret, RedirectUri)

' Login to Weibo
If Not Await WeiboService.Instance.LoginAsync() Then
    Return
End If

' Get current user info
Dim user = Await WeiboService.Instance.GetUserAsync()

' Get user timeline
ListView.ItemsSource = Await WeiboService.Instance.GetUserTimeLineAsync(user.ScreenName, 50)

' Post a status
Await WeiboService.Instance.PostStatusAsync(StatusText.Text)

' Post a status with a picture
Await WeiboService.Instance.PostStatusAsync(StatusText.Text, stream)
  
```
