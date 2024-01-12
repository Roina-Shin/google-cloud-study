### [Source of this study material : Google Cloud Security Best Practices by Dan Sullivan](https://www.udemy.com/course/google-cloud-security-best-practices/)


## Networking Security in Google cloud

1. Cloud NAT

Cloud NAT is a Google service that allows us to reduce the number of public IP addresses
we need to have in place.

NAT stands for Network Address Translation.

NAT is a mechanism for providing outbound access to the Internet by mapping multiple private addresses in a local Network
to a public IP address.

Cloud NAT works with compute engine, private GKE clusters, cloud run, cloud functions, and app engine through serverless VPC access.

Cloud NAT reduces need for external IP addresses for your VMs.

2. Cloud Armor

Cloud Armor is a service that helps us protect against distributed denial of service(DDoS) attacks, 
acting as a web application firewall.

It detects an attack that happens at layer 7 (Application Layer) at the load balancer level by using machine learning.

If you want to use Cloud Armor, you should work with an external HTTPS load balancer.

The best practice for security policy is that:

  1) Configure security policy attached to the load balancer to protect
  2) Enable Google Cloud Armor adaptive protection
  3) Set rate limiting thresholds
  4) Choose preconfigured WAF rule sensitivity level


3. Identity Aware Proxy

Identity Aware Proxy is a service from Google Cloud that allows us to control access to applications
more at the application layer level and less at those lower network levels in the OSI model.

Identity Aware Proxy controls access at layer 7 for HTTPS access.

We have access policies that are defined centrally and applied to applications and services.

The protection that Identity Aware Proxy provides is based on the identities that we have in IAM roles and permissions.

IAP is a way of enforcing IAM roles at the application access level.

