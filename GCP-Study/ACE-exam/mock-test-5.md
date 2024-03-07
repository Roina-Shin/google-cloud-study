### [Source of this study material : GCP Associate Cloud Engineer Practice Test Exam by Sayyam](https://www.udemy.com/course/latest-gcp-ace-google-associate-cloud-engineer-practice-exams-tests)


## Exam -5

### 1. Reserve a static internal IP address

- CASE: You are the founder of a stock trading app. Your app serves millions of traders. Your application communicates with a licensing server (stock exchange server) on the IP 10.194.3.41 several times a day to verify its authenticity. You need to migrate the licensing server to Compute Engine. You cannot change the configuration of the application and want the application to be able to reach the licensing server at the same IP. What should you do?


- Solution: Reserve the IP 10.194.3.41 as a static internal IP address using gcloud and assign it to the licensing server.


- An internal IP needs to be reserved as static as, by default, the IPs are ephemeral(they can change after a VM restart). It suggests reserving the IP 10.194.3.41 as a static internal IP address using gcloud and assigning it to the licensing server. This ensures that the application can still reach the licensing server at the same IP, as desired. By reserving the IP as a static internal address, it guarantees that the IP will not change and the application can establish a consistent connection with the licensing server.



### 2. Export a bill to BigQuery dataset

- CASE: You need to present the cost and estimated budget analysis to your investors. You are planning to estimate the budget for your cloud costs for the next six months. For that, you need to perform an analysis of Google Cloud Platform service costs from multiple separate projects and create a projection estimate of costs by service type, daily and monthly. Your team is comfortable using standard query syntax. What steps should you take?


- Solution:

1. Export your bill to a BigQuery dataset

2. Write time window-based SQL queries for analysis


- You can export billing reports from multiple projects to a single bigquery dataset and then use SQL to perform analysis. Exporting the bill to a BigQuery dataset and writing time window-based SQL queries for analysis is the recommended approach. BigQuery is a fully managed, serverless data warehouse that can handle large amounts of data and provides powerful querying capabilities. By exporting the bill to a BigQuery dataset, you can leverage the standard query syntax that your team is comfortable with to perform the necessary cost analysis. BigQuery also allows for easy collaboration and scalability, making it an ideal solution for analyzing Google Cloud Platform service costs.



### 3. Deployment Manager

- CASE: Your cloud development company has a large number of Compute Engine VMs with different configurations and they have realized that it is difficult to manage them manually. They are looking for a solution to provision VMs on Compute Engine dynamically. The VM specifications will be in a separate configuration file. You want to comply with Google's recommended best practices. Which method would you recommend?


- Solution: Deployment Manager


- The deployment manager is the Infrastructure as a code tool for GCP. Deployment Manager is the recommended method for dynamically provisioning VMs on Compute Engine according to Google's best practices. Deployment Manager allows you to describe and provision all the resources necessary for your application in a declarative format, using YAML or Python templates. It provides a consistent and reproducible way to create and manage your infrastructure. By defining the VM specifications in a configuration file and using Deployment Manager, you can easily create and manage multiple VM instances in an automated and scalable manner.


- **Creating a basic configuration**


```
#  imported templates, if applicable
imports:
  #  path relative to the configuration file
- path: path/to/template.jinja
  name: my-template
- path: path/to/another/template.py
  name: another-template

resources:
  - name: NAME_OF_RESOURCE
    type: TYPE_OF_RESOURCE
    properties:
      property-a: value
      property-b: value
      ...
      property-z: value
  - name: NAME_OF_RESOURCE
    type: TYPE_OF_RESOURCE
    properties:
      property-a: value
      property-b: value
      ...
      property-z: value
```


- **Creating a basic template**


```
resources:
- name: vm-created-by-deployment-manager
  type: compute.v1.instance
  properties:
    zone: us-central1-a
    machineType: zones/us-central1-a/machineTypes/n1-standard-1
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


- After creating a template, import it into your configuration file to use it. To import a template, add an imports section in your configuration, followed by the relative or absolute path from the current directory. For example, you can import your virtual machine template from the previous step by adding the following line to the top of your configuration:


```
imports:
  - path: path/to/my_vm_template.jinja
```


- If you have a long file path, you can provide an optional name property as an alias for the file. You can use this name to reference the template later. If you do not provide the name, the template can be referenced using the path.


```
imports:
  - path: path/to/my_vm_template.jinja
    name: my_renamed_template.jinja
```


- Import it into your configuration and provide the content inline like so:


```
imports:
- path: resource_type.txt

resources:
- name: my-vm
  type: {{ imports["resource_type.txt"] }} # Resolves to "compute.v1.instance"
  properties:
    zone: us-central1-a
    machineType: zones/us-central1-a/machineTypes/f1-micro
    disks:
    - deviceName: boot
      type: PERSISTENT
      boot: true
      autoDelete: true
      initializeParams:
        sourceImage: projects/debian-cloud/global/images/family/debian-9
    networkInterfaces:
    - network: global/networks/default
      accessConfigs:
      - name: External NAT
        type: ONE_TO_ONE_NAT
```


- Once you import a template, use it as a type in your configuration:


```
imports:
- path: vm-template.jinja

resources:
- name: my-vm
  type: vm-template.jinja
