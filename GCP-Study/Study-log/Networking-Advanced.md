### [Source of this study material : Google Cloud (GCP) Masterclass 2024 by Cloud99](https://www.udemy.com/course/google-cloud-specialization/)


## Network Firewalls in GCP

- First, go to VPC Networks and click Create a VPC Network.

- Give it a name and create 3 subnets:

  - 1 for web server (IPv4 range: 10.0.1.0/24)

  - 1 for database (IPv4 range: 10.0.2.0/24)

  - 1 for service (IPv4 range: 10.0.3.0/24)


![new-vpc-creation](/GCP_pictures/Study-logs/Networking-Advanced/new-vpc-creation.PNG "New VPC creation")


- Now, a new VPC including 3 subnets is created:


![new-vpc-created](/GCP_pictures/Study-logs/Networking-Advanced/new-vpc-created.PNG "New VPC created")


- Then we will go to compute engine and create a new VM machine.


- We will create a db VM first that has a corresponding region to the VPC subnet for db we created.


![db-vm-creation](/GCP_pictures/Study-logs/Networking-Advanced/create-vm-db.PNG "Create a new VM for db")


- Make sure to choose the VPC and subnet we created for this specific instance:


![choose-vpc-and-subnet](/GCP_pictures/Study-logs/Networking-Advanced/choose-vpc-and-subnet.PNG "Choose the VPC and subnet for the instance")


- Create the other 2 VMs for web server and service accordingly.


![3-vms-created](/GCP_pictures/Study-logs/Networking-Advanced/3-vms-created.PNG "3 VMs created")


- Once done, we can SSH into either of VMs and ping the internal IP of other VMs as there are firewall rules in place (that I configured earlier when I created a VPC) for SSH and ICMP:


![firewall-rules-ssh](/GCP_pictures/Study-logs/Networking-Advanced/firewall-rules-ssh.PNG "Firewall rule in place for SSH")


## How to create a Cloud VPN

- What we will do for this section:

  - create 2 custom VPC networks

  - create firewall rules in both VPCs

  - create instance each using one VPC

  - verify connectivity

  - create 2 VPNs for each network

  - create static IP for each network

  - set forwarding rules for each VPN Gateway

  - create tunnel between each Gateway

  - create route for each network

 
 - To create VPCs, go to VPC Networks and click Create New VPC Networks.

   - custom-vpc-1 / subnet-us-central1 / IPv4: 10.5.5.0/24

   - custom-vpc-2 / subnet-us-east1 / IPv4: 10.6.5.0/24


  ![2-vpc-created](/GCP_pictures/Study-logs/Networking-Advanced/2-vpc-created.PNG "2 VPCs created")


 - Then go to the Compute Engine and create 2 VMs each of which uses different custom VPC networks.


  ![vpn-2-vms-created](/GCP_pictures/Study-logs/Networking-Advanced/vpn-2-vms-created.PNG "For VPN test, 2 VMs created")


 - To verify the connectivity between the 2 VMs, SSH into one of them and ping the other VM:


  ![ping-access-denied](/GCP_pictures/Study-logs/Networking-Advanced/ping-access-denied.PNG "Ping access denied")


 - As expected, the VMs cannot communicate with each other using **internal IPs** because they are in different VPCs.


 - Now, to set up the connectivity between the two using **VPN**, go to the cloud shell:

```
gcloud compute target-vpn-gateways create central-east-vpn --network <NETWORK-NAME> --region <SUBNET-REGION>
```

 - Once done, you get the message that the VPN is created:


  ![vpn-created](/GCP_pictures/Study-logs/Networking-Advanced/vpn-1-created.PNG "VPN from central to east is created")


 - After that, you need to create a **static IP** to attach to your VPN.

```
gcloud compute addresses create --region <SUBNET-REGION> <STATIC-IP-NAME>
```


  ![static-ip-1-created](/GCP_pictures/Study-logs/Networking-Advanced/static-ip-1-created.PNG "1 Static IP is created")



 - To verity that a static IP is created:


 ```
 gcloud compute addresses list
 ```


  ![address-list](/GCP_pictures/Study-logs/Networking-Advanced/address-list.PNG "gcloud compute addresses list")



 - Now, we will create a forwarding rule using the command:


```
gcloud compute forwarding-rules create <RULE-NAME> --region <STATIC-IP-REGION> --ip-protocol ESP --address <YOUR-STATIC-IP-ADDRESS> --target-vpn-gateway <GATEWAY-NAME (vpn name)>
```


  ![forwarding-rule-created](/GCP_pictures/Study-logs/Networking-Advanced/forwarding-rule-created.PNG "Forwarding rule created")



 - Again, list out your address:


```
gcloud compute addresses list
```

 - Then you will see the static IP address is now in use by the VPN we created.


  ![static-ip-address-used-by-vpn](/GCP_pictures/Study-logs/Networking-Advanced/static-address-used-by-vpn.PNG "Static IP address is now in use by the VPN")


 - Now, we will add another forwarding rule for UDP on port 500:


```
gcloud compute forwarding-rules create <RULE-NAME> --region <STATIC-IP-REGION> --ip-protocol UDP --ports 500 --address <YOUR-STATIC-IP-ADDRESS> --target-vpn-gateway <GATEWAY-NAME (vpn name)>
```


  ![another-forwarding-rule-created](/GCP_pictures/Study-logs/Networking-Advanced/another-forwarding-rule-created.PNG "Another forwarding rule is created")


