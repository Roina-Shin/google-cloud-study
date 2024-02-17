### [Source of this study material : Google Cloud Professional Network Engineer by Ankit Mistry](https://www.udemy.com/course/google-cloud-networking/)


## Cloud VPN 

- Product for connection between your on premise data center with GCP network


- Cloud VPN securely connects your **peer network** to your VPC network through an **IPsec VPN**.


- It works between:

  - Google Cloud & your data center

  - Google Cloud & other public cloud (AWS)

  - Different VPC networks in different projects


- If you want to **quickly** set up connectivity, Cloud VPN is a good choice.


- All traffic is **encrypted** by one VPN gateway and then **decrypted** by the other VPN gateway.


- Traffic here travels over **public Internet**.


- A single Cloud VPN tunnel can support up to **3 Gbps** bandwidth.


- VPC Peering is not transitive in nature. But **Cloud VPN** is transitive.


- What transitive means is, when you peer network A and network B, and then peer network A and network C, the **VPC Peering** only allows for the connection between the **2 networks**.


- Through **Cloud VPN**, you can connect 2 different networks between on premise and GCP environments. Also, when you connect network A and B and then connect network A and network C, network B and network C by default are connected.


![cloud-vpn-overview-1](/GCP_pictures/Study-logs/cloud-vpn/cloud-vpn-overview1.PNG "Cloud VPN Overview 1")


![Cloud-vpn-overview-2](/GCP_pictures/Study-logs/cloud-vpn/cloud-vpn-overview2.PNG "Cloud VPN Overview 2")


- All the packets you want to transfer from GCP network to on premise data center is safely encrypted through Cloud VPN gateway and traverse over public Internet on VPN tunnel.



## Cloud VPN Demo

- GCP to on premise setup is difficult so we will use GCP to GCP setup in this demo.


- In real scenario, it is **not recommended** to use Cloud VPN between GCP and GCP networks. It is costly compared to VPC peering.


- For this demo, we will need 2 environments:

  - Project 1 : us-central1-subnet, allow ssh/icmp, static-us-ip, vm-us, tunnel+gateway creation

  - Project 2 : asia-northeast3-subnet, allow ssh/icmp, static-seoul-ip, vm-seoul, tunnel+gateway creation


- The static IP addresses are for VPN gateways for both sides. For 2 networks to communicate over public Internet, we need external IP address. And we will **bind** this static IP address to each VPN gateway.


- Unlike **dynamic routing Cloud VPN**, you can set the 2 projects in 2 different regions with **classic Cloud VPN**. Cloud Router requires you to create 2 VPCs in the same region to work.


- Now, after you created both VPCs in different projects, create a static external IP for both.


![create-static-ip](/GCP_pictures/Study-logs/cloud-vpn/us-static-ip.PNG "US static IP")


![seoul-static-ip](/GCP_pictures/Study-logs/cloud-vpn/seoul-static-ip.PNG "Seoul static IP")


- Also create VMs in each project in each subnet.


- During VM creation, opt for **None** for external IP address as we don't need one.


![vm-creation](/GCP_pictures/Study-logs/cloud-vpn/vm-creation.PNG "US vm creation")


![seoul-vm-creation](/GCP_pictures/Study-logs/cloud-vpn/seoul-vm-creation.PNG "Seoul vm creation")


- Now, go to VPN page on both projects.


![vpn-ui](/GCP_pictures/Study-logs/cloud-vpn/vpn-ui.PNG "VPN UI")


- For this demo, we will use **classic VPN** which supports static routing.


![classic-vpn](/GCP_pictures/Study-logs/cloud-vpn/classic-vpn.PNG "Classic VPN")


- In the VPN connection creation page, select the network and static IP for the subnet.


![vpn-connection-creation](/GCP_pictures/Study-logs/cloud-vpn/vpn-connection-creation.PNG "VPN connection creation")


- In tunnel configuration, paste the other network's VPN gateway static IP address in the **remote peer IP address**.


![remote-peer-ip](/GCP_pictures/Study-logs/cloud-vpn/remote-peer-ip.PNG "Remote peer IP address")


- And for the remote IP range, enter the other network's subnet range.


```
10.5.0.0/28
```


![remote-ip-range](/GCP_pictures/Study-logs/cloud-vpn/remote-network-ip.PNG "Remote network IP")


- We are going to repeat the same process for the other network VPN connection creation.


![seoul-vpn-creation](/GCP_pictures/Study-logs/cloud-vpn/seoul-vpn-creation.PNG "Seoul VPN creation")


![seoul-tunnel-creation](/GCP_pictures/Study-logs/cloud-vpn/seoul-tunnel-creation.PNG "Seoul tunnel creation")


![seoul-route-options](/GCP_pictures/Study-logs/cloud-vpn/seoul-route-options.PNG "Seoul routing options")


- Now both tunnels are created accordingly.


![us-to-seoul-tunnel](/GCP_pictures/Study-logs/cloud-vpn/us-to-seoul-tunnel.PNG "US to Seoul tunnel")


![seoul-to-us-tunnel](/GCP_pictures/Study-logs/cloud-vpn/seoul-to-us-tunnel.PNG "Seoul to US tunnel")


- Now, if you look into the routes page, you will see that a new route is created. The new route's destination IP range is **the other network's subnet IP range**.


![peek-into-route](/GCP_pictures/Study-logs/cloud-vpn/peek-into-routes.PNG "Peek into routes")


![seoul-to-us-route](/GCP_pictures/Study-logs/cloud-vpn/seoul-to-us-route.PNG "Seoul to US route")


- This **destination IP range** tells us that whenever the request is within this destination IP address, your **next hop** is this VPN tunnel.


![how-route-works](/GCP_pictures/Study-logs/cloud-vpn/how-route-works.PNG "How route works")


- Now, if we try to ping from one VM to another VM, it works.


![ping-works](/GCP_pictures/Study-logs/cloud-vpn/ping-works.PNG "Ping works")



## Static Routing Demo

- For this demo, we will add a new subnet to one of the VPCs. And create a new VM in that subnet and test the connectivity with the VM in other VPC.


- Then we will set up a static route for the subnet and test the connectivity again.


- In my case, I already have the other subnet in the US VPC, so I will use this subnet to create a new VM.


![new-subnet](/GCP_pictures/Study-logs/cloud-vpn/new-subnet.PNG "New subnet")


- I have created a VM in other subnet and SSH into it. If you try to ping the VM in other VPC, it doesn't work. Even if we already set up the VPN connection between 2 networks, the new subnet range should be manually added to **the route in the other network**.


![ping-fail](/GCP_pictures/Study-logs/cloud-vpn/ping-fail.PNG "Ping fails")


- It is because we chose **Route-based routing option** and specified the **remote network IP range** for just one subnet during our VPN setup.


- Now, go to the Seoul network's project and create a new route for the new subnet in the US network.


![new-route](/GCP_pictures/Study-logs/cloud-vpn/add-new-route.PNG "Add new route")


- Immediately after we added the new route, the ping from the US new subnet to the Seoul VM works.


![ping-now-works](/GCP_pictures/Study-logs/cloud-vpn/ping-now-works.PNG "Ping now works")










