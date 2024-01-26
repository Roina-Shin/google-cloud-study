### [Source of this study material : Google Cloud Professional Network Engineer by Ankit Mistry](https://www.udemy.com/course/google-cloud-networking/)


## Kubernetes Cluster Deployment

1. Create kubernetes cluster from Google Cloud console

2. Create Docker images

3. Push it to Artifact Registry

4. Deploy workloads - this means to deploy Docker image to cluster

6. Expose it as service


## Kubernetes Cluster Deployment

1. Go to Kubernetes Engine and click Create Cluster. Go with the Standard mode.


![cluster-ready](/GCP_pictures/Study-logs/GKE-2/cluster-ready.PNG "Cluster ready")



2. Now, it's time to create a Docker image.

3. Go to Cloud Shell and make a folder ace. And inside the ace folder, make a folder named kubernetes. Inside that folder make a file named server.js.


4. Inside that server.js file, write the following code:


```
var http = require('http')
var hadleRequest = function(request, response) {
  response.writeHead(200);
  response.end("<h1>Hello world to Kubernetes v1.0</h1>");
}
var www = http.createServer(handleRequest);
www.listen(8080);
```

![server-file](/GCP_pictures/Study-logs/GKE-2/server-file.PNG "Server.js file")


5. To create a docker image, we need to have a Dockerfile.

6. Using vim editor again to create a Dockerfile. Use the following code:


```
FROM node:16-alpine3.11
EXPOSE 8080
COPY server.js .
CMD node server.js
```


- So we are using node:16-alpine3.11 OS and expose it to port 8080. And copy this server.js from our host machine to the container machine. Implement this command line 'node server.js' so that our application will get started.



![dockerfile](/GCP_pictures/Study-logs/GKE-2/dockerfile.PNG "Dockerfile")


- Now, we need to create a docker image and push it to the Artifact Registry.

- In the Cloud Shell, use this command:


```
gcloud builds submit -t gcr.io/$DEVSHELL_PROJECT_ID/kube-app:v1.0
```


![build-and-push-image](/GCP_pictures/Study-logs/GKE-2/image-push-command.PNG "Build and push image command")


- After the redirection configured as below, you can check that the container image is created and pushed to the Artifact Registry.

**Give permission to the Owner with the following roles**

```
gcloud projects add-iam-policy-binding PROJECT_ID \
    --member='user:PRINCIPAL' \
    --role='roles/artifactregistry.admin'

gcloud projects add-iam-policy-binding PROJECT_ID \
    --member='user:PRINCIPAL' \
    --role='roles/storage.admin'
```

**Enable the redirection from Container Registry to Artifact Registry**

```
gcloud artifacts settings enable-upgrade-redirection \
    --project=PROJECT_ID
```


![image-pushed](/GCP_pictures/Study-logs/GKE-2/image-pushed.PNG "Image pushed")



- Now, we have a workload available. We can deploy this workload (docker image). Go back to the Kubernetes Cluster page and click Deploy.


![kubernetes-clusters-page](/GCP_pictures/Study-logs/GKE-2/kubernetes-cluster-page.PNG "Kubernetes Clusters page")


- As you have already created and pushed the image to the Artifact Registry, choose Existing container image and go with the image by using the dropdown menu.


![image-selection](/GCP_pictures/Study-logs/GKE-2/select-image.PNG "Select image from the dropdown menu")


- After configuring the cluster, etc. click create.


![deployment-creation](/GCP_pictures/Study-logs/GKE-2/deployment-creation.PNG "Deployment creation")



- Once done, it's time to expose this deployment as a service to the ouside world. Click Expose and select Port 90 (for experimentation) and choose Target port 8080. Go with the Load Balancer as a Service Type.


![expose-deployment](/GCP_pictures/Study-logs/GKE-2/expose-service.PNG "Expose deployment")


- If you go to the **Load Balancing** and check the URL of the exposed service, you can see that it works.


![load-balancer-for-gke-service](/GCP_pictures/Study-logs/GKE-2/load-balancer-for-service.PNG "Load balancer for GKE service")


- Successfully exposed our first GKE app.


![exposed-app](/GCP_pictures/Study-logs/GKE-2/first-app-exposed.PNG "First GKE app exposed")


