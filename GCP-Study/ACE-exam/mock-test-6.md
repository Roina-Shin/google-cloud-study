### [Source of this study material : GCP Associate Cloud Engineer Practice Test Exam by Sayyam](https://www.udemy.com/course/latest-gcp-ace-google-associate-cloud-engineer-practice-exams-tests)


## Exam -6

### 1. Audit Logs

- CASE: You are working at a financial services and housing loans company. Some highly sensitive financial data of your clients is stored on a Cloud Storage bucket. The client has mandated that all requests to read any of the stored data should be logged. What should you do to comply with these requirements?


- Solution: Enable DData Access audit logs for the Cloud Storage API.


- Data Access logs: Entries for operations that modify objects or read a project, bucket, or object. There are several sub-types of data access logs:


ADMIN_READ: Entries for operations that read the configuration or metadata of a project, bucket, or object.


DATA_READ: Entries for operations that read an object.


DATA_WRITE: Entries for operations that create or modify an object.



Enabling Data Access audit logs for the Cloud Storage API directly addresses the requirement to log all requests to read the stored data. By enabling these logs, every read request made to the Cloud Storage bucket will be logged, providing an audit trail of all access to the sensitive financial data. This helps ensure compliance with the client's mandate to log all read requests.


- The Data Loss Prevention (DLP) API is typically used for identifying sensitive data within structured and unstructured data and applying data loss prevention techniques such as de-identification, masking, and encryption.


- The Identity Aware Proxy API is primarily used for Google Cloud Platform services like Cloud Identity-Aware Proxy (IAP) and Cloud Identity Platform, which provide secure access to applications and resources in the cloud.



### 2. Delete Protection on the Instance

- CASE: Recently, one of your cloud interns accidentally deleted a production Compute Engine instance, which caused downtime to your app. You want to make sure such an accident of clicking the wrong button does not happen again. What should you do?


- Solution: Enable delete protection on the instance.


- Delete protection protects the VMs from being accidentally deleted. Enabling delete protection on the instance adds an extra layer of protection against accidental deletions. When delete protection is enabled, it ensures that the instance cannot be deleted directly from the Google Cloud Console or via API calls. This helps prevent accidental deletions and avoids potential downtime caused by developers mistakenly deleting production instances.



### 3. Change the billing account for the project

- CASE: You are working at a startup, where you have been tasked with exploring GCP for its suitability for a Sports Score tracking application that your company is building. You have been using your personal Credit Card on GCP and reimbursing the costs from your company every month. Your company wants to streamline the billing process such that the GCP charges are directly charged to the company based on their monthly invoice. What should you do?


- Solution: Change the billing account of your project to the billing account of your company.


- Changing the billing account to the company’s billing account will enable the company to get a single invoice. Changing the billing account of your projects to the billing account of your company will allow the charges to be directly charged to the company based on their monthly invoice. This streamlines the billing process and eliminates the need for reimbursement.



### 4. Cloud Storage Obejcts and Signed URL

- CASE: You are building multi-tenant accounting software that will be used by several different organizations. One of the features of the application allows users to upload invoices. In order to maintain data security, you need to make sure every user can only access their own invoices. The users have write access to the data only for 30 minutes and the invoices should be deleted after 45 days. How can you build such functionality in your application quickly and with minimal maintenance? (Choose two options.)


- Solution:

A. Create a lifecycle policy to delete Cloud Storage objects after 45 days.

B. Use signed URLs to provide access to users to store their objects only for a limited time.


- A lifecycle policy can be used to delete data that is more than 45 days old. It allows you to set a lifecycle policy in Cloud Storage to automatically delete objects after 45 days. This ensures that the invoices are automatically deleted within the specified time frame without the need for manual intervention.


- Signed URLs allow limited-time access to cloud storage buckets. Using signed URLs can provide access to users to store their objects only for a limited time. By generating signed URLs with a predetermined expiration time, users can only upload and access their own invoices within the specified timeframe (30 minutes). After the expiration time, the URLs will no longer be valid, effectively limiting the user's write access to their own invoices.



### 5. GKE Cluster Autoscaler

- CASE: Your company is building a video-sharing app and it wants to use a single GKE cluster for running multiple applications on Kubernetes. You as a cloud engineer want to make sure that the cluster can scale with the number of videos deployed on it. You want to keep the scaling process as automated as possible. What should you do? 


- Solution: 

1. Create a GKE cluster with autoscaling enabled on the node pool.

2. Configure a minimum and maximum size for the node pool.


- You can automatically resize your Standard Google Kubernetes Engine (GKE) cluster's node pools based on the demands of your workloads. When demand is high, the cluster autoscaler adds nodes to the node pool. When demand is low, the cluster autoscaler scales back down to a minimum size that you designate. Creating a GKE cluster with autoscaling enabled on the node pool allows for automated scaling of the cluster itself based on the workload. By configuring a minimum and maximum size for the node pool, the cluster can automatically scale up or down the number of nodes based on the demand. This ensures that the cluster can handle a larger number of videos deployed on it.


- Adding HorizontalPodAutoscaler to the deployment will scale up the existing application pods based on the load but it does not scale up the infrastructure. Adding a HorizontalPodAutoscaler to each deployment will only scale the number of replicas of the application pods within the cluster based on CPU/memory utilization. This will not directly affect the scaling of the entire cluster itself.


- Adding VerticalPodAutoscaler to the deployment will scale up the existing pods based on the load but it does not scale up the infrastructure. Adding a VerticalPodAutoscaler to the deployment will only optimize resource allocation within the application pods by adjusting CPU/memory requests and limits. This will not directly affect the scaling of the entire cluster itself.



### 6. Deployment Manager

