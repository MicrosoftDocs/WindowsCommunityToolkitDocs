---
title: Gaze Controls
author: harishsk
description: The Gaze Controls library contains a set of reusable controls to make it easier to build gaze enabled apps. This library is built on top of the Gaze Interaction Library that is also part of the toolkit.
keywords: windows 10, uwp, uwp community toolkit, uwp toolkit, windows community toolkit, gaze, eye gaze, gaze input, gaze interaction, eye tracking, eye tracker, gaze controls
dev_langs:
  - csharp
---

# Gaze Controls

Eye gaze as a form of input is similar to mouse, pen and touch in the sense that it provides a stream of coordinates that the user is looking at. But when it is actually used for input and interaction in applications, the design considerations are significantly different.

Eye gaze is less precise than pen, touch and mouse. The measurement errors are larger due to lighting and environmental conditions. There is a larger variance among user populations. There is a diversity in the quality and calibration accuracy among different trackers. When these factors are considered, it becomes apparent that a user interface designed for mouse, pen or touch cannot be directly used for effective eye gaze interaction. Just as user interfaces originally designed for mouse were modified to suit touch interaction, we need to modify the existing user interfaces to be compatible with eye gaze input.

The GazeControls library, built on the [GazeInteraction Library](https://github.com/MicrosoftDocs/WindowsCommunityToolkitDocs/blob/master/docs/gaze/GazeInteractionLibrary.md),  includes a set of user controls that can be reused in different applications with eye gaze input. Instead of trying to design controls for all forms of input simultaneously these set of controls are designed primarily for eye gaze input.

## Prerequisites

Since the GazeControls library is built on top of the GazeInteraction library, the first set of prerequisites are the same as the [prerequisites for the GazeInteraction library](https://github.com/MicrosoftDocs/WindowsCommunityToolkitDocs/blob/master/docs/gaze/GazeInteractionLibrary.md#prerequisites).

There are additional prerequisites for each of the controls and they are listed below in the context of the documentation for the specific control.

## Supported controls

The library currently supports the following user controls.

* GazeKeyboard
* GazeFilePicker

## GazeKeyboard

One of the most common uses of eye gaze input is by users with mobility impairments. And the most common task in such scenarios is text input, especially if the user also has a speech impairment, like in the case of users with ALS. Text input with eye gaze is particularly challenging for an assorted set of users. One aspect of that challenge is that it is impossible to design an optimal keyboard layout that works for all users in all occasions. The GazeKeyboard control in this library is intended to address this problem by making it easy to define new keyboard layouts and include them in your gaze application.

### GazeKeyboard Prerequsites

The GazeKeyboard control provides a way to define custom keyboard layouts (including styling) and injects the specific key the user dwells on into the application. To perform the key injection, it relies on the `inputInjectionCapability`. Please make sure to add this capability to your application's `Package.appxmanifest` as follows:

```
<Capabilities>
   <DeviceCapability Name="inputInjectionCapability" />
</Capabilities>
```

The application should also add a reference to the [GazeInteraction library nuget](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Input.GazeInteraction/).

### Builtin layouts

The `GazeKeyboard` control comes built in with three layouts.

* **MinAAC.** This layout defines the minimal possible English layout to enable an AAC (Augmentative and Assistive Communication) application. It simply contains English alphabet and a few editing keys.
* **FullKeyboard.** This layout supports all the keys for a full hardware keyboard and also some features found on a software only keyboard, like emojis. It short it is an example of all the features supported by the `GazeKeyboard` control.
* **TwoStageKeyboard.** This unique feature shows off a way to still support text entry even when the gaze accuracy is extraordinarily low. It takes a minimum of two button presses to enter one alphabet. But it shows how to define a custom layout and support text entry as long as the user can reliably gaze on a four by four grid of buttons on the screen.

(In the source code, you will see a fourth keyboard layout named `FilenameEntry`. This layout is for use by the `GazeFilePicker` dialog.)

To use any of the above layouts, please do the following:

* Add the library namespace to the XAML page as follows:

  ```
  <Page
    ...
    xmlns:gc="using:Microsoft.Toolkit.Uwp.Input.GazeControls"
    ...
    >
  ```

* Reserve a space in your layout for the gaze keyboard and instantiate the keyboard there.

  ```
    <Grid>
        <Grid.RowDefinitions>
            <RowDefinition />
            <RowDefinition />
        </Grid.RowDefinitions>
    <gc:GazeKeyboard x:Name="GazeKeyboard" Grid.Row="1"  
                     LayoutUri="ms-appx:///Microsoft.Toolkit.Uwp.Input.GazeControls/KeyboardLayouts/MinAAC.xaml" />
        
    </Grid>
  ```

### Custom layouts - Simple

You can also define your own custom layouts, include it in your application and change the layouts on the fly by assigning the `LayoutUri` property of the keyboard control to the URI of your custom keyboard layout as shown above.

Custom layouts are specified directly using XAML and a few attached properties that dictate their behavior. The best way to create new layouts, is to use one of the built-in layouts as a starting point and copy and modify them to your own needs.

The behavior of the button when it is clicked is governed by a few rules:

* The top-level element must be a `Grid`. (In the simple case, having a name for the `Grid` is optional.)
* All the styling for the buttons must be contained within the same XAML file in one of the `Resources` sections.
* All the layout elements must be subclasses of `ButtonBase`.
* If a button only has the `Content` property defined, then the content string is injected into the application. E.g., if you have a button defined as `<Button Content="p" />` the `p` key injected when the button is pressed. (This example has been shortened for brevity. In principle, you can add any other `Button` related property like `Grid.Row`, `Style` etc.)
* If a button also has a `VK` property defined, then the `Content` property only determines the appearance of the button. The integer value of the `VK` property is injected when the button is pressed. In the example below, a backspace key is injected when the button is pressed.

  ```
  <Button Style="{StaticResource Symbol}" Content="&#xE750;" k:GazeKeyboard.VK="8"/>
  ```

* If a button has the `VKList` property, the control expects a set of virtual key codes as `Int32` values and injects that list of keys in sequence. E.g. in `MinAAC.xaml` you can see the `VKList` property assigned for clearing the textbox as follows.

  ```
    <Button Grid.Row="2" Grid.Column="9" Style="{StaticResource Symbol}" Content="&#xE74D;">
        <k:GazeKeyboard.VKList>
            <x:Int32>17</x:Int32> <!-- VK_CONTROL -->
            <x:Int32>65</x:Int32> <!-- VK_A -->
            <x:Int32>8</x:Int32>  <!-- VK_BACK -->
            <x:Int32>8</x:Int32>  <!-- VK_BACK -->
            <x:Int32>65</x:Int32> <!-- VK_A -->
            <x:Int32>17</x:Int32> <!-- VK_CONTROL -->
        </k:GazeKeyboard.VKList>
    </Button>
  ```

  In the above example, when this button is pressed, it injects the following sequence of keys:

  * Control key down
  * A key down
  * Backspace key down
  * Backspace key up
  * A key up
  * Control key up

  As you can see, if a key occurs twice in the list, the first is interpreted as a down key, and the second as an up key.

### Custom layouts - Advanced

When the number of keys in the layout is larger than what the application can display (and still have space left over for the actual application needs), it can choose to split up the layout into multiple pages. When this is done, the XAML layout for the custom layout should follow the rules below:

* The top level `Grid` should have a name specified with `x:Name` property.
* There should be a `GazeKeyboard.PageList` in the layout. This node should include a list of strings that specify the names of other `Grid` notes, which define the separate pages in the layout. The example below is taken from `FullKeyboard.xaml`

  ```
    <k:GazeKeyboard.PageList>
        <x:String>MainPage</x:String>
        <x:String>UppercasePage</x:String>
        <x:String>NumbersPage</x:String>
        <x:String>EmojiPage</x:String>    
    </k:GazeKeyboard.PageList>
  ```

  The layout parser now expects to find four different `Grid` nodes with the names of `MainPage`, `UppercasePage`, `NumbersPage` and `EmojiPage`.
* Only the main layout grid should have its `Visibility` property set to `Visible` and all the other pages should have it set to `Collapsed`.
  
* **Changing pages**. In order to load a new layout when a particular button on the current layout is pressed, the button should include the `GazeKeyboard.NewPage` property and set the value to the name of one of pages specified in the `PageList` property.  In the following example, keyboard layout changes to the `NumbersPage` when the button is pressed.

  ```
  <Button Content="123" k:GazeKeyboard.PageContainer="FullKeyboard" k:GazeKeyboard.NewPage="NumbersPage"/>
  ```

* **TemporaryPages**. The `GazeKeyboard`'s layout engine supports the notion of temporary pages. A temporary page takes over the layout when a button defines `GazeKeyboard.TemporaryPage` property and sets the value to one of the pages found the in the `PageList` property. When any button is pressed even once on the temporary page, the visible page layout immediately transitions back to the previous layout. This mechanism is used to support changing the keyboard layout to upper case when the `Shift` key is pressed and to also support two stage keyboard layouts. When a button defines a `GazeKeyboard.TemporaryPage` property it also needs to define `GazeKeyboard.PageContainer` property to inform the layout engine as to which page layout to load back. The example below, illustrates this.

  ```
  <Button Style="{StaticResource Symbol}" Content="&#xE752;" k:GazeKeyboard.PageContainer="FullKeyboard" k:GazeKeyboard.TemporaryPage="UppercasePage" />
  ```

* **Unicode keys**. If a unicode character is to be injected, the button should specify the `GazeKeyboard.Unicode` property and set its value to the Unicode character to inject as shown in the example below.

  ```
  <Button Style="{StaticResource Alpha}" Content="&#x1f600;" k:GazeKeyboard.Unicode="&#x1f600;"/>
  ```

### GazeKeyboard Properties

| Property | Type | Description |
| -- | -- | -- |
| Target | TextBox | Gets or sets the target text box for injecting keys |
| PredictionLanguage | string | Gets or sets the text prediction language |
| LayoutUri | Uri | Gets or sets the URI of the layout file for the keyboard |
| PredictionTargets | Button[] | Gets or sets the prediction targets buttons. When text prediction is available, the content of the buttons it set to the prediction text. |

## GazeFilePicker

The GazeFilePicker provides a gaze optimized subset of the features of the full OS native file picker dialog. Since this control needs to enumerate the file system, appropriate capabilities need to be declared in the `Package.appxmanifest` file in the application that uses this control. E.g. if an application is going to access the documents folders, then the application needs to add the following line to the `<Capabilities>` sectioni of `Package.appxmanifest`.

```
<Capabilities>
  <DeviceCapability Name="documentsLibrary"/>
</Capabilities>
```

### Features

The GazeFilePicker dialog supports the following features:

* Enumerate files and folders in the directories the application has permission to access and display them in a gaze friendly large icon view.
* Ability to navigate folders using gaze or gaze + switch.
* Ability to set the file filter type to show only the files matching a specific set of extensions.
* Ability to define a set of folders as "favorite" starting points for the application
* A gaze friendly scroll bar.
* When the GazeFilePicker is used in save mode, it supports creating new folders and allows specifying a new filename using a gaze friendly keyboard.

### Sample Code

The following sample code illustrates how to use the GazeFilePicker dialog for file-open and file-save operations.

```
private async void OnFileOpen(object sender, RoutedEventArgs e)
{
    var file = await ShowFilePicker(false);
    _textControl.Text = await FileIO.ReadTextAsync(file);
}

private async void OnFileSave(object sender, RoutedEventArgs e)
{
    var file = await ShowFilePicker(true);
    await FileIO.WriteTextAsync(file, _textControl.Text);
}

private async Task<StorageFile> ShowFilePicker(bool saveMode)
{
    var picker = new GazeFilePicker();
    var library = await StorageLibrary.GetLibraryAsync(KnownLibraryId.Documents);
    picker.CurrentFolder = library.SaveFolder;
    picker.FileTypeFilter.Add(".txt");
    picker.FileTypeFilter.Add(".log");
    picker.SaveMode = saveMode;
    await picker.ShowAsync();
    return picker.SelectedItem;
}
```

### GazeFilePicker Properties

| Property | Type | Description |
| -- | -- | -- |
| CurrentFolder | StorageFolder | Gets or sets the current folder for the file picker dialog |
| Favorites | List\<StorageFolder\> | Gets or sets the list of storage folders that appear as shortcuts on top of the folder view |
| FileTypeFilter | List\<string\> | Gets or sets the collection of file types that the file open picker displays. |
| SaveMode | bool | Gets or sets a value indicating whether this is FileSave dialog or a FileOpen dialog |
| SelectedItem | StorageFile | Gets the currently selected file in the dialog as a StorageFile |

## Sample Project

[GazeControlsPage](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.0.0/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/GazeControls/). You can [see this in action](uwpct://Gaze?sample=GazeControls) in the [Windows Community Toolkit Sample App](https://aka.ms/windowstoolkitapp).

## Requirements

| Device family | Universal,10.0.17134.1 or higher   |
| -- | -- |
| Namespace | Microsoft.Toolkit.Uwp.Input.GazeControls |
| NuGet package | [NuGet package](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.Input.GazeControls/) |

## API

* [Gaze Controls Library source code](https://github.com/windows-toolkit/WindowsCommunityToolkit/tree/rel/7.0.0/Microsoft.Toolkit.Uwp.Input.GazeControls)

## Related Topics

* [Windows 10 Gaze Input APIs](/uwp/api/windows.devices.input.preview)
