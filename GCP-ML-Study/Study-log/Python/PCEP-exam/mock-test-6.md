### [Source of this study material : Python Certification Exam PCEP by Cord Mählmann](https://www.udemy.com/course/pcep-certification-python-exam-practice-tests/)


## Exam -6

### 1. Data Aggregates

- CASE: What is the expected output of the following code?

```
list = ['Peter', 'Paul', 'Mary']
 
 
def list(data):
    del data[1]
    data[1] = 'Jane'
    return data
 
 
print(list(list))
```

- Solution: The code is erroneous.


- Try it yourself:

```
list = ['Peter', 'Paul', 'Mary']
 

# def func(data):
def list(data):
    del data[1]
    data[1] = 'Jane'
    return data
 
 
# print(func(list))  # ['Peter', 'Jane']
print(list(list))    # TypeError: ...
```

Explanation:

The list and the function can not have the same name.

The function gets passed the itself and then naturally the del does not work.



### 2. Basics

- CASE: What is true about compilation?


- Solution:

- It tends to be faster than interpretation.

- The code is converted directly into machine code executable by the processor.


- Compilation means, that the source program is translated once

(however, this act must be repeated each time you modify the source code)

by getting a file containing the machine code.

The execution of the compiled code is usually faster.


### 3. Basics

- CASE: Insert the correct piece of code

so that the program produces the expected output.

Expected output:

```
Andy
Brown
```

- Solution: print("Andy\nBrown")

- Try it yourself:

```
print("Andy\nBrown")
# Andy
# Brown
```

The \n digraph makes the print() function to break to a new line.

The n stands for new line.


### 4. Functions

- CASE: The meaning of the positional parameter is determined by its:

- Solution: position

- Try it yourself:

```
def my_function(a, b, c):
    print(a, b, c)
 
 
my_function(7, 23, 42)  # 7 23 42
```

Explanation:

That's why it's called positional parameter.


### 5. Data Types

- CASE: The ABC company is building a basketball court

for its employees to improve company morale.

You are creating a Python program that employees

can use to keep track of their average score.

The program must allow users to enter their name and current scores.

The program will output the user name and the user's average score.

The output must meet the following requirements:



The user name must be left-aligned

If the user name has fewer than 20 characters,

additional space must be added to the right

The average score must have three places to the left of the decimal point

and one place to the right of the decimal (xxx.x)


- Solution: 

```
%-20s
%4.1f
```

- This question is about string formatting by % in the so called printf-style.

%-20s

The minus sign is for the left-alignment.

The 20 stands for 20 characters.

The s stands for string

%4.1f

The 4 stands for a minimum of 4 characters.

The .1 stands for 1 decimal place.

The f stands for float format.


### 6. Control Flow

- CASE: How many stars will the following code print to the monitor?

```
data = [[x for x in range(3)] for y in range(3)]
for i in range(3):
    for j in range(3):
        if data[i][j] % 2 != 0:
            print('*')
```

- Solution: 3

- Try it yourself:

```
data = [[x for x in range(3)] for y in range(3)]
print(data) # [[0, 1, 2], [0, 1, 2], [0, 1, 2]]
for i in range(3):
    for j in range(3):
        if data[i][j] % 2 != 0:
            print('*')  # * * *
```

The list comprehension produces a two-dimensional list

The three elements of the outer list also each have three elements:

the numbers 0, 1, 2

x % 2 != 0 tests, if x is odd.

The two for loops make it happen, that every of the nine elements is tested.

There is three times the number 1

Those are the odd ones.

Therefore three stars get printed.


### 7. Data Aggregates

- CASE: Which one of the lines should you put in the snippet below

to match the expected output?

Expected output:

[1, 2, 4, 7]


Code:

list = [2, 7, 1, 4]
 
print(list)


- Solution: list.sort()

Try it yourself:

```
list = [2, 7, 1, 4]
list.sort()
print(list) # [1, 2, 4, 7]
```

Explanation:

list.sort()

The sort() method sorts the list ascending by default.


### 8. Operators

