### [Source of this study material : Google Kubernetes Engine with DevOps 75 Real-World Demos by Kalyan Reddy Daida](https://www.udemy.com/course/gcp-google-kubernetes-engine-gke-with-devops/?couponCode=24T4FS22124)


## Kubernetes Services Introduction

- We can **expose an application** on a set of pods using dirrerent types of services available in Kubernetes.

  - **ClusterIP** service (Internal to kubernetes cluster)

  - **NodePort** service (Internet + Internal)

  - **LoadBalancer** service (Internet + Internal)

  - **Ingress** service (Internet + Internal)


- In this demo, we will simply create a loadbalancer service. 


- To access our application outside of GKE Kubernetes cluster, we can use Kubernetes LoadBalancer service which will be eventually mapped to **Google Cloud Load Balancer**.


- In **Kubernetes service**, we have **port** and **target port**:

  - **Port**: this is a service port at which you can access your service.
  
  - **target port**: this is a container port in the pod.


- A LoadBalancer service will create a Google Cloud Load Balancer and Google Cloud External IP.



## Demo - Expose Pod with a service

- We will create a pod again in the **standard-public-cluster-1**. 


```
kubectl run [pod-name] --image nginx:latest
```


![pod-created](/GCP_pictures/Study-logs/gke-service2/pod-created.PNG "Pod created")


- Now, it's time to expose pod as a **Service**.


```
kubectl expose pod [pod-name] --type=LoadBalancer --port=80 --name=nginx-service
```


- Then **kubectl get services** to see detailed info about the service. In **Port 80:32312**, **80** is a port at which we access in the browser. And **32312** is a node port. 


![service-created](/GCP_pictures/Study-logs/gke-service2/kubectl-get-services.PNG "kubectl get services")


- Then run **kubectl describe service service-name**.


```
Name:                     nginx-service
Namespace:                default
Labels:                   run=nginx-pod
Annotations:              cloud.google.com/neg: {"ingress":true}
Selector:                 run=nginx-pod
Type:                     LoadBalancer
IP Family Policy:         SingleStack
IP Families:              IPv4
IP:                       10.176.13.135
IPs:                      10.176.13.135
LoadBalancer Ingress:     35.227.26.149
Port:                     <unset>  80/TCP
TargetPort:               80/TCP
NodePort:                 <unset>  32312/TCP
Endpoints:                10.172.0.13:80
Session Affinity:         None
External Traffic Policy:  Cluster
Events:
  Type    Reason                Age    From                Message
  ----    ------                ----   ----                -------
  Normal  EnsuringLoadBalancer  7m58s  service-controller  Ensuring load balancer
  Normal  EnsuredLoadBalancer   7m18s  service-controller  Ensured load balancer
```


- You can also verify the service you created on the GCP console.


![verify-service](/GCP_pictures/Study-logs/gke-service2/verify-service.PNG "Verify service")


![loadbalancer-ip](/GCP_pictures/Study-logs/gke-service2/loadbalancer-ip.PNG "LoadBalancer IP in browser")



## Demo - Interact with a pod/container

- First run the command:


```
kubectl get pods
```

- Then if you run the **kubectl logs pod-name**, you will see the logs of the pod including HTTP access:


![kubectl-logs](/GCP_pictures/Study-logs/gke-service2/kubectl-logs.PNG "kubectl logs")


- If you want to **stream the logs** in the cloud shell, you can use the following:


```
kubectl logs -f pod-name
```

![stream-logs](/GCP_pictures/Study-logs/gke-service2/stream-logs.PNG "Stream logs")


- Now, we will see **how to connect to a container in a pod** and execute command.


```
kubectl exec -it [pod-name] -- /bin/bash
```

- This will connect you to the bash shell of your container in the pod.


![container-connection](/GCP_pictures/Study-logs/gke-service2/container-connection.PNG "kubectl exec -it podname -- /bin/bash")


- And change directory into **/usr/share/nginx/html**.


![cd-into-html](/GCP_pictures/Study-logs/gke-service2/cd-to-html.PNG "CD into html folder")


- Then you can **Exit** from the container and back to your environment.


