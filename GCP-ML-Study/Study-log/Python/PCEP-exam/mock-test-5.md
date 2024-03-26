### [Source of this study material : Python Certification Exam PCEP by Cord Mählmann](https://www.udemy.com/course/pcep-certification-python-exam-practice-tests/)


## Exam -5

### 1. Functions

- CASE: Which of the following lines properly starts a parameterless function definition?


- Solution: 

```
def fun():
```


### 2. Data Aggregates

- CASE: A data structure described as LIFO is actually a:


- Solution: stack


### 3. Functions

- CASE: The meaning of a positional argument is determined by:


- Solution: its position within the argument list


- Try it yourself:

```
def my_function(a, b, c):
    print(a, b, c)
 
 
my_function(7, 23, 42)  # 7 23 42
```

Explanation:

That's why it's called positional parameter.


### 4. Control Flow

- CASE: You are developing a Python application

for an online product distribution company.

You need the program to iterate through a list of products

and escape when a target product ID is found.

```
productIdList = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
index = 0
 
??? index < 10:
    print(productIdList[index])
    if productIdList[index] == 6:
        ???
    else:
        index += 1
```

What would you insert instead of ??? and ???


- Solution: while, break


- The while loop is the loop, that works with a condition.

The break keyword ends a loop.


### 5. Data Types

- CASE: How many arguments can the print() function take?


- Solution: Any number of arguments(including zero).


- Try it yourself:

```
print(1)                           # 1
print()                            # An empty line
print(1, 2, 3, 4, 5, 6, 7, 8, 11)  # 1 2 3 4 5 6 7 8 11
```

Explanation:

The print() function called without an argument will print an empty line.

The amount of possible arguments depends on the capacities of your computer

but it is going to be more than you will ever need.


### 6. Data Types

- CASE: You want to write a programm that asks the user for a value.

For the rest of the programm you need a whole number,

even if the user enters a decimal value.

What would you have to write?


- Solution: num = int(float(input('How many do you need? ')))


- The input() function returns a string and in the end you need an integer

You can not use int() directly,

because you would get a ValueError if the user enters a decimal value.

Therefore you have to cast the input string to a float and then to an integer

```
a = int(float(input('How many do you need? ')))

print(f"You need {a} dounuts") # 4.7 -> 4
```

### 7. Data Aggregates

- CASE: What is the expected output of the following code?

```
data1 = '1', '2'
data2 = ('3', '4')
print(data1 + data2)
```

- Solution: ('1', '2', '3', '4')


- Try it yourself:

```
data1 = '1', '2'
data2 = ('3', '4')
print(data1 + data2)  # ('1', '2', '3', '4')
```

Explanation:

You do not need the parentheses to create a tuple

The rest is normal tuple concatenation.


### 8. Control Flow

- CASE: The following is a program to validate customer numbers.



customer_number = input('Enter the employee number (dd-ddd-dddd): ')
parts = customer_number.split('-')
valid = False
if len(parts) == 3:
  if len(parts[0]) == 2 and len(parts[1]) == 3 and len(parts[2]) == 4:
    if parts[0].isdigit() and parts[1].isdigit() and parts[2].isdigit():
      valid = True
print(valid)


The number may only contain numbers and dashes.

The number must have the right format (dd-ddd-dddd).



What is true about this programm?


- Solution: The program works properly.


- Try it yourself:

```
# customer_number = input('Enter the employee number (dd-ddd-dddd): ')
customer_number = '12-345-6789'     # True
# customer_number = '12345-6789'    # False
# customer_number = 'A2-345-6789'   # False
# customer_number = '112-345-6789'  # False
parts = customer_number.split('-')
valid = False
if len(parts) == 3:
  if len(parts[0]) == 2 and len(parts[1]) == 3 and len(parts[2]) == 4:
    if parts[0].isdigit() and parts[1].isdigit() and parts[2].isdigit():
      valid = True
print(valid)
```
 
