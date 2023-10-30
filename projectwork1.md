# Project Work 1

## Aim

Over the next few weeks our aim is to complete a section of code based off a selected user story.

## Issue working on

The user story I have selected to work on is - "As an UNDAC Deputy Team Leader I want to view details of all team partners so that I can contact them immediately".

The idea behind this user story is that the Deputy Team Leader will be able to view the contact information for team partners.

The end goals for this user story are:
* User is able to contact Team Partners efficiently
* Team has access to support that they need

## Code snippet

Below is some of the code I have written for this task, it is not completed yet.

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
	List<TeamPartners> filteredTeamPartners = teamPartners.Where
	(value => value.name.Contains(searchCriteria)).ToList();

	// Return the filtered Team Partners
	return filteredTeamPartners;
}
```


## Description of Code

The first piece of code is getting and setting all values that we will need for this task.

The second piece of code includes:
* Code for a search bar - this works a little right now, but no outputs are being displayed so unsure how well it works
* Code to filter the list of team partners - unsure how well this is working right now as nothing useful is displayed when tried
* Code to add team partners to a list - this should work fine, but haven't been able to test if it has as nothing being displayed

These two pieces of code I have provided are fine for now as it is not yet completed. As I go on with this task I will improve the above code by following Clean Code practices.

## Test Code

```c#
namespace UnitTest_TeamPartners_DisplayUpdate
{
    public class UnitTest1
    {
        [Fact]
        public void Test1()
        {
		var teamPartnersView = new TeamPartnersView();
		teamPartnersView.SearchTextBox.Text = "abc";
		var expectedName = "abc";
		var expectedId = 1;

		teamPartnersView.SearchButton_Click(null, null)

		Assert.Equal(expectedName, teamPartnersView.nameLabel.Text);
		Assert.Equal(expectedId, int.Parse(teamPartnersView.idLabel.Text));
        }
    }
}

```

## Unit Test Performed

The above Unit Test that is being performed is to check if the display would update correctly if an input was entered into the SearchTextBox.

In this test we are checking if the entered name "abc" would match an existing value in the TeamPartners list. We have an expectedName value of "abc", so in this case it would match.

The output from this unit test would change the nameLabel and idLabel to the corresponding values in the list from the search criteria.

The Assert.Equal() parts of the code are to take the expected value and compare it with the actual value we got.

In this case the Unit Test passes.

## Reflection on Code Review

From the code review that happened with my code a few things were pointed out:
* Too many comments
* Code that might not be needed/makes code too complicated

This was understandable for these to be picked up on as the code isn't finished yet and still needs to be worked on to be fully completed. But even though it isn't done I will take the feedback and work with it as I finish completeing the task.

## Code Review of Others

From what I reviewed on another team members code, it pretty much followed the Clean Code principles pretty well. I didn't really spot anything that seemed like bad coding practice!

## Reflection

Working on a proper project has been a hard task so far, it can be really confusing and stressful at times! But it is a useful experience to do. As I go on with this for the next few weeks I expect to improve my skills with writing and reviewing code.

I did have some issues this week with trying to find the original user stories file on the class Github, as I was looking for more information on the tasks to pick one. It took a while to find but once I found the file it helped a lot to more understand what the user story was wanting from me.

Trying to code based off the user story was also challenging as the one I selected is mostly just to display information depending on the user, but so far I think I am making good progress. I believe it will take a little more time to fully finish this task but I hope to have it pretty well done when I complete it.
