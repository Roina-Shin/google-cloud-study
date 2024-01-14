### [Source of this study material : GCP Associate Cloud Engineer by Ranga Karanam](https://www.udemy.com/course/google-cloud-certification-associate-cloud-engineer/)


Instance Template is a resource that you use to create VM and managed instance groups.

Instance Template defines the machine type, boot disk image, or container iamage,
labels, and other instance properties.

Instance Template is a convenient way to save a VM instance's configuration
so you can use it later to create VMs or groups of VMs.

### Go to GCP console > Compute Engine > Create Instance Template

Instance Group is a collection of VM instances that you can manage as a single entity.

Instance Group is used to avoid individual instance management in project.

There are 2 kinds:
1. **Managed Instance Group** *recommended
2. Unmanaged Instance Group

Managed Instance Group is used to create multiple identical VMs.
Managed Instance Group is typically used with Load Balancers.

Advantages of MIG:

1. High availability for production : if any machine goes down, that failure cause the
MIG to automatically recreate VM in accordance with the MIG template specification.


2. Auto-healing via Health Check : User can set up an autohealing policy.
Periodically verifies that your app responds as expected on each instance in MIG.
If not responded, VM is automatically recreated.

3. Regional Coverage : Choose regional coverage over zonal coverage and it will protect
if any zone goes down you can still run your app in other zones.

4. Load Balancing : MIG works with load balancing services to distribute traffic across instances.

5. Scalability : MIG will autoscale depending on your demand.

5. Automated Updates : MIG lets you automatically update to a new version of software.

### Go to Instance Group > Create Instance Group
 - Choose instance template you created and specify nuber of instances, etc.

 > In the management > automation section of Instance Group Create page, insert this startup script to check how your expernal IP is working:

```
sudo apt-get update
sudo apt-get install -y apache2
cat <<EOF > /var/www/html/index.html
<html><body><h1>Hi Yejin</h1>
<p>You are learning one by one by practice. I think you are growing rapidly.</p>
</body></html>
EOF
```

(!!only change the protocol https > http as we configured so in console)


Load Balancer is function to distribute user traffic across multiple instances of application.

Load balancing reduces the risk that applications become overburdened, slow, or nonfunctional.

HTTP and HTTPS load balancer are external global load balancer.
(external LB for external traffic like Internet and internal LB for traffic within the same VPC)

HTTP(S) load balancer use multiple backend types.
Backend types such as homepage/user/order/registration backend services and,
these backend services' URL will be mapped to the HTTP(S) load balancer.

So, whenever you hit the DNS value or the URL of a particular website,
that request will directly land on the HTTP(S) load balancer.

And HTTP(S) load balancer will send that request to the global forwarding rules.

Forwarding rule will forward your request (after identifying it) and send it
to the proxy server.

Once that request is received by the proxy server, proxy server will evaluate
that request and send it to the URL map.

If you have defined some URL map in your HTTP(S) load balancer, URL map will send
that request to the backend services.

And from that particular backend service, that request will directly go to the nodes.

Let's look at each component of this workflow of LB in detail:

1. Forwarding rule : it specified an external IP address, port, and global target HTTP(S) proxy.

2. Clients (browser) : it uses the IP address and port to connect to the load balancer.

3. The forwarding rule for an HTTP load balancer can only reference TCP ports 80 and 8080.

4. The forwarding rule for an HTTPS load balancer can only reference TCP port 443.

5. NST stands for Network Service Tier. Theare 2 types of NST:

   - Premium Tier : Highest performance. Traffic between the internet and VM instances in your VPC network is routed by fast Google's network. It is default within GCP.

   - Standard Tier : Cost optimized. Traffic between the internet and VM instances in your VPC network is routed over the internet in general.

HTTP(S) load balancers in the Premium Tier use global external forwarding rules.
HTTP(S) load balancers in the Standard Tier use regional external forwarding rules.

6. Target Proxy : it receives a request from the client.
It evaluates the request by using the URL map to make traffic routing decisions.

Proxy can also authenticate communications by using SSL certificates.

If a user is using HTTPS load balancing, the target proxy uses global SSL certificates
to prove its identity to clients.

7. URL Map : when a request arrives at the load balancer, the load balancer routes
the request to a particular backend service based on configurations in a URL Map.

URL Map has 2 components: host and path.
Host - example.net
Path - /video/hd
http://example.net/video/hd

8. Backend services : they distribute request to healthy backends.
(e.g. instance groups containing Compute Engine VMs, GKE containers, or Cloud Storage Buckets, etc.)

9. Session Affinity : it's the best effort to send request from a particular client
to the same backend server for as long as the backend is healthy.


### To make and test a load balancer 

1. Prepare this startup script to test your load balancer.

```
VALUE_OF_MY_MACHINE_ID=$(curl http://metadata.google.internal/computeMetadata/v1/instance/attributes/my-machine-id -H "Metadata-Flavor: Google"
apt-get update
apt-get install -y apache2
cat - >/var/www/html/index.html <<EOF
<html><body><h1>Yejin! You made it.</h1>
<p>I'm glad you made it this far. Congrats and keep up the good work.</p>
</body></html>
EOF
```

2. Create an Instance Template and an Instance Group to nest the above startup script.

3. IMPORTANT! When creating an Instance Template and adding Startup Script,
don't forget to add Metadata Key / Value pair in Metadata section below the Starting Script.

In Key you should enter the same 'my-machine-id' you specified in the Startup Script 
and value (Value you can specify anything you want)

4. IMPORTANT! When creating an Instance Group and editing autoscaling criteria,
change the signal type to HTTP load balancing utilization.

5. When you check your HTTP application, search on your console 'Networking Services'.

6. Go to Load Balancing in Network Services.
Create a Load Balancer by defining frontend and backend services.

7. After creating the LB, check the external IP to see it's working.

8. Also, try ping the external IP or curl the external IP to see if it's healthy with :80 at the end.


---

Q7. You have a group of Compute Engine instances that run in multiple zones.
You have a requirement to automatically re-create instances in case any of them fail.
VMs should be re-created if they are unresponsive after 2 attempts of 8 seconds each.
What should you do?

A : 1. Use a managed instance group.
2. Set the Autohealing health check to healthy (HTTP)

An auto-healing health check with a managed instance group is required to perform
auto-healing. It suggests using a managed instance group and setting the Autohealing health check
to healthy. By setting up an HTTP-based heal check with appropriate check intervals
and unresponsive thresholds, you can ensure that instances failing the health checks
are automatically replaced, meeting the requirement of automatically re-creating
instances that become unresponsive after 2 attempts of 8 seconds each.
The health check can be configured to send HTTP requests and wait for a valid 
response with a certain time frame ( in this case 2 attempts of 8 seconds each).