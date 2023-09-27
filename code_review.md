# Code Review

## Aim

The aim for this week is to identify problems within a piece of code and suggest how we can improve the given code.

## Code Review Challenge

For this task we were given a Code Review Challenge, which had multiple pieces of code that had problems within it.

The codes could have one problem or multiple problems.

The problems the codes could have were :

* Genereal Principles
* Best Practice
* Code Smells

We were then to select a piece of code from the multiple we were given to best demonstrate our understanding of doing a Code Review.

## Code from challenge

```
class Ticket
{
    public int TicketNo;
    public string Customer;
    public DateTime CallDate;
    public string Description;
    public int Priority;
    
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

## Problems

The code I have selected to write about is above.

There were three areas we were to look at when reviewing the code.

### Does the code above violate any General Principles?

This code does not violate any General Principles.

### Does this code violate any Best Practice Rules?

This code does not violate any Best Practice Rules.

### Does this code exhibit any Code Smells?

This code has one Code Smell.

The Code Smell that this code has is the 'Primitive Obsession' smell.

This Code Smell has one or more of the following issues:

* Replacing Primitive with Object
* Replacing Type Code with Subclasses
* Replacing Conditional with Polymorphism
* Extracting Class
* Introducing Parameter Object

## Primitive Obsession Problem

The code has this problem within the first section of the code, where the data types are being set up.
This is because it is setting up primitive data types to represent different parts of the ticket, making it possible that the code could become confusing and hard to maintain.

Another problem within the code is the CallDate parts. It is being assigned DateTime within the start of the code then being assigned DateOnly values which could cause issues, as these are two different data types.

## Improved Version

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

## Solution

To fix these problems within the code we should first fix the beginning section of the code, where the data types are being set to properties. For this part of the code we would want this data to be retrieved using { get; set; }. We would do this by adding { get; set; } to each of the five properties.

To fix the other issue with the CallDate would depend on if you need the time for the ticket. If there is only a need for the day, month and year the DateOnly data type would be fine to use as it only stores those pieces of information. But if the time was also required then using the data type DateTime would be better as it also records the time. But with the given code it looks as if only the day, month and year are being assigned so using the DateOnly data type will be fine.

These solutions are beneficial to the code because it allows the code to have controlled access to the properties, which in turn helps to keep the code tidy and maintainable. It also helps to not mix different data types together, which could cause issues down the line within the program. Changing the CallDate data type to DateOnly helps to only assign the day, month and year values which help to keep the code simple. But if the time was needed for the tickets, that data type could easily be switched to DateTime, allowing the use of time along with the day, month and year.

## Reflection

Reviewing pieces of code and selecting which problems were wrong with the code was a little challenging.

I found it to be a little challenging as I haven't ever done this type of code review before, it introduced more types of things I had to look out for within code and try to spot.

I did get some wrong as it was my first time trying to find these types of problems within code, but it was a good experience to do and I believe I will improve at spotting out these types of problems within code as I go on with my studies and for the future.