- CASE: Which of the following is the correct order of operator precedence?


- Solution:

Parentheses
Exponents
Unary positive, negative, not
Multiplication and Division
Addition and Subtraction
And


### 9. Data Aggregates

- CASE: What snippet would you insert in the line indicated below to print

The highest number is 10 and the lowest number is 1. to the monitor?

```
data = [10, 2, 1, 7, 5, 6, 4, 3, 9, 8]
# insert your code here
print(
    ('The highest number is {} ' +
     'and the lowest number is {}.').format(high, low)
)
```

- Solution: 

```
def find_high_low(nums):
    nums.sort()
    return nums[-1], nums[0]

high, low = find_high_low(data)
```


- Try it yourself:

data = [10, 2, 1, 7, 5, 6, 4, 3, 9, 8]
 
``` 
def find_high_low(nums):
    nums.sort()
    print(nums)                        
    # [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
    return nums[-1], nums[0]
    # return nums[len(nums)], nums[0]
    # IndexError: list index out of range
    # return nums[0], nums[-1]
    # high and low are interchanged
 
 
high, low = find_high_low(data)
 
print(
    ('The highest number is {} ' +
     'and the lowest number is {}.').format(high, low)
)
# The highest number is 10 and the lowest number is 1.
```


Explanation:

The built-in function sort() will sort the list of integers in-place.

Then index -1 will take the last and the index 0 the first element,

which are the highest and the lowest.


### 10. Data Aggregates

- CASE: What is the expected output of the following code?

```
data = ['abc', 'def', 'abcde', 'efg']
print(max(data))
```

- Solution: efg

- Try it yourself:

```
data = ['abc', 'def', 'abcde', 'efg']
print(max(data))  # efg
 
print(ord('a'))   # 97
print(ord('d'))   # 100
print(ord('e'))   # 101
```

Explanation:

Python's built-in function max() is given a list with strings.

max() will look for the string, which first character has the highest Unicode character number,

which in this case is efg

because e has the highest Unicode character number.


### 11. Control Flow

- CASE: Which one of the lines should you put in the snippet below to match the expected output?



Expected output:

1245


```
c = 0
while c < 5:
    c = c + 1
    if c == 3:
        # enter code here
    print(c, end="")
```

- Solution: contine


- Try it yourself:

```
c = 0
while c < 5:
    c = c + 1
    if c == 3:
        continue
    print(c, end="")  # 1245
```


You want to print every number except the number 3

Therefore when c is equal to 3 you want to end

that iteration of the loop directly before the number is printed.

That is what the continue keyword is for.


### 12. Control Flow

- CASE: Consider the following code.

```
for i in range(5, 0, ???):
    print(i, i, i, i, i)
```

What would you insert instead of ??? so that the program

prints the following pattern to the monitor?

```
5 5 5 5 5
4 4 4 4 4
3 3 3 3 3
2 2 2 2 2
1 1 1 1 1
```

- Solution: -1

- Try it yourself:

```
for i in range(5, 0, -1):
    print(i, i, i, i, i)
 
print('-----')
 
# for i in range(5, 0, None):  # TypeError: ...
#     print(i, i, i, i, i)
 
print('-----')
 
# for i in range(5, 0, 0):     # ValueError: ...
#     print(i, i, i, i, i)
 
print('-----')
 
for i in range(5, 0, 1):
    print(i, i, i, i, i)
 
print(list(range(5, 0, 1)))  # []
```

Explanation:

The third argument of the range() function can neither be None nor 0

And if the third argument if a positive number,

the start argument (here 5) has to be lower than the end argument (here 0).

Otherwise range() will return an empty list


### 13. Data Aggregates

- CASE: What is the expected output of the following code?

```
data = {}
data['2'] = [1, 2]
data['1'] = [3, 4]
 
for i in data.keys():
    print(data[i][1], end=' ')
```

- Solution: 2 4

- Try it yourself:

```
data = {}
data['2'] = [1, 2]
data['1'] = [3, 4]
 
for i in data.keys():
    print(data[i][1], end=' ')  # 2 4
 
print()
print(data)  # {'2': [1, 2], '1': [3, 4]}
```

