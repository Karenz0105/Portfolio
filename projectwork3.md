## Aim

The aim for the remaining weeks of this module is to continue on the Team Project.

## Issue working on

The user story I selected to work on this week was "As an UNDAC Team Support and Logistics Manager, I want to assign vehicles and other equipment to operations on request so that assignments are appropriately equipped."

The end goal for this user story is to have a section of the program that you can view and process requests for operations and assign vehicles and equipment to those operations.

For this user story there are some main criteria :
* Current and future operations can be viewed in a list
* New requests will be highlighted in the list
* List filters can be cleared
* Details of operations and requests can be viewed
* Requests can be approved

## Progress so far

Sadly I wasn't able to complete this section of the program within the week. It was a much more demanding task than I originally thought but I got the basics down of being able to search some items as I used the code I created in the previous week as a guide.

Currently in the program you can search just the name right now and see in the list the name and request type. You can also view when the item is selected in the list, but not much details appear as they are not all set yet.

## Code Snippet

Class

```c#
public class Equipment
{
    public int id { get; set; }

    public int equipment_id { get; set; }

    public string requested_by { get; set; }
    public string request_type { get; set; }

    public DateOnly request_date { get; set; }

    public string authorised_by { get; set; }

    public DateOnly authorised_date { get; set; }

    public DateOnly start_date { get; set; }

    public DateOnly end_date { get; set; }

    public int rota_id { get; set; }

    public int operation_id { get; set; }

    public string name { get; set; }

    public string type { get; set; }

    public string make {  get; set; }

    public string model { get; set; }

    public int serial_number { get; set; }
}
```

AssignEquipment
```c#
private void SearchButton_Click(object sender, EventArgs e)
{
    try
    {
        string searchCriteria = SearchTextBox.Text;

        FilteredOperations = Search(Equipment, searchCriteria);

        operationListView.ItemsSource = FilteredOperations;

        if (FilteredOperations.Count > 0)
        {
            var foundOperation = FilteredOperations[0];
        }
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
        if (selectedOperation != null)
        {
            idLabel.Text = "Id : " + selectedOperation.id.ToString();
            equipmentLabel.Text = "Equipment Id : " + selectedOperation.equipment_id.ToString();
            requestTypeLabel.Text = "Request Type : " + selectedOperation.request_type; 
            requestedLabel.Text = "Requested By : " + selectedOperation.requested_by;
            requestDateLabel.Text = "Request Date : " + selectedOperation.request_date;
            authorisedLabel.Text = "Authorised By : " + selectedOperation.authorised_by;
            authorisedDateLabel.Text = "Authorused On : " + selectedOperation.authorised_date;
            startLabel.Text = "Start Date : " + selectedOperation.start_date;
            endLabel.Text = "End Date : " + selectedOperation.end_date;
            rotaIdLabel.Text = "Rota Id : " + selectedOperation.rota_id.ToString();
            operationIdLabel.Text = "Operation Id : " + selectedOperation.operation_id.ToString();
            nameLabel.Text = "Name : " + selectedOperation.name;
            typeLabel.Text = "Type : " + selectedOperation.type;
            makeLabel.Text = "Make : " + selectedOperation.make;
            modelLabel.Text = "Model : " + selectedOperation.model;
            serialLabel.Text = "Serial Number : " + selectedOperation.serial_number.ToString();
        }
    }
    catch (Exception ex)
    {
        ErrorLabel.Text += ex.Message;
    }
}

private void ListView_ItemSelected(object sender, SelectedItemChangedEventArgs e)
{
    selectedOperation = e.SelectedItem as Equipment;
}

private List<Equipment> Search(List<Equipment> equipment, string searchCriteria)
{
    FilteredOperations = GetOperations().Where(value => value.name.Contains(searchCriteria, StringComparison.OrdinalIgnoreCase)).ToList();
    return FilteredOperations;
}
```

## Description of Code

In the Class section of the code, we are setting up the variables we will be using in this section of the program.

In the AssignEquipment section of the code, it is showing a very basic of the search system. Similar to last weeks coding I did.

## Code Review

As I don't really have much code to be reviewed, I didn't get anybody to do a code review as there isn't enough there to review.

The code I reviewed for another team member was fine, it followed Clean Code principles.

## Reflection

This week, I didn't do the best with my user story as many things happened throughout the week, and I couldn't spend enough time to focus on this.

However, I managed to follow the new tutorial on setting up a database with SQLite, which made it much easier to understand compared to the original Microsoft version.

My goal for the next week will be to try my best to finish this user story and implement the features that are stated in the end goals and criteria.

From this week, I realized that I need to try and spend more time coding and figuring out how to implement new things.

Personally, I find the .NET Maui App a bit challenging to fully grasp. This is because previously I used WPF Application, so I am a lot more used to how that functions with the use of XAML.

Nevertheless, I hope to improve with using .NET Maui over the ramining weeks.

