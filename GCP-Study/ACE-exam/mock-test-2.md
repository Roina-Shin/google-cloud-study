### [Source of this study material : GCP Associate Cloud Engineer Practice Test Exam by Sayyam](https://www.udemy.com/course/latest-gcp-ace-google-associate-cloud-engineer-practice-exams-tests)


## Exam -2

### 0. Send transactions to Pub/Sub and use MIG to process them

- CASE: Your game generates millions of events every minute. All these events need to be processed as transactions The amount of computation required to process the transactions is way more than the processing capabilities of a single VM. How can you spread these transactions across multiple VMs in real-time in a cost-effective manner?


- Solution: 

1. Send all the transatcions to Pub/Sub.

2. Use a managed instance group to process them in VMs. 


- Pub/Sub can effectively distribute a large number of tasks among multiple servers at a low cost. Sending all transactions to Pub/Sub and using a managed instance group to process them in VMs is a scalable and cost-effective solution. Pub/Sub allows for real-time data streaming and the managed instance group ensures that the transactions are spread across multiple VMs to handle the high volume of events.


### 1. Backend service and frontend service in GKE

- CASE: The app has a backend service and frontend service, both deployed as Kubernetes deployments. How can you make sure that the communication between the frontend service and backend service is not affected if pods are moved or restarted?


- Solution: 

1. Create a service that groups your pods in the backend service.

2. Configure the frontend pods to communicate through that service.


- The Kubernetes service serves the purpose of providing a destination that can be used when the pods are moved or restarted. Creating a service in Kubernetes allows for reliable communication between the frontend and backend services even if pods are moved or restarted. By grouping the backend pods under a service, the frontend pods can communicate with the service, which automatically routes the traffic to the available backend pods. This ensures that the communication is not affected by pod movements or restarts.



### 2. Use Object Lifecycle management policies

- CASE: You need to follow certain regulations according to your organization's policy.

1. All data older than one year must be archived.

2. Data older than 5 years must be deleted.

3. All other data must be stored on Standard storage.


- Solution: Create **Object Lifecycle** management policies.


- Object Lifecycle allows you to automate the implementation of your organization's data policy. Creating Object Lifecycle management policies in Cloud Storage allows for a simple and automated way to implement the given guidelines. By creating lifecycle rules, data can be automatically transitioned to the appropriate storage class (such as ARCHIVE) based on its age. Additionally, data can be automatically deleted after a specified duration. This approach ensures compliance with organization's policy without the need for manual intervention or scripts.



### 3. Static external IP address and Cloud DNS

- CASE: You have built a service that is used by many partners. You want to make sure that the IP does not need to be changed in your DNS if the server crashes or if it is replaced. How to deliver this solution with minimal cost and avoid downtime?


- Solution: Reserve a static external IP address, and assign it using Cloud DNS.


- External IPs are routable and can be advertised and seen on the Internet, and this is also the most cost-effective solution. Reserving a static external IP addresses ensures that the IP does not need to be changed in the DNS even if the server crashes or is replaced. This way, the service can be accesses consistently without any downtime.


### 4. Attaching labels to resources

- CASE: Your management has asked you to investigate resources consumption charges and present a summary of your findings for your GCP environment.


- Solution: 

1. Attach labels to resources to reflect the owner and purpose.

2. Export Cloud Billing data into BigQuery and create a Data Studio dashboard for analysis.


- It describes Google recommended practice. Attaching labels to resources is a best practice in GCP to track metadata such as owner, purpose, or any other custom information. By attaching appropriate labels to resources, you can efficiently categorize and organize resources based on their ownership and purpose. Exporting Cloud Billing data into BigQuery allows you to centralize billing data and perform complex queries to analyze resource consumption charges effectively. Creating a Data Studio dashboard on top of BigQuery data provides an intuitive and visual representation of resource consumption, enabling your management to quickly grasp and understand the findings.


![billing-dataset-labels](/GCP_pictures/ACE-exam/mock-test-2/billing-dataset-labels.PNG "Billing dataset labels")



### 5. Autopilot cluter in GKE

- CASE: You want to migrate on-premises deployments ot GKE while keeping costs under control. What is the best way to do that?


- Solution: Configure Autopilot in GKE to monitor node utilization and eliminate idle nodes.


