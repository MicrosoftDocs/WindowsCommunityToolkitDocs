---
title: LoginButton XAML Control
author: michael-hawker
description: The LoginButton control facilitates Microsoft Identity platform authentication.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, login, loginbutton, graph
dev_langs:
  - csharp
---

# LoginButton XAML Control

The LoginButton is both a button and flyout control to facilitate Microsoft identity platform authentication. It provides two states:

* When the user is not signed in, the control is a simple button to initiate the sign in process.
* When the user is signed in, the control displays the current signed in user name, profile image, and email. When clicked, a flyout is opened with a command to sign out.

Available in the `CommunityToolkit.Graph.Uwp` package.

## Syntax

```xml
<Grid xmlns:controls="using:CommunityToolkit.Graph.Uwp.Controls">
    <controls:LoginButton />
</Grid>
```

## Sample Output

![LoginButton Control](../../resources/images/Graph/Controls/LoginButton.png)

## Properties

| Property | Type | Description |
| -- | -- | -- |
| UserDetails | User | Gets or sets details about this person retrieved from the graph or provided by the developer. |
| IsLoading | bool | Indicates if the control is loading and hasn't established a sign-in state. |

## Events

| Events | Description |
| -- | -- |
| LoginInitiated | The user clicked the sign in button to start the login process. |
| LoginCompleted | The login process was successful and the user is now signed in. |
| LoginFailed | The user canceled the login process or was unable to sign in. |
| LogoutInitiated | The user started to logout. |
| LogoutCompleted | The user signed out. |

## Requirements

* **Namespace:** CommunityToolkit.Graph.Uwp.Controls
* **NuGet package:** [CommunityToolkit.Graph.Uwp](https://www.nuget.org/packages/CommunityToolkit.Graph.Uwp)
* **Scope:** `User.Read`

## API

* [LoginButton source code](https://github.com/windows-toolkit/Graph-Controls/tree/dev/7.1.0/CommunityToolkit.Graph.Uwp/Controls/LoginButton)

## Related Topics

* [User Graph API](/graph/api/resources/user)
* [MGT Login Component](/graph/toolkit/components/login)
