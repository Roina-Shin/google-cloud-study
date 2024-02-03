### [Source of this study material : Google Cloud Data Engineer by Ankit Mistry](https://www.udemy.com/course/google-cloud-gcp-professional-data-engineer-certification/)


## Cloud SQL

- Fully managed **relational database services** for MySQL, PostgreSQL, SQL Server.


## How to use Cloud SQL

- Go to Cloud SQL on the GCP console and choose MySQL.


![choose-mysql](/GCP_pictures/Study-logs/cloud-sql/choose-mysql.PNG "Choose MySQL")


- Configure your MySQL instance as per your need.


![config-mysql](/GCP_pictures/Study-logs/cloud-sql/config-mysql.PNG "Configure your MySQL instance")


- If you go to Connections section, you will see that the public IP address is available. But to connect to your SQL instance using the IP address, you first need to **whitelist the IP addresses** that you want to grant access to.


![sql-connections](/GCP_pictures/Study-logs/cloud-sql/public-ip.PNG "Public IP address of SQL instance")


- To do that, go to Cloud Shell. Then run the command to see the version of your MySQL inside the Cloud Shell.

```
mysql --version
```

- Then search **ipify** on Google. Go to the site and grab the following command:

```
curl 'https://api64.ipify.org?format=json'
```


![curl-command](/GCP_pictures/Study-logs/cloud-sql/curl-command.PNG "Curl command from Ipify")


- This is the IP address of the Cloud Shell. We can whitelist this address:


![ip-of-cloud-shell](/GCP_pictures/Study-logs/cloud-sql/ip-of-cloud-shell.PNG "IP address of cloud shell")


- Now, go to Connections section and then to Authorized networks. Click Add a Network.


![add-network](/GCP_pictures/Study-logs/cloud-sql/add-network.PNG "Add network")


![cloud-shell-ip](/GCP_pictures/Study-logs/cloud-sql/cloud-shell-ip.PNG "Cloud Shell IP address")


- After you provided the Cloud Shell IP address as a whitelist IP, click **save**.


- Go back to the Cloud Shell and connect to the MySQL public address using the following command:


```
mysql -h [mysql public ip address] -u root -p
```

- After you enter your password, you will get connected to your MySQL instance:


![mysql-connected](/GCP_pictures/Study-logs/cloud-sql/mysql-connected.PNG "MySQL instance connected")


- Now using the **whitelisting IP address** method, you can now connect your MySQL instance from any of the machine.


- Use the following to see the databases:


```
show databases;
```


- Create a database:


```
create database [database name];
```

- Create a table inside the db:


```
use [database name];
```


- Create a **user** table:


```
CREATE TABLE Users (
       UserID int,
       LastName varchar(255),
       FirstName varchar(255),
       Address varchar(255),
       City varchar(255)
);
```


- Insert a record inside the table:


```
insert into Users values (1, 'yejin', 'shin', 'korea', 'incheon');
```


![sql-data-entry](/GCP_pictures/Study-logs/cloud-sql/sql-data-entry.PNG "SQL database - table - data entry")


- Run the query to see inside what's inside the table:


```
select * from Users where UserID=1;
```


![sample-user-query](/GCP_pictures/Study-logs/cloud-sql/table-sample-query.PNG "Sample query on the table")