- Autopilot is designed to reduce the operational cost of managing clusters and optimize your clusters for production. Configuring autopilot in GKE allows for automated monitoring of node utilization and the elimination of idle nodes. This ensures efficient resource allocation and helps keep costs under control by dynamically adjusting the number of nodes based on workload demands.



### 6. Transfer Appliance

- CASE: You are migrating 100 TB of data from your on-premise data center to GCP. Your current bandwidth is limited to 100 Mbps. What is the most efficient and cost effective way to perform this migration?


- Solution: Obtain a **Transfer Appliance**, copy the data to it, and ship it to Google.


- A Transfer Appliance is the most cost-effective solution for data migration of large size. Obtaining a Transfer Appliance, copying the data to it, and shipping it to Google allows for a faster and more efficient migration. The Transfer Appliance is a physical device that can securely transfer large amounts of data offline. By copying the data onto the Transfer Appliance and physically shipping it to Google's data center, the data can be uploaded much more quickly than relying on the limited bandwidth.



### 7. An estimate of expected Google Cloud spending in the next quarter

- CASE: Your finance team has asked you to give them an estimate of expected Google Cloud spending in the next quarter. How can you come up with an estimate as quickly as possible?


- Solution: Use the Google Cloud Pricing Calculator to find out the expected spending of all resources in the project.


- Google Cloud Pricing Calculator is the right tool to estimate GCP costing. Using the Google Cloud Pricing Calculator allows you to accurately estimate the expected spending of all resources in the project. The Pricing Calculator takes into consideration various factors such as compute, storage, networking, and other services, providing a comprehensive estimate. 


### 8. Choosing a Load Balancer

- CASE: You are building a mobile game and have chosen to use an MIG within Compute Engine for your servers. Your game requires that the user's IP address is preserved in order to function normally. Your app needs to be exposed to the Internet using TCP protocl on port 389. Which Load Balancer type is most suitable for our game?


- Solution: **External TCP Network Load Balancer**.


- An **external TCP Network Load Balancer** can be used to expose the application to the Internet while preserving the clients' IP address. It can distribute the incoming TCP traffic to the instances in the managed instance group and maintain the source IP address information.



![choosing-load-balancer](/GCP_pictures/ACE-exam/mock-test-2/choosing-load-balancer.PNG "Choosing a load balancer")



### 9. Private Google Access

- CASE: Your security team has mandated that the VMs cannot have access to the Internet aand they can only have private IP addresses. Your app needs to have access to files hosted on Google Cloud Storage within your project. How can you enable this access without breaching the security requirements?


- Solution: Enable **Private Google Access** on the subnet within the custom VPC.


- Enabling Private Google Access on the subnet within the custom VPC allows VM instances in the VPC to access Google APIs and services, such as Cloud Storage, using internal IP addresses. This ensures that the application running on Compute VM instances can access the file hosted in the Cloud Storage bucket without requiring external Internet connectivity.



### 10. Limit resource in specific locations using Organization Policy

- CASE: According to data security policies, your company cannot store or process any data outside the US region. You have several development teams that use Google Cloud to work with data. How can you restrict your teams from creating Google Cloud resources outside the US region?


- Solution: 

1. Create a folder that contains all dev projects.

2. Limit resources in US location using an Organization Policy.


- Creating a folder to contain all the dev projects allows you to organize and manage them effectively. By creating an organization policy, you can enforce restrictions on resource creation in specific locations, in this case, the United States. This ensures that each dev team can only create cloud resources in the US.



### 11. Configure a Firewall Rule to allow communication between 2 servers

- CASE: You have built a 2-tier application on Google Cloud with an application tier and a database tier. You created two subnets (subnet-a and subnet-b) in the default VPC, where the application tier runs in subnet-a and the database tier runs in subnet-b. How can you configure a firewall rule so that only the application servers can communicate with the database servers?


- Solution:

1. Create 2 service accounts namely sa-app and sa-db.

2. Associate the service account sa-app with the application tier servers and the service account sa-db with the database tier servers.

3. Allow network traffic from source service account sa-app to target service account sa-db using an ingress firewall rule. 


![firewall-rule-for-communication](/GCP_pictures/ACE-exam/mock-test-2/firewall-rule-for-communication.PNG "Firewall rule for communication")


