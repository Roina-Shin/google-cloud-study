### [Source of this study material : Google Kubernetes Engine with DevOps 75 Real-World Demos by Kalyan Reddy Daida](https://www.udemy.com/course/gcp-google-kubernetes-engine-gke-with-devops/?couponCode=24T4FS22124)


## Kubernetes Horizontal Pod Autoscaler

- Horizontal scaling means increasing and decreasing the number of replicas (pods).


- HPA automatically scales the number of pods on a deployment, replication controller, or replicaset, stateful set based on that resources' CPU and memory metrics.


- This can help our applications **scale out** to meet increased demand or **scale in** when resources are not needed, thus freeing up your worker nodes for other applications.


- When we set a **target CPU utilization percentage**, the HPA scales our application in and out to try to meet that target.


- HPA needs **Kubernetes metrics server** to verify CPU metrics of a pod. **Metrics server** is by default installed in GKE cluster.


- We **do not need to deploy or install the HPA** on our cluster to begin scaling our applications, as it is **out of the box available** as a default Kubernetes API resource.


### Kubernetes Metrics Server

- Metrics server collects resource metrics from kubelets and exposes them in Kubernetes apiserver through **Metrics API** for use by **Horizontal Pod Autoscaler** and **Vertical Pod Autoscaler**.


- Metrics API can also be accessed by **kubectl top**, making it easier to debug autoscaling pipelines.


- Metrics server is not meant for non-autoscaling purposes. For example, **don't use it to forward metrics to monitoring solutions**. Metrics server is for Kubernetes autoscaling purposes only.


- So, when we create a cluster in GKE, we have a namespace called **kube-system** by default.


![kube-system-as-namespace](/GCP_pictures/Study-logs/GKE-horizontal-pod-autoscaler/kube-system-as-namespace.PNG "Kube system as namespace")


- In real-world scenario, we deploy an application in the **default namespace** by creating a deployment with 2 pods. And you also deploy a **horizontal pod autoscaler** for this respective application. So, the HPA will have the reference to this application in the **default namespace**. 


- This horizontal pod autoscaler will make a query for metrics **every 15 seconds** for this application to the **metrics server in kube-system namespace**.


- If the metrics data sent by the metrics server is above the CPU limit, the HPA will scale the app to desired replicas.


- HPA requires:

  - Scaling metric: CPU utilization

  - Target Value (CPU = 50%)

  - Min replicas = 2

  - Max replicas = 10

  - Scaling target reference (e.g. Deployment, ReplicaSet, StatefulSet)


### Sample Horizontal Pod Autoscaler YAML Manifest


```
apiVersion: autoscaling/v1
kind: HorizontalPodAutoscaler
metadata:
  name: hap-myapp1
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: myapp1-deployment
  minReplicas: 1
  maxReplicas: 10
  targetCPUUtilizationPercentage: 50
```


## Kubernetes Horizontal Pod Autoscaler Demo

- **kubernetes-deployment.yaml**


```
apiVersion: apps/v1
kind: Deployment 
metadata: 
  name: myapp1-deployment
spec: 
  replicas: 1
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
              memory: "5Mi" # 128 MebiByte is equal to 135 Megabyte (MB)
              cpu: "5m" # `m` means milliCPU
            limits:
              memory: "50Mi"
              cpu: "50m"  # 1000m is equal to 1 VCPU core                                               
```


- **kubernetes-cip-service.yaml**


```
apiVersion: v1
kind: Service 
metadata:
  name: myapp1-cip-service
spec:
  type: ClusterIP # ClusterIP, # NodePort
  selector:
    app: myapp1
  ports: 
    - name: http
      port: 80 # Service Port
      targetPort: 80 # Container Port
```


- **kubernetes-hpa.yaml**


```
apiVersion: autoscaling/v1
kind: HorizontalPodAutoscaler
metadata:
 name: hpa-myapp1
spec:
 scaleTargetRef:
   apiVersion: apps/v1
   kind: Deployment
   name: myapp1-deployment
 minReplicas: 1
 maxReplicas: 10
 targetCPUUtilizationPercentage: 50
```


- Now, put these files in a folder and deploy them in the cloud shell:


```
kubectl apply -f gke-demo/
```


![kubectl-apply](/GCP_pictures/Study-logs/GKE-horizontal-pod-autoscaler/kubectl-apply.PNG "kubectl apply -f")


- After that, run **kubectl describe hpa** to get details.


![describe-hpa](/GCP_pictures/Study-logs/GKE-horizontal-pod-autoscaler/kubectl-describe-hpa.PNG "kubectl describe hpa")


- And you run **kubectl top pods** to get the pod related metrics:


```
kubectl top pods
```


![kubectl-top-pods](/GCP_pictures/Study-logs/GKE-horizontal-pod-autoscaler/kubectl-top-pods.PNG "kubectl top pods")


- You can also check node related metrics by running:


```
kubectl top nodes
```


![kubectl-top-nodes](/GCP_pictures/Study-logs/GKE-horizontal-pod-autoscaler/kubectl-top-nodes.PNG "kubectl top nodes")


- Then we will run this code make a continuous request to the ClusterIP service which is connected to the deployment we created. Then the HPA metrics will spike.


```
kubectl run -i --tty load-generator --rm --image=busybox --restart=Never -- /bin/sh -c "while sleep 0.01; do wget -q -O- http://myapp1-cip-service; done"
```

- Now the code is continuously running:


![continuous-running](/GCP_pictures/Study-logs/GKE-horizontal-pod-autoscaler/continous-running.PNG "Continuous running")


- And when we run **kubectl get hpa** you will see that the CPU utilization spiked.


![cpu-utilization-spiked](/GCP_pictures/Study-logs/GKE-horizontal-pod-autoscaler/cpu-utilization-spiked.PNG "CPU utilization spiked")


- And a single pod is autoscaled to 8:


![autoscaled](/GCP_pictures/Study-logs/GKE-horizontal-pod-autoscaler/pods-autoscaled.PNG "Pods are autoscaled")


- If stop the script and watch, the 8 pods will be scaled down back to 1.


- Now, clean up things including HPA, deployment and ClusterIP service.


![delete-things](/GCP_pictures/Study-logs/GKE-horizontal-pod-autoscaler/delete-things.PNG "Delete things after demo")