- CASE: Your social media startup is growing rapidly and you have learned that manually managing infrastructure is difficult and error-prone. You have decided to use Infrastructure as Code to manage all of your GCP infrastructures. How can you minimize the amount of repetitive code required for the management of the environment?


- Solution: Use Cloud Deployment Manager to develop templates for environments.


- Cloud Deployment Manager can be used to develop templates that can be applied to multiple environments. Using Cloud Deployment Manager allows you to define and manage your infrastructure resources using templates. These templates can be version controlled and reused for different environments, reducing the amount of repetitive code required for managing the environment.


NOTE:

A configuration can contain templates, which are essentially parts of the configuration file that has been abstracted into individual building blocks. After you create a template, you can reuse them across deployments as necessary. Similarly, if you find yourself rewriting configurations that share very similar properties, you can abstract the shared parts into templates. Templates are much more flexible than individual configuration files and intended to support easy portability across deployments.


- **configuration.yaml**


```
imports:
- path: vm_template.jinja

resources:
- name: my-vm
  type: vm_template.jinja
  properties:
    zone: us-central1-a
```


- **template.jinja**

```
- name: vm-{{ env["deployment"] }}
  type: compute.v1.instance
  properties:
    zone: us-central1-a
    machineType: zones/{{ properties["zone"] }}/machineTypes/n1-standard-1
    disks:
    - deviceName: boot
      type: PERSISTENT
      boot: true
      autoDelete: true
      initializeParams:
        sourceImage: projects/debian-cloud/global/images/family/debian-11
    networkInterfaces:
    - network: global/networks/default
```


```
gcloud deployment-manager deployments create a-single-vm --template vm_template.jinja \
    --properties zone:us-central1-a
```



### 7. IAM Permissions

- CASE: Your security team at a large fin-tech company is doing a mock audit of your GCP environment. They want to know who can access data stored in the production GCP project. What should you do?


- Solution: Review the IAM permissions for every role that provides data access.


- The IAM permissions will show which users have read access. Reviewing the IAM permissions for every role that provides data access is an important step in determining who can access the data stored in the production GCP project. IAM (Identity and Access Management) allows you to manage access control and permissions for resources within GCP. Reviewing the IAM permissions will help in identifying any potential misconfigurations or unauthorized access.


- IAP settings will not give a definitive list of users as some services like Cloud Storage do not use IAP. Reviewing the Identity-Aware Proxy (IAP) settings for every resource is focused on managing access to specific resources through authentication and authorization. While it is important for securing access to resources, it does not directly address determining who can access the data stored in the production GCP project as a whole.


- Creating a Data Loss Prevention (DLP) job is mainly focused on identifying and preventing the leakage of sensitive data. While it is important for data protection, it does not directly address determining who can access the data stored in the production GCP project. It is more focused on data classification and protection rather than access control.



### 8. Firewalls

- CASE: You are configuring a highly sensitive banking security web application on Compute Engine in a new VPC behind a firewall. You need to control data egress on this app such that there are as few open egress ports as possible. What should you do?


- Solution:

1. Set up a low-priority (65534) rule blocking all egress and

2. High-priority rule (1000) allowing only the appropriate ports.


- An egress rule whose action is allow, the destination is 0.0.0.0/0, and priority is the lowest possible (65535) lets any instance send traffic to any destination, except for traffic blocked by Google Cloud. Thus, any firewall rule will override this default egress rule and we need higher priority rules to open the ports. It sets up a low-priority rule blocking all egress and a high-priority rule allowing only the appropriate ports. This ensures that all egress traffic is blocked by default, except for the specific ports that are needed for the banking security web application. 


- As per the above Google Doc link, An egress rule whose action is allow, destination is ::/0, and priority is the lowest possible (65535) lets any instance send traffic to any destination, except for traffic blocked by Google Cloud. A higher-priority firewall rule may restrict outbound access. Internet access is allowed if no other firewall rules deny outbound traffic and if the instance has an external IP address.

- The implied rules cannot be removed, but they have the lowest possible priorities. You can create rules that override them as long as your rules have higher priorities (priority numbers less than 65535). Because deny rules take precedence over allow rules of the same priority, an ingress allow rule with a priority of 65535 never takes effect.



### 9. Firewalls

- CASE: You work at a mid-sized food delivery startup. Your company is mid-way through its journey of migrating all of its applications to GCP. For now, some of the resources are present on-premises and the rest are on GCP. The VMs on Compute Engine communicate with on-premise servers through Cloud VPN over private IP addresses. A database server running on-premises is used by several applications running on GCP. You want to make the GCP applications don’t need to do any configuration changes in case the IP address of the on-premise database changes. What should you do?


- Solution: Create a private zone on Cloud DNS. Configure the applications using the DNS name.


- Cloud DNS forwarding zones let you configure target name servers for specific private zones. Using a forwarding zone is one way to implement outbound DNS forwarding from your VPC network.

- In our case, it is mentioned that we have a hybrid, VPN, VPC, etc and the only thing we need is not to be dependent on IP change. From Google documentation private zone on Cloud DNS (Option-B) will help us to solve this issue.

- Creating a private zone on Cloud DNS and configuring the applications to use the DNS name allows for dynamic resolution of the database IP address. By using the DNS name instead of the IP address directly, any changes to the IP address can be managed by updating the DNS record, without requiring any configuration changes in the GCP applications.


### 10. Cloud Run

- CASE: Your team has developed the backend for an internal note-taking tool which is primarily going to be used by the employees of your organization. The app is containerized using Docker and it will only be used during work hours on weekdays. The tool needs to run on a limited budget and you want to make sure the cost of running the application becomes zero when it is not being used. What should you do?


