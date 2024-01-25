### [Source of this study material : Google Cloud Professional Network Engineer by Ankit Mistry](https://www.udemy.com/course/google-cloud-networking/)


## Deploy Cloud Run

- First go to Cloud Run and click Create Service.


![create-cloud-run](/GCP_pictures/Study-logs/Networking-Advanced4/ "Create a Cloud Run default service")


- Now, our backend service (Cloud Run service) is ready. It's time to connect this particular service to a load balancer.


- Go to Load Balancing of Network Services and click Create a load balancer. Go with the HTTP(S) Load Balancer. 


- We want an outside traffic to the service so choose Internet facing one and continue with the Global load balancer.


- Start with the Backend configuration.


![backend-config](/GCP_pictures/Study-logs/Networking-Advanced4/backend-config.PNG "Backend configuration")


- Configure frontend and routing rules and click create.


![other-config](/GCP_pictures/Study-logs/Networking-Advanced4/other-config.PNG "Ohter configuration")


- When a load balancer is ready, go to the details page and grab the IP address and check if it works on the browser.


![load-balancer-created](/GCP_pictures/Study-logs/Networking-Advanced4/load-balancer-created.PNG "Load Balancer created")


- And it is working. 


![working](/GCP_pictures/Study-logs/Networking-Advanced4/working.PNG "Load Balancer working")



- Now, it's time to connect your domain that you bought from a domain site with the Google Cloud DNS.


![cloud-dns](/GCP_pictures/Study-logs/Networking-Advanced4/create-dns-zone.PNG "Create a DNS zone")


- Click create Public DNS zone and put int the Zone name and DNS name accordingly.


![zone-creation](/GCP_pictures/Study-logs/Networking-Advanced4/zone-creation.PNG "Zone creation")


- When you create a zone, 2 records are automatically made available. Go to NS record section.


![ns-records](/GCP_pictures/Study-logs/Networking-Advanced4/ns-records.PNG "NS records")


- Go to the domain site and edit the nameservers so that the site includes these 4 nameservers from Google Cloud DNS.


![nameservers](/GCP_pictures/Study-logs/Networking-Advanced4/edit-nameservers.PNG "Edit Nameservers")


- After done, you will see these updated nameserver on the domain site.


![nameservers-updated](/GCP_pictures/Study-logs/Networking-Advanced4/nameservers-updated.PNG "Nameservers updated")


- Now, we need to do 2 important configuration on Google Cloud side: A record and CName record. Go back to the Cloud DNS and click Add record.


![a-record](/GCP_pictures/Study-logs/Networking-Advanced4/a-record-creation.PNG "A record creation")


- Keep the DNS name as is and select **A record**. Provide the IP address without the port number and protocol to it.


- CNAME creation is a little different. If someone types **www.learngcpwithyejin.site**, the CNAME helps you redirect the traffic to the canonical domain name **learninggcpwithyejin.site**. Configure it accordingly.


![cname-record](/GCP_pictures/Study-logs/Networking-Advanced4/cname-creation.PNG "CNAME creation")