Explanation:

Everything works fine here.

The string with the number gets splitted into a list.

Then there are three conditions.

First if the list has three parts.

Second if all the parts have the right length.

Third if all the parts only contain digits.


### 9. Functions

- CASE: A built‑in function is a function which ...


- Solution: coms with Python, and is an integral part of Python.


Try it yourself:

```
# To print out the built-in functions:
for i in dir(__builtins__):
    if i[0] != '_' and i[0].islower():
        print(i, end=', ')
 
"""
abs, all, any, ascii, bin, bool, breakpoint, bytearray, bytes,
callable, chr, classmethod, compile, complex, copyright,
credits, delattr, dict, dir, divmod, enumerate, eval, exec,
exit, filter, float, format, frozenset, getattr, globals,
hasattr, hash, help, hex, id, input, int, isinstance,
issubclass, iter, len, license, list, locals, map, max,
memoryview, min, next, object, oct, open, ord, pow, print,
property, quit, range, repr, reversed, round, set, setattr,
slice, sorted, staticmethod, str, sum, super, tuple, type,
vars, zip
"""
```

Explanation:

The built-in functions do not have to be imported,

they are not hidden from programmers

and not place in your code by another programmer.

The built-in functions come with Python as an integral part of the language.

Just look at the list above.

You will recognize most of them.


### 10. Functions

- CASE: What is the expected output of the following code?

```
data = [1, 2, 3, None, (), [], ]
print(len(data))
```

- Solution: 6


- An empty element is still an element.

That makes it six.

The trailing comma just gets ignored.


### 11. Error Handling

- CASE: What is the expected output of the following code?

```
try:
    raise Exception
except BaseException:
    print('1')
except Exception:
    print('2')
except:
    print('3')
```

- Solution: 1


- Explanation:

BaseException is the top-most Exception in Python.

Therefore Exception (like any other exception class)

is a subclass of BaseException

And that is why the except BaseException block is executed.


### 12. Functions

- CASE: What is the expected output of the following code?

```
x = 42
 
 
def func():
    global x
    print('1. x:', x)
    x = 23
    print('2. x:', x)
 
 
func()
print('3. x:', x)
```

- Solution: 

1. x: 42
2. x: 23
3. x: 23


- The variable x existed in the outer scope before the function call.

The global keyword turns the variable x into a global variable.

From now on it exists in the outer scope and in the function scope.

Therefore the change inside the function effect x in the outer scope.


### 13. Operators

- CASE: What is the expected output of the following code?

```
x = 1
print(++++x)
```

- Solution: 1

First of all there is no increment operator ++ in Python.

You can add as many plus signs as you like, the number stays positive.

By the way, the minus sign works differently.

Two times minus is plus.


### 14. Data Aggregates

- CASE: What is the output of the following snippet?

```
my_list = [1, 2]
 
for v in range(2):
    my_list.insert(-1, my_list[v])
 
print(my_list)
```

- Solution: [1, 1, 1, 2]


- Try it yourself:


```
my_list = [1, 2]
 
for v in range(2):
    my_list.insert(-1, my_list[v])
 
print(my_list)    # [1, 1, 1, 2]
 
# The same without for loop:
my_list_2 = [1, 2]
my_list_2.insert(-1, my_list_2[0])
print(my_list_2)  # [1, 1, 2]
my_list_2.insert(-1, my_list_2[1])
print(my_list_2)  # [1, 1, 1, 2]
```

Explanation:

The index -1 represents the last element

and therefore the new elements will be inserted before the last element.

In the first iteration the element with the index 0 will be inserted.

The value of that index is 1 and therefore the list will be: [1, 1, 2]

In the second iteration the element with the index 1 will be inserted.

The value of that index is NOW also 1 and therefore the list will be:

[1, 1, 1, 2]


### 15. Functions

- CASE: What is the expected output of the following code?

