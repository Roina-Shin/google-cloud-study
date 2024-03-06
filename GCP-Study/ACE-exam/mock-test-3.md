### [Source of this study material : GCP Associate Cloud Engineer Practice Test Exam by Sayyam](https://www.udemy.com/course/latest-gcp-ace-google-associate-cloud-engineer-practice-exams-tests)


## Exam -3

### 1. Google Cloud Monitoring Alerts

- CASE: You have received some complaints from your users that they are experiencing high latency at random intervals in your app, hosted on Comute Engine. In order to check what is going on, your team needs to be monitoring the app at the time when the latency is high. WWhat solution can you use on Google Cloud to notify your team if the latency is increased for 5 minutes?


- Solution: Develop an altert policy to trigger notifications when the HTTP response latency surpasses the predetermined threshold. 


- Creating an alert policy to send a notification when the HTTP response latency exceeds the specified threshold is a Google recommended solution with no development cost. This solution directly addresses the requirement of automatically notifying the support team when high latency is experienced by users for at least 5 minutes.



### 2. Google Cloud Storage and Dataflow

- CASE: Your team is building a Dataflow job on Google Cloud to process large quantities of unstructured data in multiple file formats using the ETL process. What should you do to make the data accessible to the Dataflow job?


- Solution: Store the data in Cloud Storage through the employment of the gcloud storage command.


- Uploading the data to Cloud Storge using the gcloud storage command allows for efficient handling of large quantities of unstructured data in different file formats. Cloud Storage is designed to store and manage objects, such as files, and provides high scalability, durability, and accessibility. By uploading the data to Cloud Storage, it can then be easily processed by a Dataflow job.



### 3. Cloud Function and Storage Buckets

- CASE: You are building a translation software that needs to extract text from audio files stored in Cloud Storage by using the Speech-to-Text API. In order to reduce development effort you are looking for a fully managed, serverless compute solution that requires authentication and follows Google-recommended practices. Your API should get called automatically whenever a new file is uploaded in the bucket. Which option is most suitable?


- Solution: Deploy a Cloud Function triggered by Cloud Storage bucket events to submit the file URI to the Google Speech-To-Text API.


- Deploying a Cloud Function triggered by Cloud Storage bucket events is a serverless and fully managed solution. Cloud Functions are designed to execute in response to various events, including Cloud Storage bucket events. This approach eliminates the need for manual scanning or continuous polling for new files, making it more efficient and cost-effective. Cloud Functions provide automatic authentication using the associated service account, following the Google recommended practices.



### 4. Cloud Run and Docker container

- CASE: You are running an e-commerce platform in your on-premises data center, that is based on multiple microservices built in Python, with each microservice running in its own Docker container. The app uses environment variables to manage configurations. How can you deploy such an application on a serverless solution on Google Cloud such that you need to make very few changes in code?


- Solution:

1. Employ your current CI/CD workflow.

2. Utilize the creataed Docker images and initiate deployment on Cloud Run.

3. Revise the settings and necessary access points accordingly.


- It utilizes the existing CI/CD pipeline and deploys the Docker images to Cloud Run. This option allows for easy migration of the current application to a serverless solution in Google Cloud. The configurations and endpoints can be updated to match the new environment.



### 5. Artifact Registry

- CASE: Your team is modernizing a legacy application by leveraging Docker. What should you choose to deploy this application on Google Cloud such that the team does not need to manage infrastructure and the app can scale well if it gains popularity?


- Solution: Move Docker images to Artifact Registry, and carry out the deployment of the application on Cloud Run.


-  It suggests uploading Docker images to Artifact Registry and deploying the application on Cloud Run. Cloud Run is a managed compute platform that automatically scales your containers based on incoming requests or events. This ensures that your application can scale automatically as it gains popularity, without the need to manage the underlying infrastructure.



### 6. Optimize the GKE Cluster for reliability

- CASE: Your team is trying to migrate a business-critical application to Google Kubernetes Engine. What steps would you recommend to optimize the cluster for reliability?