- Solution: Deploy the container on Cloud Run (fully managed) with a minimum number of instances to zero.


-  Cloud Run charges you only for the resources you use, rounded up to the nearest 100 milliseconds. Note that each of these resources has a free tier. With Cloud Run (fully managed), you can set the minimum number of instances to zero. This means that when the application is not being used, there will be no instances running, and hence the cost will be zero. When a request comes in, Cloud Run will automatically scale up to handle the request.


- Cloud Run for Anthos does not have the capability to automatically scale down to zero instances and the minimum number of instances cannot be set to zero. It is designed for running containers within a Kubernetes cluster.


- App Engine flexible environment does not scale down to zero when not in use. In the App Engine flexible environment, the min_instances value determines the minimum number of instances that should be running at all times. Setting it to zero would mean that there are no instances running, causing the application to be unavailable.



### 11. Service Account

- CASE: You are a head of a project in a product-based warehouse company running on BigQuery. Another partner company wants to collaborate with your project and wants to offer a search engine based on data available in your warehouse. They manage resources in their own GCP project but they need access to BigQuery datasets from your project. You need to provide BigQuery dataset access to this company. How would you achieve this?


- Solution:

1. Ask the partner to create a Service Account in their project.

2. Grant their Service Account access to the BigQuery dataset in your project.


- The partner creates their own Service Account within their own project, which ensures they have control over their resources. Then, you specifically grant their Service Account access only to the BigQuery dataset in your project. This way, you are granting the partner access to exactly what they need, without giving them unnecessary access to your entire project. Also, this option follows the principle of least privilege and maintains better separation of resources.


### 12. Cloud Function and Storage Bucket as Trigger

- CASE: You have created a Python function that can resize images on your webapp portal. The function needs to run on every new object that gets uploaded to a Cloud Storage bucket. How can you do it?


- Solution: Create a Cloud Function using the Python code and configure the bucket as a trigger resource.


- Cloud Functions can respond to change notifications emerging from Google Cloud Storage. These notifications can be configured to trigger in response to various events inside a bucket—object creation, deletion, archiving, and metadata updates. It suggests creating a Cloud Function using the Python code and configuring the Cloud Storage bucket as a trigger resource. This allows the function to be automatically triggered on every new object uploaded to the bucket.



### 13. Load Balancing options

- CASE: Your latest Multiplayer Online Shooting Game for Mobile is hosted on Google Cloud. The game updates the server of the user’s actions by sending UDP packets from the users Mobile phone while the users are playing in multiplayer mode. You have designed the backend such that it can scale horizontally by increasing or decreasing the number of VMs. You need to expose the backend by using a single IP address. What should you do?


- Solution: Set up an External Network Load Balancer in front of the application servers.


- External Network Load Balancer exposes the traffic to the internet and it supports UDP. Setting up an External Network load balancer allows for load balancing of UDP traffic and can provide a single IP address for external access to the backend servers.



### 14. How to create a budget

- CASE: Your company recently hired interns in the cloud and development teams. Your company provides burner GCP accounts to developers in your company for learning and testing purposes. Whenever a developer requests a burner account, you create a GCP project and provide access to the developer. You need to make sure any developer individually doesn’t spend more than 700$ per month using their burner account. If they exceed the budget, you should be notified. What should you do?


- Solution: Create a budget for each project and configure budget alerts on all of these budgets.


- You can create budgets per project to get notified for every project that goes out of budget. It suggests creating a budget for each project and configuring budget alerts on all of these budgets. This would ensure that each developer has their own budget and would be notified if they exceed their personal spending limit of $500 per month.


- To create a budget for your Cloud Billing account, you need a role that includes the following permissions on the Cloud Billing account:

billing.budgets.create to create a new budget.

billing.budgets.get and billing.budgets.list to view all budgets for the Cloud Billing account.


To gain these permissions, ask your administrator to grant you one of the following Cloud Billing IAM roles on your Cloud Billing account:

Billing Account Administrator

Billing Account Costs Manager


### 15. Synchronize on-premise storage with Google Cloud Storage

- CASE: You are part of the technology department at a large X-Ray clinic chain. Your tech team has built a clinic management app that stores images in an on-premise data room. For compliance reasons, the clinic needs to keep these images in archival storage and you have identified Cloud Storage as a suitable solution for it. How can you design and implement an automated solution to upload any new images to Cloud storage?


- Solution: 

1. Write a script that uses the gsutil command line interface to synchronize the on-premises storage with Cloud Storage.


2. Create a CRON job to invoke the script periodically.


- This option involves using 'gsutil', Google Cloud's command-line tool, to synchronize on-premise storage with Cloud Storage. A script is created to handle the synchronization, and a CRON job is set up to run the script periodically. 'gsutil' offers powerful capabilities for syncing data between on-premise and Cloud Storage. Automating this process with a script executed via a CRON job can provide an efficient and reliable way to upload new images to Cloud Storage.


```
gsutil rsync [OPTION]... src_url dst_url
```


- The gsutil rsync command makes the contents under dst_url the same as the contents under src_url, by copying any missing files/objects (or those whose data has changed), and (if the -d option is specified) deleting any extra files/objects. 



- For example, to sync the contents of the local directory "data" to the bucket gs://mybucket/data, you could do:


```
gsutil rsync data gs://mybucket/data
```


### 16. Audit Logs

- CASE: You work at a large stock-broking firm that serves millions of clients. Your company is going through a third-party Audit of data access practices on Google Cloud. The auditor has given a list of information that they need. One of the requests is to view information about who accessed data on Cloud Storage buckets. How can you provide this data to the Auditor?


- Solution: Turn on Data Access Logs for the buckets being audited. Go to the Log viewer and build a query to filter on Cloud Storage.


