### [Source of this study material : GCP Associate Cloud Engineer by Ranga Karanam](https://www.udemy.com/course/google-cloud-certification-associate-cloud-engineer/)

## Google Kubernetes Engine (GKE)

 ### Kubernetes

 - Most popular open source container orchestration solution.

 - It provides cluster management (including upgrades).

 - It provides all important container orchestration features:

   - Auto scaling

   - Load balancer

   - Self healing

   - Zero downtime deployments

 ### Googke Kubernetes Engine

 - Managed kubernetes service.

 - Minimizes operations with auto-repair (repair failed nodes) and auto-upgrade (use latest version of K8S always) features.

 - Provides **Pod and Cluster Autoscaling**.

 - Provides support for **persistent disks** and **local SSD**.


## Create a GKE Cluster

- Go to the Kubernetes Engine and click Create a Cluster.


![create-a-cluster](/GCP_pictures/Study-logs/GKE/create-cluster.PNG "Create a GKE cluster")


- When you click Create button, you are automatically taken to the **Autopilot mode** configuration page. 


![switch-to-standard-cluster](/GCP_pictures/Study-logs/GKE/switch-to-standard-cluster.PNG "Switch to the Standard Cluster mode")


- Only give the name to the cluster and leave all the settings as default. And create.

- Once created, go to Cloud Shell and run the following:

```
gcloud config set project [project-id]
```

- Now, it's time to connect your cluster via command-line. Go to Kubernetes console again and click actions (three dots) and go to Connect.


![connect-cluster](/GCP_pictures/Study-logs/GKE/connect-cluster.PNG "Connect a cluster via command line")


- Once clicked, copy the command line:


![copy-the-commandline](/GCP_pictures/Study-logs/GKE/connect-command-line.PNG "Copy the command line")


- If you got a message like below in the Cloud Shell, then you are good to go and use *kubectl* commands:


![kubectl-command-generated](/GCP_pictures/Study-logs/GKE/kubectl-commands-generated.PNG "kubectl command is now available in cloud shell")


- Run the command. As the image below was already pushed by the instructor to the Docker Hub, you don't need to worry about it:


```
kubectl create deployment hello-world-rest-api --image=in28min/hello-world-rest-api:0.0.1.RELEASE
```


![kubectl-create-deployment](/GCP_pictures/Study-logs/GKE/kubectl-create-deployment.PNG "Create a deployment using kubectl")


- To see if the deployment is working, run:

```
kubectl get deployment
```


![kubectl-get-deployment](/GCP_pictures/Study-logs/GKE/kubectl-get-deployment.PNG "kubectl get deployment")


- To expose the deployment to the outside Internet, run:

```
kubectl expose deployment hello-world-rest-api --type=LoadBalancer --port=8080
```

- When you expose a deployment, something called **a service** is created. You can check this by running:

```
kubectl get services
```


![kubectl-get-services](/GCP_pictures/Study-logs/GKE/kubectl-get-services.PNG "kubectl get services")


- As you see, the type of service we created here is a load balancer. You can also see the external IP of the service. Grab it and curl it:

```
curl [external IP address]:8080
```

- It returns back healty true:


![healthy-true](/GCP_pictures/Study-logs/GKE/healthy-true.PNG "Returns healthy true")


- To set an autoscaler on your deployment:

```
kubectl autoscale deployment hello-world-rest-api --max=4 --cpu-percent=70
```


![horizontal-pod-autoscaling](/GCP_pictures/Study-logs/GKE/horizontal-pod-autoscaling.PNG "Horizontal pod autoscaling")


- It is something called 'Horizontal Pod Autoscaling (hpa)'. You can actually run the command:

```
kubectl get hpa
```


![hpa-command](/GCP_pictures/Study-logs/GKE/hpa-command.PNG "The result of running a hpa command")


- In addition to the pod autoscaling, you can also set up an auto scaling for your cluster:

```
gcloud container clugsters update clusster-name --enable-autoscaling --min-nodes=1 --max-nodes=10 --zone=us-central1-c
```

## GKE Cluster

