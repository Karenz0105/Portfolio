## Aim

The aim for the next few weeks is to create code based off a user story.

## Issue working on

As I didn't finish the user story I selected last week I decided to continue working on that one to fully complete it before moving onto a new user story.

The user story I continued to work on was "As an UNDAC Deputy Team Leader I want to view details of all team partners so that I can contact them immediately".

The end goal for this user story is to have a section of code that in the program would allow a Deputy Team Leader to search and view Team Partners information.

There are a few set criterias for this part of the program, these are :
* Team Partners can be listed with their current association status
* Team Partner details can be viewed easily
* Search bar to filter list of Team Partners
* Information can be cleared

## Code Snippet

Class
```c#
public class TeamPartners
{
    public int id { get; set; }
    public int organisation_id { get; set; }
    public int team_id {  get; set; }
    public string name { get; set; }
    public string type { get; set; }
    public int country_id { get; set; }
    public string contact_email { get; set; }
    public int contact_telephone { get; set; }
    public string status { get; set; }
}
```

TeamPartnersView
```c#
public partial class TeamPartnersView : ContentPage
{
	public List<TeamPartners> TeamPartners { get; set; }
	public List<TeamPartners> FilteredTeamPartners { get; set; }
	private TeamPartners selectedTeamPartner;

	public TeamPartnersView()
	{
		InitializeComponent();

        	TeamPartners = GetTeamPartnerDetails();

		BindingContext = this;

        	nameLabel.Text = "Name : ";
        	idLabel.Text = "ID : ";
        	organisationLabel.Text = "Organisation ID : ";
        	teamLabel.Text = "Team ID : ";
        	typeLabel.Text = "Type : ";
        	CountryLabel.Text = "Country ID : ";
        	ContactEmailLabel.Text = "Email : ";
        	ContactPhoneLabel.Text = "Phone : ";
        	StatusLabel.Text = "Status : ";
    	}

	private void SearchButton_Click(object sender, EventArgs e)
	{
		try
		{
			string searchCriteria = SearchTextBox.Text;
			
			FilteredTeamPartners = Search(TeamPartners, searchCriteria);

			teamPartnerListView.ItemsSource = FilteredTeamPartners;

			if (FilteredTeamPartners.Count > 0)
			{
				var foundTeamPartner = FilteredTeamPartners[0];
			}
		}
		catch (Exception ex)
		{
			ErrorLabel.Text += ex.Message;
		}
	}

	private void ClearButton_Click(object sender, EventArgs e)
	{
        	nameLabel.Text = "Name : ";
        	idLabel.Text = "ID : ";
        	organisationLabel.Text = "Organisation ID : ";
        	teamLabel.Text = "Team ID : ";
        	typeLabel.Text = "Type : ";
        	CountryLabel.Text = "Country ID : ";
        	ContactEmailLabel.Text = "Email : ";
        	ContactPhoneLabel.Text = "Phone : ";
        	StatusLabel.Text = "Status : ";
		ErrorLabel.Text = "";
    	}

    	private void ViewButton_Click(object sender, EventArgs e)
    	{
		try
		{
			if (selectedTeamPartner != null)
			{
				nameLabel.Text = "Name : " + selectedTeamPartner.name;
				idLabel.Text = "ID : " + selectedTeamPartner.id.ToString();
				organisationLabel.Text = "Organisation ID : " + selectedTeamPartner.organisation_id.ToString();
				teamLabel.Text = "Team ID : " + selectedTeamPartner.team_id.ToString();
				typeLabel.Text = "Type : " + selectedTeamPartner.type;
				CountryLabel.Text = "Country ID : " + selectedTeamPartner.country_id.ToString();
				ContactEmailLabel.Text = "Email : " + selectedTeamPartner.contact_email;
				ContactPhoneLabel.Text = "Phone : " + selectedTeamPartner.contact_telephone.ToString();
                		StatusLabel.Text = "Status : " + selectedTeamPartner.status;
            		}
		}
		catch (Exception ex)
		{
			ErrorLabel.Text += ex.Message;
		}
    	}

    	private void ListView_ItemSelected(object sender, SelectedItemChangedEventArgs e)
	{
		selectedTeamPartner = e.SelectedItem as TeamPartners;
	}

    	private List<TeamPartners> GetTeamPartnerDetails()
	{
		var teamPartners = new List<TeamPartners>
		{
			new TeamPartners { name = "John Smith", id = 1, organisation_id = 00001,
			team_id = 01 , type = "CEO", country_id = 45, contact_email = "johnsmith@gmail.com",
			contact_telephone = 01111234567, status = "Requested"} ,
			new TeamPartners { name = "Alice Gates", id = 2, organisation_id = 00002,
			team_id = 02, type = "Staff", country_id = 32, contact_email = "alicegates@gmail.com",
			contact_telephone = 01321234767, status = "Confirmed" } ,
            		new TeamPartners { name = "Phil Green", id = 3, organisation_id = 00004,
			team_id = 03 , type = "CEO", country_id = 23, contact_email = "philgreen@gmail.com",
			contact_telephone = 01567159621, status = "Requested"} ,
            		new TeamPartners { name = "Logan Brown", id = 4, organisation_id = 00004,
			team_id = 04, type = "Junior", country_id = 27, contact_email = "loganbrown@gmail.com",
			contact_telephone = 01237569842, status = "Confirmed" }
        	};
		return teamPartners;
	}

	private List<TeamPartners> Search(List<TeamPartners> teamPartners, string searchCriteria)
	{
        FilteredTeamPartners = GetTeamPartnerDetails().Where(
	value => value.name.Contains(searchCriteria, StringComparison.OrdinalIgnoreCase)
	|| value.id.ToString().Contains(searchCriteria, StringComparison.OrdinalIgnoreCase)
	|| value.organisation_id.ToString().Contains(searchCriteria, StringComparison.OrdinalIgnoreCase)
	|| value.team_id.ToString().Contains(searchCriteria, StringComparison.OrdinalIgnoreCase)
	|| value.type.Contains(searchCriteria, StringComparison.OrdinalIgnoreCase)
	|| value.country_id.ToString().Contains(searchCriteria, StringComparison.OrdinalIgnoreCase)
	|| value.contact_email.Contains(searchCriteria, StringComparison.OrdinalIgnoreCase)
	|| value.contact_telephone.ToString().Contains(searchCriteria, StringComparison.OrdinalIgnoreCase)).ToList();

        return FilteredTeamPartners;
	}
}
```