- We will add yet another forwading rule for UDP on port 4500:

```
gcloud compute forwarding-rules create <RULE-NAME> --region <STATIC-IP-REGION> --ip-protocol UDP --ports 4500 --address <YOUR-STATIC-IP-ADDRESS> --target-vpn-gateway <GATEWAY-NAME (vpn name)>
```

- Once done, let's list out all the forwarding rules:


```
gcloud compute forwarding-rules list
```


  ![forwarding-rules-list](/GCP_pictures/Study-logs/Networking-Advanced/forwarding-rules-list.PNG "Forwarding Rules list")


- Now, we need to create another VPN for the other VPC network by following the same procedures we took earlier.


- After you have done all the steps, it's time to create **VPN tunnels** for each VPN.


```
gcloud compute vpn-tunnels create <TUNNEL-NAME> --peer-address <STATIC-IP-SECOND-GATEWAY> --region <REGION-FIRST-GATEWAY-SUBNET> --ike-version 2 --shared-secret <SECRET> --target-vpn-gateway <FIRST-VPN> --local-traffic-selector 0.0.0.0/0 --remote-traffic-selector 0.0.0.0/0
```


  ![vpn-tunnel-created](/GCP_pictures/Study-logs/Networking-Advanced/vpn-tunnel-created.PNG "VPN tunnel created for VPN 1")


- Do the same thing to create the other VPN tunnel for VPN 2.


  ![2-tunnels-created](/GCP_pictures/Study-logs/Networking-Advanced/2-tunnels-created.PNG "2 VPN tunnels created on GCP console")


- Finally, we need to create **routes** for the traffic between the 2 VPNs to follow.


```
gcloud compute routes create <ROUTE-NAME> --network <SOURCE-NETWORK> --next-hop-vpn-tunnel <FIRST-TUNNEL> --next-hop-vpn-tunnel-region <FIRST-TUNNEL-REGION> --destination-range <SECOND-NETWORK-SUBNET>
```


  ![vpn-route-created](/GCP_pictures/Study-logs/Networking-Advanced/vpn-route-created.PNG "VPN route created for VPN 1")


- Likewise, do the same thing to create the VPN route for VPN 2.


  ![vpn-route-2](/GCP_pictures/Study-logs/Networking-Advanced/vpn-route-2.PNG "VPN route 2 created for VPN 2")



- Now, all preparations are done for the 2 instances in different VPCs to communicate with each other!

- Go to VM instances and SSH into one of them.


  ![ping-successful](/GCP_pictures/Study-logs/Networking-Advanced/ping-successful.PNG "Ping is successful!")





** **Further study** - why do we use UDP protocol and port 500 / 4500 for the VPN connection?


- UDP port 500 is the ISAKMP port for establishing PHASE 1 of IPSEC tunnnel.

 

VPN-GW1-------nat rtr--------------------------------natrtr----------VPNGW2.

 

If two vpn routers are behind a nat device or either one of them, then you will need to do NAT traversal which uses port 4500 to successfully establish the complete IPSec tunnel over NAT devices.



- As stated, UDP 4500 is being used as ESP (IP protocol 50)  packet do not have a layer 4 information. ESP encrypts all critical information for your IPSEC traffic. However, since it doesn't have any layer 4 information (tcp, udp port) it will be dropped by devices that do PAT (packet can't be assigned a unique port and therefore PAT will fail)


Nat-t does 2 things


1) detect both peers support that function (NAT-T)

2) detect if there is a device in the transmission path that does nat

 

In simple steps what will happen is that traffic will be encrypted inside the ESP packet  and then the ESP packet will be encapulated inside a UDP/4500 packet. As a result ESP packets can now be translated via a PAT device


Please note that you can also use IPSec-over-UDP  or IPSec-over-TCP (work similarly but there are some differences)


- Most of the companies in today's date uses PAT to reduce the cost of buying more public IPs, to allow its internal users to access the public Internet. PAT is done on the basis of port numbers, where the source port of the inside traffic is mapped to a different port, so that, all the inside users should be able to access the public Internet with the help of few public IPs.

 

ESP/AH being a L3 protocol doesn't have a port number, rather it has a protocol number ( IP 50/51 respectively). & if please note that, UDP 500 is for ISAKMP & not for esp/ah. Remember, port number is only for those protocols who has there own transport (L4) mechanism, for example, RIP, BGP.

 

So, while dealing with NATing device in the transit path of the vpn tunnel, the packet will get dropped if PAT is configured. Therefore, to allow that traffic to pass thru NAT, according to the defined standards, every device should allow & process UDP4500 if NAT-T is detected, & the esp/ah packet is re-encapsulated with the port UDP4500, allowing the esp/ah inside traffic to successfully pass thru tunnel as well as thru NAT, so encryption (traffic thru IPSec tunnel) as well as NATing (hiding the inside IP) is acheived.

 

And UDP 500 is for ISAKMP which is used to negotiate the IKE Phase 1 in IPSec Site-to-Site vpn & is default port number for isakmp, used when there is no NATing in the transit path of the vpn traffic.

 

This is why we need UDP 4500.



