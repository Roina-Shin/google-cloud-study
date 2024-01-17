### [Source of this study material : GCP Associate Cloud Engineer by Ranga Karanam](https://www.udemy.com/course/google-cloud-certification-associate-cloud-engineer/)


## Database

- Database provides organized and persistent stroage for your data.

- To choose between different database types, you need to understand:

  - Availability

  - Durability

  - RTO

  - RPO

  - Consistency

  - Transactions


## Database - Getting started

- Imagine a database deployed in a data center in London.

- Let's consider some challenges:

  - 1: Your database will go down if the data center crashes or the server storage fails.

  - 2: You will permanently lose data if the database crashes.

- To resolve this, you will start taking snapshots:

  - Automate taking copy of the database (take a snapshot) every hour to another data center.

  - You can set up a database from the latest snapshot. But depending on when failure occurs, you can lose up to an hour of data.

- The solution to this is to add a standby database in another data center with replication.

  
  ---

## Availability and Durability

- Avaiability

  - Able to access data when I need it.


- Durability

  - Data is available after 10 or 100 or 1000 years.


 ### Increasing Availability and Durability of Databases

   - Increasing availability

     - Have multiple standbys available or distribute the database

       - in multiple Zones

       - in multiple Regions

   - Increasing durability

     - Multiple copies of data (standbys, snapshots, transaction logs, replicas, etc.)

       - in multiple Zones

       - in multiple Regions


 ### RTO and RPO

 - How do we measure how quickly we can recover from failure?

   - **RPO** (Recovery Point Objective): Maximum acceptable period of data loss

   - **RTO** (Recovery Time Obejctive): Maximum acceptable downtime

   - BUT achieving minimum RPO and RTO is expensive.

   - That is why we need to trade off based on the criticality of the data.


 ### Consistency

 - How do you ensure that data in multiple database instances (standbys and replicas) is updated simultaneously?

   - **Synchronous replication** to all replicas

     - BUT the transactions will slow down

   - **Asynchronous replication**. A little lag (a few seconds) before the change is available in all replicas.

     - BUT in the intermediate period, different replicas might return different values.


## Database Categories

- Choosing a type of database for your use case is **not easy**.

- A few factors you need to consider:

  - Do you want a **fixed schema**?

  - What kind of **latency** do you want? (seconds, milliseconds, microseconds, etc.)

  - How many transactions do you expect? (hundreds or thousands or millions of transactions per second)

  - How much data will be stored? (MBs or GBs or TBs or PBs)


 ### Relational Databases

   - This was the only option until a decade back.

   - Most popular or unpopular type of databases.

   - Predefined schema with tables and relationships.

   - Use them for OLTP (Online Transaction Processing)

   - Use them for OLAP (Online Analytics Processing)

 ### Relational DB - Cloud SQL and Cloud Spanner

   - Applications where large number of users make large number of small transactions.

     - Small data reads, updates and deletes

     - Most traditional applications like ERP, CRM, e-commercer, banking applications

   - Popular databases are MySQL, Oracle, SQL Server, etc.

   - Recommended Google Managed Services are:

     - **Cloud SQL** : supports PostgreSQL, MySQL, and SQL Server for regional relational DBs (Up to a few TBs)

     - **Cloud Spanner** : Unlimited scale (multiple PBs) and 99.999% availability for global applications with horizontal scaling.

 ### Relationa DB - OLAP - BigQuery

   - BigQuery is petabyte-scale distributed data warehouse.

 ### NoSQL Databases

   - New approach to building your databases.

   - Flexible schema

     - Structure data the way your application needs it.

     - Let the schema evolve with time.

   - Typical NoSQL databases trade off strong consistency and SQL features to achieve scalability and high-performance.

   - Recommended Google Managed Services are:

     - **Cloud Firestore** : Managed serverless NoSQL document database. Designed for transactional mobile and web applications. Recommended for small to medium databases (0 to a few terabytes)

     - **Cloud Bigtable** : Managed scalable NoSQL wide column database. Recommended for 10 TBs up to several PBs of data. Not recommended for transactional workloads.

 ### In-memory Databases

   - Retrieving data from memory is much faster than retrieving data from disk.

   - In-memory databases like Redis deliver microsecond latency by storing persistent data in memory.

   - Recommended Google Managed Services are:

     - **Memory Store** : If you want to implement caching, session management, gaming leader boards, geospatial applications, etc. you want to go with Memory Store.



