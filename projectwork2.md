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
			new TeamPartners { name = "John Smith", id = 1, organisation_id = 00001, team_id = 01 , type = "CEO", country_id = 45, contact_email = "johnsmith@gmail.com", contact_telephone = 01111234567, status = "Requested"} ,
			new TeamPartners { name = "Alice Gates", id = 2, organisation_id = 00002, team_id = 02, type = "Staff", country_id = 32, contact_email = "alicegates@gmail.com", contact_telephone = 01321234767, status = "Confirmed" } ,
            new TeamPartners { name = "Phil Green", id = 3, organisation_id = 00004, team_id = 03 , type = "CEO", country_id = 23, contact_email = "philgreen@gmail.com", contact_telephone = 01567159621, status = "Requested"} ,
            new TeamPartners { name = "Logan Brown", id = 4, organisation_id = 00004, team_id = 04, type = "Junior", country_id = 27, contact_email = "loganbrown@gmail.com", contact_telephone = 01237569842, status = "Confirmed" }
        };

		return teamPartners;
	}

	private List<TeamPartners> Search(List<TeamPartners> teamPartners, string searchCriteria)
	{
        FilteredTeamPartners = GetTeamPartnerDetails().Where(value => value.name.Contains(searchCriteria, StringComparison.OrdinalIgnoreCase) || value.id.ToString().Contains(searchCriteria, StringComparison.OrdinalIgnoreCase) || value.organisation_id.ToString().Contains(searchCriteria, StringComparison.OrdinalIgnoreCase) || value.team_id.ToString().Contains(searchCriteria, StringComparison.OrdinalIgnoreCase) || value.type.Contains(searchCriteria, StringComparison.OrdinalIgnoreCase) || value.country_id.ToString().Contains(searchCriteria, StringComparison.OrdinalIgnoreCase) || value.contact_email.Contains(searchCriteria, StringComparison.OrdinalIgnoreCase) || value.contact_telephone.ToString().Contains(searchCriteria, StringComparison.OrdinalIgnoreCase)).ToList();

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



## Test Code



## Unit Test Performed



## Code Review



## Reflection


