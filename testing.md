# Testing



## Aim

The aim for this week was to fix and create code for a game of Hangman with our group. Then do Unit test on the code we created.


## Test Code #1

```
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


```
using Hangman;

namespace UnitTest_UpdatedDisplay_ReturnCorrectDisplay
{
    public class UnitTest1
    {
        [Fact]
        public void Test1()
        {
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

```
using Hangman;

namespace UnitTest_UpdatedDisplay_ReturnCorrectDisplay
{
    public class UnitTest1
    {
        [Fact]
        public void Test1()
        {
            string gameType = "Easy";

            bool isCorrect = true;
            string word = "pie";
            char letter = 'a';
            int remainingAttempts = 7;


            GamePage gamePage = new GamePage(gameType);

            string expectedOutput = "_i_";

            Assert.Equal(expectedOutput, gamePage.UpdateDisplay(isCorrect, word, letter, remainingAttempts));
        }
    }
}
```

### Purpose of Code



### Test(s) Performed



### Important to Test



### Limitations



### Evaluation



## Test Code #2

```
test code here
```



### Purpose of Code



### Test(s) Performed



### Important to Test



### Limitations



### Evaluation



## Reflection