## Cloud SQL

- **Fully managed relational database service**.

- Supports MySQL, PostgreSQL, and SQL Server.

- Regional service providing high availability (99.95%)

- Use Cloud SQL for simple relational use cases.


 ### How to play with Cloud SQL

   - If you go to Cloud SQL and first created your SQL instance, you will see this dashboard:


   ![first-sql-creation](/GCP_pictures/Study-logs/Databases/first-sql-creation.PNG "The first SQL instance created")


   - Go to Databases on the left nav bar and click Create Database.


   ![create-database](/GCP_pictures/Study-logs/Databases/create-database.PNG "Create a database")


   - Once done, go to Overview again and open cloud shell to connect to the instance.


   ![open-cloud-shell](/GCP_pictures/Study-logs/Databases/open-cloud-shell.PNG "Open cloud shell to connect to the instance")


   - In the Cloud Shell, you will see a pre-populated command:

   ```
   gcloud sql connect yejin-mysql-instance --user=root --quiet
   ```
  
   - To use the database you created, run:

   ```
   use [database name]
   ```   

   - To create a table name 'user' inside the database:

  ```
  create table user (id integer, username varchar(30));
  ```


   ![table-creation](/GCP_pictures/Study-logs/Databases/table-creation.PNG "Table creation")


   - To describe the table schema:

   ```
   describe user;
   ```

   - You can insert data into the table by:

   ```
   insert into user values (1, 'Yejin');
   ```
   
   - To see the table with the data input:

   ```
   select * from user;
   ```


   ![select-all-from-user](/GCP_pictures/Study-logs/Databases/select-all-from-user.PNG "Select all from user table")



 ### Features of Cloud SQL

   - Automatic encryption: all your tables and the backups are automatically encrypted. And updates and maintenance can be done according to your schedule.

   - High availability and failover: can create a standby with automatic failover.

   - To do an automatic failover, you need to enable **Automated Backups and Binary Logging**.

   - Also supports **Automatic Storage Increase** without downtime. 

   - Point in Time Recovery: you can recover to a specific point in time by enabling Binary Logging.

   - You can also export data from the console or gcloud with formats:

     - SQL (Recommended if you import data into other databases) and CSV



## Cloud Spanner

- Fully managed, mission critical, relational (SQL), globally distributed database with VERY high availability (99.999%)

- Cloud Spanner scales horizontally for both reads and writes.

- Cloud Spanner is **expensive**: pay for nodes & storage.

- You can use cloud console to export data from Cloud Spanner.