```
def func(n):
    s = ''
    for i in range(n):
        s += '*'
        yield s
 
 
for x in func(3):
    print(x, end='')
```

- Solution: ******


- Try it yourself:

```
def func(n):
    s = ''
    for i in range(n):
        s += '*'
        yield s
 
 
for x in func(3):
    print(x, end='')  # ******
 
print()
print(func(3))        # <generator object func at ...>
print(list(func(3)))  # ['*', '**', '***']
```

Explanation:

The function call func(3) will return a generator object.

In the first iteration of the for loop that generator object will return *

The second iteration will return **

and the third iteration will pass ***

That makes six stars in total: ******


### 16. Data Aggregates

- CASE: What is the expected output of the following code?

```
data = ((1, 2),) * 7
print(len(data[3:8]))
```

- Solution: 4


```
data = ((1, 2),) * 7
print(len(data[3:8]))    # 4
 
print(data)
# ((1, 2), (1, 2), (1, 2), (1, 2), (1, 2), (1, 2), (1, 2))
print(len(data[3:100]))  # 4
```

- There is only going to be seven elements.

Therefore 6 is going to be the highest index.

And so the slicing ends up with the indexes 3, 4, 5 ,6

which are four elements.


### 17. Functions

- CASE: What is the expected output of the following code?

```
def func(data):
    data = [7, 23, 42]
    print('Function scope: ', data)
 
 
data = ['Peter', 'Paul', 'Mary']
func(data)
print('Outer scope: ', data)
```

- Solution:

```
Function scope: [7, 23, 42]
Outer scope: ['Peter', 'Paul', 'Mary']
```

- Try it yourself:

```
def func(data):
    data = [7, 23, 42]
    print('Function scope: ', data)  # [7, 23, 42]
 
 
data = ['Peter', 'Paul', 'Mary']
func(data)
print('Outer scope: ', data)  # ['Peter', 'Paul', 'Mary']
```


Explanation:

The parameter data will become a new entity with the function as its scope.

The variable data in the outer scope is a different entity.


### 17. Basics

- CASE: ASCII is:


- Solution: short for American Standard Code for Information Interchange.


### 18. Basics

- CASE: What is IDLE?


- Solution: An acronym that stands for Integrated Development and Learning Environment for Python.


### 19. Basics

- CASE: You have the following file.

```
index.py:
from sys import argv
sum = 0
for i in range(2, len(argv)):
    sum += float(argv[i])
print(
    "The average score for {0} is {1:.2f}"
    .format(argv[1], sum/(len(argv)-2))
)
```

You want the following output.

The average score for Peter is 200.00

Which command do you have to execute in the command line?


- Solution: 

```
python index.py Peter 100 200 300
```

- Try it yourself:

```
# First execute the following to create the needed file:
code = '''
from sys import argv
sum = 0
for i in range(2, len(argv)):
    sum += float(argv[i])
print(
    "The average score for {0} is {1:.2f}"
    .format(argv[1], sum/(len(argv)-2))
)
'''
with open('index.py', 'w') as f:
    f.write(code)
 
# In Terminal:
# python index.py Peter 100 200 300
```

Explanation:

range() starts at 2 because in index 0 always is the filename

and in index 1 will be the name Peter

format() is used here with numbered indexes.

The name 'Peter' from argv[1] will go to {0}

and the average will go to {1}

The numbered index {1} is also formated by {1:.2f}

with is responsible for the two fix point number format: 200.00

To test it, you have to open the folder

where you created the index.py file in a terminal

and run the file by executing python index.py Peter 100 200 300


### 20.  Data Aggregates

- CASE: The fact that tuples belong to sequence types means:


- Solution: they can be indexed and sliced like lists


- Try it yourself/Explanation:

```
my_tuple = (1, 2, 3, 4)
# Indexing:
print(my_tuple[2])    # 3
# Slicing:
print(my_tuple[1:3])  # (2, 3)
 
# They CANNOT be modified using the del instruction:
# del my_tuple[0]
# TypeError: 'tuple' object doesn't support item deletion
 
# They CANNOT be extended using the .append() method:
# my_tuple.append(5)
# AttributeError: 'tuple' object has no attribute 'append'
```

### 21.  Data Types

- CASE: Which of the following statements are true?

- Solution:

- The None value can be assigned to variables

- The None value can be compared with variables


```
# The None value can be assigned to variables:
x = None
print(x)  # None
 
# The None value can be compared with variables:
y = 3
print(y is None)  # False
 
# The None value CANNOT be used
# as an argument of arithmetic operators:
# print(None + 7)  # TypeError: unsupported operand ...
 
# The None value can be used outside functions:
z = None
print(z)  # None
```

- It is true, the None value cannot be used as an argument of arithmetic operators.

But the None value can be assigned and compared to variables.

And that can absolutely happen outside of a function.


### 22.  Basics

- CASE: What is the expected output of the following code?

```
x = '\\\'
print(len(x))
```

- Solution: The code is erroneous.

- Try it yourself:

```
# print(len('\'))    # SyntaxError: ...
print(len('\\'))     # 1
# print(len('\\\'))  # SyntaxError: ...
```

Explanation:

The backslash is the character to escape another character.

If you write '\' the backslash escapes

the ending single quote to a normal character.

It takes its syntactical meaning and the single quote becomes a normal character

and it looses its ability to end the string and therefore we get the syntax error.

If you write '\\' the one backslash escapes the other

and you end up with a string with one normal backslash.

If you write '\\\' you again have the same problem

than with one single backslash.

The first backslash escapes the second one,

but the third backslash escape the ending single quote,

the string does not get closed and you get a syntax error.


### 23.  Data Aggregates

- CASE: Which of the following sentences is true?

```
str1 = 'Peter'
str2 = str1[:] 
```

- Solution: str1 and str2 are different names of the same string.

- Try it yourself:

```
str1 = 'Peter'
str2 = str1[:]
# str2 = str1        # The same thing
 
print(id(str1))  # e.g. 140539652049216
print(id(str2))  # e.g. 140539652049216 (the same number than str1)
print(str1 is str2)  # True
print(str1 == str2)  # True
```

Explanation:

Copying with [:] only works with mutable data types like a list

A string is an immutable data type.

Whether you slice the whole thing or just assign it,

you always end up with a reference to the same object.


### 24.  Data Types

- CASE: You want to print the sum of two number.

What snippet would you insert in the line indicated below:

```
x = input('Enter the first number: ')
y = input('Enter the second number: ')
#  insert your code here
```

- Solution: print('The result is' + str(int(x) + int(y)))


- As always input() returns a string

Before you add them to each other you need to cast both of them to an integer

You need to cast the result to a string

to be able to concatenate it to the other string


### 25. Data Aggregates

- CASE: What is the expected output of the following code?

```
data = {'name': 'Peter', 'age': 30}
person = data.copy()
print(id(data) == id(person))
```

- Solution: False

- Try it yourself:

```
data = {'name': 'Peter', 'age': 30}
person = data.copy()
print(id(data) == id(person))  # False
 
person = data
print(id(data) == id(person))  # True
```

Explanation:

The copy() method creates a copy of the dictionary

If you just assign the dictionary a reference is created.



### 26. Functions

- CASE: The following snippet:

```
def func(a, b):
    return b ** a
  
print(func(b=2, 2))
```

- Solution: is erroneous.

- Try it yourself:

```
def func(a, b):
    return b ** a
 
 
# print(func(b=2, 2))
# SyntaxError: positional argument follows keyword argument
```

Explanation:

The order of the arguments is wrong.

You cannot have a keyword argument before a positional argument.


### 27. Basics

- CASE: You have the following file.

