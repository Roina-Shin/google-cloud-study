### [Source of this study material : Google Cloud Professional Network Engineer by Ankit Mistry](https://www.udemy.com/course/google-cloud-networking/)


## Cloud CDN


![cloud-cdn-workflow](/GCP_pictures/Study-logs/cloud-cdn/cloud-cdn-workflow.PNG "Cloud CDN workflow")


- Content Delivery Network(CDN) works with load balancer. 


- Before a user request hits the load balancer, if the request information alredady exists in Cloud CDN, it will simply respond with the information.


- Fast, reliable web and video content delivery with global scale and reach.


## Cloud CDN Demo


- For this demo, you need a GCS bucket and image stored in it.


- Go to Cloud Storage and create a bucket. Also, upload some image to it.


![bucket-and-images](/GCP_pictures/Study-logs/cloud-cdn/bucket-and-images.PNG "Bucket and images")


- Also, create a load balancer. When creating a load balancer, choose **backend bucket** instead of backend services. And select the bucket you created for this demo.


![choose-bucket-backend](/GCP_pictures/Study-logs/cloud-cdn/select-bucket-backend.PNG "Select bucket backend")


- You first need to make the bucket public by changing the permissions for **allUsers** to gain **Storage Object Viewer** role.


- Then when you go to the load balancer IP address, you can view the objects.


![lb-address-works](/GCP_pictures/Study-logs/cloud-cdn/lb-address-works.PNG "LB address works")


- When you go to a particular image path after the IP address, you can see the actual image.


![image-path](/GCP_pictures/Study-logs/cloud-cdn/image-path.PNG "Image path")


- Now, we can open the Cloud Shell and use the same image URL to fetch the image.


- As we can't directly see the image in the shell, we will use the script to see the image loading time when you hit the same URL multiple times.


```
for i in {1..10};do curl -s -w "%{time_total}\n" -o /dev/null http://34.36.66.248/images/new-peering.PNG; done
```


![time-script](/GCP_pictures/Study-logs/cloud-cdn/time-script.PNG "Time script")


- This time, we are going to introduce **Cloud CDN** to our load balancer.


- And I didn't know I already check the CDN box when I configured the LB backend.


- So, now, I will un-check the box and see how much time it will take to upload the image.


![backend-lb-edit](/GCP_pictures/Study-logs/cloud-cdn/backend-lb-edit.PNG "Backend load balancer edit")


- I run the same command again, but this time, for other image path and without CDN support:


![other-image-speed](/GCP_pictures/Study-logs/cloud-cdn/other-image-without-cdn.PNG "Image upload without CDN")


- We cannot see the clear sign that the time drastically increased for loading the image, but we get the idea that the CDN helps reduce the latency to get some information using caching capabilities.


- In Cloud Logging, we can see the difference more clearly. Earlier, when we first curl the image, the load balancer's CDN was on, and the first try was responded by the backend server:


![sent-by-backend](/GCP_pictures/Study-logs/cloud-cdn/sent-by-backend.PNG "Sent by backend")


- But the right next curl try was served from cache.


![response-from-cache](/GCP_pictures/Study-logs/cloud-cdn/response-from-cache.PNG "Response from cache")


- With the image that we configured the CDN off on load balancer, the first try was responded from backend.


![without-cdn-first-try](/GCP_pictures/Study-logs/cloud-cdn/without-cdn-first-try.PNG "Without CDN first try")


- And as expected, the second try also shows that our traffic is still responded by backend.


![without-cdn-second-try](/GCP_pictures/Study-logs/cloud-cdn/without-cdn-second-try.PNG "Without CDN second try")


