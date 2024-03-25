### [Source of this study material : Python Certification Exam PCEP by Cord Mählmann](https://www.udemy.com/course/pcep-certification-python-exam-practice-tests/)


## Exam -3

### 1. Error Handling

- CASE: Select the true statements about the try-except block in relation to the following example.


```
try:
    # Some code is here...
except:
    # Some code is here...
```


- Solution:

- The code that follows the except statement will be executed if the code in the try clause runs into an error.

- If you suspect that a snippet may raise an exception, you should place it in the try block.

- If there is a syntax error in code located in the try block, the except branch will not handle it, and a SyntaxError exception will be raised instead.


- The exception handling will not catch a syntax error.

A syntax error will directly end the script.



### 2. Basics

- CASE: Select the true statements?


- Solution:

- Python is a good choice for creating and executing tests for applications.

- Python is free, open-source, and multiplatform.


- Fortunately, Python is free.

Python is open-source,

so anyone can contribute to its development.

Python may be easily ported and migrated to all platforms

with the ability to compile and run "C" language programs

(virtually all platforms have this feature,

which opens up many expansion opportunities for Python).

Lots of IT project testers have started using

Python to carry out repeatable test procedures.



### 3. Functions

- CASE: What is the expected output of the following code?


```
def func(item):
    item += [1]
 
 
data = [1, 2, 3, 4]
func(data)
print(len(data))
```


- Solution: 5


- Try it yourself:


```
def func(item):
    item += [1]   # [1, 2, 3, 4] + [1] -> [1, 2, 3, 4, 1]
 
 
data = [1, 2, 3, 4]
func(data)
print(len(data))  # 5
 
print(data)       # [1, 2, 3, 4, 1]
x = [1, 2, 3, 4]
x.append([1])
print(x)          # [1, 2, 3, 4, [1]]
```


- Inside the function a list concatenation by plus operator takes place.

The plus operator merges the elements of the second list into the first list.

append() would insert the list itself into the other list.



### 4. Data Types

- CASE: Consider the following python code:


```
x1 = '23'
y1 = 7
z1 = x1 * y1
 
x2 = 42
y2 = 7
z2 = x2 / y2
 
x3 = 4.7
y3 = 1
z3 = x3 / y3
```


What are the data types of the variables z1, z2 and z3?


- Solution: str, float, float


- First the string 23 will be multiplied by 7

Second the integer 42 is divided by the integer 7

The result is the float 6.0

Remember the division operator always returns a float

Third the float 4.7 is divided by the integer 1

and surely the result is the float 4.7



### 5. Basics

- CASE: The folder created by Python used to store pyc files is named:


- Solution: __pycache__


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

Inside the folder should be a file like functions.cpython-39.pyc

You can always delete the folder __pycache__

It will be created again the next time you run index.py



### 6. Control Flow

- CASE: What is the expected output of the following code?


```
print(len([i for i in range(0, -2)]))
```


- Try it yourself:


```
print(len([i for i in range(0, -2)]))      # 0
 
# Those make more sense:
print(len([i for i in range(-2, 0)]))      # 2
print(len([i for i in range(0, -2, -1)]))  # 2
```


Explanation:

The "problem" here is the range(0, -2)

The start value 0 has to be lower than the end value -2

Otherwise range() does not return an element.



### 7. Data Aggregates

- CASE: How many elements does the L list contain?


```
L = [i for i in range(-1, -2)]
```


- Solution: 1


Try it yourself:


```
L = [i for i in range(-1, -2)]
print(L)       # []
print(len(L))  # 0
```


Explanation:

range(-1, -2) has no element

and therefore the list L will be empty.



### 8. Operators

- CASE: Which of the following code snippets will print True to the monitor?


- Solution:


```
print('is' in 'This IS Python code.')
```


```
print('t' in 'Peter')
```


- Try it yourself:


```
print('is' in 'This IS Python code.')  # True
 
print('t' in 'Peter')                  # True
 
x = 42
y = 42
print(x is not y)                      # False
 
x = 'Peter Wellert'
y = 'Peter Wellert'.lower()
print(x is y)                          # False
x = 'Peter Wellert'
y = 'Peter Wellert'
print(x is y)                          # True
 
x = ['Peter', 'Paul', 'Mary']
y = ['Peter', 'Paul', 'Mary']
print(x is y)                          # False
print(x == y)                          # True
```


Explanation:

The membership operator works very good with strings.

It looks for a string in a string.

The identity operator with immutable data types (here int and string):

The 42 in x and y will reference to the same object.

Therefore they have the same identity

and the not identity operator will evaluate to False

One string will be changed by lower() to peter wellert

and therefore they will not have the same identity.

The identity operator with mutable data types (here list):

A new list will be a new object even if the values are the same.

Therefore they will not have the same identity.

But they will have the same values,

which you can check with the equal to operator



### 9. Data Aggregates

- CASE: What is the output of the following snippet?


```
my_list = [3, 1, -2]
print(my_list[my_list[-1]])
```


Solution: 1


- Explanation:

The index -1 represents the last element -2

The index -2 represents the second last element 1



### 10. Control Flow

- CASE: How many stars will the following snippet print to the monitor?


```
x = 16

while x > 0:

    print('*')

    x //= 2

```


- Solution: five


- After each printing a floor division by 2 takes place.

And 1 // 2 is 0 and that's where the while loop ends.



### 11. Data Types

- CASE: You are an intern for ABC electric cars company.

You must create a function that calculates the average velocity

of their vehicles on a 1320 foot (1/4 mile) track.

Consider the following code.


```
distance = ???(input('Enter the distance travelled in feet'))
distance_miles = distance/5280  # convert to miles
 
time = ???(input('Enter the time elapsed in seconds'))
time_hours = time/3600  # convert to hours
 
velocity = distance_miles/time_hours
print('The average Velocity : ', velocity, 'miles/hour')
```


The output must be as precise as possible.

What would you insert instead of ??? and ???



- Solution: 


```
float
float
```


- To be as precise as possible means,

that you do not want to loose the numbers after the decimal point,

if they are given by the user.

Therefore you need float() for both inputs.

Assuming the user enters a float

the function int() would raise a ValueError anyway.



### 12. Functions

- CASE: Select the true statement:


- Solution: Keyword arguments cannot be followed by positional arguments.


```
def my_function(a=23, b=42):
    print(a, b)
 
 
# my_function(a=11, 17)
# SyntaxError: positional argument follows keyword argument
```


- If a positional argument follows a keyword argument

you directly get a syntax error.



### 13. Control Flow

- CASE: What is the expected output of the following code?


```
data = [1, {}, (2,), (), {3}, [4, 5]]
points = 0
 
for i in range(len(data)):
    if type(data[i]) == list:
        points += 1
    elif type(data[i]) == tuple:
        points += 10
    elif type(data[i]) == set:
        points += 100
    elif type(data[i]) == dict:
        points += 1000
    else:
        points += 10000
 
print(points)
```


- Solution: 11121


- Every element of data gets tested in the for loop.

There is one integer, which executes the else clause.

There is one dictionary: {}

There is one set: {3}

There are two tuples: (2,) and ()

There is one list: [4, 5]



### 14. Functions

- CASE: Which of the following function definition does not return any value?


- Solution: A function that prints integers from 1 to 100.


- Try it yourself:


```
# A function that prints integers from 1 to 100:
def f1():
    for i in range(1, 101):
        print(i)
 
 
print(f1())  # None
# Not to return a value means to return "None"
 
 
# A function that returns a random integer from 1 to 100:
def f2():
    from random import randint
    return randint(1, 100)
 
 
print(f2())  # e.g. 87
# It returns the random number.
 
 
# A function that converts an uppercase letter to lowercase:
def f3(s):
    return s.lower()
 
 
print(f3('X'))  # x
# This function would return the lower letter
```