![exit-container](/GCP_pictures/Study-logs/gke-service2/exit-container.PNG "Exit container")


- You can see the environment configurations of your container by running:


```
kubectl exec -it [pod-name] -- env
```


![env-container](/GCP_pictures/Study-logs/gke-service2/env-container.PNG "env command")


- **ls** command will show all the directories inside the container.


```
kubectl exec -it [pod-name] -- ls
```


![ls-command](/GCP_pictures/Study-logs/gke-service2/ls-command.PNG "ls command")


- To get a YAML output of the pod resources:


```
kubectl get pod [pod-name] -o yaml
```

```
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: "2024-02-21T06:40:07Z"
  labels:
    run: nginx-pod
  name: nginx-pod
  namespace: default
  resourceVersion: "82022"
  uid: 7da8f30c-9f50-43f5-95b4-ca2a9d223a03
spec:
  containers:
  - image: nginx:latest
    imagePullPolicy: Always
    name: nginx-pod
    resources: {}
    terminationMessagePath: /dev/termination-log
    terminationMessagePolicy: File
    volumeMounts:
    - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
      name: kube-api-access-hvtm9
      readOnly: true
  dnsPolicy: ClusterFirst
  enableServiceLinks: true
  nodeName: gke-standard-public-clus-default-pool-9c5ccc2b-dq87
  preemptionPolicy: PreemptLowerPriority
  priority: 0
  restartPolicy: Always
  schedulerName: default-scheduler
  securityContext: {}
  serviceAccount: default
  serviceAccountName: default
  terminationGracePeriodSeconds: 30
  tolerations:
  - effect: NoExecute
    key: node.kubernetes.io/not-ready
    operator: Exists
    tolerationSeconds: 300
  - effect: NoExecute
    key: node.kubernetes.io/unreachable
    operator: Exists
    tolerationSeconds: 300
  volumes:
  - name: kube-api-access-hvtm9
    projected:
      defaultMode: 420
      sources:
      - serviceAccountToken:
          expirationSeconds: 3607
          path: token
      - configMap:
          items:
          - key: ca.crt
            path: ca.crt
          name: kube-root-ca.crt
      - downwardAPI:
          items:
          - fieldRef:
              apiVersion: v1
              fieldPath: metadata.namespace
            path: namespace
            status:
  conditions:
  - lastProbeTime: null
    lastTransitionTime: "2024-02-21T06:40:07Z"
    status: "True"
    type: Initialized
  - lastProbeTime: null
    lastTransitionTime: "2024-02-21T06:40:09Z"
    status: "True"
    type: Ready
  - lastProbeTime: null
    lastTransitionTime: "2024-02-21T06:40:09Z"
    status: "True"
    type: ContainersReady
  - lastProbeTime: null
    lastTransitionTime: "2024-02-21T06:40:07Z"
    status: "True"
    type: PodScheduled
  containerStatuses:
  - containerID: containerd://655db644d3bd958954c26d6514344977eea33f810ff1c531619b8d0dbec5ba42
    image: docker.io/library/nginx:latest
    imageID: docker.io/library/nginx@sha256:c26ae7472d624ba1fafd296e73cecc4f93f853088e6a9c13c0d52f6ca5865107
    lastState: {}
    name: nginx-pod
    ready: true
    restartCount: 0
    started: true
    state:
      running:
        startedAt: "2024-02-21T06:40:08Z"
  hostIP: 10.0.1.5
  phase: Running
  podIP: 10.172.0.13
  podIPs:
  - ip: 10.172.0.13
  qosClass: BestEffort
  startTime: "2024-02-21T06:40:07Z"
```


- Now, it's time to clean up all the things we generated for the demo:


```
kubectl get all
```

- The command lets us see what resources we created.


![kubectl-get-all](/GCP_pictures/Study-logs/gke-service2/kubectl-get-all.PNG "kubectl get all")


- Then delete the pod and service.


```
kubectl delete pod [pod-name]
```


```
kubectl delete svc [service-name]
```


![clean-up](/GCP_pictures/Study-logs/gke-service2/clean-up.PNG "clean up things")