Explanation:

The dictionary does not automatically get sorted.

The index 2 was put in first.

The index 2 will be read first.

The keys() method reads out the keys.

In the first iteration off the for loop i is going to be 2

and in the second iteration i is going to be 1


### 14. Data Aggregates

- CASE: Which function does in-place reversal of objects in a list?

- Solution: list.reverse()

- Try it yourself:

```
my_list = [1, 2, 3]
my_list.reverse()
print(my_list)  # [3, 2, 1]
```

Explanation:

list.reverse()

The reverse() method reverses the elements of the list in place.


### 15. Data Aggregates

- CASE: What is the expected output of the following code?

```
data = (1, 2, 3, 4)
data = data[-2:-1]
data = data[-1]
print(data)
```

- Solution: 3

Try it yourself:

```
data = (1, 2, 3, 4)
data = data[-2:-1]
print(data)  # (3,)
data = data[-1]
print(data)  # 3
```

Explanation:

Slicing with negative indexes.

A start of -2 takes the second last element.

That would be the value 3

The index -1 is the last element.

The end is always exclusive.

That leaves (3,)

The index -1 is again the last element of that,

which is the value 3


### 16. Functions

- CASE: Which of the following statements are true?

- Solution:

- The return keyword may cause the function to return a value.

- The return keyword forces the function's execution to terminate.


Try it yourself/Explanation:

```
# The return keyword forces the function's execution to terminate:
def my_function():
    print("Hello")
    return
    print("World")
 
 
my_function()  # Hello
 
 
# The return keyword may cause the function to return a value:
def my_function():
    return "Hello"
 
 
print(my_function())  # Hello
```

### 17. Functions

- CASE: What is the expected output of the following code?

```
def func(n):
    s = '*'
    for i in range(n):
        s += s
    yield s
 
 
for x in func(2):
    print(x, end='')
```

- Solution: ****


- Try it yourself:

```
def func(n):
    s = '*'
    for i in range(n):
        s += s
    yield s
    # return s
 
 
for x in func(2):
    print(x, end='')  # ****
 
print()
print(func(2))        # <generator object func at ...>
print(list(func(2)))  # ['****']
 
s = '*'
s += s    # s = s + s -> s = '*' + '*' -> '**'
s += s    # s = s + s -> s = '**' + '**' -> '****'
print(s)  # ****
```

Explanation:

The generator function will produce a generator object with one element: '****'

The for loop will iterate through that string and print every single character.

The snippet would have the same output if yield gets interchanged with return

If you only have one yield keyword, it belongs in a loop.


### 18. Data Aggregates

- CASE: What is the expected output of the following code?

```
data = {1: 0, 2: 1, 3: 2, 0: 1}
x = 0
 
for _ in range(len(data)):
    x = data[x]
 
print(x) 
```

- Solution: 0

- Try it yourself:

```
data = {1: 0, 2: 1, 3: 2, 0: 1}
x = 0
 
for _ in range(len(data)):
    print(x)  # 0 - 1 - 0 - 1
    x = data[x]
 
print(x)      # 0
```

Explanation:

The dictionary has four elements

and therefore the for loop has four iterations.

The value of x gets changed four times: 0 -> 1 -> 0 -> 1 -> 0

And in the end the value again is 0


### 19. Basics

- CASE: You execute the following command in the terminal.

python index.py Hello

You want the command to print out Hello

What has to be inside of index.py?


- Solution:

```
from sys import argv
print(argv[1])
```

- You need to know two things here.

First the name of the variable is argv (argument vector).

And second the index 0 always holds the filename.

Index 1 holds the first argument from the command line.

To test it you have to open the folder

where you created the index.py file in a terminal

and run the file by executing python index.py Hello


### 20.  Operators

- CASE: Consider the following code.

```
languages = ['English', 'Spanish', 'German']
more_languages = ['English', 'Spanish', 'German']
extra_languages = more_languages
```

Which statement will print True to the monitor?