Explanation:

The function f1() does not have the return keyword.

Therefore it would return None

Every function, that does not return anything, returns None



### 15. Control Flow

- CASE: What is the expected output of the following code?


```
my_list = [[3-i for i in range(3)] for j in range(3)]
result = 0
 
for i in range(3):
    result += my_list[i][i]
 
print(result)
```


- Solution: 6


- The list comprehension produces a two-dimensional list.

The three elements of the outer list also each have three elements:

the numbers 3, 2, 1

The for loop will add together

the first element of the first list 3

the second element of the second list 2

and the third element of the third list 1

3 + 2 + 1 -> 6


### 16. Data Aggregates

- CASE: What is the expected output of the following code?


```
data = {'a': 1, 'b': 2, 'c': 3}
print(data['a', 'b'])
```


- Solution: The code is erroneous.


- Try it yourself:


```
data = {'x': 1, 'y': 2, 'z': 3}
print(data['x', 'y'])        # KeyError: ('x', 'y')
 
print(data['x'], data['y'])  # 1 2
 
data = {('x', 'y'): 1}
print(data['x', 'y'])        # 1
```


Explanation:

You can have a tuple as key of a dictionary

but that is not given here.



### 17. Basics

- CASE: By which variable of the sys module can we access command line arguments?


- Solution: argv


- Try it yourself:


```
import sys
print(sys.argv[0])  # The first index is the name of the file
 
# Now execute the following to create the needed file:
code = '''
import sys
for a in sys.argv[1:]:
    print(a)
'''
with open('argv.py', 'w') as f:
    f.write(code)
 
# In Terminal:
# python argv.py Peter Paul Mary
 
"""
Peter
Paul
Mary
"""
```


Explanation:

sys.argv[1:] slices everything except the first index with holds the filename.

You have to open the folder where you created the argv.py file in a terminal

and run the file by python argv.py Peter Paul Mary

The "v" in argv stands for vector.



### 18. Functions

- CASE: The meaning of the keyword parameter is determined by:


- Solution: the argument's name specified along with its value.


- Try it yourself/Explanation:


```
def my_function(b=7, a=11):
    print(a, b)
 
 
# The argument's name determines the keyword parameter:
my_function(b=1, a=2)  # 2 1
 
# With keyword parameters the values do not matter:
my_function(11, 7)  # 7 11
 
# With keyword parameters the position
# within the argument list does not matter:
my_function(a=1, b=2)  # 1 2
 
# Keyword parameters do not connect with existing variables:
a = 23; b = 42
my_function(a, b)  # 42 23
```


### 19. Data Aggregates

- CASE: What is the expected output of the following code?


```
data = ()
print(data.__len__())
```


- Try it yourself:


```
data = ()
print(data.__len__())  # 0
print(len(data))       # 0
 
print(type(data))      # <class 'tuple'>
```


Explanation:

Every object has the method __len__()

Normally we use the function len() which calls the method __len__()

And sure, the length of an empty tuple is 0



### 20. Data Aggregates

- CASE: Take a look at the snippet

and choose one of the following statements which is true:


```
nums = []
vals = nums
vals.append(1)
```


- Solution: nums and vals are of the same length.


- y it yourself:

```
nums = []
vals = nums
vals.append(1)
print(nums)  # [1]
print(vals)  # [1]
```


Explanation:

A list is a mutable data type.

Assigning a mutable data type creates a reference to the same object.

vals and nums will point to the same object in the memory

and when you change one you automatically change the other, too.



### 21. Operators

- CASE: What is the expected output of the following code?


```
x = 4.5

y = 2

print(x // y)
```


- Solution: 2.0


- Try it yourself:


```
print(4.5 // 2)    # 2.0
print(4.5 // 2.0)  # 2.0
print(4 // 2.0)    # 2.0
print(4 // 2)      # 2
```


Explanation:

If one operand is a float, the floor division operator returns a float.

Only if both operands are an integer,

the floor division operator returns an integer.



### 22. Control Flow

- CASE: How many stars will the following snippet print to the monitor?


```
data = [[x for x in range(y)] for y in range(3)]
 
for d in data:
    if len(d) < 2:
        print('*')
```


- Solution: two


```
data = [[x for x in range(y)] for y in range(3)]
print(data)         # [[], [0], [0, 1]]
 
for d in data:
    print('d:', d)  # [] -> [0] -> [0, 1]
    if len(d) < 2:
        print('*')  # * *
```


- The list comprehension produces a two-dimensional list.

The outer list has three elements.

Each of which is as long as its index: [], [0] and [0, 1]

The if in the for loop checks that length.

Two of the three are smaller than 2 and therefore two stars are printed.



### 23. Functions

- CASE: What is the output of the following snippet?


```
def func(x, y):
    if x == y:
        return x
    else:
        return func(x, y-1)
 
 
print(func(0, 3))
```


- Solution: 0


- This is a recursive function gone wrong.

If the recursive function call would be added to y

the result would be 3 + 2 + 1 -> 6

But here, in the end the function just returns x which is 0



### 24. Data Types

- CASE: What is the expected output of the following code?


```
print(type(1J))
```

- Solution: <type 'complex'>


- Try it yourself:

```
print(type(1J))      # <class 'complex'>
 
c = 1j
print(c.real)        # 0.0
print(c.imag)        # 1.0
print(type(0 + 1j))  # <class 'complex'>
```


Explanation:

You can use J or j for complex numbers.

1j is a complex number where the real part is 0 and the imaginary part is 1



### 25. Basics

- CASE: What is source code?


- Solution: A program written in a high-level programming language.


- A program written in a high-level programming language

is called a source code (in contrast to the machine code executed by computers).

Similarly, the file containing the source code is called the source file,

or source code file.



### 26. Data Aggregates

- CASE: An alternative name for a data structure called a stack is:


- Solution: LIFO


- Try it yourself:

```
x = []
x.append(1)
x.append(2)
x.append(3)
print(x.pop())  # 3
print(x.pop())  # 2
print(x.pop())  # 1
```


Explanation:

LIFO stands for Last-In-First-Out.

Here you find a great explanation:



### 27. Data Aggregates

- CASE: What is the expected output of the following code?


```
nums = [1, 2, 3]
data = ('Peter',) * (len(nums) - nums[::-1][0])
print(data)
```

- Solution: ()


- Try it yourself:


```
nums = [1, 2, 3]
data = ('Peter',) * (len(nums) - nums[::-1][0])
print(data)  # ()
 
print(len(nums) - nums[::-1][0])            # 0
print(len([1, 2, 3]) - [1, 2, 3][::-1][0])  # 0
print(3 - [3, 2, 1][0])                     # 0
print(3 - 3)                                # 0
print(0)                                    # 0
 
print(('Peter',))        # ('Peter',)
print(type(('Peter',)))  # <class 'tuple'>
print(type('Peter'))     # <class 'str'>
print(('Peter',) * 0)    # ()
print((1, 2, 3) * 0)     # ()
```


- The length of nums is 3

[::-1] reverses the list and then 3 is the first index.

3 minus 3 makes 0

The trailing comma marks the tuple with one element.

Otherwise it would be a string with additional parentheses.

Any tuple multiplied by 0 becomes an empty tuple.



### 28. Data Types

- CASE: What is the expected output of the following code?


```
print(ord('c') – ord('a'))
```


- Solution: 2


- Try it yourself:

```
print(ord('c') - ord('a'))  # 2
print(ord('c'))             # 99
print(ord('a'))             # 97
```


Explanation:

ord() returns an integer representing the Unicode character.

You do not need to remember the number of each character,

but like in the alphabet c is two after a


### 28. Data Aggregates

- CASE: What is the expected output of the following code?