- This is the YAML file of this deployment:

```
apiVersion: apps/v1
kind: Deployment
metadata:
  annotations:
    deployment.kubernetes.io/revision: "1"
  creationTimestamp: "2024-01-26T04:17:18Z"
  generation: 1
  labels:
    app: my-first-kube-app
  managedFields:
  - apiVersion: apps/v1
    fieldsType: FieldsV1
    fieldsV1:
      f:metadata:
        f:labels:
          .: {}
          f:app: {}
      f:spec:
        f:progressDeadlineSeconds: {}
        f:replicas: {}
        f:revisionHistoryLimit: {}
        f:selector: {}
        f:strategy:
          f:rollingUpdate:
            .: {}
            f:maxSurge: {}
            f:maxUnavailable: {}
          f:type: {}
        f:template:
          f:metadata:
            f:labels:
              .: {}
              f:app: {}
          f:spec:
            f:containers:
              k:{"name":"kube-app-sha256-1"}:
                .: {}
                f:image: {}
                f:imagePullPolicy: {}
                f:name: {}
                f:resources: {}
                f:terminationMessagePath: {}
                f:terminationMessagePolicy: {}
            f:dnsPolicy: {}
            f:restartPolicy: {}
            f:schedulerName: {}
            f:securityContext: {}
            f:terminationGracePeriodSeconds: {}
    manager: GoogleCloudConsole
    operation: Update
    time: "2024-01-26T04:17:18Z"
  - apiVersion: apps/v1
    fieldsType: FieldsV1
    fieldsV1:
      f:metadata:
        f:annotations:
          .: {}
          f:deployment.kubernetes.io/revision: {}
      f:status:
        f:availableReplicas: {}
        f:conditions:
          .: {}
          k:{"type":"Available"}:
            .: {}
            f:lastTransitionTime: {}
            f:lastUpdateTime: {}
            f:message: {}
            f:reason: {}
            f:status: {}
            f:type: {}
          k:{"type":"Progressing"}:
            .: {}
            f:lastTransitionTime: {}
            f:lastUpdateTime: {}
            f:message: {}
            f:reason: {}
            f:status: {}
            f:type: {}
        f:observedGeneration: {}
        f:readyReplicas: {}
        f:replicas: {}
        f:updatedReplicas: {}
    manager: kube-controller-manager
    operation: Update
    subresource: status
    time: "2024-01-26T04:17:27Z"
  name: my-first-kube-app
  namespace: default
  resourceVersion: "42984"
  uid: 1bdefa45-af18-4721-bc55-dd89d6703609
spec:
  progressDeadlineSeconds: 600
  replicas: 3
  revisionHistoryLimit: 10
  selector:
    matchLabels:
      app: my-first-kube-app
  strategy:
    rollingUpdate:
      maxSurge: 25%
      maxUnavailable: 25%
    type: RollingUpdate
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: my-first-kube-app
    spec:
      containers:
      - image: gcr.io/my-vpn-router-project/kube-app@sha256:0fde9d2b3563432d45614f0755264611c9a12e22ee33321804b73e0e5049bde0
        imagePullPolicy: IfNotPresent
        name: kube-app-sha256-1
        resources: {}
        terminationMessagePath: /dev/termination-log
        terminationMessagePolicy: File
      dnsPolicy: ClusterFirst
      restartPolicy: Always
      schedulerName: default-scheduler
      securityContext: {}
      terminationGracePeriodSeconds: 30
status:
  availableReplicas: 3
  conditions:
  - lastTransitionTime: "2024-01-26T04:17:27Z"
    lastUpdateTime: "2024-01-26T04:17:27Z"
    message: Deployment has minimum availability.
    reason: MinimumReplicasAvailable
    status: "True"
    type: Available
  - lastTransitionTime: "2024-01-26T04:17:19Z"
    lastUpdateTime: "2024-01-26T04:17:27Z"
    message: ReplicaSet "my-first-kube-app-5d7bf96967" has successfully progressed.
    reason: NewReplicaSetAvailable
    status: "True"
    type: Progressing
  observedGeneration: 1
  readyReplicas: 3
  replicas: 3
  updatedReplicas: 3

```


