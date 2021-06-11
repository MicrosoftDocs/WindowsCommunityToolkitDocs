---
title: WindowsProvider
author: shweaver-MSFT
description: Lightweight IProvider implementation that enables authentication using native Windows Account Manager APIs (WAM).
keywords: uwp, netstandard, windows, community, toolkit, graph, login, authentication, provider, providers, identity, wam, msa
dev_langs:
  - csharp
---

# WindowsProvider

The WindowsProvider is an authentication provider for accessing locally configured accounts on Windows.
It extends [IProvider](./custom.md) and uses the native Windows AccountManager (WAM) APIs and AccountsSettingsPane for sign in.

> Available in the `CommunityToolkit.Authentication.Uwp` package.

> [!IMPORTANT]
> Windows Community Toolkit - Graph Controls and Helpers packages are in preview. To get started using WCT preview packages visit the [WCT Preview Packages wiki page](https://aka.ms/wct/wiki/previewpackages).

## Prerequisite Windows Store Association in Visual Studio

To get valid tokens and complete sign in, the app will need to be associated with the Microsoft Store. This will enable your app to authenticate consumer MSA accounts without any additional configuration.

1. In Visual Studio Solution Explorer, right-click the UWP project, then select **Store -> Associate App with the Store...**

2. In the wizard, click **Next**, sign in with your Windows developer account, type a name for your app in **Reserve a new app name**, then click **Reserve**.

3. After completing the app registration, select the new app name, click **Next**, and then click **Associate**. This adds the required Windows Store registration information to the application manifest.

> [!NOTE]
> You must have a Windows Developer account to use the WindowsProvider in your UWP app. You can [register a Microsoft developer account](https://developer.microsoft.com/store/register) if you don't already have one.

<!-- Uncomment this when AAD account support becomes available.
## Prerequisite Configure Client Id in Partner Center

If your product integrates with Azure AD and calls APIs that request either application permissions or delegated permissions that require administrator consent, you will also need to enter your Azure AD Client ID in Partner Center:

https://partner.microsoft.com/en-us/dashboard/products/&lt;YOUR-APP-ID&gt;/administrator-consent

This lets administrators who acquire the app for their organization grant consent for your product to act on behalf of all users in the tenant.

> [!NOTE]
> You only need to specify the client id if you need admin consent for delegated permissions from your AAD app registration. Simple authentication for public accounts does not require a client id or any additional configuration.

> [!IMPORTANT]
> Be sure to Register Client Id in Azure first following the guidance here: <https://docs.microsoft.com/azure/active-directory/develop/quickstart-register-app>
>
> After finishing the initial registration page, you will also need to add an additional redirect URI. Click on "Add a Redirect URI" and add the value retrieved from running `WindowsProvider.RedirectUri`.
>
> You'll also want to set the toggle to true for "Allow public client flows".
>
> Then click "Save".
-->

## Syntax

The WindowsProvider can be used in just one line of code:

```csharp
using CommunityToolkit.Authentication;

// Easily create a new WindowsProvider instance and set the GlobalProvider.
// Don't forget to associate your app with the Microsoft Store before attempting sign in.
ProviderManager.Instance.GlobalProvider = new WindowsProvider(new string[] { "User.Read", "Tasks.ReadWrite" });
```

The WindowsProvider can also be configured to disabled auto-signin or show custom content in the `AccountsSettingsPane`.
Additional configuration for account types will be available via the `WebAccountProviderConfig` object in the future.
Currently, only consumer MSA accounts are supported. 

```CSharp
using CommunityToolkit.Authentication;

// Provider config
string[] scopes = { "User.Read", "People.Read", "Calendars.Read", "Mail.Read" };

// Additional parameters are also available,
// such as custom settings commands for the AccountsSettingsPane.
Guid settingsCommandId = Guid.NewGuid();
void OnSettingsCommandInvoked(IUICommand command)
{
    System.Diagnostics.Debug.WriteLine("AccountsSettingsPane command invoked: " + command.Id);
}

// Configure which types accounts should be available to choose from. The default is MSA, but AAD will come in the future.
// ClientId is only required for approving admin level consent in AAD tenants.
var webAccountProviderConfig = new WebAccountProviderConfig(WebAccountProviderType.MSA, "YOUR_CLIENT_ID_HERE");

// Configure details to present in the AccountsSettingsPane, such as custom header text and links.
var accountsSettingsPaneConfig = new AccountsSettingsPaneConfig(
    headerText: "Custom header text",
    commands: new List<SettingsCommand>()
    {
        new SettingsCommand(settingsCommandId: settingsCommandId, label: "Click me!", handler: OnSettingsCommandInvoked)
    });

// Determine it the provider should automatically sign in or not. Default is true.
// Set to false to delay silent sign in until SignInAsync or TrySilentSignInAsync is called.
bool autoSignIn = false;

// Set the GlobalProvider with the extra configuration
ProviderManager.Instance.GlobalProvider = new WindowsProvider(scopes, accountsSettingsPaneConfig, webAccountProviderConfig, autoSignIn);
```

## Constructor

| Parameter | Type | Default | Description |
| -- | -- | -- | -- |
| scopes | string[] | null | List of scopes to initially request. |
| webAccountProviderConfig | WebAccountProviderConfig? | null | Configuration value for determining the available web account providers. |
| accountsSettingsPaneConfig | AccountsSettingsPaneConfig? | null | Configuration values for the AccountsSettingsPane. |
| autoSignIn | bool | true | Determines whether the provider attempts to silently log in upon instantiation. |

## Properties

| Property | Type | Description |
| -- | -- | -- |
| State | ProviderState | Gets the current authentication state of the provider. |
| Scopes | string[] | List of scopes to pre-authorize on the user during authentication. |
| WebAccountsProviderConfig | WebAccountProviderConfig | configuration values for determining the available web account providers. |
| AccountsSettingsPaneConfig | AccountsSettingsPaneConfig | Configuration values for the AccountsSettingsPane, shown during authentication. |
| RedirectUri | string | Static getter for retrieving a customized redirect uri to put in the Azure app registration. |

## Events

| Event | Type | Description |
| -- | -- | -- |
| StateChanged | EventHandler&lt;ProviderStateChangedEventArgs&gt; | Event called when the provider state changes. |

## Methods

| Method | Arguments | Returns | Description |
| -- | -- | -- | -- |
| AuthenticateRequestAsync | HttpRequestMessage | Task | Authenticate an outgoing request. |
| GetTokenAsync | bool silentOnly = true, string[] scopes = null | Task&lt;string&gt; | Retrieve a token for the authenticated user. |
| SignInAsync | | Task | Sign in a user. |
| SignOutAsync | | Task | Sign out the current user. |
| TrySilentSignInAsync | | Task&lt;bool&gt; | Try signing in silently, without prompts. |

## AccountsSettingsPaneConfig Object

| Property | Type | Description |
| -- | -- | -- |
| HeaderText | string | Gets or sets the header text for the accounts settings pane. |
| Commands | IList&lt;SettingsCommand&gt; | Gets or sets the SettingsCommand collection for the account settings pane. |

## WebAccountProviderConfig Object

| Property | Type | Description |
| -- | -- | -- |
| ClientId | string | Client Id obtained from Azure registration. |
| WebAccountProviderType | WebAccountProviderType | The types of accounts providers that should be available to the user. |

### WebAccountProviderType Enum

| Name | Description |
| -- | -- |
| All | Enable authentication of all available account types. |
| MSA | Enable authentication of public/consumer MSA accounts. |