```
w = [7, 3, 23, 42]
x = w[1:]
y = w[1:]
z = w
y[0] = 10
z[1] = 20
print(w)
```


- Solution: [7, 20, 23, 42]


- Try it yourself:

```
w = [7, 3, 23, 42]
x = w[1:]  # [3, 23, 42]
y = w[1:]  # [3, 23, 42]
z = w      # A reference
print(z)   # [7, 3, 23, 42]
y[0] = 10  # Changes only y
z[1] = 20  # Changes z and w
print(w)   # [7, 20, 23, 42]
 
print(id(x))  # e.g. 140539383900864
print(id(y))  # e.g. 140539383947456 (a different number)
print(id(w))  # e.g. 140539652049216 (the same number than z)
print(id(z))  # e.g. 140539652049216 (the same number than w)
```


Explanation:

The two list slicings create new lists.

Therefore the change of y does not effect w

The assigning of the list creates a reference to the same object

Therefore the change of z does also effect w



### 29. Operators

- CASE: What is the expected output of the following code if the user enters 2 and 4?


```
x = float(input())
y = float(input())
print(y ** (1 / x))
```


- Solution: 2.0


- Try it yourself:

```
# x = float(input())
# y = float(input())
x, y = float('2'), float('4')  # Just for convenience
print(y ** (1 / x))    # 2.0
print(4.0 ** (1 / 2))  # 2.0
print(4.0 ** 0.5)      # 2.0
import math
print(math.sqrt(4))    # 2.0
```


Explanation:

As always input() returns a string

They both get casted to a float

Here you need a little bit of mathematical knowledge.

You can take the square root of a number by raising it to the power of 0.5



### 30. Operators

- CASE: Right-sided binding means that the following expression


```
1 ** 2 ** 3
```

will be evaluated:


- Solution: from right to left


Try it yourself:

```
print(1 ** 2 ** 3)    # 1
print(1 ** (2 ** 3))  # 1
print(1 ** 8)         # 1
print(1)              # 1
```


### 31. Data Aggregates

- CASE: What is the output of the following snippet?


```
my_list = [0, 1, 2, 3]
x = 1
for elem in my_list:
    x *= elem
print(x)
```


- Solution: 0


```
my_list = [0, 1, 2, 3]
x = 1
for elem in my_list:
    x *= elem
print(x)                  # 0
print(1 * 0 * 1 * 2 * 3)  # 0
```


- If you multiply by zero, the result is zero

and you can keep multiplying as long as you want with other numbers.

The result will stay zero.



### 32. Basics

- CASE: UNICODE is a standard:


- Solution: like ASCII, but much more expansive.



### 33. Control Flow

- CASE: The ABC company is creating a program

that allows customers to log the number of miles biked.

The program will send messages based on how many miles the customer logs.

You create the following Python code.


```
???
    name = input('What is your name? ')
    return name
 
 
???
    calories = miles * calories_per_mile
    return calories
 
 
distance = int(input('How many miles did you bike this week? '))
burn_rate = 50
biker = get_name()
calories_burned = calc_calories(distance, burn_rate)
print(biker + ', you burned about', calories_burned, 'calories.')
```

What would you insert instead of ??? and ???


- Solution: 


- def calc_calories(miles, calories_per_mile):

- def get_name():


- biker = get_name() calls get_name() without any arguments

and therefore you can not have any parameters:

def get_name():

calories_burned = calc_calories(distance, burn_rate)

calls calc_calories() with two arguments

and therefore you need two parameters:

def calc_calories(miles, calories_per_mile):



### 34. Data Aggregates

- CASE: What is the expected output of the following code?


```
data = (1, 2, 4, 8)
data = data[1:-1]
data = data[0]
print(data)
```


- Solution: 2


- Try it yourself:

```
data = (1, 2, 4, 8)
data = data[1:-1]
print(data)          # (2, 4)
data = data[0]
print(data)          # 2
```


Explanation:

