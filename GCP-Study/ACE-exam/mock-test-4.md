### [Source of this study material : GCP Associate Cloud Engineer Practice Test Exam by Sayyam](https://www.udemy.com/course/latest-gcp-ace-google-associate-cloud-engineer-practice-exams-tests)


## Exam -4

### 1. Billing Data Export to BigQuery

- CASE: Your app-building company has several projects under its umbrella. Different teams at your enterprise have different cloud Budgets and their GCP billing is managed by different billing accounts. Your company has a centralized finance team that needs a single visual representation of all costs incurred. New cost data should be included in the reports as soon as it's available. What should you do?


- Solution: Export the billing data to BigQuery using Billing data export and create a Data Studio dashboard for visualization.


- You can run an analysis on Bigquery after exporting the billing reports from all projects to the same dataset. It suggests using Billing data export to export the billing data to BigQuery and then create a Data Studio dashboard for visualization. This option allows for the centralization of all costs incurred from different teams and billing accounts, providing a single visual representation for the finance team.



### 2. Create a New Node Pool

- CASE: You work at a billion-dollar RPG game development company. You are running your Gaming server on GKE on multiple pods running on four n1-standard-2 nodes on a GKE cluster. Additional pods need to be deployed on the same cluster requiring an n2-highmem-16 type of node. Your app is live in production and cannot afford downtime. What should you do?


- Solution:

1. Create a new Node Pool with n2-highmem-16 machine type.

2. Deploy the new pods.


- You can add new types of instances to the GKE cluster by adding node pools. It will not cause any downtime to the existing cluster. Creating a new Node Pool with the n2-highmem-16 machine type allows for the deployment of new pods on the same cluster. This option does not involve any downtime as the existing pods can continue running on the current nodes while the new pods are deployed on the new Node Pool.



### 3. Join data from Cloud Spanner and Bigtable together

- CASE: You work as a data scientist in an e-commerce shoe-selling company. Your website uses Cloud Spanner as its database backend to keep current state information about users. All events triggered by the users are logged in Cloud Bigtable. The Cloud Spanner data is exported every day to Cloud Storage for backup purposes. Your Datascience team is training an ML model on the user data and they need to join data from Cloud Spanner and Bigtable together. How can you fulfill this requirement as efficiently as possible?


- Solution: 

1. Create two separate BigQuery external tables on Cloud Storage and Cloud Bigtable.

2. Join these tables through user fields using the BigQuery console and apply appropriate filters. 


- Bigquery supports analytics on data through external tables from Cloud Storage and Bigtable. It is perfect for this use case. It suggests creating two separate BigQuery external tables on Cloud Storage and Cloud Bigtable. By doing so, the data from both sources can be directly queried and joined in BigQuery without the need for additional data movement or processing. The join can be performed using the user fields, and appropriate filters can be applied to retrieve the required data efficiently. This approach minimizes data movement, reduces processing overhead, and provides an efficient way to join data from both Cloud Spanner and Cloud Bigtable.


- An external data source is a data source that you can query directly from BigQuery, even though the data is not stored in BigQuery storage. For example, you might have data in a different Google Cloud database, in files in Cloud Storage, or in a different cloud product altogether that you would like to analyze in BigQuery, but that you aren't prepared to migrate.

**Use cases for external data sources include the following:**

For extract-load-transform (ELT) workloads, loading and cleaning your data in one pass and writing the cleaned result into BigQuery storage, by using a CREATE TABLE ... AS SELECT query.

Joining BigQuery tables with frequently changing data from an external data source. By querying the external data source directly, you don't need to reload the data into BigQuery storage every time it changes.



### 4. Join data from Cloud Spanner and Bigtable together

- CASE: You work at a large logistics and shipment company. The shipment tracking application is hosted on Compute Engine VMs in the us-central1-a zone. You want to make sure that the app does not go down in case of a zonal failure on GCP. How should you do it with minimum costs?


- Solution:

1. Create Compute Engine resources in us-central1-b.

2. Set up a load balancer to balance the load across both us-central1-a and us-central1-b.


- In order to remediate the problem of a single point of failure, we have to replicate VMs within multiple zones. It leverages the concept of geographical redundancy by creating resources in a different zone, us-central1-b, which ensures that the app does not go down in case of zonal failure. By setting up a load balancer, the traffic can be balanced across both zones, providing high availability at minimum costs.



### 5. Join data from Cloud Spanner and Bigtable together

- CASE: You have recently joined the security team at a big enterprise. Your first task is to inspect who has the project owner role in a certain GCP project. What should you do?


- Solution: View the current role assignments by running the command gcloud projects get iam policy.


```
gcloud projects get-iam-policy [project-ID]
```


![gcloud-projects-get-iam-policy](/GCP_pictures/ACE-exam/mock-test-4/gcloud-projects-get-iam-policy.PNG "gcloud projects get-iam-policy")


- Viewing the role assignments in the command line is the fastest and easiest way to check who has what role. Running the command "gcloud projects get iam policy" provides a comprehensive view of the current role assignments within a GCP project. This command retrieves the IAM policy for a project and displays all the role assignments, which include the project owner role. This allows the security team to inspect and determine who has the project owner role in the GCP project.



### 6. Secret Manager

- CASE: You work at a large credit card company that offers loans and credits to its customers. The company's app is hosted on GCP. There are 35 distributed backend microservices that your app requires. All the distributed microservices need to connect to a non-relational database using credentials. As the chief of DevSecOps, you want to make sure that the credentials are stored securely. Where should you store these credentials?


- Solution: Secret Manager


- The secret manager is a secure and convenient storage system for API keys, passwords, certificates, and other sensitive data. Secret Manager is a secure and dedicated storage service provided by Google Cloud. It is designed specifically for storing and managing sensitive data such as API keys, passwords, and other credentials. Secret Manager provides fine-grained access control and encryption, ensuring that the credentials are securely stored and accessed only by authorized services or users.



### 7. Kubernetes Subnet Range

- CASE: You work in an app development startup as a cloud engineer. Your company extensively uses Kubernetes on GKE. Several applications are deployed on separate VPC-native Google Kubernetes Engine clusters in the same subnet. There are no more IPs available in the subnet. How can you ensure that the clusters can grow in nodes when needed?


- Solution: Expand the CIDR range of the relevant subnet for the cluster.


