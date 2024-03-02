### [Source of this study material : Google Kubernetes Engine: The Practical Guide by Shikhar Verma](https://www.udemy.com/course/google-gke)

## Labels and Selectors in Kuberntes

- Labels are key/value pairs attached to objects such as pods.


- Lables are the mechanism which can be used to organize Kubernetes objects.


- Labels are similar to tags in AWS or git.


```
apiVersion: v1
kind: Pod
metadata:
  name: label-test-pod
  labels:
    env: dev
    class: pods
    depart: test
spec:
  containers:
    - name: label-test-pod
      image: ubuntu
      command: ["/bin/bash", "-c", "while true; do echo Yejin will pass ACE exam; sleep 4; done"]
```


- Once labels are attached to an object, we would need filters to narrow down. These are called label selectors.


- We will implement this pod manifest:


```
apiVersion: v1
kind: Pod
metadata:
  name: label-testing
  labels:
    env: dev
    class: pods
    depart: devops
spec:
  containers:
    - name: c00
      image: ubuntu
      command: ["/bin/bash", "-c", "while true; do echo Yejin will pass ACE exam; sleep 4; done"]
    - name: c01
      image: ubuntu
      command: ["/bin/bash", "-c", "while true; do echo Yejin will become a Cloud Engineer; sleep 4; done"]
```


- The YAML will create **2 containers**, c00 and c01 in the pod **label-testing**. See below after the pod was created.


![2-containers-running](/GCP_pictures/Study-logs/gke-labels-and-selectors/2-containers-running.PNG "2 containers running")


- You can label the pod with a new label:


```
kubectl label pods label-testing user=yejin
```


![kubectl-show-labels](/GCP_pictures/Study-logs/gke-labels-and-selectors/kubectl-show-labels.PNG "kubectl get pods --show-labels")


- This time, I'll create another pod with 2 containers:


```
apiVersion: v1
kind: Pod
metadata:
  name: label-testing-2
  labels:
    env: dev
    class: pods
    depart: sre
spec:
  containers:
    - name: c00
      image: ubuntu
      command: ["/bin/bash", "-c", "while true; do echo Yejin will pass ACE exam; sleep 4; done"]
    - name: c01
      image: ubuntu
      command: ["/bin/bash", "-c", "while true; do echo Yejin will become a Cloud Engineer; sleep 4; done"]
```


![another-pod-created](/GCP_pictures/Study-logs/gke-labels-and-selectors/another-pod-created.PNG "Another pod is created")


- You can search pods with the label key-value:


```
kubectl get pods -l depart=sre
```


![search-pod-with-label](/GCP_pictures/Study-logs/gke-labels-and-selectors/search-pod-with-label.PNG "Search pod with label")



- You can also search pods that are not matching with the label:


```
kubectl get pods -l depart!=sre
```


![label-not-equal](/GCP_pictures/Study-logs/gke-labels-and-selectors/label-not-equal.PNG "Label not equal")



- I'll create the 3rd pod with the following YAML:


```
apiVersion: v1
kind: Pod
metadata:
  name: label-testing-3
  labels:
    env: prod
    class: pods
    depart: sre
spec:
  containers:
    - name: c00
      image: ubuntu
      command: ["/bin/bash", "-c", "while true; do echo Yejin will pass ACE exam; sleep 4; done"]
    - name: c01
      image: ubuntu
      command: ["/bin/bash", "-c", "while true; do echo Yejin will become a Cloud Engineer; sleep 4; done"]
```


![3rd-pod-generated](/GCP_pictures/Study-logs/gke-labels-and-selectors/3rd-pod-generated.PNG "3rd pod generated")


- If you want to search for pods that are either in depart "sre" or "dev" you can run:


```
kubectl get pods -l 'depart in (sre, dev)' --show-labels
```


![depart-in-sre](/GCP_pictures/Study-logs/gke-labels-and-selectors/depart-in-sre.PNG "depart in sre")



- If you find pods that are not in depart "sre":


```
kubectl get pods -l 'depart notin (sre)' --show-labels
```


![depart-notin-sre](/GCP_pictures/Study-logs/gke-labels-and-selectors/depart-notin-sre.PNG "depart notin sre")



## Node Selector

- Node Selector is used to specify the nodes into which a pod can be scheduled.


- You can tell a pod to run on a particular node.


- Generally, such constraints are unnecessary as the scheduler will automatically do a reasonable placement. But in certain circumstances, we might need it.


- We can use labels to tag nodes as well.


- When the nodes are tagged, you can use the label selectors to specify the pods to run only on specific nodes.


- **First, we will assign labels to the nodes**.


- **Then, use the node selector for the pod configuration**.



### Node Selector Demo

- For this demo, I'll add a new node pool. Currently I have a single node running in the default node pool. 


- After adding a new node, I have 2 nodes. But my existing pods are running in the default node pool and the node inside it.


![pods-running-in-deefault-pool](/GCP_pictures/Study-logs/gke-labels-and-selectors/pods-running-in-default-pool.PNG "Pods running in default node pool")


- Before you assign any labels to the nodes, check your nodes' current labels.


```
kubectl get nodes --show-labels
```


![node-labels](/GCP_pictures/Study-logs/gke-labels-and-selectors/node-labels.PNG "Node labels")



-These are system generated node labels. And I'll generate **my own labels** to the nodes.


```
kubectl label nodes [node name] depart=marketing
```


- You can see that the label is now reflected to the node label.


![label-reflected](/GCP_pictures/Study-logs/gke-labels-and-selectors/label-reflected.PNG "label reflected")


- Then I'll create a pod with a **nodeSelector** using the following YAML:


```
apiVersion: v1
kind: Pod
metadata:
  name: label-testing-4
  labels:
    env: prod
    class: pods
    depart: sre
spec:
  containers:
    - name: c00
      image: ubuntu
      command: ["/bin/bash", "-c", "while true; do echo Yejin will pass ACE exam; sleep 4; done"]
  nodeSelector:
    depart: marketing
```


- After applying the YAML, I can see that the pod is deployed in the specific node that has the **same label** as the nodeSelector.


![specific-node-for-pod](/GCP_pictures/Study-logs/gke-labels-and-selectors/specific-node-for-pod.PNG "Specific node for pod")












