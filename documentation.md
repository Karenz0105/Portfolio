# Documentation



## Aim

The aim for this week is to provide an explanation for Clean Code rules and to demonstrate Doxygen.



## Clean Code Rules

There are multiple types of Clean Code rules, below are a few of them.



### Meaningful Names

Meaningful Names is one of the Clean Code rules that is important to follow, the reason for this rule is to make our code easier to read and easier to understand. We want to give any variable, class or function a Meaningful Name, this is so we can understand what each is doing without adding comments. Meaningful Names should give an idea of what the piece of code is about, or what it is doing.

```
int banana;
int house;

house = banana + 3;
```

The above code is an example of a piece of code with names that wouldn't be meaningful. We have no idea what the code is for or doing. To improve the code we would have to change these names to something that represents what they store.

```
int numOfBananas;
int bananaHouseTotal;

bananaHouseTotal = numOfBananas + 3;
```

With just changing the variable names, we give that small piece of code alot more meaning and make it more understandable for somebody looking at the code.



### Comments

Comments are an excellent thing to use while coding, this is because they can help you for future reference when you come back to it. But in a Clean Code approach they aren't the best to use. The code you write should be self explanatory just by reading what has been written. However, it is still fine to use comments within a Clean Code approach, but only in some situations. It would be fine to use them to explain what a function is doing if it is more complex than just what is written with the variable names.

```
// Ask user for how many cheese slices they want to purchase
Console.WriteLine("Number : ")

// Get how many cheese slices they wish to purchase
int userInput = Console.ReadLine();

// Display how many
Console.WriteLine(userInput);
```

The above piece of code is an example of how comments could be used, but shouldn't be used. This is a very simple piece of code, that if written better would be easier to understand.

```
Console.WriteLine("How many slices of cheese would you like to purchase? : ")

int cheeseSlicePurchaseInput = Console.ReadLine():

Console.WriteLine("You would like to purchase : " + cheeseSlicePurchaseInput + ". Is this correct?")
```

In the above example now, the code has been written slightly better. It now is a lot more understandable and doesn't need the comments anymore to explain what is happening.



### Formatting





### Functions





### KISS

KISS is a Software Engineering Principle that extends to Clean Code Principles. KISS stands for "Keep It Simple, Stupid". The general idea of this is to help with Clean Code to eliminate any complexity that isn't needed within the code. This is so if you were to come back to the program at a later date, you could still understand what the code is doing without questioning it.



### YAGNI

YAGNI is another Software Engineering Principle that extends to Clean Code Principles. YAGNI stands for "You Ain't Gonna Need It". The idea behind this rule is to not assume you will need certain pieces of code later and end up coding them earlier, because in most cases you might not need it or never end up using it, which will just end up making the program clunky with unnecssary code. 


## Coding Example

```
class Ticket
{
    public int TicketNo { get; set; }
    public string Customer { get; set; }
    public DateOnly CallDate { get; set; }
    public string Description { get; set; }
    public int Priority { get; set; }
    
    public static void Main(string[] args)
    {
        var ticket = new Ticket
        {
            TicketNo = 1,
            Customer = "John Doe",
            CallDate = new DateOnly(2023, 4, 1),
            Description = "Lost password",
            Priority = 1
        };
    }
}
```

## How Code Implements Rules



## Doxygen



## No need for Comments



## Reflection