- In this scenario, the main issue is the depletion of available IP addresses in the subnet used by the Google Kubernetes Engine (GKE) clusters. By expanding the CIDR range of the subnet, you're essentially increasing the pool of available IP addresses within that subnet. This expansion allows for accommodating additional nodes in the existing GKE clusters without requiring the complexity of creating new subnets or VPCs. This solution ensures scalability within the current setup. As the company grows and requires more resources within the GKE clusters, having an expanded CIDR range provides the flexibility to add more nodes without hitting IP address limitations.


- Adding an alias IP range does not expand the subnet. Adding an alias IP range to the current subnet will only provide additional IP addresses for the subnet, but it will not address the issue of running out of IPs. The alias IP range will be limited and may not be sufficient to support the desired growth of the clusters.



### 8. Preemptible VMs

- CASE: Every night at 1 AM, a batch job runs on your GCP project that uses a large number of VMs. The batch job is fault-tolerant and it can still run properly if some of the VMs get destroyed. Your goal is to reduce the cost of this job. What should you do?


- Solution:

1. Run the batch job in a simulation of maintenance events.

2. If the test succeeds use preemptible N1 Standard VMs for future jobs.


-  Preemptible VMs can provide up to 80% discount over normal VMs if the workloads are fault-tolerant. It proposes running the batch job in a simulation of maintenance events. This allows for testing if the job can still run properly even if some VMs get destroyed. If the test is successful, preemptible N1 Standard VMs can be used for future jobs. Preemptible VMs are significantly cheaper than regular VMs, helping to reduce costs.



### 9. Preventing Accidental VM deletion

- CASE: You work as a site reliability engineer in a firm with multiple GCP projects. You are building a customer-facing website on Compute Engine. Your GCP project is used by other teams to host their apps as well. How can you prevent other teams from accidentally causing downtime to your application?


- Solution: Enable deletion protection on the instance.


- You can protect specific VM instances from deletion by setting the deletionProtection property on an Instance resource. Enabling deletion protection on the instance addresses the specific concern of preventing other teams from accidentally causing downtime. When deletion protection is enabled, it adds an additional confirmation step to the deletion process, preventing accidental deletion of the instance by other teams. This helps safeguard the compute resources hosting the customer-facing website from accidental disruptions or downtime caused by other teams' actions.



### 10. Google Cloud Directory Sync (GCDS)

- CASE: here are thousands of employees in your company working from all over the globe. All users in your organization have an Active Directory account. Your organization wants to control and manage all of the Google’s and Google Cloud Platform accounts of employees through Active Directory. What should you do?


- Solution: Synchronize users into Cloud Identity using Google Cloud Directory Sync (GCDS).


- Google Cloud Directory Sync enables administrators to synchronize users, groups, and other data from an Active Directory/LDAP service to their Google Cloud domain directory. Using Google Cloud Directory Sync (GCDS) allows for the synchronization of users from an organization's Active Directory into Cloud Identity. This ensures that all users in the organization, regardless of their location, will have their accounts managed and controlled through Active Directory.



### 11. Access Control

- CASE: You are part of the Data Engineering team at an e-commerce company. You are managing the BigQuery dataset that contains user activity data. Another team has requested access to the BigQuery Dataset but you need to make sure they do not accidentally delete any datasets. What are some of the recommended best practices to grant access?


- Solution:

1. Create a custom role by removing delete permissions.

2. Add users to the group.

3. Then, add the group to the custom role.


-  A custom role with no delete permissions is the best option for this use case. Granting the role to groups is considered best practice. Creating a custom role by removing delete permissions and adding users to a group, and then adding the group to the custom role, allows for easier and more efficient management of user access. By adding users to a group, you can easily add or remove multiple users from the custom role without having to individually manage each user's access permissions. Additionally, by removing delete permissions from the custom role, you can ensure that users in the group cannot accidentally delete datasets.



### 12. sudo apt-get install google-cloud-sdk-datastore-emulator

- CASE: You are using Ubuntu for developing HRMS software on GCP. You installed the Google Cloud SDK using the Google Cloud Ubuntu package repository. Your application uses Cloud Datastore as its database. How can you test this app locally without deploying it to GCP?


- Solution: Install the google-cloud-sdk-datastore-emulator component using the **apt get install** command.


```
sudo apt-get install google-cloud-sdk-datastore-emulator
```


- The datastore emulator is installed using apt and not gcloud. When you install SDK using apt Cloud SDK Component Manager is disabled and you need to install extra packages again using apt.

- The google-cloud-sdk-datastore-emulator component provides a local emulator for Cloud Datastore. By installing this component using the apt-get install command, you can set up a local testing environment that emulates Cloud Datastore. This way, you can test your HRMS software locally without the need to deploy it to GCP. The emulator simulates Cloud Datastore behavior, allowing you to perform data operations locally during development and testing.

- "google-cloud-sdk-datastore-emulator" component allows you to run a local emulator for Cloud Datastore, which can be used to test the application without deploying it to GCP.

- As per the question, the Cloud SDK was installed from the Google Cloud Ubuntu package repository; hence, to install the datastore emulator, we should use the command in Option-C.

- When you install SDK using apt Cloud the sdk component manager is disabled and we need to install extra packages again using the apt command.



### 13. Understanding IAM roles

- CASE: Your company extensively uses the Google Cloud Platform for all its government-related projects. The projects are distributed in a complex hierarchical structure with hundreds of folders and projects. Only the Cloud Governance team is allowed to view the full hierarchical structure. What minimum permission (Google-recommended practices) should be given to the Governance team to perform their duties?


- Solution:

1. Add the users to a group.

2. Add this group to roles/iam.roleViewer role.


- roles/browser role provides Read access to browse the hierarchy for a project, including the folder, organization, and IAM policy. **This role doesn't include permission to view resources in the project.** By adding the users to a group and then adding that group to the roles/browser role, the users will be granted the necessary permission to view the full hierarchical structure. This approach follows Google's recommended practice of using groups to manage access and permissions.


- roles/iam.roleViewer allows viewing IAM policies and not project hierarchy. Giving the group the roles/iam.roleViewer role will still not give the users access to the full hierarchical structure.


### 14. SSO and SAML using Cloud Identity

- CASE: You are the head of data and security in a space research organization. Your company uses Active Directory Federation Service as a Security Assertion Markup Language (SAML) identity provider and integrates it to perform Single Sign On (SSO) with supported service providers. Your company uses Cloud Identity for using GCP. What should you do to allow users to log in to Cloud Identity using Active Directory credentials?


- Solution: Set up SSO with a third-party identity provider in Cloud Identity with Google as a service provider.


