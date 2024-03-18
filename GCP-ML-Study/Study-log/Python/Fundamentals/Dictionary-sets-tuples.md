### [Source of this study material : One Week Python by Colt Steele](https://www.udemy.com/course/one-week-python/)


## Dictionary

- Dictionaries, known as associative arrays in some other languages, are **indexed by keys** rather than a numerical index.

  - A dictionary holds key-value pairs

  - Keys can be any immutable type: numbers, strings, booleans, etc.

  - Values can be whatever you want

- We use curly braces {} to create a dictionary.


```
order = {"cost": 3.5, "quantity": 12}
```


![dictionary-basics](/GCP_ML_pictures/Study-logs/Python/Fundamentals/dictionary-sets-tuple/dictionary-basics.PNG "dictionary basics")



- To retrieve the value for a key, we provide the key in square brackets: **order["quantity"]**


![retrieve-value](/GCP_ML_pictures/Study-logs/Python/Fundamentals/dictionary-sets-tuple/retrieve-value.PNG "retrieve value")


### Updating values with dictionary


![updating-dictionaries](/GCP_ML_pictures/Study-logs/Python/Fundamentals/dictionary-sets-tuple/updating-dic.PNG "Updating dictionary")


![updating-dic-value](/GCP_ML_pictures/Study-logs/Python/Fundamentals/dictionary-sets-tuple/updating-dic-value.PNG "updating dic values")


- To add a new key:value pair to your dictionary:


![add-key-value](/GCP_ML_pictures/Study-logs/Python/Fundamentals/dictionary-sets-tuple/add-key-value.PNG "add key value")



### The get() method and "in" operator

- The get() method will look for a given key in a dictionary. If the key exists, it willl return the corresponding value. Otherwise it returns None.


```
prices = {
    "banana": 4,
    "apple": 2,
    "orange": 1.5,
    "pear": 3
}

prices.get('banana')
```


![dict-get](/GCP_ML_pictures/Study-logs/Python/Fundamentals/dictionary-sets-tuple/dict-get.PNG "dict get")



### Dictionary pop(), clear(), and del

- The pop() method accepts a key and will delete the corresponding key-value pair in the dictionary. It returns the delete value.


![dict-pop](/GCP_ML_pictures/Study-logs/Python/Fundamentals/dictionary-sets-tuple/dict-pop.PNG "dict pop")


- popitem() deletes the most recently added key-value pair. It returns the item as a tuple. It takes no argument inside the parentheses.


```
prices = {
    "banana": 4,
    "apple": 2,
    "orange": 1.5,
    "pear": 3
}

prices.popitem()
```


![dict-popitem](/GCP_ML_pictures/Study-logs/Python/Fundamentals/dictionary-sets-tuple/dict-popitem.PNG "dict popitem")


- clear() deletes all items from a dictionary. It returns None.


![dict-clear](/GCP_ML_pictures/Study-logs/Python/Fundamentals/dictionary-sets-tuple/dict-clear.PNG "dict clear")


- The del statement removes items from a dictionary. Remember, it's not a method.


```
prices = {
    "banana": 4,
    "apple": 2,
    "orange": 1.5,
    "pear": 3
}

del prices['apple']
```


![dict-del](/GCP_ML_pictures/Study-logs/Python/Fundamentals/dictionary-sets-tuple/dict-del.PNG "dict del")



### Iterating dicts: keys(), values(), and items()

- If I want to iterate over the dictionary, you can iterate over the keys, valuesm and items using the keys(), values(), and items() methods.


```
test_scores= {
  "Marsha": 78,
  "Baker": 69,
  "Rosa": 92,
  "Leif": 97,
  "Peng": 61,
  "Juan": 73,
  "Esteban": 84,
  "Amir": 91,
  "Sakura": 99
}

test_scores.values()

# To make it a list
list(test_scores.values())
```


![dict-values](/GCP_ML_pictures/Study-logs/Python/Fundamentals/dictionary-sets-tuple/dict-values.PNG "dict values")


- You can then use the method to interate over the keys, values, and items.


```
for score in test_scores.values():
  print(score)
```


![iterate-values-in-dict](/GCP_ML_pictures/Study-logs/Python/Fundamentals/dictionary-sets-tuple/iterate-values-in-dict.PNG "iterate values in dict")


- To calculate the average score of the total, you can use the following:


```
test_scores= {
  "Marsha": 78,
  "Baker": 69,
  "Rosa": 92,
  "Leif": 97,
  "Peng": 61,
  "Juan": 73,
  "Esteban": 84,
  "Amir": 91,
  "Sakura": 99
}

total = 0

for score in test_scores.values():
  total += score

print(f"The average score is {round(total/len(test_scores),2)}")
```


