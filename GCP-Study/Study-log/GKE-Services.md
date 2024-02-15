### [Source of this study material : GKE The Practical Guide by Shikhar Verma](https://www.udemy.com/course/google-gke/)


## GKE Service - Cluster IP


- First, prepare this yaml file:


```
kind: Deployment
apiVersion: apps/v1
metadata:
   name: mydeployments
spec:
   replicas: 1
   selector:     
    matchLabels:
     name: deployment
   template:
     metadata:
       labels:
         name: deployment
     spec:
      containers:
        - name: c00
          image: nginx:alpine
          ports:
            - containerPort: 80
```


- Go to Cloud Shell and connect with your cluster:


```
gcloud container clusters get-credentials autopilot-cluster-1 --region us-central1 --project storied-polymer-406703
```


- Then deploy your file:


```
kubectl apply -f pod1.yaml
```


![clusterip-yaml](/GCP_pictures/Study-logs/GKE-3/clusterip-yaml.PNG "ClusterIP yaml")



- Run the commands to verify deployment, pods, and details:


```
kubectl get deploy
```

```
kubectl get pods
```

```
kubectl get pods -o wide
```

- In details, we can see the pod's IP address that is running on port 80.


![pod-address](/GCP_pictures/Study-logs/GKE-3/pod-ip-address.PNG "Pod IP address")


- But the problem can arise when the pod is crashed or restarted, the IP address also changes. To resolve this, we can use the **service objects**.


- To use **ClusterIP** service, we need the below file:


```
apiVersion: v1
kind: Service
metadata:
  name: web-cip
spec:
  selector:
    name: deployment
  ports:
  - protocol: TCP
    port: 8080
    targetPort: 80
  type: ClusterIP
```


- Run this to see the existing pod has the same **selector** as above:

```
kubectl get pods --show-labels
```


![pod-labels](/GCP_pictures/Study-logs/GKE-3/pod-labels.PNG "Pod labels")



- **ClusterIP is an excellent choice for internal communication** for different components of application.


- Now, apply the service:


```
kubectl apply -f pod-service-cip.yaml
```


- And verify the service:


```
kubectl get svc
```


![verify-svc](/GCP_pictures/Study-logs/GKE-3/get-svc.PNG "Get svc")



- When you use **kubectl describe svc/web-cip**, you can see that the service already took our existing pod's IP as its endpoints with the help of "name: deployment" selector. 


![describe-svc](/GCP_pictures/Study-logs/GKE-3/describe-svc.PNG "Describe svc")


- Now, if you deleted the pod and fired the commands again, you will see that the service enpoints is a new pod's IP address.


![pod-delete](/GCP_pictures/Study-logs/GKE-3/pod-delete.PNG "New pod IP is assigned to the service")



## GKE Service - NodePort


- **NodePort** extends the functionality of ClusterIP service by enabling external connectivity to our application.

- Suppose I have an application. To access my application within the cluster, I can use the ClusterIP. But if I want to expose my application to the external world as well, then I can use the NodePort.

- With the **NodePort**, you can access the application within the cluster as well as from the outside.


- To deploy this service, you can use the file:

```
apiVersion: v1
kind: Service
metadata:
  name: web-cip
spec:
  selector:
    name: deployment
  ports:
  - protocol: TCP
    port: 8080
    targetPort: 80
    nodePort: 31088
  type: NodePort
```

- Here, the NodePort uses the range **30000-32767**.


- Port 8080 is used to communicate with your nginx server **within the cluster**.

- Port 31088 is for the **connectivity with the outside**.


- Run the command to see the external IP of node:


```
kubectl get nodes -o wide
```


![external-ip](/GCP_pictures/Study-logs/GKE-3/external-ip.PNG "External IP of node")


- NodePort differs from ClusterIP in the sense that **it exposes port on each node**. So, if you try to access your web application from any of the nodes, the same port will be working.


- But when we try to access with the external IP and port number, we cannot access it. It's because of the firewall rule. 


![cannot-access](/GCP_pictures/Study-logs/GKE-3/cannot-access.PNG "Cannot access")



- We have to create a **firewall rule** that adds a specific port (31088).


- The command is:


```
gcloud compute firewall-rules create default-nodeport-allow --allow tcp:31088
```


- If you go back to the browser and refresh it, you are able to access it:


![firewall-resolved](/GCP_pictures/Study-logs/GKE-3/firewall-resolved.PNG "Firwall resolved")




## GKE Service - LoadBalancer


- LoadBalancer distributes traffic evenly through the pods.

- To test this, we need 3 files:


```
apiVersion: v1
kind: Pod
metadata:
  name: webserver-v1
  labels:
    app: nginxweb
    type: production
    ver: v1
spec:
  containers:
  - name: web
    image: nginx:alpine
    ports:
    - containerPort: 80
```

```
apiVersion: v1
kind: Pod
metadata:
  name: webserver-v2
  labels:
    app: nginxweb
    type: production
    ver: v2
spec:
  containers:
  - name: web
    image: nginx:alpine
    ports:
    - containerPort: 80
```

```
apiVersion: v1
kind: Pod
metadata:
  name: webserver-v3
  labels:
    app: nginxweb
    type: production
    ver: v3
spec:
  containers:
  - name: web
    image: nginx:alpine
    ports:
    - containerPort: 80
```


- Now, deploy all pods by running:


```
kubectl apply -f pod1.yaml
```

```
kubectl apply -f pod2.yaml
```

```
kubectl apply -f pod3.yaml
```

- Verify the pods:


```
kubectl get pods
```

- In my case, only 2 pods are running:


![only-2-pods](/GCP_pictures/Study-logs/GKE-3/only-2-pods.PNG "Only 2 pods running")


- Now, we are going to SSH into each pod and change the HTML file so that we can test the LoadBalancer:


```
kubectl exec [pod name] -it -- /bin/sh
```

- Go inside the directory:


```
cd /usr/share/nginx/html
```

- Then go inside the index.html and modify like below:


![nginx-v1](/GCP_pictures/Study-logs/GKE-3/nginx-v1.PNG "Nginx version1")


- Do the same thing on the other pod as well.


- Now, create a service file like below:


```
apiVersion: v1
kind: Service
metadata:
  name: web-lb
spec:
  selector:
    app: nginxweb
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
  type: LoadBalancer
```


- This time, again, we defined the selector **app: nginxweb** where all 2 pods have been labeled as well. So it will automatically apply to the 2 pods:


![pods-labels](/GCP_pictures/Study-logs/GKE-3/pod-labels.PNG "Pods labels")



- Then, apply your service.yaml file and verify it:


```
kubectl apply -f service.yaml
```

```
kubectl get svc
```


![ip-pending](/GCP_pictures/Study-logs/GKE-3/ip-pending.PNG "IP address pending")



- The external IP address is still pending. It will take some time. You can access your application through this IP. And this IP will handle the traffic for the 2 pods. It will first forward the traffic to the Cluster IP and from that it is going to distribute the traffic evenly to all the pods.


- Now, I've got the external IP.


![got-IP](/GCP_pictures/Study-logs/GKE-3/got-ip.PNG "got IP!")



- And simply grab the IP and open it in the browser:


![working-v1](/GCP_pictures/Study-logs/GKE-3/working-v1.PNG "Working V1")


![working-v3](/GCP_pictures/Study-logs/GKE-3/working-v3.PNG "Working V3")


- With the help of this LoadBalancer, I can distribute the traffic among the 2 pods!