- Setting Google as the SSO Service provider will enable users to log in to their GSuite account with their SSO credentials. It suggests setting up SSO with a third-party identity provider in Cloud Identity with Google as a service provider. This option aligns with the scenario described in the question, where the company is using Active Directory Federation Service as its SAML identity provider. By setting up SSO with a third-party identity provider (such as Active Directory Federation Service) and configuring Google as the service provider, users would be able to log in to Cloud Identity using their Active Directory credentials.



### 15. Cloud Monitoring Workspaces

- CASE: You are working at a startup that specializes in creating digital simulations of chemicals. You are working in a small team responsible for maintaining the uptime of 3 different projects: A, B, and C. You want to monitor the CPU, memory, and disk of these projects in a single dashboard. What should you do?


- Solution: Create a workspace under project A, and then add project B and C.


- Workspaces is made for monitoring multiple projects. Creating a workspace under project A would allow you to have a centralized dashboard where you can monitor the CPU, memory, and disk of all three projects (A, B, and C) together. This option provides a single dashboard solution for monitoring and analysis of all projects.



### 16. Creating and managing service accounts

- CASE: You are the Owner of a fast-growing financial services startup. You have recently hired a person to manage all service accounts for Google Cloud Projects. What is the minimum permission you should grant this person to allow him to perform his duties?


- Solution: Provide the user with roles/iam.serviceAccountAdmin role.


- serviceAccountAdmin (roles/iam.serviceAccountAdmin): Includes permissions to list service accounts and get details about a service account. Also includes permissions to create, update, and delete service accounts and view or change the IAM policy on a service account. The roles/iam.serviceAccountAdmin role provides the minimum set of permissions required to manage all service accounts for Google Cloud Projects. This role grants the user the ability to create, update, and delete service accounts, as well as manage IAM policies for the service accounts. It is specifically designed for managing service accounts within Google Cloud.


- roleAdmin is a much broader role than what is required here. The roles/iam.roleAdmin role is not necessary for managing service accounts in Google Cloud Projects. This role grants full control over IAM policies and bindings, including the ability to create, update, and delete roles, but it is not specific to managing service accounts.


- securityAdmin role does not allow the management of service accounts. The roles/iam.securityAdmin role is also not specifically focused on managing service accounts. This role grants permissions to view and manage IAM policies, but it does not provide the necessary permissions for managing service accounts.


- serviceAccountUser does not allow the creation and management of service accounts. The roles/iam.serviceAccountUser role only provides the user with the ability to use service accounts, but it does not grant permissions to manage or administer service accounts. It is a more limited role compared to the roles mentioned in the other options.



### 17. How to export data to BigQuery

- CASE: You are running a free static website showcasing some high-quality 3D renders of an under-construction real-estate property. The renders are stored as large files on an Apache web server running on a Compute Engine instance. Several other applications are also running on the same GCP project. You want to be notified by email when the egress network costs for the server exceed 100 dollars for the current month as measured by Google Cloud. What should you do?


- Solution:

1. Export the billing data to BigQuery.

2. Write a Python-based Cloud Function that queries the BigQuery table to sum the egress network costs of the exported billing data for the Apache web server for the current month and sends an email if it is over 100 dollars.

3. Set up Cloud Scheduler to trigger the function hourly.


- Exporting the billing data to bigquery and analyzing the charges incurred by egress is the best option for this use case. It exports the billing data to BigQuery, allowing for more advanced querying and analysis. By writing a Python-based Cloud Function that queries the BigQuery table to sum the egress network costs for the Apache web server for the current month, it can send an email notification if the cost exceeds $100. Setting up Cloud Scheduler to trigger the function hourly ensures real-time monitoring and timely notifications.



### 18. How to deploy Cassandra and connect on Google Cloud Platform with a few clicks

- CASE: Your e-commerce webapp is currently self-hosted. You realized that it takes lots of server and data maintenance on your part. As part of your company’s plan to migrate the on-premise workload to Google Cloud, you have decided to migrate the development environments of a few non-critical applications first. The apps use Cassandra as their database. Cassandra instances for different apps need to be isolated from each other. How can you move them to Google Cloud quickly?


- Solution: Ask the developers to launch a Cassandra image for their development work using Google Cloud Marketplace.


- Launching Cassandra from the marketplace is the fastest and safest way. It allows the developers to quickly launch a pre-configured Cassandra image from the Google Cloud Marketplace. This eliminates the need for manual installation and ensures that the Cassandra instances are properly set up.



### 19. Set the default zone using the gcloud CLI

- CASE: Your company sells beauty products globally via a web-based application. You have recently started using the Google Cloud Platform. You downloaded and installed the gcloud command line interface (CLI) and authenticated it with your Google Account. There are several Compute Engine instances in your GCP projects that you want to manage through the command line. The instances are located in the europe-west1-d zone. How can you avoid having to specify the zone with each CLI command when managing these instances? 


- Solution: Use the gcloud config subcommand to set the europe-wets1-d zone as the default zone.


```
gcloud config set compute/zone europe-west1-d
```


- Setting the default zone will enable gcloud to use the same zone for all gcloud services without having to specify it every time a command is run. The gcloud config subcommand allows you to set various configurations for the gcloud CLI tool. By using the command **"gcloud config set compute/zone europe-west1-d"**, you can set the europe-west1-d zone as the default zone for all CLI commands. This way, you do not have to specify the zone with each command when managing instances, saving time and effort.


- Changing the compute engine metadata does not change the gcloud command-line config. Creating a Metadata entry on the Compute Engine page with key compute/zone will not affect the CLI commands. Metadata entries are primarily used to add custom key-value pairs to instances for various purposes, but they do not override the default zone used by the gcloud CLI tool.


- The default region and zone set in environment variables override the default region and zone set in your local client and in the metadata server.

To make these environment variables permanent, include these commands in your ~/.bashrc file and restart your terminal.

You can override environment variables by including the --zone or --region flag in your commands.



### 20. How to SSH into your GCE machine without a public IP

- CASE: You work as a cloud engineer at a social media app company. This app is using a hybrid cloud environment with some workloads on-premises and some on GCP Compute Engine VMs. The on-premise network communicates with the GCP VPC using Cloud VPN over private IPs. A new internal service needs to be deployed on Compute Engine such that no traffic from the public internet can be routed to it. What should create such a VM?


- Solution: Create the instance without a public IP address.


- An instance without a public IP address is not accessible through the internet. Creating the instance without a public IP address ensures that no traffic from the public internet can be routed to it. By not assigning a public IP address, the VM can only be accessed through private IP addresses within the network.


- Enabling Private Google Access does not prevent internet traffic from entering the VM. Enabling Private Google Access allows instances to reach Google APIs and services using internal IP addresses, but it does not prevent traffic from the public internet from being routed to the VM. It is mainly used for instances that do not have public IP addresses but still require access to Google services.



