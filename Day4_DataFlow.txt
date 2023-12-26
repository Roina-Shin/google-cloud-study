Dataflow is a managed service for executing a variety of data processing.

Data processing is taking some data and transforming it somehow.

Take some data > combine it with other data > enriched data set > Analyze

Dataflow will allow you to gain actionable insights from your data while lowering operational costs,
without the hassle of deploying, maintaining, or scaling infrastructure.

Dataflow automates provisioning and management of processing resources to minimize
latency and maximize utilization so that  you do not need to spin up instances.



* Apache Beam

Apache Beam is helpful to create the data processing pipeline.

Beam is a framework with bindings in both Python and Java that allow you to represent
data processing pipelines with actions for inputs and outputs as well as a variety of built-in
data transformations.



Pipeline is a unit which collects the data, process the data, and produce the output.

Data that flows through the pipeline is called PCollections.

Manipulations that happen on data in pipeline are called transformations.

Pipeline refers to the high-level container of a bunch of data processing operations.

Pipelines encapsulate all of the input and output data as well as the transformation steps
that manipuate data from the input to the desired output.

Pipelines themselves can have lots of configuration options, which allow them to be somewhat customizable.

PCollections can be either bounded or unbounded.

A bounded PCollection is one that you are sure won't go on forever.
Unbounded PCollection is a stream of data that's being generated in real time,
such as the temperature sensor.

PCollections themselves are immutable. 
Once you create a PCollection, you can't change its data.

* How to create a Apache Beam project with Maven and build an Apache Beam Pipeline

1) First, go to API & Services to enable DataFlow API.

2) After done, go to Storage and create an empty bucket in your Storage.

3) You can create a second bucket in your Storage.

4) Once done, go to Cloud Shell.

5) Paste this code to the window:

mvn archetype:generate \
-DarchetypeGroupId=org.apache.beam \
-DarchetypeArtifactId=beam-sdks-java-maven-archetypes-examples \
-DarchetypeVersion=2.37.0 \
-DgroupId=yejins-bigquery-study \
-DartifactId=yejins-bigquery-study \
-Dversion="0.1" \
-Dpackage=org.loony.dataflow \
-DinteractiveMode=false

6) run ls > you will see the DartifactId [yejins-bigquery-study] on the list

7) cd to that directory

8) Open cloud shell editor and head over to pom.xml file where includes GroupId, ArtifactId etc. we specified earlier.

9) Inside that file, you can also find dataflow runner profile:

<profile>
      <id>dataflow-runner</id>
      <!-- Makes the DataflowRunner available when running a pipeline. -->
      <dependencies>
        <dependency>
          <groupId>org.apache.beam</groupId>
          <artifactId>beam-runners-google-cloud-dataflow-java</artifactId>
          <version>${beam.version}</version>
          <scope>runtime</scope>
        </dependency>
      </dependencies>
    </profile>

10) Make a new file named DefaultAndCustomOptions.java inside of src > main > subprocess folder

11) paste the code of this url:

https://github.com/loonyuser/linkedinlearning/blob/main/Learning%20Dataflow/chapter-01/DefaultAndCustomOptions.java


12) After saving the file, go to the cloud shell and run the following:

mvn compile exec:java \
  -Dexec.mainClass=org.loony.dataflow.DefaultAndCustomOptions

13) You can modify the signature name by rerunning this query:

mvn compile exec:java \
  -Dexec.mainClass=org.loony.dataflow.DefaultAndCustomOptions \
  -Dexec.args="--project=yejins-bigquery-study \
  --signature=yejins-apache-study"


14) Create a new file named PriceConversion.java in the same directory as the previous one,
and paste the following code of this url:

https://github.com/loonyuser/linkedinlearning/blob/main/Learning%20Dataflow/chapter-01/PriceConversion.java


15) After savubg that to the file, head over to the cloud shell and execute:

----------------------------------


* How to use DataFlow service when processing files in Apache Beam


1) First go to Storage and create a bucket to provide input to your Apache Beam transformations,
and also to serve as a location to provide output to.

In this regard, you need 2 folders inside that bucket for input and output storage purposes.

2) In Input folder, place the 3 files (Order Details, Sales_April, Walmart) of the following url:

https://github.com/loonyuser/linkedinlearning/tree/main/Learning%20Dataflow/chapter-02

Change the bucket name in the file according to your situation.

3) Head over to the cloud shell and run the following query:

mvn compile exec:java \
  -Dexec.mainClass=org.loony.dataflow.ExtractDetails


4) After running this, go to your Buckets and look into the output_data folder.
You will see several files that are around of equal size that were processed in parallel.

----------------------------------

* How to use DataFlow runner

1) In the Cloud Shell, run the following query:
(Change the project name and bucket address accordingly)

mvn -Pdataflow-runner compile exec:java \
  -Dexec.mainClass=org.loony.dataflow.ExtractDetails \
  -Dexec.args="--project=yejins-bigquery-study  \
  --stagingLocation=gs://yejin-bucket/staging/ \
  --runner=DataflowRunner \
  --region=asia-northeast3"


  2) Head over to the Dataflow > Jobs page.

  You will see a job and its state.

  Refer to the picture uploaded in GCP_pictures folder in this repository.

  It allows us to monitor executions and also analyze various metrics with regards to job executions.

  3) To verify it did the job we required to, head over to the Cloud Storage.

  In your bucket, you will see that an additional folder named 'staging'/ was created.

  Also, more importantly, in your output_data folder, you will see a new file created.

  View the content to see what the output looks like.









