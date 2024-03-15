### [Source of this study material : One Week Python by Colt Steele](https://www.udemy.com/course/one-week-python/)


## Conditionals

### if statement


```
if condition:
```

- After the if statement, there should be 4 spaces.


![bartender-game](/GCP_ML_pictures/Study-logs/Python/Fundamentals/conditionals/bartender-game.PNG "bartender game")



- If the statement is true, then the body of the statement will run. If false, it won't run.



### elif statement

- Indentation is important when writing if and elif statements. elif will run if the previous statement is false.


![if-and-elif](/GCP_ML_pictures/Study-logs/Python/Fundamentals/conditionals/if-and-elif.PNG "if and elif")



### else statement

- If none of the above were true, do this. You have only one else statement per conditional.


![ticket-game](/GCP_ML_pictures/Study-logs/Python/Fundamentals/conditionals/ticket-game.PNG "ticket game")



### Exercise Game

- Make a game asking for your first and last names and depending on the length of each, show a statement saying whether the name is shorter or longer than the average American name.


![name-length-game](/GCP_ML_pictures/Study-logs/Python/Fundamentals/conditionals/name-length-game.PNG "name length game")



### Generating random numbers

- random.randint is useful method but to use this, we have to first import it.


![random.randint](/GCP_ML_pictures/Study-logs/Python/Fundamentals/conditionals/random-randint.PNG "random.randint(1,1000)")



### Tweet checker

- Also, create a tweet checker that says to you whether your tweet is too long or not.


![tweet-checker](/GCP_ML_pictures/Study-logs/Python/Fundamentals/conditionals/tweet-checker.PNG "tweet checker")



### Water Boiling checker

- You can use nested conditionals like below:


```
unit = input("What unit are you using?")
temp = float(input("What temperature is the water?"))

if unit == 'f':
  if temp >= 212:
    print("The water is boiling")
  else:
    print("The water is not boiling")
elif unit == 'c':
  if temp >= 100:
    print("The water is boiling")
  else:
    print("The water is not boiling")
else:
  if temp >= 373:
    print("The water is boiling")
  else:
    print("The water is not boiling")
```


![water-boiling-checker](/GCP_ML_pictures/Study-logs/Python/Fundamentals/conditionals/water-boiling-checker.PNG "Water boiling checker")



### BMI Checker

- Create a simple script that calculates your BMI. Also, use a **round function** to round up the value to the decimal place you want:


```
weight = float(input("What is your weight?"))
height = float(input("What is your height?"))

bmi = round(weight / (height / 100), 2)

if bmi < 16.0:
  category = "Severely Underweight"
elif bmi >= 16.0 and bmi < 18.5:
  category = "Underweight"
elif bmi >= 18.5 and bmi < 25.0:
  category = "Normal"
elif bmi >= 25.0 and bmi < 30.0:
  category = "Overweight"
elif bmi >= 30.0 and bmi < 35.0:
  category = "Moderately Obese"
elif bmi >= 35.0 and bmi < 40.0:
  category = "Severely Obese"
else:
  category = "Very Severely Obese"

print(f"Your BMI of {bmi} of {category}")
```


![bmi-checker](/GCP_ML_pictures/Study-logs/Python/Fundamentals/conditionals/bmi-checker.PNG "BMI checker")



### rock - paper - scissors game


```
from random import randint

rock = """
    _______
---'   ____)
      (_____)
      (_____)
      (____)
---.__(___)"""

paper = """
    _______
---'   ____)____
          ______)
          _______)
         _______)
---.__________)
"""

scissors = """
    _______
---'   ____)____
          ______)
       __________)
      (____)
---.__(___)
"""

num = randint(1, 3)

your_move = input("What is your move? (rock, paper, scissors) ")

if your_move == "rock":
  print("*" * 25)
  print("Your move:")
  print("*" * 25)
  print(rock)
  print("*" * 25)
  print("Computer's move:")
  print("*" * 25)
  if num == 1:
    print(rock)
    print("It's a tie!")
  elif num == 2:
    print(paper)
    print("You lose!")
  else:
    print(scissors)
    print("You win!")

elif your_move == "paper":
  print("*" * 25)
  print("Your move:")
  print("*" * 25)
  print(paper)
  print("*" * 25)
  print("Computer's move:")
  print("*" * 25)
  if num == 1:
    print(rock)
    print("You win!")
  elif num == 2:
    print(paper)
    print("It's a tie!")
  else:
    print(scissors)
    print("You lose!")

else:
  print("*" * 25)
  print("Your move:")
  print("*" * 25)
  print(scissors)
  print("*" * 25)
  print("Computer's move:")
  print("*" * 25)

  if num == 1:
    print(rock)
    print("You lose!")
  elif num == 2:
    print(paper)
    print("You win!")
  else:
    print(scissors)
    print("It's a tie!")
```


![rock-paper-scissors](/GCP_ML_pictures/Study-logs/Python/Fundamentals/conditionals/rock-paper-scissors.PNG "rock paper scissors game")