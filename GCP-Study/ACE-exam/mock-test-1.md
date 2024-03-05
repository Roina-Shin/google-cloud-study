### [Source of this study material : GCP Associate Cloud Engineer Practice Test Exam by Sayyam](https://www.udemy.com/course/latest-gcp-ace-google-associate-cloud-engineer-practice-exams-tests)


## Exam -1

### 1. Create an Internal Load Balancer on Google Kubernetes Engine

- CASE: an application on Compute Engine located on a different VPC but in the same region needs to access the application on GKE.


- Solution: 

1. In GKE, create a LoadBalancer service type that uses the application's pods as backend.

2. Add an annotation: networking.gke.io/load-balancer-type: "Internal"

3. Peer the two VPCs together.

4. Configure the compute Engine instance to use the address of the load balancer that has been created.


Source: https://cloud.google.com/kubernetes-engine/docs/how-to/internal-load-balancing


- **Internal Load Balancer for Google Kubernetes Engine** can be accessible to VM instances located in the cluster's VPC.


- **Internal Load Balancer for GKE** sample YAML files for deployment and service.


```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ilb-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: ilb-deployment
  template:
    metadata:
      labels:
        app: ilb-deployment
    spec:
      containers:
      - name: hello-app
        image: us-docker.pkg.dev/google-samples/containers/gke/hello-app:1.0
```

- Container Registry hosts containers on the domain ```gcr.io``` and Artifact Registry hosts containers on the domain ```pkg.dev```.


- For example, in Container Registry, this command pushes the image ```my-image``` to the registry ```eu.gcr.io``` in the project my-project.


```
docker push eu.gcr.io/my-project/my-image
```


- In Artifact Registry, this command pushes the image ```my-image``` to the regional repository ```europe-north1-docker.pkg.dev```in repository ```my-repo``` and the project ```my-project```.


```
docker push europe-north1-docker.pkg.dev/my-project/my-repo/my-image
```


Source: https://cloud.google.com/artifact-registry/docs/transition/setup-repo



```
apiVersion: v1
kind: Service
metadata:
  name: ilb-svc
  annotations:
    networking.gke.io/load-balancer-type: "Internal"
spec:
  type: LoadBalancer
  externalTrafficPolicy: Cluster
  selector:
    app: ilb-deployment
  ports:
  - name: tcp-port
    protocol: TCP
    port: 8080
    targetPort: 8080
```


- Your manifest must contain **an annotation** that specifies that you require an internal loadbalancer service. For GKE version 1.17 and later, use the annotation **networking.gke.io/load-balancer-type: "Internal"** as above. For earlier versions, use **cloud.google.com/load-balancer-type: "Internal"** instead.



### 2. Configure Private Google Access for on-premises hosts

Source: https://cloud.google.com/vpc/docs/configure-private-google-access-hybrid


- **Private Google Access** for on-premises hosts provides a way for on-premises system to connect to Google APIs and services by routing traffic through a Cloud VPN tunnel or Cloud Interconnect.


- CASE: your on-premises servers hosting the application do not have public IP and you want to provide the application access to Cloud Storage.


- Solution:

1. Using Private VPN and Interconnect, create a tunnel to a VPC in Google Cloud.

2. Use Cloud Router to create a custom route advertisement.

3. In your on-premises network, configure your DNS server to resolve ***.googleapis.com** to **restricted.googleapis.com** as a **CNAME**.



- Create a Managed Private Zone in Cloud DNS.


```
gcloud dns managed-zones create ZONE_NAME \
 --visibility=private \
 --networks=https://www.googleapis.com/compute/v1/projects/PROJECT_ID/global/networks/NETWORK_NAME \
 --description=DESCRIPTION \
 --dns-name=googleapis.com
```


- Start a Transaction.


```
gcloud dns record-sets transaction start --zone=ZONE_NAME
```


- Add DNS record (CNAME):


```
gcloud dns record-sets transaction add --name=*.googleapis.com. \
    --type=CNAME restricted.googleapis.com. \
    --zone=ZONE_NAME \
    --ttl=300
```


