### [Source of this study material : One Week Python by Colt Steele](https://www.udemy.com/course/one-week-python/)


## Functions

- Functions are reusable actions that have a name.


- Before we can use a function, we must define it and give it a name.


- Once Python knows about our function, we can call it anytime.



## Why do we use functions?

- We can use functions to prevent code duplication. Keep code DRY.


- Functions help us abstract away code, breaking a complex program down into small pieces.



## Use Functions


```
# Define the function
def laugh():
    print("ha" * 20)


# Call the function
laugh()
```


![laugh-function](/GCP_ML_pictures/Study-logs/Python/Fundamentals/functions/laugh-functions.PNG "laugh function")



```
def divide(a, b):
    return a / b

print("*"*30)
print("Welcome to the divide function!")
ask_a = int(input("Enter the denominator: "))
ask_b = int(input("Enter the numerator "))
print("*"*30)

print(f"The result is {round(divide(ask_a, ask_b),3)}")
```


![denominator-and-numerator](/GCP_ML_pictures/Study-logs/Python/Fundamentals/functions/denominator-and-numerator.PNG "denominator and numerator")



### Return

- 'return' outputs whatever value comes after retrun keyword. **Ends the execution of a function**.


```
num = int(input("Enter a number: "))

def is_even(num):
  if num % 2 == 0:
    return print(f"The number {num} is even.")
  elif num % 2 != 0:
    return print(f"The number {num} is odd.")


is_even(num)
```


![even-number-checker](/GCP_ML_pictures/Study-logs/Python/Fundamentals/functions/even-number-checker.PNG "Even number checker")



```
phrase = input("Enter your post title to slugify: ")

def slugify(phrase):
    return print(phrase.lower().strip().replace(' ','-'))


slugify(phrase)
```


![slugify-game](/GCP_ML_pictures/Study-logs/Python/Fundamentals/functions/slugify-game.PNG "slugify game")



```
word = input("Enter a word you like: ")

def vowel_count(word):
  count = 0
  for char in word:
    if char in "aeiou":
      count += 1
  return print(f"The word has {count} vowels")

vowel_count(word)
```


![vowel-counter](/GCP_ML_pictures/Study-logs/Python/Fundamentals/functions/vowel-counter.PNG "vowel counter")



