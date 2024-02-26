### [Source of this study material : Google Cloud Developer by Ranga Karanam](https://www.udemy.com/course/google-cloud-certified-professional-cloud-developer)

## Using Kubernetes Namespaces

- I want to create **multiple virtual clusters** inside the same physical Kubernetes cluster. How can I do that?


- Creating a **namespace** is like creating a small virtual cluster in the Kubernetes cluster.


- You can create multiple **namespaces** and attach microservices or pods to each namespace.


- Only the pods in the same namespace can talk to each other.


- So, **namespaces** are recommended for clusters shared between mulitple teams or projects.


- The command to list the namespaces are:


```
kubectl get namespace
```


![kubectl-get-namespace](/GCP_pictures/Study-logs/gke-namespaces/kubectl-get-namespace.PNG "kubectl get namespace")


- If you want to see **deployments in a specific namespace**:


```
kubectl get deployment --namespace=kube-system
```


![kubectl-get-deployment--namespace](/GCP_pictures/Study-logs/gke-namespaces/kubectl-get-deployment--namespace.PNG "kubectl get deployment --namespace")


- Without specifying the **namespace**, you will see the deployment in the **default** namespace.


- You can then create a namespace:


```
kubectl create namespace [namespace name]
```


- And create a deployment in that namespace:


```
kubectl apply -f [file name] --namespace=[namespace name]
```


![deploy-with-namespace](/GCP_pictures/Study-logs/gke-namespaces/deploy-with-namespace.PNG "Deploy with namespace")


