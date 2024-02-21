### [Source of this study material : Google Kubernetes Engine with DevOps 75 Real-World Demos by Kalyan Reddy Daida](https://www.udemy.com/course/gcp-google-kubernetes-engine-gke-with-devops/?couponCode=24T4FS22124)


## Deploy and Expose the Deployment

- To create a deployment, just run the command:


```
kubectl create deployment [deploy-name] --image=[container-image]
```


- After you run the command and verify if the deployment is created.


![deployment-created](/GCP_pictures/Study-logs/gke-create-expose-deployment/deployment-created.PNG "Deployment created")


- If you run **kubectl describe deployment**, you will see the details of the deployment:


```
Name:                   example-deployment
Namespace:              default
CreationTimestamp:      Wed, 21 Feb 2024 11:17:18 +0000
Labels:                 app=example-deployment
Annotations:            deployment.kubernetes.io/revision: 1
Selector:               app=example-deployment
Replicas:               1 desired | 1 updated | 1 total | 1 available | 0 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  25% max unavailable, 25% max surge
Pod Template:
  Labels:  app=example-deployment
  Containers:
   kubenginx:
    Image:        stacksimplify/kubenginx:1.0.0
    Port:         <none>
    Host Port:    <none>
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Conditions:
  Type           Status  Reason
  ----           ------  ------
  Available      True    MinimumReplicasAvailable
  Progressing    True    NewReplicaSetAvailable
OldReplicaSets:  <none>
NewReplicaSet:   example-deployment-77f69b8d88 (1/1 replicas created)
Events:
  Type    Reason             Age    From                   Message
  ----    ------             ----   ----                   -------
  Normal  ScalingReplicaSet  3m32s  deployment-controller  Scaled up replica set example-deployment-77f69b8d88 to 1
```


- So this deployment lets GKE create (roll out) 1 replicaset.


- To see the **rollout history** of the deployment:


```
kubectl rollout history deployment/example-deployment
```


![rollout-history](/GCP_pictures/Study-logs/gke-create-expose-deployment/rollout-history.PNG "Rollout history")


- To provide the **CHANGE-CAUSE**, you need to use the following command:


```
kubectl annotate deployment/example-deployment kubernetes.io/change-cause="Create deployment - version1"
```


![annotate-change-cause](/GCP_pictures/Study-logs/gke-create-expose-deployment/annotate-change-cause.PNG "Annotate change cause")


- To **scale the deployment**:


```
kubectl scale --replicas=2 deployment/example-deployment
```


![scale-replicas](/GCP_pictures/Study-logs/gke-create-expose-deployment/scale-replicas.PNG "kubectl scale replicas")


- You can also **scale down** back to:


```
kubectl scale --replicas=1 deployment/example-deployment
```


![scale-down](/GCP_pictures/Study-logs/gke-create-expose-deployment/scale-down.PNG "Scale down deployment")


- Now, we are going to expose the deployment as a service:


```
kubectl expose deployment [deployment-name] --type=LoadBalancer --port=80 --target-port=80 --name=example-service
```


![expose-deployment-as-service](/GCP_pictures/Study-logs/gke-create-expose-deployment/expose-service.PNG "Expose deployment as a service")



## Update Deployment

- For updating deployment, we have 2 options:

  - Set image

  - Edit deployment


### Updating Application version from V1 ro V2 using "Set Image" option

- First, get the **deployment output** by running:


```
kubectl get deployment example-deployment -o yaml
```

```
apiVersion: apps/v1
kind: Deployment
metadata:
  annotations:
    deployment.kubernetes.io/revision: "1"
    kubernetes.io/change-cause: Create deployment - version1
  creationTimestamp: "2024-02-21T11:17:18Z"
  generation: 4
  labels:
    app: example-deployment
  name: example-deployment
  namespace: default
  resourceVersion: "256254"
  uid: e49d31d0-d99e-4cd7-bf53-f6cc1571bceb
spec:
  progressDeadlineSeconds: 600
  replicas: 1
  revisionHistoryLimit: 10
  selector:
    matchLabels:
      app: example-deployment
  strategy:
    rollingUpdate:
      maxSurge: 25%
      maxUnavailable: 25%
    type: RollingUpdate
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: example-deployment
    spec:
      containers:
      - image: stacksimplify/kubenginx:1.0.0
        imagePullPolicy: IfNotPresent
        name: kubenginx
        resources: {}
        terminationMessagePath: /dev/termination-log
        terminationMessagePolicy: File
      dnsPolicy: ClusterFirst
      restartPolicy: Always
      schedulerName: default-scheduler
      securityContext: {}
      terminationGracePeriodSeconds: 30
status:
  availableReplicas: 1
  conditions:
  - lastTransitionTime: "2024-02-21T11:17:19Z"
    lastUpdateTime: "2024-02-21T11:17:25Z"
    message: ReplicaSet "example-deployment-77f69b8d88" has successfully progressed.
    reason: NewReplicaSetAvailable
    status: "True"
    type: Progressing
  - lastTransitionTime: "2024-02-21T11:58:00Z"
    lastUpdateTime: "2024-02-21T11:58:00Z"
    message: Deployment has minimum availability.
    reason: MinimumReplicasAvailable
    status: "True"
    type: Available
  observedGeneration: 4
  readyReplicas: 1
  replicas: 1
  updatedReplicas: 1
```