- It uses service accounts to control access between the application servers and the database servers. By associaing the sa-app service account with the application servers and the sa-db service account with the database servers, you can ensure that only traffic originating from the application servers (source service account sa-app) is allowed to reach the database servers (target service account sa-db). The ingress firewall rule is then created to specifically allow network traffic between these two service accounts.



### 12. Provide access to compute images and disks

- CASE: You need to provide access to compute images and disks to an external member of your team in one of your projects. 


- Solution:

1. Use the **Compute Image User** role as the basse for a custom role and add the **compute.disks.list** to the includePermission field.

2. Grant the custom rule to the user at the project level.


- To provide comprehensive access to compute images and disks, you would typically need both **compute.disks.list** and **compute.disks.use** permisions. The compute.disks.list permission allows users to list disks, while the compute.disks.use permission allows users to attach and detach disks from instances.


- So, for a more complete and accurate custom role that grants access to compute images disks, you would want to use the Compute Image User role as the base and add both ompute.disks.list and compute.disks.use permissions to the includedPermissions field of the custom role. This would ensure that the user has the necessary permissions to work with compute images and disks effectively.



### 13. Pub/Sub - Dataflow - Cloud Storage flow

- CASE: Your company makes IoT devices that are spread all across the world. You need a Data Lake on Google Cloud to process the data of these devices. Your backend in the cloud receives structured and unstructured data from millions of your IoT devices. What option from the following can be used to biuld a scalable and resilient architecture on Google Cloud?


- Solution: Use Dataflow to send data to Cloud Storage by streaming data into Pub/Sub.


- Streaming data to Pub/Sub is a recommended approach for handling large-scale data streams as it provides high availability and resiliency. Using Dataflow to process the data from Pub/Sub and send it to Cloud Storage is a common practice for storing structured and unstructured data in a data lake. Cloud Storage is a highly available and provides durability., making it suitable for long-term data storage in a data lake architecture. This combination of Pub/Sub and Dataflow ensures that the data is efficiently processed, stored, and made available for further analysis or processing in the data lake.



### 14. Migrating GCP projects

- CASE: Your company has been acquired by another company and you are merging your IT systems with the parent company. You have several GCP projects that need to be moved to the parent company's organization. The parent company will take care of the billing. How can you accomplish this with minimal effort?


- Solution:

1. Move the project to the other organization using the **projects.move** method.

2. Update the billing account of the project to that of your organization.


- Migrate a project to another organization.


```
gcloud beta projects move PROJECT_ID \
    --organization ORGANIZATION_ID
```


```
gcloud beta projects move PROJECT_ID \
    --folder FOLDER_ID
```


- PROJECT_ID: The project you wish to migrate

- ORGANIZATION_ID: Organization to which you want to move the project. You can specify either an organization or folder.



### 15. Cloud DNS service for Load Balancer IP address

- CASE: You have built an app that uses Compute Engine instances behind a load balancer. How can you access app through Cloud DNS such that home.mydomain.com, mydomain.com, and www.mydomain.com point to the IP address of your Google Cloud load balancer?


- Solution: Point mydomain.com to the load balancer using one A record, and create two CNAME records to point to WWW and HOME to mydomain.com respectively.


- A record is used to map a domain name to an IPv4 address. By creating one A record to point mydomain.com to the IP address of the load balancer, you ensure that mydomain.com resolves to the correct IP. To point home.mydomain.com and www.mydomain.com to the same IP address, you can create CNAME records. CNAME records are used to create an alias for a domain name. By creating 2 CNAME records, one for home.mydomain.com and one for www.mydomain.com, both pointing to mydomain.com, you can redirect these subdomains to the same IP address as mydomain.com.



### 16. Identity Aware Proxy (IAP) for secure SSH access

- CASE: After migrating Linux VMs to Google Cloud, you need to make sure the access to these VMs is secured without any extra charges. What should you do?


- Solution:

1. Allow ingress traffic from the IP range **35.235.240.0/20** on port 22.

2. Use the gcloud compute ssh command with the **--tunnel-through-iap** flag.


- Using the gcloud compute ssh command with the **--tunnel-through-iap** flag leverages Google Cloud's Identity-Aware Proxy (IAP) for secure SSH access. IAP provides an additional layer of security by requiring user authentication and authorization before granting access to the instances. Allowing ingress traffic from the IP range **35.235.240.0/20** on port 22 ensures that only traffic from Google's IAP service is allowed to reach the instances, enhancing security.



