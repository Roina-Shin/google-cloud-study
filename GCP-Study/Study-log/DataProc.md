### [Source of this study material : Google Cloud Data Engineer by Ankit Mistry](https://www.udemy.com/course/google-cloud-gcp-professional-data-engineer-certification/)


## Dataproc

- Managed **Hadoop & Spark** services inside GCP

- Cluster type:

  - Standard (1 master, N workers)

  - Single node (1 master, 0 worker)

  - High availability (3 masters, N workers)


- Job supported:

  - Hadoop, PySpark, Notebook instance


## How to use Dataproc


- First, enable the Dataproc API and click create a cluster.


![create-cluster](/GCP_pictures/Study-logs/dataproc/create-a-cluster.PNG "Create a cluster")



- Once the Dataproc cluster is ready, we can submit a new job.


### Submit a Spark job


- To submit a Spark job, we need to provide the Spark source code:

1. **Main class or jar**

```
org.apache.spark.examples.SparkPi
```

2. **Jar files**

```
file:///usr/lib/spark/examples/jars/spark-examples.jar
```

- After configuring all, submit a Spark job:


![submit-a-job](/GCP_pictures/Study-logs/dataproc/submit-a-job.PNG "Submit a job")



- Once the job is succeeded, you get the pi value:


![job-succeeded](/GCP_pictures/Study-logs/dataproc/job-succeeded.PNG "Job succeeded")



### Submit a PySpark job


- To submit a PySpark job, prepare a python file like below and upload it to GCS.


```
#! /usr/bin/python
import pyspark
sc = pyspark.SparkContext()
rdd = sc.parallelize(['Hello', 'World!'])
words = sorted(rdd.collect())
print(words)
```

- Grab the location of the PySpark job file and paste it to the Dataproc Job Submit page.


![pyspark-file](/GCP_pictures/Study-logs/dataproc/pyspark-file.PNG "PySpark file")



![paste-location](/GCP_pictures/Study-logs/dataproc/paste-location.PNG "Paste the location")



- But when I tried, the job failed multiple times due to some SparkContext issue.


- Let me go to Compute Engine and to one of the Dataproc VMs. And SSH into it.


```
pyspark
```


![pyspark-vm](/GCP_pictures/Study-logs/dataproc/pyspark-shell.PNG "PySpark command in VM")



- Then enter all the remaining PySpark code we used earlier.


```
import pyspark
```

```
rdd = sc.parallelize(['Hello', 'World!']) 
words = sorted(rdd.collect()) 
print(words)
```


![job-executed](/GCP_pictures/Study-logs/dataproc/job-executed.PNG "Job executed")