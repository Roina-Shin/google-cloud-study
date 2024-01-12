### [Source of this study material : GCP Fundamentals for Beginners by Janakiram MSV](https://www.udemy.com/course/google-cloud-platform-gcp-fundamentals-for-beginners/)


Google Cloud SQL is a fully managed relational database service for 
MySQL, PostgreSQL, and SQL server.

Cloud SQL automates backups, replication, and failover to ensure your database is
reliable, highly available, and flexible to your performance needs.

App Engine, Compute Engine, Kubernetes, and BigQuery are easily integrated with Cloud SQL.

* Features of Cloud SQL:

1) Google Cloud SQL is fully managed by Google.

2) Pay-per-use option. By paying only for the time for which you access data, you save money.

3) Even if there is major failure, your data is secure and your database is available.

4) Connecting with the Secure Sockets Layer (SSL) protocol is available.

4) Great durability and availability of data which is replicated in various geographic locations.

Cloud Spanner is a fully managed, scalable, relational database service
for regional and global application data.

Cloud Spanner is the first scalable, globally distributed, and strongly consistent  database
service built for the cloud specifically to combine the benefits of relational database
structure with non-relational horizontal scale.

Cloud Sapnner is suitable for the application which uses the global data.

Cloud Spanner delivers high-performance transactions and strong consistency across rows,
regions, and continents with an industry-leading 99.999% availability SLA, 
no planned downtime, and enterprise-grade security.

* Cloud SQL Demo

1) Go to SQL and create MySQL database.

2) First you need to create a dedicated instance for your database.

3) After that is done, go to your SQL database section and create a database.

4) One way to create your database is by going to Overview and use Cloud Shell.

5) Open the cloud shell. Use the following command to connect to your MySQL instance:

gcloud sql connect <your sql instance name> --user=root


6) Create a sample database using the following:

create databae [database name];

7) To list all the databases:

show databases;

+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
| yejindb            |
+--------------------+


8) To use database:

use <database name>;

9) To see all the tables in the database:

show tables;

10) Use git to get sample MySQL dataset from github:

(1) First, update your apt-get environment:

sudo apt-get update

(2) Install git in your cloud shell:

sudo apt-get -y -qq install git

(3) Check git version:

git version

(4) Prepare this github data sample URL to clone:

https://github.com/datacharmer/test_db.git

(5) Run the following query:

git clone https://github.com/datacharmer/test_db.git

(6) Once done, list the db:

ls

(7) Change the directory to test_db:

cd test_db/

(8) Then list out all the files in the db:

ls

(9) Get one of the files by:

cat employees.sql


(10) To connect this file to your GCP SQL in cloud shell:

gcloud sql connect <your instance name> --user=root < [filename.sql]


(11) 

gcloud sql connetct <your instance name> --user=root


show databases;

use employees

show tables;

select count(*) from employees;

+----------+
| count(*) |
+----------+
|   300024 |
+----------+

-> There are 0.3 million rows in the employees table.


(12) To copy external database file to your GCP bucket:

gsutil copy <database name>/* gs://[your bucket name]


====================================================


Q12. Your company is looking to cut GCP costs for relational data. 
Your company's small set of day-to-day package tracking and operational data
is located in one geographic location. One of the requirements is that
you need to support point-in-time recovery. What should you do?

A : Use Cloud SQL (MySQL) with the enable binary logging option selected.

Because binary logging needs to be enabled before using point-in-time recovery.

Using Cloud SQL (MySQL) with the enable binary logging option selected allows
for point-in-time recovery. Binary logging records changes to the database,
allowing you to restore the databse to a specific point in time in case of
data loss or corruption.












