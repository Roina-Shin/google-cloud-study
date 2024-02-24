### [Source of this study material : GCP Associate Cloud Architect by Ranga Karanam](https://www.udemy.com/course/google-cloud-professional-cloud-architect-certification/)

## Google Kubernetes Engine (GKE)

- Most popular open source container orchestration solution.


- Provides cluter management (including upgrades).


- Provides all important container orchestration features:

  - Auto scaling

  - Service discovery

  - Load Balancer

  - Self healing

  - Zero downtime deployments


- Minimizes operations with auto-repair (repair failed nodes) and auto-upgrade (use latest version of K8S) features.


- Uses **Container-optimized OS**, a hardened OS built by Google.


- Provides support for **persistent disks** and **local SSD**.


## A Microservice Journey Demo

- First, we will create a Kubernetes cluster **in standard mode** with the default node pool.


- Connect to the cluster from the cloud shell:


![gcloud-container-clusters](/GCP_pictures/Study-logs/gke-kubernetes-journey/gcloud-container-clusters.PNG "gcloud container clusters")


- Now, we will deploy a microservice (deployment + service) using kubectl command:


```
kubectl create deployment hello-world-rest-api --image=in28min/hello-world-rest-api:0.0.1.RELEASE
```


![create-deployment](/GCP_pictures/Study-logs/gke-kubernetes-journey/create-deployment.PNG "Create a deployment")


- This time, we will expose the deployment as a LoadBalancer service.


```
kubectl expose deploy hello-world-rest-api --type=LoadBalancer --port=8080
```


![kubectl-expose-deploy](/GCP_pictures/Study-logs/gke-kubernetes-journey/kubectl-expose-deploy.PNG "kubectl expose deploy")


- If I go and access the external IP of the LoadBalancer, I can see that it works.


![external-ip](/GCP_pictures/Study-logs/gke-kubernetes-journey/external-ip.PNG "External IP")


- You can scale out your deployment by running:


```
kubectl scale deploy hello-world-rest-api --replicas=3
```


- This time, we will **increase the number of nodes** in your Kubernetes cluster:


```
gcloud container clusters resize standard-cluster-public-1 --node-pool default-pool --num-nodes 2  --region us-central1
```


- But we are not happy about manually resizing the number of nodes, etc. We will see how to scale automatically.


- You can **set up auto scaling** for your microservice.


```
kubectl autoscale deployment hello-world-rest-api --max=4 --cpu-percent=70
```


![autoscale-command](/GCP_pictures/Study-logs/gke-kubernetes-journey/autoscale-command.PNG "autoscale command")


- When you run **kubectl autoscale deployment** command, what gets created inside Kubernetes is **horizontal pod autoscaling (HPA)**. Verify this by running **kubectl get hpa**.


![kubectl-get-hpa](/GCP_pictures/Study-logs/gke-kubernetes-journey/kubectl-get-hpa.PNG "kubectl get hpa")


- Now, in addition to your microservice, you want to **autoscale your cluster** as well.


```
gcloud container clusters update [cluster-name] --enable-autoscaling --min-nodes=1 --max-nodes=5  --region us-central1
```


- You can create a secret inside Kubernetes:


```
kubectl create secret generic hello-world-secret --from-literal=RDS_PASSWORD=yejinsecret
```


- If you verify the secret, you can see that the secret is opaque (not shown in plain text)


```
kubectl get secret
```


![kubectl-create-secret](/GCP_pictures/Study-logs/gke-kubernetes-journey/kubectl-create-secret.PNG "kubectl create secret")



## Understanding Kubernetes Components

### Deploy a new microservice which needs nodes with a GPU attached

- Attach a new node pool with GPU instances to your cluster.


```
gcloud container node-pools create POOL_NAME --cluster CLUSTER_NAME
```

- The command to list the node pools is:


```
gcloud container node-pools list --cluster CLUSTER_NAME --region REGION
```


![gcloud-container-node-pools-list](/GCP_pictures/Study-logs/gke-kubernetes-journey/gcloud-container-node-pools-list.PNG "gcloud container node-pools list --cluster")


- If you want a specific cluster to be a default cluster, you can set this:


```
gcloud config set container/cluster CLUSTER_NAME
```


![gcloud-config-set-container/cluster](/GCP_pictures/Study-logs/gke-kubernetes-journey/gcloud-config-set-container-cluster.PNG "gcloud config set container/cluster CLUSTER_NAME")


- Then you can deploy the new microservice to the new pool by setting up **nodeSelector** in the **deployment.yaml**.


- If you want to delete the microservices:


```
kubectl delete svc SERVICE_NAME
```


```
kubectl delete deploy DEPLOYMENT_NAME
```


- If you want to delete the cluster:


```
gcloud container clusters delete CLUSTER_NAME
```


### Understanding Deployment and Services

- To update the deployment to a newer version:


```
kubectl set image deployment/[deployment-name] [container-name]=[new container image name]
```

```
kubectl set image deployment/hello-world-rest-api hello-world-rest-api=in28min/hello-world-rest-api:0.0.2.RELEASE
```


![kubectl-set-image](/GCP_pictures/Study-logs/gke-kubernetes-journey/kubectl-set-image.PNG "kubectl set image")



- To annotate the deployment change cause, you can run:


```
kubectl annotate deployment/hello-world-rest-api kubernetes.io/change-cause="deployment update to v2"
```


![kubectl-annotate-deployment](/GCP_pictures/Study-logs/gke-kubernetes-journey/kubectl-annotate-deployment.PNG "kubectl annotate deployment")


- If you verify it on the browser, you can see that the application is now updated to v2.


![hello-world-v2](/GCP_pictures/Study-logs/gke-kubernetes-journey/hello-world-v2.PNG "hello world v2")


- **Kubernetes Service**: How do you ensure that external users are not impacted when:

  - A pod fails and it's replaced by replicaset

  - A new release happens and all existing pods of old release are replaced by ones of new release

  - **Service**: Services expose pods to outside world using a **stable IP address**.

  - **kubectl expose deploy DEPLOY_NAME --type=LoadBalancer --port=80**


- There are 3 types of services:

  - **ClusterIP**: Exposes service on a cluster-internal IP. You want your microservice only to be available inside the cluster (intra cluster communication).

  - **LoadBalancer**: Exposes service externally using a cloud provider's load balancer.

  - **NodePort**: Exposes service on each node's IP at a static port.



## Using Kubernetes Ingress to Provide External Access to Services

- Kubernetes Ingress are collections of rules for routing external HTTP(S) traffic to services. 


![kubernetes-ingress](/GCP_pictures/Study-logs/gke-kubernetes-journey/kubernetes-ingress.PNG "Kubernetes Ingress")


- Here's an example Ingress YAML file:


```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: gateway-ingress
spec:
  rules:
    - http:
      paths:
        - path: /currency-exchange/*
          backend:
            serviceName: currency-exchange
            servicePort: 8000
        - path: /currency-conversion/*
          backend:
            serviceName: currency-conversion
            servicePort: 8100
```