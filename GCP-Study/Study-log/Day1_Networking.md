### [Source of this study material : GCP Fundamentals for Beginners by Janakiram MSV](https://www.udemy.com/course/google-cloud-platform-gcp-fundamentals-for-beginners/)


* IP Addresses in GCP

IP addresses are assigned to the compute resources.
When you are creating any executable instance in GCP,
there must be an IP address associated with it.

There are internal IP address and external IP address.

External IP address is not mandatory, but each VM *must* have internal IP address.

External IP address is used to communicate outside your VPC network or with the Internet.
And that is optional when you are creating the VM.

Internal IP address is used for a VM to communicate with other instances in the same VPC network.
It doesn't matter if they are in the same region or in different regions.
But they communicate with each other using internal IP addresses only.

External IP address is used to communicate with instances in other networks or the Internet.

Internal IP addresses are allocated to instances from the subnet IP range via DHCP.
DHCP is a protocol in the GCP, which allows IP addresses to instances.

Each instance must have their own region and in the VPC, you will get the subnet
for the region so that internal IP associated with the instance must define
within the range of the subnet.

No manual intervention is required to assign internal IP to a VM.
It is automatic.

Internal IP address is ephemeral. (but can be static if configured so)
It means internal IP address associated with your resource can be changed.

External IPs are also assigned via DHCP.
Google has some provided pool for external IPs and DHCP protocol will automatically
pick up IP address from the pool.

External IPs are mapped to internal IPs of VM instances.
With the help of external IP, you can access your resources over the Internet.
But that external IP is also associated with the internal IP for an instance.

External IP can be static IP address if needed.

External IP can be both ephemeral and static.

Traffic using external IP address can cause additional billing chages on GCP.

=======================================

Q1. Your app communicates with a licensing server on the IP 10.194.3.41
several times a day to verify its authenticity. You need to migrate the licensing
server to Compute Engine. You cannot change the configuration of the app and
want the app to be able to reach the licensing server at the same IP.
What should you do?

A: Reserve the IP 10.194.3.41 as a static internal IP address using 
gcloud and assign it to the licensing server.

Internal IP needs to be reserved as static as, by default, the IPs are
ephemeral.(they can change after a VM restarts)

It suggests reserving the IP 10.194.3.41 as a static internal IP address
using gcloud and assigning it to the licensing server.

This ensures that the application can still reach the licensing server
at the same IP, as desired.

By reserving the IP as a tatic internal address, it guarantees that the IP
will not change and the application can establish a consistent connection
with the licensing server.
