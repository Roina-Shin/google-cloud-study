### [Source of this study material : Python Certification Exam PCEP by Cord Mählmann](https://www.udemy.com/course/pcep-certification-python-exam-practice-tests/)


## Exam -4

### 1. Functions

- CASE: What is the expected output of the following code?

```
def get_names():
    names = ['Peter', 'Paul', 'Mary', 'Jane', 'Steve']
    return names[2:]
 
 
def update_names(names):
    res = []
    for name in names:
        res.append(name[:3].upper())
    return res
 
 
print(update_names(get_names()))
```


- Solution: ['MAR', 'JAN', 'STE']


- The slicing in get_names() is a list slicing: names[2:]

It has a start of 2 and no end.

That means, the slicing goes from the second index (inclusive) to the end.

That will be ['Mary', 'Jane', 'Steve']

That list will be passed to the update_names() function.

The other slicing inside the for loop is a string slicing,

that will slice every element of the list

name[:3] will slice from the start to the index 3 (exclusive).

Meaning it takes the first three letters.

The upper() method will then convert those letters to uppercase letters.



### 2. Data Aggregates

- CASE: Insert the correct snippet to convert the t tuple to a dictionary named d



Expected output:

{'A': 1, 'B': 2, 'C': 3}


Code:

```
t = (('A', 1), ('B', 2), ('C', 3))
# insert code here
print(d)
```

- Solution: d = dict(t)


- Try it yourself:

t = (('A', 1), ('B', 2), ('C', 3))
d = dict(t)
print(d)  # {'A': 1, 'B': 2, 'C': 3}


Explanation:

The dict() function is one of Python's built-in functions.

Here it converts a tuple of tuples with two elements into a dictionary.



### 3. Data Aggregates

- CASE: Consider the following list.


```
data = [1, 5, 10, 19, 55, 30, 55, 99]
```


Which of the code snippets below would produce a new list like the following?


```
[1, 5, 10, 99]
```


- Solution: 

```
data.pop(5)
data.remove(19)
data.remove(55)
data.remove(55)
```

- list.pop([i])

The index is optional.

If the index is given pop()

removes and returns the element at the given index.

The default index is -1

Meaning that the last index is removed and returned.

data.pop(5) removes the value 30

The remove() method removes the first occurrence

of the element with the specified value.

data.remove(19)

data.remove(55)

data.remove(55)

is exactly what is needed.


### 4. Data Types

- CASE: What is the expected output of the following code?


```
print(not 0)
print(not 23)
print(not '')
print(not 'Peter')
print(not None)
```


- Solution: 

```
True
False
True
False
True
```

- Try it yourself:

```
print(not 0)        # True
print(not 23)       # False
print(not '')       # True
print(not 'Peter')  # False
print(not None)     # True
```


Explanation:

The values 23 and 'Peter' will evaluate to True

and the rest will evaluate to False

The not turns everything around.

The values that become False in Python are the following:

```
print(bool(''))        # False
print(bool(0))         # False
print(bool(0.0))       # False
print(bool(0j))        # False
print(bool(None))      # False
print(bool([]))        # False
print(bool(()))        # False
print(bool({}))        # False
print(bool(set()))     # False
print(bool(range(0)))  # False
```

### 5. Data Types

- CASE: The user enters 123

Which of the following code snippets will print 124 to the monitor?

Choose three.


- Solution:


```
num = eval(input('Please enter your number: '))
print(num + 1)

num = int(input('Please enter your number: '))
print(num + 1)

num = input('Please enter your number: ')
print(int(num) + 1)
```

- Like always input() returns a string

eval() runs the Python code which is passed as the argument.

The string '123' will become the integer 123

int() does the same job here.

And you can cast to an integer directly after the input or before the printing.


### 6. Functions

- CASE: A way of passing arguments in which the order of the arguments

determines the initial parameter's values is referred to as:


- Solution: positional


