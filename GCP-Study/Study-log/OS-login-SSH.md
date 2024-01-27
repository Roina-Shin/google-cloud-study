## OS Login Setup

- **OS Login** is a feature through which you can SSH into your virtual machine on your local system or outside the project where the VM operates without generating public SSH keys.


1. In your project, go to the IAM section and click Service Accounts.


![sa-creation](/GCP_pictures/Study-logs/os-login/sa-creation.PNG "Service Account creation")


2. There, create a service account without any role or service account users assigned to it. This is the service account that we will use to set up our virtual machine.


3. Choose the service account that you configured earlier during the VM creation.


![choose-service-account](/GCP_pictures/Study-logs/os-login/choose-service-account.PNG "Choose a service account")


4. In the Metadata section of your VM configuration, add the 'enable-oslogin', 'TRUE' pair to it.


![metadata-oslogin](/GCP_pictures/Study-logs/os-login/metadata-oslogin.PNG "Metadata os login")


5. Now, grant a new user or a user outside of the project a new role: either **Compute OS Admin Login** or **Compute OS Login**


![os-login-role](/GCP_pictures/Study-logs/os-login/grant-new-user.PNG "Assign a new user the Compute OS Login role")


6. Then go to the Service Accounts and add the new user to the service account as the Service Account User:


![service-account-user](/GCP_pictures/Study-logs/os-login/service-account-user.PNG "Service account user")


7. You can test the SSH into the VM by using the Google Cloud SDK with the new user identity.


8. This is the command you need to use in either of the shell:


```
gcloud compute ssh --project [project-name]  --zone [your-vm-zone]  [your-vm-name]
```


![gcloud-sdk-demo](/GCP_pictures/Study-logs/os-login/gcloud-sdk-demo.PNG "OS Login successful with Google Cloud SDK")


