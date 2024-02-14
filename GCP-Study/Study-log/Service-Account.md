### [Source of this study material : Google Cloud Professional Security Engineer by Ankit Mistry](https://www.udemy.com/course/google-cloud-gcp-professional-cloud-security-engineer-certification/)


## Service Account

- For non human users like Apps, services


- Service account is identity for compute engine



## Service Account Demo

- Create a service account.


![sa-creation](/GCP_pictures/Study-logs/service-account/sa-creation.PNG "Service account creation")


- For the time being, we are not giving any access or users to this service account. Just click create.


![just-create](/GCP_pictures/Study-logs/service-account/just-create.PNG "Just create a service account")


- Now, go to compute engine and create an instance.


- When creting a service account, be sure to select the demo service account we created.


![select-demo-sa](/GCP_pictures/Study-logs/service-account/select-demo-sa.PNG "Select demo service account")


- Also, create a vVM with the default service account.


![vm-with-default-sa](/GCP_pictures/Study-logs/service-account/vm-with-default-sa.PNG "VM with default service account")


- Then SSH into each of the 2 machines:


```
gcloud auth list
```


- The above command will let you see which account is associated with the VM.


![default-vm-auth](/GCP_pictures/Study-logs/service-account/default-sa-auth.PNG "VM with default SA auth list")


![demo-vm-auth](/GCP_pictures/Study-logs/service-account/demo-sa-auth.PNG "VM with demo SA auth list")


- When you go to the VM with default SA and see details, you see that most of the APIs are disabled under the API and identity management.


![api-and-identity-management](/GCP_pictures/Study-logs/service-account/API-and-identity-management.PNG "API and identity management")


- Actually, this is the legacy way to manage the API access scope. You have to **stop the VM** first to edit this settings. 


- Whereas, if you use the IAM, it is easier to manage the access without stopping the VM.


- To change the API access scope in the VM, we will stop the machine.


- Set access scopes for each API and change the Storage access to **none**. (In default setting, it is read only)


- After saving it, SSH into the VM.


```
gsutil ls
```


- If you run the command, you will see that the access is denied.


![access-denied](/GCP_pictures/Study-logs/service-account/access-denied.PNG "Access denied")


- And this access scope is only available for VM with **default service account**. If you choose a custom service account for your VM, then this access scope option is not available.


- This time, when you go to the VM with custom SA, you will see that **API scope access is set to all cloud APIs**.


- SSH into the VM. Run the **gsutil ls** command.


![gsutil-denied](/GCP_pictures/Study-logs/service-account/gsutil-denied.PNG "gsutil ls access denied")


- To fully utilize the VM to access APIs, you need to go to IAM section.


- There, we can grant the service account with the **storage admin** role.


![storage-admin-sa](/GCP_pictures/Study-logs/service-account/storage-admin-sa.PNG "Storage Admin SA")


- After you update the IAM policy, go back to the VM and run the command again:


```
gcloud storage buckets create gs://BUCKET_NAME --location=BUCKET_LOCATION
```


```
gsutil ls
```


```
gcloud storage rm --recursive gs://BUCKET_NAME
```


- Now, the VM can create, list, and even delete the bucket.


![bucket-operations](/GCP_pictures/Study-logs/service-account/bucket-operations.PNG "Bucket operations")


- In the IAM section, now, grant a new user with **compute admin** and **service account user** role.


- Now, if you switch the account to the new user and go inside the compute engine, you can see the list of VMs.


![list-of-vms](/GCP_pictures/Study-logs/service-account/list-of-vms.PNG "List of VMs")


- When you SSH into one of the VMs, you can do various operations there:


![new-user-operations](/GCP_pictures/Study-logs/service-account/new-user-operations.PNG "New user operations")


- Now, we go to Service Account section again and grant the new user with the **Service Account Token Creator** role.


- Also, delete all the permissions given to the new user previously. So that we will see how this **Service Account Token Creator** role works.


![service-account-token-creator](/GCP_pictures/Study-logs/service-account/service-account-token-creator.PNG "Service Account Token Creator role")


- Then give the service account **compute admin** role.


![compute-admin-to-sa](/GCP_pictures/Study-logs/service-account/compute-admin-to-sa.PNG "Compute Admin to SA")


- We are going to **impersonate this service account** as a new user.


- Now, the new user's only role is **Service Account Token Creator**.


![new-user-only-role](/GCP_pictures/Study-logs/service-account/new-user-only-role.PNG "New user's only role")


- It doesn't have any role assigned in both the project and organization level.


![project-level-iam](/GCP_pictures/Study-logs/service-account/project-level-iam.PNG "Project level IAM")


![organization-level-iam](/GCP_pictures/Study-logs/service-account/organization-level-iam.PNG "Organization level IAM")


- Now in the new browser change the project to a new one **under the same organization** and switch the account as the new user.


- And run the following commands:


```
gcloud config unset project
```


```
gcloud compute instances list --project [project where the SA lives]
```


- Then you will get error as the new user doesn't have **compute admin** role. But if you impersonate the service account with the **compute admin** role as the new user, you can do the same operation.


![error-without-permission](/GCP_pictures/Study-logs/service-account/error-without-permission.PNG "Error without permissions")


- Run the following command to impersonate the service account:


```
gcloud compute instances list --project [project name] --impersonate-service-account [service-account-address]
```


![impersonate-sa-success](/GCP_pictures/Study-logs/service-account/impersonate-sa-success.PNG "Impersonate SA successfully")


- With impersonation, the new user successfully listed the compute engine resources.



## Service Account RSA Private Key

- Like Google Account has password, service account has keys.


- Keys can be used for authentication purposes.  


- To test this, we will first generate keys in the service account.


![generate-key-for-sa](/GCP_pictures/Study-logs/service-account/generate-key-for-sa.PNG "Generate key for SA")


- Anyone who has the key file can have a full control on the service account.


- When you downloaded the key file, rename it to a simple name like **key.json**.


- If you open the file, you can see the service account email and the private key itself.


- Now go to your **personal GCP account** and open one project to start a Cloud Shell.


- First, unset the project inside the cloud shell:


```
gcloud config unset project
```


- Then upload the service account key file.


- After you upload the file, run the command to verify the current active account:


```
gcloud auth list

```


- As this is the personal GCP account, the active account is also a personal account. So we will activate our organization service account here by running:


```
gcloud auth activate-service-account --key-file=key.json
```


- Now if you run the command **gcloud auth list**, the active account is the service account we just set.


![active-service-account](/GCP_pictures/Study-logs/service-account/active-service-account.PNG "Active service account")


- And if you run the following command, you will see that the service account as **compute admin** can implement the task:


```
gcloud compute instances list --project [project where the service account lives]
```


![sa-with-key-operations](/GCP_pictures/Study-logs/service-account/sa-with-key-operations.PNG "SA with key file can do operations in other account/project")


- Whenever the key is compromised, you can simply delete the key in the service account page.


