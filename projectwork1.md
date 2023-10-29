# Project Work 1

## Aim

Over the next few weeks our aim is to complete a section of code based off a selected user story.

## Issue working on

The issue I have chose to work on is the user story ;

"As an UNDAC Deputy Team Leader I want to view details of all team partners so that I can contact them immediately"

The idea behind this user story is that the Deputy Team Leader will be able to view the contact information about team partners.


## Code snippet

```c#
namespace UNDAC_App.Models
{
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
    }
}
```

```c#
public partial class TeamPartnersView : ContentPage
{
	// List of Team Partners
	public List<TeamPartners> TeamPartners { get; set; }

	public TeamPartnersView()
	{
		InitializeComponent();

		// Get Team Partner details
		var teamPartnerDeatils = GetTeamPartnerDetails();

		// Creates a new list to store Team Partner information
		TeamPartners = new List<TeamPartners>();

		BindingContext = this;

	}

	private void SearchButton_Click(object sender, EventArgs e)
	{
		// Get search criteria entered by user from textbox
		string searchCriteria = SearchTextBox.Text;
		// Check list for search criteria
		List<TeamPartners> filteredTeamPartners = Search(TeamPartners, searchCriteria);

		// If search criteria is found then display
		if (filteredTeamPartners.Count > 0)
		{
			var foundTeamPartner = filteredTeamPartners[0];
			nameLabel.Text = foundTeamPartner.name;
			idLabel.Text = foundTeamPartner.id.ToString();
		}
		// If it isn't found then don't show anything
		else
		{
			nameLabel.Text = "";
			idLabel.Text = "";
		}
	}

	private List<TeamPartners> GetTeamPartnerDetails()
	{
		// Creates list of Team Partners
		var teamPartners = new List<TeamPartners>
		{
			new TeamPartners { name = "abc", id = 1, organisation_id = 1, team_id = 1 },
			new TeamPartners { name = "123", id = 2, organisation_id = 2, team_id = 2 }
		};

		// Return list of Team Partners
		return teamPartners;

	}

	private List<TeamPartners> Search(List<TeamPartners> teamPartners, string searchCriteria)
	{
		// Filter Team Partners by name
		List<TeamPartners> filteredTeamPartners = teamPartners.Where(value => value.name.Contains(searchCriteria)).ToList();

		// Return the filtered Team Partners
		return filteredTeamPartners;
	}
}
```

```c#

```

```c#

```

```c#

```


## Description of code



## Reflection on code review



## Summary of any issues with code after code review



## Reflection