- Add DNS record (A):


```
gcloud dns record-sets transaction add --name=restricted.googleapis.com. \
    --type=A 199.36.153.4, 199.36.153.5, 199.36.153.6, 199.36.153.7 \
    --zone=ZONE_NAME \
    --ttl=300
```



### 3. RDP to Windows VM

- When creating a VM, choose **windows server** in boot disk. 


- On the right hand side, click dropdown besides **RDP** (it's where SSH is for linux VMs) and click **Set Windows password**.


- Giver new **username** and Google will automatically generate a new Windows password.


- Copy the **password** and keep it in the notepad. 


- Also, click dropdown again and click **Download the RDP file**.


- Click connect and the **Remote Desktop Connection** will start. 


- The you will be prompted to enter your **credentials**. The credentials (username, password) will be used to connect to your windows vm (35.224.49.174).


- Then, we will be logged in the windows VM. 


- CASE: What should I do if I plan to use a windows VM on Compute Engine?


- Solution: Create the VM using gcloud and use **gcloud compute reset-windows-password** to generate the login credentials for the VM.


- This command will cause the account to be created and the password for that new account will be returned. 



### 4. Integrate Cloud Pub/Sub with Cloud Run

- CASE: Your team create an app that directly consumes messages from a Cloud Pub/Sub topic. The app will be deployed on Cloud Run. What recommended practice should you follow?


- Solution:

1. Create a service account.

2. Give the **Cloud Run Invoker** role to that service account for your Cloud Run application.

3. Create a Cloud Pub/Sub subscription that uses that service account and uses your Cloud Run application as the push endpoint.



### 5. Authenticate with GCP APIs using service account

- CASE: Your on-premise app needs to authenticate with GCP APIs for using GCP AutoML. What should you do?


- Solution: Create a key file for the service account with appropriate permissions using gcloud.


- To use a service account outside of Google Cloud, such as on other platforms or on-premises, you must first establish the identity of the service account. Public/private key pairs provide a secure way of accomplishing this goal.


- Creating a key file for the service account with appropriate permissions using gcloud is the recommended approach as it allows the on-premise service to authenticate with GCP APIs using the key file securely.



### 6. Ensure that your GKE in one project can download container iamges from the other central project

- CASE: All container images are stored in a single GCP project and your GKE cluster in the other project needs to have access to these images. 


- Solution: In the project where the images are stored, grant the **Storage Object Viewer** IAM role to the service account used by the Kubernetes nodes.


- Container Registry uses Cloud Storage buckets as the underlying storage for container images. 


- Granting the **Storage Object Viewer** IAM role to the service account used by the Kubernetes nodes allows them to have read access to the container images in the central project's Container Registry.



### 7. Create a DaemonSet in the kube-system namespace of the cluster using the Deployment Manager Template.

- CASE: You are working on a Deployment Manager template and configure GCP resources. You want to create a DeamonSet in the kube-system namespace of the cluster using the Deployment Manager template.


- Solution: Add the cluster's API as a new Type Provider in Deployment Manager, and use the new tye to create the Deamonset.



### 8. Command like for only enabled APIs in a Project

- CASE: You need the list of the enabled Google Cloud Platform APIs for your GCP project. How can you use the command line to do it?


- Solution: Run **gcloud services list --project <project ID>** to list only the enabled APIs in the project. You can choose the mode in which the command will list services by using exactly one of the **--enabled** or **--available** flags. **--enalbed** is the default. Running the **gcloud services list --project <project ID>** will retrieve all the enabled services for the specified GCP project.


![gcloud-services-list](/GCP_pictures/ACE-exam/mock-test-1/gcloud-services-list.PNG "gcloud services list")



### 9. Rolling Update on MIGs

- CASE: You want to apply an update to all instances in MIG while minimizing downtime and affected capacity in the application.


- Solution: 

1. Perform a rolling-action start-update

2. maxSurge set to 1

3. masUnavailable set to 0


- The maxSurge option is used to configure how many new instances the MIG can create above its targetSize during an automated update and the maxUnavailable option is used to configure how many instances are unavailable at any time during an automated update. The maxUnavailable count must be 0. It sets maxSurge to 1, allowing for one additional instance to be created during the update process. This will provide additional capacity to handle the deployment and ensure that live traffic is not affected. Setting maxUnavailable to 0 ensures that the available capacity does not decrease during the deployment, further minimizing downtime.


![rolling-update-to-MIG](/GCP_pictures/ACE-exam/mock-test-1/rolling-update-to-instance-group.PNG "Rolling update to MIG")


### 10. Link a project to a billing account

- CASE: Finance team needs to link a project to a billing account. What should you do?


- Solution:

Assign the Finance team:

1. On billing account -> **Billing Account User Role**

2. In the organization -> **Project Billing Manager Role**


- Finance team needs the billing account user role to access the billing account and the billing administrator role in the project in order to link the billing account to the project. This option involves granting the finance team two distinc roles. First, they are granted the Billing Account User role at the billing account level. This allows them to manage billing information and budgets. Second, at the organizational level, they are given the Project Billing Manager role. This role specifically grants authority to link project to billing accounts. By combining these roles, this option ensures that only the finance team has the necessary permissions to link projects to the billing account, meeting the requirements of the scenario.



### 11. Enable communication beween 2 VMs in different projects in the same org.

- CASE: You need to enable communication between 2 compute engine VMs hosted on different projects in separate VPCs in the same org.


- Solution:

1. Make sure both projects belong to the same GCP organization.

2. Share the VPC from one project and request that the Compute Engine instances in the other porject use this shared VPC.


- Shared VPC allows an organization to connect resources from multiple projects to a common VPC so that they can communicate with each other securely using internal IPs from that network. Only projects within the same organization can share a VPC.



### 12. Implement a single caching HTTP reverse proxy on GCP to reduce latency.

- CASE: Your website latency is caused by repeated database queries of similar nature. You plan to implement a single caching HTTP reverse proxy on GCP to reduce latency. This proxy needs 30 GB in-memory cache and an additional 2 GP of memory for the rest of the process. 


- Solution: Use a **Cloud Memorystore for Redis instance** with 32 GB capacity.


- Cloud Memorystore is the managed version of redis or Memcached. It suggests using Cloud Memorystore for Redis instance with a 32 GB capacity. Cloud Memorystore is a fully managed data store service provided by Google Cloud Platform, and it is specifically designed for caching purposes like this. It provides high performance and low-latency access to data stored in memory, which will help reduce latency issues experienced by the website.



### 13. Expand the IP range of a subnet

- CASE: The current subnet has no more free IP addresses. You are planning to migrate 15 more VMs on the same subnet.


- Solution: Expand the IP range of the current subnet using gcloud. To expand the IP range of subnet to **/16**, run:


```
gcloud compute networks subnets expand-ip-range SUBNET --region=us-central1 --prefix-length=16
```


![gcloud-exapnd-ip-range](/GCP_pictures/ACE-exam/mock-test-1/gcloud-expand-ip-range.PNG "gcloud expand ip range")



### 14. Create a GKE node pool with a sandbox type "gvisor"

- CASE: You run multi-tenant clusters whose containers run untrusted workloads. For security purposes, all customers' pods need to be isolated. How can you achieve this?


- Solution: 

1. Create a GKE node pool with a sandbox type configured to gvisor.

2. Add the parameter runtimeClassName: gvisor to the specification of your customers' pods.



```
gcloud container node-pools create smt-enabled \
  --cluster=CLUSTER_NAME \
  --machine-type=MACHINE_TYPE \
  --threads-per-core=2 \
  --sandbox type=gvisor
```


```
apiVersion: v1
kind: Pod
metadata:
  name: nginx-untrusted
spec:
  runtimeClassName: gvisor
  containers:
  - name: nginx
    image: nginx
```


- GKE Sandbox protects the hostkernel on your nodes when containers in the pod executes unknown or untrusted code. For example, multi-tenant clusters such as software-as-a-service providers often execute unknown code submitted by their users. It suggests creating a GKE node pool with a **sandbox type configured to gvisor** and adding the parameter **runtimeClassName: gvisor** to the specification of customers' pods. gVisor is an open-source sandbox runtime that provides isolation for containers. By configuring the node pool to use gvisor as the sandbox type and specifying gvisor as the runtime class for customers' pods, it ensures that each pod is isolated and runs within its own secure environment. 



### 15. How to use gcloud config

- CASE: Use **gcloud config** to identify currently active google cloud project.


- Solution:

1. Check which project is active


```
gcloud config get-value project
```


2. View all your projects


```
gcloud projects list
```


3. Switch to a particular project


```
gcloud config set project PROJECT_ID
```


### 16. How to make SDAP server reachable via TLS on port 636 over UDP

- CASE: Your company is migrating Active Directory to GCP. As a first step, you deployed an LDAP server on a Compute Engine instance. The LDAP server is reachable via TLS on port 636 over UDP. How can you make sure the clients can access the server?


- Solution: 

1. Tag the VM running the LDAP server with a **network tag** of your choice.


2. Create a firewall rule to allow **ingress on UDP port 636** for that **networking tag**.


- The LDAP server will sit internally in the network protected by a Firewall, so an ingress rule will allow traffic to be routed internally to the LDAP server. It suggests tagging the VM running the LDAP server with a network tag of your choice and creating a firewall rule to allow ingress on UDP port 636 for that network tag. By tagging the VM and creating a specific firewall rule for that tag, you can control the traffic and allow clients to access the server on port 636.



### 17. Compute Engine Machine Type n1-standard-96

- CASE: The application requires 96 vCPU to perform its tasks. How can you create a similar environment in GCP to run this application?


- Solution: Use **Compute Engine machine type n1-standard-96**.


- Using Compute Engine machine type n1-standard-96 is the most direct and appropriate way to create a similar environment with 96 vCPUs in GCP. This machine type provides the necessary number of CPUs required by the application.



![machine-types-general-purpose](/GCP_pictures/ACE-exam/mock-test-1/general-purpose-workloads.PNG "General purpose workload machine type")



### 18. Search which table contains a specific field name in BigQuery

- CASE: Your CIO asked you to examine all datasets to find tables that contain an employee_nu column. How can you perform this task with minimum effort?


- Solution: Search for employee_nu in the search box in the **Data Catalog**.


- Data Catalog allows you to discover, manage, and understand data assets across Google Cloud Platform. Data Catalog API natively indexes Cloud Storage, and Cloud Pub/Sub data assets. Searching for the "employee_nu" column in the search box in the Data Catalog is the simplest way to find all datasets that contain this column. The Data Catalog is a centralized and searchable metadata service that allows users to easily discover and understand the data assets within their organization. By searching for the specific column name, the user can quickly identify all datasets that meet the given criteria.


### 19. Know when users are added to Cloud Spanner Identity Access Management roles on a GCP project

- CASE: You want to know when users were added to Cloud Spanner Identity Access Management roles on a certain GCP project.


- Solution: Review admin activity logs by filtering them for Cloud Spanner IAM roles in the Cloud Logging console.


- The Admin Activity logs show when users were given roles. The Admin Activity logs in the Cloud Logging console can be filtered to show specific activities related to Cloud Spanner IAM roles. These logs can provide a historical record of when users were added to IAM roles in Cloud Spanner.



### 20. Control BigQuery budget

- CASE: Query costs for BigQuery are going out of budget as multiple teams run queries and you want to control these costs. Which method is the most suitable. 


- Solution: Apply custom query quota for BigQuery data warehouse at the user-level or project-level.


- Adding a query quota can help limit costs. Applying custom query quotas for BigQuery at the user-level or project-level allows you to set limits on the amount of query resources users or projects can consume. By setting accurate quotas, you can prevent excessive query costs and ensure that each team or user stays within their allocated budget.