Choose two.


- Solution:

- print(more_languages is extra_languages)

- print(languages == more_languages)


- All the lists will have the same values.

more_languages is assigned to extra_languages

A list is a mutable data type.

Assigning a list creates a reference.

Therefore more_languages and extra_languages will have the same identity.


### 21.   Data Aggregates

- CASE: What is the output of the following snippet?

```
my_list = ['Mary', 'had', 'a', 'little', 'lamb']
 
 
def my_list(my_list):
    del my_list[3]
    my_list[3] = 'ram'
 
 
print(my_list(my_list))
```

- Solution: no output, the snippet is erroneous.

- Try it yourself:

```
my_list = ['Mary', 'had', 'a', 'little', 'lamb']
 
 
def my_list(my_list):
    del my_list[3]
    # TypeError: 'function' object
    # does not support item deletion
    my_list[3] = 'ram'
    # TypeError: 'function' object
    # does not support item assignment
 
 
print(my_list(my_list))
```

Explanation:

The list and the function have the same name.

Inside of the function the function tries to delete its index 3

That is not possible.

A function does not have an index.



### 22. Data Types

- CASE: The following code:

```
print(float("1, 3"))
```

- Solution: raises a ValueError exception.


- Try it yourself:

```
# print(float("1, 3"))  # ValueError ...
# print(float("1. 3"))  # ValueError ...
# print(float("1,3"))   # ValueError ...
print(float("1.3"))     # 1.3
```

Explanation:

There are two problems.

There is a comma instead of a point and there is a space.


### 23. Functions

- CASE: A variable defined outside a function:


- Solution: may be read, but not written (something more is needed to do so)

- Try it yourself:

```
# Reading a variable inside of a function:
value1 = 23
 
 
def my_function1():
    print(value1)
 
 
my_function1()  # 23
 
# Trying to write a variable inside of a function:
value2 = 42
 
 
def my_function2():
    value2 = 67
 
 
my_function2()
print(value2)  # 42
 
# global, the something more that is needed:
value3 = 74
 
 
def my_function3():
    global value3
    value3 = 99
 
 
my_function3()
print(value3)  # 99
```

- In Python variables are shadowing into functions.

You can read them, but not write to them.

If you use the global keyword, you can also write to them.


### 24. Basics

- CASE: The compiled Python bytecode is stored in files having names ending with:

- Solution. pyc

Try it yourself:

```
# First execute the following to create the needed file:
functions = '''
def func():
    print('Hello world')
'''
with open('functions.py', 'w') as f:
    f.write(functions)
 
index = '''
import functions
functions.func()
'''
with open('index.py', 'w') as f:
    f.write(index)
```

- First please check, if the files index.py

and functions.py are created as expected.

Now run the file index.py and the folder __pycache__ should be created.

In case your Editor/IDE does not show the folder, check in your file system.

Inside the folder should be a file like functions.cpython-39.pyc

This file contains compiled Python bytecode.

Next time you run index.py Python will use

the compiled bytecode for faster execution.


### 25.  Data Aggregates

- CASE: What is the output of the following snippet?

```
my_list_1 = [1, 2, 3]
my_list_2 = []
for v in my_list_1:
    my_list_2.insert(0, v)
print(my_list_2)
```

- Solution: [3, 2, 1]


- Every element of my_list_1 will be inserted at the beginning of my_list_2

In the end my_list_2 will be a reversed version of my_list_1


### 26. Control Flow

- CASE: You work for a company that distributes media for all ages.

You are writing a function that assigns a rating based on a user's age.

The function must meet the following requirements:

Anyone 18 years old or older receives a rating of A

Anyone 13 or older, but younger than 18 receives a rating of T

Anyone 12 years old or younger receives a rating of C

If the age is unknown, the rating is set to C

```
def get_rating(age):
    rating = ''
    if             # Line-3
    elif           # Line-4
    elif           # Line-5
    else           # Line-6
    return rating
```

Which of the following should you insert on Line-3 to Line-6?


