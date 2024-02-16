### [Source of this study material : Google Cloud Professional Network Engineer by Ankit Mistry](https://www.udemy.com/course/google-cloud-networking/)


## Shared VPC

- Assume that you have organization and you are running multiple projects inside the org.


- We have Project 1 and Project 2. And Project 1 has a custom VPC and the resource in Project 2 wants to use the custom VPC in Project 1.


- The **shared VPC** is maintained inside one project and the resources in other projects can use the same VPC.


- It's the **host project** where the **shared VPC** resides in.


- They are the **service projects** that are using the **shared VPC**.


- This way, we can achieve the central management of VPC.


- Generally, large organizations use this **shared VPC** where they have a dedicated network engineer team.


- Shared VPC is only available for projects within **an organization node**.



## Shared VPC Demo

- First, we will create a host project.


- Then we will create 2 service projects.


- Next, we will share the VPC of the host project with service projects.


- Our **host project** will be SRE project.


- And I have created **Service project 1** and **Service project 2**.


- Move to the SRE project and search for **shared VPC**.


![shared-vpc-ui](/GCP_pictures/Study-logs/shared-vpc/shared-vpc-ui.PNG "Shared VPC UI")


- But if you try to **enable the host project** it gets error because of insufficient permissions.


![permission-error](/GCP_pictures/Study-logs/shared-vpc/permission-error.PNG "Permission error")


- Grab the required permission and search it in the IAM roles.


![search-role](/GCP_pictures/Study-logs/shared-vpc/search-role.PNG "Search role")


- Copy the **Compute Shared VPC Admin** role, and change the node to **organization level**.


- And give the permission to the current user (which is the owner) at the **organization node**.


![owner-given-role](/GCP_pictures/Study-logs/shared-vpc/owner-given-role.PNG "Permission given to the current user")


- After updating the policy, if you try again, enabling host project now works.


![enable-host-project](/GCP_pictures/Study-logs/shared-vpc/enable-shared-vpc.PNG "Enable host project")


- Then choose the subnets you want to share with. Use the arrow button to find the custom VPC subnets and share them.


![select-2-subnets](/GCP_pictures/Study-logs/shared-vpc/select-2-subnets.PNG "Select 2 subnets")


- The next step is to choose the projects to share the VPC with:


![to-which-subnet](/GCP_pictures/Study-logs/shared-vpc/to-which-projects.PNG "To which projects to share the VPC")


- The last step is to select the users in service projects to be given **Compute Network User** role.


![selected-users](/GCP_pictures/Study-logs/shared-vpc/selected-users.PNG "Selected users")


- Now, the shared VPC is set up with 5 respective users in the service projects with the permissions.


![shared-vpc-setup](/GCP_pictures/Study-logs/shared-vpc/shared-vpc-setup.PNG "Shared VPC set up")


- Go to the Service Project 1 and create a VM with the shared VPC network.


![vm-creation-shared-vpc](/GCP_pictures/Study-logs/shared-vpc/vm-creation-shared-vpc.PNG "VM creation with shared VPC")


- In the Service Project 2, the VM can choose the shared VPC network.


![service-vm-2](/GCP_pictures/Study-logs/shared-vpc/service-vm-2.PNG "Service VM 2")


- If I try to ping the other machine in Service Project 1, it works as the two VMs now lives in the same shared VPC.


![ping-works](/GCP_pictures/Study-logs/shared-vpc/ping-vm-success.PNG "Pinging works")







