## Aim

The aim for this week is to finish off a final user story and reflect on portfolio entries.

## Issue Working On

As an UNDAC Analyst, I want to view the status of current and completed operations so that I can evaluate the effectiveness of the mission

The user story I selected to work on this week was "As an UNDAC Analyst, I want to view the status of current and completed operations so that I can evaluate the effectiveness of the mission."

The goal for this user story is for an Analyst user to view operations and evaluate how effective the mission has been.

The main criteria for this user story is :

* Operations can be viewed in a list
* Operation details can be viewed


## Code

Class
```c#
public class OperationStatuses
{
    public string name {  get; set; }
    public int id { get; set; }
    public int operational_team_id { get; set; }
    public DateOnly date {  get; set; }
    public string status { get; set; }
    public int latitude { get; set; }
    public int longitude { get; set; }
    public string comments { get; set; }

}
```

XAML
```c#
<ScrollView>
    <StackLayout Margin="20">
        <StackLayout Orientation="Horizontal" Spacing="10">
            <Button Text="View" Clicked="ViewButton_Click" FontSize="18"/>
            <Button Text="Clear" Clicked="ClearButton_Click" FontSize="18"/>
        </StackLayout>

        <ListView x:Name="operationsListView" ItemsSource="{Binding operationalStatuses}" ItemSelected = "ListView_ItemSelected">
            <ListView.ItemTemplate>
                <DataTemplate>
                    <ViewCell>
                        <StackLayout Orientation="Horizontal">
                            <Label Text="{Binding name}" FontSize="18"/>
                            <Label Text=" -  " FontSize="18"/>
                            <Label Text="{Binding status}" FontSize="18"/>
                        </StackLayout>
                    </ViewCell>

                </DataTemplate>
            </ListView.ItemTemplate>
        </ListView>

        <StackLayout>
            <Label Text="Operation Information : " FontSize="20" TextDecorations="Underline" FontAttributes="Bold"/>
            <Label Text=""/>
            <Label x:Name="nameLabel" FontSize="18"/>
            <Label x:Name="idLabel" FontSize="18"/>
            <Label x:Name="operationIdLabel" FontSize="18"/>
            <Label x:Name="dateLabel" FontSize="18"/>
            <Label x:Name="statusLabel" FontSize="18"/>
            <Label x:Name="latitudeLabel" FontSize="18"/>
            <Label x:Name="longitudeLabel" FontSize="18"/>
            <Label x:Name="commentsLabel" FontSize="18"/>
        </StackLayout>

        <Label x:Name="ErrorLabel"/>

    </StackLayout>
</ScrollView>

```

OperationalStatus
```c#
public List<OperationStatuses> operationalStatuses { get; set; }
private OperationStatuses selectedOperation;

public OperationalStatus()
{
    InitializeComponent();

    operationalStatuses = GetStatus();
    operationsListView.ItemsSource = operationalStatuses;

    if (operationalStatuses.Count > 0)
    {
        selectedOperation = operationalStatuses[0];
        UpdateOperationDetails(selectedOperation);
    }

    nameLabel.Text = "Name : ";
    idLabel.Text = "Id : ";
    operationIdLabel.Text = "Operational Team Id : ";
    dateLabel.Text = "Date : ";
    statusLabel.Text = "Status : ";
    latitudeLabel.Text = "Latitude : ";
    longitudeLabel.Text = "Longitude : ";
    commentsLabel.Text = "Comments : ";
}

private List<OperationStatuses> GetStatus()
{
    try
    {
        var status = new List<OperationStatuses>
        {
            new OperationStatuses { name = "Operation 1", id = 1, operational_team_id = 1, date = new DateOnly(2023, 11, 15) , status = "Complete", latitude = 40, longitude = 118, comments = "Completed Operation" },
            new OperationStatuses { name = "Operation 2", id = 2, operational_team_id = 2, date = new DateOnly(2023, 11, 24) , status = "Ongoing", latitude = 90, longitude = 139, comments = "Ongoing Operation" }


        };

        return status;
    }
    catch (Exception ex)
    {
        ErrorLabel.Text += ex.Message;
        return null;
    }
}

private void UpdateOperationDetails(OperationStatuses selectedOperation)
{
    try
    {
        nameLabel.Text = $"Name : {selectedOperation.name}";
        idLabel.Text = $"Id : {selectedOperation.id}";
        operationIdLabel.Text = $"Operational Team Id : {selectedOperation.operational_team_id}";
        dateLabel.Text = $"Date : {selectedOperation.date}";
        statusLabel.Text = $"Status : {selectedOperation.status}";
        latitudeLabel.Text = $"Latitude : {selectedOperation.latitude}";
        longitudeLabel.Text = $"Longitude : {selectedOperation.longitude}";
        commentsLabel.Text = $"Comments : {selectedOperation.comments}";
    }
    catch (Exception ex)
    {
        ErrorLabel.Text += ex.Message;
    }
}

private void ClearButton_Click(object sender, EventArgs e)
{
    try
    {
        nameLabel.Text = "Name : ";
        idLabel.Text = "Id : ";
        operationIdLabel.Text = "Operational Team Id : ";
        dateLabel.Text = "Date : ";
        statusLabel.Text = "Status : ";
        latitudeLabel.Text = "Latitude : ";
        longitudeLabel.Text = "Longitude : ";
        commentsLabel.Text = "Comments : ";
    }
    catch (Exception ex)
    {
        ErrorLabel.Text += ex.Message;
    }
}

private void ListView_ItemSelected(object sender, SelectedItemChangedEventArgs e)
{
    try
    {
        selectedOperation = e.SelectedItem as OperationStatuses;
    }
    catch (Exception ex)
    {
        ErrorLabel.Text += ex.Message;
    }
}

private void ViewButton_Click(object sender, EventArgs e)
{
    try
    {
        if (operationsListView.SelectedItem is OperationStatuses selectedItem)
        {
            UpdateOperationDetails(selectedItem);
        }
    }
    catch (Exception ex)
    {
        ErrorLabel.Text += ex.Message;
    }
}
```

## Description


## Code Review


## Reflection