The start of the slicing is index 1 (inclusive)

and the end is the last index -1 (exclusive).

That would be the numbers 2, 4

The first one of those is the 2



### 35. Control Flow

- CASE: How many elements will the following list contain?


```
data = [i for i in range(-1, 2)]
```

- Solution: three


- Try it yourself:


```
data = [i for i in range(-1, 2)]
 
print(data)                # [-1, 0, 1]
print(len(data))           # 3
 
print(list(range(-1, 2)))  # [-1, 0, 1]
```


### 36. Data Aggregates

- CASE: What is the expected output of the following code?


```
data = (1,) * 3
data[0] = 2
print(data)
```

- Solution: The code is erroneous.


- Try it yourself:

```
data = (1,) * 3
data[0] = 2  # TypeError: ...
print(data)
```

Explanation:

A tuple is immutable. You can not change it.

Therefore you can not assign something to one of its indexes.



### 37. Data Types

- CASE: The most important difference between integer and floating-point numbers lies in the fact that:


- Solution: They are stored differently in the computer memory.



### 38. Data Types

- CASE: You want to print each name of the list on a new line.


```
data = ['Peter', 'Paul', 'Mary', 'Jane']
```


Which statement will you use?



- Solution: print('\n'.join(data))


- Try it yourself:

```
data = ['Peter', 'Paul', 'Mary', 'Jane']
print('\n'.join(data))
 
"""
Peter
Paul
Mary
Jane
"""
 
# print(data.join('\n'))           # AttributeError: ...
# print(data.concatenate('\n'))    # AttributeError: ...
# print(data.join('%s\n', names))  # AttributeError: ...
```


- join() is a string method.

The string is the separator

and the list (or any other iterable) is passed as argument.

The elements of the list will then be joined into a string

using the original string as separator.



### 39. Operators

- CASE: What value will be assigned to the x variable?


```
z = 2
y = 1
x = y < z or z > y and y > z or z < y
```


- Solution: True


- The operators here are from three different groups.

"Comparisons, Identity, Membership operators", "Logical AND", "Logical OR".

The two comparison operators,

greater than operator and less than operator have the highest precedence.

Then the logical **and** operator has a higher precedence

than the logical **or** operators


```
z = 7
y = 3
x = y < z or z > y and y > z or z < y
print(x)                                  # True
print(y < z or z > y and y > z or z < y)  # True
print(3 < 7 or 7 > 3 and 3 > 7 or 7 < 3)  # True
print(True or True and False or False)    # True
print(True or (True and False) or False)  # True
print(True or False or False)             # True
print((True or False) or False)           # True
print(True or False)                      # True
print(True)                               # True
```


### 40. Data Types

- CASE: What is the result of the following code?


```
x = (3, )
print(len(x))
```


- Solution: 1


- A tuple with only one value needs a tailing comma to distinguish it

from a single value (e.g. an integer) in parentheses.



### 41. Basics

- CASE: You have the following file.

index.py:


```
from sys import argv
print(argv[0])
```

You run the file by executing the following command in the terminal.


```
python index.py Hello
```


What is the expected oputput?


- Solution: index.py


- Try it yourself:


```
# First execute the following to create the needed file:
code = '''
from sys import argv
print(argv[0])
'''
with open('index.py', 'w') as f:
    f.write(code)
 
# In Terminal:
# python index.py Hello
"""
index.py
"""
```


Explanation:

You have to open the folder where you created the index.py file in a terminal

and run the file by executing python index.py Hello

The first index (the index 0) of the argv variable is always the filename.

If you want Hello to be the output, you have to write print(argv[1])


### 42. Functions

- CASE: What is the output of the following snippet?


```
def any():
    print(var + 1, end='')
 
 
var = 1
any()
print(var)
```

- Solution: 21


- The variable var shadows inside the function and is readable there.

Therefore, 2 is printed within the function.

After that the value of the variable var is printed, which is 1


### 43. Operators

- CASE: What is the expected output of the following code?


