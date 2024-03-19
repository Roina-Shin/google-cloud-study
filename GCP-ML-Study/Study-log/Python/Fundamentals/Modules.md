### [Source of this study material : One Week Python by Colt Steele](https://www.udemy.com/course/one-week-python/)


## Modules

- A module is simply a Python file that contains code that can be re-used in other files.


- Modules allow us to break up complex programs into smaller, more manageable pieces across multiple files.


- To use a module, we **must import** it first using the import keyword.



### Standard Library

- Python comes with tons of built-in modules that we can use, **if we import them**.


- Each module consists of methods and functionality bundled together.


- For example, you can import 'calendar' module. You can start with **calendar.weekday(*year, month, day*)** and enter in some date. **0 is Monday.**


```
import calendar

calendar.isleap(1988)

calendar.weekday(year, month, day)
```


![built-in-modules](/GCP_ML_pictures/Study-logs/Python/Fundamentals/modules/built-in-modules.PNG "built in modules")



### Import as

- Use the **as keyword** to import a module and give it a custom name in your script.


```
import random as rand

rand.randint(1,6)

4
```


### from... import

- Use the **from <module> import <method>** syntax to import specific pieces of a module.


```
from random import randint

randint(1,6)

2
```


## pip

- pip is the Python package installer that we can use to install hundreds of thousands of packages for use in our projects.



- The Python Package Index (PyPI) is a repository of a software for the Python programming language. To install a package, use python3 -m pip install followed by the exact name of the package.


```
python3 -m pip install <package>
```


- To practice, we will install some packages to do sentiment analysis.


```
pip install pyttsx3

pip install textblob

python -m textblob.download_corpora lite
```


- Then run this code. You will see some sentiment analysis result from the output:


```
from textblob import TextBlob

blob = TextBlob("I really hate you so much moron!")

print(blob.sentiment)
```


![sentiment-analysis](/GCP_ML_pictures/Study-logs/Python/Fundamentals/modules/sentiment-analysis.PNG "sentiment analysis")


- Now, you are prompting the user to enter some positive comment. If the user doesn't pass the threshold (< 0.5) it will keep prompting the user.


```
from textblob import TextBlob

wellness = input("Enter your wellness statement: ")
blob = TextBlob(wellness)

while blob.sentiment.polarity < 0.5:
    wellness = input("Be more positive, please: ")
    blob = TextBlob(wellness)

print("Thank your for your positive statement!")
```


![prompting-user](/GCP_ML_pictures/Study-logs/Python/Fundamentals/modules/prompting-user.PNG "prompting user")



- Then we will add a text-to-speech robot and make it read some texts outloud.


```
from textblob import TextBlob
import pyttsx3

engine = pyttsx3.init()
engine.say("Hello employee number 77886. We hope you had a great day of work. It's time to submit your employee wellness statement.")
engine.runAndWait()

wellness = input("Enter your wellness statement: ")
blob = TextBlob(wellness)

while blob.sentiment.polarity < 0.5:
    engine.say("Be more positive, please")
    engine.runAndWait()
    wellness = input("Enter your wellness statement: ")
    blob = TextBlob(wellness)

print("Thank your for your positive statement!")
engine.say("Employee number 77886, thank you for such a kind and positive statement. We appreciate you too. Have a great day.")
engine.runAndWait()
```


![text-to-speech](/GCP_ML_pictures/Study-logs/Python/Fundamentals/modules/text-to-speech.PNG "text to speech")