- Other option is to use **Data Flow** to automate export.


 ### How to play with Cloud Spanner

   - You can use a free trial and go ahead to create a new Cloud Spanner instance:


   ![cloud-spanner-db-creation](/GCP_pictures/Study-logs/Databases/cloud-spanner-db-creation.PNG "Cloud Spanner DB creation")


   - In the Database creation tab, you can also configure a table:


   ![spanner-table-config](/GCP_pictures/Study-logs/Databases/spanner-db-table.PNG "Cloud Spanner table creation")


   - When you go into your Spanner table 'user', you can see the table schema as you configured:


   ![spanner-table-schema](/GCP_pictures/Study-logs/Databases/spanner-table-schema.PNG "Cloud Spnner table schema")


   - Then you can insert data in the Data section on the left nav bar. Go there and run the query:


   ![run-query-on-spanner-table](/GCP_pictures/Study-logs/Databases/run-query-on-table.PNG "Run a query on the Cloud Spanner table")


   - After you run the query, you get the result below:


   ![run-query-result](/GCP_pictures/Study-logs/Databases/run-query-result.PNG "Cloud Spanner query result")


   - You can also see the System Insights of your Spanner instance. It provides you with CPU utilization, transaction latency, etc.


   ![spanner-system-insights](/GCP_pictures/Study-logs/Databases/spanner-system-insights.PNG "Spanner's System Insights panel")


   - Make sure you delete the Spanner instance after you play with it:


   ![delete-spanner-instance](/GCP_pictures/Study-logs/Databases/delete-spanner-instance.PNG "Delete the Spanner instance after use")



 ### Cloud Datastore and Firestore

   - Datastore is a highly scalable **NoSQL document database**.

   - It automatically scales and partitions data as it grows.

   - It is recommended for up to a few TBs of data. For bigger volumes, BigTable is recommended.

   - For use cases requiring flexible schema with transactions:

     - User Profile

     - Product Catalogs

   - With Datastore, you can only export data ONLY from gcloud (NOT from cloud console)

   - **Google is slowly replacing Datastore with Firestore**. Firestore is optimized for multi device access.

   - Firestore supports offline mode and data synchronization across multiple devices - mobile, IoT, etc.

   - Firestore provides client side libraries - web, iOS, Android, etc.


 ### How to play with Firestore

   - When you go to Firestore on Google Cloud Console and click Create Database, you are prompted to select either Native mode or Datastore mode.

     - Native mode: recommended.

     - Datastore mode: If you have old Datastore project you are moving to the Firestore, then go with this option.

   
   ![firestore-mode](/GCP_pictures/Study-logs/Databases/firestore-mode.PNG "Firestore mode options")


   - Choose Native mode and create a database. Once created, you are now ready to populate the DB with data.


   ![firestore-start-collection](/GCP_pictures/Study-logs/Databases/start-collection.PNG "Start collection for data entry")



   - Click Start Collection. A **collection** is a set of one or more documents that contain data. Collection here is very similar to the table in SQL database.

   - Now we created the first document inside our collection. The document name is automatically created and I populated some info inside the document.


   ![firestore-first-document](/GCP_pictures/Study-logs/Databases/firestore-document.PNG "The first document created inside the collection of Firestore")


   - What is interesting here is, inside the document, not only can you add more fields to it, but also you can create another hierarchy by adding a collection beneath the document. (See above)


 ### Cloud Bigtable

  - Petabyte scale, wide column NoSQL DB (HBase API compatible)

  - You can handle millions of read/write transactions at very low latency.

  - Cloud Bigtable supports **single row transactions** only. (multi row transactions NOT supported)

  - That is why Cloud Bigtable is not a good candidate for transactional applications.

  - Cloud Bigtable is **NOT serverless**. You need to create a server instance and then create your **table**.

  - You can either choose SSD or HDD.

  - Cloud Bigtable can scale horizontally with multiple nodes. 

  - You CANNOT export data using cloud console or gcloud.

  - You can either use a Java application (java -jar JAR export/import) or use HBase commands.


  ![cloud-bigtable-structure](/GCP_pictures/Study-logs/Databases/bigtable-structure.PNG "Cloud Bigtable Structure")


  - Use cases: IoT streams, graph data, real time analytics, time series data, financial data, transaction history, stock prices, etc.

  - To export data from Bigtable, you can first use **Cloud Dataflow** to export data from it and move it to the Cloud Storage.

  - CLI for Cloud Bigtable (NOT gcloud)

  - It uses **cbt** instead of gcloud.

  ```
  echo project=project-id > ~/.cbtrc

  echo instance=instance-id >> ~/.cbtrc
  ```

 ### Memorystore

 - Memorystore is a **in-memory datastore** service. You can reduce access times.

 - Memorystore is fully managed. Provisioning, replication, failover, and patching included.

 - Monitoring can be easily set up with Cloud Monitoring.

 - Memorystore supports 2 options: **Redis** and **Memcached**.

   - **Why cache?**: Caching allows you to reuse the result of complex queries instead of redoing the work over and over again.

   - Use Memcached for: reference data, database query caching, session store, etc.

   - Use Redis for: low latency access with persistence and high availability. e.g.) gaming leader boards, player profiles, in memory stream processing, etc.


 ### BigQuery - Datawarehouse

 - Exabyte scale modern datawarehousing solution from GCP.

 - Relational database (SQL, schema, consistency, etc.)

 - You can use SQL-like commands to query massive datasets.

 - When we talk about a datawarehouse, **importing and exporting data** becomes very important.

 - Bigquery supports a variety of formats: 

   - CSV, JSON, Avro, Parquet, ORC, Datastore backup, etc.

 - You can also export data to Cloud Storage (long term storage) & visualize data using Data Studio.

   - Formats: CSV/JSON (with Gzip compression), Avro (with deflate or snappy compression)

 - You can automatically expire data using **Configurable Table Expiration**.

 - BigQuery allows you to query **external data sources** without storing data in BigQuery:

   - Cloud Storage

   - Cloud SQL

   - BigTable

   - Google Drive


 - Best practice : always run **estimate BigQuery queries** before running:

   - Use UI(console) or bq(--dry-run) to get scanned data volume.

   - Use pricing calculator to find out the price for scanning 1 MB of data.
