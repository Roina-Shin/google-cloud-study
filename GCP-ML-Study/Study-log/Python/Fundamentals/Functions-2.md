### [Source of this study material : One Week Python by Colt Steele](https://www.udemy.com/course/one-week-python/)


## Functions

### *args

- We can use the wildcard or * notation to write functions that accept any number of arguments.


```
def average(*args):
  total = 0
  for arg in args:
    total += arg
  return total/len(args)
```


- *args gathers all remaining arguments into a tuple. This way, you can iterate over this tuple (a collection of args), add them up, and calculate the average.



```
def average(*args):
    total = 0
    for arg in args:
        total += arg
    return total / len(args)


print(average(1,5,3,8,5,8,54,74,5,4,5,4,5,4,5,4,5,4,5,4))
```


![args-in-average](/GCP_ML_pictures/Study-logs/Python/Fundamentals/functions-2/args-in-average.PNG "args in average")



### **kwargs

- We can use the ** notation to write functions that accept **any number of keyword arguments**. kwargs would be a dictionary containing keyword arguements as key-value pairs.


```
def demo(**kwargs):
    print(kwargs)
```

```
def demo(**kwargs):
    for key, value in kwargs.items():
        print(key, value)


print(demo(yejin=88, colt=100, roina=90))
```


![kwargs](/GCP_ML_pictures/Study-logs/Python/Fundamentals/functions-2/kwargs.PNG "kwargs")



### Argument unpacking

- Turning sequences into separate args.


- Suppose you created an average function. You can pass individual numbers as arguments to the function, but you cannot pass a list directly into it. Ohterwise, it will cause a Type Error.



![type-error](/GCP_ML_pictures/Study-logs/Python/Fundamentals/functions-2/type-error.PNG "type error")



- The function expects individual arguments, not a single collection of numbers. 


- Instead, we can **unpack** the list into individual args using an asterisk (*).



![unpack-list](/GCP_ML_pictures/Study-logs/Python/Fundamentals/functions-2/unpack-list.PNG "unpack list")



```
scores = [99,84,59,43,68,36,75,36,85,33,78,38,75,86]

def count_fails(*args):
  count = 0
  for arg in args:
    if arg <= 50:
      count += 1
  return count

print(count_fails(*scores))

student_card = {'yejin': 83, 'stacey': 90, 'roina': 89, 'tim': 65, 'carlos': 96, 'cecelia': 77, 'juan': 75, 'jesse': 67}

def get_top_students(**kwargs):
    score_list = list(kwargs.values())
    max_score = score_list[0]
    for student, score in kwargs.items():
        if score > max_score:
            max_score = score
            max_student = student
    return print(f"The top student is {max_student} with a score of {max_score}")

get_top_students(**student_card)
```


![args-and-kwargs-set](/GCP_ML_pictures/Study-logs/Python/Fundamentals/functions-2/args-and-kwargs-set.PNG "args and kwargs set")