- If the arguments are just literal values they are positional arguments.


```
def my_function(a, b):
    print(a, b)
 
 
my_function('Hello', 'World')  # Hello World
my_function('World', 'Hello')  # World Hello
```

### 7. Functions

- CASE: What does the following code do?


```
def a(b, c, d):
    pass
```

- Solution: Defines a function, which does nothihg


- Try it yourself:

```
def a(b, c, d):
    pass
```

Explanation:

def a(b, c, d): defines the function

and pass just does nothing.

You can use that, when you know, that you will need a function,

but want to write the function body later on.


### 8. Functions

- CASE: Which of the following enclose the input parameters or arguments of a function?


- Solution: Parentheses



### 9. Functions

- CASE: What is the expected output of the following code?

```
box = {}
jars = {}
crates = {}
 
box['biscuit'] = 1
box['cake'] = 3
 
jars['jam'] = 4
 
crates['box'] = box
crates['jars'] = jars
 
print(len(crates[box]))
```

- Solution: The code is erroneous.


```
box = {}
jars = {}
crates = {}
 
box['biscuit'] = 1
box['cake'] = 3
 
jars['jam'] = 4
 
crates['box'] = box
crates['jars'] = jars
 
print(len(crates[box]))  # TypeError: unhashable type: 'dict'
print(len(crates['box']))  # 2
print(crates['box'])       # {'biscuit': 1, 'cake': 3}
print(crates)
# {'box': {'biscuit': 1, 'cake': 3}, 'jars': {'jam': 4}}
```


- Much ado about nothing.

In the end there are just missing single quotes around box in the last line.


### 10. Functions

- CASE: What is the expected output of the following code?

```
x = (1, 4, 7, 9, 10, 11)
y = {2: 'A', 4: 'B', 6: 'C', 8: 'D', 10: 'E', 12: 'F'}
res = 1
for z in x:
    if z in y:
        res += z
print(res)
```

- Solution: 15


- The for loop iterates through the tuple x

The if statement checks, whether one of the elements of the tuple

also is in index of the dictionary y

This is the case for 4 and for 10

Therefore 4 and 10 are added to the res variable,

which is already 1 in the beginning:

1 + 4 + 10 -> 15


### 11. Control Flow

- CASE: What is the expected output of the following code?


```
data = [[42, 17, 23, 13], [11, 9, 3, 7]]
res = data[0][0]
for da in data:
    for d in da:
        if res > d:
            res = d
print(res)

```

- Solution: 3


### 12. Basics

- CASE: What is machine code?


- Solution: A low-level programming language consisting of binary digits/bit that the computer reads and understands.


### 13. Basics

- CASE: What is the default value of encoding in the string function encode()?


- Solution: utf-8


- Try it yourself:

print(list('a'.encode()))          # [97]
print(list('a'.encode('utf-8')))   # [97]
print(list('a'.encode('utf-16')))  # [255, 254, 97, 0]
print(list('a'.encode('utf-32')))  # [255, 254, 0, 0, 97, 0, 0, 0]
Explanation:

The official documentation says it all:

https://docs.python.org/3/library/stdtypes.html?highlight=str.encode#str.encode

str.encode(encoding="utf-8", errors="strict")

Return an encoded version of the string as a bytes object.

Default encoding is 'utf-8' ...


### 14. Operators

- CASE: What is the expected output of the following code?


```
a = 1
b = 0
c = a & b
d = a | b
e = a ^ b
print(c + d + e)
```


- Solution: 2


```
a = 1
b = 0
c = a & b
d = a | b
e = a ^ b
print(c + d + e)  # 2
 
print(1 & 0)      # 0
print(1 | 0)      # 1
print(1 ^ 0)      # 1
```

- 1 and 0 is 0

1 or 0 is 1

1 xor 0 is 1

The total is 2


### 15. Data Types

- CASE: What is the expected output of the following code?