- Solution: Establish a GKE Autopilot cluster and choose to enroll the cluster in the stable release channel.


- Creating a GKE Autopilot cluster and enrolling it in the stable release channel would be the recommended practice for provisioning a Kubernetes cluster for a business-critical application. Autopilot clusters provide automatic scaling, management, and reliability, while the stable release channel ensures that the cluster receives tested and stable updates. This combination offers a balance between reliability and up-to-date features.



### 7. A separate node pool with a specific machine type

- CASE: You have built a complex microservices-based app on Kubernetes Engine. One of the microservices, which is responsible for rendering images, requires a large amount of CPU time and an average amount of memory. The cluster is made up of n2-type nodes which are suitable for the other microservices. How can you optimize your cluster to ensure efficient usage of resources?


- Solution: Establish a separate node pool composed of compute-optimized machine-type nodes for the image rendering microservie while employing a distinct node pool with general-purpose machine-type nodes for the other microservices.


- Creating a separate node pool with compute-optimized machine-type nodes specifically for the image rendering microservice will ensure that it has access to the CPU resources it needs while not affecting the performance of the other microservices.



### 8. Cloud Run and splitting customer traffic

- CASE: You are running a customer-facing application on Cloud Run in production. How can you make sure that only a limited number of customers get affected by an outage whenever there is a new release while making sure that development or operational costs to your customers are as low as possible?


- Solution: Split customer traffic between the revisions and gradually roll out the release to allow rollaback in case a problem occurs.


- Splitting customer traffic between revisions allows for a controlled and gradual rollout. This approach minimizes the impact on a limited number of customers initially, enabling monitoring and validation before a full release. If issues arise, you can rollback the release for the affected customers without affecting the entire user base.


### 9. Avoid zonal failure and achieve high availability

- CASE: You are building a news website that is going to be accessed from all over the world. You need to build the architecture on Google Cloud such that the app is able to withstand a zonal failure. What can help you achieve this kind of high availability?


- Solution:

1. Place the application data onto a persistent disk with a regional scope.

2. In the event of an outage, establish a new instance in a different zone and connect this disk to ensure continuity.


- It utilizes a regional persistent disk, which is automatically replicated across two zones within a region, providing built-in redundancy and high availability. In the event of a zonal outage, the application data remains accessible as the persistent disk can be attached to a new instance in a different zone without the need for manual data restoration processes. This ensures that the application can withstand a zonal failure with minimal downtime and no data loss, making it the best option for achieving high availability for the app.



### 10. Service account security

- CASE: You need a quick solution to limit the lifetime of service account credentials in your company with the following requirements:

Only a project called pj-sa will host all service accounts that require a key.

Service account keys should expire automatically after one day.

What is a cost-effective solution for the above requirements?


- Solution:

- Enact an organization policy that enforces a 24-hour limit on the lifespan of service account keys.

- Additionally, apply a policy to prevent the creation of service account keys, except for pj-sa.




### 11. Gradual Rollout for Revisions

- CASE: Your company is exploring serverless technologies for their new E-commerce website. The requirement is that you need to be able to test a new version of the application with a small percentage of production traffic. Which option is most suitable?


- Solution:

1. Use Cloud Run to deploy your application.

2. Enable traffic splitting and gradual rollouts.


- Gradual rollout for revisions


1. Deploy a revision, initially setting it to receive no traffic.


```
gcloud run deploy --image IMAGE --no-traffic
```


2. Specify the percentage of traffic you want the new revision to handle, for example, 5 percent:


```
gcloud run services update-traffic SERVICE --to-revisions LATEST=5
```


3. Split traffic between multiple revisions.


```
gcloud run services update-traffic SERVICE --to-revisions hello2-00005-red=25,hello2-00001-bod=25,hello2-00002-nan=50
```


4. Send all traffic to the latest revision.


```
gcloud run services update-traffic SERVICE --to-latest
```


![revisions-manage-traffic](/GCP_pictures/ACE-exam/mock-test-3/revision-manage-traffic.PNG "Manage traffic between revisions")



### 12. Link a project to a billing account

