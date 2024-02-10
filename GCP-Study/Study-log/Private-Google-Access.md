### [Source of this study material : Google Cloud Professional Network Engineer by Ankit Mistry](https://www.udemy.com/course/google-cloud-networking/)


## Private Google Access

- Let's say you have a VM. And you want to connect the VM with the GCS and other Google APIs and services (Youtube API, etc.)


- And with **Private Google Access**, the VM can access without any external IP and only with internal IP.


- This option can be chosen when creating a subnet in your custom VPC.


![subnet-creation](/GCP_pictures/Study-logs/private-google-access/subnet-creation.PNG "During subnet creation")


- **Private Google Access** sets whether VMs in this subnet can access Google services without assigning external IP addresses.


- So for now, create a VM in us-east1 region where PGA is off. And try to SSH into it.


![gsutil-ls](/GCP_pictures/Study-logs/private-google-access/gsutil-ls.PNG "gsutil ls")



- When you run **gsutil ls** and it works. It is because the default Cloud API access is enabled when creating the VM.


![cloud-api-access](/GCP_pictures/Study-logs/private-google-access/cloud-api-acccess.PNG "Cloud API access scopes")



- Internally, **gsutil** is using this particular UI:


```
storage.googleapis.com
```

- And when you ping the UI, it works. Because the VM has an external IP.


![ping-googleapis](/GCP_pictures/Study-logs/private-google-access/ping-googleapis.PNG "Ping googleapis")



- We will remove this external IP on the running VM. And SSH into it again.


- And when you run **gsutil ls** again, it cannot access:


![gsutil-not-working](/GCP_pictures/Study-logs/private-google-access/gsutil-not-works.PNG "gsutil not working")



- We will edit the subnet where the VM resides in. So that the Private Google Access is on.


![private-google-access-on](/GCP_pictures/Study-logs/private-google-access/private-google-access-on.PNG "Private Google Access on")


- With this Private Google Access, the VM can access all the Google APIs and services through **internal IP address** only inside the same network.


- If you try SSHing and running the command again, now the connection works.


![access-works](/GCP_pictures/Study-logs/private-google-access/access-success.PNG "Access successful")


- But you cannot still ping the same **storage.googleapis.com** because you don't have an external IP address.