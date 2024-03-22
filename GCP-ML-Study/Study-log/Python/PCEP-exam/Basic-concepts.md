### [Source of this study material : Python PCEP by Adrian Wiech](https://www.udemy.com/course/python-pcep/)


## Basic Concepts

- It's the best practice to use single quotes to surround strings. When you have **apostrophe(')** inside your string, then use escape character(\) right before the apostrophe to print the string as you intended.


```
print('I\'m studying Python')
```


- If you want to insert a new line inside the string, you can add **\n**.


```
print('I\'m studying\nPython')
```


![about-print](/GCP_ML_pictures/Study-logs/Python/PCEP-exam/basic-concepts/about-print.PNG "about print")



- In programming the booleans (True / False) are equivalent to:


```
1 = True

0 = False
```


- There are numerical representations you need to know:


```
# underscores in numbers
12000300
12_000_300

# scientific notation
# 3e4 = 3E4 = 3 * 10000 = 30000
# 3-e4 = 3-E4 = 3 * 1/10000 = 0.0003
print(0.0000000000000000000000000003)
```


![scientific-notation](/GCP_ML_pictures/Study-logs/Python/PCEP-exam/basic-concepts/scientific-notation.PNG "scientific notation")



- Changing between data types (e.g. strings to float) is called type casting.


```
height_cm = float(input('Height converter: enter your height in cm: '))
print('Your height in feet is ', height_cm / 30.48)
```


![type-casting](/GCP_ML_pictures/Study-logs/Python/PCEP-exam/basic-concepts/type-casting.PNG "type casting")



- **Binary operators** (e.g. + and - signs) have 2 operands or 2 values to work with like below:


![binary-operators](/GCP_ML_pictures/Study-logs/Python/PCEP-exam/basic-concepts/binary-operators.PNG "binary operators")


- **Unary operator**, on the other hand, works with a single operand or a single value. We can simply use a + or - sign before a single number to inidicate that the number is above or below zero.


![unary-operator](/GCP_ML_pictures/Study-logs/Python/PCEP-exam/basic-concepts/unary-operator.PNG "unary operator")


- The precision of float numbers in Python is limited. If you add 0.1 + 0.1 + 0.1, the Python does not give you exactly 0.3. It's simply the way most computers work these days. 


![precision-of-floats](/GCP_ML_pictures/Study-logs/Python/PCEP-exam/basic-concepts/precision-of-floats.PNG "precision of floats")


- The exponentiation(**) operator uses right-sided binding (i.e. starts from the right).


![exponentiation-right-sided-first](/GCP_ML_pictures/Study-logs/Python/PCEP-exam/basic-concepts/exponentiation.PNG "exponentiation happens right-sided first")


- Keyword arguments are arguments that you can use at the end of the function after all the other arguments. Keyword arguments are always optional. The end argument in print function specifies what is supposed to be printed at the end of the print function. 


![keyword-argument](/GCP_ML_pictures/Study-logs/Python/PCEP-exam/basic-concepts/keyword-arguments.PNG "keyword arguments")


- You can use the sep='' argument at the end of the function arguments to indicate a specific separator between the arguments.


![sep-argument](/GCP_ML_pictures/Study-logs/Python/PCEP-exam/basic-concepts/sep-argument.PNG "sep argument")



- When we use for loops, we talk about iterating. Scanning or broswing a sequence is often called iterating and entering a loop's body is called iteration. 


![iterating-and-iteration](/GCP_ML_pictures/Study-logs/Python/PCEP-exam/basic-concepts/iterating-and-iteration.PNG "iterating and iteration")


- The 'break' instruction lets users exit a loop and move on to the next instruction outside the loop.


```
while True:
    name = input('Enter your name or EXIT to close the program: ')
    if name == 'EXIT':
        break
    else:
        print('Hello ', name)
```


- The 'continue' is used to escape the current iteration and move on to the next one. 'continue' is typically used with 'if' statements when you want to escape certain iterations.


- If a number % divided by 5 equals 0, it means the number is divisible by 5. In such cases, we use the **continue** statement and thus we don't print the number.


```
for i in range(1, 21):
    if i % 5 == 0:
        continue
    print(i)
```


![continue-instruction](/GCP_ML_pictures/Study-logs/Python/PCEP-exam/basic-concepts/continue-instruction.PNG "continue instruction")



```
for a in range(1,6):
    for b in range(1,6):
        print(f"{a} x {b} = {a * b}")
```


![nested-for-loop](/GCP_ML_pictures/Study-logs/Python/PCEP-exam/basic-concepts/nested-for.PNG "nested for loop")