- **Permissions required for this task**

To change the Cloud Billing account for a project, you need to be able to move a project from one Cloud Billing account to another. To accomplish this task, you need permissions adequate to unlink the project from the current Cloud Billing account AND to link the project to the target Cloud Billing account.

You need both project permissions and billing account permissions. These predefined roles have adequate permissions to perform this task:

On the project: **Project Billing Manager + Project Viewer OR Project Owner**

AND

On the current and target Cloud Billing account: **Billing Account User + Billing Account Viewer OR Billing Account Administrator**

**Using an Organization?** If you are set up to use an Organization to manage your Google Cloud resources and manage Organization billing accounts, then the **Billing Account Administrator** role granted at the Organization level will have adequate permissions to perform this task.



### 13. Link a project to a billing account

- CASE: Your organization requires you to configure proxy settings in order to use the internet from your workstation. After installing the Google Cloud CLI, how can you make sure that your proxy credentials are not recorded in the gcloud CLI logs?


- Solution: Set the CLOUDSDK_PROXY_USERNAME and CLOUDSDK_PROXY_PASSWORD environment variables in your command line tool.


- Setting the CLOUDSDK_PROXY_USERNAME and CLOUDSDK_PROXY_PASSWORD environment variables in your command line tool is a common and secure practice to provide proxy credentials without storing them in plaintext in configuration files or logs. Using environment variables helps prevent accidental exposure of sensitive information.


- When you are behind a corporate proxy or firewall, the Google Cloud CLI might not be able to access the Internet with its default settings. In that case, you need to configure proxy settings in order to use the Internet from your workstation.


- First, set the type of proxy you are using and the address and port on which to reach it:


```
gcloud config set proxy/type [PROXY_TYPE]

gcloud config set proxy/address [PROXY_IP_ADDRESS]

gcloud config set proxy/port [PROXY_PORT]
```


- For an authenticated proxy, you will need to set your proxy username and password using properties as follows:


```
gcloud config set proxy/username [USERNAME]

gcloud config set proxy/password [PASSWORD]
```


- Alternatively, to avoid having the proxy credentials recorded in any logs (such as shell history or gcloud CLI logs) or in the gcloud CLI configuration file, you can set the properties using environment variables, as shown in the following sample:


```
export CLOUDSDK_PROXY_USERNAME [USERNAME]

export CLOUDSDK_PROXY_PASSWORD [PASSWORD]
```


- The gcloud CLI won't store these values. This way, the credentials can be stored in an encrypted file locally, or they can be stored in a secure network location and retrieved when necessary.



### 14. Compute Engine VM

- CASE: You have a locally hosted data analytics toolkit, consisting of executable files, that handles data files in memory for roughly 50 minutes each night. The data can be from 1 gigabyte to 20 gigabytes in size. What steps should you take to transition this to Google Cloud with minimal effort and cost?


- Solution:

- Transition the entire setup to a virtual machine hosted on Compute Engine.

- Implement an instance schedule to initiate and terminate the VMs as needed.


- Lifting and shifting the application to a virtual machine (VM) on Compute Engine and using an instance schedule to start and stop the instance would allow you to migrate the application with minimal effort and cost. Compute Engine provides virtual machines that can run various workloads, including long-running tasks like data analytics. By using an instance schedule, you can automate the start and stop times of the VM to align with the data analytics process. This approach keeps the application architecture intact while taking advantage of the scalability and flexibility of Google Cloud.



### 15. How Cloud Shell works

- CASE: You are using Cloud Shell to build and deploy your crypto-wallet webapp. Your webapp needs a custom utility to build and you need to make sure it is in the default execution path and persists across sessions. Where should you store it?


- Solution:  ~/bin


- In the context of Google Cloud Platform's Cloud Shell, the home directory (denoted as ~) is persistent across sessions. This means that any files or directories you place within it, including a custom ~/bin directory for executable scripts or utilities, will remain available across Cloud Shell sessions. By placing your custom utility in ~/bin and ensuring this directory is included in your PATH environment variable, you can achieve both persistence and easy accessibility. Cloud Shell is designed to retain the contents of your home directory, making ~/bin a suitable location for tools and scripts you wish to keep readily accessible.


 
### 16. GKE Cluster get credentials

