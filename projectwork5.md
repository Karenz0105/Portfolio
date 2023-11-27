## Aim

The aim for this week is to finish off a final user story and reflect on portfolio entries.

## Issue Working On

The user story I selected to work on this week was "As an UNDAC Analyst, I want to view the status of current and completed operations so that I can evaluate the effectiveness of the mission."

The goal for this user story is for an Analyst user to view operations and evaluate how effective the mission has been.

The main criteria for this user story is :

* Operations can be viewed in a list
* Operation details can be viewed


## Code Snippet

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

## Description of Code

In the above Class code, it shows all the variables that are used within this section of the program, by getting and setting them to be used.

In the XAMl code above, it shows the layout of how the interface looks for this section of the program. It is a very simple layout that includes:
* View Button
* Clear Button
* List
* Display area

In the last section of code, it shows how the program runs. The way this section of code works is that when a user selects an item in the list then clicks view, the program will get the information associated with the selected item and display it for the user to see. There is also a clear button for when a user wants to clear what has already been displayed.

## Screenshots of Program

![Selecting view OperationalStatus](https://github.com/Karenz0105/Portfolio/blob/main/images/Screenshot%20(23).png)

In the above screenshot we select the 'view OperationalStatus' button to get to the section of the program that we want to be in.

![OperationalStatus Interface](https://github.com/Karenz0105/Portfolio/blob/main/images/Screenshot%20(24).png)

Once we have selected the button to get to the section of the program we want to be in, we are greeted with this interface. It shows a 'View' and 'Clear' button. Underneath a list with the operations and below the list a display area that will display the operation information.

![Viewing Operation 1](https://github.com/Karenz0105/Portfolio/blob/main/images/Screenshot%20(25).png)

We can view an operation by first selectin in the list box which operation, in the above screenshot we select 'Operation 1', then we select the 'View' button. In the display area, the informaiton will now be updated to the information for that operation.

![Viewing Operation 2](https://github.com/Karenz0105/Portfolio/blob/main/images/Screenshot%20(26).png)

Viewing another operation is just the same as above, we will just select a different operation and then select the 'View' button. The information in the display area will then be updated to display the information for that operation.

## Code Review

For the final code review on my code, it was said that it is good and that it has improved each week since the start of the team project.

For the last code review I did, I was very impressed by the others with how much they have improved with what they have been coding.

## Reflection

Over these past few weeks working on the Team Project, I have learned a lot about coding better than I had before. I have been able to put into practise many of the things we learned in the lectures and improve on them each week, by learning what I was doing wrong and with feedback from the others in the team.

I am proud of the progress I have made, even if it took a little while to get there on some parts, it was still a good learning experience and I am happy to have progressed from the start to now.

This week with my final piece for the team project, I selected one that seemed easy but that I could improve with what I had done in the previous weeks. I was able to notice when I repeated sections of code and made the coding the best I could for this last submission.

Overall, from the start of this module to now I have learned many useful things to help with being a Software Engineer. Many things that I can further study about and learn more on and other things that I can put into practise and improve on.

From when I did my first portfolio to now, I have improved much more than I thought I would have. At the start of the portfolios I was unsure if I was doing it correctly, everything was feeling like a riddle. But as it went on and asking others to make sure, checking the guides, I became more confident that I was doing the portfolios correctly.

I am very proud of all the progress I have made with the portfolios, they will be an excellent resource to look back on and provide as evidence for working in a team setting and with using new equipment that I haven't used before, like Github.

My final notes on all that I have done in this module and how it has went is that it was a bumpy ride, there was some difficult moments. But as with everything, it takes time and practise to get through it. I know I can improve much more with my coding and with using Github, but for just the past few months of doing so for this module I am happy with the progress that has been made.