### 21. How to SSH into your GCE machine without a public IP

- CASE: You are part of the infrastructure governance team at your digital ad agency. One of the apps is going through a revamp and requires changes in infrastructure as well. You need to get the proposed changes reviewed by your team. What is Google's recommended practice for it?


- Solution: 

1. Describe the proposed changes using Deployment Manager.

2. Store them in Cloud Source Repositories.


- It aligns with Google's recommended best practices for managing infrastructure changes. Deployment Manager templates allow you to define and describe your infrastructure changes in a declarative manner. Storing these templates in Cloud Source Repositories provides version control, collaboration, and a centralized location for managing the changes.


- Cloud Source Repositories are specifically designed for hosting and versioning source code. While Deployment Manager templates are not traditional source code, they are configuration files that define the desired state of the infrastructure. Storing them in a source code repository allows you to track changes, manage different versions, and collaborate with the rest of the team effectively.



### 22. GKE Node Auto Provisioning

- CASE: Your data science team uses Google Kubernetes Engine for running their machine learning pipelines. These pipelines mostly train image processing models. Some of the long-running, non-restartable jobs in a few pipelines require the use of GPU. How can you fulfill the request at an optimal cost?


- Solution: Use the GKE cluster's node auto-provisioning feature.


- Node auto-provisioning is a mechanism of the cluster autoscaler, which scales on a per-node pool basis. With node auto-provisioning enabled, the cluster autoscaler can extend node pools automatically based on the specifications of unschedulable Pods. Using the GKE cluster's node auto-provisioning feature allows for dynamically provisioning nodes with GPUs only when they are needed. This helps optimize cost as resources are only allocated as necessary.


- For infrequent access, you don't want to have a permanent homogeneous cluster. Enabling autoscaling on a node pool with a minimum size of 1 would not optimize cost. This means that there would always be at least 1 GPU-enabled instance running, even if it's not currently being utilized. This could lead to unnecessary costs when the GPU is not needed.


- The question mentions "You want to minimize the cost". D is clearly not ideal because 1 instance with GPUs running all the time for an incidental job is too expensive and is not recommended here.

Using auto-provisioning (Option-A) new node pools are created and deleted automatically.


- To enable the **node auto-provisioning**, run the following command:


```
gcloud container clusters update CLUSTER_NAME \
    --enable-autoprovisioning \
    --min-cpu MINIMUM_CPU \
    --min-memory MIMIMUM_MEMORY \
    --max-cpu MAXIMUM_CPU \
    --max-memory MAXIMUM_MEMORY \
    --autoprovisioning-scopes=https://www.googleapis.com/auth/logging.write,https://www.googleapis.com/auth/monitoring,https://www.googleapis.com/auth/devstorage.read_only
```


- Using the **node auto-provisioning config file**:


```
resourceLimits:
  - resourceType: 'cpu'
    minimum: 4
    maximum: 10
  - resourceType: 'memory'
    maximum: 64
  - resourceType: 'nvidia-tesla-k80'
    maximum: 4
management:
  autoRepair: true
  autoUpgrade: true
shieldedInstanceConfig:
  enableSecureBoot: true
  enableIntegrityMonitoring: true
diskSizeGb: 100
```


- Apply the configuration file by running:


```
gcloud container clusters update CLUSTER_NAME \
   --enable-autoprovisioning \
   --autoprovisioning-config-file FILE_NAME
```


- With Autopilot clusters, you don't need to manually provision nodes or manage node pools because GKE automatically manages node scaling and provisioning. Node auto-provisioning looks at Pod requirements in your cluster to determine what type of nodes would best fit those Pods.


- Node auto-provisioning automatically manages and scales a set of node pools on the user's behalf. Without node auto-provisioning, the GKE cluster autoscaler creates nodes only from user-created node pools. With node auto-provisioning, GKE automatically creates and deletes node pools.


- Node auto-provisioning creates node pools based on the following information:

1. CPU, memory, and ephemeral storage resource requests.
2. GPU requests.
3. Pending Pods' node affinities and label selectors.
4. Pending Pods' node taints and tolerations.



### 23. GKE Node Auto Provisioning

- CASE: You are building a stock trading app using Compute Engine and Cloud SQL. The app is deployed in a development environment and you are planning to release it to the general public soon. You need to create a production environment for the release. Your security team has given a list of recommendations to be implemented for the production environment. One of the non-negotiable requirements is that network routes should not exist between the two environments. What is the Google-recommended way of fulfilling this requirement?


- Solution:

1. Create a new GCP project.

2. Enable the Compute Engine and Cloud SQL APIs.

3. Replicate the development environment setup in the new project.


- Keeping the development and production environments separate is a best practice as it is the best way to isolate the environments. It suggests creating a new GCP project and replicating the development environment setup in the new project. By doing this, the production environment is completely isolated from the development environment, ensuring that there are no network routes between the two environments.


- The shared VPC allows entities in both VPCs to communicate as if they were in the same VPC. That's wrong. It suggests updating the existing VPC to be a Shared VPC and replicating the development environment setup in a new project within the Shared VPC. While this does create some level of isolation between the development and production environments, it does not completely eliminate network routes between them.



### 24. Organization Policy

- CASE: The production environment of your Cryptocurrency trading website is going through an external security audit. The Organization Policy called Domain Restricted Sharing is applied on the organization node, preventing users other than the organization’s Cloud Identity domain from gaining access to the GCP organization. The auditor needs to view the resources in the project but not edit anything. How can you enable this access?


- Solution:

1. Create a temporary account for the auditor in Cloud Identity.

2. Give that account the Viewer role on the project.


- It involves creating a temporary account for the auditor within the organization's Cloud Identity domain, thus complying with the Domain Restricted Sharing policy. By giving this account the Viewer role on the project, the auditor will be able to view all resources in the project without the ability to edit them. This method adheres to the policy constraints and fulfills the audit requirements by enabling read-only access to the auditor who is now considered part of the organization's domain.


- The security reviewer role is over-permissive and against the best practices. The Security Reviewer role allows the user to not only view resources but also review security configuration and settings within the project, which is not required for the audit.



### 25. Snapshot Best Practice

- CASE: You are running a Social Media Platform on Compute Engine. You cannot afford to lose any user data and you need to back up the VM’s boot disk regularly. You also need to make sure the data can be restored quickly in case of a disaster. Older backups should be deleted automatically to save costs. What is the Google Recommended approach for it?


