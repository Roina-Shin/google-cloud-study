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


