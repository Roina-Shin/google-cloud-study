### [Source of this study material : DevOps Masterclass 2024 by Anshul A Chauhan](https://www.udemy.com/course/devops-training)


## Daemonsets in Kubernetes

- Daemonset automatically **runs a copy of a pod** on each node.


- Daemonset runs a copy of a pod on a new node as they are added to the cluster.


- It will create a copy of the particular pod which is defined in the Daemonset YAML file and execute it in every node in the cluster.


- Daemonset will be helpful in case of Monitoring, Log Collection, Proxy Configuration, etc.



## Daemonset Demo

- We need to create a file **daemonset.yaml**.


```
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: logging
spec:
  selector:
    matchLabels:
      app: httpd-logging
  template:
    metadata:
      labels:
        app: httpd-logging
    spec:
      containers:
        - name: webserver
          image: httpd
          ports:
            - containerPort: 80
```


- Currently, no pod is running in my Kubernetes cluster. Let's execute the Daemonset YAML.


```
kubectl apply -f daemonsets.yaml
```


![creating-daemonsets](/GCP_pictures/Study-logs/gke-daemonsets/creating-daemonsets.PNG "Creating Daemonsets")


- If we check the daemonset and the pods, we will see that one daemonset is created. And 3 daemonset pods are running in each of 3 nodes.


![daemonset-running](/GCP_pictures/Study-logs/gke-daemonsets/daemonset-running.PNG "Daemonset running")


- Run **kubectl get pods -o wide** to see the details of the daemonset pods.


![details-daemonset](/GCP_pictures/Study-logs/gke-daemonsets/detailed-daemonset-pods.PNG "Detailed Daemonset")


- If you see the details of the Daemonset, you can run:


```
kubectl describe daemonset [daemonset-name]
```


```
Name:           logging
Selector:       app=httpd-logging
Node-Selector:  <none>
Labels:         <none>
Annotations:    deprecated.daemonset.template.generation: 1
Desired Number of Nodes Scheduled: 3
Current Number of Nodes Scheduled: 3
Number of Nodes Scheduled with Up-to-date Pods: 3
Number of Nodes Scheduled with Available Pods: 3
Number of Nodes Misscheduled: 0
Pods Status:  3 Running / 0 Waiting / 0 Succeeded / 0 Failed
Pod Template:
  Labels:  app=httpd-logging
  Containers:
   webserver:
    Image:        httpd
    Port:         80/TCP
    Host Port:    0/TCP
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Events:
  Type    Reason            Age    From                  Message
  ----    ------            ----   ----                  -------
  Normal  SuccessfulCreate  9m22s  daemonset-controller  Created pod: logging-wnprc
  Normal  SuccessfulCreate  9m22s  daemonset-controller  Created pod: logging-m9s4h
  Normal  SuccessfulCreate  9m22s  daemonset-controller  Created pod: logging-87gtw
```


![daemonset-describe](/GCP_pictures/Study-logs/gke-daemonsets/daemonset-describe.PNG "Daemonset describe")