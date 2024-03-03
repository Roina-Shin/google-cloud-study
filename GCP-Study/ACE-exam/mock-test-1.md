### [Source of this study material : GCP Associate Cloud Engineer Practice Test Exam by Sayyam](https://www.udemy.com/course/latest-gcp-ace-google-associate-cloud-engineer-practice-exams-tests)


## Exam -1

### 1. Create an Internal Load Balancer on Google Kubernetes Engine

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


- CASE: an application on Compute Engine located on a different VPC but in the same region needs to access the application on GKE.


- Solution: 

1. In GKE, create a LoadBalancer service type that uses the application's pods as backend.

2. Add an annotation: networking.gke.io/load-balancer-type: "Internal"

3. Peer the two VPCs together.

4. Configure the compute Engine instance to use the address of the load balancer that has been created.



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



### 6. Create a DaemonSet in the kube-system namespace of the cluster using the Deployment Manager Template.

- CASE: You are working on a Deployment Manager template and configure GCP resources. You want to create a DeamonSet in the kube-system namespace of the cluster using the Deployment Manager template.


- Solution: Add the cluster's API as a new Type Provider in Deployment Manager, and use the new tye to create the Deamonset.



### 7. Command like for only enabled APIs in a Project

- CASE: You need the list of the enabled Google Cloud Platform APIs for your GCP project. How can you use the command line to do it?


- Solution: Run **gcloud services list --project <project ID>** to list only the enabled APIs in the project. You can choose the mode in which the command will list services by using exactly one of the **--enabled** or **--available** flags. **--enalbed** is the default. Running the **gcloud services list --project <project ID>** will retrieve all the enabled services for the specified GCP project.


![gcloud-services-list](/GCP_pictures/ACE-exam/mock-test-1/gcloud-services-list.PNG "gcloud services list")



### 8. Rolling Update on MIGs

- CASE: You want to apply an update to all instances in MIG while minimizing downtime and affected capacity in the application.


- Solution: 

1. Perform a rolling-action start-update

2. maxSurge set to 1

3. masUnavailable set to 0


- The maxSurge option is used to configure how many new instances the MIG can create above its targetSize during an automated update and the maxUnavailable option is used to configure how many instances are unavailable at any time during an automated update. The maxUnavailable count must be 0. It sets maxSurge to 1, allowing for one additional instance to be created during the update process. This will provide additional capacity to handle the deployment and ensure that live traffic is not affected. Setting maxUnavailable to 0 ensures that the available capacity does not decrease during the deployment, further minimizing downtime.


![rolling-update-to-MIG](/GCP_pictures/ACE-exam/mock-test-1/rolling-update-to-instance-group.PNG "Rolling update to MIG")


### 9. Link a project to a billing account

- CASE: Finance team needs to link a project to a billing account. What should you do?


- Solution:

Assign the Finance team:

1. On billing account -> **Billing Account User Role**

2. In the organization -> **Project Billing Manager Role**


- Finance team needs the billing account user role to access the billing account and the billing administrator role in the project in order to link the billing account to the project. This option involves granting the finance team two distinc roles. First, they are granted the Billing Account User role at the billing account level. This allows them to manage billing information and budgets. Second, at the organizational level, they are given the Project Billing Manager role. This role specifically grants authority to link project to billing accounts. By combining these roles, this option ensures that only the finance team has the necessary permissions to link projects to the billing account, meeting the requirements of the scenario.



### 10. Enable communication beween 2 VMs in different projects in the same org.

- CASE: You need to enable communication between 2 compute engine VMs hosted on different projects in separate VPCs in the same org.


- Solution:

1. Make sure both projects belong to the same GCP organization.

2. Share the VPC from one project and request that the Compute Engine instances in the other porject use this shared VPC.


- Shared VPC allows an organization to connect resources from multiple projects to a common VPC so that they can communicate with each other securely using internal IPs from that network. Only projects within the same organization can share a VPC.


