### [Source of this study material : One Week Python by Colt Steele](https://www.udemy.com/course/one-week-python/)


## Lists

- Lists are **ordered collections** of data.


- They can hold any of the data types we've seen.


- We use square brackets [] and use commas to separate items in the list.



### List index

- We can retrieve individual elements from a list by passing an index number inside of square brackets. Like strings, indices start at zero.



![waiting-lists](/GCP_ML_pictures/Study-logs/Python/Fundamentals/lists/waiting-lists.PNG "waiting lists")



### Updating list elements

- You can use the index to update a specific element.


![updating-list](/GCP_ML_pictures/Study-logs/Python/Fundamentals/lists/updating-list.PNG "Updating list")



### append() and extend()

- append() adds a single value to the end of a list.


![list-append](/GCP_ML_pictures/Study-logs/Python/Fundamentals/lists/list-append.PNG "list append")


- extend() accepts an iterable and appends each item from that iterable to the end of the list. It will **iterate over** the argument we provide (in below case, '12345')


![list-extend](/GCP_ML_pictures/Study-logs/Python/Fundamentals/lists/adding-iterable.PNG "list extend")


- When you append a list to another list and when you want to add each element of the list rather than the list itself, **extend()** is very useful. But if you **append() a list**, a list itself is added to another list.


![extend-and-append](/GCP_ML_pictures/Study-logs/Python/Fundamentals/lists/append-and-extend.PNG "append and extend")



### insert(index, element)

- Index is the index number before which to insert the element. Element is a thing to be inserted into the list.


![list-insert](/GCP_ML_pictures/Study-logs/Python/Fundamentals/lists/list-insert.PNG "list insert")



### Slicing lists

- You can slice a portion of a list using index. You can omit the index if it is in the first place or the last place of the list.


![slicing-list](/GCP_ML_pictures/Study-logs/Python/Fundamentals/lists/slicing-list.PNG "slicing list")


### clear(), pop(), del

- clear() will completely empty out a list. It removes all items from a list.


![list-clear](/GCP_ML_pictures/Study-logs/Python/Fundamentals/lists/list-clear.PNG "list clear")


- pop() method removes AND returns the last element from a list. It shows which last element it removed and the last element is completely gone.


![list-pop](/GCP_ML_pictures/Study-logs/Python/Fundamentals/lists/list-pop.PNG "list pop")



- pop() also accepts a specific index. It will remove the item at that index in the list AND return it.


![list-pop-index](/GCP_ML_pictures/Study-logs/Python/Fundamentals/lists/list-pop-index.PNG "list pop index")