- CASE: You are learning Google Cloud concepts and you created 2 GKE clusters using the gcloud container clusters command.



- cluster-1 is a standard cluster

- cluster-2 is an auto-pilot cluster.



You are able to only see the nodes from cluster-1 when you run the kubectl get nodes command. Which commands can help you check the node status for cluster-2?


- Solution:

- gcloud container clusters get-credentials cluster-2

- kubectl get nodes


- It first fetches the credentials for the cluster-2 using the gcloud container clusters get-credentials command. This command updates the kubeconfig file with the necessary information and authentication credentials for accessing the cluster-2. Then, the kubectl get nodes command is used to check the node status for the cluster-2.



### 17. Lob-based metrics

- CASE: Your company recently had a security incident and now they have employed a dedicated security team that monitors what is happening in the Google Cloud environment. The security team needs to monitor unexpected firewall changes and instance creation. Which is a simple solution that can be provided to the Security team?


- Solution:

1. Create log-based metrics for firewall and instance actions using Cloud Logging Filters.

2. Set up reasonable alerts to monitor the changes.


- **Log result using firewalls.insert**


```
{
  "protoPayload": {
    "@type": "type.googleapis.com/google.cloud.audit.AuditLog",
    "authenticationInfo": {
      "principalEmail": "service-195817460494@container-engine-robot.iam.gserviceaccount.com"
    },
    "requestMetadata": {
      "callerIp": "private",
      "callerSuppliedUserAgent": "google-api-go-client/0.5 GoogleContainerEngine/v1",
      "requestAttributes": {},
      "destinationAttributes": {}
    },
    "serviceName": "compute.googleapis.com",
    "methodName": "v1.compute.firewalls.insert",
    "resourceName": "projects/devops-project-yj/global/firewalls/gke-standard-public-cluster-1-a073f674-inkubelet",
    "request": {
      "@type": "type.googleapis.com/compute.firewalls.insert"
    }
  },
  "insertId": "-dl9hmre1i3ge",
  "resource": {
    "type": "gce_firewall_rule",
    "labels": {
      "project_id": "devops-project-yj",
      "firewall_rule_id": "866871467450502233"
    }
  },
  "timestamp": "2024-03-02T05:01:46.274985Z",
  "severity": "NOTICE",
  "labels": {
    "compute.googleapis.com/root_trigger_id": "2457180e-ad02-44a9-822e-ad771e1c5ee3"
  },
  "logName": "projects/devops-project-yj/logs/cloudaudit.googleapis.com%2Factivity",
  "operation": {
    "id": "operation-1709355701816-612a66366cb01-2cbd9c19-276b5716",
    "producer": "compute.googleapis.com",
    "last": true
  },
  "receiveTimestamp": "2024-03-02T05:01:46.535826232Z"
}
```


- Creating log-based metrics for firewall and instance actions using Cloud Logging Filters and setting up alerts is a straightforward and effective way to monitor unexpected changes. This solution allows the security team to receive timely notifications when specific events occur.



![log-based-metric-creation](/GCP_pictures/ACE-exam/mock-test-3/log-based-metric-creation.PNG "Log-based metric creation")



### 18. Ops-agent for collecting telemetry from Compute Engine instances

- CASE: You are building a project management tool that is hosted on a single Compute Engine instance. You have received complaints from your users that they are facing some errors. Your application writes all logs to the disk. How can you diagnose the cause of the error?


- Solution: View the logs from Cloud Logging by installing and configuring the Ops agent.


- Installing and configuring the Ops agent and viewing the logs from Cloud Logging would provide a comprehensive and centralized solution for diagnosing the reported errors. The Ops agent allows for enhanced monitoring and logging capabilities, enabling you to easily access and analyze application logs. It provides a more scalable and efficient approach compared to manually reading logs or relying on health checks.



### 19. Audit Logging and Pub/Sub as a Logging Sink