- Solution: Create a snapshot schedule for the disk using the desired interval.


- Snapshots and disks are independent objects on GCP, you could create a snapshot from the disk and then delete the disk, and the snapshot will stay in place. Actually, you could use this snapshot to create a new disk, assign to another VM, mount it, and use it (all the information that the original disk had at the time of the snapshot will still be there). Creating a snapshot schedule for the disk using the desired interval is the recommended approach for backing up the VM's boot disk. Snapshots are point-in-time copies of the disk, and by creating a schedule, you can ensure regular backups are taken. Snapshots are efficient for backup and restore operations, and by using them, you can quickly restore the data in case of a disaster. Additionally, with a snapshot schedule, you can also configure the retention policy to automatically delete older backups, helping to save costs.



### 26. Access Control

- CASE: You have been assigned to facilitate an external audit of your travel booking application hosted on GCP. The Auditor has requested for permissions to review your GCP Audit Logs and also to review your Data Access logs. What Cloud Identity and Access Management (Cloud IAM) should you provide to the Auditor? 


- Solution:

1. Provide the auditor with the IAM role roles/logging.privateLogViewer.

2. Direct the Auditor to also review the logs for changes to Cloud IAM policy.


- The role roles/logging.privateLogViewer is required to view data access logs and the logs can be accessed from the logs console. It provides the auditors with the IAM role for private log viewing. Additionally, it directs the auditors to also review the logs for changes to Cloud IAM policy. This ensures that the auditors have access to the necessary logs for their review.


- Audit logs help you answer "who did what, where, and when?" within your Google Cloud resources with the same level of transparency as in on-premises environments. Enabling audit logs helps your security, auditing, and compliance entities monitor Google Cloud data and systems for possible vulnerabilities or external data misuse.


**Admin Activity audit logs**
Admin Activity audit logs contain log entries for API calls or other actions that modify the configuration or metadata of resources. For example, these logs record when users create VM instances or change Identity and Access Management permissions.


Admin Activity audit logs are always written; you can't configure, exclude, or disable them. Even if you disable the Cloud Logging API, Admin Activity audit logs are still generated.


**Data Access audit logs**
Data Access audit logs contain API calls that read the configuration or metadata of resources, as well as user-driven API calls that create, modify, or read user-provided resource data.


Publicly available resources that have the Identity and Access Management policies allAuthenticatedUsers or allUsers don't generate audit logs. Resources that can be accessed without logging into a Google Cloud, Google Workspace, Cloud Identity, or Drive Enterprise account don't generate audit logs. This helps protect end-user identities and information.

Data Access audit logs—except for BigQuery Data Access audit logs—are disabled by default because audit logs can be quite large. If you want Data Access audit logs to be written for Google Cloud services other than BigQuery, you must explicitly enable them. Enabling the logs might result in your Google Cloud project being charged for the additional logs usage. 



### 27. Best Practice for working with Google Cloud Audit Logging

- CASE: Your company runs multiple websites on different GCP projects for selling groceries, medicines, liquor, etc. Your security team is developing an anomaly detection tool that will be used to analyze all logs from all projects over the last 60 days. To facilitate the development of the tool, you need to enable the security team to quickly explore and analyze the log contents. What is the Google recommended practice to obtain combined logs of all projects?


- Solution:

1. Export the logs using a Stackdriver Logging Export with a Sink destination to a BigQuery dataset.

2. Configure the table partitioning in BigQuery based on the log timestamp and set up a lifecycle policy to delete partitions older than 60 days.


- This option involves exporting logs from Stackdriver Logging to BigQuery, which is a robust data warehousing solution capable of handling large datasets efficiently. By configuring table partitioning based on log timestamps in BigQuery and setting up a lifecycle policy to delete older partitions, it ensures that only logs within the last 60 days are retained for analysis. This aligns perfectly with the requirement of analyzing logs for the last 60 days while managing data retention effectively.

- This way, logs are segmented into partitions based on timestamps, ensuring that only the necessary data (logs within the last 60 days) is retained for the security team's anomaly detection tool. Old data beyond the required timeframe is automatically managed and deleted as per the defined lifecycle policy.



### 28. Managing Projects

- CASE: Your company is a well-reputed firm in the food delivery sector. Your company has hosted its web and mobile applications on GCP. You are responsible for managing GCP costs for your organization. You have identified that a certain division of your company has several services configured but they are not using them. What should you do to turn off all configured services in the GCP project?


- Solution:

1. Make sure you have the Project Owner IAM role for this project.

2. Navigate to the project in the GCP console, click Shut down, and then enter the project ID.


- An owner of a GCP project can shut it down. It outlines the correct steps to turn off all configured services in the GCP project. First, the person should have the Project Owner IAM role for this project, which gives them the necessary permissions. Then, they need to navigate to the project in the GCP console and click on the "Shut down" option. Finally, they should enter the project ID to confirm the shutdown.


- Organizational Administrator IAM role does not include the permissions necessary to delete a project or its resources in the Google Cloud Platform. This role is focused on broader organizational management and lacks specific permissions like resourcemanager.projects.delete, which are essential for project deletion. Therefore, someone with the Organizational Administrator role would be unable to execute the steps in Option C for shutting down a GCP project, as they cannot directly delete the project or its resources. The Project Owner IAM role, in contrast, has the required permissions for such actions.



### 29. Access Control examples

- CASE: You are responsible for maintaining all Service Accounts for your Logistics application that is distributed over multiple projects. Some activity data is stored in a bigquery dataset in the em-databases-app project and it needs to be accessed by VMs in a web-applications project. How can you enable this access to service accounts using Google’s recommended practices?


- Solution: Grant bitquery.dataViewer role to em-databases-app and appropriate roles to web-applications.


- Granting the bigquery.dataViewer role to em-databases-app ensures that the service account in the em-databases-app project has the necessary permissions to view the data in the bigquery dataset. Additionally, granting appropriate roles (such as the necessary permissions or roles for accessing the dataset or resources) to the web-applications project ensures that the service account in the web-applications project also has the necessary permissions to access the dataset in the em-databases-app project. This combination of granting roles to both projects ensures that the service account can access the dataset as recommended by Google's practices.



### 30. Configure Data Access

- CASE: One of your key employees received a job offer from another cloud company. S/he left the Organization without giving notice. His Google Account was kept active for 3 weeks. How can you find out if the employee accessed any sensitive data after s/he left?


- Solution:

1. Visit Cloud Logging to view Data Access audit logs.

2. Search for the user's email as the principal.