```


- Deploy templates directly with command line


```
gcloud deployment-manager deployments create a-single-vm --template vm-template.jinja
```



- Cloud Composer is a workflow automation tool and is not the right use case for infrastructure provisioning. It is a fully managed workflow orchestration service that is built on Apache Airflow. While it can be used to manage complex workflows, it is not specifically designed for provisioning VMs on Compute Engine. Cloud Composer is better suited for managing and coordinating tasks and dependencies across various services and resources in a cloud environment.




### 4. Deployment Manager command lines

- CASE: You are working at a giant e-commerce company. Thousands of users access your website per minute. You have created a deployment using the deployment manager. You have updated the deployment definition file to add a new Compute Engine instance. You need to update the deployment on GCP but you cannot afford downtime for any resources. Which command should you use?


- Solution: 


```
gcloud deployment-manager deployments update --config <deployment-config-path>
```


- The update command will update the existing deployment. The command "gcloud deployment-manager deployments update --config <deployment-config-path>" is used to update an existing deployment using the deployment manager. It does not guarantee zero downtime for resources as it only updates the existing deployment, which may cause disruptions to the resources.


- You cannot create a deployment that already exists. The command "gcloud deployment-manager deployments create --config <deployment-config-path>" is used to create a new deployment using the deployment manager. In this scenario, the deployment definition file has been updated to add a new Compute Engine instance, and using the create command ensures that the updated deployment is created without causing any downtime for resources.



### 5. gcloud iam roles copy

- CASE: Your game development startup is up and has started implementing devops best practices. Your one of game apps has separate projects in GCP for development and production. The development project has appropriate IAM roles defined. You want to have the same IAM roles on the production project. How would you achieve this in the fewest possible steps?


- Solution:

1. Use gcloud iam roles copy.

2. Set the production project as the destination project.


```
gcloud iam roles copy [--dest-organization=DEST_ORGANIZATION] [--dest-project=DEST_PROJECT] [--destination=DESTINATION] [--source=SOURCE] [--source-organization=SOURCE_ORGANIZATION] [--source-project=SOURCE_PROJECT] [GCLOUD_WIDE_FLAG …]
```



### 6. BigQuery Dry Run

- CASE: You have 1000 GB of user analytics data on BigQuery. You need to run a query on the dataset but expect it to return a lot of records. You want to find out the cost of running the query before running it. You are using on-demand pricing. What should you do?


- Solution:

1. Run a dry tun query using the command line to estimate the number of bytes read.

2. Then use the Pricing Calculator to convert that bytes to dollars.


- **If you are using a command line**:


```
bq query \
--use_legacy_sql=false \
--dry_run \
'SELECT
   COUNTRY,
   AIRPORT,
   IATA
 FROM
   `project_id`.dataset.airports
 LIMIT
   1000'
```


- Bigquery charges you based on the amount of data processed by your queries and doing a dry-run gives you an estimate of the number of bytes that will be read and processed if you run your query. Running a dry-run query using the command line allows you to estimate the number of bytes read by the query. This estimation is important because the cost of running a query in BigQuery is based on the amount of data processed (in bytes). By knowing the estimated number of bytes read, you can then use the Pricing Calculator provided by Google Cloud to determine the cost of running the query in dollars.



### 7. Autohealing Health Check

- CASE: You are a cloud engineer on a client-facing app that is hosted on GCP. There are a group of Compute Engine instances that run in multiple zones. You have a requirement to automatically re-create instances in case any of them fail. VMs should be re-created if they are unresponsive after 2 attempts of 8 seconds each. What should you do?


- Solution:

1. Use a managed instance group.

2. Set the Autohealing Health Check to healthy (HTTP).


- An auto-healing health check with a managed instance group is required to perform auto-healing. It suggests using a managed instance group and setting the Autohealing health check to healthy. By setting up an HTTP-based health check with appropriate check intervals and unresponsive thresholds, you can ensure that instances failing the health checks are automatically replaced, meeting the requirement of automatically re-creating instances that become unresponsive after 2 attempts of 8 seconds each. The health check can be configured to send HTTP requests and wait for a valid response within a certain time frame (in this case 2 attempts of 8 seconds each).


- HTTP load balancer can play a crucial role in distributing traffic and ensuring the availability of your application, it does not have the necessary features to automatically re-create instances that become unresponsive after a specific number of attempts and timeframes. For the requirement specified, the use of a managed instance group with autohealing capabilities, as mentioned in Option C, is a more appropriate solution.



### 8. Cloud Billing Account

- CASE: Different teams at your company create projects on GCP and use separate billing accounts and payment cycles. To make payment management easier and more efficient the company wants to centralize all these projects under a single new billing account for all these projects. What should you do?


- Solution: 

1. In the GCP Console, create a new billing account and set up a payment method.


- A new billing account needs to be created with a payment method and all projects need to be linked with the new billing account. It suggests creating a new billing account and setting up a payment method in the GCP Console. This is the recommended method for centralizing all projects under a single billing account. By creating a new billing account, payment management for all projects can be made easier and more efficient.


NOTE:

A Cloud Billing account is set up in Google Cloud and is used to define who pays for a given set of Google Cloud resources and Google Maps Platform APIs. Access control to a Cloud Billing account is established by IAM roles. A Cloud Billing account is connected to a Google payments profile. Your Google payments profile includes a payment instrument to which costs are charged.



### 9. Autoscaling MIG

- CASE: You have developed a note-taking application that you want to run on the Google Cloud Platform. For that, you are planning to create a single binary of the application and run it on GCP. You want to automatically scale the application efficiently and fast based on CPU usage. Your engineering manager has asked you to use virtual machines directly. What should you do?


- Solution:

1. Create a Compute Engine instance template.

2. Use the template in the autoscaling managed instance group.


-  A managed instance group with auto-scaling enabled will scale your app based on CPU usage by default. It suggests creating a Compute Engine instance template and using the template in an autoscaling managed instance group. This approach allows for the efficient and fast scaling of the application based on CPU usage, as requested by the engineering manager. By using an autoscaling managed instance group, the number of virtual machine instances can automatically increase or decrease based on the CPU usage, ensuring efficient scaling of the application.



### 10. Deployment Manager Preview

- CASE: Your team is working on revamping a legacy application on GCP. You are tasked with updating the infrastructure which is managed through complex deployment manager templates. You found that you need to significantly change one of the Deployment Manager templates to accommodate the change and want to confirm that the dependencies of all defined resources are properly met before committing it to the project. You need rapid feedback so that you can deploy quickly. What should you do?


- Solution: Run the Deployment Manager template using the --preview option in the same project, and observe the state of interdependent resources.


-  The deployment manager provides a preview functionality to review the changes in infrastructure before applying updates. It suggests running the Deployment Manager template using the --preview option in the same project and observing the state of interdependent resources. The --preview option allows you to simulate the deployment without making any changes, giving you rapid feedback on the state of the resources and validating the dependencies. This approach allows you to quickly confirm if the infrastructure changes will meet the dependencies of all defined resources before committing the changes.


Deployment Manager does not instantiate any actual resources when you preview a configuration, giving you the opportunity to see the deployment before committing to it.


```
gcloud deployment-manager deployments update example-deployment \
    --config configuration-file.yaml \
    --preview
