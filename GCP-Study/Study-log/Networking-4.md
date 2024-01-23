### [Source of this study material : Google Cloud Professional Network Engineer by Ankit Mistry](https://www.udemy.com/course/google-cloud-networking/)


## Cloud Router

- **Cloud Router** is a fully distributed and managed Google Cloud service that uses the **Border Gateway Protocol (BGP)** to advertise IP address ranges.

- Router detects all changes an create new optimal routes like Google Maps.

- It makes intelligent decision and exchange information in network.

- It has the ability to discover remote networks.

- Also, it is able to find the new best path if the current path is no longer available.


![cloud-router-structure](/GCP_pictures/Study-logs/Networking-Advanced3/cloud-router-structure.PNG "Cloud Router Structure")


- If a new subnet is added to the office network, then with the help of **BGP**, Cloud Router will do the necessary update of the new routes on the GCP side.


- I have 2 different projects and in each of them lives a different VPC. The first 2 pair of Projects is one I created earlier. And I got an error during the VPN Tunnel creation, so I changed it back to the second pair of Projects. For the Cloud Router to work, the 2 VPCs should be in **the same region**.

  - **Project 1**: uscentral-vpc, subnet ip: 10.0.0.0/24

  - **Project 2**: useast-vpc, subnet ip: 192.168.0.0/24

  - **Project 1**: **uscentral-vpc-1**, subnet ip: 10.0.0.0/24

  - **Project 2**: **uscentral-vpc-2**, subnet ip: 192.168.0.0/24


![vm1-vpc1](/GCP_pictures/Study-logs/Networking-Advanced3/vm1-vpc1.PNG "VM 1 in VPC 1 created")


![vm2-vpc2](/GCP_pictures/Study-logs/Networking-Advanced3/vm2-vpc2.PNG "VM 2 in VPC 2 created")


- Now, it's time to create a Cloud Router. Go create a Cloud Router for each VPC in each project.


![create-router](/GCP_pictures/Study-logs/Networking-Advanced3/create-router.PNG "Router creation")


- Next, we will create a VPN gateway and VPN Tunnels. Go to VPN and click Create VPN Gateway. Go with the **HA VPN**. HA VPN supports only dynamic routing and that is what we are after with the Cloud Router.


- After you created a new VPN gateway, do not proceed with the VPN Tunnel creation yet. Instead, go to another project's VPN page and create a peer VPN gateway so that we can connect them together.


![vpn-gateway-created](/GCP_pictures/Study-logs/Networking-Advanced3/vpn-gateway-created.PNG "VPN gateway created")


- And due to this High Availability mode, the VPN will automatically reserve 2 static IP address (without the need for manually reserving a static IP address).


- Now, it's time to create a VPN Tunnel for both VPN gateways.

- **WARNING** And I got an error during the Tunnel creation because I couldn't select the corresponding VPN gateway from the Project. And the reason was the region is different from the VPN gateway region I was working on. So I changed it so that they have the same region. (us central)




