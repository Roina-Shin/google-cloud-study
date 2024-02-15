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


![tunnel-creation](/GCP_pictures/Study-logs/Networking-Advanced3/tunnel-creation.PNG "Tunnel creation was possible only after I had changed so that the 2 VPNs live in the same region")


- Here, you can see the 2 VPN interfaces: 1 is from this VPN gateway and 1 is from the other (peer) VPN gateway. So, these 2 are associated to form this VPN tunnel. And we need to set this up 2 times as we have 2 tunnels created for this HA VPN setup.


![2-vpn-interfaces](/GCP_pictures/Study-logs/Networking-Advanced3/vpn-tunnel-establishment.PNG "2 VPN gateways are associated for a tunnel")



- Once done, **go to your another project** and finish the same process for Tunnel creation.


- Now, we have 2 BGP sessions to configure for both Tunnels!


![bgp-sessions-config](/GCP_pictures/Study-logs/Networking-Advanced3/bgp-sessions-config.PNG "BGP Sessions config")


- Click Configure BGP Session on the far left side. Inside the config panel, opt for 'Manually' when you allocate BPG IPv4 address and take the Google suggested IP address for each Cloud Router BGP IPv4 and peer IPv4 addresses.


![bgp-session-config-router](/GCP_pictures/Study-logs/Networking-Advanced3/bpg-config-router.PNG "The Cloud Router BGP IPv4 and peer addresses")


- On the other side of the BPG Session config, opt for 'Automatically' when you allocate BGP IPv4 address.


- Now, we have 2 tunnels created accordingly:


![2-tunnels-created](/GCP_pictures/Study-logs/Networking-Advanced3/2-tunnels-created.PNG "2 Tunnels created")



- Let's move on to the other project's BGP session config and do the same thing except:

  - The Cloud Router BGP IPv4 and peer addresses are the opposite for this case as you set **manually** in the previous project.


![another-bgp-config](/GCP_pictures/Study-logs/Networking-Advanced3/aonther-bgp-config.PNG "Another BGP config and the Cloud Router addresses are opposites")



- Now for the second BGP session for your another project, it's **important** that you again set the BGP IPv4 address allocation as **manually** and select the automatically created BGP IP addresses of the first project.


![bgp-address-selection](/GCP_pictures/Study-logs/Networking-Advanced3/bgp-address-another-project.PNG)


- If you look at the first project's automatically created BGP addresses like below, they now become another project's BGP address and peer address.


![automatic-bgp-address](/GCP_pictures/Study-logs/Networking-Advanced3/automatic-bgp-address.PNG "Automatically created BGP addresses of the first project")


- If you save and continue, you will see the summary of your BGP sessions configured for another project as well.


![bgp-session-summary](/GCP_pictures/Study-logs/Networking-Advanced3/bgp-session-configured.PNG "BGP sessions configured for another project")


- Now, if I go and check, only automatically created BGP session and tunnel are established. (So maybe when you create a BGP session, automatic BGP IP assignment could be a better choice.)


![only-automatic-BGP-ips-established](/GCP_pictures/Study-logs/Networking-Advanced3/only-automatic-bgp-ips-established.PNG "Only automatically created BGP IPs are established")


- I can now go and ping the other VM in another project. The ping was anyway successful that otherwise would have been impossible.


![ping-successful](/GCP_pictures/Study-logs/Networking-Advanced3/ping-successful.PNG "Ping successful")


- When we go to the first project and check the Routes, it shows a new dynamic route whose **destination IP range** is the other project's VPC subnet IP ranges.


![first-project-routes](/GCP_pictures/Study-logs/Networking-Advanced3/first-project-routes.PNG "First Project - Routes")


- Now to see the real power of the Cloud Router, we are going to introduce a new subnet in the first project's VPC.


![new-subnet-created](/GCP_pictures/Study-logs/Networking-Advanced3/new-subnet-created.PNG "New subnet created for the first project")


- When you go to another project's Routes, you will see that a new route for the subnet we just created is now present.


![another-project-routes](/GCP_pictures/Study-logs/Networking-Advanced3/another-project-routes.PNG "Another project's routes")


- To sum up, whenever you create or delete a subnet in each of the VPCs, **the Cloud Router will automatically update your routes**.


- **(IMPORTANT)** The reason why you can only add subnets in the same region as the VPC region for the Cloud Router is because of this.

  - **Dynamic Routing Mode** when creating your VPCs was set to **regional**.

  - If you change the regional to the **global** in your VPC edit page, then you can create a subnet in different regions and the Cloud Router will dynamically learn the change and update the routes.