- Information about users accessing data is available through Data Access Logs. Turning on Data Access Logs for the buckets being audited allows you to track and monitor who accessed the data on Cloud Storage buckets. By going to the Log viewer, you can build a query to filter and gather the required information for the auditor.


- Admin Activity Audit Logs track actions taken by administrators within a Google Cloud project, but it does not provide detailed information about data access by individual users.



Random GCP Concept (optional read)

Types of Google Cloud quotas

- Rate quotas are typically used for limiting the number of requests that you can make to an API or service. Rate quotas reset after a time interval that is specific to the service—for example, the number of API requests per day.

- Allocation quotas are used to restrict the use of resources that don't have a rate of usage. For example, the number of VMs used by your project at a given time. Allocation quotas don't reset over time. Instead, they must be explicitly released when you no longer want to use them—for example, by deleting a GKE cluster.

- Concurrent quotas are used to restrict the total number of concurrent operations in flight at any given time. These are usually long-running operations. For example, Compute Engine uses insert_operations that are expected to last as long as one hour.



### 17. Using SSH keys

- CASE: You are working on a complex crypto trading application. Your company has started a pilot project for outsourcing management of their Linux Compute Engine VMs to a third-party service provider. The third-party provider does not use Google Accounts, but they require SSH access to the VMs in order to do their work. How can you enable this access?


- Solution:

1. Ask the operations partner to generate SSH key pairs.

2. Add the public keys to the VM instances.



- Why Cloud IAP is not valid in this case: because the operations partner does not have a Google account. Activating and enabling Cloud IAP (Identity-Aware Proxy) for the Compute Engine instances would only allow access to users with Google Accounts. In this case, the third-party service provider does not use Google Accounts, so this option would not enable their access.


- The operations partner can use SSH keys to SSH into the VMs. Asking the operations partner to generate SSH key pairs and adding the public keys to the VM instances would allow the third-party service provider to authenticate and access the VMs securely using SSH. This option ensures that only authorized users with the corresponding private key can access the VMs. It is a common practice for granting SSH access to external parties.



### 18. gcloud auth activate-service-account

- CASE: You work at a game development company. For local testing of paid premium game version, your devops team has provided a JSON file to you that contains the private key of a service Account that has access to the required GCP services. You have the gcloud SDK installed on your laptop. How can you use the provided private key for performing authentication and authorization while using gcloud commands?


- Solution: Run the gcloud auth activate-service-account command and point it to the private key.


- The gcloud auth activate-service-account command is used to activate the service account in Cloud SDK. The gcloud auth activate-service-account command is used to authenticate with the Google Cloud services as a service account. By providing the path to the private key file, you can activate the service account for use with gcloud commands, allowing you to perform actions and access resources based on the service account's permissions.


```
gcloud auth activate-service-account [Email of service account] --key-file=KEY_FILE 
```


- gcloud auth login is for authenticating a user and not a service account. The gcloud auth login command is used for interactive user authentication, not for authenticating as a service account using a private key file. It won't work for using the provided service account private key.



### 19. Log based metric for specific error

- CASE: You are part of the on-call SRE team for an E-commerce startup. You received incident tickets from multiple users saying that the site is giving error. On investigating further, you realized that the error is caused by a Service Account with insufficient permissions. You fixed the issue but how can you make sure you get notified if the problem recurs?


- Solution: Create a custom log-based metric for the specific error and use it in an Alerting Policy.


- You need to create a log-based metric for the error to get notified if it occurs again. Creating a custom log-based metric for the specific error allows you to track and monitor the occurrence of the error. By using this custom log-based metric in an Alerting Policy, you can configure the system to notify you whenever the error occurs again. This option meets the requirement of being notified if the problem recurs.


**Log based metrics**

Log-based metrics derive metric data from the content of log entries. For example, you can use a log-based metric to count the number of log entries that contain a particular message or to extract latency information recorded in log entries. You can use log-based metrics in Cloud Monitoring charts and alerting policies.


Consider a log-based metric with the following filter:


```
severity>="ERROR"
resource.type="gce_instance"
```

Cloud Monitoring recognizes that this data is for a Compute Engine VM instance. Therefore, when you create a chart for a VM instance, your log-based metric is listed as an option in the menus. When you create a chart for a different resource type, your log-based metric isn't listed as an option.



### 20. Microservices on GKE

- CASE: You are building a new-age social media platform using the microservices architecture. Each microservice will be packaged in its own Docker container image. What is the best approach to deploy the entire application on Kubernetes Engine such that each microservice can scale individually?


- Solution: Use a Deployment per microservice.


- Microservices run as deployments or statefulsets on Kubernetes. Using a Deployment per microservice is a recommended approach for deploying microservices individually on Kubernetes. A Deployment provides declarative updates to manage and scale the microservice, including features like rolling updates, scaling, and rollback. It ensures that the desired number of replicas of the microservice are running at all times, allowing each microservice to scale individually as needed.


-  Using a Docker Compose file is typically used for defining and running multi-container Docker applications. While it can be used to define and manage multiple microservices, it does not provide the built-in scalability features and management capabilities that Kubernetes offers.


- Using a Job per microservice is typically used for running batch processes or one-time tasks in Kubernetes, rather than continuously running and scaling microservices.



### 21. Identity Aware Proxy for SSH and TCP resources

- CASE: You are working on a noise reduction app project that has multiple Linux machines on Compute Engine. The VMs do not have a public IP, but you need to be able to access those VMs using an SSH client over the internet without having to configure any specific network-related changes. You also want to make sure no additional configuration is required for any new VMs added to the project. What should you do?


