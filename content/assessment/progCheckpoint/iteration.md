---
title: Iteration
weight: 3
---
*from [The Computing Zone](https://thecomputing.zone/Python/15-Challenges/)*

{{< columns >}}
## 13. Lines cheat
A naughty pupil has been given lines to copy as a punishment from their Computing teacher. The have been asked to type out “I must not behave like muppet in class” 20 times. Write a program that asks a pupil to enter a sentence. The same sentence should then be displayed 20 times. 

<--->
```md
What sentence would you like copied?
> I must not behave like a muppet in class.
I must not behave like a muppet in class.
I must not behave like a muppet in class.
I must not behave like a muppet in class.
I must not behave like a muppet in class.
I must not behave like a muppet in class.
I must not behave like a muppet in class.
I must not behave like a muppet in class.
I must not behave like a muppet in class.
I must not behave like a muppet in class.
I must not behave like a muppet in class.
I must not behave like a muppet in class.
I must not behave like a muppet in class.
I must not behave like a muppet in class.
I must not behave like a muppet in class.
I must not behave like a muppet in class.
I must not behave like a muppet in class.
I must not behave like a muppet in class.
I must not behave like a muppet in class.
I must not behave like a muppet in class.
I must not behave like a muppet in class.
```
{{< /columns >}}

{{< columns >}}
## 14. Cricket over
In cricket a bowler bowls 6 balls at a time. This is called an *over*. Each ball bowled may be hit by the batter who may score some *runs*.
Write a program that allows the runs from an over to be entered (for example: 0, 2, 0, 0, 4, 6). The total scored in that over should then be displayed.
<--->
```md
Please enter the runs for each ball:
> 0
> 2
> 0
> 0
> 4
> 6
This over's score was 12.
```
{{< /columns >}}

{{< columns >}}
## 15. Flexible cheater
The naughty pupil forgot to hand their lines in and now has more to do. Adapt program 13 to allow the
pupil to select how many lines the program produces. 
<--->
```md
What sentence would you like copied?
> I must not behave like a muppet in class.
How many times would you like it copied?
> 7
I must not behave like a muppet in class.
I must not behave like a muppet in class.
I must not behave like a muppet in class.
I must not behave like a muppet in class.
I must not behave like a muppet in class.
I must not behave like a muppet in class.
I must not behave like a muppet in class.
```

{{< /columns >}}

{{< columns >}}
## 16. Charity drive
The following year the three friends recruit many more charity raisers. Adapt program 11 to repeatedly ask for the next amount of money raised. If the user types a number, that number is added to the total and the program asks again. If the user just presses Enter, with nothing else, the program stops asking and displays the total raised, including the doubled value if appropriate.
<--->
```md
Enter the total raised by each person:
> 238
> 624
> 546
> 333
> 651
> 174
> 
A total of $2566 was raised.
This will be increased to $4566.
{{< /columns >}}

{{< columns >}}
## 17. Password
The program should give the user an error message if they enter the wrong password. A message “Entry gained!” should be displayed when the password is entered correctly.
<--->
```md
Please enter the password.
> snool
Sorry, Incorrect! Try again.
Please enter the password.
> giraffe
Sorry, Incorrect! Try again.
Please enter the password.
> sesame
Entry gained!
{{< /columns >}}

{{< columns >}}
## 18. No more presents
You have money to spend on your birthday. Write a program that will ask you what you have to spend, and then to enter the price of each present you want until your total reaches or is over the amount you started with. The program should produce the output shown.
<--->
```md
How much money did you get?
> 200
You have $200.
Price of next item:
> 35
You have $165.
Price of next item:
> 100
You have $65.
Price of next item:
> 50
You have $15.
Price of next item:
> 45
You have overspent!
You can't afford the $45 item.
```
---
```md
How much money did you get?
> 48
You have $48.
Price of next item:
> 48
You have spent all $48!
```
{{< /columns >}}

{{< columns >}}
## 19. Guess the number
A game is created where a user is required to guess an unknown number between 1 and 100 (inclusive). Each time the user guesses the program informs them if their guess is too high, too low or correct. The guessing game only finishes when the user’s guess matches the unknown number.
<--->
```md
I'm thinking of a number between 1 and 100.
Which number do you think it is?
45
Your guess is too low. Try again.
86
Your guess is too high. Try again.
67
Your guess is too high. Try again.
50
Your guess is too low. Try again.
54
Your guess is too high. Try again.
52
Correct! I was thinking of 52.
```
{{< /columns >}}

{{< columns >}}
## 20. Dance group (extension)
You have been asked to write a program to store the names and ages of competitors in a dance competition. The program should display the name of the competitor and which level of competition they should be entered in. ‘Junior’ competitors are less than 12 years old, ‘Senior’ competitors are at least 18 years old. ‘Intermediate’ competitors are aged 12-17.
<--->
```md
Please enter a name:
> Jean Gray
Please enter Jean Gray's age:
> 13
Please enter a name:
> Robert Drake
Please enter Robert Drake's age:
> 24
Please enter a name:
> Scott Summers
Please enter Scott Summers's age:
> 15
Please enter a name:
> Anna LeBeau
Please enter Anna LeBeau's age:
> 9
Please enter a name:
> 
Names and competition list:
Jean Gray - Intermediate
Robert Drake - Senior
Scott Summers - Intermediate
Anna LeBeau - Junior
{{< /columns >}}
