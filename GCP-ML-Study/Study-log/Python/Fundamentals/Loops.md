### [Source of this study material : One Week Python by Colt Steele](https://www.udemy.com/course/one-week-python/)


## Loops

### While loops


```
answer = input("Please say hi  ")

while answer != 'hi':
  answer = input("Rude. Please say hi.")

print("Hi to you, too!")
```


![loop-basics](/GCP_ML_pictures/Study-logs/Python/Fundamentals/loops/loop-basics.PNG "loop basics")


```
num = 0

while num < 10:
  print(f"The number is {num}")
  num += 1

print("The loop is done")
```


![num-loop](/GCP_ML_pictures/Study-logs/Python/Fundamentals/loops/num-loop.PNG "num loop")



```
count = 10

while count > 0:
  print("*" * count)
  count -= 1

count = 1

while count <= 10:
  print("*" * count)
  count += 1
```


![count-loop](/GCP_ML_pictures/Study-logs/Python/Fundamentals/loops/count-loop.PNG "count loop")



```
from random import randint

num = randint(1,6)
num_2 = randint(1,6)
count = 1

while num != 1 or num_2 != 1:
  print(f"Your numbers are {num} and {num_2}")
  num = randint(1,6)
  num_2 = randint(1,6)
  count += 1

print(f"Your numbers are {num} and {num_2}. You have tried {count} times to get the snake eyes.")
```


![snake-eyes](/GCP_ML_pictures/Study-logs/Python/Fundamentals/loops/snake-eyes.PNG "Snake eyes")



### for loops


```
for letter in "Yejin willl pass PCEP":
  print(letter)
```


![for-basics](/GCP_ML_pictures/Study-logs/Python/Fundamentals/loops/for-basics.PNG "for basics")



- You can also use the built in **range** function:


```
for number in range(1,20):
  print(number)
```


![for-range](/GCP_ML_pictures/Study-logs/Python/Fundamentals/loops/for-range.PNG "for range")



- Now, we will create a range from 0 to 100 (not including 100) and count by 5.


```
for number in range(1,100,5):
  print(number)
```


![for-range-count-by-5](/GCP_ML_pictures/Study-logs/Python/Fundamentals/loops/for-range-count-by-5.PNG "for range count by 5")



```
for num in range(99,1,-1):
  print(f"There are {num} bottle(s) of beer on the wall.")
  print(f"Take one down, pass it around, {num-1} bottle(s) of beer on the wall.")
  print("*" * 50)

print("There are 1 bottles of beer on the wall.")
print("Take one down, pass it around, no more bottles of beer on the wall.")
```


![beer-bottle-game](/GCP_ML_pictures/Study-logs/Python/Fundamentals/loops/beer-bottle-game.PNG "Beer bottle game")



### Nested loops


- Nested loop is supposed to run all the way up to its range for each iteration of the outer loop.


```
for outer in range(1,6):
  print(outer)
  for inner in range(1,6):
    print("\t",inner)
```


![nested-loop](/GCP_ML_pictures/Study-logs/Python/Fundamentals/loops/nested-loop.PNG "nested loop")




```
import random

dice_num = int(input("How many diece are we rolling?"))
side_num = int(input("How many sides are on the die?"))

while True:
  result = "|"
  for die in range(dice_num):
    rand = random.randint(1,side_num+1)
    result += f" {rand} |"
    print(result)
  question = input("Roll again? (q to quit)")
  if question == "q":
    break
```


![nested-loop2](/GCP_ML_pictures/Study-logs/Python/Fundamentals/loops/nested-loop2.PNG "nested loop 2")



```
player_1 = input("Enter player1's name: ")
player_2 = input("Enter player2's name: ")

num_left = 30

while num_left > 0:
  print("|" * num_left)
  print(f"There are {num_left} tooth picks left.")
  p1_choice = int(input(f"{player_1}, how many tooth picks do you pick? "))
  if p1_choice > 3:
    print("Please enter a number between 1 and 3: ")
  else:  
    num_left -= p1_choice
    if num_left <= 0:
      print(f"{player_1} won the game!")
      break

  print("|" * num_left)
  print(f"There are {num_left} tooth picks left.")
  p2_choice = int(input(f"{player_2}, how many tooth picks do you pick? "))
  if p2_choice > 3:
    print("Please enter a number between 1 and 3: ")
  else:
    num_left -= p2_choice
    if num_left <= 0:
      print(f"{player_2} won the game!")
      break
```


![tooth-pick-game](/GCP_ML_pictures/Study-logs/Python/Fundamentals/loops/tooth-pick-game.PNG "tooth pick game")