- Solution: Configure Cloud Identity Aware Proxy for SSH and TCP resources.


- Cloud Identity Aware Proxy can be used to enable access to VMs that do not have external IP addresses or do not permit Direct Access over the internet. Configuring Cloud Identity-Aware Proxy for SSH and TCP resources allows you to access the VMs using an SSH client over the internet without having to configure any specific network-related changes. This option ensures that no additional configuration is required for new VMs added to the project.


### 22. Associating service account to an instance

- CASE: Your company has developed a social media app called 'Pony'. The Pony app has multiple sub-applications deployed on Compute Engine in the same GCP project. How can you specify a granular level of permissions for each instance which calls Google Cloud APIs?


- Solution: Create a different service account for each instance.


- Assigning different service accounts to different compute engine instances is a best practice if the instances require granular access control. Creating a different service account for each instance allows for a granular level of permissions. Each service account can be assigned specific roles and permissions, allowing for fine-grained control over the resources and APIs that each instance can access.



### 23. BigQuery user role

- CASE: Your company is the largest analytics firm in Asia. You are supporting the Business Intelligence team at your company to generate insights on user activity data. The data is loaded into BigQuery using streaming inserts through a data pipeline. The BI department needs to run custom SQL queries on the latest data in BigQuery. What should you do?


- Solution: Assign the IAM role of BigQuery User to the BI team's Google group.


- roles/bigquery.user, when applied to a dataset, provides the ability to read the dataset's metadata and list tables in the dataset. Assigning the IAM role of BigQuery User to the BI team's Google group would allow the BI team members to directly query the latest data in BigQuery without any additional steps or dependencies. This would give them the necessary permissions and access to generate insights on user activity data in real-time.


- Distributing service account private keys is not safe and should be avoided if possible. Creating a Service Account and distributing private keys to each member of the BI team is not necessary for running custom SQL queries on the latest data in BigQuery. Service Accounts and private keys are typically used for programmatic access to Google Cloud resources, but in this case, the BI team can directly access BigQuery using their own user accounts.



### 24. Link a project to a billing account

- CASE: Your company provides cloud services that help migrate other companies to GCP. Multiple teams at your Organization use Google Cloud services in their own separate projects. The marketing team is working on a new initiative and the GCP costs for this initiative will be borne by the Marketing department. How can you bill the Marketing team only for their Google Cloud services for the new initiative within their group?


- Solution:

1. Make sure you have the Billing Administrator IAM role for the company's Marketing department GCP project.

2. Link the new project to a Marketing Billing account.


- The Billing Administrator role is an owner role for a billing account. It can be used to manage payment instruments, configure billing exports, view cost information, link and unlink projects, and manage other user roles on the billing account. By linking the new project to a Marketing Billing Account, it is ensured that all the resources used by the marketing team will be billed separately to its specific billing account. It outlines the correct steps to bill the Marketing team only for their Google Cloud services for the new initiative within their group.

1. By having the Billing Administrator IAM role for the Marketing department's GCP project, you have the necessary permissions to manage billing for that project.

2. Linking the new project to a Marketing Billing Account ensures that the costs for the new initiative are charged to the Marketing department specifically.



### 25. Design networking setup

- CASE: You work as a senior cloud engineer at a premiere medical institute where your team is working on migrating the entire infrastructure of a legacy enterprise client to GCP Compute Engine. Some medical servers are accessible from the internet, others via the institute's internal intranet. All servers talk to each other over specific ports and protocols. You are studying the current network setup and you have found that the public servers rely on a demilitarized zone (DMZ) and the private servers use the Local Area Network (LAN). How can you design the networking setup on GCP with these requirements?


- Solution:

1. Use a single VPC with two subnets: one for the DMZ and one for LAN.

2. Control traffic between LAN and DMZ using firewall rules, and create firewall rules to allow public ingress traffic for the DMZ.


- The DMZ and LAN can be logically separated as 2 subnets and firewall rules can be created to open up ports between them. It suggests using a single VPC (Virtual Private Cloud) with two subnets to separate the DMZ (Demilitarized zone) and LAN (Local Area Network) servers. This setup allows for control of traffic between the two subnets using firewall rules. Additionally, it mentions creating firewall rules to allow public ingress traffic for the DMZ, which is necessary for the accessible public servers.



### 26. Access Control Folders

- CASE: You are working for a Cloud Consulting firm that specializes in providing managed services for managing Google Cloud environments. You are working with a customer that has recently started using GCP and they need you to set up billing configuration for their environments. Their requirement is that all resources that share common IAM policies need to be grouped together. What should you do?


- Solution: Group resources that share common IAM policies by folders.


- Projects sharing similar IAM policies can be grouped in a folder and then the IAM policies can be applied at the folder level. Grouping resources that share common IAM policies by folders is the recommended approach in GCP. Folders provide a way to organize resources hierarchically and can be used to apply IAM policies to all resources within a folder. By grouping resources in folders, you can easily manage and apply consistent IAM policies to multiple resources at once.


- IAM policies are managed at either organization, folder or project level. Labels do not have anything to do with IAM policy. Using labels is not the recommended method for grouping resources that share common IAM policies. Labels are used for organizing and categorizing resources based on specific attributes, but they do not have any direct impact on IAM policies.



### 27. Dual region storage

- CASE: Your company has built a train booking application. A daily running mission-critical data analysis pipeline at your company relies on files stored in a Cloud Storage bucket. Data is accessed frequently and dynamically. The users are located in Bangalore, India. How can you configure the most optimal and cost-effective storage for these files on Cloud Storage?


- Solution: Configure regional storage with standard storage class for the region closest to the users.


