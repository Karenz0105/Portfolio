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

Another rule within Clean Code is Formatting, this rule is to help keep the code in a readable format. We achieve this by using proper indentation thoughout the code, using consistent spacing and keeping functions, classes and variables to consistent and clear names. The end goal with following the Formatting rule for Clean Code is to have code that is organised and readable to make it easier to maintain within the future or continuation of the project.

```
public class Program
{
static void Main()
{
Console.WriteLine("Hello World!");
}
}
```

Above is an example of how a piece of code could look if you don't format it correctly. It is still readable but it looks horrible and could become confusing if it was a larger piece of code with multiple if/else statements in it.

```
public class Program
{
    static void Main()
    {
        Console.WriteLine("Hello World!");
    }
}
```

Above is the same as the previous example, but now with the formatting fixed! It now looks a lot better as it is easier to read and won't get confusing if more code is added that follows the correct formatting.


### Functions

Within the Clean Code rules there is one about Functions. This one has a lot of information about how the code should be structured. Functions should be kept small and get right to the point, they should have only up to 20 lines, the smaller the function the better! This can be done by using blocks and indenting propertly, for example when using if, else or while statements to not have many lines. Within those lines have a function call, which would call to the needed function and it would help to keep the code very organised. Functions should also use descriptive names, it helps with keeping the code easy to read, helps to describe what the function does and also helps to eliminate the need for unnecessary comments! Functions should not cause any side effects or errors to the code! Make sure that they work correctly and don't cause anything that breaks your code or makes you have to write something new to work around it!

```
public class Employee
{
    public void DetermineEmployeePayCategory(decimal employeeSalary)
    {
        if (employeeSalary > 25000)
        {
            EmployeePayForOver25000();
        }
        else
        {
            EmployeePayGeneral();
        }
    }

    private void EmployeePayForOver25000()
    {
        // No code as just example
    }

    private void EmployeesPayGeneral()
    {
        // No code as just example
    }
}
```

In the above example, it gives an idea of how to use functions properly and how much easier it can be to read the code and understand what it is doing.



### KISS

KISS is a Software Engineering Principle that extends to Clean Code Principles. KISS stands for "Keep It Simple, Stupid". The general idea of this is to help with Clean Code to eliminate any complexity that isn't needed within the code. This is so if you were to come back to the program at a later date, you could still understand what the code is doing without questioning it.



### YAGNI

YAGNI is another Software Engineering Principle that extends to Clean Code Principles. YAGNI stands for "You Ain't Gonna Need It". The idea behind this rule is to not assume you will need certain pieces of code later and end up coding them earlier, because in most cases you might not need it or never end up using it, which will just end up making the program clunky with unnecessary code. 


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

The above code is code I have refined from a previous week within this module.

This code follows the six Clean Code rules that I previously wrote about

* The code includes Meaningful Names for any entry that needs them, such as the variables, class and functions. All the given names for each item are very easy to understand and follow, allowing us to know what each is for and what is does/gains.
* The code doesn't include any Comments as it is unnecessary for the small piece of code, but also because everything within the code is easy to understand just by reading each line!
* The code follows a good Format as there is proper indentation, use of white space and follows a consistant flow which makes it easy for us to read.
* The code uses Functions correctly as it has kept the function small and only includes what is needed for it, it doesn't overcomplicate what it is getting and doesn't have anything extra that isn't needed.
* The code follows the KISS rule as the above code is simple and doesn't include any complex elements within it making it easy for us to come back to work on it at any time.
* The code follows the YAGNI rule as it doesn't include any unused code or extra code that would take up space.

Even though it is a small piece of code it is able to follow all the previously explained rules, as the code grew it would be easy to keep to these rules and maintain them.



## Doxygen




## Reflection





## References

Clean Code ([Martin, 2009](https://napier.primo.exlibrisgroup.com/permalink/44NAP_INST/13v8mut/alma9923581530002111))