- CASE: Your company handles very sensitive personally identifiable information (PII) data of its clients using Bigtable. Your security team has mandated that all read or write operations, including any metadata or configuration reads of this database table should be logged. You want to use your company’s Security Information and Event Management (SIEM) system for storing the logs. What approach should you take?


- Solution: 

1. Visit the Audit Logs page within the Google Cloud console and activate the logging of Data Read, Data Write, and Admin Read activities pertinent to the Bigtable instance.


2. Establish a Pub/Sub topic to serve as a Cloud Logging sink destination, subsequently incorporating your SIEM as a subscriber to this topic.


- This option aligns closely with the security team's mandate by activating the logging of Data Read, Data Write, and Admin Read activities for the Bigtable instance. This ensures that read and write operations, along with administrative reads, are logged comprehensively. Setting up a Pub/Sub topic as a Cloud Logging sink allows the logs to be directed, and integrating the SIEM as a subscriber ensures that the logs are forwarded to the SIEM system for compliance and analysis.



### 20. Node pools for Spot VM and standard VM

- CASE: You are working for a major retailer that is developing a new application to sell groceries online. You have chosen to use Google Kubernetes Engine for the new app. Your app can tolerate downtime in certain parts. Critical parts of the application must always be available. How can you configure a Google Kubernetes Engine cluster in the most cost-optimal way?


- Solution:

1. Use both Spot VM node and Standard VMs to create a cluster with two node pools.

2. Deploy the critical deployments on the standard VMs node pool and the fault-tolerant deployments on the Spot VM node pool.


- Using both Spot VM node and standard VMs to create a cluster with two node pools and deploying critical deployments on standard VMs and fault-tolerant deployments on the Spot VM node pool is the most correct option. This configuration ensures that critical parts of the application, which must always be available, are deployed on the more stable standard VMs, while the fault-tolerant parts benefit from the cost savings of Spot VMs.



### 21. gcloud auth login

- CASE: Your employees have Google Cloud CLI installed on their corporate laptops. What steps need to be taken by the users to list the existing Compute Engine instances from GCP in their command line? (Choose two)


- Soluton:

1. Run the gcloud auth login command, enter your login credentials in the dialog window, and paste the received login token to gcloud CLI.


2. Run the gcloud config set project $my_project to set the default project for gcloud CLI.


- Running gcloud auth login initiates the authentication process, prompting the user to enter their login credentials in a dialog window. After successful authentication, a login token is received and automatically set in the gcloud CLI. This token allows the user to access resources in Google Cloud, including Compute Engine instances.


- **gcloud auth login** uthorizes gcloud to access the Cloud Platform with Google user credentials. It obtains access credentials for your user account via a web-based authorization flow. 


```
gcloud auth login

gcloud config set project PROJECT_ID 
```


- Setting the default project using the gcloud config set project is essential for users to operate within a specific Google Cloud project. When users run commands related to Compute Engine instances, having a default project ensures that the commands apply to resources within that project.


- If you'd rather authorize without a web browser but still interact with the command line, use the --no-browser flag. To authorize without a web browser and non-interactively, create a service account with the appropriate scopes using the Google Cloud Console and use gcloud auth activate-service-account with the corresponding JSON key file.


```
gcloud auth activate-service-account --key-file=key.json
```

```
gcloud compute instances list --project [project where the service account lives]
```


### 22. VPC Peering and custom routes

- CASE: Your Data Engineering team is running a Dataproc cluster in a single Virtual Private Cloud (VPC) network in a single subnetwork with a range 10.18.20.128/25. All available IP addresses have been used in the subnetwork. How can you add new VMs to communicate with your cluster in as few steps as possible?


- Solution:

1. Create a new VPC network for the VMs with a subnet of 10.18.20.128/16. 

2. Use VPC network Peering between the Dataproc VPC network and the VM's VPC network and configure a custom route exchange.