- Cluster is a group of compute engine instances including:

  - **Master node**: manages the cluster

    - **API server**: handles all communication for a cluster (from nodes and outside)

    - **Scheduler**: decides placement of pods

    - **Control manager**: manages deployments & replica sets

    - **etcd**: distributed database that stores the data of the cluster state

  - **Worker nodes**: run your workloads (pods)

    - **pods**

    - **kubelet**


 ### Kubernetes - Pods

 - Pod is a smallest deployable unit in Kubernetes.

 - A pod contains **one or more containers**.

 - Each pod is assigned an ephemeral IP address.

 - Pod is where microservices are running.

 - Pod can have multiple containers inside of it. But most pods have just one container.

 - When we created a deployment with 3 instances, we had 3 pods.

 - This command will give you a more detailed info about a pod:

 ```
 kubectl get pods -o wide
 ```

 ![kubectl-pod-detail](/GCP_pictures/Study-logs/GKE/kubectl-pod-detail.PNG "To see the details of a pod")


 - All containers in a pod share:

   - Network

   - Storage

   - IP Address

   - Ports

   - Volumes (shared persistent disk)

 - Pod statuses: Running / Pending / Succeeded / Failed / Unknown


 ### Kubernetes - Deployment vs Replica Set

 - A **deployment** is created for each microservice:

 ```
 kubectl create deployment m1 --image=m1:v1
 ```

 - A single deployment represents a microservice (with all its releases).

 - Deployment manages new releases ensuring zero downtime. You can easily upgrade to a new version without any downtime.

 - To update the deployment to another version:

 ```
 kubectl set image deployment m1 m1=m1:v2
 ```

 ```
 kubectl set image deployment hello-world-rest-api hello-world-rest-api=in28min/hello-world-rest-api:0.0.2.RELEASE
 ```


 ![update-deployment](/GCP_pictures/Study-logs/GKE/update-deployment.PNG "Update a deployment using kubectl")


 - A **replica set** on the other hand ensures that a specific number of pods are running for a specific microservice version.


 ![pod-replicaset-structure](/GCP_pictures/Study-logs/GKE/pod-replicaset-structure.PNG "Deployment vs Replica Set")


 - To ensure that you have always 2 replica sets running, run:

 ```
 kubectl scale deployment m2 --replicas=2
 ```


 ![kubectl-get-replicasets](/GCP_pictures/Study-logs/GKE/kubectl-get-replicasets.PNG "kubectl get replicasets")



 ### Kubernetes - Service

 - Each pod has its own IP address:

   - Create service:

     ```
     kubectl expose deployment deployment-name --type=LoadBalancer --port=80
     ```

   - Expose pods to outside world using a stable IP address.

   - Ensures that the external world doesn't get impacted as pods go down and come up.


 - 3 Types of services:

   - **ClusterIP**: exposes service on a cluster-internal IP.

     - Use cases: you want your microservice only to be available inside the cluster (intra cluster communication)

   - **LoadBalancer**: exposes service externally using a cloud provider's load balancer.

     - Use cases: you want to create an individual load balancer for each microservice.

   - **NodePort**: exposes service on each node's IP at a static port.

     - Use cases: you **don't** want to create an external load balancer for each microservice (You can create one Ingress component to load balance multiple microservices.)



 ### Artifact Registry

 - Docker Hub is a public container registry.

 - Artifact Registry can be integrated to CI/CD tools like Cloud Build to publish images to registry.

 - You can secure your container images. You can also analyze images for vulnerabilities and enforce deployment policies.


 ### GKE Cluster command line

| Description | Command |
| ------ | ----------- |
| Create Cluster   | gcloud container clusters **create** my-cluster --zone us-central1-c --node-location us-central1-c,us-central1-b |
| Resize Cluster  | gcloud container clusters **resize** my-cluster --node-pool my-node-pool --num-nodes 10 |
| Autoscale Cluster    | gcloud container clusters **update** cluster-name --enable-autoscaling --min-nodes=1 --max-nodes=3 |
| Delete Cluster    | gcloud container clusters **delete** my-cluster |
| Adding Node Pool    | gcloud container **node-pools create** new-node-pool-name --cluster my-cluster |
| List Images    | gcloud container images list |


 ### GKE Workload command line

| Description | Command |
| ------ | ----------- |
| List Pods/Service/ReplicaSets   | kubectl **get pods/services/replicasets** |
| Create Deployment  | kubectl **apply -f deployment.yaml** or kubectl **create deployment** |
| Create Service    | kubectl **expose deployment** hello-world-rest-api --type=LoadBalancer --port=8080 |
| Scale Deployment    | kubectl **scale deployment** hello-world-rest-api --replicas=2 |
| Autoscale Deployment    | kubectl **autoscale deployment** --max=2 --cpu-percent=70 |
| Delete Deployment    | kubectl **delete deployment** hello-world-rest-api |
| Update Deployment    | kubectl **apply -f** deployment.yaml |
| Rollback Deployment    | kubectl **rollout undo deployment** hello-world-rest-api --to-revision=1 |
