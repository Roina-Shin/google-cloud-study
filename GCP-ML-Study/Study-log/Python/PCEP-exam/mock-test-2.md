### [Source of this study material : Python Certification Exam PCEP by Cord Mählmann](https://www.udemy.com/course/pcep-certification-python-exam-practice-tests/)


## Exam -2 

### 1. Operators

- CASE: The += operator, when applied to strings, performs:


- Solution: Concatenation


- The add and assign operator when applied to strings,

performs a string concatenation.

Just like the addition operator



### 2. Data Types

- CASE: What is the expected output of the following code?


```
data = 'abbabadaadbbaccabc'
print(data.count('ab', 1))
```


- Solution: 2



- Try it yourself:


```
data = 'abbabadaadbbaccabc'
print(data.count('ab', 1))  # 2
print(data.count('ab', 0))  # 3
```


Explanation:

Remember to bring your best reading glasses to the exam.

The second parameter will determine where the count() method

will start its counting.

The first parameter (in this case ab) is what count() will look for.

count() will start at index 1

and therefore it will not find the ab right at the beginning of the string.

That leaves two more ab to find.



### 3. Data Aggregates

- CASE: Take a look at the snippet

and choose one of the following statements which is true:


```
nums = []
vals = nums[:]
vals.append(1)
```


- Solution: vals is longer than nums


- Try it yourself:


```
nums = []
vals = nums[:]
vals.append(1)
print(nums)  # []
print(vals)  # [1]
```

Explanation:

nums[:] slices the list from beginning to end and therefore makes a copy.

If you change vals afterwards, nums will not also change.



### 4. Data Aggregates

- CASE: After execution of the following snippet,

the sum of all vals elements will be equal to:


```
vals = [0, 1, 2]
vals.insert(0, 1)
del vals[1]
```


- Solution: 4


- Try it yourself:


```
vals = [0, 1, 2]
vals.insert(0, 1)
print(vals)  # [1, 0, 1, 2]
del vals[1]
print(vals)  # [1, 1, 2]
print(sum(vals))  # 4
```


Explanation:

First 1 is inserted at index 0 and the list is: [1, 0, 1, 2]

Then the new index 1 is deleted and the list is: [1, 1, 2]

1 + 1 + 2 -> 4



### 5. Control Flow

- CASE: Consider the following code.


```
for n in range(1, 6, 1):
    print(??? * 5)
```


What would you insert instead of ???

so that the program prints the following pattern to the monitor?


```
11111
22222
33333
44444
55555
```


- Solution: str(n)


- Try it yourself:


```
for n in range(1, 6, 1):
    print(str(n) * 5)
"""
11111
22222
33333
44444
55555
"""
 
print('----------')
 
for n in range(1, 6, 1):
    print(n * 5)
"""
5
10
15
20
25
"""
 
print('----------')
 
for n in range(1, 6, 1):
    print(-1 * 5)
"""
-5
-5
-5
-5
-5
"""
 
```


Explanation:

range(1, 6, 1) delivers the right numbers 1, 2, 3, 4, 5.

