### [Source of this study material : Python Certification Exam PCEP by Cord Mählmann](https://www.udemy.com/course/pcep-certification-python-exam-practice-tests/)


## Exam -1 

### 1. Error Handling

- CASE: What will happen when you attempt to run the following code?

```
print(Hello, World!)
```


- Solution: The code will raise the **SyntaxError** exception.


- The exclamation mark makes it a syntax error.



### 2. Control Flow

- CASE: What is the expected output of the following code?


```
x = True
y = False
z = False
 
if not x or y:
    print(1)
elif not x or not y and z:
    print(2)
elif not x or y or not y and x:
    print(3)
else:
    print(4)
```


- Solution: 3


- There are three operators at work here. The **not** operator has the highest precedence, followed by the **and** operator. The **or** operator has the lowest precedence.



### 3. Functions

- CASE: What is the expected output of the following code?


```
num = 1
 
def func():
    num = num + 3
    print(num)
 
func()
 
print(num)
```


- A variable name shadows into a function. You can use it in an expression like **x = num + 3** or you can assign a new value to it like in **num = 3** but you CANNOT do both at the same time like in **num = num +3**. There is going to be the new variable **num** and you cannot use it in an expression before its first assignment.



### 4. Data Aggregates

- CASE: What is the expected output of the following code?


```
x = [0, 1, 2]
x.insert(0, 1)
del x[1]
print(sum(x))
```


- Solution: 4


- insert() iserts an item at a given position. 


```
list.insert(i, x)
```


- The first argument is the index of the element before which to insert. insert(0, 1) inserts 1 before index 0 (at the front of the list). 



### 5. Data Aggregates

- CASE: Assuming that the tuple is a correctly created tuple,

the fact that tuples are immutable means that the following instruction:



- Solution: is illegal.


- A tuple is immutable and therefore you cannot assign a new value to one of its indexes.


```
my_tuple = (1, 2, 3)
my_tuple[1] = my_tuple[1] + my_tuple[0]
# TypeError: 'tuple' object does not support item assignment
```


### 6. Operators

- CASE: What will be the output of the following code snippet?


```
x = 2
y = 1
x *= y + 1
print(x)
```


- Solution: 4


- The operator precedence of the **addition operator** is higher than the operator precedence of the **multiply and assign operator**. That means the addition takes place before the multiplication.



### 7. Functions

- CASE: Which of the following lines correctly invoke the function defined below:


```
def fun(a, b, c=0):
    # Body of the function.
```


- Solution: func(0, 1, 2) and func(b=0, a=0)


```
def fun(a, b, c=0):
    # Body of the function.
    pass
 
 
fun(b=0, a=0)
fun(0, 1, 2)
# fun()     # TypeError: fun() missing 2 required
            # positional arguments: 'a' and 'b'
# fun(b=1)  # TypeError: fun() missing 1 required
            # positional argument: 'a'

```


- Only the parameter c has a default value. Therefore, you need at least 2 arguments.



### 8. Functions

- CASE: What is the expected output of the following code?


```
def func(num):
    res = '*'
    for _ in range(num):
        res += res
    return res
 
 
for x in func(2):
    print(x, end='')
```


- Solution: ****


- The **for** loop inside of the function will iterate twice. The for loop outside of the function will just iterate through the string and print every single star.



### 9. Functions

- CASE: What is the default return value for a function

that does not explicitly return any value?


- Solution: None


```
def func1():
    pass
print(func1())  # None

def func2():
    return
print(func2())  # None
```


- If a function does not have the keyword **return**, the function will return the value **None**. The same happens if there is no value after the keyword **return**.



### 10. Functions

- CASE: If a list passed into a function as an argument,

deleting any of its elements inside the function using the del instruction:


- Solution: will affect the argument.


```
my_list = [1, 2, 3]
 
 
def delete_first(x):
    del x[0]
 
 
delete_first(my_list)
print(my_list)  # [2, 3]
```


- A list is a mutable data type and it is pass by reference to a function. Meaning that the list inside of the function and the list outside of the function will point to the same object in the memory. If you change the list inside of the function, that will change the list outside of the function in the same way.



