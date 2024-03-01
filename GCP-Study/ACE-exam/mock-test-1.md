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