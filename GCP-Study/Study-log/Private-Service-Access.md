### [Source of this study material : Google Cloud Professional Network Engineer by Ankit Mistry](https://www.udemy.com/course/google-cloud-networking/)


## Private Service Access

- Let's say we have 3rd party services available. In that case, how can you connect your VM with the relational database service?

- This service is Cloud SQL with only **internal IP** within some **VPC**. This VPC is not owned by us, but owned by Google. 

- We will connect this VM to this Cloud SQL with only internal IP with **Private Service Access**.

- The following Google services support private service access:

  - Apigee

  - Cloud Build

  - **Cloud SQL**

  - **Memorystore for Memcached and Redis**

  - Vertext AI

  - Filestore (...)


## Private Service Access Demo

- For this demo, we need Cloud SQL instance. Quickly create it.


- When creating a SQL instance, be sure to choose **only private IP** in connections.


![private-ip](/GCP_pictures/Study-logs/private-service-access/sql-instance-private-ip.PNG "Private IP only")


- When you choose **private IP**, you are prompted with the message saying that your VPC needs **private service access** connection.


![private-service-access-notice](/GCP_pictures/Study-logs/private-service-access/private-service-access-notice.PNG "Notice")


- Click SET UP CONNECTION and configure.


- This will create automatically **one peering** for us. Between our network and Google managed network where this SQL instance resides in.


- While configuring your peering connection, it's ok to go with automatically allocating IP range.


![automatic-ip-range](/GCP_pictures/Study-logs/private-service-access/ip-range-automatically.PNG "Automatically allocated IP range")



- Once done, and check your Network. In VPC Network Peering section, you will see that a new peering is generated.


![new-peering](/GCP_pictures/Study-logs/private-service-access/new-peering.PNG "New peering")



- And you get this connection success message in the instance creation page as well.


![connection-created](/GCP_pictures/Study-logs/private-service-access/connection-created.PNG "Connection created")



- Now, start creating the instance.


- Also, you need a VM machine to connect to the SQL instance.


- Go create it. Be sure to include it in **the same network that you set peering with the Google network**. 


- Also, enable the **external IP** for the VM as we are going to SSH into it and try to connect with the SQL instance there.


- Once created the VM, SSH into it and run the command:


```
mysql
```

- If not available, you have to install **mariadb-client**.


```
sudo apt install mariadb-client
```


![mysql-error](/GCP_pictures/Study-logs/private-service-access/mysql-error.PNG "mysql error")



- After installing it, run this command **mysql** again. If you see the message like below, it is installed:


![error-but-installed](/GCP_pictures/Study-logs/private-service-access/error-but-installed.PNG "Error but installed")



- Go to your SQL instance and grab the private IP address.


![sql-private-ip](/GCP_pictures/Study-logs/private-service-access/sql-private-ip.PNG "SQL private IP address")



- Now, run the command to connect with your SQL instance:


```
mysql -h 10.76.64.3 -u root -p
```

- **-h** for remote host, **-u** for user, and **-p** for password.


- And you are connected with your MySQL instance.


![mysql-connected](/GCP_pictures/Study-logs/private-service-access/mysql-connected.PNG "MySQL instance connected")


- Try making a database and a table using the queries:


```
create database demodb;
```

```
use demodb;
```

```
CREATE TABLE Persons (
     PersonID int,
     Lastname varchar(255),
     Firstname varchar(255),
     Address varchar(255),
     City varchar(255)
);
```


![table-creation](/GCP_pictures/Study-logs/private-service-access/table-creation.PNG "Table creation")



- Also, insert some values into the table:


```
insert into Persons values (100, 'shin', 'yejin', 'Korea', 'incheon')
```


- So that is the idea behind how you can privately access 3rd party services in Google managed VPC. And that is the **Private Service Access**.