### 11. Operators

- CASE: What is the expected output of the following code?


```
x = 28

y = 8

print(x / y)

print(x // y)

print(x % y)
```


- Solution: 


```
3.5
3
4
```


### 12. Basics

- CASE: What is CPython?


- Solution: It's a default, reference implementation of the Python language, written in C.


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



### 13. Functions

- CASE: isalnum() checks if a string contains only letters and digits, and this is:


- Solution: A method


```
print('James007'.isalnum())     # True
print('Hello world'.isalnum())  # False
```


- isalnum() is a String-Method. 'Hello world' is not alphanumeric, because of the space character.



### 14. Basics

- CASE: What are the four fundamental elements that make a language?


- Solution: An alphabet, a lexis, a syntax, and semantics


- We can say that each language (machine or natural, it doesn't matter)

consists of the following elements:



An alphabet:

a set of symbols used to build words of a certain language

(e.g., the Latin alphabet for English,

the Cyrillic alphabet for Russian, Kanji for Japanese, and so on)



A lexis:

(aka a dictionary) a set of words the language offers its users

(e.g., the word "computer" comes from the English language dictionary,

while "cmoptrue" doesn't;

the word "chat" is present both in English and French dictionaries,

but their meanings are different)



A syntax:

a set of rules (formal or informal, written or felt intuitively)

used to determine if a certain string of words forms a valid sentence

(e.g., "I am a python" is a syntactically correct phrase, while "I a python am" isn't)



Semantics:

a set of rules determining if a certain phrase makes sense

(e.g., "I ate a doughnut" makes sense, but "A doughnut ate me" doesn't)



### 15. Data Aggregates

- CASE: What will be the output of the following code snippet?


```
a = [1, 2, 3, 4, 5, 6, 7, 8, 9]
print(a[::2])
```


- Solution: [1, 3, 5, 7, 9]


- Try it yourself:


```
a = [1, 2, 3, 4, 5, 6, 7, 8, 9]
print(a[::2])  # [1, 3, 5, 7, 9]
```

List slicing: [start(inclusive):end(exclusive):step]

The start and end values are missing here.

If you leave them out, you will slice from the beginning to the end.

If you leave the end out it will also be inclusive.

The third value (the step) is 2 therefore every second element gets taken.



### 16. Control Flow

- CASE: What is the expected output of the following code?


```
def func(text, num):
    while num > 0:
        print(text)
    num = num - 1
 
func('Hello', 3)

```


- Solution: An infinite loop.


- The incrementation of num needs to be inside of the while loop.

Otherwise the condition num > 0 will never be False

It should look like this:


```
def func(text, num):
    while num > 0:
        print(text)
        num = num - 1
func('Hello', 3)
"""
Hello
Hello
Hello
"""
```


### 17. Operators

- CASE: What is the expected output of the following code?


```
x = 1 / 2 + 3 // 3 + 4 ** 2

print(x)
```


- Solution: 17.5


- Explanation:

The operators here come from three different groups:

"Exponent" has the highest precedence.

Followed by "Multiplication, Division, Floor division, Modulus".

"Addition, Subtraction" has the lowest precedence.

Therefore the order of operations here is: ** -> / -> // -> + -> +



### 18. Operators

- CASE: What will be the output of the following code snippet?


```
print(3 / 5)
```


Solution: 0.6


- The division operator does its normal job.

And remember the division operator ALWAYS returns a float.



### 19. Functions

- CASE: What is the expected output of the following code? 


```
def func(data):
    for d in data[::2]:
        yield d
 
for x in func('abcdef'):
    print(x, end='')
```


Solution: ace


- The generator function will return every second element of the passed data.



### 20. Basics

- CASE: Which of the following variable names is illegal?


- Solution: in


Try it yourself:


```
# in = 'Hello'  # SyntaxError: invalid syntax
# Does not work because "in" is a python keyword
# for the membership operator:
print(7 in [1, 4, 7, 11])  # True
 
# Those work because python is case sensitive
In = 'Hello'
IN = 'Hello'
 
# This one works because the underscore
# is a valid character for naming variables:
in_ = 'Hello'
```

Explanation:

You can not name a variable like a Python keyword.

Here is a list of all the Python keywords:

import keyword
print(keyword.kwlist)
"""
['False', 'None', 'True', 'and', 'as', 'assert', 'async',
'await', 'break', 'class', 'continue', 'def', 'del', 'elif',
'else', 'except', 'finally', 'for', 'from', 'global', 'if',
'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or',
'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']
"""
Here are the other rules for naming variables in Python:

A variable name must start with a letter or the underscore character.

A variable name can not start with a number.

A variable name can only contain alpha-numeric characters

and underscores (a-z, 0-9, and _)

Variable names are case-sensitive

(age, Age and AGE are three different variables)



### 21. Control Flow

- CASE: What is the expected output of the following code?


```
x = 1
 
if x > 0 or x < 1:
    print("1")
if x > 1:
    print("2")
elif x >= 1:
    print("3")
else:
    print("4")
```


- Solution:


```
1
3
```


- Try it yourself:

```
x = 1
 
if x > 0 or x < 1:
    print("1")  # 1
if x > 1:
    print("2")
elif x >= 1:
    print("3")  # 3
else:
    print("4")
```

Explanation:

1 is greater than 0 and therefore the condition

of the first if evaluates to True and 1 is printed.

1 is greater than or equal to 1 and therefore the condition

of the elif also evaluates to True and 3 is also printed.



### 22. Operators

- CASE: What value will be assigned to the x variable?


```
z = 3
y = 7
x = y < z and z > y or y > z and z < y
```


- Solution: True


- Try it yourself:


```
z = 3
y = 7
x = y < z and z > y or y > z and z < y
print(x)                                     # True
 
print(y < z and z > y or y > z and z < y)    # True
print(7 < 3 and 3 > 7 or 7 > 3 and 3 < 7)    # True
print(False and False or True and True)      # True
print((False and False) or (True and True))  # True
print(False or True)                         # True
print(True)                                  # True
```


Explanation:

The operators here are from three different groups.

"Comparisons, Identity, Membership operators", "Logical AND", "Logical OR".

The two comparison operators

the greater than operator and the less than operator

have the highest precedence.

Then the logical and operator has a higher precedence

than the logical or operator



### 23. Data Aggregates

- CASE: Take a look at the snippet, and choose the true statements:


```
nums = [1, 2, 3]
vals = nums
del vals[1:2]
```


- Solution: 


- nums and vals refer to the same list.

- nus and vals are of the same length.


- A list is a mutable data type.

Assigning a mutable data type creates a reference to the same object.

vals and nums will point to the same object in the memory

and when you change one you automatically change the other, too.



### 24. Control Flow

- CASE: What is the expected output of the following code?


```
x = [[[1, 2], [3, 4]], [[5, 6], [7, 8]]]
 
def func(data):
    res = data[0][0]
    for da in data:
        for d in da:
            if res < d:
                res = d
    return res
 
print(func(x[0]))
```


- Solution: 4


- Try it yourself:


```
x = [[[1, 2], [3, 4]], [[5, 6], [7, 8]]]
 
def func(data):
    print('data:', data)    # [[1, 2], [3, 4]]
    res = data[0][0]        # 1
    print('res:', res)
    for da in data:
        print('da:', da)    # [1, 2] -> [3, 4]
        for d in da:
            print('d:', d)  # 1 -> 2 -> 3 -> 4
            if res < d:
                res = d
    return res
 
print(func(x[0]))              # 4
 
print(func([[1, 7], [3, 4]]))  # 7
```


Explanation:

This function looks for the highest element

in a two dimensional list (or another iterable).

In the beginning the first number data[0][0] gets taken as possible result.

In the inner for loop every number is compared to the possible result.

If one number is higher it becomes the new possible result.

And in the end the result is the highest number.




### 25. Data Aggregates

- CASE: What is the expected output of the following code?


```
nums = [3, 4, 5, 20, 5, 25, 1, 3]
nums.pop(1)
print(nums)
```


- Solution: [3, 5, 20, 5, 25, 1, 3]


- list.pop([i])

The index is optional.

If the index is given, pop() removes and returns

the element at the given index.

The default index is -1

Meaning that the last index is removed and returned.

Here the index 1 gets removed: the number 4



### 26. Data Types

- CASE: Consider the following code snippet:


```
w = bool(23)
x = bool('')
y = bool(' ')
z = bool([False])
```

Which of the variables will contain False?


Try it yourself:


```
print(bool(23))       # True
print(bool(''))       # False
print(bool(' '))      # True
print(bool([False]))  # True
```


Explanation:

The list with the value False is not empty and therefore it becomes True

The string with the space also contain one character

and therefore it also becomes True

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


### 27. Control Flow

- CASE: What is the expected output of the following code?


```
def func(x):
    return 1 if x % 2 != 0 else 2
 
print(func(func(1)))
```


- Solution: 1


```
def func(x):
    return 1 if x % 2 != 0 else 2
 
print(func(func(1)))  # 1
 
print(1 % 2)          # 1
print(1 % 2 != 0)     # True
```


- This is a conditional expression.

1 % 2 is 1 and therefore not equal to 0

The condition is True and the inner func() function call returns 1

That 1 is passed to the outer function which will also return 1



### 28. Error Handling

- CASE: What is the expected behavior of the following program?


```
try:
    print(5/0)
    break
except:
    print("Sorry, something went wrong...")
except (ValueError, ZeroDivisionError):
    print("Too bad...")
```


- Solution: The program will cause a **SyntaxError** exception.


```
try:
    print(5/0)
    # break
except:
    print("Sorry, something went wrong...")
# except (ValueError, ZeroDivisionError):
    # print("Too bad...")
```


- There are two syntax errors:

break can not be used outside of a loop,

and the default except must be last.



### 29. Basics

- CASE: What do you call a tool that lets you launch your code

step-by-step and inspect it at each moment of execution?



- Solution: A debugger



### 30. Basics

- CASE: What is the expected output of the following code?


```
x = 1
y = 2
x, y, z = x, x, y
z, y, z = x, y, z
print(x, y, z)
```


- Solution: 1 1 2


We have multiple assignment in Python.

You can assign multiple values to multiple variables.

```
a, b = 3, 7
```

It is just shorter than

```
a = 3
b = 7
```

It does not have practical use, but what also works is

```
c, c = 23, 42
```

First c becomes 23 and then c becomes 42

You better write

```
c = 42
```

The same happens in this question in

```
z, y, z = 1, 1, 2
```

First z becomes 1 and then z becomes 2

You can also assign the same value to multiple variables:

```
a = b = c = d = 1
print(a, b, c, d) # 1 1 1 1
```


### 31. Functions

- CASE: The function body is missing.

What snippet would you insert in the line indicated below:


```
def func(number):
    # insert your code here
 
print(func(7))
```


- Solution: return number


```
def func(number):
    return number      # works and only 7 would be printed
    # print(number)    # works, but 7 & None would be printed
    # print('number')  # works, but number & None would be printed
    # return 'number'  # works, but number would be printed
print(func(7))
```


- The parameter name is number therefore it can not be in quotes.

If you only print something in the function,

the function will return None and that is not wanted here,

because the return values gets already printed outside of the function.



### 32. Functions

- CASE: What is the expected output of the following code?


```
def func(p1, p2):
    p1 = 1
    p2[0] = 42
 
x = 3
y = [1, 2, 3]
 
func(x, y)
 
print(x, y[0])
```


- Solution: 3 42


- This question is about argument passing.

It is a big difference, whether you pass a mutable or an immutable data type.

The immutable integer in x gets copied to p1

and the change of p1 does not effect x

The mutable list in y gets referenced to p2

and the change of p2 effect y



### 33. Functions

- CASE: What is the output of the following code snippet?


```
def test(x=1, y=2):
    x = x + y
    y += 1
    print(x, y)
 
test(2, 1)
```


- Solution: 3 2


```
def test(x=1, y=2):
    x = x + y    # 2 + 1 -> 3
    y += 1       # 1 + 1 -> 2
    print(x, y)  # 3 2
 
test(2, 1)  # 3 2
```


- Okay, both parameters get the default value of the other one,

but for the rest it's business as usual.



### 34. Control Flow

- CASE: The ABC organics company needs a simple program

that their call center will use to enter survey data for a new coffee variety.

The program must accept input

and return the average rating based on a five-star scale.

The output must be rounded to two decimal places.



You need to complete the code to meet the requirements.



```
sum = count = done = 0
average = 0.0
 
while done != -1:
    rating = XXX
    if rating == -1:
        break
    sum += rating
    count += 1
 
average = float(sum / count)
 
YYY + ZZZ
```

- Solution: 


```
XXX -> float(input('Enter next rating (1-5), -1 for done'))
YYY -> print('The average star rating for the new coffee is: ')
ZZZ -> format(average, '.2f'))
```


- The input() function always returns a string

You need to cast that string to a float with the float() function.

The function to print something to the monitor is called print()

And if you want to round a float to two decimal places,

you need the format string '.2f'


```
sum = count = done = 0
average = 0.0
while done != -1:
    rating = float(input('Enter next rating (1-5), -1 for done'))
    if rating == -1:
        break
    sum += rating
    count += 1
 
average = float(sum / count)
print('The average star rating for the new coffee is: '
      + format(average, '.2f'))
 
# format(average, '.2d') -> ValueError: ...
```


### 35. Data Aggregates

- CASE: Insert the correct snippet so that the program produces the expected output.

Expected output:


```
True
```

Code:


```
list = [False, True, "2", 3, 4, 5]
# insert code here
print(b)
```


- Solution: b = 0 in list


- The in operator uses the equal to operator on every element of the list.

The value 0 is not in the list as a literal,

BUT because 0 == False evaluates to True

the False element makes it look like 0 would be in the list.


```
list = [False, True, "2", 3, 4, 5]
b = 0 in list
print(b)  # True
 
# The same without the in operator:
list2 = [False, True, "2", 3, 4, 5]
res = False
for i in list2:
    if i == 0:
        res = True
print(res)  # True
 
print(0 == False)  # True
```


### 36. Data Types

- CASE: What is the expected output of the following code?


```
z = y = x = 1
print(x, y, z, sep='*')
```


- Solution: 1*1*1


- Try it yourself:

```
z = y = x = 1
print(x, y, z, sep='*')  # 1*1*1
print(x, y, z, sep=' ')  # 1 1 1
print(x, y, z)           # 1 1 1
```


Explanation:

The print() function has a sep parameter which stands for separator.

The default value of the sep parameter is a space character.

You can change it to anything you want.



### 37. Operators

- CASE: What is the output of the following code?


```
a = 1
b = 0
x = a or b
y = not(a and b)
print(x + y)
```


- Solution: 2


- If you calculate with a boolean True becomes the integer 1

and therefore 1 + True is 2



### 38. Control Flow

- CASE: Which of the following for loops would output the below number pattern?


```
11111
22222
33333
44444
55555
```


- Solution:


```
for i in range(1,6):
    print(str(i) * 5)
```


- You need range(1, 6)

because the start value 1 is inclusive and the end value 6 is exclusive.

To get the same numbers next to each other

(without a space between them) you need to make a string

and then use the multiply operator string concatenation

The standard separator of the print() function is one space.

print(i, i, i, i, i) gives you one space between each number.

It would work with print(i, i, i, i, i, sep='')

but that answer is not offered here.



### 39. Data Types

- CASE: Strings in Python are delimited with:


- Solution: double quotes(i.e., ") or single quotes(i.e., ')


```
print("Hello")  # Hello
print('World')  # World
```


- Unlike in other programming languages, in Python

double quotes and single quotes are synonyms for each other.

You can use either one or the other.

The result is the same.



### 40. Basics

- CASE: What is the expected output of the following code?


```
x = '\''
print(len(x))
```


- Solution: 1


- The backslash is the character to escape another character.

Here the backslash escapes the following single quote character.

Together they are one character.



### 41. Basics

- CASE: Python is an example of:



- Solution: a high-level programming language.




### 42. Control Flow

- CASE: How many stars will the following snippet print to the monitor?


```
i = 4
while i > 0:
    i -= 2
    print('*')
    if i == 2:
        break
else:
 
    print('*')

```


- Solution: 1


```
i = 4
while i > 0:    # i is 4
    i -= 2      # i is 2
    print('*')  # *
    if i == 2:  # Yip, i is 2
        break   # Leave the loop directly
else:           # Does not apply, because the break got triggered
    print('*')

```


- In the first iteration the break gets directly triggered.

Therefore there will be only one star.

The else would only apply, if the break does NOT get triggered.



### 43. Basics

- CASE: Which of the following variable names are illegal?


- Solution: True, and


- Try it yourself:


```
TRUE = 23
true = 42
# True = 7  # SyntaxError: cannot assign to True
# and = 7   # SyntaxError: invalid syntax
```


- You cannot use keywords as variable names.



### 44. Operators

- CASE: The result of the following addition:


```
123 + 0.0
```


- Solution: is equal to 123.0


- If you have an arithmetic operation with a float,

the result will also be a float.



### 45. Data Types

- CASE: The 0o prefix means that the number after it is denoted as:


- Solution: Octal


- Try it yourself:

```
print(0o10)  # 8
print(0o77)  # 63
```

Explanation:

The octal numeral system, or oct for short,

is the base-8 number system, and uses the digits 0 to 7



### 46. Data Types

- CASE: The value thirty point eleven times ten raised to the power of nine

should be written as:


- Solution: 30.11E9


- Try it yourself:

```
print(30.11E9)        # 30110000000.0
# print(30E11.9)      # SyntaxError: invalid syntax
# print(30.11E9.0)    # SyntaxError: invalid syntax
# print(30.11*10^9)   # TypeError: unsupported operand ...
 
print(30.11 * 10 ** 9)  # 30110000000.0
```

Explanation:


You could replace the E by * 10 **



### 47. Functions

- CASE: What is the output of the following snippet?


```
def fun(x, y, z):
    return x + 2 * y + 3 * z
 
print(fun(0, z=1, y=3))
```


- Solution: 9


- The function here works fine.

The keyword arguments do not have to be in the correct order among themselves

as long as they are all listed after all positional arguments.

And because multiplication precedes addition 9 gets returned and printed.



### 48. Basics

- CASE: The digraph written as #! is used to:



- Solution: tell a Unix or Unix-like OS how to execute the contents of a Python file.


- #! shebang



### 49. Error Handling

- CASE: Which of the approachable except: branches

is taken into consideration when an exception occurs?



- Solution: The first matching branch


- Try it yourself:

```
try:
    zahl = 100 / 0
except ArithmeticError:
    print('ArithmeticError')  # ArithmeticError
except ZeroDivisionError:
    print('ZeroDivisionError')
 
try:
    zahl = 100 / 0
except ZeroDivisionError:
    print('ZeroDivisionError')  # ZeroDivisionError
except ArithmeticError:
    print('ArithmeticError')
 
print(issubclass(ZeroDivisionError, ArithmeticError))  # True
```


- The ZeroDivisionError is a subclass of the ArithmeticError

Therefore here they are both approachable except: branches.

And the first match is taken into consideration.



### 50. Operators

- CASE: You develop a Python application for your company.

You have the following code.


```
def main(a, b, c, d):
    value = a + b * c - d
    return value
```


Which of the following expressions is equivalent to the expression in the function?



- Solution: (a + (b * c)) - d


- This question is about operator precedence

The multiplication operator has the highest precedence

and is therefore executed first.

That leaves the addition operator and the subtraction operator

They both are from the same group and therefore have the same precedence.

That group has a left-to-right associativity.

The addition operator is on the left and is therefore executed next.

And the last one to be executed is the subtraction operator



### 51. Data Aggregates

- CASE: What is the output of the following snippet?


```
dictionary = {'one': 'two', 'three': 'one', 'two': 'three'}
v = dictionary['one']
 
for k in range(len(dictionary)):
    v = dictionary[v]
 
print(v)
```


- Solution: two


- Before the for loop the value of index 'one' is assigned to v

And that value is 'two'

In the first iteration of the for loop the value of index 'two' is assigned to v

And that value is 'three'

In the second iteration of the for loop

the value of index 'three' is assigned to v

And that value is 'one'

In the third iteration of the for loop the value of index 'one' is assigned to v

And that value is again 'two'

After the for loop that value 'two' is printed.



### 52. Functions

- CASE: What is the expected output of the following code?


```
def fun():
    return True
x = fun(False)
print(x)
```


- Solution: The program will cause an error.


- Try it yourself:

```
def fun():
    return True
 
 
x = fun(False)
# TypeError: fun() takes 0 positional arguments but 1 was given
print(x)
```


- The fun() function is defined with any parameters

and therefore it cannot be called with an argument.



### 53. Data Aggregates

- CASE: What is the expected output of the following code?


```
print(list('hello'))
```


- Solution: ['h', 'e', 'l', 'l', 'o']



- Try it yourself:

print(list('hello'))  # ['h', 'e', 'l', 'l', 'o']



Explanation:

A string is a sequence of characters

and works very fine with the list() function.

The result is a list of strings, in which every character is a string of its own.



### 54. Data Aggregates

- CASE: What will be the output of the following code snippet?


```
d = {}
d[1] = 1
d['1'] = 2
d[1] += 1
 
sum = 0
 
for k in d:
    sum += d[k]
 
print(sum)
```


- Solution: 4


- Try it yourself:

```
d = {}
print(d)  # {}
d[1] = 1
print(d)  # {1: 1}
d['1'] = 2
print(d)  # {1: 1, '1': 2}
d[1] += 1
print(d)  # {1: 2, '1': 2}
 
sum = 0
for k in d:
    sum += d[k]
    print("key: ", k, " - value: ", d[k])
    # key:  1  - value:  2
print(sum)  # 4
 
sum = 0
for k in d.keys():
    sum += d[k]
    print("key: ", k, " - value: ", d[k])
    # key:  1  - value:  2
print(sum)  # 4
```


- The knowledge you need here is that a dictionary

can have indexes of different data types.

Therefore d[1] is a different index than d['1']

and they can both exist in the same dictionary.



To iterate through a dictionary is the same as

iterating through dict.keys()

In k will be the keys of the dictionary.

In this case 1 and '1'

The value of the first key will be 2

and the value of the other key will also be 2

and therefore (the) sum is 4



### 55. Data Aggregates

- CASE: What is the output of the following snippet?


```
dct = {}
dct['1'] = (1, 2)
dct['2'] = (2, 1)
 
for x in dct.keys():
    print(dct[x][1], end='')
```


- Solution: 21


- Try it yourself:

```
dct = {}
dct['1'] = (1, 2)
dct['2'] = (2, 1)
print(dct)  # {'1': (1, 2), '2': (2, 1)}
 
for x in dct.keys():
    print(dct[x][1], end='')  # 21
print()
print(dct['1'][1])  # 2
print(dct['2'][1])  # 1
```


- dct.keys() are the keys '1' and '2'

dct['1'][1] is 2 and

dct['2'][1] is 1



### 56. Data Aggregates

- CASE: What is the expected output of the following code?


```
list1 = [1, 3]
list2 = list1
list1[0] = 4
print(list2)
```


- Solution: [4, 3]


- Try it yourself:

```
list1 = [1, 3]
list2 = list1
list1[0] = 4
print(list2)  # [4, 3]
print(id(list1))  # e.g. 140539383947452
print(id(list2))  # e.g. 140539383947452 (the same number)
```


Explanation:

A list is mutable.

When you assign it to a different variable,

you create a reference of the same object.

If afterwards you change one of them, the other one is changed too.


