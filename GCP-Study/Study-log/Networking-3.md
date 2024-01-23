### [Source of this study material : Google Cloud Professional Network Engineer by Ankit Mistry](https://www.udemy.com/course/google-cloud-networking/)


## Identity Aware Proxy Demo Order

- SSH with just a private IP

- Protect compute engine SSH resources and assign Secured Tunnel User Role



## Identity Aware Proxy Demo

- First, we need to create 2 VMs with and without a public IP.


![2-vms-created](/GCP_pictures/Study-logs/Networkign-Advanced2/2-vms.PNG "2 VMs created")


- In this case, even with the VM without the external IP, we can SSH into it since I have the Owner role in the project.


- There's a difference between gcloud command for SSH into each of the machines.

  - VM with external IP

  ```
  gcloud compute ssh --zone "us-central1-c" "vm-with-external-ip" --project "my-anthos-demo-410923"
  ```


  - VM without external IP

  ```
  gcloud compute ssh --zone "us-central1-c" "vm-without-external-ip" --tunnel-through-iap --project "my-anthos-demo-410923"
  ```

- '--tunnel-through-iap' : with this, one can connect to VM without external IP via IAP.


- Now, as the Owner of this project, we want to provide another user with IAM role so that he/she can access this VM without external IP.


- Go to IAM and click Grand Access. You need to add a new principal (gatsbyflight@gmail.com) and assign him 2 new roles: **Compute Instance Admin** and **Service Account User** roles.


- If you don't assign a service account user role, then the user will get this permission deny message when he tries to SSH into the VM.


![error-msg-without-role](/GCP_pictures/Study-logs/Networkign-Advanced2/service-account-user-role-required.PNG "Service Account User role required")


- So, be sure to add 2 roles to the new user.


![2-roles-assigned](/GCP_pictures/Study-logs/Networkign-Advanced2/add-2-roles.PNG "Add 2 roles to the new user")


- Now, you can SSH into the VM with external IP **as a new user**, but you cannot still SSH into the VM without external IP. 


![ssh-enabled](/GCP_pictures/Study-logs/Networkign-Advanced2/ssh-enabled.PNG "SSH enabled partially for a VM with external IP")


- Go back to your primary account and go to IAM and click Identity Aware Proxy from the menu bar. Then, select the SSH and TCP Resources tab and click the VM resource that you want to give a new user access to.


![identity-aware-proxy](/GCP_pictures/Study-logs/Networkign-Advanced2/identity-aware-proxy.PNG "Identity Aware Proxy forwards TCP traffic safely")


- And assign 'IAP secured Tunnel User' role to the new user and click Save.


![iap-secured-tunnel-user](/GCP_pictures/Study-logs/Networkign-Advanced2/iap-secured-tunnel-user.PNG "IAP Secured Tunnel User")


- Now, switch to the new user account and test the connectivity by SSHing into the VM without external IP. You will be able to access it.


![ssh-success-new-user](/GCP_pictures/Study-logs/Networkign-Advanced2/ssh-success-new-user.PNG "SSHing into the VM is successful")



## Firewall Rulle allowing SSH into VM without External IP

- When you go to IAP and see the SSH and TCP Resources section, you will see a warning sign below the VM resource that you assign the new user access to.


![iap-warning](/GCP_pictures/Study-logs/Networkign-Advanced2/iap-warning.PNG "IAP warning")


- This is because you didn't set the Firewall Rule that **allows all the IAP traffic** to the VM.

- The default Firewall Rule allows all traffic from any source to SSH into the VMs. We want to change this rule to allow only IAP traffic to SSH into the VMs.


![default-firewall-rule](/GCP_pictures/Study-logs/Networkign-Advanced2/default-firewall-rule.PNG "Default firewall rules")


- Go edit this rule and make it disabled.

- After disabling the Firewall Rule, you cannot SSH into VMs even as the Owner.


![connection-failed-without-rule](/GCP_pictures/Study-logs/Networkign-Advanced2/connection-fail-without-rule.PNG "Connection failed without the proper firewall rule in place")


- We need to create a new Firewall Rule that allows only **particular IAP source IP range (35.235.240.0/20)** to SSH into the VMs.


![IAP-source-ip](/GCP_pictures/Study-logs/Networkign-Advanced2/iap-source-ip.PNG "IAP source IP")


- When creating the Firewall Rule (allow-ssh-custom-vpc), be sure to include the source IP range like below:


![firewall-rule-creation](/GCP_pictures/Study-logs/Networkign-Advanced2/firewall-rule-creation.PNG "Firewall Rule creation")


- After creating the Firewall Rule, we are able to SSH into VMs both as the Owner and the IAP Secured Tunnel User.


![ssh-into-vm-with-IAP-firewall-rule](/GCP_pictures/Study-logs/Networkign-Advanced2/ssh-with-firewall-rule.PNG "Able to SSH into VMs both as the Owner and the new user")