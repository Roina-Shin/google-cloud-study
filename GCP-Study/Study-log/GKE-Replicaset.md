### [Source of this study material : Google Kubernetes Engine with DevOps 75 Real-World Demos by Kalyan Reddy Daida](https://www.udemy.com/course/gcp-google-kubernetes-engine-gke-with-devops/?couponCode=24T4FS22124)


## GKE Replicaset

- A **replicaset's purpose** is to maintain a stable set of **replica pods** running at any given time.


- If our application crashes (if any pod dies), replicaset will **recreate the pod** immediately to ensure the configured number of pods running at any time.


- To avoid overloading of traffic to a single pod, we can use **load balancing**.


- Kubernetes provides pod load balancing using **Services** for the pods which are part of a ReplicaSet.


- **Labels & selectors** are the key items which ties all 3 together (Pod, ReplicaSet, and Service).



## Demo - Deploy ReplicaSet and Verify

- As we are creating a ReplicaSet in a declarative way, we are going to use the yaml file:


```
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: my-helloworld-rs
  labels:
    app: my-helloworld
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-helloworld
  template:
    metadata:
      labels:
        app: my-helloworld
    spec:
      containers:
      - name: my-helloworld-app
        image: stacksimplify/kube-helloworld:1.0.0
```


- Save this file and upload it to the cloud shell.


- Then run the command:


```
kubectl create -f [yaml file name]
```


![kubectl-create-yaml](/GCP_pictures/Study-logs/gke-replicaset/kubectl-create-yaml.PNG "kubectl create yaml file")


- Once the ReplicaSet is created, list the replicaset.


```
kubectl get replicaset
```


![kubectl-get-replicaset](/GCP_pictures/Study-logs/gke-replicaset/kubectl-get-replicaset.PNG "kubectl get replicaset")


- As we configured in the replicaset yaml file, it created the 3 replica pods running.


- To get a detailed info about the replicaset, you can run:


```
kubectl describe rs [rs name]
```


![describe-rs](/GCP_pictures/Study-logs/gke-replicaset/rs-describe.PNG "describe rs")



- The replicaset created 3 pods for us:


```
kubectl get pods -o wide
```


![get-pods](/GCP_pictures/Study-logs/gke-replicaset/get-pods.PNG "kubectl get pods")


- Then we are going to verify the owner of the pod:


```
kubectl get pods [one of the pod name] -o yaml
```


```
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: "2024-02-21T08:05:57Z"
  generateName: my-helloworld-rs-
  labels:
    app: my-helloworld
  name: my-helloworld-rs-hnz5v
  namespace: default
  ownerReferences:
  - apiVersion: apps/v1
    blockOwnerDeletion: true
    controller: true
    kind: ReplicaSet
    name: my-helloworld-rs
    uid: 55604be7-69cf-4fa3-aeec-c5839dd4e101
  resourceVersion: "128679"
  uid: f8424720-f843-4622-890b-9b1e78a80051
spec:
  containers:
  - image: stacksimplify/kube-helloworld:1.0.0
    imagePullPolicy: IfNotPresent
    name: my-helloworld-app
    resources: {}
    terminationMessagePath: /dev/termination-log
    terminationMessagePolicy: File
    volumeMounts:
    - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
      name: kube-api-access-ghsbz
      apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: "2024-02-21T08:05:57Z"
  generateName: my-helloworld-rs-
  labels:
    app: my-helloworld
  name: my-helloworld-rs-hnz5v
  namespace: default
  ownerReferences:
  - apiVersion: apps/v1
    blockOwnerDeletion: true
    controller: true
    kind: ReplicaSet
    name: my-helloworld-rs
    uid: 55604be7-69cf-4fa3-aeec-c5839dd4e101
  resourceVersion: "128679"
  uid: f8424720-f843-4622-890b-9b1e78a80051
spec:
  containers:
  - image: stacksimplify/kube-helloworld:1.0.0
    imagePullPolicy: IfNotPresent
    name: my-helloworld-app
    resources: {}
    terminationMessagePath: /dev/termination-log
    terminationMessagePolicy: File
    volumeMounts:
    - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
      name: kube-api-access-ghsbz
```


- And in the owner references, you can see that the owner of the pod is the name of the replicaset. It means the pods belong to the replicaset.


- Now, we will expose the replicaset as a service.


```
kubectl expose rs [replicaset-name] --type=LoadBalancer --port=80 --target-port=8080 --name=[service-name]
```


![expose-service](/GCP_pictures/Study-logs/gke-replicaset/expose-service.PNG "Expose service")


- And this replicaset ensures the **availability**. To test this, we will delete one of the pods and see what happens.


![availability](/GCP_pictures/Study-logs/gke-replicaset/availability.PNG "availability")


- As we set the number of replicas as **3** in the yaml file, the replicaset ensures that we always have 3 pods at any point.