```
print(type(+1E10))
print(type(5.0))
print(type('True'))
print(type(False))
```


- Solution: 

```
<class 'float'>
<class 'float'>
<class 'str'>
<class 'bool'>
```

- Try it yourself:

print(type(+1E10))   # <class 'float'>
print(type(5.0))     # <class 'float'>
print(type('True'))  # <class 'str'>
print(type(False))   # <class 'bool'>
Explanation:

The scientific notation always returns a float

A string with the word 'True' is still a string


### 16. Data Aggregates

- CASE: What is the expected output of the following code?


```
data = {}
data[1] = 1
data['1'] = 2
data[1.0] = 4
 
res = 0
for d in data:
    res += data[d]
 
print(res)
```


- Solution: 6


```
data = {}
data[1] = 1
data['1'] = 2
data[1.0] = 4
 
res = 0
for d in data:
    res += data[d]
 
print(res)                       # 6
 
print(data)                      # {1: 4, '1': 2}
```

- Dictionary can have different data types as a key.

BUT if an integer and a float have the same value,

the second value overrides the first values.

And the first index is still name giving.


### 17. Error Handling

- CASE: Which of the following snippets shows the correct way

of handling multiple exceptions in a single except clause?


- Solution: 

```
except (TypeError, ValueError, ZeroDivisionError):
    # some code
```

- In Python the colon always has to be at the end of the line.

The list of possible exceptions has to be in parentheses.


```
try:
    print(7 / 0)
except (TypeError, ValueError, ZeroDivisionError):
    print("That is not allowed!")
```


### 18. Data Aggregates

- CASE: How many elements does the my_list list contain?

```
my_list = [0 for i in range(1, 3)]
```

- Solution: two


- Try it yourself:

```
my_list = [0 for i in range(1, 3)]
print(my_list)       # [0, 0]
print(len(my_list))  # 2
# The same without list comprehension:
my_list2 = []
for i in range(1, 3):
    my_list2.append(0)
print(my_list)       # [0, 0]
print(len(my_list))  # 2
```

- range(1, 3) will be 1 & 2 and therefore

the for loop will iterate twice.

Both times 0 will be appended to the list.


### 19. Data Aggregates

- CASE: What is the output of the following snippet?

```
l1 = [1, 2, 3]
 
for v in range(len(l1)):
    l1.insert(1, l1[v])
 
print(l1)
```


- Solution: [1, 1, 1, 1, 2, 3]


- Try it yourself:

```
l1 = [1, 2, 3]
# for v in range(len(l1)):
for v in range(3):
    l1.insert(1, l1[v])
print(l1)  # [1, 1, 1, 1, 2, 3]
 
l2 = [1, 2, 3]
l2.insert(1, l2[0])
print(l2)  # [1, 1, 2, 3]
l2.insert(1, l2[1])
print(l2)  # [1, 1, 1, 2, 3]
l2.insert(1, l2[2])
print(l2)  # [1, 1, 1, 1, 2, 3]
```

Explanation:

This code will insert thrice the value 1

In the first iteration the 1 from index 0 will be inserted.

That changes the list and in the second iteration there is also the value 1 at index 1

And in the third iteration there is also a value 1 at index 2

The list gets altered in the for loop

and there is always the value 1 at the index l1[v]


### 20. Data Types

- CASE: What is the expected output of the following code if the user enters 3 and 2?


```
x = int(input())
y = int(input())
x = x % y
x = x % y
y = y % x
print(y)
```

- Solution: 0


### 21. Error Handling

- CASE: What is the expected result of the following code?

```
try:
    raise Exception
except:
    print("c")
except BaseException:
    print("a")
except Exception:
    print("b")
```

- Solution: The code will cause a syntax error.


- Try it yourself:

```
"""
try:
    raise Exception
except:
    print("c")
except BaseException:
    print("a")
except Exception:
    print("b")
"""
# SyntaxError: default 'except:' must be last
 
# This still does not make much sense,
# but there would be no syntax error.
try:
    raise Exception
except BaseException:
    print("a")          # a
except Exception:
    print("b")
except:
    print("c")
```

Explanation:

As the error message claims:

default 'except:' must be last


### 22. Error Handling

- CASE: The following statement ...

```
assert x == 0
```


- Solution: will stop the program if x is not equal to 0


- Try it yourself:

```
x = 0
assert x == 0
print('Hello')  # Hello
 
x = 7
assert x == 0   # AssertionError
print('Hello')
```

Explanation:

If the assertion (here x == 0) is True

the program will continue.

Otherwise an AssertionError occurs.


### 23. Functions 

- CASE: Which of the literals below is not a valid function name?


- Solution: 1function


- A function name has to start with a letter or an underscore.

Then numbers, letters and underscores can follow.


### 24. Operators 

- CASE: What will be the output of the following snippet?

```
a = 1
b = 0
a = a ^ b
b = a ^ b
b = a ^ b
print(a, b)
```

- Solution: 1 0


- The bitwise xor operator returns 1 when one operand is 1 and the other is 0

When both operands are 0 or both operands are 1 it returns 0


### 25. Data Aggregates

- CASE: What is the expected output of the following code?


```
data = {'z': 23, 'x': 7, 'y': 42}
 
for _ in sorted(data):
    print(data[_], end=' ')
```


- Solution: 7 42 23


- Try it yourself:

```
data = {'z': 23, 'x': 7, 'y': 42}
 
for _ in sorted(data):
    print(data[_], end=' ')  # 7 42 23
 
print()
print(sorted(data))          # ['x', 'y', 'z']
print(data)                  # {'z': 23, 'x': 7, 'y': 42}
```


Explanation:

The sorted() function returns a sorted

list from the elements in a dictionary (or any other iterable).

In this case the list ['x', 'y', 'z']

In the for loop those indexes get printed out.


### 26. Control Flow

- CASE: Consider the following code.


```
room = input('Enter the room number: ')
rooms = {101: 'Gathering Place', 102: 'Meeting Room'}
if not room in rooms:
    print('The room doesn\'t exist.')
else:
    print('The room name is: ' + rooms[room])

```
Why is it not working?


- Solution: Mismatched data type(s)


- Try it yourself:

```
# room = input('Enter the room number: ')
room = '101'  # Just for convenience
rooms = {101: 'Gathering Place', 102: 'Meeting Room'}
if not room in rooms:
    # if room not in rooms:
    print('The room does not exist.')
else:
    print('The room name is: ' + rooms[room])
```

Explanation:

The reason, why the code will never find a room is,

that input() always returns a string

and the indexes of the dictionary are all an integer

not room in rooms is not very good code.

Better is room not in rooms

But it is not a syntax error (like it would be in other languages).

In Python it is "only" a violation against the Python coding conventions


### 27. Basics

- CASE: Select the true statements:

(Select two answers)


- Solution:

- You cannot use keywords as variable names in Python.

- You cannot use keywords as function names in Python.


### 28. Basics

- CASE: The pyc file contains ...


- Solution: compiled Python bytecode.


- Try it yourself:

```
# You have to run this to create the needed files:
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

Explanation:

First please check, if the files index.py

and functions.py are created as expected.

Now run the file index.py and the folder __pycache__ should be created.

In case your Editor/IDE does not show the folder, check in your file system.

Inside the folder should be a file like functions.cpython-<versionnumber>.pyc

This file contains compiled Python bytecode.

Next time you run index.py Python will use

the compiled bytecode for faster execution.


### 29. Data Types

- CASE: What is the expected output of the following code?

```
print(chr(ord('p') + 3))