- The data access logs show if the user tried to access any sensitive data. It suggests visiting Cloud Logging to view Data Access audit logs, which can provide a detailed record of data access activities. By searching for the user's email as the principal, it is possible to identify if the employee accessed any sensitive data.



### 31. Custom Role Permissions Support

- CASE: You work at a top tech firm that provides CRM solutions to its clients around the globe. One of the CRM projects is hosted on GCP. One of the use cases for a GCP service in your project requires a custom IAM role. The permissions in the role must be suitable for production use. Your security team needs to keep track of the status of this custom role. This will be the first version of the custom role, but it may get new versions in the future. What should you do?


- Solution:

1. Make sure all permissions in your role have a 'supported' support level for role permissions.

2. Set the role stage to ALPHA while testing the role permissions.


- Custom roles include a launch stage, which is stored in the stage property for the role. The launch stage is informational; it helps you keep track of whether each role is ready for widespread use. ALPHA means the role is still being developed or tested, or it includes permissions for Google Cloud services or features that are not yet public. It is not ready for widespread use.


- Setting the role stage to BETA might imply that the role is still in a testing or pre-production phase, potentially conflicting with the need to have permissions ready for production. Using BETA might suggest an ongoing evaluation phase rather than indicating that the permissions are considered production-ready.


- The permissions that have status TESTING may not be yet fully supported to be used with custom roles. Thus, they are not fit for production use. It suggests using a 'testing' support level for role permissions, which may not provide the necessary level of confidence in the stability and suitability of the permissions for production use. Additionally, setting the role stage to ALPHA does not guarantee that all permissions in the role have a 'supported' support level.



### 32. Access Control to BigQuery

- CASE: You have created a UI on the App engine that queries BigQuery and aggregates the data to create beautiful visualizations. The application uses the default App Engine Service Account. The BigQuery dataset is managed by another team in a different GCP project. You don’t need access to the GCP project but your app needs to create the visualizations by reading the data from BigQuery. What should you do?


- Solution: Ask the other team to grant the BigQuery Data Viewer role to your default App Engine Service account.


- The Bigquery data viewer role allows users to read data and metadata from the table or view. The BigQuery Data Viewer role grants the necessary permissions to read data from BigQuery. By granting this role to the default App Engine Service account, the application will be able to create visualizations by querying and aggregating the data from BigQuery.


- Bigquery job user role Provides permissions to run jobs, including queries, within the project, it is not suitable to read data. The BigQuery Job User role only allows the user to submit jobs to BigQuery, but it does not grant the necessary permissions to read data from BigQuery or create visualizations.



### 33. Cloud Dataflow and Cloud Storage

- CASE: Your Motorcycle company is going through a Digitization phase. There are a lot of unstructured files in different file formats. ETL transformations on the data will be performed using Cloud Dataflow. What should you do to make the data accessible on Google Cloud?


- Solution: Use the gsutil command line tool to upload the data to Cloud Storage.


- Cloud Storage is object storage and can store files of any type. The gsutil command line tool is used to interact with Cloud Storage, which provides a scalable and durable object storage solution. It is well-suited for storing and accessing unstructured files. By using gsutil, you can upload the unstructured files to Cloud Storage and make them accessible on Google Cloud.



### 34. gcloud config set

- CASE: You are part of the Google Cloud operations team at the Digital vertical of your retail stores' chain. You are managing multiple projects. How can you configure the Google Cloud SDK to easily manage multiple projects?


- Solution:

1. Make a separate configuration for each project you need to manage.

2. Activate the appropriate configuration for each of your assigned Google Cloud projects as required.


- It is considered best practice to create separate configurations for separate projects and switch between them as needed. It suggests making a separate configuration for each project that needs to be managed. This allows for better organization and separation of settings for each project. Additionally, activating the appropriate configuration for each assigned project ensures that the correct settings are used when working on a specific project.


- **Set the project property**


```
gcloud config set project PROJECT_ID
```

- **Set the zone property in the compute section**


```
gcloud config set compute/zone ZONE_NAME
```

- **To set a proxy with the appropriate type, and specify the address and port on which to reach it, run:**


```
gcloud config set proxy/type http
gcloud config set proxy/address 1.234.56.78
gcloud config set proxy/port 8080
```


- gcloud config set sets the specified property in your active configuration only. A property governs the behavior of a specific aspect of Google Cloud CLI such as the service account to use or the verbosity level of logs. To set the property across all configurations, use the --installation flag.



### 35. How to update Instance Templates

- CASE: You are part of the production support team for a global e-commerce app. You received an alert that a new instance creation failed to create new instances on a managed instance group used by the app. The app requires the number of active instances specified in the template to serve its users properly. What should you do in such a scenario?


- Solution:

1. Create a new instance template with a valid syntax and set disks.autoDelete=true.

2. Delete existing persistent disks with the same name as instance names.

3. Make rolling update (to switch to a new template).


- We cannot update an existing template hence our best option is to create a new instance template and set disks.autoDelete=true. Also, we need to make a rolling update in order to switch to a new instance. It provides a sequence of steps to resolve the issue. It suggests creating a new instance template with a valid syntax, and setting the disks.autoDelete property to true, deleting existing persistent disks with the same name as instance names, and performing a rolling update to switch to the new template. This sequence of steps helps in resolving the issue and ensuring proper instance creation on the managed instance group.


**NOTE**: When auto-delete is on, the persistent disk is deleted when the instance it is attached to is deleted.


**How to update instance templates**
Instance templates are designed to create instances with identical configurations. So you cannot update an existing instance template or change an instance template after you create it.

If you need to make changes to the configuration, create a new instance template. You can create a template based on an existing instance template, or based on an existing instance. You can also override instance template fields when creating a VM instance from an instance template.



- To enable auto-delete for a disk named 'my-disk' on an instance named 'my-instance', run:


```
gcloud compute instances set-disk-auto-delete my-instance --auto-delete --disk=my-disk
```


- To make a rolling update to the new instance template for MIG


```
gcloud compute instance-groups managed rolling-action start-update INSTANCE_GROUP_NAME \
    --version=template=INSTANCE_TEMPLATE_NAME
    [--zone=ZONE | --region=REGION]
```

Replace the following:

INSTANCE_GROUP_NAME: the name of the MIG
INSTANCE_TEMPLATE_NAME: the new instance template
ZONE: for zonal MIGs, provide the zone
REGION: for regional MIGs, provide the region



- we cannot delete an existing instance template when it's in use. We need a rolling update. It suggests creating a new instance template to replace the existing one and ensuring that the instance name and persistent disk name values are different in the template.



### 36. Monitoring Alerts