```


If you do not want to continue, or if you want to use a different configuration file to update the deployment, cancel the current preview.


```
gcloud deployment-manager deployments cancel-preview my-first-deployment
```


If you want to move forward with the configuration:


```
gcloud deployment-manager deployments update my-first-deployment
```


### 11. Managing Service Account keys

- CASE: Your web-development company was founded in the early 2000s and is self-hosted. You are migrating your web application from on-premises servers to GCP. Your application uses My-SQL as its database. You have identified that you can run your application on a Linux VM and connect to the MY-SQL instance on Cloud SQL. Your security team has created a service account with the appropriate access rights. You are asked to use that service account to connect to Cloud SQL instead of the default Compute Engine Service account. What should you do?


- Solution: Specify the service account under the 'Identity and API Access' section by creating the VM via the web console.


- Assigning the service account to the VM will automatically allow applications running on it to use the application-default credentials without the need for any further configurations. It specifies the service account under the 'Identity and API Access' section during the creation of the VM via the web console. By doing this, the VM will have the necessary access rights to connect to Cloud SQL using the specified service account.


### 12. Cloud SQL with the enable binary logging option

- CASE: Your logistics company is looking to cut GCP costs and looking for a cost-effective solution for relational data. Your company’s small set of day-to-day package tracking and operational data is located in one geographic location. One of the requirements is that you need to support point-in-time recovery. What should you do?


- Solution: Use Cloud SQL (MySQL) with the enable binary logging option selected.


- **Binary logging** needs to be enabled before using **point-in-time recovery**. Using Cloud SQL (MySQL) with the enable binary logging option selected allows for point-in-time recovery. Binary logging records changes to the database, allowing you to restore the database to a specific point in time in case of data loss or corruption.


- Failover replicas do not offer point-in-time recovery. Creating failover replicas in Cloud SQL (MySQL) does not provide point-in-time recovery. Failover replicas are used for high availability and automatic failover in case the primary replica becomes unavailable. It does not store historical changes or allow for point-in-time recovery.



### 13. App Engine Scaling Configuration

- CASE: Your website sells educational courses and the tech team in your company is looking to build an application to be deployed on App Engine. Thousands of users access your website every day and the number of instances needs to scale based on the request rate. A minimum of 4 unoccupied instances should be live at all times. As an engineering manager in your firm which scaling configuration should you recommend?


- Solution: Use Automatic Scaling and set min_idle_instances to 4.


- Automatic scaling creates instances based on request rate, response latencies, and other application metrics. You can specify thresholds for each of these metrics, as well as a minimum number of instances to keep running at all times. Using automatic scaling with min_idle_instances set to 4 allows for automatic scaling based on the request rate. It ensures that there are always at least 4 instances running, even during periods of low traffic. Additionally, as the request rate increases, additional instances will be automatically created to handle the load, ensuring optimal performance and scalability.



### 14. Use multiple gcloud configurations

- CASE: You have taken the responsibility of deploying every new iteration of your app to Development and Test environments in GCP. Both environments are located in separate GCP projects in different regions and zones. How can you deploy a Compute Engine instance to both environments through the command line interface?


- Solution: 

1. Create two configurations in gcloud, one for development and other for test environment.

2. Run gcloud config configurations activate [NAME] to switch between configurations and use gcloud commands to deploy Compute Engine instances.


- gcloud config configurations activate [NAME] is the correct way to switch between two gcloud configurations. It suggests creating two configurations in gcloud, one for the development environment and one for the test environment. By using the command "gcloud config configurations activate [NAME]", we can easily switch between the two configurations and use the gcloud commands to deploy Compute Engine instances to the respective environments.


All the gcloud configs are present in  ~/.config/gcloud/configurations folder.

The configs present in the configurations folder would look like the following.


1. cd in to the config directory.


```
~/.config/gcloud/configurations
```


2. Create a new configuration file with config_ prefix


```
vi config_demo-account
```


3. Enter the required parameters in the config file and save it. An example is shown below. You should change the values according to your google cloud account, project, zone and region.


```
[core]
account = accounts@devopscube.com
project = devopscube

