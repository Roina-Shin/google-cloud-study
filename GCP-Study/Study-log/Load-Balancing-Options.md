### [Source of this study material : Google Cloud Associate Cloud Engineer Certification by Jose Portilla](https://www.udemy.com/course/google-cloud-associate-cloud-engineer-certification-course)


## Internal HTTP(S) Load Balancing

- External HTTP(S) Load Balancing is for external public traffic reaching a single external IP address and then being redirected to the appropriate backend.


- GCP also offers **internal HTTP(S) load balancing** for internal HTTP(S) traffic.


- Internal HTTP(S) Load Balancing distributes HTTP and HTTPS traffic to backends hosted on Compute Engine and Google Kubernetes Engine (GKE).


- The load balancer is accessible only in the chosen region of your VPC on an internal IP address.


- Internal HTTP(S) Load Balancing consists of:

  - An internal IP address to which clients send traffic

  - Only clients that are located in the same region as the load balancer can access this IP address

  - Internal client requests stay internal to your network and region.

  - Backends can be Compute Engine VMs, Managed Instance Groups, or GKE nodes. These backends must be located in the same region as the load balancer.


## SSL Proxy Load Balancing

- SSL Proxy Load Balancing is a reverse proxy load balancer that distributes SSL traffic coming from the Internet to virtual machine instances in your Google Cloud VPC network.


- When you are using SSL Proxy Load Balancing for your SSL traffic, user SSL (TLS) connections are terminated at the load balancing layer and then proxied to the closest available backend instances by using either SSL (recommended) or TCP.


- With the Premium Tier, SSL Proxy Load Balancing can be configured as a global load balancing service.


- With Standard Tier, the SSL Proxy Load Balancer handles load balancing regionally.


![ssp-proxy-load-balancer](/GCP_pictures/Study-logs/load-balancer-options/ssl-proxy-load-balancing-diagram.PNG "SSL Proxy Load Balancer diagram")


- User goes to Google CLoud Load Balancing with SSL proxy and terminates the SSL connection at that load balancing layer. Then Load Balancer goes to the managed instance groups. You can decide **to want SSL between the proxy and your backends or not**. We recommend using SSL.


- It also supports **Intelligent Routing**. The load balancer can route requests to backend locations where there is capacity. In contrast, an Layer 3 and Layer 4 load balancer must route to regional backends without considering capacity.


- SSL Proxy Load Balancing features:

  - **Better utilization of backends**:

    - SSL processing can be very CPU-intensive if the ciphers used are not CPU efficient.


  - **Certificate Management**:

    - Your customer-facing SSL certificates can be either certificates that you obtain and manage or certificates that Google obtains and manages for you.


    - Google-managed SSL certificates each support up to 100 domains.


  - **Security Patching**:

    - If vulnerabilities arise in the SSL or TCP stack, Google will apply patches at the load balancer automatically to keep your VMs safe.



## TCP Proxy Load Balancing

- TCP Proxy Load Balancing is a reverse proxy load balancer that distributes TCP traffic coming from the Internet to virtual machine (VM) instances in your Google Cloud VPC network.


- When using TCP Proxy Load Balancing, traffic coming over a TCP connection is terminated at the load balancing layer, and then forwarded to the closest available backend using TCP or SSL.


- TCP Proxy Load Balancing lets you use a single IP address for all users worldwide. The TCP Proxy Load Balancer automatically routes traffic to the backends that are closest to the user.


- With Premium Tier, TCP proxy load balancing can be configured as a global load balancing service.


- With Standard Tier, the TCP proxy load balancer handles load balancing regionally.


- TCP Proxy Load Balancing features:

  - Supports both IPv4 / IPv6: for IPv6, it terminates the request at the proxy and sends the IPv4 request to the backend. 

  - Intelligent Routing

  - Seucurity Patching

  - Support for well-known TCP Ports



## External TCP/UDP Network Load Balancing

- Note, since its most commonly used with TCP or UDP, you often see it referred to as **External TCP/UDP Network Load Balancing** although you will later see this shortened to just **Network Load Balancing**.


- A **Network Load Balancer** balances traffic originating from the Internet.


- **Network Load Balancing** is a regional, non-proxied load balancing service.


- This means that it can only balance for instances within the same region (non-global).


- Network Load Balancing supports the following traffic types:

  - **TCP**

  - **UDP**

  - **EDP**

  - **ICMP**


- A network load balancer can receive traffic from:

  - Any client on the Internet

  - Google Cloud VMs with external IPs

  - Google Cloud VMs that have internet access through Cloud NAT or instance-based NAT


- Network load balancers are not **proxies**.

  - Load-balanced packets are received by backend VMs with the packet's source and destination IP addresses, protocol, and, if the protocol is port-based, the source and destination ports unchanged.


  - Load-balanced connections are terminated by the backend VMs.


  - Responses from the backend VMs go directly to the cients, not back through the load balancer.


  - The industry term for this is direct server return.


![external-tcp-udp-network-load-balancer](/GCP_pictures/Study-logs/load-balancer-options/network-load-balancer-diagram.PNG "External TCP/UDP Network Load Balancer")



### Network Load Balancer Use Cases:

- When you need to load balance non-TCP traffic, or you need to load balance a TCP port that isn't supported by other load balancers.


- It is acceptable to have SSL traffic decrypted by your backends instead of by the the load balancer. The network load blanacer cannot perform this task. When the backends decrypt SSL traffic, there is a greater CPU burden on the VMs.


- Or self-managing the backend VM's SSL certificates is acceptable to you. Google-managed SSL certificates are only available for HTTP(S) Load Balancing and SSL Proxy Load Balancng.


- Or you need to forward the original packets **unproxied**. For example, if you need the client source IP to be preserved.


- Or you have an existing setup that uses a pass-through load balancer, and you want to migrate it without changes.


## Load Balancing Options

- Feature Considerations:

  - External vs Internal Load Balancing

  - Global vs Regional Load Balancing

  - Premium vs Standard Network Tiers

  - Proxy vs Pass-through Load Balancing

  - Traffic types and DDoS protections


![choose-a-load-balancer](/GCP_pictures/Study-logs/load-balancer-options/choose-a-load-balancer.PNG "Choose a load balancer")


- **Proxy Load Balancers** terminate incoming client connections and open new connections from the load balancer to the backends. 


- **Passthrough Load Balancers** do not terminate client connections. Instead, load-balanced traffic is sent directly to backends. 


![application-load-balancer](/GCP_pictures/Study-logs/load-balancer-options/application-load-balancer.PNG "Application Load Balancer")


![proxy-network-load-balancer](/GCP_pictures/Study-logs/load-balancer-options/proxy-network-load-balancer.PNG "Proxy Network Load Balancer")


![passthrough-network-load-balancer](/GCP_pictures/Study-logs/load-balancer-options/passthrough-network-load-balancer.PNG "Passthrough Network Load Balancer")