- CASE: You are part of the SRE team responsible for maintaining the site reliability for an e-commerce application in production on Compute Engine. You want to be proactive about monitoring the environment and want to be notified by email if the Compute Engine Instance’s CPU utilization goes above 90%. What Google Services can you use to achieve this?


- Solution:

1. Go to Stackdriver Monitoring and a Cloud Monitoring Workspace and associate your Google Cloud Platform (GCP) project with it.

2. Create a Cloud Monitoring Alerting Policy that uses the threshold as a trigger condition.

3. Configure your email address in the notification channel.


- Stackdriver Alerting gives timely awareness to problems in your cloud applications so you can resolve the problems quickly. It suggests using Stackdriver Monitoring and Cloud Monitoring Workspace to monitor the CPU utilization. By associating the GCP project with Stackdriver Monitoring, you can create a Cloud Monitoring Alerting Policy that triggers when the CPU utilization exceeds the threshold. The email notification can be configured with the desired email address.


**The Cloud Monitoring alerting process contains three parts:**

An alerting policy, which describes the circumstances under which you want to be alerted and how you want to be notified about an incident. The alerting policy can monitor time-series data stored by Cloud Monitoring or logs stored by Cloud Logging. When that data meets the alerting policy condition, Cloud Monitoring creates an incident and sends the notifications.

Each incident is a record of the type of data that was monitored and when the conditions were met. This information can help you troubleshoot the issues that caused the incident.

A notification channel defines how you receive notifications when Cloud Monitoring creates an incident. For example, you can configure an notification channel to email my-support-team@example.com and to post a Slack message to the channel #my-support-team. An alerting policy can contain one or more notification channels.


**Alerting policies can evaluate two types of data:**

Time-series data, also called metric data, which is stored by Monitoring. These types of policies are called metric-based alerting policies.

To learn how to set up a metric-based alerting policy, try the Quickstart for Compute Engine.

Log data stored by Cloud Logging. These types of policies are called log-based alerting policies. Log-based alerting policies notify you when a particular message appears in your logs.


The alerting process helps you respond to issues when the performance of an application fails to meet acceptable values. For example, you deploy a web application onto a Compute Engine virtual machine (VM) instance. While you expect the HTTP response latency to fluctuate, you want your support team to respond when the application has high latency for a significant time period. You could create a metric-based alerting policy that monitors the application's HTTP response latency metric. If the response latency is higher than two seconds for at least five minutes, then Monitoring creates an incident and sends email notifications to your support team.



### 37. Cloud Spanner Autoscaler

- CASE: Your Online multi-player RPG game uses Cloud Spanner as its Database to store, update, and retrieve player points. The game receives traffic in a very predictable manner. How can you automatically scale up and scale down the number of Spanner nodes depending on traffic?


- Solution:

1. Create a Cloud Monitoring alerting policy that sends an alert to a webhook when the Cloud Spanner CPU is over or under the threshold. 

2. Create a Cloud Function that listens to HTTP and resizes Spanner resources accordingly.


- Alerting policy is the most proactive approach to auto-scaling and a cloud function is a good candidate for the backend service responsible for scaling spanner nodes up or down. It recommends creating a Cloud Monitoring alerting policy that sends an alert to a webhook when the Cloud Spanner CPU is over or under the threshold. Additionally, it proposes creating a Cloud Function that listens to HTTP and automatically resizes the Spanner resources accordingly. This solution enables real-time scaling by utilizing automation and the capabilities of Cloud Functions to respond to alerts and trigger resizing actions. It eliminates the need for manual intervention and minimizes delays in scaling up or down based on traffic changes.



### 38. Load Balancing Options

- CASE: You are a software engineer at a startup. You have built an image search API service that is used by users from all over the world. The application receives SSL-encrypted TCP traffic on port 443. Which load balancing option should you use to minimize latency for the clients?


- Solution: SSL Proxy Load Balancer


- SSL Proxy Load Balancing is a reverse proxy load balancer that distributes SSL traffic coming from the internet to virtual machine (VM) instances in your Google Cloud VPC network.

- Minimize latency for global users means SSL offloading close to those users while sending the traffic as much through the Google network as possible as opposed to over the internet. This means we need to use SSL Load Balancer.

- Moreover, SSL Proxy Load Balancing support for the following ports: 25, 43, 110, 143, 195, 443, 465, 587, 700, 993, 995, 1883, 3389, 5222, 5432, 5671, 5672, 5900, 5901, 6379, 8085, 8099, 9092, 9200, and 9300.



### 39. Local SSDs

- CASE: You work at a software solutions company and you have hosted your HRMS software on a general-purpose Compute Engine instance. Your application is experiencing excessive disk read throttling on its Zonal SSD Persistent Disk. The disk size is currently 350 GB. The application primarily reads large files from disk. How can you provide a maximum amount of throughput with an optimal cost?


- Solution: Use a Local SSD on the instance instead.


- Local SSD has more IOPS (Input/Output Operations Per Second). Moreover, SSD persistent disks are designed for single-digit millisecond latencies. Observed latency is application-specific.


- Local SSDs are physically attached to the server that hosts your VM instance. Local SSDs have higher throughput and lower latency than standard persistent disks or SSD persistent disks. The performance gains from local SSDs require certain trade-offs in availability, durability, and flexibility.


- Here are the calculations (taken from GCP when creating an instance):

350 Gb SSD Persistent disk: 59.50$/month, read IOPS: 10 500 with n1-standard-1

1000 Gb SSD Persistent disk: 170.00$/month, read IOPS: 15 000 with n1-standard-1

375 Gb Local SSD (NVMe): 30.00$/month, read IOPS: 170 000 with n1-standard-1


These values prove that switching to a local SSD makes it cheaper and faster. Adding CPUs will make it more expensive than the old price.



### 40. Expand subnet IP range

- CASE: One of your Machine Learning pipelines at your AI services company uses Dataproc. The Dataproc cluster runs in a single VPC network in a single subnet with range 10.0.2.0/25. The VPC network does not have any more private IP addresses left. You need to add a few more VMs to communicate with the cluster. How can you do it with the minimum number of steps?


- Solution: Modify the existing subnet range to 10.0.2.0/24.


- It is possible to increase the IP range of a subnet after creation. This option allows for expanding the available IP address range within the same VPC network, providing additional addresses for the new VMs. By modifying the subnet range from /25 to /24, the subnet size is increased, which allows for more IP addresses to be assigned. This can be done without the need to create additional VPC networks or establish VPC peering. We can increase the CIDR range with a minimum number of steps.


**To expand the IP range of SUBNET to /16, run:**


