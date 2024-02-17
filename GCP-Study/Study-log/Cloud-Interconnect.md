### [Source of this study material : Google Cloud Professional Network Engineer by Ankit Mistry](https://www.udemy.com/course/google-cloud-networking/)


## Cloud Interconnect

- Extend your on premises network to GCP network.


- Highly available, low latency connection.


- Here, you are using the **physical connection** between your data center directly to the Google Cloud.


- There is no public Internet available between your data center and GCP.


- You can access all your resources inside GCP via **internal IP address** only.


- No encryption while traffic travels.


- There are 3 types of physical Interconnect.


![3-types](/GCP_pictures/Study-logs/cloud-interconnect/interconnect-types.PNG "3 types of Interconnect")



## Create Cloud Interconnect request

- If you click **Dedicated Interconnect**, there is no intermediary between your data center and GCP network.


- You can either choose **Order new Interconnect connection** or **Go with existing Interconnect connection**.


![order-new-interconnect](/GCP_pictures/Study-logs/cloud-interconnect/order-new-connection.PNG "Order new Interconnect connection")


- If you go one step further, you will see the pricing for the default 10GB capacity. The price will increase if you increase the capacity per month.


![pricing](/GCP_pictures/Study-logs/cloud-interconnect/order-form.PNG "Order form")


- You can also choose the location of Interconnect facility near your data center.


![interconnect-facility](/GCP_pictures/Study-logs/cloud-interconnect/interconnect-locations.PNG "Interconnect colocation facility")


- Next, you are recommended to create a second Interconnect for redundancy purposes.


![second-interconnect](/GCP_pictures/Study-logs/cloud-interconnect/redundant-place.PNG "Redundant Interconnect")


- Next step is entering contact information.


![contact-info](/GCP_pictures/Study-logs/cloud-interconnect/contact-info.PNG "Contact info")


- And, when should you go with **Partner Interconnect**? If your data center is not near the Google Interconnect facilities, you can simply rely upon **partner network**.


![partner-interconnect](/GCP_pictures/Study-logs/cloud-interconnect/partner-interconnect.PNG "Partner Interconnect")


- And you can see the document to check who is the supported service providers in your region.


![supported-service-providers](/GCP_pictures/Study-logs/cloud-interconnect/supported-service-providers.PNG "Supported service providers")


- That is how you can place a request for Dedicated Interconnect or Partner Interconnect connection.


![demo-ending](/GCP_pictures/Study-logs/cloud-interconnect/demo-ending.PNG "Demo ending")


