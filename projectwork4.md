## Aim

The aim for this weeks entry of the portfolio is to finish the selected user story from the previous week.

## Issue Working On

The user story I am working on is a continuation from last week, which was the user story "As an UNDAC Team Support and Logistics Manager, I want to assign vehicles and other equipment to operations on request so that assignments are appropriately equipped."

The goal for this user story is to have a section of the program that will allow UNDAC Team Support and Logistics Manager users to view operations and assign equipment and vehicles.

The main criteria for this user story is :

* Operations can be viewed in a list
* New requests will be highlighted in the list
* List filters can be cleared
* Operations details can be viewed
* Requests can be approved

## Progress from Previous Week

Compared to last week I have the issue much more complete. It doesn't meet all the criteria that the user story wanted, but that is because I do not know how to get some of those things to work using .NET Maui. Such as the highlighting of new requests in a list.


## Code Snippet

XAML
```c#
<ScrollView>
    <StackLayout Margin="20">
        <Entry x:Name="SearchTextBox"  Placeholder="Search" FontSize="18"/>

        <StackLayout Orientation="Horizontal" Spacing="10">
            <Button Text="Search" Clicked="SearchButton_Click" FontSize="18"/>
            <Button Text="Clear" Clicked="ClearButton_Click" FontSize="18"/>
        </StackLayout>

        <ListView x:Name="operationListView" ItemsSource="{Binding FilteredOperation}" SelectedItem="{Binding SelectedItem}" ItemSelected = "ListView_ItemSelected">
            <ListView.ItemTemplate>
                <DataTemplate>
                    <ViewCell>
                        <StackLayout Orientation="Horizontal">
                            <Label Text="{Binding name}" FontSize="18"/>
                            <Label Text=" -  " FontSize="18"/>
                            <Label Text="{Binding request_type}" FontSize="18"/>
                        </StackLayout>
                    </ViewCell>

                </DataTemplate>
            </ListView.ItemTemplate>
        </ListView>

        <StackLayout Orientation="Horizontal" Spacing="10">
            <Button Text="View" Clicked="ViewButton_Click" FontSize="18"/>
            <Button x:Name="EditButton" Text="Edit" Clicked="EditButton_Click" FontSize="18"/>
            <Button x:Name="SaveButton" Text="Save" Clicked="SaveButton_Click" FontSize="18"/>
        </StackLayout>

        <StackLayout>
            <Label Text="Operation Information : " FontSize="20" TextDecorations="Underline" FontAttributes="Bold"/>
            <Label Text=""/>
            <Label x:Name="idLabel" FontSize="18"/>
            <Label x:Name="equipmentLabel" FontSize="18"/>
            <Label x:Name="requestedLabel" FontSize="18"/>
            <Label x:Name="requestTypeLabel" FontSize="18"/>
            <Label x:Name="requestDateLabel" FontSize="18"/>
            <Label x:Name="authorisedLabel" FontSize="18"/>
            <Label x:Name="authorisedDateLabel" FontSize="18"/>
            <Label x:Name="startLabel" FontSize="18"/>
            <Label x:Name="endLabel" FontSize="18"/>
            <Label x:Name="rotaIdLabel" FontSize="18"/>
            <Label x:Name="operationIdLabel" FontSize="18"/>
            <Label x:Name="nameLabel" FontSize="18"/>
            <Label x:Name="typeLabel" FontSize="18"/>
            <Label x:Name="makeLabel" FontSize="18"/>
            <Label x:Name="modelLabel" FontSize="18"/>
            <Label x:Name="serialLabel" FontSize="18"/>

            <Label x:Name="idEntryLabel" Text="ID : " FontSize="18" IsVisible="False"/>
            <Entry x:Name="idEntry" FontSize="18" IsVisible="False"/>

            <Label x:Name="equipmentEntryLabel" Text="Equipment ID : " FontSize="18" IsVisible="False"/>
            <Entry x:Name="equipmentEntry" FontSize="18" IsVisible="False"/>

            <Label x:Name="requestedByEntryLabel" Text="Requested By : " FontSize="18" IsVisible="False"/>
            <Entry x:Name="requestedByEntry" FontSize="18" IsVisible="False"/>

            <Label x:Name="requestTypeEntryLabel" Text="Requested Type : " FontSize="18" IsVisible="False"/>
            <Entry x:Name="requestTypeEntry" FontSize="18" IsVisible="False"/>

            <Label x:Name="requestDateEntryLabel" Text="Request Date : " FontSize="18" IsVisible="False"/>
            <DatePicker x:Name="requestDateEntry" Date="{Binding request_date}" Format="yyyy-MM-dd" FontSize="18" IsVisible="False"/>

            <Label x:Name="authorisedByEntryLabel" Text="Authorised By : " FontSize="18" IsVisible="False"/>
            <Entry x:Name="authorisedByEntry" FontSize="18" IsVisible="False"/>

            <Label x:Name="authorisedDateEntryLabel" Text="Authorised Date : " FontSize="18" IsVisible="False"/>
            <DatePicker x:Name="authorisedDateEntry" Date="{Binding authorised_date}" Format="yyyy-MM-dd" FontSize="18" IsVisible="False"/>

            <Label x:Name="startDateEntryLabel" Text="Start Date : " FontSize="18" IsVisible="False"/>
            <DatePicker x:Name="startDateEntry" Date="{Binding start_date}" Format="yyyy-MM-dd" FontSize="18" IsVisible="False"/>

            <Label x:Name="endDateEntryLabel" Text="End Date : " FontSize="18" IsVisible="False"/>
            <DatePicker x:Name="endDateEntry" Date="{Binding end_date}" Format="yyyy-MM-dd" FontSize="18" IsVisible="False"/>

            <Label x:Name="rotaIdEntryLabel" Text="Rota ID : " FontSize="18" IsVisible="False"/>
            <Entry x:Name="rotaIdEntry" FontSize="18" IsVisible="False"/>

            <Label x:Name="operationIdEntryLabel" Text="Operation ID : " FontSize="18" IsVisible="False"/>
            <Entry x:Name="operationIdEntry" FontSize="18" IsVisible="False"/>

            <Label x:Name="nameEntryLabel" Text="Name : " FontSize="18" IsVisible="False"/>
            <Entry x:Name="nameEntry" FontSize="18" IsVisible="False"/>

            <Label x:Name="typeEntryLabel" Text="Type : " FontSize="18" IsVisible="False"/>
            <Entry x:Name="typeEntry" FontSize="18" IsVisible="False"/>

            <Label x:Name="makeEntryLabel" Text="Make : " FontSize="18" IsVisible="False"/>
            <Entry x:Name="makeEntry" FontSize="18" IsVisible="False"/>

            <Label x:Name="modelEntryLabel" Text="Model : " FontSize="18" IsVisible="False"/>
            <Entry x:Name="modelEntry" FontSize="18" IsVisible="False"/>

            <Label x:Name="serialEntryLabel" Text="Serial Number : " FontSize="18" IsVisible="False"/>
            <Entry x:Name="serialEntry" FontSize="18" IsVisible="False"/>
        </StackLayout>


        <Label x:Name="ErrorLabel"/>

    </StackLayout>
</ScrollView>
```