XAML
```c#
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="UNDAC_App.TeamPartnersView"
             Title="TeamPartnersView">

    <StackLayout Margin="20">
        <Entry x:Name="SearchTextBox"  Placeholder="Search" FontSize="18"/>

        <StackLayout Orientation="Horizontal" Spacing="10">
            <Button Text="Search" Clicked="SearchButton_Click" FontSize="18"/>
            <Button Text="Clear" Clicked="ClearButton_Click" FontSize="18"/>
        </StackLayout>

        <ListView x:Name="teamPartnerListView" ItemsSource="{Binding FilteredTeamPartner}" SelectedItem="{Binding SelectedItem}" ItemSelected = "ListView_ItemSelected">
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

        <StackLayout Orientation="Horizontal" Spacing="10">
            <Button Text="View" Clicked="ViewButton_Click" FontSize="18"/>
        </StackLayout>

        <StackLayout>
            <Label Text="Team Partner Information : " FontSize="20" TextDecorations="Underline" FontAttributes="Bold"/>
            <Label Text=""/>
            <Label x:Name="nameLabel" FontSize="18"/>
            <Label x:Name="idLabel" FontSize="18"/>
            <Label x:Name="organisationLabel" FontSize="18"/>
            <Label x:Name="teamLabel" FontSize="18"/>
            <Label x:Name="typeLabel" FontSize="18"/>
            <Label x:Name="CountryLabel" FontSize="18"/>
            <Label x:Name="ContactEmailLabel" FontSize="18"/>
            <Label x:Name="ContactPhoneLabel" FontSize="18"/>
            <Label x:Name="StatusLabel" FontSize="18"/>
        </StackLayout>

        <Label x:Name="ErrorLabel"/>

    </StackLayout>
</ContentPage>
```


## Description of Code

In the Class section of code, it is being used to set up any variables we will need and will be used throughout the program, mostly in the piece of code I was writing.

