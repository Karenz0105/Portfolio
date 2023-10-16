# Testing



## Aim

The aim for this week's task was to code a function(s) within an unfinished game of Hangman with our team, then perform Unit Tests on the function(s).


## UpdateDisplay Function for Hangman Game

The task we were given this week in our practical session was to finish coding an unfinished Hangman game with our team. We were provided a copy of the unfinished game and had to decide between each other who was doing what function.

I chose to do the UpdateDisplay function for the game.

The function I created is below :

```c#
 public string UpdateDisplay(bool isCorrect, string word, char letter, int remainingAttempts)
 {

     StringBuilder updatedDisplay = new StringBuilder(word.Length);

     if (isCorrect)
     {
         for (int i = 0; i < word.Length; i++)
         {
             if (word[i] == letter)
             {
                 string labelName = $"Letter{i + 1}";
                 Label label = (Label)FindByName(labelName);
                 label.Text = letter.ToString();

                 updatedDisplay.Append(letter);
             }
             else
             {
                 updatedDisplay.Append("_");
             }
         }
     }
     else
     {
         for (int i = 0; i < word.Length; i++)
         {
             updatedDisplay.Append("_");
         }

         remainingAttempts--;
     }

     return updatedDisplay.ToString();
 }
```

The general idea for this function is to update the display when the user guesses a letter. The way the code works is by checking if the letter the user has guessed is correct, if it is, then the program will loop around the length of the word to find out where the letter is within the word then update the corresponding label to the letter.

If the user has guessed a letter and it isn't within the word then the display should remain with an underscore and the count for the remaining attempts will go down.



## Unit Test 1

```c#
using Hangman;

namespace UnitTest_UpdatedDisplay_ReturnCorrectDisplay
{
    public class UnitTest1
    {
        [Fact]
        public void Test1()
        {

            // Unit Test to check if the UpdateDisplay() function changes the display based
            // on if a user provides a correct guess

            string gameType = "Easy";

            bool isCorrect = true;
            string word = "pie";
            char letter = 'i';
            int remainingAttempts = 7;


            GamePage gamePage = new GamePage(gameType);

            string expectedOutput = "_i_";

            Assert.Equal(expectedOutput, gamePage.UpdateDisplay(isCorrect, word, letter, remainingAttempts));
        }
    }
}
```



### Unit Test Performed

The above Unit Test that is being performed is to check if the display has been updated correctly from the inputs provided.

With this test we are checking if the letter that has been guessed, 'i', is within the word that has been selected, "pie".
The isCorrect variable is set to true and we have 7 attempts still remaining.
The game type has also been set to easy.

The output that we are expecting to recieve from this guess is "\_i_".

The Assert.Equal() takes in the expected output and compares it to the information provided.

In this case the Unit Test passes.



### Importance of Unit Test

It is important to test this aspect of the code as it is in charge of changing the display the user sees depending on if their guess is correct or not. For this specific Unit Test it is important as we are checking the output if the user has guessed a letter correctly and that it would change the display accordingly.



## Unit Test 2

```c#
using Hangman;

namespace UnitTest_UpdatedDisplay_ReturnCorrectDisplay
{
    public class UnitTest2
    {
        [Fact]
        public void Test2()
        {

            // Unit Test to check if the UpdateDisplay() function changes the display based
            // on if a user provides an incorrect guess

            string gameType = "Easy";

            bool isCorrect = false;
            string word = "pie";
            char letter = 'a';
            int remainingAttempts = 7;


            GamePage gamePage = new GamePage(gameType);

            string expectedOutput = "___";

            Assert.Equal(expectedOutput, gamePage.UpdateDisplay(isCorrect, word, letter, remainingAttempts));
        }
    }
}
```



### Unit Test Performed

The above Unit Test that is being performed is to check if the display has been updated correctly from the inputs provided.

With this test we are checking if the letter that has been guessed, 'a', is within the word that has been selected, "pie".
The isCorrect variable is set to false and we have 7 attempts still remaining.
The game type has also been set to easy.

The output that we are expecting to recieve from this guess is "\___".

The Assert.Equal() takes in the expected output and compares it to the information provided.

In this case the Unit Test passes.



### Importance of Unit Test

It is important to test this aspect of the code as it is in charge of changing the display the user sees depending on if their guess is correct or not. For this specific Unit Test it is important as we are checking the output if the user has not guessed a letter correctly and if the display would be changed accordingly.



## Limitations

// To be completed once Code Battle has finalized.



## Evaluation

// To be completed once Code Battle has finalized.



## Reflection

Working on a random function within an unfinished program was an interesting task to do, it required a lot of checking around the code to better understand how everything was functioning as is. It was also very interesting as many parts of the code were unfinished or not yet implemented which meant trying to figure out how the function I was working on would work with code that would be added later was interesting to do.

After completeing my function I was working on, I then tried to do Unit Tests using xUnit. It was a little difficult at first and sometimes frustrating to do, but after a while of playing around with it and reading over the troubleshooting.md the lecturer provided, it became a slightly easier task to do. Still took some time to get it to work, but I was eventually able to get the Unit Tests to pass with the function I made.
