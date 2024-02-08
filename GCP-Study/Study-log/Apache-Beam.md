### [Source of this study material : Google Cloud Data Engineer by Ankit Mistry](https://www.udemy.com/course/google-cloud-gcp-professional-data-engineer-certification/)


## Apache Beam

- Top level Apache Open Source project

- Started in 2016

- Apache Beam is a unified programming model that can build portable big data pipelines

- Unified API to process both batch & streaming data

- **B**atch + Str**eam** = Beam

- Beam supports Python, Java, Go

- Once your pipeline is created, it can be executed on any execution framework


## How to use Apache Beam

- In your Cloud Shell, run the command:


```
python3
```

```
import apache_beam
```

- If error occurs, install command is:


```
pip3 install apache beam
```

- But we will go with the other option this time. Go to Google Colab and create a New Notebook.


- Run the command on the notebook with **shift + enter**:


```
import apache_beam
```


![error-not-found](/GCP_pictures/Study-logs/apache-beam/first-notebook.PNG "Error not found")



- You can simply install it by using linux command like below:


```
!pip3 install apache-beam
```


![pip-apache-beam-install](/GCP_pictures/Study-logs/apache-beam/pip-apache-install.PNG "Apache Beam install")


- Run the command to verify:


```
import apache_beam
```

- If no error, then your installation finished successfully.


- Now run the code first:


```
import apache_beam as beam
```

- And as we want to display data, we want to install **interactive runner**:


```
from apache_beam.runners.interactive.interactive_runner import InteractiveRunner
```


- **To create a Pipeline** object with no other steps defined so far:


```
p1 = beam.Pipeline(InteractiveRunner())
```

- Once done, run this command to verify the type of p1:


```
type(p1)
```


![beam-pipeline](/GCP_pictures/Study-logs/apache-beam/pipeline-creation.PNG "Beam Pipeline creation")


- Next, run the code:


```
from apache_beam import Create, Map
```


- Now, what we are going to define in the pipeline:

  - create a range consisting of 10 elements (from 0 to 10)

  - then, find out the **cube number** of these elements


- To do that, we create a pipeline named cubes:


```
cubes = (p1
        | "Create element" >> Create(range(10))
        | "Find cube" >> Map(lambda x : x**3))
```


![pipeline-definition](/GCP_pictures/Study-logs/apache-beam/pipeline-definition.PNG "Pipeline definition")


- To execute the pipeline:


```
p1.run()
```

- When you print **cubes**, it still is just pcollection. 


```
print(cubes)
```


![pcollection-cubes](/GCP_pictures/Study-logs/apache-beam/pcollection-cubes.PNG "Pcollection cubes")



- To show graph of the pipeline we defined:


```
import apache_beam.runners.interactive.interactive_beam as ib
```

```
ib.show_graph(p1)
```


![show-graph](/GCP_pictures/Study-logs/apache-beam/show-graph.PNG "Show graph of pipeline")



- But when you try to display the array, it shows no content:


```
ib.show(cubes)
```


![error](/GCP_pictures/Study-logs/apache-beam/error.PNG "Show no content")



- If the error like above happens, bundle all code in one snippet and re-run it in the new notebook:


```
!pip3 install apache-beam
import apache_beam as beam
from apache_beam.runners.interactive.interactive_runner import InteractiveRunner

p1 = beam.Pipeline(InteractiveRunner())
from apache_beam import Create, Map
cubes = (p1
        | "Create element" >> Create(range(10))
        | "Find cube" >> Map(lambda x : x**3))
p1.run()
import apache_beam.runners.interactive.interactive_beam as ib
ib.show(cubes)
```


![code-visualization](/GCP_pictures/Study-logs/apache-beam/code-visualization.PNG "Cubes visualization")


- Or, more simply, you can run this:


```
import apache_beam as beam
from apache_beam import Create, Map

p1 = beam.Pipeline()
cubes = (p1
        | "Create element" >> Create(range(10))
        | "Find cube" >> Map(lambda x : x**3)
        | "Print" >> Map(print))
p1.run()
```


![simple-code](/GCP_pictures/Study-logs/apache-beam/simple-code.PNG "Simple code")



## Various Apache Beam functions

### Create


```
import apache_beam as beam
from apache_beam import Create, Map

p1 = beam.Pipeline()
cubes = (p1
        | "Create element" >> Create([1,5,8])
        | "Find cube" >> Map(lambda x : x**3)
        | "Print" >> Map(print))
p1.run()
```


![new-list](/GCP_pictures/Study-logs/apache-beam/new-list.PNG "New list creation")



- We can use **lambda x** in strings as well like below:


![lambda-x](/GCP_pictures/Study-logs/apache-beam/lambda-x-function.PNG "Lambda x used in strings")


- You can even use lambda in dictionary format too. **lambda x : x[0]** means to grab the first keys in the key-value pairs.


![lambda-in-dictionary](/GCP_pictures/Study-logs/apache-beam/dictionary-lambda.PNG "Lambda in dictionary")



### Flatten


- With Flatten function, we can **combine 2 arrays** like below:


```
import apache_beam as beam

p1 = beam.Pipeline()

even = {2,4,6,8}
odd = {1,3,5,7,9}

even_p1 = p1 | "Even numbers" >> beam.Create(even)
odd_p1 = p1 | "Odd numbers" >> beam.Create(odd)

flat_out = (even_p1, odd_p1) |  beam.Flatten() | beam.Map(print)

p1.run()
```


![flatten](/GCP_pictures/Study-logs/apache-beam/flatten-function.PNG "Flatten in beam")



### MAP / FlatMap


- You can define a function and use **map** to print out the function.


```
import apache_beam as beam
from apache_beam import Create, Map

def findcube(element):
  return element ** 3

p1 = beam.Pipeline()

findcube = (p1
            | "Create Element" >> Create([1,3,5,7])
            | "Fine Cube" >> Map(findcube)
            | "Print" >> Map(print)
            )

p1.run()
```


![map-function](/GCP_pictures/Study-logs/apache-beam/map-function.PNG "Map function")



- FlatMap returns every value as completely separate things. Even if it was the same string, the split words are now separate values.


```
import apache_beam as beam
from apache_beam import Create, Map, FlatMap

p1 = beam.Pipeline()

string_split = (p1
            | "Create Element" >> Create(["yejin gcp specialist", "eunjung python programmer"])
            | "String split" >> FlatMap(str.split)
            | "Print" >> Map(print)
            )

p1.run()
```


![flatmap-function](/GCP_pictures/Study-logs/apache-beam/flatmap-function.PNG "Flatmap function")



### Filter


- Apply the filter function on integer values:



![filter-integer](/GCP_pictures/Study-logs/apache-beam/filter-integer.PNG "Filter on integer values")



- You can also apply the filter on string values:


![filter-string](/GCP_pictures/Study-logs/apache-beam/string-filter.PNG "Filter on string values")



### ParDo


- ParDo does exactly the same thing as FlatMap.


![pardo-function](/GCP_pictures/Study-logs/apache-beam/pardo-function.PNG "ParDo is similar to FlatMap")



### KvSwap


- KvSwap swaps Key-Value pairs like below:


![kvswqp](/GCP_pictures/Study-logs/apache-beam/kvswqp.PNG "How KvSwaps works")



### Partition


- Import sympy:


```
%pip install sympy
```


```
import sympy
```


- We will see that if a certain number is **prime number** or not. The prime number is only divisible by 1 or the number itself. 


```
import apache_beam as beam
from apache_beam import Create, Map

p1 = beam.Pipeline()

def is_prime_function(element, no_par):
  return 1 if sympy.isprime(element) else 0

is_prime = (p1
            | "Create element" >> Create(range(1,100))
            | "Partition" >> beam.Partition(is_prime_function, 2)
            )
is_prime[1] | "Print Prime Number" >> Map(print)
p1.run()
```


- If is_prime[0], then it will return non-prime numbers. 



![prime-return](/GCP_pictures/Study-logs/apache-beam/prime-number-return.PNG "Return prime numbers")



### Regular Expression (Regex)


- Regex expression like **(\d+)** signifies to grab all the **decimal** values with one or more than one occurences.



![regex-in-beam](/GCP_pictures/Study-logs/apache-beam/regex-in-beam.PNG "Regex in beam")



### Aggregation


- Combiners let you use **count** function.


```
import apache_beam as beam
from apache_beam import Create, Map

p1 = beam.Pipeline()

Aggregation_test = (p1
             | "Create element" >> Create(["1", "23", "Hello","Yejin"])
             | "Count" >> beam.combiners.Count.Globally()
             | "Print" >> Map(print) 
              )

p1.run()
```


![combiners-example](/GCP_pictures/Study-logs/apache-beam/combiners-example.PNG "Combiners example")



- Add all the values in the range together:


```
import apache_beam as beam
from apache_beam import Create, Map

p1 = beam.Pipeline()

Aggregation_test = (p1
             | "Create element" >> Create(range(20))
             | "Sum" >> beam.CombineGlobally(sum)
             | "Print" >> Map(print) 
              )

p1.run()
```


![sum-in-beam](/GCP_pictures/Study-logs/apache-beam/sum-beam.PNG "Sum in beam")


