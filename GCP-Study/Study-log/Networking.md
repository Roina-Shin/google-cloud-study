### [Source of this study material : Google Cloud Platform from Zero to Hero by Memi Lavi](https://www.udemy.com/course/google-cloud-platform-from-zero-to-hero-the-complete-guide/)


Networking knowledge is what makes a good cloud architect.

We'll cover 4 networking cloud services:

  - VPC

  - Subnets

  - Firewall

  - Laod balancer


## VPC

 - VPC stands for Virtual Private Cloud.

 - This is a network in which you can deploy cloud resources.

 - Many cloud resources by default are deployed within VPC.

   - VMs and load balancers

 - There are also many cloud resources that are not by default deployed in VPC.

   - App Engine, Cloud SQL, and more

 - Resources in VPC can communicate with each other by default.

 - In general, you can think of it as your organization's private network.

 - VPCs are basically free and there is a limit of 15 VPCs that you can create per project.


## Characteristics of VPC

 - VPCs are automatically created per project.

 - Can be connected via peering.

 - VPCs are segmented using subnets.

 - VPCs are projected using firewall rules.

 - The most important thing to think about when designing networkig is:

   - How to limit access to the resources in the VPC so that risk is minimized.


## Subnet

 - Subnet is a logical segment in the VPC.

 - It has its own IP range.

 - Subnet is used as a logical group of resources in the VPC.

 - Subnet is a must. Resources must be placed in a subnet and cannot be placed directly in a VPC.

 - Resources in a subnet can talk to resources in other subnets in the same VPC.

 - Similar to VPCs, subnets are free. 

 - New VPCs are created using one of two modes:

   | Auto Mode | Custom mode |
   | ------ | ----------- |
   | One subnet from each region is automatically created   | No subnets are created automatically |
   | Subnets are automatically assigned IP range | Full control on subnets and IP ranges |
   | Ranges fit within the 10.128.0.0/9 CIDR blcok | If you plan to connect the VPC to other VPCs, it is preferred mode |
   | When new regions are added, new subnets are automatically added | Good when you have no need for subnets in every region |

 - Auto mode is useful when you want to have a subnet in every region.

 - Custom mode is a preferred for production scenarios. It's a good idea to have a full control of networking structure in production.


## CIDR Notation

 - CIDR stands for Classless Inter-Domain Routing.

 - It's a method for representing an IP range.

 - Composed of an address in the range and a number between **0 and 32**.

 - The smaller the number is, the larger the range. See the example IP address below:


 ![CIDR_range](/GCP_pictures/Study-logs/Networking/CIDR_range.PNG "CIDR notation example")


 - Each number 109, 186... is of 8 bits. And 8 bits is a binary number composed of eight digits (e.g. 00000000 = 0, 11111111 = 255)

 - The minimum number is 0 and maximum number is 255.

 - When we put the number 24 after the IP address in CIDR notation, it means that **24 bits are allocated to the address**.

 - And this leaves **8 bits to the range**, because the total bits we have in IP address is 32.  (8 + 8 + 8 + 8 = 32 bits)

 - What 8 bits allocated to the range means is, 

   > **109.186.149.000 - 109.186.149.255**  (256 addresses)

 - We have a total of 256 addresses that we can use.


 ![CIDR_range](/GCP_pictures/Study-logs/Networking/CIDR_range_2.PNG "CIDR notation example 2")


 - In this case, we have 65,536 addresses.

   > **109.186.000.000 - 109.186.255.255** (65,536 addresses)

 

## A look at VPC

 
 ![default-vpc-mode-auto](/GCP_pictures/Study-logs/Networking/default-vpc-mode-auto.PNG "The default VPC is auto mode")


 - When you create a project, this default VPC is automatically created.

 - Also see that the mode of the VPC is **auto**.

 - Subnets were also automatically created in each region of the cloud (42).




 ![vpc-subnets-ip-ranges](/GCP_pictures/Study-logs/Networking/vpc-subnets-ip-ranges.PNG "IP ranges of each subnet don't overlap")


 - Subnet name is also default. Note that IP ranges of each subnet don't overlap.

 - Each subnet has its own IP range which doesn't overlap with other subnets.

 - That allows the resources in one subnet to communicate with the resources in other subnets. 



 ## Firewall Rules

 - Configure Firewall Rules to control traffic going in or out of the network:

   - Each firewall rule has priority (0 - 65535) assigined to it.

   - 0 has highest priority. 65535 has lowest priority.

   - There is the default implied rule with lowest priority (65535)

     - allow all egress (from inside the network)

     - deny all ingress

     - default rules cannot be deleted

     - you can override default rules by defining new rules with priority 0-65535

   - In addition to the above default rule, there are 4 default rules with priority 65534

     - allow incoming traffic from VM instances in the same network (default-allow-internal)

     - allow incoming TCP traffic on **port 22 (SSH)** (default-allow-ssh) - Linux machine

     - allow incoming TCP traffic on **port 3389 (Remote Desktop Protocol)** (default-allow-rdp) - Windows machine

     - allow incoming ICMP from any source on the network (default-allow-icmp)


   - **Ingress Rules**: incoming traffic from outside to GCP targets

     - **Target (destination)**: all instances or instances with TAG/Service Account

     - **Source (Where the traffic is coming from)**: CIDR or all instances/instances with TAG/SA

   - **Egress Rules**: outgoing traffic to destination from GCP targets

     - **Target (defines the source)**: all instances or instances with TAG/SA

     - **Destination**: CIDR block (specific range of IP addresses)



 ## Shared VPC

 - Scenario: Your organization has multiple projects. You want resources in different projects to talk to each other.

   - How to allow resources in different projects to talk to each other with internal IPs securely and efficiently?


 - **Shared VPC**

   - A shared VPC is created at organization or shared folder level (requiremment: Shared VPC Admin)

   - Allows VPC network to be shared between projects in the same organization.

   - A shared VPC contains one host project and multiple service projects:

     - Host project contains shared VPC network

     - Service projects are attached to host project

   - It helps you achieve **separation of concerns**.

     - Network administrators responsible for Host project and resource users use Service projects


  - **VPC Peering**

    - Scenario: How to connect VPC networks across different organizations?
  
    - **VPC Peering** allows networks in the same project, different projects, and across projects in different organizations can be **peered**.

    - All communications happen using internal IP addresses.

      - Highly efficient as all communication happens inside Google network.

      - Highly secure as not accessible from Internet.


 ## Cloud VPN

 - Cloud VPN - connects on-premise network to the GCP network.

   - Implemented using **IPSec VPN Tunnel**

   - Traffic through Internet (public)

   - However, traffic is encrypted using **Internet Key Exchange** protocol

 - 2 Types of Cloud VPN

   - **HA VPN** (SLA of 99.99% service availability with 2 external IP addresses)

     - High Availability - only dynamic routing (BGP) supported

   - **Classic VPN** (SLA of 99.9% service availability, a single external IP address)

     - Supports both static routing (policy based, route based) and dynamic routing using BGP


 ## Cloud Interconnect

 - High speed **physical** connection between on-premise and VPC networks:

   - Highly available and high throughput

   - 2 Types of connections possible

     - Dedicated Interconnect: 10 Gbps or 100 Gbps configurations

     - Partner Interconnect: 50 Gbps to 10 Gbps configurations


 - Data exchange happens through a private network:

   - Communicate using VPC nework's internal IP addresses from on-premise network

   - Reduces egress costs

     - As public Internet is not used

 - Supported Google API's and services can be privately accessed from on-premise   

 - Use only for high bandwidth needs:

   - For low bandwidth, Cloud VPN is recommended