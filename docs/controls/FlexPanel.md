---
title: FlexPanel 
author: baskren
description: A panel based on the CSS Flexible Box Layout Module, commonly known as flex layout or flex-box, so called because it includes many flexible options to arrange children within the layout.
keywords: windows 10, uwp, windows community toolkit, uwp community toolkit, uwp toolkit, FlexPanel
dev_langs:
  - csharp
---
 
# FlexPanel
 
The [FlexPanel](https://docs.microsoft.com/dotnet/api/microsoft.toolkit.uwp.ui.controls.flexpanel) is based on the [CSS Flexible Box Layout Module](https://www.w3.org/TR/css-flexbox-1/), commonly known as flex layout or flex-box, so called because it includes many flexible options to arrange children within the layout.  
 
`FlexPanel` is similar to the StackPanel in that it can arrange its children horizontally and vertically in a stack. However, the `FlexPanel` is also capable of wrapping its children if there are too many to fit in a single row or column, and also has many options for orientation, alignment, and dynamically adapting to various screen sizes.
 
`FlexPanel` defines six public dependency properties and five attached dependency properties that affect the size, orientation, and alignment of its child elements. These properties are described in detail in the sections below on [The dependency properties in detail](#the-dependency-properties-in-detail) and [The attached dependency properties in detail](#the-attached-dependency-properties-in-detail). However, this article begins with a section on some Common usage scenarios of `FlexPanel` that describes many of these properties more informally.
 
> [!div class="nextstepaction"]
> [Try it in the sample app](uwpct://categoryName?sample=FlexPanel)
 
## Syntax
 
**XAML**
 
``` xaml
<Page
    x:Class="FlexPanelTest.SimpleStackPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:FlexPanelTest"
    xmlns:controls="using:Microsoft.Toolkit.Uwp.UI.Controls"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d"
    Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
 
    <Grid>
        <controls:FlexPanel 
            Direction="Column"
            AlignItems="Center"
            JustifyContent="SpaceEvenly">
 
            <TextBlock 
                Text="FlexPanel in Action"
                FontSize="40" />
 
            <Image 
                Stretch="None"
                Source="/Assets/SeatedMonkey.jpg" />
 
            <Button 
                Content="Do-Nothing Button" />
 
            <TextBlock 
                Text="Another Label" />
        </controls:FlexPanel>
    </Grid>
</Page>
```
 
## Sample Output
 
![SimpleStack](../resources/images/Controls/FlexPanel/SimpleStack.png)
 
## Properties
 
| Property | Type | Description |
| -- | -- | -- |
| AlignContent | FlexAlignContent | Controls how multiple rows or columns of child elements are aligned in the minor-axis direction. |
| AlignItems | FlexAlignItems | Controls how items are aligned within their row or column. |
| Direction | FlexDirection | Controls the flex direction for child elements within this layout. |
| JustifyContent | FlexJustifyContent | Controls how child elements are justified when there is extra space around them. |
| Wrap | FlexWrap | Controls whether and how child elements within this layout wrap |
 
## Attached Properties
| Attached Property | Type | Description |
| -- | -- | -- |
| AlignSelf | FlexAlignSelf | Optionally overrides the item alignment for this child within its row or column in the parent. |
| Basis | FlexBasis | Optionally controls this element's relative or absolute basis within the FlexPanel. |
| Grow | double |  Optionally controls the proportional growth that this element will accept to accommodate the layout in the row or column. |
| Order | int |  Optionally controls this element's visual order among its siblings. |
| Shrink | double | Optionally controls the proportional reduction in size that this element will accept to accommodate the layout in the row or column.
 
## Methods
 
<!-- Explain all methods in a table format -->
 
| Methods | Return Type | Description |
| -- | -- | -- |
| GetAlignSelf(UIElement) | FlexAlignSelf | Returns the value that optionally overrides the item alignment for this child within its row or column in the parent. |
| GetFlexBasis(UIElement) | FlexBasis | Returns the value that describes this element's relative or absolute basis length. |
| GetGrow(UIElement) | double | Returns the value that determines the proportional growth that this element will accept to accommodate the layout in the row or column. |
| GetOrder(UIElement) | int | Returns the visual order of the element among its siblings. |
| GetShrink(UIElement) | double | Returns the value that determines the proportional reduction in size that this element will accept to accommodate the layout in the row or column. |
| SetAlignSelf(UIElement, FlexAlignSelf) |  | Sets a value that optionally overrides the parent element's item alignment for this child element. |
| SetFlexBasis(UIElement, FlexBasis) | |  Sets the value that describes this element's relative or absolute basis length. |
| SetGrow(UIElement, double) |  | Sets the value that determines the proportional growth that this element will accept to accommodate the layout in the row or column. |
| SetOrder(UIElement, int) |  | Sets the visual order priority of the element among its siblings. |
| SetShrink(UIElement, double) |  | Sets the value that determines the proportional reduction in size that this element will accept to accommodate the layout in the row or column. | 
 
 
## Events
 
No events.
 
 
## Examples
 
### Using FlexPanel for a simple stack
 
`FlexPanel` can substitute for a StackLayout but with simpler markup. Everything in this sample is defined in the XAML page. 
 
``` xaml
<Page
    x:Class="FlexPanelTest.SimpleStackPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:FlexPanelTest"
    xmlns:controls="using:Microsoft.Toolkit.Uwp.UI.Controls"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d"
    Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
 
    <Grid>
        <controls:FlexPanel 
            Direction="Column"
            AlignItems="Center"
            JustifyContent="SpaceEvenly">
 
            <TextBlock 
                Text="FlexPanel in Action"
                FontSize="40" />
 
            <Image 
                Stretch="None"
                Source="/Assets/SeatedMonkey.jpg" />
 
            <Button 
                Content="Do-Nothing Button" />
 
            <TextBlock 
                Text="Another Label" />
        </controls:FlexPanel>
    </Grid>
</Page>
```
 
![SimpleStack](../resources/images/Controls/FlexPanel/SimpleStack.png)
 
Three properties of `FlexPanel` are shown in the above xaml file:
 
 - The `Direction` property is set to a value of the `FlexDirection` enumeration. The default is `Row`. Setting the property to `Column` causes the children of the `FlexPanel` to be arranged in a single column of items.
 
    When items in a `FlexPanel` are arranged in a column, the `FlexPanel` is said to have a vertical main axis and a horizontal cross axis.
 
 - The `AlignItems` property is of type `FlexAlignItems` and specifies how items are aligned on the cross axis. The `Center` option causes each item to be horizontally centered.
 
    If you were using a `StackPanel` rather than a `FlexPanel` for this task, you would center all the items by assigning the `HorizontalAlignment` property of each item to `Center`. The `HorizontalAlignment` property doesn't work for children of a `FlexPanel`, but the single `AlignItems` property accomplishes the same goal. If you need to, you can use the `AlignSelf` attached dependency property to override the `AlignItems` property for individual items:
 
    ``` xaml
    <TextBlock 
        Text="FlexPanel in Action"
        FontSize="36"
        FlexPanel.AlignSelf="Start" />
    ```
    With that change, this one `TextBlock` is positioned at the left edge of the `FlexPanel` when the reading order is left-to-right.
 
 - The `JustifyContent` property is of type `FlexJustify`, and specifies how items are arranged on the main axis. The `SpaceEvenly` option allocates all leftover vertical space equally between all the items, and above the first item, and below the last item.
 
These `FlexPanel` properties are discussed in more detail in the section [The dependency properties](#the-dependency-properties-in-detail) in detail below.
 
### Using FlexPanel for wrapping items
 
The below sample demonstrates how `FlexPanel` can wrap its children to additional rows or columns. The XAML file instantiates the `FlexPanel` and assigns two properties of it:
 
``` xaml
<Page
    x:Class="FlexPanelTest.PhotoWrappingPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:FlexPanelTest"
    xmlns:controls="using:Microsoft.Toolkit.Uwp.UI.Controls"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d"
    Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
    <Page.Content>
        <Grid>
            <Grid.Children>
                <ScrollViewer>
                    <controls:FlexPanel x:Name="flexPanel"
                        Wrap="Wrap"
                        JustifyContent="SpaceAround" />
                </ScrollViewer>
 
                <ProgressRing x:Name="activityIndicator"
                      VerticalAlignment="Center"
                      HorizontalAlignment="Center"
                      />
            </Grid.Children>
        </Grid>
    </Page.Content>
</Page>
```
 
The `Direction` property of this `FlexPanel` is not set, so it has the default setting of Row, meaning that the children are arranged in rows and the main axis is horizontal.
 
The `Wrap` property is of an enumeration type `FlexWrap`. If there are too many items to fit on a row, then this property setting causes the items to wrap to the next row.
 
Notice that the `FlexPanel` is a child of a `ScrollViewer`. If there are too many rows to fit on the page, then the `ScrollViewer` has a default `Orientation` property of `Vertical` and allows vertical scrolling.
 
The `JustifyContent` property allocates leftover space on the main axis (the horizontal axis) so that each item is surrounded by the same amount of blank space.
 
The code-behind file accesses a collection of sample photos and adds them to the Children collection of the `FlexPanel`:
 
``` csharp
    public partial class PhotoWrappingPage : Page
    {
        class ImageList
        {
            [JsonProperty("photos")]
            public List<string> Photos { get; set; }
        }
 
        public PhotoWrappingPage()
        {
            this.InitializeComponent();
            LoadBitmapCollection();
        }
 
        async void LoadBitmapCollection()
        {
            using (WebClient webClient = new WebClient())
            {
                try
                {
                    // Download the list of stock photos
                    Uri listUri = new Uri("https://raw.githubusercontent.com/xamarin/docs-archive/master/Images/stock/small/stock.json");
                    byte[] listData = await webClient.DownloadDataTaskAsync(listUri);
 
                    // Convert to a Stream object
                    using (Stream listStream = new MemoryStream(listData))
                    {
                        // Deserialize the JSON into an ImageList object
                        ImageList imageList = null;
                        using (var reader = new StreamReader(listStream)) 
                        using (var jsonReader = new JsonTextReader(reader))
                        {
                            var jsonSerializer = new JsonSerializer();
                            imageList = jsonSerializer.Deserialize<ImageList>(jsonReader);
                        }
 
                        // Create an Image object for each bitmap
                        foreach (string filepath in imageList.Photos)
                        {
                            var imageUri = new Uri(filepath, UriKind.Absolute);
 
                            byte[] imageBytes = await webClient.DownloadDataTaskAsync(imageUri);
                            var bitmapImage = await BitmapImageFromBytes(imageBytes);
                            var image = new Image { Stretch=Stretch.None, Source = bitmapImage };
                            flexPanel.Children.Add(image);
                        }
                    }
                }
                catch
                {
                    flexPanel.Children.Add(new TextBox
                    {
                        Text = "Cannot access list of bitmap files"
                    });
                }
            }
 
            activityIndicator.Visibility = Visibility.Collapsed;
        }
 
        async static Task<BitmapImage> BitmapImageFromBytes(Byte[] bytes)
        {
            var image = new BitmapImage();
 
#if WINDOWS_UWP
            using (var stream = new InMemoryRandomAccessStream())
            {
                await stream.WriteAsync(bytes.AsBuffer());
                stream.Seek(0);
                await image.SetSourceAsync(stream);
            }
#else
            Stream stream = new MemoryStream(bytes);
            await image.SetSourceAsync(stream);
#endif
            return image;
        }
 
    }
```
 
![PhotoWrap](../resources/images/Controls/FlexPanel/PhotoWrap.png)
 
### Page layout with FlexPanel
 
There is a standard layout in web design called the holy grail because it's a layout format that is very desirable, but often hard to realize with perfection. The layout consists of a header at the top of the page and a footer at the bottom, both extending to the full width of the page. Occupying the center of the page is the main content, but often with a columnar menu to the left of the content and supplementary information (sometimes called an aside area) at the right. Section 5.4.1 of the CSS Flexible Box Layout specification describes how the holy grail layout can be realized with a flex box.
 
The below sample shows a simple implementation of this layout using one `FlexPanel` nested in another. Because this page is designed for a phone in portrait mode, the areas to the left and right of the content area are only 50 pixels wide:
 
``` xaml
<Page
    x:Class="FlexPanelTest.HolyGrailLayoutPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:FlexPanelTest"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    xmlns:controls="using:Microsoft.Toolkit.Uwp.UI.Controls"
    mc:Ignorable="d"
    Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
    <Page.Content>
        <Grid>
 
            <controls:FlexPanel Direction="Column">
 
                <Border Background="Aqua">
                    <TextBlock
                        Text="HEADER"
                        FontSize="40"
                        HorizontalTextAlignment="Center" />
                </Border>
 
                <!-- Body -->
                <controls:FlexPanel 
                    Grid.Row="0"
                    Direction="Row"
                    Background="AliceBlue"
                    controls:FlexPanel.Grow="1.0"
                    >
 
                    <!-- Navigation items-->
                    <Rectangle 
                        controls:FlexPanel.Order="-1"
                        controls:FlexPanel.Basis="50"
                        Fill="Blue" />
 
                    <!-- Content -->
                    <Border 
                        Background="Gray"
                        controls:FlexPanel.Grow="1" 
                        >
                        <TextBlock 
                            Text="CONTENT"
                            FontSize="40"
                            HorizontalTextAlignment="Center"
                            HorizontalAlignment="Stretch"
                            VerticalAlignment="Center"
                            />
                    </Border>
 
                    <!-- Aside items -->
                    <Rectangle 
                        Fill="Green" 
                        controls:FlexPanel.Basis="50"
                        />
 
                </controls:FlexPanel>
                <Border Background="Pink" >
                    <TextBlock 
                        Text="FOOTER"
                        FontSize="40"
                        HorizontalTextAlignment="Center" />
                </Border>
            </controls:FlexPanel>
        </Grid>
    </Page.Content>
</Page>
```
 
![TheGrail](../resources/images/Controls/FlexPanel/HolyGrail.png)
 
The first `FlexPanel` in the XAML file has a vertical main axis and contains three children arranged in a column. These are the header, the body of the page, and the footer. The nested `FlexPanel` has a horizontal main axis with three children arranged in a row.
 
Three attached dependency properties are demonstrated in this program:
 
The `Order` attached dependency property is set on the first `Border`. This property is an integer with a default value of 0. You can use this property to change the layout order. Generally developers prefer the content of the page to appear in markup prior to the navigation items and aside items. Setting the `Order` property on the first `Border` to a value less than its other siblings causes it to appear as the first item in the row. Similarly, you can ensure that an item appears last by setting the `Order` property to a value greater than its siblings.
 
The `Basis` attached dependency property is set on the two `Border` items to give them a width of 50 pixels. This property is of type `FlexBasis`, a structure that defines a static property of type `FlexBasis` named `Auto`, which is the default. You can use `Basis` to specify a pixel size or a percentage that indicates how much space the item occupies on the main axis. It is called a basis because it specifies an item size that is the basis of all subsequent layouts.
 
The `Grow` property is set on the nested Layout and on the `TextBlock` child representing the content. This property is of type double and has a default value of 0. When set to a positive value, all the remaining space along the main axis is allocated to that item and to siblings with positive values of `Grow`. The space is allocated proportionally to the values, somewhat like the star specification in a Grid.
 
The first `Grow` attached property is set on the nested `FlexPanel`, indicating that this `FlexPanel` is to occupy all the unused vertical space within the outer `FlexPanel`. The second `Grow` attached property is set on the `TextBlock` representing the content, indicating that this content is to occupy all the unused horizontal space within the inner `FlexPanel`.
 
There is also a similar `Shrink` attached dependency property that you can use when the size of children exceeds the size of the `FlexPanel` but wrapping is not desired.
 
### Catalog items with FlexPanel
 
The following is similar to [Example 1 in Section 1.1 of the CSS Flex Layout Box specification](https://www.w3.org//TR/css-flexbox-1/#overview) except that it displays a horizontally scrollable series of pictures and descriptions of three monkeys:
 
![CatalogPage1](../resources/images/Controls/FlexPanel/CatalogPage1.png)
![CatalogPage2](../resources/images/Controls/FlexPanel/CatalogPage2.png)
 
Each of the three monkeys is a `FlexPanel` contained in a `Border` that is given an explicit height and width, and which is also a child of a larger `FlexPanel`. In this XAML file, most of the properties of the `FlexPanel` children are specified in styles, all but one of which is an implicit style:
 
``` xaml
<Page
    x:Class="FlexPanelTest.CatalogItemsPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:FlexPanelTest"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    xmlns:controls="using:Microsoft.Toolkit.Uwp.UI.Controls"
    mc:Ignorable="d"
    Padding="0"
    Margin="0"
    Background="LightGray">
    <Page.Resources>
        <Style TargetType="Border">
                <Setter Property="Background" Value="LightYellow" />
                <Setter Property="BorderBrush" Value="Blue" />
                <Setter Property="BorderThickness" Value="1" />
                <Setter Property="Margin" Value="5" />
                <Setter Property="Padding" Value="20" />
                <Setter Property="CornerRadius" Value="20" />
                <Setter Property="Width" Value="350"/>
                <Setter Property="Height" Value="500" />
        </Style>
 
        <Style TargetType="TextBlock">
                <Setter Property="Margin" Value="0, 2" />
                <Setter Property="TextWrapping" Value="WrapWholeWords"/>
                <Setter Property="Foreground" Value="Black"/>
        </Style>
 
        <Style x:Key="headerTextBlock" TargetType="TextBlock">
            <Style.Setters>
                <Setter Property="Margin" Value="0, 8" />
                <Setter Property="FontSize" Value="30" />
                <Setter Property="Foreground" Value="Blue" />
            </Style.Setters>
        </Style>
 
        <Style TargetType="Image">
            <Style.Setters>
                <Setter Property="controls:FlexPanel.Order" Value="-1" />
                <Setter Property="controls:FlexPanel.AlignSelf" Value="Center" />
            </Style.Setters>
        </Style>
 
        <Style TargetType="Button">
            <Style.Setters>
                <Setter Property="Content" Value="LEARN MORE" />
                <Setter Property="FontSize" Value="30" />
                <Setter Property="Foreground" Value="White" />
                <Setter Property="Background" Value="Green" />
                <Setter Property="CornerRadius" Value="10" />
                <Setter Property="controls:FlexPanel.AlignSelf" Value="Center" />
            </Style.Setters>
        </Style>
    </Page.Resources>
 
    <Page.Content>
        <ScrollViewer
            Background="Pink"
            HorizontalScrollMode="Enabled"  
            HorizontalScrollBarVisibility="Visible"
            HorizontalAlignment="Stretch"
            VerticalScrollMode="Disabled"
            VerticalScrollBarVisibility="Visible"
            VerticalAlignment="Stretch"
            Margin="0"
            Padding="0"
            >
            <ScrollViewer.Content>
                <controls:FlexPanel Background="Cyan">
                    <Border>
                        <controls:FlexPanel Direction="Column">
                            <TextBlock Text="Seated Monkey" Style="{StaticResource headerTextBlock}" />
                            <TextBlock Text="This monkey is laid back and relaxed, and likes to watch the world go by." />
                            <TextBlock Text="  &#x2022; Doesn't make a lot of noise" />
                            <TextBlock Text="  &#x2022; Often smiles mysteriously" />
                            <TextBlock Text="  &#x2022; Sleeps sitting up" />
                            <Image Source="/Assets/SeatedMonkey.jpg"
                                Width="180"
                                Height="180"
                                />
                            <TextBlock controls:FlexPanel.Grow="1" />
                            <Button />
                        </controls:FlexPanel>
                    </Border>
 
                    <Border>
                        <controls:FlexPanel Direction="Column">
                            <TextBlock Text="Banana Monkey" Style="{StaticResource headerTextBlock}" />
                            <TextBlock Text="Watch this monkey eat a giant banana." />
                            <TextBlock Text="  &#x2022; More fun than a barrel of monkeys" />
                            <TextBlock Text="  &#x2022; Banana not included" />
                            <Image Source="/Assets/Banana.jpg"
                                Width="240"
                                Height="180" />
                            <TextBlock controls:FlexPanel.Grow="1" />
                            <Button />
                        </controls:FlexPanel>
                    </Border >
 
                    <Border>
                        <controls:FlexPanel Direction="Column">
                            <TextBlock Text="Face-Palm Monkey" Style="{StaticResource headerTextBlock}" />
                            <TextBlock Text="This monkey reacts appropriately to ridiculous assertions and actions." />
                            <TextBlock Text="  &#x2022; Cynical but not unfriendly" />
                            <TextBlock Text="  &#x2022; Seven varieties of grimaces" />
                            <TextBlock Text="  &#x2022; Doesn't laugh at your jokes" />
                            <Image Source="/Assets/FacePalm.jpg"
                                Width="180"
                                Height="180" />
                            <TextBlock controls:FlexPanel.Grow="1" />
                            <Button />
                        </controls:FlexPanel>
                    </Border>
                </controls:FlexPanel>
            </ScrollViewer.Content>
        </ScrollViewer>
    </Page.Content>
</Page>
```
 
The implicit style for the `Image` includes settings of two attached dependency properties of `FlexPanel`:
 
``` xaml
        <Style TargetType="Image">
            <Style.Setters>
                <Setter Property="controls:FlexPanel.Order" Value="-1" />
                <Setter Property="controls:FlexPanel.AlignSelf" Value="Center" />
            </Style.Setters>
        </Style>
```
 
The `Order` setting of –1 causes the `Image` element to be displayed first in each of the nested `FlexPanel` views regardless of its position within the children collection. The `AlignSelf` property of `Center` causes the `Image` to be centered within the `FlexPanel`. This overrides the setting of the `AlignItems` property, which has a default value of `Stretch`, meaning that the `TextBlock` and `Button` children are stretched to the full width of the `FlexPanel`.
 
Within each of the three `FlexPanel` views, a blank `TextBlock` precedes the `Button`, but it has a `Grow` setting of 1. This means that all the extra vertical space is allocated to this blank `TextBlock`, which effectively pushes the `Button` to the bottom.
 
## The dependency properties in detail
 
Now that you've seen some common applications of `FlexPanel`, the properties of `FlexPanel` can be explored in more detail. `FlexPanel` defines five dependency properties that you set on the `FlexPanel` itself, either in code or XAML, to control orientation and alignment.
 
You can experiment with the five dependency properties using the [FlexPanelExperimentPage](https://github.com/baskren/WindowsCommunityToolkit/tree/FlexPanel/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/FlexPanel) page of the [Windows Community Toolkit Sample App](https://github.com/baskren/WindowsCommunityToolkit/tree/FlexPanel/Microsoft.Toolkit.Uwp.SampleApp). This page allows you to add or remove children from a `FlexPanel` and to set combinations of the five dependency properties. All the children of the `FlexPanel` are Border views, with a nested `TextBlock`, of various colors and sizes, with the `Text` property set to a number corresponding to its position in the Children collection.
 
When the program starts up, five Picker views display the default values of these five `FlexPanel` properties. The `FlexPanel` towards the bottom of the screen contains three children:
 
![ExperimentPage1](../resources/images/Controls/FlexPanel/Experiment1.png)
 
Each of the `Border` views has a gray background that shows the space allocated to that `Border` within the `FlexPanel`. The background of the `FlexPanel` itself is Alice Blue. It occupies the entire bottom area of the page except for a little margin around it.
 
### The Direction property
 
The `Direction` property is of type `FlexDirection`, an enumeration with four members:
 
 - `Column`
 - `ColumnReverse` (or "column-reverse" in XAML)
 - `Row`, the default
 - `RowReverse` (or "row-reverse" in XAML)
 
 
Here's the Experiment page showing (from left to right), the Row direction, Column direction, and ColumnReverse direction:
 
![ExperimentPage2](../resources/images/Controls/FlexPanel/Experiment2.png)
![ExperimentPage3](../resources/images/Controls/FlexPanel/Experiment3.png)
![ExperimentPage4](../resources/images/Controls/FlexPanel/Experiment4.png)
 
Notice that for the `Reverse` options, the items start at the right or bottom.
 
### The Wrap property
 
The `Wrap` property is of type `FlexWrap`, an enumeration with three members:
 
 - `NoWrap`, the default
 - `Wrap`
 - `Reverse` (or "wrap-reverse" in XAML)
 
From left to right, these screens show the `NoWrap`, `Wrap` and `Reverse` options for 12 children:
 
![ExperimentPage5](../resources/images/Controls/FlexPanel/Experiment5.png)
![ExperimentPage6](../resources/images/Controls/FlexPanel/Experiment6.png)
![ExperimentPage7](../resources/images/Controls/FlexPanel/Experiment7.png)
 
When the `Wrap` property is set to `NoWrap` and the main axis is constrained (as in this program), and the main axis is not wide or tall enough to fit all the children, the `FlexPanel` attempts to make the items smaller. You can control the shrinkness of the items with the `Shrink` attached dependency property.
 
### The JustifyContent property
 
The `JustifyContent` property is of type `FlexJustify`, an enumeration with six members:
 
 - `Start` (or "flex-start" in XAML), the default
 - `Center`
 - `End` (or "flex-end" in XAML)
 - `SpaceBetween` (or "space-between" in XAML)
 - `SpaceAround` (or "space-around" in XAML)
 - `SpaceEvenly`
 
This property specifies how the items are spaced on the main axis, which is the horizontal axis in this example:
 
![ExperimentPage8](../resources/images/Controls/FlexPanel/Experiment8.png)
![ExperimentPage9](../resources/images/Controls/FlexPanel/Experiment9.png)
![ExperimentPage10](../resources/images/Controls/FlexPanel/Experiment10.png)
 
 
In all three screenshots, the `Wrap` property is set to `Wrap`. The `Start` default is shown in the first screenshot, below. The second screenshot, below, shows the `Center` option: all the items are moved to the center. The three other options (the ones beginning with the word `Space`) allocate the extra space not occupied by the items. `SpaceBetween` allocates the space equally between the items; `SpaceAround` puts equal space around each item, while `SpaceEvenly` puts equal space between each item, and before the first item and after the last item on the row.
 
### The AlignItems property
 
The `AlignItems` property is of type `FlexAlignItems`, an enumeration with four members:
 
 - `Stretch`, the default
 - `Center`
 - `Start` (or "flex-start" in XAML)
 - `End` (or "flex-end" in XAML)
 
This is one of two properties (the other being `AlignContent`) that indicates how children are aligned on the cross axis. Within each row, the children are stretched (as shown in the previous screenshot), or aligned on the start, center, or end of each item, as shown in the following three screenshots:
 
![ExperimentPage11](../resources/images/Controls/FlexPanel/Experiment11.png)
![ExperimentPage12](../resources/images/Controls/FlexPanel/Experiment12.png)
![ExperimentPage13](../resources/images/Controls/FlexPanel/Experiment13.png)
 
In the first screenshot, the tops of all the children are aligned. In the second screenshot, the items are vertically centered based on the tallest child. In the last screenshot, the bottoms of all the items are aligned.
 
For any individual item, the `AlignItems` setting can be overridden with the `AlignSelf` attached dependency property.
 
### The AlignContent property
 
The `AlignContent` property is of type `FlexAlignContent`, an enumeration with seven members:
 
 - `Stretch`, the default
 - `Center`
 - `Start` (or "flex-start" in XAML)
 - `End` (or "flex-end" in XAML)
 - `SpaceBetween` (or "space-between" in XAML)
 - `SpaceAround` (or "space-around" in XAML)
 - `SpaceEvenly`
 
Like `AlignItems`, the `AlignContent` property also aligns children on the cross axis, but affects entire rows or columns:
 
![ExperimentPage14](../resources/images/Controls/FlexPanel/Experiment14.png)
![ExperimentPage15](../resources/images/Controls/FlexPanel/Experiment15.png)
![ExperimentPage16](../resources/images/Controls/FlexPanel/Experiment16.png)
 
In the first screenshot, both rows are at the top; in the second screenshot they're in the center; and in the last screenshot they're at the bottom. The rows can also be spaced in various ways:
 
![ExperimentPage17](../resources/images/Controls/FlexPanel/Experiment17.png)
![ExperimentPage18](../resources/images/Controls/FlexPanel/Experiment18.png)
![ExperimentPage19](../resources/images/Controls/FlexPanel/Experiment19.png)
 
The `AlignContent` has no effect when there is only one row or column.
 
## The attached dependency properties in detail
 
The `AlignSelf` attached dependency property is of type `FlexAlignSelf`, an enumeration with five members:
 
 - `Auto`, the default
 - `Stretch`
 - `Center`
 - `Start` (or "flex-start" in XAML)
 - `End` (or "flex-end" in XAML)
 
For any individual child of the `FlexPanel`, this property setting overrides the `AlignItems` property set on the `FlexPanel` itself. The default setting of `Auto` means to use the `AlignItems` setting.
 
For a `TextBlock` element named label (or example), you can set the `AlignSelf` property in code like this:
 
``` csharp
FlexPanel.SetAlignSelf(label, FlexAlignSelf.Center);
```
 
Notice that there is no reference to the `FlexPanel` parent of the `TextBlock`. In XAML, you set the property like this:
 
``` xaml
<TextBlock ... FlexPanel.AlignSelf="Center" ... />
```
 
### The Order Property
 
The `Order` attached dependency property is of type int. The default value is 0.
 
The `Order` property allows you to change the order that the children of the `FlexPanel` are arranged. Usually, the children of a `FlexPanel` are arranged in the same order that they appear in the `Children` collection. You can override this order by setting the `Order` attached dependency property to a non-zero integer value on one or more children. The `FlexPanel` then arranges its children based on the setting of the `Order` property on each child, but children with the same `Order` setting are arranged in the order that they appear in the `Children` collection.
 
### The Basis Property
 
The `Basis` attached dependency property indicates the amount of space that is allocated to a child of the `FlexPanel` on the main axis. The size specified by the `Basis` property is the size along the main axis of the parent `FlexPanel`. Therefore, `Basis` indicates the width of a child when the children are arranged in rows, or the height when the children are arranged in columns.
 
The `Basis` property is of type `FlexBasis`, a structure. The size can be specified in either device-independent units or as a percentage of the size of the `FlexPanel`. The default value of the `Basis` property is the static property `FlexBasis.Auto`, which means that the child's requested width or height is used.
 
In code, you can set the `Basis` property for a `TextBlock` named label to 40 device-independent units like this:
 
``` csharp
FlexPanel.SetBasis(label, new FlexBasis(40));
```
 
An implicit conversion from `double` to `FlexBasis` is defined, so you can simplify it even further:
 
``` csharp
FlexPanel.SetBasis(label, 40);
```
 
You can set the size to 25% of the `FlexPanel` parent like this:
 
``` csharp
FlexPanel.SetBasis(label, new FlexBasis(0.25f, true));
```
 
This fractional value must be in the range of 0 to 1.
 
In XAML, you can use a number for a size in device-independent units:
 
```xaml
<Label ... FlexPanel.Basis="40" ... />
```
 
Or you can specify a percentage in the range of 0% to 100%:
 
```xaml
<Label ... FlexPanel.Basis="25%" ... />
```
 
### The Grow Property
 
The `Grow` attached dependency property is of type int. The default value is 0, and the value must be greater than or equal to 0.
 
The `Grow` property plays a role when the `Wrap` property is set to `NoWrap` and the row of children has a total width less than the width of the `FlexPanel`, or the column of children has a shorter height than the `FlexPanel`. The `Grow` property indicates how to apportion the leftover space among the children.
 
If any one child is given a positive `Grow` value, then that child takes up all the remaining space. This space can also be allocated among two or more children.
 
How the child view uses that space depends on the particular type of child. For a `TextBlock`, the text can be positioned within the total space of the `TextBlock` using the properties `HorizontalAlignment` and `VerticalAlignment`.
 
### The Shrink Property
 
The Shrink attached dependency property is of type int. The default value is 1, and the value must be greater than or equal to 0.
 
The `Shrink` property plays a role when the `Wrap` property is set to `NoWrap` and the aggregate width of a row of children is greater than the width of the `FlexPanel`, or the aggregate height of a single column of children is greater than the height of the `FlexPanel`. Normally the `FlexPanel` will display these children by constricting their sizes. The `Shrink` property can indicate which children are given priority in being displayed at their full sizes.
 
You can set both the `Grow` and `Shrink` values to accommodate situations where the aggregate child sizes might sometimes be less than or sometimes greater than the size of the `FlexPanel`.
 
 
 
<!-- All control/helper must at least have an example to show the use of Properties and Methods in your control/helper with the output -->
<!-- Use <example> and <code> tags in C# to create a Propertie/method specific examples. For more info - https://docs.microsoft.com/dotnet/csharp/programming-guide/xmldoc/example -->
<!-- Optional: Codes to achieve real-world use case with the output. For eg: Check https://docs.microsoft.com/windows/communitytoolkit/animations/animationset#examples  -->
 
## Sample Project
 
<!-- Link to the sample page in the Windows Community Toolkit Sample App -->
[FlexPanel Sample Page](https://github.com/baskren/WindowsCommunityToolkit/tree/FlexPanel/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/FlexPanel). You can [see this in action](uwpct://CategoryName?sample=FlexPanel) in [Windows Community Toolkit Sample App](http://aka.ms/uwptoolkitapp).
 
## Requirements
 
| [Device family](http://go.microsoft.com/fwlink/p/?LinkID=526370#device-families) | Universal, 10.0.16299.0 or higher   |
| -- | -- |
| Namespace | Microsoft.Toolkit.Uwp.UI.Controls |
| NuGet package | [Microsoft.Toolkit.Uwp.UI.Controls](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI.Controls/) |
## API
 
* [FlexPanel](https://github.com/baskren/WindowsCommunityToolkit/tree/FlexPanel/Microsoft.Toolkit.Uwp.UI.Controls/FlexPanel/FlexPanel.cs)
* [FlexBasis](https://github.com/baskren/WindowsCommunityToolkit/blob/FlexPanel/Microsoft.Toolkit.Uwp.UI.Controls/FlexPanel/FlexBasis.cs)
* [FlexAlignContent](https://github.com/baskren/WindowsCommunityToolkit/blob/FlexPanel/Microsoft.Toolkit.Uwp.UI.Controls/FlexPanel/Enums/FlexAlignContent.cs)
* [FlexAlignItems](https://github.com/baskren/WindowsCommunityToolkit/blob/FlexPanel/Microsoft.Toolkit.Uwp.UI.Controls/FlexPanel/Enums/FlexAlignItems.cs)
* [FlexAlignSelf](https://github.com/baskren/WindowsCommunityToolkit/blob/FlexPanel/Microsoft.Toolkit.Uwp.UI.Controls/FlexPanel/Enums/FlexAlignSelf.cs)
* [FlexDirection](https://github.com/baskren/WindowsCommunityToolkit/blob/FlexPanel/Microsoft.Toolkit.Uwp.UI.Controls/FlexPanel/Enums/FlexDirection.cs)
* [FlexJustify](https://github.com/baskren/WindowsCommunityToolkit/blob/FlexPanel/Microsoft.Toolkit.Uwp.UI.Controls/FlexPanel/Enums/FlexJustify.cs)
* [FlexWrap](https://github.com/baskren/WindowsCommunityToolkit/blob/FlexPanel/Microsoft.Toolkit.Uwp.UI.Controls/FlexPanel/Enums/FlexPosition.cs)
 
## Related Topics
 
* [CSS Flexible Box Layout Module](https://www.w3.org/TR/css-flexbox-1/)
* [Xamarin.Forms FlexLayout](https://docs.microsoft.com/en-us/xamarin/xamarin-forms/user-interface/layouts/flex-layout)
* [!VIDEO https://youtube.com/embed/Ng3sel_5D_0]
* [Xamarin.Forms FlexLayoutDemos](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-flexlayoutdemos)

