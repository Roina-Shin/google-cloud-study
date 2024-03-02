### [Source of this study material : Google Cloud Associate Cloud Engineer Certification by Jose Portilla](https://www.udemy.com/course/google-cloud-associate-cloud-engineer-certification-course)


## Managed Instance Group

- Often you'll want to create a group of identical VM instances.


- Fortunately, GCP provides **managed instance groups** that allow you to create multiple identical instances and manage them together as a single group.


- To use MIG we first create Instance Template to be duplicated N times for the managed instance group.



## External HTTPS Load Balancing

- A load balancer distributes user traffic across multiple instances of your applications.


- By spreading the load, load balancing reduces the risk that your applications experience performance issues.


- External HTTP(S) Load Balancing is a proxy-based Layer 7 load balancer that enables you to run and scale your services behind a single external IP address.


- HTTP(S) Load Balancing supports global load balancing, allowing for customers to access a backend service through a single **anycast IP address**.

  - **Anycast** allows for multiple servers to share the same IP address as a single interface.


- HTTP(S) Load Balancing:

  - HTTP load balanced on Port 80 and 8080

  - HTTPS load balanced on Port 443


- HTTP(S) Load Balancing supports IPv4 and IPv6 and autoscaling



## Load Balancing Demo

### Load Balancing Demo Steps

1. Create a health check firewall rule


2. Create a NAT configuration


3. Create a custom image


4. Create an instance template


5. Configure HTTP Load Balancer


6. Perform a Load Test



- First, for health checks to work, you need to create **ingress allow firewall rule** so that the traffic from Google Cloud probers can connect to your backends.


- When creating a firewall rule, you need to include the following  IPv4 ranges to the **ingress allow healthcheck firewall rule**.


- source: https://cloud.google.com/load-balancing/docs/health-check-concepts#ip-ranges

- **35.191.0.0/16**

- **130.211.0.0/22**

- **209.85.152.0/22**

- **209.85.204.0/22**


![probe-ip-ranges-for-healthcheck](/GCP_pictures/Study-logs/MIG-Load-Balancing2/probe-ip-ranges-for-health-check.PNG "Probe IP ranges for healthcheck")


![create-firewall-rule](/GCP_pictures/Study-logs/MIG-Load-Balancing2/create-firewall-rule.PNG "Create a firewall rule")


- **TCP** is the underlying protocol so allow tcp protocol and port 80. TCP traffic includes SSL, HTTP, HTTPS, and HTTP/2.


- If you use **tcp:80** for the protocol and port, this allows TCP traffic on port 80 so Google Cloud could contact your VMs using HTTP on port 80 but it couldn't contact them using HTTPS on port 443.


![tcp-80](/GCP_pictures/Study-logs/MIG-Load-Balancing2/tcp-80.PNG "tcp 80")


