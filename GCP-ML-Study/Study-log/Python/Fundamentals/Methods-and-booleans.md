### [Source of this study material : One Week Python by Colt Steele](https://www.udemy.com/course/one-week-python/)


## Methods

- Methods are functions that "live" on objects.


```
thing.method()
```


- For example, we have string methods like following:


```
str.capitalize()
str.endswith()
str.find()
str.join()
str.lower()
str.removeprefix()
str.replace()
str.split()
str.rfind()
str.rindex()
str.rjust()
str.startswith()
str.strip()
str.swapcase()
str.title()
str.upper()
```


![method-example](/GCP_ML_pictures/Study-logs/Python/Fundamentals/methods-and-booleans/methods-example.PNG "method example")



- Capitalize method is very useful as it capitalizes the first letter and then lower cases all the rest.


![capitalize-method](/GCP_ML_pictures/Study-logs/Python/Fundamentals/methods-and-booleans/capitalize-method.PNG "Capitalize method")



- The upper method, for example, doesn't aceept any arguments inside the parenthesis (). Like this:


```
string.upper()
```


- And **strip method** can have various arguments. The classic string method may not need any arguments like below. It will strip away all the trailing spaces or characters:



![classic-strip-method](/GCP_ML_pictures/Study-logs/Python/Fundamentals/methods-and-booleans/classic-strip-method.PNG "Classic strip method")



- Strip method has 2 derivatives: **lstrip** and **rstrip**.



![strip-method](/GCP_ML_pictures/Study-logs/Python/Fundamentals/methods-and-booleans/strip-method.PNG "strip methods")



- The **replace method** replaces the old string into a new string in the parenthesis.



```
string.replace([old string], [new string])
```


![old-and-new-string](/GCP_ML_pictures/Study-logs/Python/Fundamentals/methods-and-booleans/old-new-string.PNG "replace method")



- The **find method** tries to find a character in the general string and returns the index number of that particular string. If there are multiple same characters in the string, then it will return the first occuring character's index number.



![find-method](/GCP_ML_pictures/Study-logs/Python/Fundamentals/methods-and-booleans/find-method.PNG "find method")



- You can **chain methods** together like below:


![method-chaining](/GCP_ML_pictures/Study-logs/Python/Fundamentals/methods-and-booleans/method-chaining.PNG "method chaining")




## Booleans

- Booleans are another basic Python type. There are only two possible values: True and False. Notice the capitalization.


![booleans](/GCP_ML_pictures/Study-logs/Python/Fundamentals/methods-and-booleans/booleans.PNG "booleans")



- There are basic comparison operators:

  - **>** Greater than

  - **<** Less than

  - **>=** Greater than or equal to

  - **<=** Less than or equal to

  - **==** Equal to

  - **!=** Not equal to


  ![true-and-false](/GCP_ML_pictures/Study-logs/Python/Fundamentals/methods-and-booleans/true-and-false.PNG "true and false")



  ### The "in" operator

  - The "in" operator looks to see if an item is a member of a sequence. 


  ![in-operator](/GCP_ML_pictures/Study-logs/Python/Fundamentals/methods-and-booleans/in-operator.PNG "in operator")


  - You can use "in" operator in the list as well:


  ![in-operator-on-list](/GCP_ML_pictures/Study-logs/Python/Fundamentals/methods-and-booleans/in-operator-in-list.PNG "in operator on list")


  