In the TeamPartnersView section of code, it is basically the main section of code for the program to run what I was working on. The code first sets up some lists and gets the information about the Team Partners and sets up the display labels. The code then goes on depending which button you select on the screen. If you select the 'Clear' button it will clear all labels. If you select the 'Search button' it will search for the information you have provided in the search bar and if there is a match it will then be displayed into the list view. That piece of code also related to the piece of code at the bottom that searches the list and filters the items for the search. Then the 'View button' code checks if an item in the list has been selected. It will then display the information corresponding to that selected item.

In the XAML section of code, it just lays out how the user interface looks. The way it is set up is that the search bar is at the top of the screen, then underneath is the Search and Clear buttons, then the ListView, then the View button and then all the labels to display information.

# Screenshots of Program

![Selecting view TeamPartnersView](https://github.com/Karenz0105/Portfolio/blob/main/images/Screenshot%20(10).png)

In the above screenshot, we select on the 'view TeamPartnersView' to get to my section of the program I was working on.

![View of TeamPartnersView](https://github.com/Karenz0105/Portfolio/blob/main/images/Screenshot%20(11).png)

Once we are in this section of the program we can see multiple things, such as :
* Search Bar
* Search Button
* Clear Button
* ListView
* View Button
* Display Labels

![Searching "CEO"](https://github.com/Karenz0105/Portfolio/blob/main/images/Screenshot%20(12).png)

In the search bar we can put in a search criteria that we wish to searh, in the screenshot I selected to search for "CEO". From that search there are two Team Partners that come up.

![Selecting and viewing Team Partner](https://github.com/Karenz0105/Portfolio/blob/main/images/Screenshot%20(13).png)

We can then select on one of the Team Partners, and press the View Button. Once that is done it will display the selected Team Partners information.

## Test Code

```c#
namespace UnitTest_TeamPartners_DisplayUpdate
{
    public class UnitTest1
    {
        [Fact]
	public void ViewButton_Update_Labels()
	{
		var teamPartnersView = new TeamPartnersView();
		teamPartnersView.selectTeamPartner = new TeamPartners
		{
			name = "John Smith",
			id = 1,
			organisation_id = 1,
			team_id = 1,
			type = "CEO",
			country_id = 45,
			contact_email = "johnsmith@gmail.com",
			contact_telephone = 1111234567,
			status = "Requested"
		};

		teamPartnerView.ViewButton_Click(null, null);

		Assert.Equal("John Smith", teamPartnersView.nameLabel);
		Assert.Equal(1, teamPartnersView.idLabel);
		Assert.Equal(1, teamPartnersView.organisationLabel);
		Assert.Equal(1, teamPartnersView.teamLabel);
		Assert.Equal("CEO", teamPartnersView.typeLabel);
		Assert.Equal(45, teamPartnersView.CountryLabel);
		Assert.Equal("johnsmith@gmail.com", teamPartnersView.ContactEmailLabel);
		Assert.Equal(1111234567, teamPartnersView.ContactPhoneLabel);
		Assert.Equal("Requested", teamPartnersView.StatusLabel);
	}
}
```

## Unit Test Performed

The above Unit Test that is being performed is to check if the display would be correctly updated once the View button is clicked.

In the test we are comparing the values to see if they match each other as it is to represent that those values are already stored within the system.

The Assert.Equal() parts of the code are comparing that the values entered would match.

In this case the Unit Test passes.

## Code Review

From the code review that happened with my code this week, it was given that my code is much better than last week and flows nicely. There aren't any issues that the code reviewer spotted.

The code review I did on another team members code was good, they had followed Clean Code principles and didn't have anything wrong with their code.

## Reflection

Continuing on this week with the project was much easier as I decided to focus on just the task I selected last week. I decided to do this as I could produce a better piece of code for the project and I didn't want to overwhelm myself with extra sections of code to work on.

After thinking about the program more this week, I realised I had previously made something similar that could help me with the coding. Last year in College I created a program that you could select a user from a listbox and display their information, the only difference with this program was that I also needed to put in the search feature and make it work with that but it was easy enough to do once I played around with the code.

My overall opinion on the user story I selected and code I made for it, is that I did pretty well and have created a piece of code that mostly follows the criteria, at least in my opinion it does follow it but it depends on how strict the criteria is meant to be.

As these next few weeks go on with the project, I am hoping to improve my coding skills more and practice Clean Coding principles more.