```
index.py:
from sys import argv
print(argv[1] + argv[2])
```

You run the file by executing the following command in the terminal.

```
python index.py 42 3
```

What is the expected oputput?


- Solution: 423

- The indexes 1 and 2 are the right ones

(Remember the filename always is in index 0).

All the values in argv are going to be strings.

Therefore string concatenation will take place

and the result will be the string '423'

To test it you have to open the folder

where you created the index.py file in a terminal

and run the file by executing python index.py 42 3


### 28. Control Flow

- CASE: What is the expected output of the following code?

```
x = 2

y = 6

x += 2 ** 3

x //= y // 2 // 3

print(x)
```

- Solution: 10


- Try it yourself:

```
x = 2
y = 6
x += 2 ** 3
x //= y // 2 // 3
print(x)                      # 10
 
x += 2 ** 3
x = x + (2 ** 3)
print(2 + (2 ** 3))           # 10
print(2 + 8)                  # 10
print(10)                     # 10
 
x //= y // 2 // 3
x = x // (y // 2 // 3)
print(10 // (6 // 2 // 3))    # 10
print(10 // ((6 // 2) // 3))  # 10
print(10 // (3 // 3))         # 10
print(10 // 1)                # 10
print(10)                     # 10
```


### 29. Data Aggregates

- CASE: Which one of the lines should you put in the snippet below

to match the expected output?


Expected output:

[4, 1, 7, 2, 'A']


Code:

list = ['A', 2, 7, 1, 4]
 
# enter code here
 
print(list)


- Solution: list.reverse()


- list.reverse()

The reverse() method reverses the elements of the list in place.


### 30. Basics

- CASE: What is CPython?

- Solution: The default implementation of the Python programming language.

- Guido van Rossum used the "C" programming language

to implement the very first version of his language

and this decision is still in force.

All Pythons coming from the PSF (Python Software Foundation)

are written in the "C" language.

There are many reasons for this approach.

One of them (probably the most important) is that thanks to it,

Python may be easily ported and migrated to all platforms

with the ability to compile and run "C" language programs

(virtually all platforms have this feature,

which opens up many expansion opportunities for Python).

This is why the PSF implementation is often referred to as CPython.

This is the most influential Python among all the Pythons in the world.


### 31. Basics

- CASE: A keyword is a word:

- Solution:

- that cannot be used as a function name.

- that cannot be used as a variable name.


- Try it yourself:

```
# for = 7          # SyntaxError: invalid syntax
# def for(): pass  # SyntaxError: invalid syntax
import keyword
print(keyword.kwlist)
"""
['False', 'None', 'True', 'and', 'as', 'assert', 'async',
'await', 'break', 'class', 'continue', 'def', 'del', 'elif',
'else', 'except', 'finally', 'for','from', 'global', 'if',
'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or',
'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']
"""
```

### 32. Basics 

- CASE: The print() function can output values of:


- Solution: any number of arguments (including zero)


Try it yourself:

```
print("Hello")  # Hello
print()         # An extra line break
print("World")  # World
 
print("The", "quick", "brown", "fox", "jumps", "over", "...")
# The quick brown fox jumps over ...
```

### 33. Functions

- CASE: What is the expected output of the following code?

```
def func(x):
    if x % 2 == 0:
        return 1
    else:
        return
 
 
print(func(func(2)) + 1) 
```

- Solution: The code is erroneous.

- Try it yourself:

```
def func(x):
    if x % 2 == 0:
        return 1
    else:
        return
 
 
print(func(func(2)) + 1)  # TypeError: ...
```
Explanation:

The condition x % 2 == 0 tests for even numbers.

The first function call func(2) passes an even number

and the return value will be 1

The second function call will therefore pass an odd number func(1)

The return with no value will return None

And you can not calculate with None


### 34. Data Aggregates

- CASE: What is the output of the following snippet?

```
tup = (1, ) + (1, )
tup = tup + tup
print(len(tup))
```