```

- Solution: s


Try it yourself:

```
print(chr(ord('p') + 3))  # s
print(ord('p'))           # 112
print(chr(115))           # s
```

Explanation:

ord() returns an integer representing the Unicode character.

chr() turns that integer back to the Unicode character.

You do not need to remember the number of each character,

but like in the alphabet s is three after p


### 30. Functions

- CASE: The following snippet:


```
def func(a, b):
    return a ** a
 
 
print(func(2))
```

- Solution: is erroneous

- Try it yourself:

```
def func(a, b):
    return a ** a
 
 
# print(func(2))
# TypeError: func() missing 1 required positional argument: 'b'
```

Explanation:

There are two parameters without any default values and only one argument.

That causes a TypeError


### 31. Data Types

- CASE: Which of the following is the output of the below Python code?

```
str = 'Hello World'
print(str[::-1])
```

- Solution: dlrow olleH


- Try it yourself:

```
str = 'Hello World'
print(str[::-1])  # dlroW olleH
```

Explanation:

[start:stop:step]

Slicing the string with [::-1] makes a reversed copy of the string.

The step is -1 which takes every element but in reversed order.


### 32. Control Flow

- CASE: What will happen when you attempt to run the following code?

```
While True:
    print("1")
```

- Solution: The code will not run due to syntax error.

- Try it yourself:

```
# While True:
    # print("1")
```

Explanation:

Python is case sensitiv and While with a capital W is not a keyword.

Therefore the program will not run and produce a syntax error.


### 33. Basics

- CASE: What do you call a computer program which directly

executes instructions written in a programming language?


- Solution: An interpreter


- Interpretation means, that you (or any user of the code)

can translate the source program each time it has to be run.

The program performing this kind of transformation is called an interpreter,

as it interprets the code every time it is intended to be executed.

Python is an interpreted language.

If you want to program in Python, you'll need the Python interpreter.


### 34. Data Types

- CASE: The None keyword designates:

- Solution: a None value

- Try it yourself:

```
x = None
print(x)  # None
 
# An empty instruction:
if True:
    pass
 

def my_function(a):
    a = a + 7

 
print(my_function(11))  # None
```

Explanation:

The None keyword stands for a value: The value None

An empty instruction is represented by the pass keyword.

It is true, a function, which doesn't return a value,

returns None, but that does not mean, that the None keyword designates that.

The None keyword is more and has more use cases.

The None keyword designates a None value.


### 35. Operators

- CASE: Consider the following code.

```
x = float('23.42')
```

Which of the following expressions will evaluate to 2?


- Solution: bool(x) + True


- Try it yourself:

```
x = float('23.42')
 
print(bool(x) + True)  # 2
print(int(x) + False)  # 23
print(str(x))          # '23.42'
print(bool(x))         # True
 
print(float('23.42'))  # 23.42
print(bool(23.42))     # True
 
print(True + True)     # 2
print(True - False)    # 1
print(True * True)     # 1
print(True / True)     # 1.0
print(True % True)     # 0
```

Explanation:

First the string '23.42' becomes the float 23.42

Casted to a boolean the float 23.42 becomes True

If you calculate with a boolean True becomes 1 and False becomes 0


### 36. Basics

- CASE: The escape character owes its name to the fact that it:


- Solution: change the meaning of the character next to it.


- Try it yourself:

```
print("Hello\nWorld")
# Hello
# World
```

### 37. Control Flow

- CASE: Analyze the following code fragments

that assign a boolean value to the variable even?


```
num = 42
 
# Code-1
if num % 2 == 0:
    even = True
else:
    even = False
 
# Code-2
even = True if num % 2 == 0 else False
 
# Code-3
even = num % 2 == 0
```

- Solution: All three are correct, but Code-3 is preferred.

- They all work without a syntax error but Code-3 is preferred.

The condition num % 2 == 0 evaluates to a boolean

and therefore that is all you need.


### 38. Functions

- CASE: What is the expected behavior of the following snippet?

```
x = 1
 
 
def a(x):
    return 2 * x
 
 