- Creating a new VPC network for the VMs with a subnet of 10.18.20.128/16 and using VPC network Peering between the Dataproc VPC network and the VM’s VPC network, along with configuring a custom Route exchange, effectively addresses the issue. This solution allows for a significant increase in available IP addresses by expanding the subnet mask to /16, thereby providing up to 65,536 IP addresses (minus the network and broadcast addresses). The use of VPC Peering facilitates secure communication between the two VPC networks without the need for public IP addresses or VPNs. The custom Route exchange ensures that traffic between the VMs and the Dataproc cluster is properly routed across the peered VPC networks, allowing for scalable and flexible network architecture while minimizing changes to existing configurations. This approach solves the interconnectivity issue directly and efficiently, providing a scalable path for network expansion with minimal disruption.



### 23. VPC Peering and custom routes

- CASE: You are part of the Cloud governance team in your organization and you are responsible for providing access for all Google Cloud users in your company. An external company is merging with your company. The other company has its own Google Cloud Organization. How can you ensure that the Site Reliability Engineers (SREs) in your company have the same project permissions in the other company's organization as in your own organization?


- Solution: Provide the Organization ID of the startup company's Google Cloud Organizations as the destination in the iam roles copy command.


- The gcloud iam roles copy command can be used to copy custom roles between organizations. In this scenario, you would provide the Organization ID of the startup company's Google Cloud Organization as the destination, ensuring that the roles are copied to the appropriate organization.


- **gcloud iam roles copy**


```
gcloud iam roles copy [--dest-organization=DEST_ORGANIZATION] [--dest-project=DEST_PROJECT] [--destination=DESTINATION] [--source=SOURCE] [--source-organization=SOURCE_ORGANIZATION] [--source-project=SOURCE_PROJECT] [GCLOUD_WIDE_FLAG …]
```

--destination=DESTINATION
The destination role ID for the new custom role. For example: viewer.

--source=SOURCE
The source role ID. For predefined roles, for example: roles/viewer. For custom roles, for example: myCompanyAdmin.



### 24. OS Config agent

- CASE: You are running a critical banking application on a Compute Engine VM. For security and compliance, a member of the security team at your company needs to be able to view vulnerabilities and other OS metadata for the Compute Engine instance. Which is a recommended way to implement the company’s security and vulnerability policy?


- Solution:

1. Install the OS Config agent on the Compute Engine instance.

2. Provide the **roles/osconfig.vulnerabilityReportViewer** permission to the security team member.


- It proposes installing the OS Config agent on the Compute Engine instance, which is designed for OS configuration management and vulnerability reporting. Additionally, providing the security team member with the roles/osconfig.vulnerabilityReportViewer permission ensures that they have the necessary access to view vulnerability reports. This option directly aligns with the company’s security and vulnerability policy, offering a focused and efficient solution for the specified requirements.


- On Compute Engine you can manage the operating systems that are running on your virtual machines (VMs) by using **VM Manager**. 


To enable VM Manager, you have two options

1. Automatic enablement: applies to your entire Google Cloud project. You complete automatic enablement from the Google Cloud console. You might still need to manually complete some steps.

2. Manual enablement: can be done per VM or for the entire Google Cloud project.


The first time you navigate to any of the VM Manager pages in the Google Cloud console, you can choose to automatically enable VM Manager.

If you follow the guided steps, you can use the automatic enablement to complete the following:

1. Enable OS Config service API on the Google Cloud project

2. Activate OS Config agents on all VMs in the Google Cloud project that have the agent installed.


![vm-manager-os-config-agent](/GCP_pictures/ACE-exam/mock-test-3/vm-manager-os-config-agent.PNG "VM manager os config agent")



### 25. GKE Horizontal Pod Autoscaler and Vertical Pod Autoscaler

- CASE: Your company is exploring Kubernetes on GCP. You want to calculate the resource requirements of a workload and figure out how the requirements vary by usage patterns, external dependencies, or other factors. What is a Google-recommended solution that provides recommendations regarding cost-effectiveness, CPU, and memory requirements while the workload consistently keeps functioning in any situation?


- Solution: Configure the Horizontal Pod Autoscaler, and for suggestions, configure the Vertical Pod Autoscaler recommendations.


