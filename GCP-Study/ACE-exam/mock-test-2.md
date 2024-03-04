### [Source of this study material : GCP Associate Cloud Engineer Practice Test Exam by Sayyam](https://www.udemy.com/course/latest-gcp-ace-google-associate-cloud-engineer-practice-exams-tests)


## Exam -2

### 1. Send transactions to Pub/Sub and use MIG to process them

- CASE: Your game generates millions of events every minute. All these events need to be processed as transactions The amount of computation required to process the transactions is way more than the processing capabilities of a single VM. How can you spread these transactions across multiple VMs in real-time in a cost-effective manner?


- Solution: 

1. Send all the transatcions to Pub/Sub.

2. Use a managed instance group to process them in VMs. 


- Pub/Sub can effectively distribute a large number of tasks among multiple servers at a low cost. Sending all transactions to Pub/Sub and using a managed instance group to process them in VMs is a scalable and cost-effective solution. Pub/Sub allows for real-time data streaming and the managed instance group ensures that the transactions are spread across multiple VMs to handle the high volume of events.


### 2. Backend service and frontend service in GKE

- CASE: The app has a backend service and frontend service, both deployed as Kubernetes deployments. How can you make sure that the communication between the frontend service and backend service is not affected if pods are moved or restarted?


- Solution: 

1. Create a service that groups your pods in the backend service.

2. Configure the frontend pods to communicate through that service.


- The Kubernetes service serves the purpose of providing a destination that can be used when the pods are moved or restarted. Creating a service in Kubernetes allows for reliable communication between the frontend and backend services even if pods are moved or restarted. By grouping the backend pods under a service, the frontend pods can communicate with the service, which automatically routes the traffic to the available backend pods. This ensures that the communication is not affected by pod movements or restarts.



### 3. Use Object Lifecycle management policies

- CASE: You need to follow certain regulations according to your organization's policy.

1. All data older than one year must be archived.

2. Data older than 5 years must be deleted.

3. All other data must be stored on Standard storage.


- Solution: Create **Object Lifecycle** management policies.


- Object Lifecycle allows you to automate the implementation of your organization's data policy. Creating Object Lifecycle management policies in Cloud Storage allows for a simple and automated way to implement the given guidelines. By creating lifecycle rules, data can be automatically transitioned to the appropriate storage class (such as ARCHIVE) based on its age. Additionally, data can be automatically deleted after a specified duration. This approach ensures compliance with organization's policy without the need for manual intervention or scripts.



### 4. Static external IP address and Cloud DNS

- CASE: You have built a service that is used by many partners. You want to make sure that the IP does not need to be changed in your DNS if the server crashes or if it is replaced. How to deliver this solution with minimal cost and avoid downtime?


- Solution: Reserve a static external IP address, and assign it using Cloud DNS.


- External IPs are routable and can be advertised and seen on the Internet, and this is also the most cost-effective solution. Reserving a static external IP addresses ensures that the IP does not need to be changed in the DNS even if the server crashes or is replaced. This way, the service can be accesses consistently without any downtime.


### 5. Attaching labels to resources

- CASE: Your management has asked you to investigate resources consumption charges and present a summary of your findings for your GCP environment.


- Solution: 

1. Attach labels to resources to reflect the owner and purpose.

2. Export Cloud Billing data into BigQuery and create a Data Studio dashboard for analysis.