- Check the container name in **spec.containers.name** in the output yaml file and make a note of it. Then replace in **kubectl set image command**:


```
kubectl set image deployment/example-deployment [container-name]=[container-image-to-update-to] --record=true
```

```
kubectl set image deployment/example-deployment kubenginx=stacksimplify/kubenginx:2.0.0 --record=true
```


![image-updated](/GCP_pictures/Study-logs/gke-create-expose-deployment/image-updated.PNG "Image updated")


- To verify the **deployment status**:


```
kubectl rollout status deployment/example-deployment
```

![kubectl-rollout-status](/GCP_pictures/Study-logs/gke-create-expose-deployment/rollout-status.PNG "kubectl rollout status")


- If you run **kubectl describe deployment**, you will see the version of the deployment:


```
Name:                   example-deployment
Namespace:              default
CreationTimestamp:      Wed, 21 Feb 2024 11:17:18 +0000
Labels:                 app=example-deployment
Annotations:            deployment.kubernetes.io/revision: 2
                        kubernetes.io/change-cause: kubectl set image deployment/example-deployment kubenginx=stacksimplify/kubenginx:2.0.0 --record=true
Selector:               app=example-deployment
Replicas:               1 desired | 1 updated | 1 total | 1 available | 0 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  25% max unavailable, 25% max surge
Pod Template:
  Labels:  app=example-deployment
  Containers:
   kubenginx:
    Image:        stacksimplify/kubenginx:2.0.0
    Port:         <none>
    Host Port:    <none>
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Conditions:
  Type           Status  Reason
  ----           ------  ------
  Available      True    MinimumReplicasAvailable
  Progressing    True    NewReplicaSetAvailable
OldReplicaSets:  example-deployment-77f69b8d88 (0/0 replicas created)
NewReplicaSet:   example-deployment-66dc9d9b7f (1/1 replicas created)
Events:
  Type    Reason             Age    From                   Message
  ----    ------             ----   ----                   -------
  Normal  ScalingReplicaSet  29m    deployment-controller  Scaled up replica set example-deployment-77f69b8d88 to 2 from 1
  Normal  ScalingReplicaSet  26m    deployment-controller  Scaled down replica set example-deployment-77f69b8d88 to 1 from 2
  Normal  ScalingReplicaSet  5m47s  deployment-controller  Scaled up replica set example-deployment-66dc9d9b7f to 1
  Normal  ScalingReplicaSet  5m44s  deployment-controller  Scaled down replica set example-deployment-77f69b8d88 to 0 from 1
```


- Also, run **kubectl rollout history deployment/example-deployment** to get the rollout history:


![rollout-history-again](/GCP_pictures/Study-logs/gke-create-expose-deployment/rollout-history-again.PNG "Rollout history again")


- Also change the annotation of change cause:


```
kubectl annotate deployment/example-deployment kubernetes.io/change-cause="Update to v2"
```


![change-cause-again](/GCP_pictures/Study-logs/gke-create-expose-deployment/change-cause-again.PNG "Change cause of the update")



### Updating Deployment with "Edit" option

- Run the command to update from version 2 to version 3:


```
kubectl edit deployment/example-deployment
```


- Then you will be prompted to a editor window:


![editor-window](/GCP_pictures/Study-logs/gke-create-expose-deployment/editor-window.PNG "Editor window")


- Edit the container image from 2.0.0 to 3.0.0 and save the file.


![edit-container-image](/GCP_pictures/Study-logs/gke-create-expose-deployment/edit-container-image.PNG "Edit container image")


- Then verify the version update like following:


![verify-update](/GCP_pictures/Study-logs/gke-create-expose-deployment/verify-update.PNG "Verify update")


- Run **kubectl get rs** to get replicaset:


![kubectl-get-rs](/GCP_pictures/Study-logs/gke-create-expose-deployment/get-rs.PNG "kubectl get rs")


- You will see that the latest replicaset is active now.



## Rollback a deployment to a previous version

- First, check out the rollout history:


```
kubectl rollout history deployment/example-deployment
```


- You can see the details of each rollout by:


```
kubectl rollout history deployment/example-deployment --revions=1
```


![rollout-history-revision](/GCP_pictures/Study-logs/gke-create-expose-deployment/rollout-history-revision.PNG "Rollout history revision")


- Now, roll back to the previous version:


```
kubectl rollout undo deployment/example-deployment
```


- Now, if you verify by running:


```
kubectl get deployment example-deployment -o yaml
```


- The deployment is rolled back to the previous version.


![rollback-happens](/GCP_pictures/Study-logs/gke-create-expose-deployment/rollback-happens.PNG "Rollback happens")


- This is the rollout history after the rollback:


![rollout-history-after-rollback](/GCP_pictures/Study-logs/gke-create-expose-deployment/rollout-history-after-rollback.PNG "Rollout history after rollback")


- In order to rollback to a specific version:


```
kubectl rollout undo deployment/example-deployment --to-revision=3
```


![to-revision-3](/GCP_pictures/Study-logs/gke-create-expose-deployment/to-revision-3.PNG "To revision 3")


- **Rollout restart** will kill the existing pods and recreate new pods in a rolling fashion (**without any downtime)**.


```
kubectl rollout restart deployment/example-deployment
```


- After rollout restart, you will see that the pod hash is changed. (pod is changed)


![pod-hash-changed](/GCP_pictures/Study-logs/gke-create-expose-deployment/pod-hash-changed.PNG "Pod hash changed")


