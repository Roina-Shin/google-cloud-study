### [Source of this study material : Google Kubernetes Engine with DevOps 75 Real-World Demos by Kalyan Reddy Daida](https://www.udemy.com/course/gcp-google-kubernetes-engine-gke-with-devops/?couponCode=24T4FS22124)


## Kubernetes Service Introduction

- In Kubernetes, services are of multiple types:

  - **CluterIP** service

  - **NodePort** service

  - **Headless** service

  - **LoadBalancer** service

  - **ExternalName** service

  - **Ingress** service


### CluterIP service

- ClusterIP service is used for **internal communication** between applications inside kubernetes cluster with a stable internal IP.


### NodePort service

- Clients send requests to the IP address of a **worker node on** one or more NodePort values that are specified by the service.


### Ingress service

- Ingress is an advanced load balancer which provides context path based routing, SSL, SSL redirect and many more which operate at HTTP layer 7.


### LoadBalancer service

- Primarily for cloud providers to integrate with their load balancers.


### ExternalName service

- Internal clients use the DNS name of a service as an alias for an external DNS name.


### Headless service

- It is used for discovering individual pods (especially pod IPs) which allow another service to interact directly with the pods instead of a proxy.



## Kubernetes ClusterIP and Load Balancer service Demo

- For this demo, we will first create a deployment for the backend application (Spring Boot REST application).


- Then create a clusterIP service for load balancing backend application.


```
kubectl create deployment my-backend-rest-app --image=stacksimplify/kube-helloworld:1.0.0
```


![deployment-creation](/GCP_pictures/Study-logs/gke-clusterIP-LoadBalancer/deployment-creation.PNG "Deployment creation")


- Now, you need to expose this deployment as a service.


```
kubectl expose deployment my-backend-rest-app --port=8080 --target-port=8080 --name=my-backend-service
```


- So, the clusterIP service port (--port) is 8080 and the backend application port a.k.a **container port** (--target-port) is also 8080.


- Also, we **didn't specify --type=ClusterIp** because default setting is to create ClusterIP.


![expose-deployment](/GCP_pictures/Study-logs/gke-clusterIP-LoadBalancer/expose-deployment.PNG "Expose deployment as a service")


- Now, we are going to deploy the frontend **LoadBalancer** service in relation with **ClusterIP** service.


- We will create a **deployment** for frontend application which is **nginx acting as a reverse proxy**.


- And then, create a **LoadBalancer** service for load balancing frontend application.


- In nginx reverse proxy, ensure that the backend service name is **my-backend-service** when you are building a frontend container.


- So first, we will create a deployment for the frontend nginx proxy.


```
kubectl create deployment my-frontend-nginx-app --image=stacksimplify/kube-frontend-nginx:1.0.0
```


![creating-frontend-deploy](/GCP_pictures/Study-logs/gke-clusterIP-LoadBalancer/creating-frontend.PNG "Creating frontend deployment")


- And expose this deployment as a LoadBalancer service:


```
kubectl expose deployment my-frontend-nginx-app --type=LoadBalancer --port=80 --target-port=80 --name=my-frontend-service
```


![expose-deployment-as-loadbalancer](/GCP_pictures/Study-logs/gke-clusterIP-LoadBalancer/expose-deployment-loadbalancer.PNG "Expose deployment as a LoadBalancer service")


- And if you go to the http://[external IP of service]/hello, you will see the output.


![service-output](/GCP_pictures/Study-logs/gke-clusterIP-LoadBalancer/ip-output.PNG "Service output")


- You can scale your deployment by:


```
kubectl scale --replicas=2 deployment/my-backend-rest-app
```


![scale-replicas](/GCP_pictures/Study-logs/gke-clusterIP-LoadBalancer/scale-replicas.PNG "Scale replicas")


- Then the ClusterIP service will load balance between the scaled 2 pods.


![loadbalancing-pod1](/GCP_pictures/Study-logs/gke-clusterIP-LoadBalancer/loadbalancing-pod1.PNG "Loadbalancing pod1")


![loadbalancing-pod2](/GCP_pictures/Study-logs/gke-clusterIP-LoadBalancer/loadbalancing-pod2.PNG "Loadbalancing pod2")



## YAML Basics

- We can use YAML to define **key-value** pairs like variables, lists, and object.


- YAML is very similar to JSON (Javascript Object Notation)


- YAML primarily focuses on **readability** and **user friendliness**.


- Comment in YAML


```
# Sample Key Value Pairs
```


- Key-Value pair in YAML


```
name: yejin
age: 35
city: Incheon
```


- Dictionary in YAML


```
Person:
  name: yejin
  age: 35
  city: Incheon
```


- List in YAML


