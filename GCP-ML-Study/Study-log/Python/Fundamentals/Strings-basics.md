### [Source of this study material : One Week Python by Colt Steele](https://www.udemy.com/course/one-week-python/)


## String Operator

### plus (+) is concatenation in strings

- "hello" + "world" will concatenate the 2 words and print 'helloworld'.



## Strings are indexed

- 'Hello': H is 0, e is 1, l is 2, l is 3, o is 4.


![string-index](/GCP_ML_pictures/Study-logs/Python/Fundamentals/strings/string-index.PNG "String index")



## Slices

- 'Hello world': 'hello world'[2:6]


- In the string, starting in index 2 and ending in index 6 (not including 6).


![slices](/GCP_ML_pictures/Study-logs/Python/Fundamentals/strings/slices.PNG "Slices")


- Slicing is useful when you want to extract specific value from the data.


![extract-data](/GCP_ML_pictures/Study-logs/Python/Fundamentals/strings/extract-data.PNG "Extract data")



## Escape Characters

### New line - \n


![escape-character-newline](/GCP_ML_pictures/Study-logs/Python/Fundamentals/strings/escape-character-newline.PNG "Escape character - new line")



## Triple Quotes

- Triple quotes are used to write multiple line sentences. 


![triple-quotes](/GCP_ML_pictures/Study-logs/Python/Fundamentals/strings/triple-quotes.PNG "Triple quotes")



## Strings and Functions

- **Functions** are reusable actions that have a name.



### The Len() Function

- The **len()** function will return the length of whatever item we pass to it.


![len-function](/GCP_ML_pictures/Study-logs/Python/Fundamentals/strings/len-function.PNG "len function")



### The Input() Function

- The **input()** function will prompt a user to enter some input, convert it into a string, and then return it. We can use it to gather inputs in our programs.


![input-function](/GCP_ML_pictures/Study-logs/Python/Fundamentals/strings/input-function.PNG "input function")


- You can use it to interact with users by asking them a question and use the answer later.


![input-function2](/GCP_ML_pictures/Study-logs/Python/Fundamentals/strings/input-function2.PNG "input function2")


- What you need to remember about input function is that even if the user inputs an integer, it will be stored as **string**.



### Change types

- If you need to change the type (e.g. string to integer) you can use:


![change-type](/GCP_ML_pictures/Study-logs/Python/Fundamentals/strings/change-type.PNG "Change type")



- You can create an age program like this by changing the types.


![age-program](/GCP_ML_pictures/Study-logs/Python/Fundamentals/strings/age-program.PNG "Age program")



## f strings

- f-strings are an easy way to generate strings that contain interpolated expressions. Any code between **curly braces {}** will be evaluated and then the result will be turned to a string and inserted into the overall string.


![f-strings](/GCP_ML_pictures/Study-logs/Python/Fundamentals/strings/f-strings.PNG "f strings")


- You can apply the f string to your age program.


![age-program-with-f-string](/GCP_ML_pictures/Study-logs/Python/Fundamentals/strings/age-program-with-f-string.PNG "age program with f string")



- You can make a shopping cart program like this:


```
print("WELCOME TO OUR USELESS STORE!")
print("*"*20)

item_input = input("What item are you purchasing?")

item_price = int(input(f"Ok. What is the price of {item_input}?"))

item_count = int(input(f"How many {item_input} are you buying?"))

print(f"Added {item_count} {item_input}(s) to shopping cart.")

print(f"Subtotal: ${item_count * item_price}")
```


![shopping-cart-program](/GCP_ML_pictures/Study-logs/Python/Fundamentals/strings/shopping-cart-program.PNG "Shopping cart program")
