### [Source of this study material : Google Cloud Professional Network Engineer by Ankit Mistry](https://www.udemy.com/course/google-cloud-networking/)


## Cloud NAT

- NAT - Network Address Translation


- How can you **sudo apt update** with just internal IP address from GKE private cluster?


- How to access with **internal IP**:

  - GCS services (**Private Google Access**)

  - Cloud SQL, Vertex AI, Memory Store (**Privte Service Access**)

  - sudo apt update (**Need external IP**)

  - Reach anywhere on Internet (**Need external IP**)


- **Cloud NAT** is the solution which allows VM to connect with Internet without external IP.


- Cloud NAT is bound to VPC (region).


## Cloud NAT Demo

- First, check your VPC and subnets. In my VPC in the project, I have a subnet in us-east1.


![us-east-subnet](/GCP_pictures/Study-logs/cloud-nat/us-east-subnet.PNG "us east subnet")


- Then create a VM within the subnet **without internal IP address**.


![vm-creation](/GCP_pictures/Study-logs/cloud-nat/vm-creation.PNG "VM creation")


- When you SSH into it and run **gsutil ls**, it's not working as we didn't have **Private Google Access** on in the subnet.


![gsutil-not-working](/GCP_pictures/Study-logs/cloud-nat/gsutil-not-working.PNG "gsutil not working")


- And when you ping **google.com**, it doesn't work either as we don't have external IP.


![ping-not-working](/GCP_pictures/Study-logs/cloud-nat/ping-not-working.PNG "Ping not working")


- **sudo apt update** doesn't work either for the same reason.


- Go to Network Services and to the Cloud NAT.


![what-cloud-nat-does](/GCP_pictures/Study-logs/cloud-nat/what-cloud-nat-does.PNG "What Cloud NAT does")


- The text says the Cloud NAT gateway is region specific.


![cloud-nat-retion](/GCP_pictures/Study-logs/cloud-nat/cloud-nat-gateway.PNG "Cloud NAT Gateway is region specific")


- Also, create a Cloud Router. NAT Gateway connects your subnet to the Cloud Router, a virtual router that connects to the Internet and other VPC networks.


![cloud-router-creation](/GCP_pictures/Study-logs/cloud-nat/cloud-router-creation.PNG "Cloud Router creation")


- You can also choose whether to go with static IP address or automatically allocated IP address.


![automatic-ip-address](/GCP_pictures/Study-logs/cloud-nat/choose-automatic-ip.PNG "Automatic IP address")


- Now, the Cloud NAT gateway and Cloud Router are set up. Also, try to ping some address in the nat demo VM.


![gateway-set-up](/GCP_pictures/Study-logs/cloud-nat/nat-gateway-provisioned.PNG "NAT Gateway provisioned")


![ping-started-working](/GCP_pictures/Study-logs/cloud-nat/ping-started-working.PNG "Ping started working")