x = 2 + a(x)      # Line 8
print(a(x))       # Line 9
```

- Solution: 8


### 39. Operators

- CASE: The expression:

'mike' > 'Mike'

is


- Solution: true


- Try it yourself:

```
print('mike' > 'Mike')  # True
print(ord('m'))         # 109
print(ord('M'))         # 77
```

Explanation:

The ASCII code of m is greater than the ASCII code of M


### 40. Data Aggregates

- CASE: What is the expected output of the following code?

```
x = [1, 2, 3, 4, 5, 6, 7, 8, 9]
x[::2] = 10, 20, 30, 40, 50, 60
print(x)
```

- Solution: The code is erroneous.

- Try it yourself:

```
x = [1, 2, 3, 4, 5, 6, 7, 8, 9]
# x[::2] = 10, 20, 30, 40, 50, 60  # ValueError ...
print(x)
 
y = [1, 2, 3, 4, 5, 6, 7, 8, 9]
y[::2] = 10, 20, 30, 40, 50
print(y)  # [10, 2, 20, 4, 30, 6, 40, 8, 50]
```

Explanation:

It is just one value too much.

The list slicing [::2] takes every second index

and assigns one value 1->10, 3->20, 5->30, 7->40, 9->50

In the end there is no index for 60


### 41. Functions

- CASE: What is the expected output of the following code?

```
v = 1
 
 
def fun():
    global v
    v = 2
    return v
 
 
print(v) 
```

- Solution: 1


- Try it yourself:

```
v = 1
 
 
def fun():
    global v
    v = 2
    return v
 
 
print(v)  # 1
```

Explanation:

The fun() function is never called and therefore the value of v stays 1


### 42. Operators

- CASE: What is the expected output of the following code?

```
print(1 // 2)

```

- Solution: 0


- Try it yourself:

```
print(1 // 2)      # 0
print(1.0 // 2)    # 0.0
print(1 // 2.0)    # 0.0
print(1.0 // 2.0)  # 0.0
```

Explanation:

If both operands are an integer the floor division operator will return an integer

If at least one operand is a float the result will also be a float


### 43. Data Aggregates

- CASE: What is the expected output of the following code?

```
data1 = 'a', 'b'
data2 = ('a', 'b')
print(data1 == data2)
```

- Solution: True

- Try it yourself:

```
data1 = 'a', 'b'
data2 = ('a', 'b')
print(data1 == data2)  # True
print(data1 is data2)  # True
print(id(data1))       # e.g. 140539383900864
print(id(data2))       # e.g. 140539383900864 (the same number)
```

Explanation:

You do not need the parentheses to create a tuple

The second tuple will be exactly the same.

And because a tuple is immutable the second tuple will reference

to the same object than the first tuple

And sure, their value will be the same, too.

is tests for identity of the object.

== tests for equality of the values.


### 44. Data Types

- CASE: You want the name, the user puts in to be written back to the monitor.

What snippet would you insert in the line indicated below:

```
print('Enter Your Name: ')
# insert your code here
print(name)
```

- Solution: name = input()


- Try it yourself:

```
print('Enter Your Name: ')
name = input()
print(name)
```

Explanation:

The input() function allows user input.

Here you just ask for the name and directly print it.


### 45. Data Aggregates

- CASE: What is the expected output of the following code?

```
x = {(1, 2): 1, (2, 3): 2}
print(x[1, 2])
```

- Solution: 1


- Try it yourself:

```
x = {(1, 2): 1, (2, 3): 2}
print(x[1, 2])    # 1
print(x[(1, 2)])  # 1
```

Explanation:

Yes, a tuple can be the index of a dictionary

And calling it you can (like often) leave out the parentheses.


### 46. Basics

- CASE: What do you call a command-line interpreter which lets you interact

with your OS and execute Python commands and scripts?


- Solution: A console