- It recommends using regional storage with the standard storage class, which is optimized for storing data that is frequently accessed in the same region as the users. In this case, configuring regional storage in the region closest to the users (Bangalore, India) would minimize latency and increase the performance of data access for the mission-critical analysis pipeline. The standard storage class is the most appropriate for data that needs to be accessed frequently and quickly, as it would be in a daily analysis scenario, making it the most optimal and cost-effective choice for this use case.


- Dual-regional storage provides higher availability and redundancy by storing data in two geographic locations, which may be more than what is necessary for the specified requirements and can result in higher storage costs. For a mission-critical application that is predominantly used by users in a single region, the added expense and complexity of dual-regional storage do not provide a proportional benefit compared to regional storage.


NOTE:

Mission-critical applications like train booking services, stock trading broker apps, etc heavily rely on the 'time' factor and need frequent data access to fulfill their services.

As per the GCP docs:

- Standard storage is best for frequently accessed data also known as hot data.

- Nearline storage is used for storing infrequently accessed data.



### 28. App Engine Split Traffic

- CASE: You are building a new medicine delivery web application that will be deployed on GCP. One of your requirements is that you need to be able to test updates for the application on a small portion of live users before rolling it out to everyone. The rest of the users should still see the live version of the app. What should be your GCP deployment strategy?


- Solution:

1. Use App Engine to run your app.

2. For each update, create a new version of the same service.

3. Send a small percentage of traffic to the new version using traffic splitting.


- You can use traffic splitting to specify a percentage distribution of traffic across two or more of the versions within a service. Splitting traffic allows you to conduct A/B testing between your versions and provides control over the pace when rolling out features. It allows you to test updates on a small portion of live users before rolling it out to everyone. In this strategy, you would use App Engine to run your app and create a new version of the same service for each update. You can then use traffic splitting to send a small percentage of traffic to the new version, while the rest of the users continue to see the live version of the app.


- Updating the deployment on kubernetes directs all traffic to the new version, thus you cannot perform A/B testing that way. It suggests using Kubernetes Engine to run your app and simply updating the deployment to use the new version for each release. While this strategy allows for easy updates, it does not provide the ability to test updates on a small portion of live users before rolling it out to everyone.


-  Traffic splitting works with versions of the same service. Not within multiple services. It suggests creating a new service for each update. This would result in multiple instances of the app running simultaneously, which may cause difficulties in managing and coordinating the updates.



### 29. Machine Type M1

- CASE: You are migrating an on-premise customer-facing application to GCP. The application stores the full database in-memory to keep the latency minimum. How should you configure resources on GCP for this application?


- Solution: Use Compute Engine instances with M1 machine type.


- "The application holds the full database in-memory for fast data access", so it'll be more appropriate to use memory-optimized machine types. The M1 machine type in Compute Engine is designed for memory-intensive workloads. It provides a high memory-to-CPU ratio, making it suitable for applications that need to store the full database in memory to minimize latency. By choosing the M1 machine type, you can configure the instance with enough memory capacity to hold the entire database, ensuring fast access to data and reducing disk-based latency.


- Adding a local SSD does not improve the performance of RAM. Local SSDs are temporary block storage devices that are physically attached to the host machine. They provide high IOPS (input/output operations per second) and low latency compared to network-attached storage options like standard persistent disks. However, local SSDs are ephemeral and do not persist data after the instance is shut down or terminated. Therefore, using local SSDs would not be suitable for an application that requires the full database to be stored in memory for minimizing latency.



### 30. CPU Utilization of Cloudl Spanner

- CASE: Your photo-sharing application is hosted on GCP. You have been asked to manage a Cloud Spanner instance in production for optimal query performance. The Spanner instance is running in a single Google Cloud region. You want to follow Google's recommended practices for service configuration. What should you do to improve performance as quickly as possible?


- Solution:

1. Create an alert in Cloud Monitoring to alert when the percentage of high-priority CPU utilization reaches 65%.

2. Add nodes to your instance when the threshold is exceeded.


- The recommended maximum CPU utilization for single-region Spanner instances is 65%.


- When this threshold is exceeded, you should add more nodes to the Spanner instance and take advantage of Spanner’s horizontal scalability. It suggests creating an alert in Cloud Monitoring to alert when the percentage of high-priority CPU utilization reaches 65% and adding nodes to the instance when the threshold is exceeded. This approach takes into account the high CPU utilization and adds more resources to the instance to handle the increased workload, thereby improving query performance.


- The whole point of Cloud Spanner is that you can take advantage of horizontal scalability instead of trying to optimize query for performance.



### 31. VPN concepts

- CASE: Your VMs on Compute Engine need to connect with physical servers running at a remote site through private IPs.

You require:

Dynamic routing

A shared address space of 10.108.0.1/22

To make sure tunnels are not overprovisioned during a failover event


What are some Google-recommended practices for setting up a high-availability Cloud VPN for such a use case?


- Solution:

1. Create a custom mode VPC network.

2. Use Cloud Router border gateway protocol (BGP) routes with active/passive routing.


- **HA VPN's Active/Passive Routing option**

If a Cloud VPN tunnel goes down, it restarts automatically. If an entire virtual VPN device fails, Cloud VPN automatically instantiates a new one with the same configuration. The new gateway and tunnel connect automatically.

VPN tunnels connected to HA VPN gateways must use dynamic (BGP) routing. Depending on the way that you configure route priorities for HA VPN tunnels, you can create an active-active or active-passive routing configuration.


- In case of Active/Passive routing, it **uses a maximum of one tunnel** at a time so that the second tunnel is able to handle all your egress bandwidth if the first tunnel fails and needs to be failed over.


