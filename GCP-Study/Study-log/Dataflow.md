### [Source of this study material : Google Cloud Data Engineer by Ankit Mistry](https://www.udemy.com/course/google-cloud-gcp-professional-data-engineer-certification/)


## Cloud Dataflow

- Cloud version of Apache Beam (Batch + Stream)

- Managed service for variety of data processing

- Implement batch and streaming data processing jobs

- Serverless, horizontal autoscaling of workers


## How Dataflow works

- Write job in Java, Python, or Go

- Unified API for both batch + streaming data

- Dataflow works upon **Apache Beam**


  - Pipeline

    - A graph of transformations that a user contstructs to define data processing

  - Pcollection

    - Dataset or data stream in Beam

  - Ptransform

    - The operations executed within a pipeline

  - Runner

    - An execution engine


 ## How to use Dataflow


- First, go to dataflow and click **Create job from template**.


![dataflow-template](/GCP_pictures/Study-logs/dataflow/dataflow-template.PNG "Dataflow job creation")


- Simply go with **Word Count** for template and for output bucket, go to Cloud Storage and create a bucket.


![output-bucket](/GCP_pictures/Study-logs/dataflow/output-bucket.PNG "Output bucket")


- After you completed all the required parameters, click create.


![required-parameters](/GCP_pictures/Study-logs/dataflow/required-parameters.PNG "Required parameters")


- Once created, the job started running and it shows like below:


![job-started](/GCP_pictures/Study-logs/dataflow/dataflow-run-started.PNG "Dataflow job started")


- If all the steps have been succeeded like below:


![all-steps-succeeded](/GCP_pictures/Study-logs/dataflow/all-steps-succeeded.PNG "All steps succeeded")


- Go to Storage bucket and see if any output file is generated:


![output-file-generated](/GCP_pictures/Study-logs/dataflow/output-file.PNG "Output file generated")


![wordcount-result](/GCP_pictures/Study-logs/dataflow/wordcount-result.PNG "Wordcount result")


 ## How to use Dataflow with Notebook instance


- Go to Dataflow and click Workbench and create an instance.


![notebook-instance](/GCP_pictures/Study-logs/dataflow/notebook-instance.PNG "Notebook instance")


- After creating the instance, click **Open Jupyterlab**.


![open-notebook](/GCP_pictures/Study-logs/dataflow/notebook-open.PNG "Open Jupyyerlab")


- By default, Apache Beam and GCP extensions are already installed in this instance.


![notebook-opened](/GCP_pictures/Study-logs/dataflow/notebook-opened.PNG "Notebook opened")


- Create a brand new notebook. File > New > Notebook. And use Apache Beam notebook.


![new-notebook](/GCP_pictures/Study-logs/dataflow/new-notebook.PNG "New notebook created")


