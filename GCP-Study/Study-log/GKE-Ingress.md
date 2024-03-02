### [Source of this study material : Google Kubernetes Engine with DevOps 75 Real-World Demos by Kalyan Reddy Daida](https://www.udemy.com/course/gcp-google-kubernetes-engine-gke-with-devops/?couponCode=24T4FS22124)


## Ingress Service Basics

- Before you start, you need to make sure that the GKE cluster is priavate and **HTTP Load Balancing** enabled.


![http-load-balancing-enabled](/GCP_pictures/Study-logs/gke-ingress/http-load-balancing-enabled.PNG "HTTP Load Balancing enabled")


- You also need to know about **Ingree Class**. **Ingress Class** helps the Ingress Service to associate with the respective Ingresss Controller defined in Ingress Class Value.


![ingress-sample](/GCP_pictures/Study-logs/gke-ingress/ingress-sample.PNG "Ingress sample")


- It is now **spec.ingressClassName: "gce"**. kubernetes.io/ingress.class: "gce" is now deprecated.


- Types of Ingress Class

  - **External Ingress** ("gce")

  - **Internal Ingress** ("gce-internal")

  - Multi-Cluster Ingress 

  - Third-Party Ingress (e.g. nginx)


### Ingress Basics Demo

1. We are first going to create a deployment with multiple pods.


2. Then we will front the deployment with NodePort service. **When you create a NodePort service, it includes all the nodes in the cluster.**


3. With NodePort service, when you access each of node IP addresses with a node port, it sends the traffic to the pods.


4. In this demo, we are going to use **an external Ingress service**. The **annotations** will state that it is external Ingress service.


5. In Ingress manifest, we will have **Default Backend** that has information about the NodePort service. The Ingress service will have a load balancer. 


6. Whenever a user accesses the LoadBalancer IP, the traffic will pass through **Ingress Service > Default Backend > NodePort Service > Deployment Pods**.


- **nginx app3 deployment and NodePort service YAML**


```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app3-nginx-deployment
  labels:
    app: app3-nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      app: app3-nginx
  template:
    metadata:
      labels:
        app: app3-nginx
    spec:
      containers:
        - name: app3-nginx
          image: stacksimplify/kubenginx:1.0.0
          ports:
            - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: app3-nginx-nodeport-service
  labels:
    app: app3-nginx
  annotations:
spec:
  type: NodePort
  selector:
    app: app3-nginx
  ports:
    - port: 80
      targetPort: 80
```


- **nginx app3 deployment and NodePort service YAML**


```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: ingress-basics
  annotaions:
    # If the class annotation is not specified, it defaults to "gce".
    # gce: external load balancer
    # gce-internal: internal load balancer
    spec.ingressClassName: "gce"
spec:
  defaultBackend:
    service:
      name: app3-nginx-nodeport-service
      port:
        number: 80
```


- Let's go ahead and deploy our YAML manifests.


![apply-yaml-manifests](/GCP_pictures/Study-logs/gke-ingress/apply-yaml-manifests.PNG "Apply YAML manifests")


- When you **kubectl get ingress**, you can see the IP address of the Ingress.


![kubectl-get-ingress](/GCP_pictures/Study-logs/gke-ingress/kubectl-get-ingress.PNG "kubectl get ingress")


- If you go to the IP address on the browser, the Ingress service now works.


![ingress-works](/GCP_pictures/Study-logs/gke-ingress/ingress-works.PNG "Ingress works")




## Path-based Routing Ingress Service Demo

- In this demo, we will create 3 App Deployments:

  - App 1 Deployment

  - App 2 Deployment

  - App 3 Deployment


- Also, we will create 3 NodePort services:

  - App 1 NodePort

  - App 2 NodePort

  - App 3 NodePort


- Finally, we will create an Ingress service. 


- When you access in the browser **lb-address/app1**, the request goes to App 1 NodePort service.


- When you access **lb-address/app2**, the request goes to App 2 NodePort service.


- But if you access the **root context (lb-address/)** or any other context, a.k.a **Default Backend**, your request goes to the App 3 NodePort service.


- For this, we will have 3 manifests for App1, App2, App3 Deployment and Service YAML:


- **nginx-app1-deployment-and-nodeport-service.yaml**


```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app1-nginx-deployment
  labels:
    app: app1-nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      app: app1-nginx
  template:
    metadata:
      labels:
        app: app1-nginx
    spec:
      containers:
        - name: app1-nginx
          image: stacksimplify/kube-nginxapp1:1.0.0
          ports:
            - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: app1-nginx-nodeport-service
  labels:
    app: app1-nginx
  annotations:
spec:
  type: NodePort
  selector:
    app: app1-nginx
  ports:
    - port: 80
      targetPort: 80
```


- **nginx-app2-deployment-and-nodeport-service.yaml**


```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app2-nginx-deployment
  labels:
    app: app2-nginx 
spec:
  replicas: 1
  selector:
    matchLabels:
      app: app2-nginx
  template:
    metadata:
      labels:
        app: app2-nginx
    spec:
      containers:
        - name: app2-nginx
          image: stacksimplify/kube-nginxapp2:1.0.0
          ports:
            - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: app2-nginx-nodeport-service
  labels:
    app: app2-nginx
  annotations:
spec:
  type: NodePort
  selector:
    app: app2-nginx
  ports:
    - port: 80
      targetPort: 80

```


- **nginx-app3-deployment-and-nodeport-service.yaml**


```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app3-nginx-deployment
  labels:
    app: app3-nginx 
spec:
  replicas: 1
  selector:
    matchLabels:
      app: app3-nginx
  template:
    metadata:
      labels:
        app: app3-nginx
    spec:
      containers:
        - name: app3-nginx
          image: stacksimplify/kubenginx:1.0.0
          ports:
            - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: app3-nginx-nodeport-service
  labels:
    app: app3-nginx
  annotations:
spec:
  type: NodePort
  selector:
    app: app3-nginx
  ports:
    - port: 80
      targetPort: 80
```


- **Ingress-ContextPath-Based-Rounting.yaml**


```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: ingress-cpr
  annotations:
    # External Load Balancer  
    spec.ingressClassName: "gce"  
spec: 
  defaultBackend:
    service:
      name: app3-nginx-nodeport-service
      port:
        number: 80                            
  rules:
    - http:
        paths:           
          - path: /app1
            pathType: Prefix
            backend:
              service:
                name: app1-nginx-nodeport-service
                port: 
                  number: 80
          - path: /app2
            pathType: Prefix
            backend:
              service:
                name: app2-nginx-nodeport-service
                port: 
                  number: 80
#          - path: /
#            pathType: Prefix
#            backend:
#              service:
#                name: app3-nginx-nodeport-service
#                port: 
#                  number: 80                     
             
```


- Now, let's deploy our YAML manifests.


```
kubectl apply -f kube-manifests/
```


![apply-all-manifests](/GCP_pictures/Study-logs/gke-ingress/apply-all-manifests.PNG "Apply all manifests")



- And when you go to the original Ingress IP, :80/app1, and :80/app2, all the cases work.


![default-path](/GCP_pictures/Study-logs/gke-ingress/default-path.PNG "Default path")


![app1-path](/GCP_pictures/Study-logs/gke-ingress/app1-path.PNG "App1 path")


![app2-path](/GCP_pictures/Study-logs/gke-ingress/app2-path.PNG "App2 path")



- If you go to Load Balancing section on GCP and check, it also shows the path rules we configured in Ingress manifest:


![path-rules](/GCP_pictures/Study-logs/gke-ingress/path-rules.PNG "Path rules")