(It would also work without step 1, because that's the default value.)

You need the str() function here to get more numbers.

Otherwise a calculation takes place

and you end up with one number per row.

By string concatenation you get the right result:

'1' * 5 -> '11111'
'2' * 5 -> '22222'
'3' * 5 -> '33333'
'4' * 5 -> '44444'
'5' * 5 -> '55555'



### 6. Basics

- CASE: A code point is:


- Solution: A number which makes up a character.


- Try it yourself:

print(ord('A')) # 65

Explanation:

For example in ASCII the number 65 makes up the character A



### 7. Data Aggregates

- CASE: What is the expected output of the following code?


```
data = {'1': '0', '0': '1'}
 
for d in data.vals():
    print(d, end=' ')
```


- Solution: The code is erroneous.


- Try it yourself:


```
data = {'1': '0', '0': '1'}
 
# for d in data.values():
for d in data.vals():  # AttributeError: ...
    print(d, end=' ')    # 0 1
```


Explanation:

This question is a little tricky.

Everything seems to be fine,

BUT the right name of the dictionary method is values()



### 8. Data Aggregates

- CASE: You develop a Python application for your company.



A list named employees contains 200 employee names,

the last five being company management.

You need to slice the list to display all employees excluding management.



Which code segments can you use?

Choose two.



- Solution: 


- employees[0:-5]

- employees[:-5]


```
employees = []
 
# for i in range(1, 196):
for i in range(1, 6): # Just for convenience
    employees.append('Employee' + str(i))
 
for i in range(1, 6):
    employees.append('Manager' + str(i))
 
print(employees)
print(employees[:-5])
print(employees[0:-5])
print(employees[1:-4])
# One manager present and one employee is missing
print(employees[1:-5])  # One employee is missing
print(employees[0:-4])  # One manager present
```

- List slicing: [start(inclusive):end(exclusive)]

The default value for the start is 0

Meaning you can write it or leave it out.

The negative index counts from the end.

The end is exclusive.

-1 cuts out one element.

-5 cuts out five elements.

And that is what you need here for the five managers.



### 9. Control Flow

- CASE: How many stars will the following code send to the monitor?


```
x = 0
while x < 6:
    x += 1
    if x % 2 == 0:
        continue
    print('*')
```


- Solution: 3


- Try it yourself:


```
x = 0
while x < 6:
    print('1. x:', x)         # 0 -> 1 -> 2 -> 3 -> 4 -> 5
    x += 1
    print('2. x:', x)         # 1 -> 2 -> 3 -> 4 -> 5 -> 6
    if x % 2 == 0:
        print('x in if:', x)  # 2 -> 4 -> 6
        continue
    print('x behind if:', x)  # 1 -> 3 -> 5
    print('*')
"""
*
*
*
"""
```


Explanation:

When x is 2, 4 and 6 the if condition is True

and the continue gets triggered.

The iteration ends directly and the print() function doesn't get executed.

When x is 1, 3 and 5 the if condition is False

the continue does not get triggered

and those three times the print() function gets executed.

Therefore there will be three stars printed.



### 10. Control Flow

- CASE: Which of the following sentences correctly describes

the output of the below Python code?


```
data = [4, 2, 3, 2, 1]
res = data[0]
 
for d in data:
    if d < res:
        res = d
 
print(res)
```


- Solution: res is the smallest number in the list.


- Classic way to find the smallest number.

Take the first element as possible result.

Compare the next number with the possible result.

If the next number is smaller,

it becomes the new possible result and so forth.

In the end the result is the smallest number.



### 11. Data Aggregates

- CASE: What is the expected output of the following code?


```
a = [1, 2, 3, 4, 5]
print(a[3:0:-1])
```


- Solution: [4, 3, 2]


- Try it yourself:

```
a = [1, 2, 3, 4, 5]
print(a[3:0:-1])  # [4, 3, 2]
```


Explanation:

List slicing: [start(inclusive):end(exclusive):step]

The step is negative here.

That makes the slice be build from right to left (start interchanges with end).

The start is the index 3 (inclusive) and the end is index 0 (exclusive).

Therefore we will get index 3 index 2 and index 1

which are the numbers 4, 3, 2



### 12. Functions

- CASE: What is the expected output of the following code?


```
num = 1
 
 
def func():
    num = 3
    print(num, end=' ')
 
 
func()
 
print(num)
```


- Solution: 3 1


- Try it yourself:


```
num = 1
 
 
def func():
    num = 3              # Shadows name 'num' from outer scope
    print(num, end=' ')  # 3
 
 
func()
 
print(num)  # 1
```


Explanation:

The num variable inside the function scope will be a different variable.

It will shadow the name of the num variable from the outer scope,

but it will be a different entity.



### 13. Functions

- CASE: What is the expected output of the following code?


```
data = 'abcdefg'
 
 
def func(text):
    del text[2]
    return text
 
 
print(func(data))
```


- Solution: The code is erroneous.


- Try it yourself:


```
data = 'abcdefg'
 
 
def func(text):
    # del text[2]  # TypeError: ...
    return text
 
 
print(func(data))
 
# Strings are immutable
# The indexes are readable but not writeable:
s = 'Hello'
print(s[0])   # H
# s[0] = 'h'  # TypeError: ...
```


Explanation:

A string is immutable. You can not change it.

You can read something by indexing,

BUT you can not write something by indexing.



### 14. Operators

- CASE: What is the expected output of the following code?


```

x = True
y = False
x = x or y
y = x and y
x = x or y
print(x, y)
```


- Solution: True False


```
x = True
y = False
x = x or y   # True or False -> True
y = x and y  # True and False -> False
x = x or y   # True or False -> True
print(x, y)  # True False
```


### 15. Basics

- CASE: What is the best definition of a script?


- Solution: It's a text file that contains instructions which make up a Python program.


- Due to historical reasons, languages designed for use in interpretation

are often called scripting languages,

while the source programs encoded using them are called scripts.



### 16. Basics

- CASE: What do you call a file containing a program written in a high-level programming language?


- Solution: A source file


- You can also call it source code file,

but not just code file.



### 17. Error Handling

- CASE: What is the output of the following program

if the user enters kangaroo at the first prompt

and 0 at the second prompt?


```
try:
    first_prompt = input("Enter the first value: ")
    a = len(first_prompt)
    second_prompt = input("Enter the second value: ")
    b = len(second_prompt) * 2
    print(a/b)
except ZeroDivisionError:
    print("Do not divide by zero!")
except ValueError:
    print("Wrong value.")
except:
    print("Error.Error.Error.")
```


- Solution: 4.0


- No exception will be thrown.

The length of kangaroo is 8

and the length of 0 is 1

1 * 2 -> 2

8 / 2 -> 4.0



### 18. Data Aggregates

- CASE: What is the expected output of the following code?


```
data = [
    [1, 2, 3, 4],
    [5, 6, 7, 8],
    [9, 10, 11, 12],
    [13, 14, 15, 16]
]
for i in range(0, 4):
    print(data[i].pop(), end=' ')
```


- Solution: 4 8 12 16


- Try it yourself:

```
data = [
    [1, 2, 3, 4],
    [5, 6, 7, 8],
    [9, 10, 11, 12],
    [13, 14, 15, 16]
]
for i in range(0, 4):
    print(data[i].pop(), end=' ')  # 4 8 12 16
 
print()
print(list(range(0, 4)))  # [0, 1, 2, 3]
 
print([1, 2, 3, 4].pop())      # 4
print([5, 6, 7, 8].pop())      # 8
print([9, 10, 11, 12].pop())   # 12
print([13, 14, 15, 16].pop())  # 16
```


Explanation:

data is a two dimensional list.

In every iteration of the for loop,

pop() removes the last element of the corresponding inner list.

That last element gets printed.

The default value of the print() functions end parameter is the line feed.

That gets overwritten here by a single space character.



### 19. Control Flow

- CASE: The ABC Video company needs a way to determine the cost

that a customer will pay for renting a DVD.

The cost is dependent on the time of day the DVD is returned.

However, there are also special rates on Thursdays and Sundays.

The fee structure is shown in the following list:



The cost is $1.59 per night.

If the DVD is returned after 8 PM, the customer will be charged an extra day.

If the video is rented on a Sunday,

the customer gets 30% off for as long as they keep the video.

If the video is rented on a Thursday,

the customer gets 50% off for as long as they keep the video.



You need to write code to meet the requirements.


```
# ABC Video, DVD Rental Calculator
 
ontime = input('Was the video returned before 8 pm? y or n').lower()
days_rented = int(input('How many days was the video rented?'))
day_rented = input('What day was the video rented?').capitalize()
 
cost_per_day = 1.59
 
if ontime XXX
    days_rented += 1
if day_rented YYY
    total = (days_rented * cost_per_day) * .7
elif day_rented ZZZ
    total = (days_rented * cost_per_day) * .5
else:
    total = (days_rented * cost_per_day)
 
print('Cost of the DVD rental is: $', total)
```


- Solution:

```
XXX -> == 'n':
YYY -> == 'Sunday':
ZZZ -> == 'Thursday':
```


- At this company to return a video on time means to return it before 8 PM.

Otherwise one day is added to the amount of rented days.

If you return your video on a Sunday you get 30% off.

Meaning you only pay 70%.

And if you return your video on a Thursday, you pay only half (50%).



### 20. Control Flow

- CASE: How many stars will the following code print to the monitor?


```
i = 0
while i < i + 2:
    i += 1
    print('*')
else:
    print('*')
```


- The snippet will enter an infinite loop.


- Try it yourself:


```
i = 0
while i < i + 2:
    i += 1
    print('*')
    if i == 1000: break  # Safeguard
else:
    print('*')
```


Explanation:

i gets incremented inside the while loop,

BUT i will always be smaller than i + 2

Therefore the while condition will always be True

and we build ourselves a nice infinite loop.



### 21. Data Types

- CASE: What is the decimal value of the following binary number?


```
1010
```


- Solution: 10


```
print(0b1010)   # 10
print(bin(10))  # 0b1010
print(0b0010)   # 2
print(0b1000)   # 8
print(0b1000 + 0b0010)  # 10
```


- The value of the second bit is 2

and the value of the forth bit is 8

That is 10 in total.



### 22. Basics

- CASE: UTF‑8 is ...


- Solution: an encoding form of the Unicode Standard.


- Topic: UTF-8

Explanation:

UTF-8 is one of three encoding forms of the Unicode Standard.

The others are UTF-16 and UTF-32.

UTF-8 is the most popular one, because it is most flexible.

UTF-8 requires 8, 16, 24 or 32 bits (one to four bytes)

to encode a Unicode character,

UTF-16 requires either 16 or 32 bits to encode a character,

and UTF-32 always requires 32 bits to encode a character.



### 23. Operators

- CASE: What value will be assigned to the x variable?


```
z = 3
y = 7
x = y == z and y > z or z > y and z != y
```


- Solution: False



### 24. Error Handling

- CASE: What is the output of the following code?


```
try:
    value = input("Enter a value: ")
    print(value/value)
except ValueError:
    print("Bad input...")
except ZeroDivisionError:
    print("Very bad input...")
except TypeError:
    print("Very very bad input...")
except:
    print("Booo!")
```


- Solution: Very very badd input...


- The input() function always returns a string.

If you try to divide by a string you get a TypeError



### 25. Functions

- CASE: The following snippet:


```
def function_1(a):
    return None
 
def function_2(a):
    return function_1(a) * function_1(a)
 
print(function_2(2))
```


- Solution: will cause a runtime error


```
def function_1(a):
    return None
 
 
def function_2(a):
    return function_1(a) * function_1(a)
    # TypeError: unsupported operand type(s) for *: 
    # NoneType' and 'NoneType'
 
 
print(function_2(2))
 
print(None * None)
# TypeError: unsupported operand type(s) for *:
# 'NoneType' and 'NoneType'
 
print(function_2(2))
```


- function_1() returns the None value

and any arithmetic operation with the None value will cause a TypeError.



### 26. Operators

- CASE: What is the expected output of the following code?


```
print(1 / 1)
```


- Solution: 1.0


- Topic: division operator

Try it yourself:


```
print(1 / 1)  # 1.0
```


Explanation:

All you have to know here is,

that the division operator always returns a float.

Even if it is operating with two integers.



### 27. Operators

- CASE: What is the output of the following code?


```
a = 10
b = 20
c = a > b
print(not(c))
```

- Solution: True



### 28. Operators

- CASE: Which of the following items are present in the function header?


- Solution: function name and parameter list


- Topics: def parameter function header

Try it yourself:

```
def func(para1, para2):  # This line is the function header
     para1 + para2
```


Explanation:

In the function header is the keyword def

the function name

and the parameter list.



### 29. Data Types

- CASE: What is the expected output of the following code?


```
print(chr(ord('z') - 2))
```


- Solution: x


- Topics: chr() ord()

Try it yourself:

```
print(chr(ord('z') - 2))  # x
print(ord('z'))           # 122
print(chr(120))           # x
```


Explanation:

ord() returns an integer representing the Unicode character.

chr() turns that integer back to the Unicode character.

You don't need to remember the number of every character,

but like in the alphabet x is two before z



### 30. Functions

- CASE: What is the expected output of the following code?


```
data = {}
 
 
def func(d, key, value):
    d[key] = value
 
 
print(func(data, '1', 'Peter'))
```


- Solution: None


- Topics: def return

Try it yourself:


```
data = {}
 
def func(d, key, value):
    d[key] = value
 
print(func(data, '1', 'Peter'))  # None
```


Explanation:

func() has no return statement.

Therefore None gets returned.


```
data = {}

def func(d, key, value):
    d[key] = value
    return d

print(func(data, '1', 'Peter')) # {'1': 'Peter'}
```


### 31. Error Handling

- CASE: The unnamed except block ...


- Solution: must be the last one.


- The unnamed except block always needs to be

the last one of the except blocks,

otherwise you will receive a SyntaxError



### 32. Operators

- CASE: Consider the following code.


```
x = 1
x = x == x
```


The value eventually assigned to x is equal to:


- Solution: True


- x has the value 1

x gets compared with the equal to operator with itself.

It is true, that x is equal to x

True gets stored in the same variable, in x



### 33. Control Flow

- CASE: How many stars (*) will the following code output to the screen?


```
n = 1
if n == 1:
    print("*")
if n == True:
    print("**")
if n == False:
    print("***")
```


- Solution: three


- Try it yourself:

```
n = 1
if n == 1:
    print("*")   # *
if n == True:
    print("**")  # **
if n == False:
    print("***")
```


Explanation:

1 is equal to 1 and one star is printed.

If you compare an integer with a boolean,

the boolean True will be implicitly casted to the integer 1

and again 1 is equal to 1 and two more stars are printed.



### 34. Basics

- CASE: What is the expected output of the following code?


```
x = '\\\\'
print(len(x))
```


- Try it yourself:


```
# print(len('\'))    # SyntaxError: ...
print(len('\\'))     # 1
# print(len('\\\'))  # SyntaxError: ...
print(len('\\\\'))   # 2
```


Explanation:

The backslash is the character to escape another character.

If you write '\' the backslash escapes

the ending single quote to a normal character.

It takes its syntactical meaning

and the single quote becomes a normal character

and it looses its ability to end the string.

And therefore we get the syntax error.

If you write '\\' the one backslash escapes the other

and you end up with a string with one normal backslash.

If you write '\\\\' it is kind of the same

and you end up with a string with two normal backslashes.



### 35. Operators

- CASE: What is the expected output of the following code?


```
i = 0
while i <= 5:
    i += 1
    if i % 2 == 0:
        break
    print('*')
```


- Solution : One


- Try it yourself:

```
i = 0
while i <= 5:
    print('1. i: ', i)  # 0 -> 1
    i += 1
    print('2. i: ', i)  # 1 -> 2
    if i % 2 == 0:  # False, True
        break
    print('*')  # *
```


Explanation:

i % 2 == 0 is known as test for even numbers.

In the first iteration i is an odd 1

and therefore the break does not get triggered

and a star gets printed.

In the second iteration i is an even 2

the break gets triggered and there is no more stars.



### 36. Data Aggregates

- CASE: What is the output of the following snippet?


```
my_list = [x * x for x in range(5)]
 
def fun(lst):
    del lst[lst[2]]
    return lst
 
print(fun(my_list))
```


- Solution: [0, 1, 4, 9]


- Try it yourself:


```
my_list = [x * x for x in range(5)]
print(my_list)  # [0, 1, 4, 9, 16]
# The same without list comprehension:
my_list = []
for x in range(5):
    my_list.append(x * x)
print(my_list)  # [0, 1, 4, 9, 16]
 
def fun(lst):
    # del lst[lst[2]]
    del lst[4]
    return lst
 
print(fun(my_list))  # [0, 1, 4, 9]
```


Explanation:

First my_list is generated as [0, 1, 4, 9, 16]

This list is passed to the fun() function.

The fun() function looks for the value at the second index: lst[2]

That value is 4

lst[lst[2]] becomes lst[4]

Therefore the index 4 is deleted

and the list is returned without the value 16



### 37. Functions

- CASE: Which of the following lines properly starts a function using two parameters,

both with zeroed default values?


- Solution: def (a=0, b=0):


- Try it yourself:

```
def fun(a=0, b=0):
    print(a, b)
 
 
fun()  # 0 0
 
 
def fun(a, b=0):
    print(a, b)
 
    
fun()  # TypeError: fun() missing 1 required positional argument: 'a'
 
# def fun(a=0, b): print(a, b)
# SyntaxError: non-default argument follows default argument
 
# def fun(a=b=0): print(a, b)
# SyntaxError: invalid syntax
```

Explanation:

There is no multiple assignment inside of the parameter list.

You have to assign each parameter its default value.



### 38. Data Aggregates

- CASE: What is the expected output of the following code?


```
numbers = [1, 2, 3, 4, 5]
nums = numbers[2: ]
print(nums)
```


- Solution: [3, 4, 5]


- Explanation:

[start:stop]

The stop is not given which means the last element is included.

The start is index 2 (inclusive) and therefore the result is [3, 4, 5]



### 39. Data Types

- CASE: Which of the following statements is false?


- Solution: The None value may not be used outside functions.


- Try it yourself:


```
# The None value can be assigned to variables.
x = None
print(x)  # None
 
# The None value can be compared with variables.
y = 3
print(y is None)   # False
 
# The None value cannot be used
# as an argument of arithmetic operators:
# print(None + 7)  # TypeError: unsupported operand ...
```


Explanation:

It is true that the None value can not be used

as an argument of arithmetic operators.

But the None value can be assigned and compared to variables.

And that can absolutely happen outside of a function.



### 40. Data Aggregates

- CASE: What is the expected output of the following code?


```
data = set([1, 2, 2, 3, 3, 3, 4, 4, 4, 4])
print(len(data))
```


- Solution : 4


```
data = set([1, 2, 2, 3, 3, 3, 4, 4, 4, 4])
print(len(data))  # 4
 
print(type(data))  # <class 'set'>
print(data) # {1, 2, 3, 4}
 
# Also works directly:
print(len({1, 2, 2, 3, 3, 3, 4, 4, 4, 4}))  # 4
```

- A set can not have duplicates.



### 41. Functions

- CASE: What is the expected output of the following code?


```
people = {}
 
 
def add_person(index):
    if index in people:
        people[index] += 1
    else:
        people[index] = 1
 
 
add_person('Peter')
add_person('Paul')
add_person('peter')
 
print(len(people))
```


- Solution: 3


- Try it yourself:


```
people = {}
 
 
def add_person(index):
    if index in people:
        people[index] += 1
    else:
        people[index] = 1
 
 
add_person('Peter')
add_person('Paul')
add_person('peter')
 
print(len(people))  # 3
print(people)       # {'Peter': 1, 'Paul': 1, 'peter': 1}
```


Explanation:

Peter is a different index than peter

because P is a different character than p

and therefore the dictionary will have three entries.



### 42. Data Aggregates

- CASE: What is the expected output of the following code?


```
data = [1, 2, 3, 4, 5, 6]
 
for i in range(1, 6):
    data[i - 1] = data[i]
 
for i in range(0, 6):
    print(data[i], end=' ')
```


- Solution: [2, 3, 4, 5, 6, 6]


- Try it yourself:


```
data = [1, 2, 3, 4, 5, 6]
 
for i in range(1, 6):  # 1 -> 2 -> 3 -> 4 -> 5
    data[i - 1] = data[i]
 
print(data)  # [2, 3, 4, 5, 6, 6]
 
# This is just for output:
for i in range(0, 6):
    print(data[i], end=' ')  # 2 3 4 5 6 6 
```



### 43. Functions

- CASE: What is the expected output of the following code?


```
def func(message, num=1):
    print(message * num)
 
 
func('Hello')
func('Welcome', 3)
```


- Solution: 


```
Hello
WelcomeWelcomeWelcome
```


### 44. Data Aggregates

- CASE: What code would you insert instead of the comment to obtain the expected output?



Expected output:


```
a
b
c
```


Code:


```
dictionary = {}
my_list = ['a', 'b', 'c', 'd']
 
for i in range(len(my_list) - 1):
    dictionary[my_list[i]] = (my_list[i], )
 
for i in sorted(dictionary.keys()):
    k = dictionary[i]
    # Insert your code here.

```


- Solution: print(k[0])


```
dictionary = {}
my_list = ['a', 'b', 'c', 'd']
 
# for i in range(len(my_list) - 1):
for i in range(3):
    dictionary[my_list[i]] = (my_list[i], )
print(dictionary)  # {'a': ('a',), 'b': ('b',), 'c': ('c',)}
 
# for i in sorted(dictionary.keys()):
for i in dictionary.keys():
    k = dictionary[i]
    # print(k)  # ('a',) ('b',) ('c',)
    # print(k['0'])  # TypeError: tuple indices must be integers or slices, not str
    # print(k["0"])  # TypeError: tuple indices must be integers or slices, not str
    print(k[0])
```


- You need k[0] because every element of the dictionary is a tuple

and you want the first index of each of those tuples.



### 45. Functions

- CASE: A function definition:


- Solution: must be placed before the first invocation.


- Try it yourself:


```
# my_first_function()
# NameError: name 'my_first_function' is not defined
 
def my_first_function():
    print('Hello')
```


Explanation:

The interpreter works line by line and therefore

a function definition must be placed before the first invocation.



### 46. Control Flow

- CASE: How many stars will the following code print to the monitor?


```
x = 1
while x < 10:
    print('*')
    x = x << 1
```


- Solution: four


- Try it yourself:


```
x = 1
while x < 10:
    print('*')
    x = x << 1
    print('x:', x)            # 2 -> 4 -> 8 -> 16
    print('bin(x):', bin(x))  # 0b10->0b100->0b1000->0b10000
 
"""
1 -> 00001 << 1 -> 00010 (2)
2 -> 00010 << 1 -> 00100 (4)
4 -> 00100 << 1 -> 01000 (8)
8 -> 01000 << 1 -> 10000 (16)
"""
```


Explanation:

Left shift by one, a classic way to double values.

Every value goes to the bit on its left and thereby doubles in value.

And 1, 2, 4, 8 are all smaller than 10 but not the 16

and therefore four stars will be printed.



### 47. Basics

- CASE: A complete set of known commands is called:


- Solution: an instruction list


- A complete set of known commands is called an instruction list,

sometimes abbreviated to IL.

Different types of computers may vary depending on the size of their ILs,

and the instructions could be completely different in different models.

The IL is, in fact, the alphabet of a machine language.

This is the simplest and most primary set of symbols

we can use to give commands to a computer.

It's the computer's mother tongue.



### 48. Basics

- CASE: How did Python, the programming language, get its name?


- Solution: Guido van Roddum named it after the Pythonidae - a family of large, nonvenomous snakes.


- While you may know the python as a large snake,

the name of the Python programming language comes from

an old BBC television comedy sketch series

called Monty Python's Flying Circus.

At the height of its success,

the Monty Python team were performing their sketches

to live audiences across the world,

including at the Hollywood Bowl.

Since Monty Python is considered one of the two

fundamental nutrients to a programmer (the other being pizza),

Python's creator named the language in honor of the TV show.



### 49. Functions

- CASE: Which of the following function headers is correct?


- Solution: def func(a=1, b=1, c=2):


Try it yourself:


```
def func(a=1, b=1, c=2):
    pass
 
# def func(a=1, b): pass            # SyntaxError: ...
# def func(a=1, b, c=2): pass       # SyntaxError: ...
# def func(a=1, b=1, c=2, d): pass  # SyntaxError: ...
 
 
# This would also work:
def func(a, b=1, c=2):
    pass
 
 
"""
def func(a=1, b): pass
func(7)
The 7 would go into a and there is nothing left for b.
"""
```


Explanation:

The default argument(s) have to be at the end.




### 50. Basics

- CASE: Which of the following variable names are illegal and will cause the SyntaxError exception?


- Solution: for, in


Try it yourself:


```
# in = 42  # SyntaxError: invalid syntax
# for = 7  # SyntaxError: invalid syntax
In = 23
print = 42
print(print)  # TypeError: 'int' object is not callable
```


Explanation:

in and for are both Python keywords and

therefore cannot be used as variable names.



### 51. Data Types

- CASE: What is the expected output of the following code?


```
print('Peter' 'Wellert')
```


- Solution: PeterWellert


- Try it yourself:

```
print('Peter' 'Wellert')  # PeterWellert
 
x = 'Hello' 'world'
print(x)  # Helloworld
```


Explanation:

String literals that are delimited by whitespace are automatically concatenated.



### 52. Operators

- CASE: What is the expected output of the following code?


```
x = 9
y = 12
result = x // 2 * 2 / 2 + y % 2 ** 3
print(result)
```


- Solution: 8.0


- The operators here are from three different groups:

"Exponent" has the highest precedence.

Followed by "Multiplication, Division, Floor division, Modulus".

"Addition, Subtraction" has the lowest precedence.

Therefore the order of operations here is: ** -> // -> * -> / -> % -> +



### 53. Basics

- CASE: What is the expected output of the following code?


```
x = """
"""
print(len(x))
```


- Solution: 1


- Try it yourself:


```
x = """
"""
print(len(x))  # 1
 
# ord() returns an integer representing the Unicode character.
print(ord(x[0]))  # 10 (LF: line feed, new line)
 
# Same result with single quotes:
y = '''
'''
print(len(y))  # 1
 
# Every line feed is a character:
z = """
 
"""
print(len(z))  # 2
```

Explanation:

In a multiline string the line feed gets saved like any other character.



### 53. Functions

- CASE: What is the output of the following snippet?


```
def fun(in=2, out=3):
    return in * out
 
print(fun(3))
```


- Solution: The snippet is erroneous.


- in is a keyword and therefore can not be used as a variable or a parameter.



### 54. Functions

- CASE: 

Which of the following function calls can be used to invoke

the below function definition?



def test(a, b, c, d):



Choose three.


- Solution: test(1, 2, 3, d=4), test(1, 2, 3, 4), test(a=1, a=2, a=3, a=4)


- Try it yourself:


```
def test(a, b, c, d):
    print(a, b, c, d)
 
 
test(1, 2, 3, 4)          # 1 2 3 4
test(a=1, b=2, c=3, d=4)  # 1 2 3 4
test(1, 2, 3, d=4)        # 1 2 3 4
 
# test(a=1, 2, 3, 4).     # SyntaxError: ...
# test(a=1, b=2, c=3, 4)  # SyntaxError: ...
# test(a=1, 2, c=3, 4)    # SyntaxError: ...
 
# print(end='', 'Hello')  # SyntaxError: ...
```

Explanation:

The keyword arguments always have to be at the end.