- Then go to Cloud NAT and click Get Started. (It's for an internal VM we will create)


![cloud-nat](/GCP_pictures/Study-logs/MIG-Load-Balancing2/cloud-nat.PNG "Cloud NAT")


![cloud-nat-creation](/GCP_pictures/Study-logs/MIG-Load-Balancing2/cloud-nat-creation.PNG "Cloud NAT creation")


- Let's go to Compute Engine to create a custom Image for a web server.


- We are going to pretend to create a VM but actually create a custom image. Click create VM and go down to **boot disk**. There, opt for **keep boot disk** on deletion of the VM.


![keep-boot-disk](/GCP_pictures/Study-logs/MIG-Load-Balancing2/keep-boot-disk.PNG "Keep boot disk")


- Go down to Networking section and type **allow-health-check** for Network tags as we did on creating the firewall rule for healthcheck.


![add-network-tag-to-vm](/GCP_pictures/Study-logs/MIG-Load-Balancing2/add-network-tag-to-vm.PNG "Add network tag to VM")


![target-tags-on-firewall](/GCP_pictures/Study-logs/MIG-Load-Balancing2/target-tags-on-firewall.PNG "Target tags on firewall rule for healthcheck")


- And set your VM NOT to have an external IP:


![external-ip-none](/GCP_pictures/Study-logs/MIG-Load-Balancing2/external-ip-none.PNG "External IP none")


- Then create your VM.


- SSH into your VM and install apache2 web server. Then we will test the default page to see it's working. We will then set the apache to run at boot and select that as a custom image.


```
sudo apt-get update

sudo apt-get install -y apache2
```


- Then we will verify the apache server is working.


```
sudo service apache2 start

curl localhost
```


![verify-web-server](/GCP_pictures/Study-logs/MIG-Load-Balancing2/verify-web-server.PNG "Verify web server")


- We will make this apache2 to **start on booting**.


```
sudo update-rc.d apache2 enable
```


- Then go back to the console and reset the VM. **Reset** actually stops and reboots the machine. However, it **keeps the same IP and the same persistent boot disk** but memories are wiped.


![reset-the-vm](/GCP_pictures/Study-logs/MIG-Load-Balancing2/reset-the-vm.PNG "Reset the VM")



- Reconnect to your VM and run:


```
sudo service apache2 status
```

![sudo-service-apache2-status](/GCP_pictures/Study-logs/MIG-Load-Balancing2/sudo-service-apache2-status.PNG "sudo service apache2 status")


- Now go ahead and delete your VM instance. But as you already configured to keep boot disk, you will see the persistent disk on Storage > Disks section.


![boot-disk-persists](/GCP_pictures/Study-logs/MIG-Load-Balancing2/boot-disk-persists.PNG "Boot disk persists")


- Then go to Images section and click Create Image. Select the **my-example-web-server** as the source disk. An image is a replica of a disk that contains the applications and operating system needed to start a VM.


![create-image](/GCP_pictures/Study-logs/MIG-Load-Balancing2/create-custom-image.PNG "Create custom image")


- We are now ready to create an Instance Template that uses the image.


- When creating a template, be sure to **select the custom image we created** under the boot disk section.


![boot-disk-custom-image](/GCP_pictures/Study-logs/MIG-Load-Balancing2/boot-disk-select-custom-image.PNG "Boot disk, select custom image")


- Under Networking section, add **allow-health-checks** network tags to connect the instance template with the firewall rule (allow health check).


![add-network-tag-to-template](/GCP_pictures/Study-logs/MIG-Load-Balancing2/add-network-tag-to-template.PNG "Add network tag to Instance Template")


- Also, make the External IP for the instance template to **NONE**. Then click create.


![external-ip-none-again](/GCP_pictures/Study-logs/MIG-Load-Balancing2/external-ip-none-again.PNG "External IP none")


- Now, go to Instance Group and click create Instance Group. Choose the instance template we created and choose multi zones.


![choose-instance-template](/GCP_pictures/Study-logs/MIG-Load-Balancing2/choose-instance-template.PNG "Choose instance template and choose multi zones")


- And as the **autoscaling signal**, choose **HTTP load balancing utilization: 80**.


![http-load-balancing-utilization-80](/GCP_pictures/Study-logs/MIG-Load-Balancing2/load-balancing-utilization-80.PNG "HTTP load balancing utilization: 80")


- Then create a Health Check for the Instance Group.


![create-health-check](/GCP_pictures/Study-logs/MIG-Load-Balancing2/create-health-check.PNG "Create a health check for the instance group")


- Click create and you will meet the **Autoscaling configuration is not complete**. This is because we haven't configure the HTTP Load Balancing yet and we have already configured the austoscale signal to HTTP Load Balancing in the Instance Group.


![load-balancer-config-needed](/GCP_pictures/Study-logs/MIG-Load-Balancing2/load-balancer-config-needed.PNG "Load balancer config needed")


- Now, I'm going to repeat the same for another region (eu) Instance Group. For this, the template should be a global template. 


![2-instance-groups-created](/GCP_pictures/Study-logs/MIG-Load-Balancing2/2-instance-gruops-created.PNG "2 instance groups created")


- Now, let's go ahead and configure the Load Balancer.


- We have 2 backends in US and Europe. We will go with the HTTP(S) Load Balancing.


![http-load-balancing](/GCP_pictures/Study-logs/MIG-Load-Balancing2/http-load-balancing.PNG "HTTP Load Balancing")


- We will go with Internet facing option and choose Global HTTP(S) Load Balancer (classic).


![choose-classic-load-balancer](/GCP_pictures/Study-logs/MIG-Load-Balancing2/choose-classic-load-balancer.PNG "Choose classic load balancer")


- When configuring the backend for the load balancer, add the Instance Groups for EU and US. An Port number is 80. Also, enable logging.


![add-instance-groups-as-backend](/GCP_pictures/Study-logs/MIG-Load-Balancing2/add-instance-groups-as-backend.PNG "Add instance groups as backend")


![enable-logging](/GCP_pictures/Study-logs/MIG-Load-Balancing2/enable-logging.PNG "Enable logging")


- Then, add a frontend. Ephemeral IPv4 and Port 80. Also, add another frontend. Ephemeral IPv6 and Port 80. So that the load balancer will process both IPv4 and IPv6 requests.


![add-frontend](/GCP_pictures/Study-logs/MIG-Load-Balancing2/add-frontend.PNG "Add frontend")


![frontend-ipv6](/GCP_pictures/Study-logs/MIG-Load-Balancing2/frontend-ipv6.PNG "IPv6 frontend")


- Now create the load balancer. After creating the load balancer, come back to the Compute Engine and create another VM to test the load balancer. Select the custom image as its boot disk and then create.


![load-tester-creating](/GCP_pictures/Study-logs/MIG-Load-Balancing2/load-tester-creating.PNG "Load tester creating")



- Meanwhile, the load balancer IP address is working.


![load-balancer-working](/GCP_pictures/Study-logs/MIG-Load-Balancing2/load-balancer-working.PNG "Load balancer working")


- SSH into the load tester VM and ping the load balancer IP address. Once done, go back to your Load Balancer and check the monitoring section.


![load-balancer-monitoring](/GCP_pictures/Study-logs/MIG-Load-Balancing2/load-balancing-monitoring.PNG "Load balancing monitoring")


- Go down and expand the backend and you will see that the traffic is balanced across the EU and US MIGs.


![load-balanced-across-migs](/GCP_pictures/Study-logs/MIG-Load-Balancing2/load-balanced-across-migs.PNG "Load balanced across MIGs")
