```c#
private void UpdateOperationDetails()
{
    try
    {
    idLabel.Text = $"Id : {selectedOperation.id}";
    equipmentLabel.Text = $"Equipment Id : {selectedOperation.equipment_id}";
    requestedLabel.Text = $"Requested By : {selectedOperation.requested_by}";
    requestTypeLabel.Text = $"Request Type : {selectedOperation.request_type}";
    requestDateLabel.Text = $"Request Date : {selectedOperation.request_date}";
    authorisedLabel.Text = $"Authorised By : {selectedOperation.authorised_by}";
    authorisedDateLabel.Text = $"Authorised On : {selectedOperation.authorised_date}";
    startLabel.Text = $"Start Date : {selectedOperation.start_date}";
    endLabel.Text = $"End Date : {selectedOperation.end_date}";
    rotaIdLabel.Text = $"Rota Id : {selectedOperation.rota_id}";
    operationIdLabel.Text = $"Operation Id : {selectedOperation.operation_id}";
    nameLabel.Text = $"Name : {selectedOperation.name}";
    typeLabel.Text = $"Type : {selectedOperation.type}";
    makeLabel.Text = $"Make : {selectedOperation.make}";
    modelLabel.Text = $"Model : {selectedOperation.model}";
    serialLabel.Text = $"Serial Number : {selectedOperation.serial_number}";
    }
    catch (Exception ex)
    {
        ErrorLabel.Text += ex.Message;
    }
}
```