[compute]
zone = asia-east1-b	
region = asia-east1
```


4. For using any new configuration, you need to activate it. Use the following command to activate the configuration you created. You just need to specify the suffix of the configuration name as shown below.


```
gcloud config configurations activate demo-account
```


5. Once activated, login to the google cloud account using the following command.


```
gcloud auth login
```


6. Once logged in, you will be able to make all the gcloud api calls for the new configuration.



### 15. The largest possible IP range

- CASE: You are an intern at a cloud-based tech company. You are working with your manager on a large-scale GCP project that requires you to create a custom VPC with a single subnet that should have the largest possible range. Which is the best possible range in this scenario?


- Solution: 10.0.0.0/8


- This option represents a range of IP addresses starting from 10.0.0.0 and having a subnet mask of /8. The /8 subnet mask allows for 16,777,214 usable IP addresses (2^24 - 2), which is the maximum possible number of IP addresses in a subnet with an 8-bit network prefix. This makes it the best option for creating a subnet with the largest possible range. It represents a subnet range of 10.0.0.0 with a subnet mask of /8. This means that the subnet range will include all IP addresses from 10.0.0.0 to 10.255.255.255, which is a very large range but not the largest possible range.


- If we want to set the subnet to custom, the minimum size is /8. (Hence, Option-B is correct)



The private network range is defined by IETF and needs to be adhered to by all cloud providers.

[Ref: https://tools.ietf.org/html/rfc1918]



The supported internal IP Address ranges are:

1. 24-bit block 10.0.0.0/8 (16777216 IP Addresses)

2. 20-bit block 172.16.0.0/12 (1048576 IP Addresses)

3. 16-bit block 192.168.0.0/16 (65536 IP Addresses)



### 16. Deploying the application in GKE

- CASE: You are working as an intern at a tech company. Your manager has assigned you a task to dockerize their application and later deploy it on the Kubernetes Engine. What approach should you take?


- Solution:

1. Build a docker image from the Dockerfile and upload it to Container Registry.

2. Create a Deployment YAML file to point to the newly uploaded image.

3. Use the kubectl command line utility to create the deployment with that file.


- You need to push the docker image to the Google container registry first and then use the kubectl tool to create a deployment. GKE cannot deploy a local Docker image. It follows the correct approach for dockerizing and deploying the application on Kubernetes Engine. It suggests building a docker image from the Dockerfile, uploading it to Container Registry, and creating a Deployment YAML file to point to the uploaded image. The `kubectl` command is then used to create the deployment using the YAML file.



### 17. Cloud Storage Object Life Cycle

- CASE: You are storing CCTV video footage on Cloud Storage. In order to save costs, you need to move videos stored in a specific Cloud Storage Regional bucket to Coldline after 90 days, and then delete them after one year from their creation. How should you set up the policy?


- Solution:

1. Enable Cloud Storage Lifecycle Management and set Age conditions with SetStorageClass and Delete actions.

2. Set the SetStorageClass action to 90 days and the Delete action to 365 days.



- Lifecycle management is used to change storage class or delete objects after specified days from creation. It enables Cloud Storage Object Lifecycle Management and sets the SetStorageClass action to 90 days, which moves the videos to Coldline storage after 90 days. It also sets the Delete action to 365 days, which deletes the videos after one year from their creation, as required.


NOTE:
Object Lifecycle Management example use cases:

Downgrade the storage class of objects older than 365 days to Coldline storage.

Delete objects created before January 1, 2019.

Keep only the 3 most recent versions of each object in a bucket with versioning enabled.



### 18. Cloud Monitoring

- CASE: There are multiple apps running in your Google Cloud Platform organization-level in separate projects. You want to monitor the health of all these apps under the same Stackdriver Monitoring dashboard. How can you do it?


- Solution: Create a single Stackdriver account (now termed 'Google Workspace') and link all projects to the same account.


- You can monitor multiple GCP projects from a single stackdriver account (now called workspace). Creating a single Stackdriver account and linking all projects to the same account allows you to monitor the health of all apps under the same Stackdriver Monitoring dashboard. By linking projects to the same Stackdriver account, you can view and analyze metrics, logs, and other monitoring data from all projects in a centralized manner. This simplifies the monitoring process and provides a unified view of the health of all apps.


**Google Cloud Skill Boost Demo**


1. Create a Cloud Monitoring account that has two Google Cloud projects.
2. Monitor across both projects from the single Cloud Monitoring account.


**Create a Monitoring Metrics Scope**
Set up a Monitoring Metrics Scope that's tied to your Google Cloud Project. The following steps create a new account that has a free trial of Monitoring.

In the Cloud Console, click Navigation menu (Navigation menu icon) > Monitoring.
When the Monitoring Overview page opens, your metrics scope project is ready.

Now add both projects to Monitoring.

In the left panel, click Settings and then in the Settings window, click +Add GCP PROJECTS in the GCP Projects section.

Click Select Projects.

Check Project ID 1 and click Select.

Click Add projects.


**About Cloud Monitoring groups**
Cloud Monitoring lets you define and monitor groups of resources, such as VM instances, databases, and load balancers. Groups can be based on names, tags, regions, applications, and other criteria. You can also create subgroups, up to six levels deep, within groups.

Create a Cloud Monitoring group
In the left menu, click Groups, then click +Create group.

Name your group DemoGroup.


**Uptime check for your group**
Uptime checks let you quickly verify the health of any web page, instance, or group of resources. Each configured check is regularly contacted from a variety of locations around the world. Uptime checks can be used as conditions in alerting policy definitions.

In the left menu, click Uptime checks, then click +Create uptime check.

Create your uptime check with the following information:

Protocol: TCP

Resource Type: Instance

Applies To: Group, and then select DemoGroup.

Port: 22

Check frequency: 1 minute, then click Continue.

Click Continue again.

Leave the slider ON state for Create an alert option in Alert & notification section, then click Continue.

For Title: enter DemoGroup uptime check.

Click TEST to verify that your uptime check can connect to the resource.

When you see a green check mark everything can connect, click Create.



### 19. GKE kubectl config

- CASE: You are managing multiple GCP projects and you have created separate configurations for gcloud in your CLI for each project. You have an inactive configuration with a configured Kubernetes Engine cluster and you want to review this Kubernetes configuration using the fewest possible steps. What should you do?


- Solution: Run kubectl config use-context and kubectl config view to review the output.


- Running the kubectl config view after setting the appropriate context will return the correct output. The 'kubectl config use-context' command is used to switch to a specific Kubernetes context, and the 'kubectl config view' command is used to display detailed information about the current Kubernetes configuration. By using these two commands, you can switch to the inactive configuration with the configured Kubernetes Engine cluster and review its Kubernetes configuration.


- The 'kubectl config get-contexts' command only lists the available Kubernetes contexts, which are different from the configurations. This command does not provide details about the Kubernetes configuration itself.



### 19. Connecting to Windows machine

- CASE: You are the head of the backend and database management team in your company. Your DB team does weekly maintenance on your company’s customers and operational data. DB team has upgraded one of the SQL servers on a Windows Compute engine instance to the latest version and asked you to test with the new version so they can roll out the upgrade to all servers. In order to do some debugging, you want to connect to this instance. How can you do it in the fewest number of steps?


- Solution:

1. Install an RDP client on your desktop.

2. Set a Windows username and password in the GCP console.

3. Use the credentials to log in to the instance.


- An RDP client allows you to establish a remote desktop connection with the Windows-based Compute Engine instance. With the RDP client installed and the Windows credentials set, you can launch the RDP client and enter the IP address or hostname of the Windows Compute Engine instance. Supply the Windows username and password you set in the GCP Console to authenticate and establish a remote desktop connection to the instance. This option is the most straightforward and efficient way to connect to the upgraded SQL Server instance on the Windows Compute Engine.



### 20. Auditor Roles

- CASE: Your app deals with the financial data of your customers and it needs to be audited by external auditors. You need to configure IAM access audit logging in BigQuery to facilitate the audit. How can you do it following Google recommended practices?


- Solution: Add the auditors group to the 'logging.viewer' and 'bigQuery.dataViewer' predefined IAM roles.


-  It is considered best practice to group people requiring similar permissions to a Google group and assigning roles to the group instead of individual users. For logging and bigquery access, the logging.viewer and bigQuery.dataViewer roles need to be assigned. It follows the recommended practice of granting the auditors group the 'logging.viewer' and 'bigQuery.dataViewer' predefined IAM roles. These roles provide the necessary access to view both the logging and BigQuery data, allowing the auditors to perform their auditing tasks.



### 21. Audit logs

- CASE: Some of your highly sensitive banking-management application data is stored on Cloud Storage. As per the recommendation from your security team, you enabled data access logging on the buckets. As a security drill, you want to verify activities for a particular user for these buckets, using the fewest possible steps. You are interested in activities that involve the addition of metadata labels and files that have been viewed from those buckets. How will you achieve this?


- Solution: View the information in the Audit log in the GCP console.


- Audit logs are more suitable for verifying the addition of metadata labels. Viewing the information in the Audit log in the GCP console allows you to easily see all the activities related to the buckets, including addition of metadata labels and file views. The Audit log provides detailed information about actions taken by users within your Cloud Storage buckets.


- When you enable data access logging for a bucket, GCP generates logs for read, write, and metadata changes for objects in the bucket. These logs are saved in the Audit log in Stackdriver.


To filter the Audit log, you can follow these steps:

Go to the GCP Console and navigate to the Stackdriver Logging section.

Click on "Logs" in the left-hand menu.

Select "Cloud Storage" as the Resource Type.

In the filter section, enter the search criteria for the user whose activities you want to view. You can search by user email or user ID.

Add a filter to view the metadata labels that have been added or to view file access events.

Select the time range for which you want to view the logs.

Click on the "Submit" button to apply the filter.


Once you apply the filter, the Audit log will display all the access and activity events made by the specified user within the selected time range.



### 22. IAM Roles

- CASE: You have newly joined the Operations and Access Governance team at a large organization. One of the teams has requested access to manage buckets and files in Cloud Storage in one of the GCP projects that you manage. Which IAM roles should you grant your colleagues?


- Solution: Storage Admin


- The Storage Admin role provides the minimum permission required to create and manage Cloud Storage buckets. The Storage Admin IAM role provides the necessary permissions to manage buckets and files in Cloud Storage. This role allows your colleagues to create, delete, modify, and administer buckets and objects within the project. It provides granular control over the Cloud Storage resources without granting excessive permissions beyond the intended scope.



### 23. Load Balancing options

- CASE: Your PDF merging application is running on Managed Instance group. You want to have a single public IP over HTTPs that load balances your application. The load balancer must terminate the client SSL session once merging is completed. What is the Google Recommended approach for such a requirement?


- Configure an HTTP(S) load balancer.


- The application serves over HTTP and the HTTP(s) load balancer supports SSL. An HTTP(S) load balancer is a global load balancer that supports both HTTP and HTTPS traffic. It can handle SSL termination, meaning it can decrypt the SSL session from the client and forward the unencrypted traffic to the backend instances. This is important because the question mentions that the load balancer must terminate the client SSL session once merging is completed.

- By using an HTTP(S) load balancer, you can have a single public IP address that load balances your application, ensuring high availability and scalability. Additionally, it allows SSL termination at the load balancer level, which offloads the SSL encryption/decryption process from your backend instances, improving overall performance.



- An internal TCP load balancer is used for distributing TCP traffic within a virtual private cloud (VPC). It does not support SSL termination or HTTP(S) traffic. Since the requirement specifies that SSL termination is necessary for the application, this option is incorrect.

- SSL Proxy Load Balancing is intended for non-HTTP(S) traffic. An external SSL proxy load balancer is designed for handling SSL traffic and terminating SSL at the load balancer level. However, it does not support HTTP(S) traffic, which means it cannot handle HTTP requests or load balance an HTTP-based application. As the question mentions that the application is an HTTP-based PDF merging application, this option is incorrect.

- A TCP proxy load balancer can distribute TCP traffic to backend instances, but it does not support SSL termination or HTTP(S) traffic. Since the requirement specifies that the load balancer must terminate the client SSL session, this option does not meet the requirements and is incorrect.



### 24. Signed URLs

- CASE: You work at a large product-based tech company. One of your joint business partners from the external company has requested access to a sensitive file on your Cloud Storage. Your partner does not use Google accounts. Given the sensitivity of the data, access to the content needs to be removed after five hours. You want to follow Google-recommended practices. What should you do? 


- Solution: Create a signed URL with a five-hour expiration and share the URL with the company.


- A signed URL is a URL that provides limited permission and time to make a request. Signed URLs contain authentication information in their query string, allowing users without credentials to perform specific actions on a resource. When you generate a signed URL, you specify a user or service account which must have sufficient permission to make the request that the signed URL will make. After you generate a signed URL, anyone who possesses it can use the signed URL to perform specified actions, such as reading an object, within a specified period of time. It involves creating a signed URL with a four-hour expiration. This means that the partner would be able to access the sensitive file by using the URL but the access would automatically be revoked after four hours. This follows Google-recommended practices for sharing sensitive data securely.



### 25. DaemonSet

- CASE: Multiple teams in your company deploy their apps on a single GKE auto-scaling cluster. You want to centralize monitoring by running a monitoring pod that sends container metrics to a third-party monitoring solution. Which is the simplest way to do it?


- Solution: Deploy the monitoring pod in a DaemonSet object.


-  A daemonSet gets deployed to every node in the cluster. Deploying the monitoring pod in a DaemonSet object is the simplest way to centralize monitoring in this scenario. A DaemonSet ensures that a copy of the monitoring pod is running on each node of the GKE cluster. This allows the monitoring pod to collect container metrics from all the pods running on the cluster.


```

apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: counter-app
spec:  
  selector:
    matchLabels:
      app: counter
  template:
    metadata:
      name: counter-app
      labels:
        app: counter
    spec:
      tolerations: 
      - effect: NoSchedule
        operator: Exists
      containers:
      - name: counter
        image: "kahootali/counter:1.1"
        volumeMounts:
        - name: counter
          mountPath: /app/
      volumes:
      - name: counter
        persistentVolumeClaim:
          claimName: counter
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: counter
spec:
  accessModes:
  - ReadWriteMany
  resources:
    requests:
      storage: 50Mi
  storageClassName: efs
```


- When you deploy the daemonset, it will create pods equal to the number of nodes. In terms of behavior, it will behave the same as Deployments i.e. all pods will share the same Persistent Volume.



### 26. Managed Instance Group

- CASE: Your apparel-selling app is just launched. Your app uses a Managed Instance group. Since very little traffic is expected, for a while, only a single instance of the VM should be active in every GCP project. How should you configure the instance group?


- Solution:

1. Set autoscaling to On

2. Set the minimum number of instances to 1

3. Set the maximum number of instances to 1


- Setting the minimum and maximum instance config to 1 will always keep only 1 VM active in the managed instance group. We want the application running at all times. If the VM crashes due to any underlying hardware failure, we want another instance to be added so we need autoscaling to be ON. It sets autoscaling to On, ensuring that the instance group can dynamically adjust the number of instances based on incoming traffic. By setting the minimum number of instances to 1 and the maximum number of instances to 1, it guarantees that only a single instance will be active in the project.



### 27. VPC

- CASE: You are tasked with building the VPC config for a new logistics app. The app will have a production and a test environment on Compute Engine. Both environments need to have their own separate individual subnets. Network connectivity is required between all VMs over internal IPs, without the need to create additional routes. Which configuration should you select?


- Solution: Create a single custom VPC with 2 subnets such that each subnet resides in a different region and has a different CIDR range. 


- The requirements specify that both production and test VMs must be in the same VPC but different subnets. It allows for the creation of a single custom VPC with 2 subnets that each reside in a different region and have a different CIDR range. This configuration meets the requirement for separate individual subnets for the production and test environments. Additionally, by having a single VPC, network connectivity between all VMs over internal IPs is automatically enabled.


- You cannot create 2 subnets with the same CIDR range. Having both subnets in the same region and with the same CIDR range does not meet the requirement for separate individual subnets for the production and test environments.



### 28. Understanding Roles

- CASE: You are facilitating a security audit and the auditors have asked for a list of all IAM users and roles assigned within a GCP project named my-project. What should you do?


- Solution: Navigate to the project and then to the IAM section in the GCP console. Review the members and roles.


- IAM section displays all users and their roles in the project. Navigating to the project and then to the IAM section in the GCP Console will allow you to view the members and roles assigned within the project. IAM (Identity and Access Management) is a GCP service that controls access to resources and allows you to manage permissions for individuals and groups of users.



### 29. Link a billing account to a project

- CASE: You work at a large search engine company. Your finance team has asked you to create a new Billing account specifically for your project to track expenses. You need to link it with your GCP project. What steps should you take?


- Solution:

1. Make sure you have the Project Billing Manager IAM role in the GCP project.

2. Create a new billing account and link it to the existing project.


- It meets the requirement of creating a new billing account specifically for your project to track expenses. It states that you should make sure you have the Project Billing Manager IAM role in the GCP project, which gives you the necessary permissions to manage billing. Then, you can create a new billing account and link it to the existing project.



### 30. Managing Traffic on App Engine

- CASE: You developed a website to sell used smartphones and deployed it on App Engine. You found that the user interface is breaking for some users in the latest release. Prior versions of the application did not have this issue. You want to immediately revert to an older version to mitigate the issue. What should you do?


- Solution: Open the GCP console and go the the App Engine Versions page, route 100% traffic to the previous version.


- Routing all the traffic back to a previous version is the fastest way to roll back a change on App Engine. In the GCP Console, going to the App Engine Versions page allows you to view and manage different versions of your deployed application. By routing 100% of the traffic to the previous version, you effectively revert to that version and mitigate the issue with the user interface breaking.


Note:
Traffic migration switches the request routing between the versions within a service of your application, moving traffic from one or more versions to a single new version. Traffic is migrated immediately between your versions in the flexible environment. Unlike versions in the standard environment, gradual traffic migration is not supported in the flexible environment.


To migrate traffic immediately:


```
gcloud app services set-traffic [MY_SERVICE] --splits [MY_VERSION]=1
```


Split traffic across multiple versions:


```
gcloud app services set-traffic [MY_SERVICE] --splits [MY_VERSION1]=[VERSION1_WEIGHT],[MY_VERSION2]=[VERSION2_WEIGHT] --split-by [IP_OR_COOKIE]
```


### 31. Compute OS Login

- CASE: You work in a large airline company as a cloud engineer. Your company’s operational and flight schedule data is hosted on GCP. There are a large number of instances deployed on Compute Engine, which are managed by an operations team. The operations team does maintenance work on flight schedule data and they require administrative access to these servers. Your security team needs to ensure credentials are optimally distributed to the operations team and they must be able to audit who accessed a given instance. What approach should you take?


- Solution:

1. Let each member of the team generate a new SSH key pair and add the public key to their Google account.

2. Grant the compute.osAdminLoginrole to the Google group corresponding to this team.


- The OS login grants SSH access to VMs using the GCP IAM policy and does not require the distribution of SSH keys to users. It leverages the native identity and access management features of the Google Cloud Platform (GCP). Each member of the team can generate a new SSH key pair and add the public key to their Google account. The compute.osAdminLogin role can then be granted to the Google group corresponding to the team. This approach provides centralized management of credentials and allows for auditability of access to the instances.


-  Letting each member of the team generate a new SSH key pair and sending their public keys to the cloud engineer. This approach does not provide a centralized way to manage and audit access to the instances. It also adds an extra step of manually deploying the keys on each instance using a configuration management tool.



### 32. Cloud Spanner IAM roles

- CASE: Your company’s image tagging app is hosted on GCP. A new team at your Organization has requested view and edit access to one of the existing Cloud Spanner instances. What is the best practice to grant such access?


- Solution: 

1. Run gcloud iam roles describe roles/spanner.databaseUser

2. Add the users to a new group

3. Add the group to the role


- GCP recommends adding users requiring the same permissions to a Google group and assign IAM permissions to the group instead of individual users. It uses the 'spanner.databaseUser' role but adds the users to a new group. By adding the group to the role, it ensures that any users added to the group will have the view and edit access to the Cloud Spanner instance.



### 33. Node Auto-Upgrade feature

- CASE: Kubernetes regularly releases patches and fixes to vulnerabilities in its latest versions. You want to keep your GKE cluster updated to take advantage of the latest fixes. What should you do?


- Solution: Use the Node Auto-Upgrades feature for your GKE cluster.


- Node auto-upgrades help you keep the nodes in your cluster up-to-date with the cluster control plane (master) version when your control plane is updated on your behalf. The Node Auto-Upgrades feature in GKE automatically upgrades the nodes in a cluster to the latest stable version of Kubernetes. This ensures that the cluster is kept up to date with the latest fixes and vulnerability patches, allowing you to take advantage of the latest features and improvements. It simplifies the process of keeping your GKE cluster updated.


- The Node Auto-Upgrades feature is specifically designed for keeping the cluster updated with the latest fixes in Kubernetes.


- The Node Auto-Repair feature in GKE is responsible for identifying and repairing issues with individual nodes in the cluster, such as terminating unresponsive nodes or replacing them if they fail health checks. It does not specifically handle updating the Kubernetes version or applying patches.



### 34. Parallel Composite Uploads

- CASE: You work at a food-delivery startup that has generated a large amount of data in the last month. You are backing up application data of one of your servers to a Nearline Cloud Storage Bucket. The total backup file is 35 GB. You have provisioned a dedicated 1 Gbps WAN connection for this purpose. You want to use the bandwidth of 1 Gbps as efficiently as possible to transfer the file rapidly. How should you upload the file?


- Solution: Enable parallel composite uploads using gsutil on the file transfer.


- Parallel composite uploads will upload different parts of your file in parallel chunks. Enabling parallel composite uploads using gsutil allows the file to be split into smaller parts and uploaded in parallel. This utilizes the available bandwidth more effectively and can result in faster file transfers.


- Upload an object to a bucket:


```
gcloud storage cp OBJECT_LOCATION gs://DESTINATION_BUCKET_NAME
```

OBJECT_LOCATION is the local path to your object. For example, Desktop/dog.png.


- Use parallel composite uploads:


```
gcloud storage cp OBJECT_LOCATION gs://DESTINATION_BUCKET_NAME storage/parallel_composite_upload_enabled
```


### 34. Kubernetes secret

- CASE: One of your teammates has deployed a microservice called myapp1 to your Kubernetes cluster using the YAML specification. A part of YAML specifications is shown below:

apiVersion: apps/v1
"
"
"
"
"
spec:
     containers:
     - name: main-container
        image: noonclub.io/company-repo/myapp1:1.7
        env:
        - name: DB_PASSWORD
           value: "tough0password1"
        ports:
        - containerPort: 8080



While reviewing the above configuration, you have found that the database password is stored in the YAML file as plain text. You want to suggest some security best practices to your teammate. What should you suggest?



- Solution:

1. The database password should be stored inside a Secret object.


2. Modify the YAML file to populate the DB_PASSWORD environment variable from the Secret.


- Secret YAML

```
apiVersion: v1
kind: Secret
metadata:
  name: dotfile-secret
