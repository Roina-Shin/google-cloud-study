### [Source of this study material : Google Kubernetes Engine with DevOps 75 Real-World Demos by Kalyan Reddy Daida](https://www.udemy.com/course/gcp-google-kubernetes-engine-gke-with-devops/?couponCode=24T4FS22124)


## Demo - Implement Kubernetes Pods Imperative Way


- Go to Kubernetes Engine on GCP console and create a standard cluster with the following conditions.

  - Regional: us-central1

  - Number of nodes (per zone): 1

  - Total number of nodes: 3


- After creating the cluster, go to the far right side of the cluster info panel and click three dots. Select connect.


![connect-to-cluster-command](/GCP_pictures/Study-logs/gke-kubectl-imperative-pods/connect-to-cluster-command.PNG "Connect to the Cluster command")


- Open the cloud shell and run the command.


```
gcloud container clusters get-credentials standard-public-cluster-1 --region us-east1 --project devops-project-yj
```


![connection-command-run](/GCP_pictures/Study-logs/gke-kubectl-imperative-pods/connection-command-run.PNG "Connection command run")


- If you run **kubectl get nodes**, you will see that the 3 nodes are running.


![3-nodes-running](/GCP_pictures/Study-logs/gke-kubectl-imperative-pods/3-nodes-running.PNG "3 nodes are running")


- If you want to get some additional info about the nodes, use **kubectl get nodes -o wide**.


![kubectl-o-wide](/GCP_pictures/Study-logs/gke-kubectl-imperative-pods/kubectl-o-wide.PNG "kubectl get nodes -o wide")


- If you run **kubectl get pods**, there is currently no pods running in the cluster.


![no-pods-running](/GCP_pictures/Study-logs/gke-kubectl-imperative-pods/no-pods-running.PNG "no pods running")


- Let's try to run a example pod:


```
kubectl run [pod-name] --image nginx:latest
```


![nginx-pod](/GCP_pictures/Study-logs/gke-kubectl-imperative-pods/nginx-pod.PNG "nginx pod created")



- Then you can run **kubectl get pods -o wide** to see in which node the pod is deployed.


![kubectl-get-pods-o-wide](/GCP_pictures/Study-logs/gke-kubectl-imperative-pods/kubectl-get-pods-o-wide.PNG "kubectl get pods -o wide")


- We can see that the pod is **scheduled on this node** called gke-standard-public-clus-default-pool-9c5ccc2b-dq87.


- So what happened when you run **kubectl run pod-name --image nginx**:

  - Kubernetes created a pod

  - Pulled the docker image from docker hub

  - Created the container in the pod

  - Started the container present in the pod


- When you want to see the detailed info about your pod, you can run **kubectl describe pod pod-name**.


```
Name:             nginx-pod
Namespace:        default
Priority:         0
Service Account:  default
Node:             gke-standard-public-clus-default-pool-9c5ccc2b-dq87/10.0.1.5
Start Time:       Wed, 21 Feb 2024 04:44:08 +0000
Labels:           run=nginx-pod
Annotations:      <none>
Status:           Running
IP:               10.172.0.12
IPs:
  IP:  10.172.0.12
Containers:
  nginx-pod:
    Container ID:   containerd://3590b8a312afaac4d69640d01e6ae9edd7529ab2ba508c082439d78e2934c3c0
    Image:          nginx:latest
    Image ID:       docker.io/library/nginx@sha256:c26ae7472d624ba1fafd296e73cecc4f93f853088e6a9c13c0d52f6ca5865107
    Port:           <none>
    Host Port:      <none>
    State:          Running
      Started:      Wed, 21 Feb 2024 04:44:09 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-c46f5 (ro)
Conditions:
  Type              Status
  Initialized       True 
  Ready             True 
  ContainersReady   True 
  PodScheduled      True 
Volumes:
  kube-api-access-c46f5:
    Type:                    Projected (a volume that contains injected data from multiple sources)
TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type    Reason     Age    From               Message
  ----    ------     ----   ----               -------
  Normal  Scheduled  7m14s  default-scheduler  Successfully assigned default/nginx-pod to gke-standard-public-clus-default-pool-9c5ccc2b-dq87
  Normal  Pulling    7m14s  kubelet            Pulling image "nginx:latest"
  Normal  Pulled     7m13s  kubelet            Successfully pulled image "nginx:latest" in 411.255667ms (411.274409ms including waiting)
  Normal  Created    7m13s  kubelet            Created container nginx-pod
  Normal  Started    7m13s  kubelet            Started container nginx-pod
```


- If you look at the **Events** in description, there is a **default scheduler** that scheduled a pod to a particular node.


- Once the pod is scheduled, inside that node, we will have a **kubelet**. That **kubelet** has pulled the docker image and started the container inside the pod.


- If any error happens in the process, always this **event** section in the **kubectl describe** command.


![events-in-describe](/GCP_pictures/Study-logs/gke-kubectl-imperative-pods/events-in-describe.PNG "Events in description")



- Currently, we can access the application **only inside the worker nodes** and not through browser.


- To access it externally, we need to create a **NodePort** or **Load Balancer service**.


- So for now, we will delete the pod.


```
kubectl delete pod [pod-name]
```


![kubectl-delete-pod](/GCP_pictures/Study-logs/gke-kubectl-imperative-pods/delete-pod.PNG "delete pod")








