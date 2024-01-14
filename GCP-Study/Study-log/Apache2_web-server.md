### [Source of this study material : GCP Associate Cloud Engineer by Ranga Karanam](https://www.udemy.com/course/google-cloud-certification-associate-cloud-engineer/)


## What is Apache2 web server?

Apache2 is a web server software that you can install on your VM instance as well as at the external IP of your VM instance so that visitors from the Internet can view content on your website.


## To play with Apache2 web server on your VM

- SSH into your VM and run the command:

```
sudo su
```

  This will make you a root user in the Cloud Shell.


- Update all the packages that are present in the root directory:

```
apt update
```


- Install Apache2 on your VM:

```
apt install apache2
```


- Go to the GCP console and click the external IP of your VM instance. Then, you will see the page like below:


![apache2-default-page](/GCP_pictures/Study-logs/Apache/apache2-default-page.PNG "Apache2 web server default page")


- Here, the important thing to note is **the default document root** shown in the page:

```
/var/www/html
```

The root directory is where you put all the files for your website.



- To see which file is present in the directory, you can simply run:

```
ls /var/www/html
```


- And you can see the **index.html** in that directory.


- That is the file where you want to put your own content. To experiment:

```
echo "Hello from $(hostname)" > /var/www/html/index.html
```


- By this, we send the hostname variable and hello greetings to the index.html file. We replaced the default content with our simple hello content.


- When you refresh the external IP page, you will see the test was successful.


![apache-hello-test](/GCP_pictures/Study-logs/Apache/apache-html-test.PNG "Simple hello test with apache server HTML file")


- And this hello message on the external IP persists even after you close the SSH terminal. But when you stop your VM instance, the external IP address is lost.


- When you stopped your VM instance and restarted it, then your external IP address will be different. 


- Also, to see the HTML file you modified earlier, you **need to** restart the Apache server as well. In the SSH terminal:

```
sudo su

service apache2 start
```


- Once this service is up and running, you can go and use the new external IP address to see your customized HTML page.


## Internal & External IP Address

- External IP address (a.k.a public IP address) is Internet addressable.

- Internal IP address is internal to a corporate network.

- All VMs are assigned at least one internal IP address.

- When you stop your VM instance, the internal IP address remains the same. However, the external IP address changes when you restart the VM instance.


## Reserve a static external IP address

- Go to VPC Network on GCP console.

- There, click Reserve External Static IP Address. After you configured your static external IP address, you will see something like below:


![reserve-static-ip-address](/GCP_pictures/Study-logs/Apache/reserve-static-ip.PNG "Reserve a static IP address")


- On the far right side of the screen, you will see three dots. When you click this, you will see some actions you can take on the static IP address. As I already made a static IP address and once used it for other resource, I see 'Reassign it to another resource" option.


![reassign-to-resource](/GCP_pictures/Study-logs/Apache/reassign-to-resource.PNG "Reassign to another resource button")


- Once you click that, you can choose the VM instance to attach to the static IP address.


![reassign-ip-address](/GCP_pictures/Study-logs/Apache/reassign-ip-address.PNG "Reassign static IP address to VM")


- That static IP address is now assigned to the VM instance. And this allows you to stop and restart the VM instance and still have the same external IP address.