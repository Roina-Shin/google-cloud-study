### [Source of this study material : One Week Python by Colt Steele](https://www.udemy.com/course/one-week-python/)


## Tuples

- Like lists, tuples are ordered, indexed collections


- Unlike lists, **tuples are immutable**. They cannot change once created


- You can't put a single element inside the parentheses in a tuple. If you add a trailing comma after the single element, then it's acceptable to Python.


```
dishes = ("burrito", "taco", "fajita", "quesadilla")
```


- And you can't update an immutable element inside the tuple. If you try to assign a new value to an element, it will cause error.



![tuple-elements-are-immutable](/GCP_ML_pictures/Study-logs/Python/Fundamentals/tuples-and-sets/tuple-element-immutable.PNG "tuple elements are immutable")



## Why use tuples?

- They are more efficient than lists.


- Use them for data that shouldn't change.


- Some methods return them in the form of tuple like dict.items()


- They can be used as keys in a dictionary. ('latitude and longitude' as a tuple key and the region name as a value)


```
{(37.532600, 127.024612) = 'seoul'}
```


## Sets

- They are unordered collections with **no duplicate elements**. Think of it as a set of unique values.


- Only **immutable elements** can be contained in sets.


```
evens = {2, 4, 6, 8}
```


- We use curly braces {} to create sets. 



### Sets - add() / remove()

- add() adds a single value to a set. No duplates in sets!


```
evens = {2,4,6,8,10}

evens.add(12)

evens = {2,4,6,8,10,12}
```


- remove() removes a single value from a set.


```
evens = {2,4,6,8,10}

evens.remove(4)

evens = {2,6,8,10}
```


![sets-add-and-remove](/GCP_ML_pictures/Study-logs/Python/Fundamentals/tuples-and-sets/sets-add-and-remove.PNG "sets add and remove")



### Intersection (&) and Union (|) and Difference (-)

- Intersection (&) returns a new set with members common to left and right. We use '&' to do the operation.


```
set_odd = {1,3,5,7,9,11}
set_prime = {1,3,5,7,11}

set_odd & set_prime

{1,3,5,7,11}
```


- Union (|) returns a new set with members combined from left and right. We use pipe symbol (|) to do the operation.


```
set_odd = {1,3,5,7,9,11}
set_even = {2,4,6,8,10}

set_odd | set_even

{1,2,3,4,5,6,7,8,9,10,11}
```


- Difference (-) returns a new set with only members unique from left and not in right. We use minus sign (-) to do the operation.


```
set_odd = {1,3,5,7,9,11}
set_prime = {1,3,5,7,11}

set_odd - set_prime

{9}
```


![set-intersection-union-difference](/GCP_ML_pictures/Study-logs/Python/Fundamentals/tuples-and-sets/set-intersection-union-difference.PNG "set intersection - union - difference")