```
Person:
  name: yejin
  age: 35
  city: Incheon
  hobby:
    - cooking
    - drawing
    - Internet browse
```


- You can also use list in YAML


```
Person:
  name: yejin
  age: 35
  city: Incheon
  hobby: [cycling, drawing, cooking] # Another notation for list
```


- Multiple list in YAML


```
Person:
  name: yejin
  age: 35
  city: Incheon
  hobby:
    - cooking
    - drawing
    - Internet browse
  friends: # Multiple list
    - name: minkyung
      age: 30
    - name: youngja
      age: 33
```


- YAML separator is 3 dashes: **---**


- Sample YAML:


```
apiVersion: v1 
kind: Pod  
metadata: 
  name: myapp-pod
  labels: 
    app: myapp         
spec:
  containers: 
    - name: myapp
      image: stacksimplify/kubenginx:1.0.0
      ports: 
        - containerPort: 80
          protocol: "TCP"
        - containerPort: 81
          protocol: "TCP"
```


## Create a simple pod using YAML file

### Understanding the Kubernetes YAML Top Level Obejcts


```
apiVersion:
kind:
metadata:

spec:

# apiVersion: version of kubernetes objects
# kind: kubernetes object (e.g. pod, service)
# metadata: define name and labels for kubernetes objects
# spec: specification or definition for kubernetes objects
```


- The 4 (apiVersion, kind, metadata, spec) will be the most common Kubernetes objects.


- When you write a Kubernetes YAML file, see the links below:


![Kubernetes reference](https://kubernetes.io/docs/reference/)


![Kubernetes API reference](https://kubernetes.io/docs/reference/kubernetes-api/)


- Write a sample YAML file for creating a simple pod:


```
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
  labels: 
    app: myapp
spec:
  containers:
    - name: myapp
      image: stacksimplify/kubenginx:1.0.0
      ports:
        - containerPort: 80
```


- Save the YAML file and upload it to the cloud shell. Then run:


```
kubectl apply -f pod-spec.yaml
```


![create-pod-using-yaml](/GCP_pictures/Study-logs/gke-clusterIP-LoadBalancer/create-pod.PNG "Create a pod using YAML")


- Now, we will create a load balancer using YAML and test it.


```
apiVersion: v1
kind: Service
metadata:
  name: myapp-pod-loadbalancer-service
spec:
  type: LoadBalancer
  selector: 
    app: myapp
  ports:
    - name: http
      port: 80 # Service port
      targetPort: 80 # Container port
```


- When creating a service YAML, it is **VERY IMPORTANT** to specify the **selector**. Selector will send the traffic to the pods with the **matching labels**.


- Then create a service using the YAML file:


```
kubectl apply -f service.yaml
```


![create-service](/GCP_pictures/Study-logs/gke-clusterIP-LoadBalancer/create-service.PNG "Create service using YAML")


- And when you go to the external IP of the load balancer, you can access the service.


![loadbalancer-access](/GCP_pictures/Study-logs/gke-clusterIP-LoadBalancer/loadbalancer-front.PNG "Loadbalancer service access")



## Create a ReplicaSet using YAML file

- We are going to create a replicaset definition YAML file.


- Using the ![Kubernetes API](https://kubernetes.io/docs/reference/kubernetes-api/workload-resources/replica-set-v1/) website, formulate a YAML file.


```
apiVersion: apps/v1
kind: ReplicaSet
metadata: 
  name: myapp2-rs 
spec:
  replicas: 2
  selector:
    matchLabels:
      app: myapp2
  template:
    metadata:
      name: myapp2-pod
      labels:
        app: myapp2
    spec:
      containers:
        - name: myapp2-container
          image: stacksimplify/kubenginx:2.0.0
          ports:
            - containerPort: 80
```

- The **selector in spec** specifies matchLabels ({key, value} pairs) as a label selector. The pair of **app: myapp2** will be used by the LoadBalancer service to route traffic to the respective pods with the same labels.


- Then create a ReplicaSet using the YAML file.


![replicaset-file](/GCP_pictures/Study-logs/gke-clusterIP-LoadBalancer/replicaset-file-apply.PNG "ReplicaSet file apply")


- If you delete a pod, the **replicaset** immediately recreates a pod in place of the deleted pod.


- Now, we will create a LoadBalancer service for the replicaset.


```
apiVersion: v1
kind: Service
metadata:
  name: replicaset-loadbalancer-service
spec:
  type: LoadBalancer
  selector:
    app: myapp2
  ports:
    - name: http
      port: 80
      targetPort: 80
```


- Let's create the LoadBalancer service:


```
kubectl apply -f rs-lb-service.yaml
```


![rs-lb-service-created](/GCP_pictures/Study-logs/gke-clusterIP-LoadBalancer/rs-lb-service-created.PNG "ReplicaSet LoadBalancer service created")



## Create a Deployment using YAML and Test

- To create a deployment YAML file, you can refer to your replicaset YAML file as it is quite similar.


- Let's create a deployment YAML file:


```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp3-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: myapp3
  template:
    metadata:
      name: myapp3-pod
      labels:
        app: myapp3
    spec:
      containers:
        - name: myapp3-container
          image: stacksimplify/kubenginx:3.0.0
          ports:
            - containerPort: 80
```


- Also, create a LoadBalancer service for the deployment:


```
apiVersion: v1
kind: Service
metadata:
  name: deployment-loadbalancer-service
spec:
  type: LoadBalancer
  selector:
    app: myapp3
  ports:
    - name: http
      port: 80
      targetPort: 80
```


- Now, if you create the service and verify it, you can see it's working.


![external-ip](/GCP_pictures/Study-logs/gke-clusterIP-LoadBalancer/external-ip.PNG "External IP of LoadBalancer")


![loadbalancer-working](/GCP_pictures/Study-logs/gke-clusterIP-LoadBalancer/loadbalancer-working.PNG "LoadBalancer working")



## Create ClusterIP service for Backend and LoadBalancer service for Frontend

- For this demo, we will create a backend app using Spring Boot deployment and then create a ClusterIP service for the backend app.


- Once done, we will create a frontend app using nginx deployment and then create a LoadBalancer service for the frontend app.


- We will create 4 files:

  - backend deployment YAML

  - backend clusterIP YAML

  - frontend deployment YAML

  - frontend LoadBalancer YAML


- **Backend deployment YAML**


```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: backend-restapp
  labels:
    app: backend-restapp
    tier: backend
spec:
  replicas: 3
  selector:
    matchLabels:
      app: backend-restapp
  template:
    metadata:
      labels:
        app: backend-restapp
        tier: backend
    spec:
      containers:
        - name: backend-restapp
          image: stacksimplify/kube-helloworld:1.0.0
          ports:
            - containerPort: 8080
```


- **Backend service YAML**


```
apiVersion: v1
kind: Service
metadata:
  name: my-backend-service
  labels:
    app: backend-restapp
    tier: backend
spec:
  type: ClusterIP # We don't need to specify ClusterIP as it's default service
  selector:
    app: backend-restapp
  ports:
    - name: http
      port: 8080
      targetPort: 8080
```

- **Frontend deployment YAML**


```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: frontend-nginxapp
  labels:
    app: frontend-nginxapp
    tier: frontend
spec:
  replicas: 3
  selector:
    matchLabels:
      app: frontend-nginxapp
  template:
    metadata:
      labels:
        app: frontend-nginxapp
        tier: frontend
    spec:
      containers:
        - name: frontend-nginxapp
          image: stacksimplify/kube-frontend:1.0.0
          ports:
            - containerPort: 80
```


- **Frontend service YAML**


```
apiVersion: v1
kind: Service
metadata:
  name: frontend-nginx-loadbalancer-service
  labels:
    app: frontend-nginxapp
    tier: frontend
spec:
  type: LoadBalancer
  selector:
    app: frontend-nginxapp
  ports:
    - name: http
      port: 80
      targetPort: 80
```


- Now, we can go ahead and deploy the backend deployment and service:


```
kubectl apply -f backend-deployment.yaml -f backend-service.yaml
```


![2-yaml-for-backend](/GCP_pictures/Study-logs/gke-clusterIP-LoadBalancer/2-yaml-for-backend.PNG "2 YAML for backend")


- This time, we will create a frontend deployment and service:


```
kubectl apply -f frontend-deployment.yaml -f frontend-service.yaml
```


![2-yaml-for-frontend](/GCP_pictures/Study-logs/gke-clusterIP-LoadBalancer/2-yaml-for-frontend.PNG "2 YAML for frontend")


- If you verify the external IP of the load balancer, you will see that it distributes the traffic across 3 pods.


![lb-1](/GCP_pictures/Study-logs/gke-clusterIP-LoadBalancer/lb-1.PNG "lb-1")


![lb-2](/GCP_pictures/Study-logs/gke-clusterIP-LoadBalancer/lb-2.PNG "lb-2")


![lb-3](/GCP_pictures/Study-logs/gke-clusterIP-LoadBalancer/lb-3.PNG "lb-3")



## Kubernetes NodePort service

- NodePort service **allows external clients** to access pods via network ports opened on the Kubernetes nodes.


- If your GKE cluster is **public cluster**, then your cluster nodes are **Internet accessible**.


- If you run **kubectl get nodes**, you will see that the nodes have external IPs. (as it's public cluster)


![nodeport-external-ip](/GCP_pictures/Study-logs/gke-clusterIP-LoadBalancer/nodeport-external-ip.PNG "NodePort external IPs")


- NodePort range is **30000 - 32768** on Kubernetes Nodes.


- In real world, NodePort services are not used in production grade implementations.


- NodePort services are generally used to **test our application by external clients** via Internet provided it is a public cluster.


- With NodePort service, the node external IP and the allocated port is fronting your application.


- NodePort is generally not a recommended practice to use in production for our application.


- But for **testing purposes**, NodePort service is very helpful.



### Kubernetes NodePort service demo

- In this demo, we will create a simple myapp1 deployment in the default namespace in GKE Cluster. 


- Then we will front it with the **NodePort** service.


- Then as a user, I'm going to take any of the node external IPs with a node port (e.g. http://34.27.64.117:32768") and access the node port service (port 80) and access my application.


- So for this demo, we will need 2 YAML files:

- **nodeport-deployment.yaml**


```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp1-deployment
spec:
  replicas: 2
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
```


- **nodeport-service.yaml**


```
apiVersion: v1
kind: Service
metadata:
  name: myapp1-nodeport-service
spec:
  type: NodePort
  selector:
    app: myapp1
  ports:
    - name: http
      port: 80
      targetPort: 80
      nodePort: 32700 # Node Port Range: 30000 - 32768
```


- If tou don't commend the **nodePort** in the nodePort service YAML file, it will automatically create the node port from **30000 to 32768**.


- Now, we will deploy these 2 YAML files:


```
kubectl apply -f nodeport-deployment.yaml -f nodeport-service.yaml
```


- You will see that we don't have **an external IP** for the **NodePort** service. We will have the external IPs for the nodes, not from the NodePort service.


![no-external-ip-for-service](/GCP_pictures/Study-logs/gke-clusterIP-LoadBalancer/no-external-ip.PNG "No external IP for NodePort service")


- We will access the node external IPs by running **kubectl get nodes -o wide**.


![node-external-ip](/GCP_pictures/Study-logs/gke-clusterIP-LoadBalancer/node-external-ip.PNG "Node external IP")



- If you access one of the node external IP, it **fails**. It is because there is **no firewall rule in place for the node port 32700**.


- You can run this to check the firewall rules:


```
gcloud compute firewall-rules list
```


![gcloud-compute-firewall](/GCP_pictures/Study-logs/gke-clusterIP-LoadBalancer/gcloud-compute-firewall.PNG "gcloud compute firewall-rules")



- You can create the firewall rules by running this command:


```
gcloud compute firewall-rules create default-allow-gke-nodeport --allow tcp:32700
```


![firewall-rule-created](/GCP_pictures/Study-logs/gke-clusterIP-LoadBalancer/firewall-rule-created.PNG "Firewall rule created")


- If you access each of the node external IP addresses with the node port (32700), you can now access the application.


![nodeport-1](/GCP_pictures/Study-logs/gke-clusterIP-LoadBalancer/nodeport-1.PNG "nodeport 1")


![nodeport-2](/GCP_pictures/Study-logs/gke-clusterIP-LoadBalancer/nodeport-2.PNG "nodeport 2")


![nodeport-3](/GCP_pictures/Study-logs/gke-clusterIP-LoadBalancer/nodeport-3.PNG "nodeport 3")


- After done with the demo, you can delete the firewall rules by:


```
gcloud compute firewall-rules delete [firewall rule name] 
```


![firewall-rule-deleted](/GCP_pictures/Study-logs/gke-clusterIP-LoadBalancer/firewall-rule-deleted.PNG "Firewall rule deleted")


- In summary, the NodePort service has several nodes (zonal resources e.g. us-central1-a, us-central1-b) all of which have the same node port (e.g. 32768) and the user traffic goes through this node port and to the **NodePort** service where the service port is 80. And through the NodePort service, the traffic is distributed to the target container ports of the pods which are 80 in the deployment.



## Kubernetes Headless service

- In **headless service**, we should use both the **Service Port** and the **Target Port** same.


```
apiVersion: v1
kind: Service
metadata:
  name: myapp1-headless-service
spec:
  clusterIP: None
  selector:
    app: myapp1
  ports:
    - name: http
      port: 8080
      targetPort: 8080
```

- Also, you should provide **ClusterIP: None** in the spec.


- Headless service **directly sends traffic** to the pod with **pod IP and Container Port**.


- DNS resolution directly happens from headless service to **pod IP**.


- Finally, we cannot connect to ClusterIP services directly from Internet to test headless service concept.