- In the list, 'append' method appends an element at the end of the list. On the other hand, 'insert' method inserts an element at a certain index of the list.


```
list = [1, 3, 5, 7, 9]

list.append(10)

list.insert(5, 10)
```


![play-with-list](/GCP_ML_pictures/Study-logs/Python/PCEP-exam/basic-concepts/play-with-list.PNG "play with list")



- To swap the values inside the list:


```
even = [0, 2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26]
even[0], even[len(even)-1] = even[len(even)-1], even[0]
print(even)
```


![swap-the-values](/GCP_ML_pictures/Study-logs/Python/PCEP-exam/basic-concepts/swap-the-values.PNG "swap the values")


- To sort numbers in order in the list, run the following:


```
numbers = [-5, 8, 6, 4, 99, -2, -77, 1,5, 3]
numbers.sort()
print(numbers)

numbers.sort(reverse = True)
print(numbers)
```


![sort-list](/GCP_ML_pictures/Study-logs/Python/PCEP-exam/basic-concepts/sort-list.PNG "sort list")


- The difference between 'sort' and 'sorted': 

  - **list.sort()**: sorts the original list

  - **sorted(list)**: gives back a new, sorted list, keeps the original unchanged


![sort-and-sorted](/GCP_ML_pictures/Study-logs/Python/PCEP-exam/basic-concepts/sort-and-sorted.PNG "sort and sorted")


- list.sort() is a method that changes the list. sorted(list) is a general purpose function that returns the sorted list but doesn't change the list.


- To iterate an element in nested lists, do the following:


```
nested = [['A1', 'A2','A3'], ['B1', 'B2', 'B3']]
for i in nested:
    for ii in i:
        print(ii)
```


![nested-list](/GCP_ML_pictures/Study-logs/Python/PCEP-exam/basic-concepts/nested-list.PNG "nested list")


- Lists are mutable data type and tuples are immutable data types. There's no way to **add or delete an element** to and from a tuple. Strings are immutable, too.


- Lists are generally used to group the same data types like floats or strings. On the other hand, tuples are typically used to group different data types that are related together to form a structure.



- To update the dictionary, you can do the following:


```
grades = {}

grades['Angela'] = 'A-'
grades['Anne'] = 'B+'

print(grades)
```


![update-dictionary](/GCP_ML_pictures/Study-logs/Python/PCEP-exam/basic-concepts/update-dictionary.PNG "update dictionary")



- To iterate each item in the dictionary:


```
grades = {'Angela': 'A-', 'Anne': 'B+'}

for student, grade in grades.items():
    print(f"{student} got {grade}")
```


![iterating-on-dict](/GCP_ML_pictures/Study-logs/Python/PCEP-exam/basic-concepts/iterating-on-dict.PNG "iterating on dict")



- Recursion takes place when a function calls itself. 


- A factorial is the multiplication of all integeres **from 1 after the number**. It is expressed as:


```
# factorial
# 3! = 1 * 2 * 3
# 5% = 1 * 2 * 3* 4 * 5 
```


- We will write 2 versions of factorial functions: 1. iterative, 2. recursive.


```
# iterative

def get_factorial(num):
  factorial = 1
  for i in range(1, num+1):
    factorial *= i
  return factorial


print(get_factorial(10))

```


```
def get_factorial(num):
    if num <= 1:
        return 1
    return num * get_factorial(num - 1)


print(get_factorial(5))
```


![factorial-function-recursive](/GCP_ML_pictures/Study-logs/Python/PCEP-exam/basic-concepts/factorial-function-recursive.PNG "factorial function recursive")



- An exception is an event which occurs during the execution of a program that disrupts the normal flow of the program instructions. You can handle the exceptions so that program executes normally by using:


```
try:
  value = int(input("Enter a number: "))
  print('The exponenial value of', value, 'is', value**2)

except:
  print('Invalid value.')
```


![exceptions](/GCP_ML_pictures/Study-logs/Python/PCEP-exam/basic-concepts/exceptions.PNG "exceptions")



- In case a user provided 0 for a divison, it causes ZeroDivisionError. You can handle it by using:


```
try:
  value = int(input("Enter a number: "))
  print('The exponenial value of', value, 'is', 1/value)

except ValueError:
  print('You did not provide a number.')
except ZeroDivisionError:
  print('You cannot divide by zero.')
```


![zero-deivision-error](/GCP_ML_pictures/Study-logs/Python/PCEP-exam/basic-concepts/zerodivisionerror.PNG "zero division error")













