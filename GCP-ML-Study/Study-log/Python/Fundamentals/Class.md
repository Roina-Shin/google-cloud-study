### [Source of this study material : One Week Python by Colt Steele](https://www.udemy.com/course/one-week-python/)


## Class

- A class contains a special **init method** that is automatically called whenever new <class name> is created. The below example is to show how to create a new class and instantiate a new instance inside that class.


```
class Dog:
    def __init__(self, name, breed, location):
        self.name = name
        self.breed = breed
        self.location = location
        self.tricks = []

    def add_trick(self, new_trick):
        self.tricks.append(new_trick) 


# Let's instantiate a new dog!

tina = Dog('tina', 'corgi', 36536)
```


![creating-new-class](/GCP_ML_pictures/Study-logs/Python/Fundamentals/class/creating-new-class.PNG "creating a new class")



- A class is a layout that describes what objects (data, functionalities, etc.) a given instance contains. You can add a new instance method like 'add_trick'.



```
class Dog:
  def __init__(self, name, breed, location):
      self.name = name
      self.breed = breed
      self.location = location
      self.tricks = []

  def add_trick(self, new_trick):
      if new_trick not in self.tricks:
          self.tricks.append(new_trick) 


tina = Dog("Tina", "Terrier", "NYC")

tina.add_trick("sit")
tina.add_trick("roll over")

print(f"Tina can do {tina.tricks}")
```


![practicing-instance-methods](/GCP_ML_pictures/Study-logs/Python/Fundamentals/class/practicing-instance-methods.PNG "Practicing instance methods")



- To define an attribute that is commonly applied to all instances in the class:


```
class Dog:

  species = 'canine'

  def __init__(self, name, breed, location):
      self.name = name
      self.breed = breed
      self.location = location
      self.tricks = []
```


![define-attribute](/GCP_ML_pictures/Study-logs/Python/Fundamentals/class/define-attribute.PNG "define attribute")


-  To track the number of a newly added dog (def __init__()), you can put a shared variable **num_dog = 0** at the top and add **num_dog += 1** to the function:


```
class Dog:

  species = 'canine'
  num_dog = 0
  
  def __init__(self, name, breed, location):
      self.name = name
      self.breed = breed
      self.location = location
      self.tricks = []
      Dog.num_dog += 1

  def add_trick(self, new_trick):
      if new_trick not in self.tricks:
          self.tricks.append(new_trick) 


tina = Dog("Tina", "Terrier", "NYC")

tina.add_trick("sit")
tina.add_trick("roll over")

print(f"Tina is a {tina.species}")
print(f"Tina can do {tina.tricks}")
print(f"Tina's number is {tina.num_dog}")


tim = Dog("Tim", "Poodle", "CA")

print(f"Tim's number is {tim.num_dog}")
```


![tracking-number](/GCP_ML_pictures/Study-logs/Python/Fundamentals/class/tracking-num.PNG "tracking number")


