### [Source of this study material : Google Kubernetes Engine with DevOps 75 Real-World Demos by Kalyan Reddy Daida](https://www.udemy.com/course/gcp-google-kubernetes-engine-gke-with-devops/?couponCode=24T4FS22124)


## GKE Autopilot Cluster

- When we create a cluster in GKE, we have 2 options:

  - **Autopilot mode**

  - **Standard mode**


- Autopilot Cluster is for non-technical users who want the minimum configurations on their side.


- Autopilot reduces platform administration overhead by removing need to continuously monitor nodes and to scale and schedule operations.


- Once the **autopilot cluster** is created, and if we don't deploy any workload, we can observe after some time that the number of nodes, total vCPUs and total memory all will come to zero.



## GKE Autopilot Cluster Demo

- Now, let's create an autopilot cluster.


![autopilot-cluster-creation](/GCP_pictures/Study-logs/gke-autopilot-cluster/autopilot-cluster-creation.PNG "Autopilot cluster creation")


- In Networking section, choose the custom VPC and the us-central1 region. Also, choose private cluster.


![cluster-networking](/GCP_pictures/Study-logs/gke-autopilot-cluster/cluster-networking.PNG "Cluster networking")


- Provide the **Control Plane IP Range**. As recommended there is **172.16.0.0/28** IP range. But make sure your other clusters don't use the same IP range as your new autopilot cluster. If overlapped, use the different one.


![control-plane-ip-range](/GCP_pictures/Study-logs/gke-autopilot-cluster/control-plane-ip-range.PNG "Control plane IP range")


- Now, review the configurations of the private autopilot cluster and click create.


![cluster-creation-review](/GCP_pictures/Study-logs/gke-autopilot-cluster/cluster-creation-review.PNG "Cluster creation review")


- Open the cloud shell and connect with the cluster:


```
gcloud container clusters get-credentials autopilot-cluster-private-1 --region us-central1 --project my-vpn-router-project
```


![cluster-get-credentials](/GCP_pictures/Study-logs/gke-autopilot-cluster/cluster-get-credentials.PNG "Cluster get credentials")


- Now, we are going to create a deployment and loadbalancer service in the autopilot cluster.


- **autopilot-deployment.yaml**


```
apiVersion: apps/v1
kind: Deployment 
metadata: 
  name: myapp1-deployment
spec: 
  replicas: 5 
  selector:
    matchLabels:
      app: myapp1
  template:  
    metadata: 
      name: myapp1-pod
      labels: 
        app: myapp1  
    spec:
      containers: 
        - name: myapp1-container
          image: stacksimplify/kubenginx:1.0.0
          ports: 
            - containerPort: 80  
          resources:
            requests:
              memory: "128Mi" # 128 MebiByte is equal to 135 Megabyte (MB)
              cpu: "200m" # `m` means milliCPU
            limits:
              memory: "256Mi"
              cpu: "400m"  # 1000m is equal to 1 VCPU core                                               
```


- **autopilot-service.yaml**


```
apiVersion: v1
kind: Service 
metadata:
  name: myapp1-lb-service
spec:
  type: LoadBalancer # ClusterIp, # NodePort
  selector:
    app: myapp1
  ports: 
    - name: http
      port: 80 # Service Port
      targetPort: 80 # Container Port
```


- Upload these files to the cloud shell and run the command:


```
kubectl apply -f autopilot-deployment.yaml -f autopilot-service.yaml
```


- When an autopilot cluster is created, there are no nodes if you run **kubectl get nodes**. In a standard cluster, you will see some nodes running when you created the cluster. To create nodes, you **first need to create a deployment and service**. 


- Then run **kubectl get nodes** and **kubectl get pods**.


![kubectl-get-nodes](/GCP_pictures/Study-logs/gke-autopilot-cluster/kubectl-get-nodes.PNG "kubectl get nodes")


- Also, run **kubectl get svc** and see the external IP of your loadbalancer service.


![loadbalancer-external-ip](/GCP_pictures/Study-logs/gke-autopilot-cluster/loadbalancer-external-ip.PNG "LoadBalancer external IP")


- If you scale your deployment to 10 pods, you will see that the number of nodes are automatically scaled:


```
kubectl scale --replicas=10 deployment/myapp1-deployment
```


