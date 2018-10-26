---
title: How to - Add a DataGrid control to a page
author: harinik
description: Guidance document that shows how to add a DataGrid control and display data in rows and columns
keywords: windows 10, uwp, windows community toolkit, windows toolkit, DataGrid, xaml control, xaml
---

# How to: Add a DataGrid control to a page

The Windows 10 [DataGrid](../datagrid.md) control is part of the Windows Community Toolkit DataGrid library. To use the DataGrid control in your Windows 10 application, you need to add the appropriate reference to your application as shown in the following section.

## Getting started with the DataGrid control

The toolkit is available as NuGet packages that can be added to any existing or new project using Visual Studio.

1. Download [Visual Studio 2017](https://developer.microsoft.com/en-us/windows/downloads) and ensure you choose the **Universal Windows Platform development** Workload in the Visual Studio installer.

2. Open an existing project, or create a new project using the Blank App template under Visual C# -> Windows -> Universal.  **Important**:  Build 16299 or higher is supported by current version of the Toolkit.

3. In Solution Explorer panel, right click on your project name and select **Manage NuGet Packages**. Search for **Microsoft.Toolkit.UWP.UI.Controls.DataGrid**, and choose the [Microsoft.Toolkit.Uwp.UI.Controls.DataGrid](https://www.nuget.org/packages/Microsoft.Toolkit.Uwp.UI.Controls.DataGrid/) nuget package.

    ![NuGet Packages](../../resources/images/ManageNugetPackages.png "Manage NuGet Packages Image")

4. Add a reference to the toolkit and add the DataGrid control in your XAML page

    * Add a reference at the top of your page

        ```xml
        xmlns:controls="using:Microsoft.Toolkit.Uwp.UI.Controls"
        ```
    * Add the following XAML in your page to add the DataGrid control

       ```xml
       <controls:DataGrid x:Name="dataGrid">

       </controls:DataGrid>
       ```

5. Alternatively, you can add the DataGrid control directly in C# in your page code behind. **Important** You would either add it to the XAML directly or the code behind, not both. 

    * Add the namespaces to the toolkit

        ```c#
        using Microsoft.Toolkit.Uwp.UI.Controls;
        ```

    * Add the control in your Loaded event

        ```c#
        DataGrid dataGrid1 = new DataGrid();
        LayoutRoot.Children.Add(dataGrid1);
        ```

## Binding a DataGrid to a data source

You can use the **DataGrid.ItemsSource** property to bind to a collection that will be used to generate the contents of the DataGrid control. The following example demonstrates how to use the **ItemsSource** and **AutoGenerateColumns** properties to automatically display a collection of Customer data in rows and columns.

```xml
<controls:DataGrid x:Name="dataGrid1" 
    Height="600" Margin="12"
    AutoGenerateColumns="True"
    ItemsSource="{x:Bind MyViewModel.Customers}" />  
```

```C#
//backing data source in MyViewModel
public class Customer
{
    public String FirstName { get; set; }
    public String LastName { get; set; }
    public String Address { get; set; }
    public Boolean IsNew { get; set; }

    public Customer(String firstName, String lastName, 
        String address, Boolean isNew)
    {
        this.FirstName = firstName;
        this.LastName = lastName;
        this.Address = address;
        this.IsNew = isNew; 
    }

    public static List<Customer> Customers()
    {
        return new List<Customer>(new Customer[4] {
            new Customer("A.", "Zero", 
                "12 North Third Street, Apartment 45", 
                false), 
            new Customer("B.", "One", 
                "34 West Fifth Street, Apartment 67", 
                false),
            new Customer("C.", "Two", 
                "56 East Seventh Street, Apartment 89", 
                true),
            new Customer("D.", "Three", 
                "78 South Ninth Street, Apartment 10", 
                true)
        });
    }
}
```

## Customizing columns

By default, the DataGrid control generates columns automatically when you set the ItemsSource property as shown above. The generated columns are of type **DataGridCheckBoxColumn** for bound Boolean (and nullable Boolean) properties, and of type **DataGridTextColumn** for all other properties. If a property does not have a String or numeric value type, the generated text box columns are read-only and display the data object's ToString value.

You can override the default automatic generation of columns by setting the **AutoGenerateColumns** property to False and explicitly creating the bound columns with styling in XAML as shown below.

```xml
<controls:DataGrid x:Name="dataGrid1" 
    Height="600" Margin="12"
    AutoGenerateColumns="False"
    ItemsSource="{x:Bind MyViewModel.Customers}">
    <controls:DataGrid.Columns>
       <controls:DataGridTextColumn 
            Header="First Name" 
            Width="SizeToHeader"
            Binding="{Binding FirstName}" 
            FontSize="20" />
        <controls:DataGridTextColumn 
            Header="Last Name" 
            Width="SizeToCells"
            Binding="{Binding LastName}" 
            FontSize="20" />
        <controls:DataGridTextColumn 
            Header="Address"
            Width="150"
            Binding="{Binding Address}" >
            <controls:DataGridTextColumn.ElementStyle>
                <Style TargetType="TextBlock">
                    <Setter Property="TextWrapping" Value="Wrap"/>
                </Style>
            </controls:DataGridTextColumn.ElementStyle>
            <controls:DataGridTextColumn.EditingElementStyle>
                <Style TargetType="TextBox">
                    <Setter Property="Foreground" Value="Blue"/>
                </Style>
            </controls:DataGridTextColumn.EditingElementStyle>
        </controls:DataGridTextColumn>
        <controls:DataGridCheckBoxColumn 
            Header="New?" 
            Width="40"
            Binding="{Binding IsNew}" />
    </controls:DataGrid.Columns>
</controls:DataGrid>  
```

### DataGridComboBoxColumn

In display mode the combobox column looks like the normal text column. In edit mode the column allows the user to select a value from a provided collection displayed in a **ComboBox** control.

The **DataGridComboBoxColumn** contains the following specific properties:

* **ItemsSource** (IEnumerable): This property is bound to a collection of objects representing the elements of the combobox (the source is the same for all cells in the column). The **ItemsSource** elements of the column must have at least one property with the same name as the elements of the **ItemsSource** belonging to the **DataGrid** itself.

* **Binding** (Binding): This property binds the column to a property in the **DataGrid**'s **ItemsSource**. It also links this property to a property with the same name within the column's **ItemsSource**.

* **DisplayMemberPath** (string): This property tells the column which property value to show in both display and edit mode. It's value must match the name of a property within the column's **ItemsSource** elements.

The following code example demonstrates how to specify and configure a **DataGridComboBoxColumn** in XAML.

```xml
<controls:DataGrid x:Name="EmployeeGrid"
                  ItemsSource="{x:Bind Persons}"
                  AutoGenerateColumns="False">
            <controls:DataGrid.Columns>
                <controls:DataGridTextColumn Header="First Name"
                                             Binding="{Binding FirstName}"/>
                <controls:DataGridTextColumn Header="Last Name"
                                             Binding="{Binding LastName}"/>
                <controls:DataGridTextColumn Header="Position"
                                             Binding="{Binding Position}"/>
                <controls:DataGridComboBoxColumn Header="Department"
                                                 Binding="{Binding DepartmentId}"                                                  
                                                 ItemsSource="{x:Bind Departments, Mode=OneWay}"
                                                 DisplayMemberPath="DepartmentName"/>
            </controls:DataGrid.Columns>
</controls:DataGrid>
```

Code-Behind:

```C#
public class Department
{
    public int DepartmentId { get; set; }
    public string DepartmentName { get; set; }
}

public class Person
{
    public int PersonId { get; set; }
    public int DepartmentId { get; set; }
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public string Position { get; set; }
}
public sealed partial class MainPage : Page
{
    public List<Department> Departments { get; set; }
    public List<Person> Persons { get; set; }

    public MainPage()
    {
        this.InitializeComponent();

        Departments = new List<Department>
        {
            new Department {DepartmentId = 1, DepartmentName = "R&D"},
            new Department {DepartmentId = 2, DepartmentName = "Finance"},
            new Department {DepartmentId = 3, DepartmentName = "IT"}
        };

        Persons = new List<Person>
        {
            new Person
            {
                PersonId = 1, DepartmentId = 3, FirstName = "Ronald", LastName = "Rumple",
                Position = "Network Administrator"
            },
            new Person
            {
                PersonId = 2, DepartmentId = 1, FirstName = "Brett", LastName = "Banner",
                Position = "Software Developer"
            },
            new Person
            {
                PersonId = 3, DepartmentId = 2, FirstName = "Alice", LastName = "Anderson",
                Position = "Accountant"
            }
        };
    }
}
```

### DataGridTemplateColumn

The DataGridTemplateColumn type enables you to create your own column types by specifying the cell templates used to display values and enable editing. Set the **CellTemplate** property to specify the contents of cells that display values, but do not allow editing. Set the **CellEditingTemplate** property to specify the contents of cells in editing mode. If you set the column's **IsReadOnly** property to true, the CellEditingTemplate property value is never used.

The following code example demonstrates how to specify and configure a DataGridTemplateColumn in XAML. 

```xml
<controls:DataGrid x:Name="dataGrid1" 
    Height="600" Margin="12"
    AutoGenerateColumns="False"
    ItemsSource="{x:Bind MyViewModel.Customers}">
    <controls:DataGrid.Columns>
        <!-- Name Column -->
        <controls:DataGridTemplateColumn Header="Name">
            <controls:DataGridTemplateColumn.CellTemplate>
                <DataTemplate>
                    <StackPanel Orientation="Horizontal" VerticalAlignment="Center">
                        <TextBlock Padding="5,0,5,0"
                            Text="{x:Bind FirstName}"/>
                        <TextBlock Text="{x:Bind LastName}"/>
                    </StackPanel>
                </DataTemplate>
            </controls:DataGridTemplateColumn.CellTemplate> 
            <controls:DataGridTemplateColumn.CellEditingTemplate>
                <DataTemplate>
                    <StackPanel Orientation="Horizontal">
                        <TextBox Text="{x:Bind FirstName}" BorderThickness="0"/>
                        <TextBox Text="{x:Bind LastName}" BorderThickness="0"/>
                    </StackPanel>
                </DataTemplate>
            </controls:DataGridTemplateColumn.CellEditingTemplate> 
        </controls:DataGridTemplateColumn>              
        <!-- other columns below -->
</controls:DataGrid>
```

## See Also

* [Customize the DataGrid control using styling and formatting options](styling_formatting_options.md)
* [Sizing options in the DataGrid control](sizing_options.md)
* [Default keybaord navigation and selection patterns](keyboard_navigation_selection.md)
* [Display and configure Row Details](rowdetails.md)
* [Configure Auto-generated columns in the DataGrid control](customize_autogenerated_columns.md)
* [Group, sort and filter data using LINQ and the DataGrid control](group_sort_filter.md)
* [Editing and input validation in the DataGrid control](editing_inputvalidation.md)
* [DataGrid Sample Page Source](https://github.com/Microsoft/WindowsCommunityToolkit/tree/master/Microsoft.Toolkit.Uwp.SampleApp/SamplePages/DataGrid)
