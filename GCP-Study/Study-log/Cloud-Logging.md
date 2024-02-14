### [Source of this study material : Google Cloud Professional DevOps Engineer Certification by Ankit Mistry](https://www.udemy.com/course/gcp-google-cloud-professional-devops-engineer-certification/)


## Cloud Logging

- Log management tool


- Fully managed service


- Store exabyte scale data


- Logs can be collected from multiple sources


- Search & analyze logs



## Cloud Logging Demo

- When you go to Cloud Logging and filter it out with **system eventS**, there is no logs yet.


- To see what kind of logs is generated under **system events**, we will go to compute engine and create a preemtible VM. 


- In the Cloud Console, create a spot VM for preemptible VM.


![spot-vm-created](/GCP_pictures/Study-logs/cloud-logging/spot-vm-created.PNG "Spot VM created")


- As it is a preemptible VM, Google will take it back within 24 hours or so. And this will appear in the system generated logs.