- Solution: 4

- Try it yourself:

```
# tup = (1, ) + (1, )
tup = (1, 1)
print(tup)       # (1, 1)
# tup = tup + tup
tup = (1, 1) + (1, 1)
print(tup)       # (1, 1, 1, 1)
print(len(tup))  # 4
```

Explanation:

You can add one tuple to another.

It becomes a tuple with all the elements of both tuples.


### 35. Error Handling

- CASE: What is the expected behavior of the following program if the user enters 0?

```
value = input("Enter a value: ")
print(10/value)
```

- Solution: The program will raise the TypeError exception.


- Try it yourself:

```
# value = input("Enter a value: ")
value = "0"
print(10/value)
# TypeError: unsupported operand type(s) for /: 'int' and 'str'
```

The input() function always returns a string.

If you try to divide by a string you get a TypeError


### 36. Operators

- CASE: What would you insert instead of ???

so that the program prints True to the monitor?

```
x = 'Peter'
y = 'Peter'
res = ???
print(res)
```

- Solution: x is y

- Try it yourself:

```
x = 'Peter'
y = 'Peter'
res = x is y       # True
print(res)
 
print(x < y)       # False
print(x != y)      # False
print(x is not y)  # False
 
print(id(x))  # e.g. 140539652049216
print(id(y))  # e.g. 140539652049216 (the same number)
```

Explanation:

A string is an immutable data type.

If you create a second string of the same value,

Python will create a reference to the same object.

Therefore those two strings will have the same identity.


### 37. Control Flow

- CASE: Which one of the lines should you put in the snippet below

to match the expected output?

Expected output:

```
adam_smit
```

Code:

```
for ch in "adam_smit@openedg.org":
 
    if ch == "@":
        # insert code here
 
    print(ch, end="")
```

- Solution: break

- Try it yourself:

```
for ch in "adam_smit@openedg.org":
    if ch == "@":
        break
    print(ch, end="")  # adam_smit
```

Explanation:

The for loop with a string will assign one character after the other to ch

When the @-character is assigned the loop needs to

stop in order to end the printing of the characters.

That is what the break keyword is for.


### 38. Control Flow

- CASE: How many stars will the following snippet print to the monitor?

```
for i in range(1):
    print('*')
else:
    print('*')
```

- Solution: two

- Try it yourself:

```
for i in range(1):
    print('i:', 1)  # 1
    print('*')      # *
else:
    print('*')      # *
```

Explanation:

There will be just one iteration.

But because there is no break inside the for loop,

the else clause will execute and the second star will be printed.


### 39. Error Handling

- CASE: An assertion can be used to:

- Solution: Stop the program when some data have improper values.

- Try it yourself:

```
def remove_min(s):
    assert type(s) == list
    assert len(s) > 0
    m = min(s)
    s.remove(m)
    return s
 
 
print(remove_min([1, 2, 3]))  # [2, 3]
# print(remove_min('Hello'))  # ... AssertionError
# print(remove_min([]))       # ... AssertionError
```

Explanation:

The function remove_min() removes the minimal value from a list.

First the function checks, whether the argument is a list

and second the function checks, whether that list has elements.


### 40. Data Types

- CASE: If you want to build a string that reads:

Peter's sister's name's "Anna"

Which of the following literals would you use?


- Solution: 'Peter\'s sister\'s name\'s \"Anna\"'


- Try it yourself:

print("Peter's sister's name's \"Anna\"")
# Peter's sister's name's "Anna"
print('Peter\'s sister\'s name\'s \"Anna\"')
# Peter's sister's name's "Anna"
# print("Peter's sister's name's "Anna"")
# SyntaxError: invalid syntax
# print('Peter's sister's name's "Anna"')
# SyntaxError: invalid syntax
Explanation:

When you use the same kind of quotes inside of a string

and outside to delimiter the string

you have to escape the ones inside of the string