- The Horizontal Pod Autoscaler (HPA) is designed to automatically adjust the number of running pods based on observed CPU utilization, while the Vertical Pod Autoscaler (VPA) provides recommendations for adjusting individual pod resource requirements (CPU and memory). This combination allows you to scale horizontally with HPA and optimize resource requirements with VPA.


- The Horizontal Pod Autoscaler (HPA) is focused on adjusting the number of replicas of a pod based on observed CPU utilization or other custom metrics. It does not provide recommendations regarding cost-effectiveness or specific CPU/memory requirements.


- the Vertical Pod Autoscaler (VPA) is more focused on adjusting the resource requests and limits of individual pods based on historical usage patterns, but it doesn't directly address the cost-effectiveness or overall cluster scaling.



### 26. GKE shielded nodes

- CASE: You are building a banking-related application on Google Kubernetes Engine. Your security team has given the following requirements for the cluster:



The cluster should have verifiable node identity and integrity

The nodes should not be accessible from the internet.



What should you do to honor these requirements while keeping operational costs to a minimum?


- Solution: Deploy a standard private cluster and enable shielded nodes.


- Deploying a standard private cluster and enabling shielded nodes would meet all the requirements. In a private cluster, nodes are not accessible from the internet by default. Enabling shielded nodes provides verifiable node identity and integrity. Additionally, following Google-recommended practices includes using standard clusters rather than autopilot clusters for more control and reducing operational costs.



### 27. Enable APIs

- CASE: Your company has provided you with a blank Google Cloud Project with an attached Billing account. You are going to use that project to deploy an app that uses Compute Engine, Firewall, and Cloud Storage. What is the first step that you need to perform on this project?


- Solution: Employ the gcloud CLI command gcloud services enable compute.googleapis.com to enable Compute Engine, and also use the gcloud services enable storage-api.googleapis.com command to activate the Cloud Storage APIs.


```
gcloud services list --available
```

```
gcloud services enable my-consumed-service
```


### 28. Load Balancing and Cloud Storage backend

- CASE: You are building a website for tracking shipments. You need the website to be secure and scalable based on the load on the compute instance CPU. Static content will be stored in Cloud Storage for enhanced performance. Which resources can you use to distribute the user traffic?


- Solution:

1. Use an external HTTP(S) load balancer with a managed SSL certificate to distribute the load.

2. Target the requests for the static content to the Cloud Storage backend using URL maps.


- It utilizes an external HTTP(S) load balancer with a managed SSL certificate to distribute the load. It efficiently targets requests for static content to the Cloud Storage backend using URL maps, optimizing performance and security.


### 29. Transfer Appliance & Storage Transfer Service

- CASE: You are working for a logistics company that has all of their infrastructure on-premises. You are leading the efforts of migrating the on-premise data to GCP. The data consists of:

-SAN storage consisting of 300 TB of video files
-Amazon Redshift consisting of Data warehouse data
-S3 Bucket consisting of 20 GB of PNG files

The video files must be loaded into a Cloud Storage bucket. The data warehouse data must be loaded into BigQuery, and the PNG files must be loaded into a second Cloud Storage bucket. How can you perform this migration without having to write any code while following Google's recommended practices?


- Solution:

1. Migrate the videos using Transfer Appliance.

2. Use the BigQuery Data Transfer Service for the data warehouse data.

3. Storage Transfer service for the PNG files.


- The Transfer Appliance is designed for high-volume data transfers, such as the 300 TB of video files, making it an ideal choice for migrating large datasets that cannot be efficiently transferred over the internet. The **BigQuery Data Transfer Service** is specifically designed to simplify the migration of data warehouse data to BigQuery, providing a managed service that automates the data transfer process. For the PNG files, the **Storage Transfer Service** is the appropriate tool, as it supports transferring data between Cloud Storage buckets or from an external source into Cloud Storage, handling small datasets like the 20 GB of PNG files efficiently.



### 30. Cloud Bigtable