```
gcloud compute networks subnets expand-ip-range SUBNET --region=us-central1 --prefix-length=16
```


### 41. Custom Images and Snapshots

- CASE: Your startup recently got acquired by a large E-commerce company and it has significantly increased the traffic to your website. Your website is hosted on a custom Compute Engine instance. You need to create a copy of your VM to facilitate the increase in demand (NOTE: A custom image already exists). What should you do?


- Solution: 

1. Create a Compute Engine snapshot from the base VM.

2. Create a custom Compute Engine image from this snapshot.

3. Use the image to launch new instances.


- Custom images are ideal for situations where you have created and modified a persistent boot disk or specific image to a certain state and need to save that state for creating VMs.


- This option follows a more standard and recommended process in GCP. It suggests creating a snapshot from the base VM, which captures the current state of the disk. From this snapshot, a custom image is created. This custom image serves as a template from which new instances can be launched. This method allows scalability by creating multiple instances from the custom image to handle the increased demand, aligning with best practices in GCP.


- In summary, an image is a template used to create new VM instances, while a snapshot is a copy of a persistent disk used for backup and recovery purposes. **Images are used to create instances with the same configuration, while snapshots are used to create new disks or restore existing ones.**


- Options A and B propose using snapshots directly to create images or instances, which isn't standard in GCP. Option C involves creating a custom image from a snapshot, which is valid, but the subsequent mention of "creating new images" could be inaccurate. Option D, however, correctly suggests creating a custom image from a snapshot and then using instances from that image, aligning with recommended practices in GCP to handle increased demand.



### 42. Cloud Logging Agent

- CASE: You are running a website to sell products made by local artisans on a single Compute Engine instance. Some of your users have reported that they are getting errors while using the application. The application writes logs to the disk. How can you diagnose the problem?


- Solution: Install and configure the Cloud Logging Agent on the VM and view the logs from Cloud Logging.


- Cloud Logging agent needs to be installed in the VM so that the logs can be collected and sent to Cloud Logging for analysis. Installing and configuring the Cloud Logging Agent on the VM allows the application logs written to the disk to be automatically collected and sent to Cloud Logging. This enables real-time access to the logs, making it easier to diagnose and troubleshoot any errors or issues with the application.



### 43. IAM roles and Access Control

- CASE: You work in the business intelligence engineering department in your company. You are collaborating with another team at your organization to build a Business Intelligence Dashboard for the directors of the company. The other team owns the data which they use to generate reports on a daily basis using a CRON job on a VM in a corp-data-analysis project. Your team is working on the frontend of the dashboard and they need a copy of the daily exports in the bucket corp-total-analysis-storage in the corp-total-analysis project. You are asked to configure access for the daily exports from the VM to be made available in the bucket corp-total-analysis-storage in as few steps as possible using Google’s recommended practices. What should you do?


- Solution: Assign Storage Object Creator to the VM service account on corp-total-analysis-storage.


- Granting the service account access to create objects in the other project is the fastest and the recommended way to achieve this. Assigning the Storage Object Creator role to the VM Service Account on corp-total-analysis-storage allows the VM to create and write objects (daily exports) to the specified bucket. This aligns with the requirement of making the daily exports available in the bucket.



### 44. Set the Authentication

- CASE: You are building an API using Python. The API internally uses several Google Cloud Services using Application Default credentials. You have tested the API locally and it works correctly. As a next step, you want to deploy the API on a Compute Engine Instance. How can you set up authentication using Google-recommended practices and minimal changes?


- Solution: Provide necessary IAM permissions for Google services to the Compute Engine VM's service account.


- You can attach service accounts to resources for many different Google Cloud services, including Compute Engine, Google Kubernetes Engine, App Engine, Cloud Run, and Cloud Functions. We recommend using this strategy because it is more convenient and secure than manually passing credentials. It is recommended to provide necessary IAM permissions for Google services to the Compute Engine VM's service account. By granting the required IAM permissions to the service account, the API deployed on the Compute Engine Instance will have the necessary access to the Google Cloud services it needs to interact with.



### 45. Migrating a workload to a Compute Engine VM

- CASE: You are working at a steel company that aims to transform its digital processes by moving to the Google Cloud Platform. You have identified a monthly running Batch job (that takes 40 hours to complete) on your on-premises data center as a candidate for cloud migration. The job process can be performed offline, and it must be restarted if interrupted. What is the best approach for migrating this workload to GCP?


- Solution: 

1. Migrate the workload to a Compute Engine VM.

2. Start and stop the instance as needed.


- Migrating the workload to a standard Compute Engine VM and starting/stopping the instance as needed offer the most reliability and control for a long-running, offline batch job that requires 40 hours to complete and must be restarted if interrupted. Compute Engine VMs provide persistent, on-demand compute capacity that can be tailored to the job's requirements, including custom machine types and the ability to stop and start the instance, thus optimizing costs when the resources are not in use. This approach avoids the risk of preemption and ensures that the job can run to completion without interruption, aligning with the workload's requirements.


- A preemptible VM is not fit for long-running tasks as it can be terminated anytime. Creating an Instance Template with Preemptible VMs and a Managed Instance Group might not be the best approach for this scenario. While it could provide some level of fault tolerance with the ability to automatically recreate terminated instances, it may not guarantee data integrity or consistent job execution if the instance is terminated before the workload is completed. Additionally, adjusting the Target CPU Utilization might not address the requirement of restarting the job if interrupted.


NOTE:

If the task is stopped it is needed to restart AND it takes 40 hours. Preemptible will stop in 24 hours and restart will happen which means JOB will never finish. Be it VM or K8s. Hence, the correct answer is C.



### 46. Cloud Bigtable

- CASE: You are running a new-age business of commercial vehicle renting business. Sensors on the vehicles monitor signals like engine status, distance traveled, fuel level, and more. The customers are billed based on these metrics. The devices can emit a very high amount of data, up to thousands of events per hour per device. The system needs to store the individual signals atomically and data retrieval should be consistent based on the time of the event. What should you do?


- Solution:

1. Load the data into Cloud Bigtable.

2. Use the event timestamp to create a row key based event.


- Cloud Bigtable is a petabyte-scale no-SQL database that is very good at storing and analyzing time-series data. Cloud Bigtable is a scalable, fully managed NoSQL wide-column database. It is designed for storing and retrieving large amounts of data with low latency. By using the event timestamp to create a row key, you can ensure consistent data retrieval based on event time. Bigtable can handle the high data ingestion rate and provide efficient queries for analyzing the signals from commercial vehicles.


