data:
  .secret-file: dmFsdWUtMg0KDQo=
---
apiVersion: v1
kind: Pod
metadata:
  name: secret-dotfiles-pod
spec:
  volumes:
    - name: secret-volume
      secret:
        secretName: dotfile-secret
  containers:
    - name: dotfile-test-container
      image: registry.k8s.io/busybox
      command:
        - ls
        - "-l"
        - "/etc/secret-volume"
      volumeMounts:
        - name: secret-volume
          readOnly: true
          mountPath: "/etc/secret-volume"
```


- Storing sensitive information like passwords in Kubernetes secrets is the recommended way.


### 35. Cross Project Management Using service accounts

- CASE: Your Security team manages all service accounts in a project called sec-sa. You need to take snapshots of VMs running in another project called proj-vm. Your security team has asked you to use a specific service account from their project for this purpose. What should you do?


- Solution: In the project called proj-vm, grant the service account the IAM role of Compute Storage Admin.


- Compute Storage Admin role needs to be assigned to the service account in the target project in order for it to take snapshots of VMs in that project. Granting the service account the IAM Role of Compute Storage Admin in the proj-vm project provides it with the necessary permissions to take snapshots of the VMs in that project. By granting the specific role, the service account is only given the necessary access required for the task, minimizing the risk of unauthorized access.



### 36. Cloud Storage Object Content Type

- CASE: You work at a graphics design studio that serves multiple clients. You have created a static website on Cloud Storage to showcase your freelance services. Your website also includes your work portfolio in PDF files that users can download by clicking on its links. Instead of prompting the user to download the PDFs, you want the clicked PDF files to be displayed within the browser window directly. How can you achieve this?


- Set Content-Type metadata to application/pdf on the PDF file objects.


- Setting the content type to application/pdf will allow the browser to open the PDF file directly in the browser instead of prompting to save. Setting the Content-Type metadata to application/pdf on the PDF file objects informs the browser that the file being served is a PDF file. This allows the browser to display the PDF file directly within the browser window instead of downloading it. By setting the correct Content-Type metadata, the PDF files will be displayed as intended.



### 37. MIG health check

- CASE: You are working as a GCP engineer at a legal cricket betting application where customers use historical data points and statistics to place their bets. Millions of users place bets daily on an ongoing T20 Worldcup match series. Your application is hosted on an auto-scaling managed instance group. New instances are added to the group if CPU utilization exceeds 85%. The maximum number of VMs in the group can be 6 VMs. The health check on the group is configured to become active after an initial delay of 30 seconds. Recently, you have noticed that when the managed instance group auto-scales, it creates more instances than required to support end-user traffic. One of your developers has made some changes to the application startup script and that has caused the app to take 3 minutes to initialize and become ready to serve traffic. The initial delay of HTTP healthchecks is set to 30 seconds. You suspect that there is over-provisioning of VMs and unnecessary use of resources. You want to make sure there is no overprovisioning of resources. How can you do it?


- Solution: Increase the initial delay of the HTTP health check to 200 seconds.


- In this case, GCP is creating more instances than required because the initial health check fails as the newly created instance takes 180 seconds to get ready to serve traffic but the health check delay is kept at 30 seconds. So, increasing the initial delay to a value of more than 180 seconds solves our problem. Increasing the initial delay of the HTTP health check to 200 seconds would help prevent overprovisioning. By increasing the delay, the health check will only start after a longer period of time, allowing more time for the instances to initialize and become ready to handle the traffic. This ensures that instances are not created before they are actually able to serve traffic, reducing overprovisioning of resources.



### 38. Batch Job run on Preemptible VMs

- CASE: You are building an application to detect malicious financial transactions. Every night at 2 AM, you fetch the records of all financial transactions done during the previous day from the database and run a batch job to analyze all the transactions. The batch jobs take around 2 hours to complete. You want to minimize service costs. What approach should you take?


- Solution: Run the batch job on preemptible Compute Engine VMs with standard machine type.


- Preemptible VMs are the most cost-effective for this task as the batch jobs run only for a small period of time at regular intervals. Using preemptible VMs can provide up to an 80% discount compared to normal instances of the same specifications. It suggests running the batch job on preemptible Compute Engine VMs with standard machine types. Preemptible VMs are instances that can be terminated by Google at any time, but they come at a significantly lower cost compared to regular instances. Since the batch job runs overnight and can tolerate interruptions, using preemptible VMs can help minimize costs while still achieving the desired analysis. Standard machine types provide a balance of CPU and memory resources suitable for batch-processing tasks.



### 39. gcloud config while deploying an app

- CASE: You are a freelancer working on multiple GCP projects at the same time. You deployed an App Engine application using gcloud app deploy, but the deployment is not showing in the intended project. You suspect it got deployed in a different project. You want to find out why this happened and where the application is deployed. How can you debug this?


- Solution: Review the Google Cloud configuration used for deployment by going to the cloud shell and run gcloud config list.


- If you do not specify the --project flag while deploying, gcloud will deploy the app in the project configured in the gcloud config, which can be viewed by running the gcloud config list command. Reviewing the Google Cloud configuration used for deployment by running the "gcloud config list" in the cloud shell would provide information on the current project and other configuration settings. Running this command would display the active configuration, which includes the project ID you are currently targeting. By checking the output of this command, you can determine if the application was deployed to the intended project or a different one.


```
yejinshin@cloudshell:~ (devops-project-yj)$ gcloud config list