```c#
private void SaveButton_Click(object sender, EventArgs e)
{
    try
    {
        if (selectedOperation != null)
        {
            selectedOperation.id = int.Parse(idEntry.Text);
            selectedOperation.equipment_id = int.Parse(equipmentEntry.Text);
            selectedOperation.request_type = requestTypeEntry.Text;
            selectedOperation.requested_by = requestedByEntry.Text;
            selectedOperation.request_date = DateOnly.FromDateTime(requestDateEntry.Date);
            selectedOperation.authorised_by = authorisedByEntry.Text;
            selectedOperation.authorised_date = DateOnly.FromDateTime(authorisedDateEntry.Date);
            selectedOperation.start_date = DateOnly.FromDateTime(startDateEntry.Date);
            selectedOperation.end_date = DateOnly.FromDateTime(endDateEntry.Date);
            selectedOperation.rota_id = int.Parse(rotaIdEntry.Text);
            selectedOperation.operation_id = int.Parse(operationIdEntry.Text);
            selectedOperation.name = nameEntry.Text;
            selectedOperation.type = typeEntry.Text;
            selectedOperation.make = makeEntry.Text;
            selectedOperation.model = modelEntry.Text;
            selectedOperation.serial_number = int.Parse(serialEntry.Text);


            idEntryLabel.IsVisible = false;
            idEntry.IsVisible = false;

            equipmentEntryLabel.IsVisible = false;
            equipmentEntry.IsVisible = false;

            requestTypeEntryLabel.IsVisible = false;
            requestTypeEntry.IsVisible = false;

            requestedByEntryLabel.IsVisible = false;
            requestedByEntry.IsVisible = false;

            requestDateEntryLabel.IsVisible = false;
            requestDateEntry.IsVisible = false;

            authorisedByEntryLabel.IsVisible = false;
            authorisedByEntry.IsVisible = false;

            authorisedDateEntryLabel.IsVisible = false;
            authorisedDateEntry.IsVisible = false;

            startDateEntryLabel.IsVisible = false;
            startDateEntry.IsVisible = false;

            endDateEntryLabel.IsVisible = false;
            endDateEntry.IsVisible = false;

            rotaIdEntryLabel.IsVisible = false;
            rotaIdEntry.IsVisible = false;

            operationIdEntryLabel.IsVisible = false;
            operationIdEntry.IsVisible = false;

            nameEntryLabel.IsVisible = false;
            nameEntry.IsVisible = false;

            typeEntryLabel.IsVisible = false;
            typeEntry.IsVisible = false;

            makeEntryLabel.IsVisible = false;
            makeEntry.IsVisible = false;

            modelEntryLabel.IsVisible = false;
            modelEntry.IsVisible = false;

            serialEntryLabel.IsVisible = false;
            serialEntry.IsVisible = false;


            idLabel.Text = "Id : " + selectedOperation.id.ToString();
            equipmentLabel.Text = "Equipment Id : " + selectedOperation.equipment_id.ToString();
            requestedLabel.Text = "Requested By : " + selectedOperation.requested_by.ToString();
            requestTypeLabel.Text = "Request Type : " + selectedOperation.request_type.ToString();
            requestDateLabel.Text = "Request Date : " + selectedOperation.request_date.ToString();
            authorisedLabel.Text = "Authorised By : " + selectedOperation.authorised_by.ToString();
            authorisedDateLabel.Text = "Authorised On : " + selectedOperation.authorised_date.ToString();
            startLabel.Text = "Start Date : " + selectedOperation.start_date.ToString();
            endLabel.Text = "End Date : " + selectedOperation.end_date.ToString();
            rotaIdLabel.Text = "Rota Id : " + selectedOperation.rota_id.ToString();
            operationIdLabel.Text = "Operation Id : " + selectedOperation.operation_id.ToString();
            nameLabel.Text = "Name : " + selectedOperation.name.ToString();
            typeLabel.Text = "Type : " + selectedOperation.type.ToString();
            makeLabel.Text = "Make : " + selectedOperation.make.ToString();
            modelLabel.Text = "Model : " + selectedOperation.model.ToString();
            serialLabel.Text = "Serial Number : " + selectedOperation.serial_number.ToString();


            idLabel.IsVisible = true;
            equipmentLabel.IsVisible = true;
            requestTypeLabel.IsVisible = true;
            requestedLabel.IsVisible = true;
            requestDateLabel.IsVisible = true;
            authorisedLabel.IsVisible = true;
            authorisedDateLabel.IsVisible = true;
            startLabel.IsVisible = true;
            endLabel.IsVisible = true;
            rotaIdLabel.IsVisible = true;
            operationIdLabel.IsVisible = true;
            nameLabel.IsVisible = true;
            typeLabel.IsVisible = true;
            makeLabel.IsVisible = true;
            modelLabel.IsVisible = true;
            serialLabel.IsVisible = true;


            EditButton.IsVisible = true;
            SaveButton.IsVisible = false;
        }

        if (FilteredOperations.Contains(selectedOperation))
        {
            int index = FilteredOperations.IndexOf(selectedOperation);
            FilteredOperations[index] = selectedOperation;
        }

        FilteredOperations = Search(Equipment, searchCriteria);

        operationListView.ItemsSource = FilteredOperations;
    }
    catch (Exception ex)
    {
        ErrorLabel.Text = ex.Message;
    }
}
```

