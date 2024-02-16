### [Source of this study material : Google Cloud Professional Network Engineer by Ankit Mistry](https://www.udemy.com/course/google-cloud-networking/)


## VPC Peering

- No central management


- VPC managed by individual project teams & control all ingress/egress traffic


- Use case:

  - Project 1 (Ecommerce App) wants to communicate with Project 2 (ML Services App) for sentiment analysis


- Peering works for:

  - 2 different VPCs in the same project

  - 2 different VPCs in 2 different projects in the same org

  - 2 different VPCs in 2 different projects in different orgs



## VPC Peering Demo between 2 different projects within the same org

- I have already created a custom VPC with 3 subnets (us-east1, us-central1, asia-southeast1)


![custom-vpc](/GCP_pictures/Study-logs/vpc-peering/custom-vpc.PNG "Custom VPC")


- Also, quickly create a VM within one of the subnets in the VPC.


![vm-creation](/GCP_pictures/Study-logs/vpc-peering/vm-creation.PNG "VM creation")


- Meanwhile, create another VPC in the other project.


![another-vpc](/GCP_pictures/Study-logs/vpc-peering/another-vpc.PNG "Another VPC")


- Also, create a VM in another VPC in the other project.


![vm-creation2](/GCP_pictures/Study-logs/vpc-peering/vm-creation2.PNG "VM creation 2")


- Now, if you try **Data VM** in one project to talk to the **Devops VM** in the other project with **internal IP**, it's not going to work.


- With **external IP** it's going to work. 


- But to secure your application, using internal IP address is recommended.


- SSH into Data VM and Devops VM.


- Run **ip a** and see what internal IP addresses are.


![ip-a](/GCP_pictures/Study-logs/vpc-peering/ip-a.PNG "ip a command")


- And when you ping each other from 2 VMs, it doesn't work.


- Now, we are going to establish the link between the 2 VPCs.


- Go to VPC Network and go to VPC peering.


![vpc-peering-ui](/GCP_pictures/Study-logs/vpc-peering/vpc-peering-ui.PNG "VPC Peering UI")


- Click create a connection and select the peered project ID and network name.


![vpc-peering-connection](/GCP_pictures/Study-logs/vpc-peering/vpc-peering-creation.PNG "VPC peering creation")


- Now, you've created a peering for Data VPC, but the status is inactive. You need to establish the peering connection **on both sides**.


![status-inactive](/GCP_pictures/Study-logs/vpc-peering/status-inactive.PNG "Status inactive")


- Create the other side VPC peering connection as well.


![another-peering](/GCP_pictures/Study-logs/vpc-peering/another-peering.PNG "Another peering")


- But the connection failed as I have created **the same subnet range (10.0.3.0/28) for both VPC subnets**. 


![connection-failed](/GCP_pictures/Study-logs/vpc-peering/connection-failed.PNG "Connection failed")


- I've deleted the duplicate subnet range in one VPC and created one with different subnet range.


![new-subnet](/GCP_pictures/Study-logs/vpc-peering/new-subnet.PNG "New subnet")


- And I try to create the VPC peering in the Devops Project once again.


- This time, the status is active.


![status-active](/GCP_pictures/Study-logs/vpc-peering/status-active.PNG "Status active")


- If you go back to the SSH windows of both VMs in different VPCs of different project, the ping now works!


![ping-working](/GCP_pictures/Study-logs/vpc-peering/ping-working.PNG "Ping works")


