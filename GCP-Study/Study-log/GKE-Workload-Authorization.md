### [Source of this study material : GCP Professional Cloud Architect by Ranga Karanam](https://www.udemy.com/course/google-cloud-professional-cloud-architect-certification/)


## Authorization of Kubernetes Workloads

- How can you give access to your microservices?


- Solution: Assign permissions at **pod level**.


- But how can you assign a service account to a microservice (or a pod)?


  1. Use Kubernetes Secrets

  2. Use Workload Identity


### Use Kubernetes Secret

- First, create a service account for the Kubernetes microservice-a. We will give the service account a **Storage Object Admin** role.


![create-service-account](/GCP_pictures/Study-logs/gke-authorization/create-service-account.PNG "Create a service account")


- Now, we will create a JSON key file for the service account.


![create-json-key](/GCP_pictures/Study-logs/gke-authorization/create-json-key.PNG "Create a json key file")


- Let's **import the service account key as a secret** in the cloud shell:


```
kubectl create secret generic microservice-a-sa-key --from-file=key.json
```


- Once you have a secret created in your cluster, make your application use the Kubernetes secret by configuring the deployment.


```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: microservice-a
spec:
  replicas: 3
  selector:
    matchLabels:
      app: microservice-a
  template:
    metadata:
      name: microservice-a-pod
      labels:
        app: microservice-a
    spec:
      volumes:
        - name: microservice-a-sa-key
          secret:
            secretName: microservice-a-sa-key
      containers:
        - name: microservice-a
          image: nginx:latest
          volumeMounts:
            - name: microservice-a-sa-key
              mountPath: /var/secrets/google
          env:
            - name: GOOGLE_APPLICATION_CREDENTIALS
              value: /var/secrets/google/key.json
```


- When you apply this deployment file where the service account key is coded to the deployment pods, your pod will be given all the permissions of the service account.


![microservice-permission-given](/GCP_pictures/Study-logs/gke-authorization/microservice-permission-applied.PNG "Microservice permission applied")




### Use Workload Identity

- **Workload Identity** is a recommended way to assign permissions at the pod level.


- **Google Cloud IAM** lets a IAM user do across clusters created in a project, folder or organization.


- **Kubernetes RBAC** provides you with fine-grained access controls at a individual cluster and namespace level.

  - Control access at Kubernetes resource levels (deployment, service, pod, secrets, configMap)


- **Kubernetes Role-based Access Control (RBAC)** is a Kubernetes resource, not of GKE, AKS (Azure) or EKS (AWS). Not related to GCP IAM, but internall to Kuberntes.


- How do you mananage access using **Kubernetes RBAC**?


  - Create **Kubernetes RBAC API objects**

    - **Role**: a set of allowed permissions in a namespace.

    - **ClusterRole**: a set of allowed permissions in a cluster.

    - **RoleBinding**: Map a user (or group or serviceaccount) to a Role or ClusterRole **at the level of namespace**.

    - **ClusterRoleBinding**: Map a user (or group or serviceaccount) to a ClusterRole **across all namespaces in a cluster**.



- **Example Kubernetes RBAC YAML - Role**


```
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: default
  name: all-configmaps-editor-role
rules:
  - apiGroups: [""]
    reources: ["configmaps"]
    verbs: ["update", "get"]
```


- **resources**: Which resources?


- **verbs**: what do you want to allow?

  - examples: "get", "list", "create", "update", "delete", etc.



- **Example Kubernetes RBAC YAML - ClusterRole**


```
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  # Namespace is not configured
  name: all-secrets-viewer-role
rules:
  - apiGroups: [""]
    reources: ["secrets"]
    verbs: [""get", "watch", "list"]
```


- **ClusterRole** represents allowed permissions in a cluster.



- **Kubernetes RBAC - RoleBinding and ClusterRoleBinding**


```
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding # RoleBinding or ClusterRoleBinding
metadata:
  name: edit-configmaps
  namespace: default
subjects:
  - kind: User # Google Cloud User account
    name: yejinshin@yejin-cloud-study.site
  - kind: ServiceAccount # Kubernetes service account
    name: kubernetes-service-account-name
  - kind: User # IAM service account
    name: iam-service-account@PROJECT-ID.google.com.iam.gserviceaccount.com
roleRef:
  kind: Role # Role or ClusterRole
  name: all-configmaps-editor-role
```



## Understanding Kubernetes Security Best Practices

- Enable Node Auto-Upgrade for GKE nodes.


- Use shielded GKE nodes with secure boot.


- Enable workload identity.

  - Use Workload identity to provide microservices specific accesses.


- Use namespaces and **RBAC** to restrict user access to cluster resources.


- Use Kubernetes secrets or Secret Manager for secret management.



## Authorization for Kubernetes - Scenarios


| Solution | Scenarios |
| ------:| -----------:|
| Workload Identity   | Your microservice is going to be deployed to GKE. You want to give each microservice specific access to Google Cloud resources. |
| Node Pool Service Account | Your microservice is going to be deployed in GKE. You want to give common permissions to Cloud Logging and Cloud Monitoring. |
| Kubernetes RBAC    | You are sharing GKE cluster between different teams. You want to ensure that each team has access to deploy only to their specific namespaces. |
| Kubernetes Engine Admin    | Which role gives you complete access to GKE clusters and the Kubernetes API objects? |
| Check if IAM has the permission - **container.clusters.get**    | You are assigned permissions using Kubernetes RBAC. But you are unable to access the cluster. |