### 17. Reduce the startup latency with min-instances

- CASE: You are running a blogging website on Cloud Run which sees traffic for a few hunderd users. Some of your users have raised an issue that the loading time of the first page is higher than subsequent pages. What is the recommended practice to overcome this issue?


- Solution:  In your Cloud Run service, set the minimum number of instances to 3.


- Setting the minimum number of instances for your Cloud RUn keeps at least three instances running and ready to handle incoming requests. This helps reduce the startup latency that might occur when a new instance needs to be spun up to handle the initial request, improving the overall performance of the web application.



### 18. Synchronize an on-premises file system to Google Cloud Storage

- CASE: Your E-commerce website stores images in the server's local file system. You are exploring Cloud Storage to use as archive storage of these images. Which solution from the below options can be used to upload all newly created images to Google Cloud without needing manual intervention?


- Solution:

1. Prepare a script that employs the gcloud storage command to synchronize the on-premise storage with Cloud Storage.

2. Afterward, schedule the script as a cron job.


- It directly addresses the need for automatic and periodic synchronization of newly created images from an on-premise file system to Google Cloud Storage without manual intervention. By preparing a script that uses the 'gcloud storaage' command to synchronize the local file system with Cloud Storage, and scheduling this script to run as a cron job, you ensure that new images are automatically uploaded to Cloud Storage at regular intervals. This method is efficient for achieving continuous synchronization between on-premises stroage and Cloud Storage, aligning perfectly with the requirements outlined in the question.



### 19. Instance Template with Spot VMs On

- CASE: You are working at an E-commerce company that runs monthly batch processing on customer order data to generate insights. The batch process is run in an on-premises server and it takes around 20 hours to complete. The task is run only once a month and can be restarted if it is interrupted. How to migrate this job to Compute engine while optimizing costs?


- Solution:

1. Create a Managed Instance Group using a template with Spot VMs on and adjust Target CPU Utilization.

2. Migrate the workload.


- Creating an Instance Template with Spot VMs on allows you to take advantage of preemptible virtual machines, which are significantly cheaper than regular VMs, helping to minimize the cost. By creating the managed instance group from the template and adjusting the Target CPU Utilization, you can control the number of preemptible VMs running at any given time, optimizing cost and ensuring efficient resource usage. Migrating the workload to the Managed Instance group with preemptible VMs will allow you to execute the batch process in the cloud at a much lower cost while still achieving the required offline processing and ability to restart if interrupted.



### 20. Manage environments consistently with Deployment Template

- CASE: You team is building a brand new user-facing photo editing application and they plan to use GCP. The app will be deployed in 3 separate environments namely development, test, and production. How can you deploy and manage these environments to ensure that they are consistent?


- Solution: Create one deployment template that will work for all environments using the Cloud Foundation Toolkit(CFT), and deploy with Terraform.


- The Cloud Foundation (CFT) provides ready-made templates that reflect Google Cloud recommended practices and can be used to automate the creation of the environments. Creating one deployment template that is compatible with all environments using the Cloud Foundation Toolkit (CFT) and deploying with Terraform ensures consistency across environments. It allows for easy management and maintenance, reducing the chances of error or variations between environments.


- Terraform Resource Samples: https://cloud.google.com/docs/terraform/samples


- VM creation


```
# Create a VM instance from a public image
# in the `default` VPC network and subnet

resource "google_compute_instance" "default" {
  name         = "my-vm"
  machine_type = "n1-standard-1"
  zone         = "us-central1-a"

  boot_disk {
    initialize_params {
      image = "ubuntu-minimal-2210-kinetic-amd64-v20230126"
    }
  }

  network_interface {
    network = "default"
    access_config {}
  }
}
# [END compute_instances_create]

# [START vpc_compute_basic_vm_custom_vpc_network]
resource "google_compute_network" "custom" {
  name                    = "my-network"
  auto_create_subnetworks = false
}
# [END vpc_compute_basic_vm_custom_vpc_network]

# [START vpc_compute_basic_vm_custom_vpc_subnet]
resource "google_compute_subnetwork" "custom" {
  name          = "my-subnet"
  ip_cidr_range = "10.0.1.0/24"
  region        = "europe-west1"
  network       = google_compute_network.custom.id
}
# [END vpc_compute_basic_vm_custom_vpc_subnet]

# [START compute_instances_create_with_subnet]

# Create a VM in a custom VPC network and subnet

resource "google_compute_instance" "custom_subnet" {
  name         = "my-vm-instance"
  tags         = ["allow-ssh"]
  zone         = "europe-west1-b"
  machine_type = "e2-small"
  network_interface {
    network    = google_compute_network.custom.id
    subnetwork = google_compute_subnetwork.custom.id
  }
  boot_disk {
    initialize_params {
      image = "debian-cloud/debian-10"
    }
  }
}
# [END compute_instances_create_with_subnet]
# [END compute_basic_vm_parent_tag]
```


