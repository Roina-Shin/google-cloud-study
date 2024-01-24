### [Source of this study material : Google Cloud Professional Network Engineer by Ankit Mistry](https://www.udemy.com/course/google-cloud-networking/)


## Load Balancer

- **Load balancer** distributes user traffic across multiple instances of your applications.

- By spreading the load, load balancer reduces the risk that your applications experience performance issues.


## Cloud DNS

- To test the Cloud DNS service, I created a Hello Cloud Run service and the corresponding Load Balancer for the service.


![hellow-cloud-run](/GCP_pictures/Study-logs/Networking-Advanced4/hello-cloud-run.PNG "Hello Cloud Run service")



![lb-for-cloud-run](/GCP_pictures/Study-logs/Networking-Advanced4/lb-for-cloud-run.PNG "Load Balancer for Cloud Run")


- DNS is an Address Book for Internet.

- It maps a particular domain (www.google.com) to an IP address (74.125.29.101).

- Highly scalable, reliable and managed Domain Name System (DNS) service on GCP.

- Cloud DNS

  - Public zone

  - Private zone


- So, in the above Load Balancer example, we have this particular IP address (35.190.115.250) but we want to map this to a meaningful domain name.


- First, to use Google Cloud DNS service, you need to buy a domain from the domain site. I already bought one:


![domain-purchase](/GCP_pictures/Study-logs/Networking-Advanced4/domain-purchase.PNG "Domain purchase")


- Then, go to GCP console and head over to Cloud DNS.

- Click Create Zones and configure Zone name and DNS name in the format that Google requires:


![create-zone](/GCP_pictures/Study-logs/Networking-Advanced4/create-zone.PNG "Create a zone")


- Now, the zone is created. If you take a look at the NS record, you can see there are 4 name servers that you need to register on your domain site.


![name-server](/GCP_pictures/Study-logs/Networking-Advanced4/ns-server.PNG "NS Record -name servers")


- Register these 4 name server addresses on your domain site.


![nameservers-registration](/GCP_pictures/Study-logs/Networking-Advanced4/nameservers-registration.PNG "Nameservers registration")


- Now, we also need to create A Record and CNAME Record on our zone. Provide the IP address for each record.


![cname-record-creation](/GCP_pictures/Study-logs/Networking-Advanced4/cname-record-creation.PNG "CNAME Record registration")


