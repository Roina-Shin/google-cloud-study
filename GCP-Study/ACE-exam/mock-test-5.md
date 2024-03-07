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



## 3. Deployment Manager

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




## 4. Deployment Manager command lines

- CASE: You are working at a giant e-commerce company. Thousands of users access your website per minute. You have created a deployment using the deployment manager. You have updated the deployment definition file to add a new Compute Engine instance. You need to update the deployment on GCP but you cannot afford downtime for any resources. Which command should you use?


- Solution: 


```
gcloud deployment-manager deployments update --config <deployment-config-path>
```


- The update command will update the existing deployment. The command "gcloud deployment-manager deployments update --config <deployment-config-path>" is used to update an existing deployment using the deployment manager. It does not guarantee zero downtime for resources as it only updates the existing deployment, which may cause disruptions to the resources.


- You cannot create a deployment that already exists. The command "gcloud deployment-manager deployments create --config <deployment-config-path>" is used to create a new deployment using the deployment manager. In this scenario, the deployment definition file has been updated to add a new Compute Engine instance, and using the create command ensures that the updated deployment is created without causing any downtime for resources.



## 5. gcloud iam roles copy

- CASE: Your game development startup is up and has started implementing devops best practices. Your one of game apps has separate projects in GCP for development and production. The development project has appropriate IAM roles defined. You want to have the same IAM roles on the production project. How would you achieve this in the fewest possible steps?


- Solution:

1. Use gcloud iam roles copy.

2. Set the production project as the destination project.


```
gcloud iam roles copy [--dest-organization=DEST_ORGANIZATION] [--dest-project=DEST_PROJECT] [--destination=DESTINATION] [--source=SOURCE] [--source-organization=SOURCE_ORGANIZATION] [--source-project=SOURCE_PROJECT] [GCLOUD_WIDE_FLAG …]
```



## 6. BigQuery Dry Run

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



## 7. Autohealing Health Check

- CASE: You are a cloud engineer on a client-facing app that is hosted on GCP. There are a group of Compute Engine instances that run in multiple zones. You have a requirement to automatically re-create instances in case any of them fail. VMs should be re-created if they are unresponsive after 2 attempts of 8 seconds each. What should you do?


- Solution:

1. Use a managed instance group.

2. Set the Autohealing Health Check to healthy (HTTP).


- An auto-healing health check with a managed instance group is required to perform auto-healing. It suggests using a managed instance group and setting the Autohealing health check to healthy. By setting up an HTTP-based health check with appropriate check intervals and unresponsive thresholds, you can ensure that instances failing the health checks are automatically replaced, meeting the requirement of automatically re-creating instances that become unresponsive after 2 attempts of 8 seconds each. The health check can be configured to send HTTP requests and wait for a valid response within a certain time frame (in this case 2 attempts of 8 seconds each).


- HTTP load balancer can play a crucial role in distributing traffic and ensuring the availability of your application, it does not have the necessary features to automatically re-create instances that become unresponsive after a specific number of attempts and timeframes. For the requirement specified, the use of a managed instance group with autohealing capabilities, as mentioned in Option C, is a more appropriate solution.



## 8. Cloud Billing Account

- CASE: Different teams at your company create projects on GCP and use separate billing accounts and payment cycles. To make payment management easier and more efficient the company wants to centralize all these projects under a single new billing account for all these projects. What should you do?


- Solution: 

1. In the GCP Console, create a new billing account and set up a payment method.


- A new billing account needs to be created with a payment method and all projects need to be linked with the new billing account. It suggests creating a new billing account and setting up a payment method in the GCP Console. This is the recommended method for centralizing all projects under a single billing account. By creating a new billing account, payment management for all projects can be made easier and more efficient.


NOTE:

A Cloud Billing account is set up in Google Cloud and is used to define who pays for a given set of Google Cloud resources and Google Maps Platform APIs. Access control to a Cloud Billing account is established by IAM roles. A Cloud Billing account is connected to a Google payments profile. Your Google payments profile includes a payment instrument to which costs are charged.



## 9. Autoscaling MIG

- CASE: You have developed a note-taking application that you want to run on the Google Cloud Platform. For that, you are planning to create a single binary of the application and run it on GCP. You want to automatically scale the application efficiently and fast based on CPU usage. Your engineering manager has asked you to use virtual machines directly. What should you do?


- Solution:

1. Create a Compute Engine instance template.

2. Use the template in the autoscaling managed instance group.


-  A managed instance group with auto-scaling enabled will scale your app based on CPU usage by default. It suggests creating a Compute Engine instance template and using the template in an autoscaling managed instance group. This approach allows for the efficient and fast scaling of the application based on CPU usage, as requested by the engineering manager. By using an autoscaling managed instance group, the number of virtual machine instances can automatically increase or decrease based on the CPU usage, ensuring efficient scaling of the application.



 ## 10. Deployment Manager Template

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




