```
    if age == None: rating = 'C'
    elif age < 13: rating = 'C'
    elif age < 18: rating = 'T'
    else: rating = 'A'
```


- Try it yourself:

```
def get_rating(age):
    rating = ''
    if age == None: rating = 'C'
    elif age < 13: rating = 'C'
    elif age < 18: rating = 'T'
    else: rating = 'A'
    return rating
 
 
print(get_rating(19))    # A
print(get_rating(18))    # A
print(get_rating(17))    # T
print(get_rating(13))    # T
print(get_rating(12))    # C
print(get_rating(11))    # C
print(get_rating(None))  # C
```


- The None condition needs to be first,

because None does not support the less than operator

And if you start with rating C you can best continue with it.

That would be: age < 13

The next bigger rating is T: age < 18

Then anyone who is at least 18 remains.

They all get the rating A in the else clause.


### 27. Control Flow

- CASE: Which of the following code snippets will print all prime numbers

between 2 and 100 to the monitor?


- Solution:

```
num = 2
while num <= 100:
    is_prime = True
    for i in range(2, num):
        if num % i == 0:
            is_prime = False
            break
    if is_prime == True:
        print(num)  # 2 -> 3 -> 5 -> ... -> 89 -> 97
    num += 1
```


### 28. Operators

- CASE: What is the output of the following snippet?


```
y = 2 + 3 * 5.
print(y)
```

- Solution: 17.0

- 5. is the the same as 5.0

and multiplication precedes addition.


### 29. Control Flow

- CASE: Consider the following code.

```
x = 42
y = 7
data = "I'm gonna make him an offer he can't refuse."
```

Which of the following expressions will evaluate to 19?


- Solution: data.find('an') if data else None

- Try it yourself:

```
x = 42
y = 7
data = "I'm gonna make him an offer he can't refuse."
 
print(data.find('an') if data else None)   # 19
print(19 if None else x / y)               # 6.0
print(data.rfind('an') if data else None)  # 32
print(7 if len(data) > 19 else 6)          # 7
```

Explanation:

The find() method is looking for the first occurrence of a string in a string

and returns the index, where this string is starting.

In this case 'an' starts in data at index 19

rfind() looks from the right and will find the last occurrence.

In this case the 'an' in "can't" at index 32

None evaluates to False and therefore the else clause executes.

And yes, the string is longer than 19 but anyway 7 and 6 are both not 19


### 30. Functions

- CASE: What is the expected output of the following code?

```
def func(x=2, y=3):
    return x * y
 
 
print(func(y=2, 3))
```


- Solution: The code is erroneous.


- Try it yourself:

```
def func(x=2, y=3):
    return x * y
 
 
print(func(y=2, 3))
# SyntaxError: positional argument follows keyword argument
print(func(3, y=2))  # 6
```

Explanation:

The keyword arguments always have to be at the end of the list of arguments.

In other words: You can not have a keyword argument before a positional argument.


### 31. Error Handling

- CASE: What is the expected output of the following code?

```
num = '7' * '7'
print(num)
```

- Solution: The code is erroneous.

- Try it yourself:

```
# num = '7' * '7'   # TypeError: ...
print('7' * 4)      # 7777
```

Explanation:

As the error message above states,

you can only multiply a string by an integer.


### 32. Functions

- CASE: Consider the following code.

```
def function(x=0):
    return x
```

With sentence describes the function the best?

A function defined like function() ...


- Solution: may be called without any argument, or with just one.

- Try it yourself:

```
def function(x=0):
    return x
 
print(function())        # 0
print(function(7))       # 7
# print(function(4, 7))  # TypeError: ...
```

Explanation:

The parameter x has the default value 0

You call the function without any argument.

Then x becomes its default 0

Or you can call the function with exactly one argument.

x will get the value of that argument.


### 33. Functions

- CASE: What is the expected output of the following snippet?

```
s = 'python'
for i in range(len(s)):
    i = s[i].upper()
print(s, end='')
```

- Solution: python


- Try it yourself:

```
s = 'python'
for i in range(len(s)):
    i = s[i].upper()
    # s[i] = s[i].upper()  # TypeError: ...
print(s, end="")           # python
```