- Classic VPN and HA VPN gateways use external (internet routable) IPv4 addresses. Only **ESP, UDP 500, and UDP 4500 traffic** is permitted to these addresses. This applies to Cloud VPN addresses configured by you for Classic VPN or to automatically assigned IP addresses for HA VPN.


- We need a custom mode vpc so that subnets do not get created automatically as the ip range is mentioned in the question. Also, we will need active/passive HA VPN as it is not mentioned we will have to use more than one HA VPN gateway. It recommends using a custom mode VPC network, which allows for more control and flexibility in network configuration. It also suggests using Cloud Router border gateway protocol (BGP) routes, which support dynamic routing and provide high availability. Lastly, it mentions using active/passive routing, which ensures tunnels are not overprovisioned during a failover event.



### 32. Cloud SQL

- CASE: Your company has an internal performance tracking application that they want to migrate to GCP. All employees using the application are located in a single region. The application uses PostgreSQL and relies heavily on strong consistency and ACID transactions for multi-table write operations. Which database is most appropriate for this application?


- Solution: Cloud SQL


- Cloud SQL supports PostgreSQL, which can be used to deploy the application to GCP with minimal code changes as the existing application uses PostgreSQL. Cloud SQL is a fully managed relational database service that supports PostgreSQL. It provides strong consistency and ACID transactions, making it suitable for the performance-tracking application that relies heavily on these features.


- Cloud Spanner supports acid transactions and strong consistency it does not support the Postgres query Syntax and thus it will require lots of code changes. Cloud Spanner is a globally distributed, horizontally scalable, and strongly consistent relational database service. While it provides strong consistency and ACID transactions, it may be overkill for the scenario described in the question as all employees using the application are located in a single region.


- BigQuery does not provide strong consistency and ACID transactions. BigQuery is a fully managed, serverless data warehouse solution that is best suited for running fast and complex analytical queries on large datasets. It is not designed for strong consistency or ACID transactions.


- Cloud data storage and NoSQL database and integrating it require significant code changes. Cloud Datastore is a NoSQL document database service that does not provide strong consistency or ACID transactions. It is designed for high scalability and flexibility, but it may not be the best fit for an application that heavily relies on strong consistency and ACID transactions.



### 33. Understanding custom roles

- CASE: Your company has recently started using GCP and you are leading the initiative. Several developers and testers are participating in the pilot project. The project contains some sensitive data and only certain members of the team should have access to it. How can you assign appropriate identity and access management roles to the participants such that minimum maintenance is required?


- Solution:

1. Create different gruops based on the privileges required.

2. Assign users to their respective groups.

3. Assign an IAM Predefined role to each group as required, including those who should have access to sensitive data.


- Predefined roles are fine-grained enough to set permissions for specific roles requiring sensitive data access. This solution also uses groups, which is the recommended practice for managing permissions for individual roles. By creating different groups based on the privileges required, assigning users to their respective groups, and assigning an IAM Predefined role to each group as required, including those who should have access to sensitive data, the access management becomes streamlined and easier to maintain.


- Using custom roles requires more maintenance than using Predefined roles. 



### 34. gcloud config set container/cluster [cluster-name]

- CASE: You are part of the Kubernetes and Infrastructure Admin team at a digital news app company. You are responsible for managing a GKE cluster called ‘prod’. How can you ensure that all commands run from your local gcloud cli address this specific cluster by default?


- Solution: Run gcloud config set container/cluster prod command.


- The gcloud config set container/cluster dev command **sets the default cluster for your Google Cloud CLI**. By running the command "gcloud config set container/cluster dev", it sets the default cluster for the gcloud CLI to 'dev'. This means that any subsequent gcloud CLI commands will automatically be applied to the 'dev' cluster without the need to explicitly specify the cluster name in each command.



### 35. Cloud Function

- CASE: You are building an application that monitors changes in Cloud Storage and Firestore instances. Whenever a change occurs, an action needs to be invoked which will verify and process the updated data in almost real-time. How can you accomplish this with minimum setup?


- Solution: Call the data processing script from the Cloud Function triggers using Cloud Function events.


- Cloud Function can be triggered by both Cloud Storage and Firestore database changes, which will give a fast response in near real-time. Using Cloud Function triggers and events allows for a simple setup and seamless integration with Cloud Storage and Firestore instances. The data processing script can be called directly from the Cloud Function triggers whenever a change occurs. This approach ensures almost real-time processing with minimal setup and maintenance.



### 36. BigQuery DataViewer role

- CASE: You are leading the migration of accounting software from on-premises to Google Cloud for your organization. You have decided to use BigQuery for its financial transaction monitoring feature. The app allows Auditors to view the data and run reports in BigQuery, but they cannot perform transactions in the application. What is the simplest solution for this use case with the least maintenance?


- Solution: Provide the Auditors Google Group with roles/bigquery.dataViewer role.


- It is considered best practice to assign roles to Google Group and the roles/bigquery.dataViewer role only allows read-only access to the dataset. It provides the Auditors Google Group with the roles/bigquery.dataViewer role. This option simplifies maintenance by assigning the role to a group, and the roles/bigquery.dataViewer role grants the necessary permissions for auditors to view the data and run reports in BigQuery.



### 37. Cloud SQL Backup Recovery

- CASE: Your logistics application uses a Cloud SQL MYSQL instance. The laws in your country mandate you to retain a month-end copy of the database for three years. What steps should you take?


- Solution:

1. Rely on the automatic first-of-the-month backup functionality.

2. Set the bucket object auto-deletion to three years.

3. Store the backup to a Cloud Storage bucket with the Archive class.


- backups are managed by Cloud SQL according to retention policies, and are stored separately from the Cloud SQL instance to take the backup and store it in Bucket.