![scale-deployment-nodes-increased](/GCP_pictures/Study-logs/gke-autopilot-cluster/scale-deployment-nodes-increased.PNG "Scale out deployment and nodes are scaled out")



## Access to Multiple Clusters with kubectl config command

- Think of a situation where you have multiple clusters running.


- As an admin, you are using kubectl to access the cluster resources.


- Now, you have 2 kubectl commands to configure access to multiple clusters:

  - **kubectl config current-context**

    - View the current context for kubectl

  - **kubectl config use-context context-name**

    - Switch context


- We have 2 clusters now:

  - standard-cluster-private-1

  - autopilot-cluster-private-1


- Now, we will **clean up the kube config file** which is the credential file that has the access information.


```
cd $HOME/.kube
```

- In my **HOME** directory, go to **.kube** folder.


- Then run **cat config** to see the inside of config file.


![cd-home-kube](/GCP_pictures/Study-logs/gke-autopilot-cluster/cd-home-kube.PNG "cd $HOME/.kube")


- So this **config** file is this: whenever you run **get-credentials** command, all the cluster information is stored in this file.


![get-credentials](/GCP_pictures/Study-logs/gke-autopilot-cluster/get-credentials.PNG "cluster get-credentials")


- Now, we will clear everything in this config file by running:


```
>config
```


- Then, everything in the file will be cleared out.


![clear-config](/GCP_pictures/Study-logs/gke-autopilot-cluster/clear-config.PNG "Clear config file")


- Now, if we run **kubectl config view**, it will get the information of the present config file in **.kube** folder.


![kubectl-config-view](/GCP_pictures/Study-logs/gke-autopilot-cluster/kubectl-config-view.PNG "kubectl config view")


- This time, run the command to get credentials for the **standard cluster**.


```
gcloud container clusters get-credentials standard-cluster-private-1 --region us-central1 --project my-vpn-router-project
```


- Then if run the **cat config** again, you will see that the current context is the standard cluster.


![current-context](/GCP_pictures/Study-logs/gke-autopilot-cluster/current-context.PNG "Current context")


- Now, it is **VERY VERY IMPORTANT** to run when you have multiple clusters. 


```
kubectl config current-context
```


- Before you deploy anything in the cluster, it's recommended to verify which context you are in first.


![kubectl-config-current-context](/GCP_pictures/Study-logs/gke-autopilot-cluster/kubectl-config-current-context.PNG "kubectl config current-context")


- It shows very clearly which cluster I'm in.


- Now, we will **configure the autopilot cluster access** for kubectl.


- To do this, we first need to get credentials for the autopilot cluster.


```
gcloud container clusters get-credentials autopilot-cluster-private-1 --region us-central1 --project my-vpn-router-project
```


- With this, the current context is now switched from **standard** to **autopilot**.


![standard-to-autopilot](/GCP_pictures/Study-logs/gke-autopilot-cluster/autopilot-cluster-context.PNG "Autopilot cluster -current context")


- If you run **kubectl config view** again, you will see that the 2 cluster information is now present in the config file.


![kubectl-config-view](/GCP_pictures/Study-logs/gke-autopilot-cluster/kubectl-config-view-again.PNG "kubectl config view")


- Now to **★★★★switch the context from autopilot cluster to standard cluster★★★★**, run this:


```
kubectl config use-context [context name]
```


![kubectl-config-use-context](/GCP_pictures/Study-logs/gke-autopilot-cluster/kubectl-config-use-context.PNG "kubectl config use-context")


- If you run **kubectl get nodes**, you will see that the 3 nodes related to the standard cluster are running:


![kubectl-get-nodes](/GCP_pictures/Study-logs/gke-autopilot-cluster/kubectl-get-nodes-again.PNG "kubectl get nodes")


- To see the configured clusters(contexts), you can run **kubectl config get-contexts**.


![kubectl-config-get-contexts](/GCP_pictures/Study-logs/gke-autopilot-cluster/kubectl-config-get-contexts.PNG "kubectl config get-contexts")


- This command will also do a similar thing, but as the name implies, it will get the clusters instead of contexts.


```
kubectl config get-clusters
```

![kubectl-config-get-clusters](/GCP_pictures/Study-logs/gke-autopilot-cluster/kubectl-config-get-clusters.PNG "kubectl config get-clusters")