### 21. Scale down to zero when it is not in use

- CASE: You are bulding an internal web portal that is only going to be accessed duing business hours. In order to save costs, you need the application to scale down to zero when it is not in use. Which compute resource is the most suitable?


- Solution: A. Cloud Functions


A. Cloud Functions

B. Compute Engine

C. Google Kubernetes Engine

D. AppEngine flexible environment



- Cloud Functions charges based on invocations and CPU time. It scales down to zero billing when there is no traffic. Google Cloud Functions is a serverless compute platform that allows you to run code in response to events, such as HTTP requests, Pub/Sub messages, Cloud Storage events, etc. It automatically scales based on the number of incoming requests and scales down to zero when there is not activity. Since the application is only accessed during business hours, Cloud Functions is the most suitable choice as it will automatically scales down to zero during non-business hours, minimizing cost.




### 22. Use gcloud command for quick recreation of VMs in MIG

- CASE: You are running a shipment tracking application on a managed instance group on Google Cloud. While checking the logs, you found that one VM has unresponsive processes. How can you replace that VM quickly?


- Solution: Utilize the 'gcloud compute instance-groups managed recreate-instances' command to generate a new instance for the VM.


- The 'gcloud compute instance-groups managed recreate-instances' command allows you to recreate the VM in the managed instance group (MIG). This command terminates the unresponsive VM and create a new one to replace it in the MIG. This is the recommended approach to quickly replace a problematic VM in a MIG.



### 23. Delete the Pub/Sub topic created using Config Connector

- CASE: You are using Config Connector in Google Cloud and you have created a Pub/Sub topic using it. How can you permanently delete the Pub/Sub topic?


- Solution: Leverage kubectl to remove the topic resource.


- Using kubectl to delete the topic resource will permanently delete the Pub/Sub topic managed by Config Connector in the Google Cloud project.



### 24. Identity Federation between Cloud Identity and Google Workspace

- CASE: You are the Cloud Architect at your startup. All your employees have Google Workspace accounts. Your company is going to hire a large number of staff in the next 2 years. What should you do to make sure the systems and processes are able to support the growth in employee count without performance degradation, unnecessary complexity, or security issues?


- Solution:

- Turn on identity federation between Cloud Identity and Google Workspace.

- Enforce multi-factor authentication for domain-wide delegation.


- Turning on identity federation between Cloud Identity and Google Workspace allows for seamless and secure access management for the anticipated growth. Enforcing multi-factor authentication for domain-wide delegation adds an additional layer of security to protect the system from potential security issues. This approach doesn't require migrating to external systems and aligns with the cloud-native architecture, making it suitable for scalability and growth. Also, it combines seamless integration with security practices, aligning well with scalability and cloud-native principles. 



### 25. Removal of persistent disks sharing names with instance identifiers

- CASE: You are part of the SRE team for an E-commerce website. You received an alert that one of the instances in your managed instance groups failed to be created. What should you do to solve the instance creation problem?


- Solution:

1. Develop an instance template with an appropriate structure for utilization in the instance group.

2. Ensure the removal of persistent disks sharing names with instance identifiers.


- It addresses the common issue of instance creation failures within MIG on Google Cloud Platform, which can occur due to conflicts in naming conventions, particularly when persistent disks share names with instance identifiers. By developing a new instance template that ensures no shared names between eprsistent disks and instance identifiers, you eliminate one potential cause of instance creation failures. This solution directly tackles the problem mentioned in the alert without introducing unnecessary changes or configurations that might not be relevant to the specific issue at hand.


