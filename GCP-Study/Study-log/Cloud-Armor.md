### [Source of this study material : Google Cloud Professional Network Engineer by Ankit Mistry](https://www.udemy.com/course/google-cloud-networking/)


## Cloud Armor

- Network security product


- Web application firewall + DDos attack prevention


- Works for Layer 3 to Layer 7 (as opposed to Layer 3 to 4 as normal firewall does - based on IP and port)


- Has ML-based adaptive filtering to detect malicious attacks


- Works well with Load Balancer



## Cloud Armor Demo Steps

- Only organization node can create Cloud Armor


- Create 1 VM with nginx installed


- Create unmnaged instance group from VM


- Create load balancer with unmanaged instance group as backend


- Cloud Armor 

  - Create policy & add rule (attached with load balancer)




## Cloud Armor Demo

- I'm using my organization account in GCP for this Cloud Armor demo.


![organization-account](/GCP_pictures/Study-logs/cloud-armor/organization-account.PNG "Organization account")


- Go create a VM. When creating it, include this startup script:


```
apt update
apt install -y nginx
```


![startup-script](/GCP_pictures/Study-logs/cloud-armor/startup-script.PNG "Startup script")


- While creating the VM, go to the MIG and create **unmanaged instance group**. Be sure to select the VM you created.


![unmanaged-ig](/GCP_pictures/Study-logs/cloud-armor/unmaged-ig-vm.PNG "Unmanaged instance group")


- After creating the unmanaged instance group, go create a load balancer.


![lb-backend](/GCP_pictures/Study-logs/cloud-armor/lb-backend.PNG "Load balancer backend")


- If you go to the load balancer URL, you will see that nginx page works.


![nginx-lb-works](/GCP_pictures/Study-logs/cloud-armor/lb-nginx-works.PNG "nginx works through load balancer")


- Now, go to Cloud Armor and click Create Policy.


- First, for testing purposes, we will create a deny-all policy.


![deny-all-policy](/GCP_pictures/Study-logs/cloud-armor/deny-all-rule.PNG "Deny all policy")


- And choose the load balancer when selecting a target for Cloud Armor policy.


![lb-as-target](/GCP_pictures/Study-logs/cloud-armor/target-as-lb.PNG "LB as target")


- The policy will take some time to be fully propagated.


![policy-being-created](/GCP_pictures/Study-logs/cloud-armor/policy-being-created.PNG "Policy being created")


- After some time, when we try accessing the same load balancer IP address, it shows 403 forbidden page as we configured in Cloud Armor policy page.


![403-forbidden](/GCP_pictures/Study-logs/cloud-armor/403-forbidden.PNG "403 forbidden")


- Now, we are going to add one more rule:


![add-rule](/GCP_pictures/Study-logs/cloud-armor/add-rule.PNG "Add rule")


- This time, we are adding allow-all rule. Give it a priority of 1000 which is higher than the deny-all rule that we created earlier.


![allow-all](/GCP_pictures/Study-logs/cloud-armor/allow-all.PNG "Allow all rule")


- With this rule applied, the same load balancer IP address works as before:


![nginx-works-again](/GCP_pictures/Study-logs/cloud-armor/nginx-works-again.PNG "nginx works again")


- For our next test, we need the IP address of our local machine and the cloud shell.


- To know the Cloud Shell IP address, use Ipify site:


![ipify](/GCP_pictures/Study-logs/cloud-armor/cloud-shell-ip-find.PNG "Ipify")


- Ipify lets you know the IP address of your Cloud Shell:


![ipify-solution](/GCP_pictures/Study-logs/cloud-armor/ipify-solution.PNG "Ipify lets you know ip address")


- My local IP address is this one:


![local-ip-address](/GCP_pictures/Study-logs/cloud-armor/local-ip-address.PNG "Local IP address")


- When we are trying to curl the load balancer IP address from both our local machine Powershell and Cloud shell, it works.


![powershell-curl-works](/GCP_pictures/Study-logs/cloud-armor/powershell-curl-works.PNG "Powershell curl works")


![cloud-shell-curl-works](/GCP_pictures/Study-logs/cloud-armor/cloud-shell-curl-works.PNG "Cloud Shell curl works")


- Now, create another rule that allows **cloud shell** IP address to access the LB IP address:


![allow-cloud-shell](/GCP_pictures/Study-logs/cloud-armor/allow-cloud-shell.PNG "Allow Cloud Shell")


- Also, make sure **to delete the clashing allow-all rule** to prevent any test validity issue. This way, we have 2 rules: allow cloud shell rule and deny all rule.


- When I try curling the same load balancer IP address this time, it doesn't work. It shows 403 forbidden error.


![powershell-now-denied](/GCP_pictures/Study-logs/cloud-armor/powershell-now-denied.PNG "Powershell now denied")


- And Cloud Shell curling still works due to the Cloud Armor allow-cloud-shell rule:


![cloud-shell-still-works](/GCP_pictures/Study-logs/cloud-armor/cloud-shell-still-works.PNG "Cloud Shell still works")


- This time, I created a rule that allows local machine IP address.


![allow-local-machine](/GCP_pictures/Study-logs/cloud-armor/allow-local-machine.PNG "Allow local machine")


- After some tries, curl from local machine finally works again!


![curl-from-local-works](/GCP_pictures/Study-logs/cloud-armor/curl-from-local-works.PNG "Curl from local machine now works!")


- Now, we are going to add some additional paths (/goodpath/*, /badpath/*) to our nginx html page. Before we do that, let's remove our deny-all rule. (or add higher priority allow-all rule)


- SSH into your nginx VM and go to html directory.


```
cd /var/www/html/
```


- There make 2 directories:


```
sudo mkdir goodpath
```

```
sudo mkdir badpath
```


- Make a new index.html file inside the goodpath:


```
sudo vim index.html
```

- Just add **<h1>Good path</h1>** inside the file and get out of the file.


- In the same way, edit the index.html file inside the badpath directory also.


![path-making](/GCP_pictures/Study-logs/cloud-armor/path-making.PNG "Path making")


- Now go to browser and access the /goodpath.


![goodpath-works](/GCP_pictures/Study-logs/cloud-armor/goodpath-works.PNG "Goodpath works")


- The /badpath also works.


![badpath-works](/GCP_pictures/Study-logs/cloud-armor/badpath-works.PNG "Badpath works")


- We are now prepared to add a new custom rule. First we are going to create allow-goodpath rule:


- This time, we cannot create a rule based on IP address. So, we should go with **advanced mode** in the rule creation page:


![advanced-mode](/GCP_pictures/Study-logs/cloud-armor/advanced-mode-rule.PNG "Advanced mode")


- Also add this **Match** rule like above. More information about this match rule syntax, go to this [documentation](https://cloud.google.com/armor/docs/rules-language-reference?_ga=2.170851558.-753445000.1707540068) page.


- After creating the goodpath-allow rule, let's create a badpath-deny rule this time.


- Now, let's test our goodpath/badpath rules by going to the browser:


![after-rule-goodpath](/GCP_pictures/Study-logs/cloud-armor/after-rule-goodpath.PNG "After rule goodpath works")


![after-rule-badpath](/GCP_pictures/Study-logs/cloud-armor/after-rule-badpath.PNG "After rule badpath doesn't work")


- Obviously, while goodpath still works, badpath no longer works. That's the beauty of Cloud Armor. You can specifically target some pages to allow or deny traffic for further protection.


- After you are done with your test, make sure to wipe out all the Policy, load balancer, and VMs to prevent any unnecessary cost from incurring.