![total-score-using-variable](/GCP_ML_pictures/Study-logs/Python/Fundamentals/dictionary-sets-tuple/total-score-using-variable.PNG "total score using variable")



- items() method is going to return to us an iterable object which is a key-value pair in the form of tuple.


```
test_scores= {
  "Marsha": 78,
  "Baker": 69,
  "Rosa": 92,
  "Leif": 97,
  "Peng": 61,
  "Juan": 73,
  "Esteban": 84,
  "Amir": 91,
  "Sakura": 99
}

for pair in test_scores.items():
  print(pair)
```


![dict-tems](/GCP_ML_pictures/Study-logs/Python/Fundamentals/dictionary-sets-tuple/dict-items.PNG "dict items")


- To **unpack the tuple** that contains the 2 elements, use:


```
test_scores= {
  "Marsha": 78,
  "Baker": 69,
  "Rosa": 92,
  "Leif": 97,
  "Peng": 61,
  "Juan": 73,
  "Esteban": 84,
  "Amir": 91,
  "Sakura": 99
}

for key, value in test_scores.items():
  print(key, value)
```


![unpack-the-tuple](/GCP_ML_pictures/Study-logs/Python/Fundamentals/dictionary-sets-tuple/unpack-the-tuple.PNG "unpack the tuple")


- To get the maximum score, you can run:


```
test_scores= {
  "Marsha": 78,
  "Baker": 69,
  "Rosa": 92,
  "Leif": 97,
  "Peng": 61,
  "Juan": 73,
  "Esteban": 84,
  "Amir": 91,
  "Sakura": 99
}

scores = list(test_scores.values())

max_score = scores[0]

for score in scores:
  if max_score < score:
    max_score = score

print(f"The max score is {max_score}.")
```


- If you want to know both pieces of information (student, max score):


```
test_scores= {
  "Marsha": 78,
  "Baker": 69,
  "Rosa": 92,
  "Leif": 97,
  "Peng": 61,
  "Juan": 73,
  "Esteban": 84,
  "Amir": 91,
  "Sakura": 99
}

scores = list(test_scores.values())
max_score = scores[0]

for student, score in test_scores.items():
  if max_score < score:
    max_score = score
    max_student = student

print(f"The highest score is {max_score} by {max_student}")
  
```


![calculate-max-student-and-score](/GCP_ML_pictures/Study-logs/Python/Fundamentals/dictionary-sets-tuple/calculate-max-student-and-score.PNG "calculate max student and score")



### Update and join dictionaries

- The update method will update a dictionary using the key-value pairs from a second dictionary, passed as the argument.


```
test_scores= {
  "Marsha": 78,
  "Baker": 69,
  "Rosa": 92,
  "Leif": 97,
  "Peng": 61,
  "Juan": 73,
  "Esteban": 84,
  "Amir": 91,
  "Sakura": 99
}

test_scores.update({'Yejin': 89, 'Roina': 100})
```


![update-dictionary](/GCP_ML_pictures/Study-logs/Python/Fundamentals/dictionary-sets-tuple/update-dictionary.PNG "update dictionary")


- You can join two dictionaries by using update, too:


![join-two-dictionaries](/GCP_ML_pictures/Study-logs/Python/Fundamentals/dictionary-sets-tuple/join-two-dictionaries.PNG "join two dictionaries")



- We can use two stars ** to combine multiple dictionaries into a new resulting dictionary.


```
dict1 = {"a": 1, "b": 2}
dict2 = {"c": 3, "d": 4}

dict3 = {**dict1, **dict2}

dict3 = {"a": 1, "b": 2, "c": 3, "d": 4}
```


![join-dictionaries-trick](/GCP_ML_pictures/Study-logs/Python/Fundamentals/dictionary-sets-tuple/join-dictionaries-trick.PNG "join dictionaries trick")



### Dictionary union

- Python 3.9 added the dict union operator (|). It will return a new dict containing the items from the left and the right dicts. In the case of duplicated keys, the right side "wins".


```
final_scores = test_scores | new_scores
```


![dictionary-union](/GCP_ML_pictures/Study-logs/Python/Fundamentals/dictionary-sets-tuple/dictionary-union.PNG "dictionary union")



### Dictionaries and Lists

- In real world, we often use nested dictionaries inside dictionaries.


```
produce = {
  "arugala": {
    "price": 3,
    "quantity": 60,
    "organic": True
    "producer": "yejin"
  }
}
```


- To access the "producer" of "arugala":


```
produce["arugala"]["producer"]
```


![nested-dictionaries](/GCP_ML_pictures/Study-logs/Python/Fundamentals/dictionary-sets-tuple/nested-dictionaries.PNG "nested dictionaries")