[accessibility]
screen_reader = True
[component_manager]
disable_update_check = True
[compute]
gce_metadata_read_timeout_sec = 30
[core]
account = yejinshin@example.com
disable_usage_reporting = True
project = devops-project-yj
[metrics]
environment = devshell
```


### 40. Setting Instance Scheduling options

- CASE: You are developing a mission-critical application for the stock market on Compute Engine. You have a set of 10 Compute Engine instances and you need to configure them for availability. These instances should attempt to automatically restart if they crash. And you cannot afford to lose the instances during system maintenance activity. What should you do?


- Solution:

1. Create an instance template for the instances

2. Set the 'Automatic Restart' to on

3. Set the 'On-host maintenance' to Migrate VM instance

4. Add the instance template to an instance group


- Automatic restart will restart the instance if it crashes and setting on host maintenance to migrate the instance will not let the application go down during maintenance. It fulfills the requirements of automatically restarting the instances if they crash and ensuring that they are not lost during system maintenance activity. By setting the 'Automatic Restart' to on, the instances will attempt to automatically restart if they crash. By setting the 'On-host maintenance' to Migrate VM instance, the instances will be migrated to another host during system maintenance, preventing any downtime.



### 41. Changing machine type of stopped instance

- CASE: Traffic on your blogging website has suddenly increased after a relatively popular technology magazine wrote about you. Your website is hosted on a Compute engine instance configured with 2 vCPUs and 4 GB of memory. The increase in traffic is causing the virtual machine to run out of memory. You want to upgrade the virtual machine to have 8 GB of memory. What is the recommended way to do it?


- Solution:

1. Stop the VM

2. Increase the memory to 8 GB

3. Start the VM


- You need to stop the VM to modify the RAM. Stopping the VM, increasing the memory to 8 GB, and starting the VM will directly increase the memory capacity of the virtual machine as per the requirement. By stopping the VM, any running processes are temporarily paused, allowing for the modification of the memory allocation. Once the memory is increased and the VM is started again, it will have an upgraded memory capacity of 8 GB.










 


 
































