- CASE: You are working at a company that manufactures trucks. The trucks have multiple sensors that continuously send event information such as engine status, distance traveled, fuel level, etc. Up to thousands of events are expected per hour from each truck. Your analysts need to retrieve consistent data based on the time of the event. Which solution can you adopt to make sure that the above requirements are fulfilled along with the ability to store and retrieve the individual rows atomically?


- Solution: Load the data into Bigtable. Create a row key based on the event timestamp.


- Using Bigtable allows for the storage and retrieval of individual rows atomically, and it supports high-throughput scenarios. Creating a row key based on the event timestamp ensures that the data can be consistently retrieved based on the time of the event.



### 31. Connecting to Instance

- CASE: Your company is employing the services of an external consultant to work on certain features for an app that is deployed on a Compute Engine Linux-based instance. How can the consultant access your VM if they are connected to your corporate VPN but don’t have a Google Account?


- Solution:

1. Ask the consultant to generate an SSH key pair, and provide you with the public key.

2. Manually add the public key to the instance and ask the consultant to access the instance through SSH with their private key.


- Asking the consultant to generate an SSH key pair and providing you with the public key is a secure and standard practice. You can manually add the public key to the authorized_keys file on the Compute Engine instance. This way, the consultant can access the instance through SSH using their private key, ensuring secure authentication without relying on Google Accounts or exposing the instance to the public internet.



### 32. Cloud Tasks

- CASE: Your company has a legacy application on Google Cloud that is made up of the following components:

A Flask web application

A backend API

A scheduled long-running background job for ETL and reporting



What should you do to migrate this app to Google Cloud on a serverless solution, while keeping operational costs to a minimum?


- Solution:

1. Transition the web application to App Engine and transfer the backend API to Cloud Run.

2. Utilize Cloud Tasks to manage the execution of your background operation within the Cloud Run environment.


- It follows the Google-recommended practices to migrate the given workloads to serverless solutions on Google Cloud. Migrating the web application to App Engine allows for automatic scaling, handling traffic spikes, and managing resources effectively based on demand. Migrating the backend API to Cloud Run provides a fully managed serverless environment that scales automatically, reducing operational costs. Using Cloud Tasks to run the background job on Cloud Run allows for running scheduled long-running background tasks without the need for managing and provisioning infrastructure separately.



### 33. Service Accounts

- CASE: You are part of the Cloud Support team for your company and you have been asked to configure service accounts for an application whose parts are deployed in multiple projects. Virtual machines (VMs) running in the application-layer project must be able to access BigQuery datasets in the crm-layer project. What is the Google-recommended practice so that the service account in the application-layer project can get the required access?


- Solution: Grant roles/bigquery.dataViewer role to crm-layer and appropriate roles to application-layer.


- Granting the roles/bigquery.dataViewer role to the crm-layer allows the service account in the application-layer project to access BigQuery datasets in the crm-layer project with the appropriate level of access. This approach adheres to the principle of least privilege by ensuring that the service account only has the permissions necessary to view the BigQuery datasets and no more. Additionally, specifying "appropriate roles to application-layer" suggests tailoring the access rights to fit the exact needs of the application-layer project, further aligning with best practices for security and access management in cloud environments.



### 34. Using IAM Securely

- CASE: You are working at a major bank that is going through a technology modernization phase. As a lead engineer, you have suggested migrating CI/CD pipelines to Compute Engine instances to manage all the cloud infrastructure through code. What do you need to do to ensure you are following security best practices while making sure that the pipeline has appropriate permissions?


- Solution:

1. Add appropriate IAM permissions to multiple service accounts.

2. Store the key files of the service accounts using a secret manager.

3. Request the appropriate secrets during the execution of the pipeline from within the CI/CD pipeline.


-  Adding appropriate IAM permissions to multiple service accounts allows for a more fine-grained control of permissions, following the principle of least privilege. Storing key files of the service accounts using a secret manager enhances security by centralizing and securing sensitive information. Requesting the appropriate secrets during the execution of the pipeline from within the CI/CD pipeline ensures that the necessary credentials are retrieved securely at runtime.











































