- The del statement (it's not a method) can be used to delete a whole slice from the list.


![del-statement](/GCP_ML_pictures/Study-logs/Python/Fundamentals/lists/del-statement.PNG "del statement")


- You can delete **every other element** in the list using the del statement.


![delete-every-other-element](/GCP_ML_pictures/Study-logs/Python/Fundamentals/lists/delete-every-other-element.PNG "delete every other element")



### Iterating lists

- To iterate each item on the list, you can use **for.. in..**:


```
emails = ['yejin@gmail.com', 'roina@naver.com', 'jimbo@gmail.com', 'jasmine@yahoo.com', 'greenbox@gmail.com', 'firsthuman@yahoo.com', 'darling@ggmail.com']

for email in emails:
  print(email)
```


![iterating-list](/GCP_ML_pictures/Study-logs/Python/Fundamentals/lists/interating-list.PNG "iterating list")



- You can also use **while** loop, but it will iterate over the index.


```
emails = ['yejin@gmail.com', 'roina@naver.com', 'jimbo@gmail.com', 'jasmine@yahoo.com', 'greenbox@gmail.com', 'firsthuman@yahoo.com', 'darling@ggmail.com']

index = 0

while index < len(emails):
  for email in emails:
    print(email)
    index += 1
```


![iterating-list-with-while-loop](/GCP_ML_pictures/Study-logs/Python/Fundamentals/lists/using-while-loop-for-iterating-list.PNG "itertaing list with while loop")



### Adding up elements in the list

- We use a variable (total = 0) to add up all the elements in the list.


```
result = [1,3,5,6,3,5,3,5,6,7,4,3,3,6,8,3,5,7,2,5]

total = 0

for element in result:
  total += element

print(total)
```


![adding-up-elements](/GCP_ML_pictures/Study-logs/Python/Fundamentals/lists/adding-up-elements.PNG "Adding up elements")



- To calculate the average, do this:


```
result = [1,3,5,6,3,5,3,5,6,7,4,3,3,6,8,3,5,7,2,5]

total = 0

for element in result:
  total += element

print(f"The total is {total}")
print(f"The average is {total/len(result)}")
```


![calculating-average](/GCP_ML_pictures/Study-logs/Python/Fundamentals/lists/calculating-avg.PNG "Calculating average")



- Create a function to add up all the elements:


```
numlist = [1,3,5,6,3,5,3,5,6,7,4,3,3,6,8,3,5,7,2,5]

def average(numlist):
  total = 0
  for i in numlist:
    total += i
  return total / len(numlist)

print(average(numlist))
print(round(average([1,5,75,43,5,2,4]),2))
```


![using-function-for-average](/GCP_ML_pictures/Study-logs/Python/Fundamentals/lists/using-function-for-average.PNG "using function for average")



### Finding a minimum in the list


```
numlist = [1,3,5,6,3,5,3,5,6,7,4,3,3,6,8,3,5,7,2,5]

min = numlist[0]

for element in numlist:
  if element < min:
    min = element

print(min)
```


![finding-minimum](/GCP_ML_pictures/Study-logs/Python/Fundamentals/lists/fiding-minimum.PNG "finding minimum")



### Grand Prix Drivers


```
drivers = ['Valterri', 'Lewis', 'Elton', 'George', 'Lando', 'Esteban', 'Pierre']

for idx in range(len(drivers)):
  print(f"{idx+1}. {drivers[idx]}")
```


![grand-prix-drivers](/GCP_ML_pictures/Study-logs/Python/Fundamentals/lists/grand-prix-drivers.PNG "Grand Prix drivers")



### Nested lists

- You can iterate over the nested list (list inside of list) like below:


```
couples = [['yejin','momo'],['toto','mimi'],['tommy','angela'],['shaun','tiana']]

for couple in couples:
  for person in couple:
    print(f"Send email to {person}")
```


![nested-lists](/GCP_ML_pictures/Study-logs/Python/Fundamentals/lists/nested-lists.PNG "nested lists")



### Count elements in lists

- The count method returns the number of times a value occurs in a list. If the value is not in the list, it returns 0.


```
numbers = [1,6,3,8,4,8,0,4,5,84,6,3,7,9,34,6,8,4,8,5,6,4,4,6,8,9,0,4,5,6,7,8,9,0,1]


def count_num(numbers, num):
  return print(f"The number {num} occurs {numbers.count(num)} times in the list")


print(count_num(numbers,8))
```


![count-numbers](/GCP_ML_pictures/Study-logs/Python/Fundamentals/lists/count-numbers.PNG "count numbers")



### Sort and reverse methods

- The sort method sorts your list in an ascending order by default while reverse method reverses the order in place.


```
numbers = [1,6,3,8,4,8,0,4,5,84,6,3,7,9,34,6,8,4,8,5,6,4,4,6,8,9,0,4,5,6,7,8,9,0,1]


numbers.sort(reverse=True)

print(numbers)
```


![sort-reverse](/GCP_ML_pictures/Study-logs/Python/Fundamentals/lists/sort-reverse.PNG "sort and reverse")



### Comparing lists

1. Use **==** to compare the contents inside of two lists. Do they hold the same values?


2. Use **is** to compare the identity of two lists. Are they the same "container" in memory?


![comparing-lists](/GCP_ML_pictures/Study-logs/Python/Fundamentals/lists/comparing-lists.PNG "Comparing lists")



### Split methods

- **split()** is a string method that will split a string on a given character. It returns a list that holds the split strings.


![split-method](/GCP_ML_pictures/Study-logs/Python/Fundamentals/lists/split-method.PNG "split method")



### Join methods

- **join()**  joins together individual elements in the list:


![join-method](/GCP_ML_pictures/Study-logs/Python/Fundamentals/lists/join-method.PNG "join method")



### Copy lists

- **list2 = list1.copy()** returns a shallow copy of a list. Nested objects are not copied.


![copy-list](/GCP_ML_pictures/Study-logs/Python/Fundamentals/lists/copy-list.PNG "copy lists")


- The **deepcopy()** method will make a copy of a list AND any nested objects contained inside that list.


```
import copy
list1 = [1,2,3,4,[5,6,7,8]]
list2 = copy.deepcopy(list1)
```


![deepcopy](/GCP_ML_pictures/Study-logs/Python/Fundamentals/lists/deepcopy.PNG "deepcopy")



### Create a todo list


```
header = """
  _____         _           
 |_   _|__   __| | ___  ___ 
   | |/ _ \ / _` |/ _ \/ __|
   | | (_) | (_| | (_) \__ \
   |_|\___/ \__,_|\___/|___/
"""

todos = []
while True:
  for i in range(len(todos)):
    print(f"{i+1}) {todos[i]}")
  print("*"*50)
  print("Enter a command.")
  command = input("> ")
  if command == 'q':
    break
  elif command.isnumeric():
    if int(command) > len(todos):
      print("There is no todo with that number.")
    else:
      num = int(command)
      todos.pop(num-1)
  else:
    todos.append(command)
```


![todo-list](/GCP_ML_pictures/Study-logs/Python/Fundamentals/lists/todo-list.PNG "todo list")