```
x = 0
y = 1
x = x ^ y
y = x ^ y
y = x ^ y
print(x, y)
```


- Solution: 1 1


- Try it yourself:

```
x = 0
y = 1
print(x, y)   # 0 1
x = x ^ y
print(x, y)   # 1 1
y = x ^ y
print(x, y)   # 1 0
y = x ^ y
print(x, y)   # 1 1
 
print(1 ^ 1)  # 0
print(1 ^ 0)  # 1
print(0 ^ 1)  # 1
print(0 ^ 0)  # 0
```

Explanation:

The bitwise xor operator returns 1 when one operand is 1 and the other is 0

When both operands are 0 or both operands are 1 it returns 0



### 44. Operators

- CASE: What is the expected output of the following code?


```
print(2 ** 3 ** 2 ** 1)
```


- Solution: 512


- Try it yourself:

```
print(2 ** 3 ** 2 ** 1)    # 512
print(2 ** 3 ** (2 ** 1))  # 512
print(2 ** 3 ** 2)         # 512
print(2 ** (3 ** 2))       # 512
print(2 ** 9)              # 512
print(512)                 # 512
```

Explanation:

This question is about associativity of operators

Most operators have the associativity from left to right.

That means if you have two operators that are the same

or of the same group the left one is executed first.

The exponentiation operator has an associativity from right to left

therefore the right one is executed first.

Just picture the expression on a piece of paper with your handwriting

where you write each exponent a little bit higher than its base.

Naturally you have to start at the top to resolve the expression.


### 45. Functions

- CASE: A function parameter is a kind of variable accessible:


- Solution: only inside the function


- Try it yourself:

```
def my_function(text):
    print(text)  # Hello
 
 
my_function('Hello')
print(text)  # NameError: name 'text' is not defined
```

Explanation:

Yes, a function parameter is only accessible inside the function.


### 46. Functions

- CASE: What is the expected output of the following code?


```
def test(x=1, y=2):
    x = x + y
    y += 1
    print(x, y)
 
 
test()
```


- Solution: 3 3


### 47. Data Aggregates

- CASE: What is the expected output of the following code?


```
fruits1 = ['Apple', 'Pear', 'Banana']
fruits2 = fruits1
fruits3 = fruits1[:]
 
fruits2[0] = 'Cherry'
fruits3[1] = 'Orange'
 
res = 0
 
for i in (fruits1, fruits2, fruits3):
    if i[0] == 'Cherry':
        res += 1
    if i[1] == 'Orange':
        res += 10
 
print(res)
```


- Solution: 12


- A list is a mutable data type.

Assigning it will create a reference.

Slicing it from start to end [:] will create a copy.

Therefore  Cherry goes in fruits2 and thereby also in fruits1

Orange only goes in fruits3



### 48. Functions

- CASE: What is the expected output of the following code?


```
def func(x):
    global y
    y = x * x
    return y
 
 
func(2)
print(y)

```

- Solution: 4


- The global keyword can be used to read

and write a global variable inside of a function.

Once you write global y then y also exists in the outer scope.

You would not need the return here.

It is of no use, because the return value of func(2)

does not get processed any further.

But still you can print y because y is global


### 49. Error Handling

- CASE: What is the expected behavior of the following program?


```
foo = (1, 2, 3)
foo.index(0)
```


- Solution: The program will cause a ValueError exception.


```
foo = (1, 2, 3)
foo.index(0)
# ValueError: tuple.index(x): x not in tuple
```

- The tuple.index() method expects a value

and looks for that value in the tuple.

It will return the index of the first value it finds.

If it does not find the value, it raises a ValueError


### 50. Error Handling

- CASE: What is the expected output of the following code?


```
x = True
y = False
z = False
 
if x or y and z:
    print('TRUE')
else:
    print('FALSE')
```


- Solution: TRUE


- The one important thing here is, that the logical and operator

has a higher precedence than the logical or operator





