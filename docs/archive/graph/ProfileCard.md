---
title: ProfileCard Control
author: OGcanviz
description: The ProfileCard Control is a simple way to display a user in multiple different formats and mixes of name/image/e-mail (outdated docs).
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, ProfileCard Control
---

# ProfileCard Control

> [!WARNING]
> (This API has been removed. For the latest guidance on using the Microsoft Graph see the [PersonView](../../graph/controls/PersonView.md).)

The [ProfileCard Control](/dotnet/api/microsoft.toolkit.uwp.ui.controls.graph.profilecard) is a simple way to display a user in multiple different formats and mixes of name/image/e-mail, it relies on the [MicrosoftGraphService](../../services/MicrosoftGraph.md) for authentication.

## Syntax

```xaml
<Page ...
    xmlns:controls="using:Microsoft.Toolkit.Uwp.UI.Controls.Graph"/>

<controls:ProfileCard x:Name="ProfileCard1"
    UserId="xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
    DisplayMode="PictureOnly" />
```

## Example Image

![ProfileCard animation](../../resources/images/Graph/ProfileCard.png)

## Properties

| Property | Type | Description |
| -- | -- | -- |
| RequiredDelegatedPermissions | String[] | Gets required delegated permissions for Graph API access |
| UserId | String | Identifier of the user being displayed, this user id can come from the Graph APIs like `/me/people`, `/users`, etc. |
| DisplayMode | [ViewType](https://github.com/windows-toolkit/WindowsCommunityToolkit/blob/rel/7.0.0/Microsoft.Toolkit.Uwp.UI.Controls.Graph/ProfileCard/ViewType.cs) | The visual layout of the control. Default is `PictureOnly` |
| DefaultImage | BitmapImage | The default image displayed when no user is signed in |
| LargeProfileTitleDefaultText | String | Default title text in LargeProfilePhotoLeft mode or LargeProfilePhotoRight mode when no user is signed in |
| LargeProfileMailDefaultText | String | Default secondary mail text in LargeProfilePhotoLeft mode or LargeProfilePhotoRight mode when no user is signed in |
| NormalMailDefaultText | String | Default mail text in EmailOnly mode when no user is signed in |

## Sample Code

First of all, initialize the [MicrosoftGraphService](../../services/MicrosoftGraph.md) with your [Azure AD v2.0 app](/azure/active-directory/develop/active-directory-v2-app-registration), this should be done globally with the combined and unique [delegate permissions](/azure/active-directory/develop/active-directory-v2-scopes) required by all Graph controls and services used in your app.

```csharp
MicrosoftGraphService.Instance.AuthenticationModel = MicrosoftGraphEnums.AuthenticationModel.V2;

MicrosoftGraphService.Instance.Initialize(
    "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    MicrosoftGraphEnums.ServicesToInitialize.UserProfile,
    ProfileCard.RequiredDelegatedPermissions
);
```

The sign in will be processed by the [AadLogin](AadLogin.md) control, however, you could do sign in with the following alternatively.

```csharp
await MicrosoftGraphService.Instance.LoginAsync();
```

[ProfileCard Sample Page Source](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.0.0/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/ProfileCard). You can [see this in action](uwpct://Controls?sample=ProfileCard) in the [Windows Community Toolkit Sample App](https://aka.ms/windowstoolkitapp).

## Default Template

[ProfileCard XAML File](https://github.com/windows-toolkit/WindowsCommunityToolkit/blob/rel/7.0.0/Microsoft.Toolkit.Uwp.UI.Controls.Graph/ProfileCard/ProfileCard.xaml) is the XAML template used in the toolkit for the default styling.

## Requirements

| Device family | Universal, 10.0.16299.0 or higher |
| -- | -- |
| Namespace | Microsoft.Toolkit.Uwp.UI.Controls.Graph |
| NuGet package | [Microsoft.Toolkit.Uwp.UI.Controls.Graph](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI.Controls.Graph/) |