Explanation:

A string is immutable.

You can not change it, even if you tried.

Here it is not even tried

otherwise the code would cause a TypeError


### 34. Operators

- CASE: What is the expected output of the following code?

```
print('Mike' > 'Mikey')
```

- Solution: False


- Try it yourself:

```
print('Mike' > 'Mikey')  # False
print('y' > '')          # True
print('B' > 'A')         # True
```

Explanation:

Every letter is greater than no character at all.

First the letters M, i, k, e are compared with each other.

Than the empty string is smaller than y

Therefore Mike is smaller than Mickey and it is False that Mike is greater.


### 35. Data Types

- CASE: Consider the following Python code:

```
distance = 1876.23
amount = +42E7
country = 'Italy'
```

What are the types of the variables distance, amount and country?

- Solution: float, float, str

- Try it yourself:

```
print(type(1876.23))  # <class 'float'>
print(type(+42E7))    # <class 'float'>
print(type('Italy'))  # <class 'str'>
 
print(10e6)  # 10000000.0
```

Explanation:

There is no double in Python.

The scientific notation always returns a float

The letter E is called exponent and it does not matter whether you use e or E


### 36. Data Types

- CASE: Consider the following code.

```
data = eval(input('Input: '))
print('Output:', data)
```

Which of the inputs below would produce the specified output?


- Solution: 

```
Input: [x**2 for x in range(1, 4)]
Output: [1, 4, 9]
```

- This question is about the eval() function.

It will evaluate the given code inside of the passed string

Remember input() always returns a string

That works with a number and even the list comprehension.

But to make it work with a string you need to put extra quotation marks around it.


### 37. Data Types

- CASE: What is the expected output of the following code?

```
print('x', 'y', 'z', sep='sep')
```

- Solution: xsepysepz

- Try it yourself:

```
print('x', 'y', 'z', sep='sep')  # xsepysepz
print('x', 'y', 'z')             # x y z
print('x', 'y', 'z', sep='')     # xyz
```

The print() function has the sep parameter

for the separation BETWEEN the arguments.

Its default value is one space.


### 38. Functions

- CASE: What is the expected output of the following code?

```
def func():
    print(x + 1, end=' ')
 
x = 1
func()
print(x)
```

- Solution: 2 1

- Try it yourself:

```
def func():
    print(x + 1, end=' ')  # 2
 
x = 1
func()
print(x)  # 1
```

There is no variable x inside of the function.

Python then will look for a variable x in the outer scope and read from that.

But that will definitely not change the value of the variable x in the outer scope.



### 39. Data Types

- CASE: The following code reads two numbers.

Which of the following is the correct input for the code?

```
x, y = eval(input('Enter two numbers: '))
print(x)
print(y)
```

- Solution: 3, 4

- Try it yourself:

```
# x, y = eval(input('Enter two numbers: '))
x, y = eval('3, 4')              # works
# x, y = eval('3 4')             # SyntaxError: ...
# x, y = eval('<pre>3 4</pre>')  # SyntaxError: ...
print(x)  # 3
print(y)  # 4
```

Explanation:

eval() runs the Python code which is passed as an argument.

For multiple assignment you need a comma separated list.

Therefore '3, 4' is the only possible input.


### 40. Data Aggregates

- CASE: What is the expected output of the following code?

```
data = ['Peter', 'Paul', 'Mary']
print(data[int(-1 / 2)])
```

- Solution: peter

- Try it yourself:

```
data = ['Peter', 'Paul', 'Mary']
print(data[int(-1 / 2)])  # Peter
 
print(-1 / 2)     # -0.5
print(int(-0.5))  # 0
```

First the division takes place and -0.5 is the result.

The integer value of -0.5 is 0

And index 0 is 'Peter'


### 41. Basics

- CASE: The \n digraph forces the print() function to:

- Solution: break the output line

- Try it yourself:

```
print("Hello\nWorld")
# Hello
# World
```

Explanation:

\n is an escape character which results in a new line.