```c#
private void EditButton_Click(object sender, EventArgs e)
{
    try
    {
        if (selectedOperation != null)
        {
            idEntryLabel.IsVisible = true;
            idEntry.IsVisible = true;
            idEntry.Text = selectedOperation.id.ToString();

            equipmentEntryLabel.IsVisible = true;
            equipmentEntry.IsVisible = true;
            equipmentEntry.Text = selectedOperation.equipment_id.ToString();

            requestTypeEntryLabel.IsVisible = true;
            requestTypeEntry.IsVisible = true;
            requestTypeEntry.Text = selectedOperation.request_type;

            requestedByEntryLabel.IsVisible = true;
            requestedByEntry.IsVisible = true;
            requestedByEntry.Text = selectedOperation.requested_by;
        }
}
```

```c#
private List<Equipment> Search(List<Equipment> equipment, string searchCriteria)
{
    try
    {
        FilteredOperations = equipment.Where(value => value.id.ToString().Contains(searchCriteria, StringComparison.OrdinalIgnoreCase) || value.equipment_id.ToString().Contains(searchCriteria, StringComparison.OrdinalIgnoreCase) || value.requested_by.Contains(searchCriteria, StringComparison.OrdinalIgnoreCase) || value.request_date.ToString().Contains(searchCriteria, StringComparison.OrdinalIgnoreCase) || value.authorised_by.Contains(searchCriteria, StringComparison.OrdinalIgnoreCase) || value.start_date.ToString().Contains(searchCriteria, StringComparison.OrdinalIgnoreCase) || value.end_date.ToString().Contains(searchCriteria, StringComparison.OrdinalIgnoreCase) || value.rota_id.ToString().Contains(searchCriteria, StringComparison.OrdinalIgnoreCase) || value.operation_id.ToString().Contains(searchCriteria, StringComparison.OrdinalIgnoreCase) || value.name.Contains(searchCriteria, StringComparison.OrdinalIgnoreCase) || value.name.Contains(searchCriteria, StringComparison.OrdinalIgnoreCase) || value.type.Contains(searchCriteria, StringComparison.OrdinalIgnoreCase) || value.make.Contains(searchCriteria, StringComparison.OrdinalIgnoreCase) || value.model.Contains(searchCriteria, StringComparison.OrdinalIgnoreCase) || value.serial_number.ToString().Contains(searchCriteria, StringComparison.OrdinalIgnoreCase)).ToList();
        return FilteredOperations;
    }
    catch (Exception ex)
    {
        ErrorLabel.Text = ex.Message;
        return null;
    }
}
```

```c#

```

## Description of Code



## Screenshots of Program



## Code Review



## Reflection
