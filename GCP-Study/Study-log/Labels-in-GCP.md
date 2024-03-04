### [Source of this study material : Google Cloud Professional Cloud Architect by Anshul A Chauhan Jenkins](https://www.udemy.com/course/google-cloud-specialization)


## What is labels?

- Labels are kind of sticky notes which you can apply on Google Resources.


- Labels are useful for searching resources in cloud.



## How labels work?

- Labels are key-value pair. 


- User is allowed to put 64 labels per resource.


- Example:

  - Define cost center and location

    - Whenever user create resource, user can attach a cost center with labels

  - Define resource environment / project

  - Define service type / owner

    - This way, you can define service A is using x number of services, etc.

  - Define resource state: ready / inuse / readyfordeletion


## Labels vs Network Tags

### Labels

- Can be applied across all GCP resources


- Can be applied for monitoring purpose


- Labels cannot affect the resource operations


### Network Tags

- Network Tags can only be applied for Network/VPC resources


- Network Tags also affect the resource operations (e.g. Firewall rule access, network route)



## Labels Demo in GCP

- First, we will create an instance using web console and apply labels. You can find label right below VM name section.


![labels-in-gcp](/GCP_pictures/Study-logs/labels-in-gcp/labels-in-gcp.PNG "Labels in GCP")


- Click Manage labels and add labels and create the VM.


![add-labels](/GCP_pictures/Study-logs/labels-in-gcp/add-labels.PNG "Add labels")



- Now, we will see how to create a VM and attach a new label to it using CLI.


- If you want to **set a specific region and zone** so that you won't need to define the region and zone whenever you execute gcloud command, run:


```
gcloud config set compute/region us-east1
```

```
gcloud config set compute/zone us-east1-c
```


![gcloud-config-set](/GCP_pictures/Study-logs/labels-in-gcp/gcloud-config-set-zone.PNG "gcloud config set compute/zone")



- Now create a VM with labels using:


```
gcloud compute instances create my-instance --labels owner=yejin,env=development,service_type=backend_app
```


![create-vm-with-labels](/GCP_pictures/Study-logs/labels-in-gcp/create-vm-with-labels.PNG "Create a VM with labels")



- To see the labels of a particular VM:


```
gcloud compute instances describe my-instance --format "yaml(labels)"
```


![instances-describe-labels](/GCP_pictures/Study-logs/labels-in-gcp/instances-describe-labels.PNG "instances describe labels")



- If you want to update the labels:


```
gcloud compute instances update my-instance --update-labels owner=minkyung
```


![update-labels](/GCP_pictures/Study-logs/labels-in-gcp/update-labels.PNG "Update labels")


![labels-updated](/GCP_pictures/Study-logs/labels-in-gcp/labels-updated.PNG "Labels updated")


- To remove the labels:


```
gcloud compute instances update my-instance --remove-labels owner
```


![labels-removed](/GCP_pictures/Study-logs/labels-in-gcp/labels-removed.PNG "Labels removed")



- Suppose we want to **filter out the resources with labels**. Go to GCP console and Compute Engine VM instances. In filter section, type **labels**. 


![filter-labels](/GCP_pictures/Study-logs/labels-in-gcp/filter-labels.PNG "Filter labels")


- If you type **en** the filter automatically suggests matching search terms like **env: development**. Enter the search term. 


![label-env-dev](/GCP_pictures/Study-logs/labels-in-gcp/label-env-dev.PNG "labels env: development")


- If you keep adding labels, the list of VMs with the labels are filtered and shown.


![adding-labels](/GCP_pictures/Study-logs/labels-in-gcp/adding-labels.PNG "adding labels")





