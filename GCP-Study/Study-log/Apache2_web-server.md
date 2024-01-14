### [Source of this study material : GCP Associate Cloud Engineer by Ranga Karanam](https://www.udemy.com/course/google-cloud-certification-associate-cloud-engineer/)


## What is Apache2 web server?

Apache2 is a web server software that you install on your VM instance as well as at the external IP of your VM instance so that visitors from the Internet can view content on your website.


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


- And you can see the **index.html** which are present in the directory.


- That is the file where you want to put your own content. To experiment:

```
echo "Hello from $(hostname)" > /var/www/html/index.html
```


- By this, we send the hostname variable and hello greetings to the index.html file. We replaced the default content with our simple hello content.


- When you refresh the external IP page, you will see the test was successful.


![apache-hello-test](/GCP_pictures/Study-logs/Apache/apache-html-test.PNG "Simple hello test with apache server HTML file")

