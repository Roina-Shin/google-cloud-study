### [Source of this study material : Google Cloud Platform from Zero to Hero](https://www.udemy.com/course/google-cloud-platform-from-zero-to-hero-the-complete-guide/)


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