- Automatic backup: This is used when we have a fixed backup schedule i.e. on a particular day and time. As per this question, we need to retain a month-end copy of the database. On the last day of the month (At the time: 11:59:59 PM) we want to back up that entire month's data. So it will be great if we use automatic backup in this case. In this case, option-B is correct.

- It suggests relying on the automatic first-of-the-month backup functionality provided by Cloud SQL MYSQL. By enabling the automatic backup feature and storing the backup file in a Cloud Storage bucket with Archive class, the database can be retained for three years as mandated by the laws in the country. This option provides a simple and reliable solution without requiring manual intervention.


- Exporting a Cloud SQL MySQL database creates a logical representation of the data in the form of SQL statements or a SQL dump file. While exports can be useful for various purposes, such as data migration or analysis, they are not designed specifically for long-term data retention or backup purposes.

Here are a few reasons why option A is not the ideal choice:



1. Data Integrity: Exporting a database does not guarantee the same level of data integrity as a backup. Backups capture the entire state of the database at a specific point in time, including the database schema, indexes, and other metadata. On the other hand, an export may not capture all the necessary information to restore the database to its exact state.



2. Recovery Time: In the event of a disaster or data loss, restoring a database from an export file can be a time-consuming process. You would need to recreate the database structure, set up indexes, import the data, and perform other configuration steps manually. Backups, on the other hand, provide a more straightforward and efficient method of restoring the entire database.



3. Retention Policy: While Archive class Cloud Storage is a cost-effective storage option for infrequently accessed data, it may not be the most suitable choice for long-term database backups. Archive class storage is designed for data with minimal access requirements and a minimum storage duration of 365 days. Performing regular exports and storing them in an Archive class bucket might not align with the desired retention policy of retaining a month-end copy for three years.



In summary, while exporting a Cloud SQL MySQL database and storing the export file in an Archive class Cloud Storage bucket can be useful for certain purposes, it is not the recommended approach for retaining a month-end copy of the database for three years for audit purposes. Using the built-in automatic backups feature of Cloud SQL and storing the backups in an Archive class bucket provides a more reliable, efficient, and cost-effective solution for long-term data retention and recovery.



### 38. Deployment in GKE

- CASE: You work as an intern at a client-facing app. As part of the application modernization initiative at your organization, you have dockerized the app your team is working on. How can you deploy this app as a workload on Google Kubernetes Engine?


- Solution:

1. Upload the image to Container Registry.

2. Create a Kubernetes Deployment using the image.


- Deployment in kubernetes is used to manage pods which are the basic unit of compute on kubernetes. It suggests uploading the image to Container Registry, which is the best option for storing container images in Google Kubernetes Engine. Additionally, it recommends creating a Kubernetes Deployment using the image, which is the recommended method for deploying an app as a workload on Google Kubernetes Engine.



### 39. Migrating Consumer Accounts

- CASE: You work at a search engine company that has more than 1500 employees located in global offices. Your company has recently started using Cloud Identity for all of its GCP users. Some of the users in your organization already have a Google Account. How can you avoid conflicting accounts with Cloud Identity using Google's recommended practices?


- Solution: Invite the user to transfer their existing account.


- If a user created a personal Google Account using the domain name of your organization, it may result in a conflicting account. To resolve this, you need to invite the user to transfer their account to Cloud Identity. By inviting the user to transfer their existing account, you can avoid conflicting accounts with Cloud Identity. This allows the user to retain their existing account and data while seamlessly integrating it with Cloud Identity.


**Each consumer account that you plan to migrate must meet the following criteria:**

1. It can't be a Gmail account.

2. It must use a primary email address that corresponds to the primary or a secondary domain of your Cloud Identity or Google Workspace account. In the context of a consumer account migration, alternate email addresses and alias domains are ignored.

3. Its owner must be able to receive email on the account's primary email address.


**How consumer account works in Cloud Identity**

When you *add and verify a domain* in Cloud Identity or Google Workspace, any consumer account that uses an email address **with this domain** becomes an unmanaged account. For the user, this has no impact; they can sign in and access their data as normal.

Adding a domain in Google Workspace or Cloud Identity affects only users whose email address matches this exact domain. For example, **if you add example.com, the account johndoe@example.com is identified as an unmanaged account**, while johndoe@corp.example.com is not unless you also add corp.example.com to the Cloud Identity or Google Workspace account.

The existence of unmanaged accounts is surfaced to you as the Cloud Identity or Google Workspace administrator. You can then ask the user to transfer their account into a managed account.

In the preceding diagram, if the user johndoe consents to a transfer, the unmanaged account is converted to a managed account. The identity remains the same, but now Cloud Identity or Google Workspace controls the account, including all of its data.



### 40. GKE Node Pools

- CASE: Your image-sharing app consists of multiple microservices running in a GKE cluster. The image processing microservice requires a large amount of CPU time and relatively less memory. All other microservices are optimized for n1-standard machine types. How can you optimize your cluster to enable workloads to use resources as efficiently as possible?


- Solution:

1. Create a new node pool with compute-optimized machine type nodes.

2. Deploy the image processing microservice on those nodes.

3. Use the general purpose machine type node pool for the other microservices.


- The image rendering microservice requires a large amount of CPU which can be provided by compute-optimized machines. So it should be deployed on a separate node pool with compute optimized machine type while other services can be deployed on general purpose machine type node pool. Creating a new node pool with compute-optimized machine type nodes and deploying the image processing microservice on those nodes allows for efficient utilization of resources. By using compute-optimized machine type nodes, which are designed for CPU-intensive workloads, the image processing microservice can make the most of the available CPU resources. The general-purpose node pool can still be used for the other microservices, as they are optimized for n1-standard machine types.









































