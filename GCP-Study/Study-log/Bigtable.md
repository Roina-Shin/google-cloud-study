### [Source of this study material : Google Cloud Data Engineer by Ankit Mistry](https://www.udemy.com/course/google-cloud-gcp-professional-data-engineer-certification/)


## Cloud Bigtable

- Fully managed wide column NoSQL database

- Not serverless: you need to create **instance** for server

- Scale horizontally with multiple nodes

- Columns are grouped into **column family**

- Handles millions of requests per second

- How to access:

  - cbt - command line (part of cloud sdk)

  - Hbase API

- No multi column index

  - Only row key based indexing

- To design a row key is very important

  - which is your frequent query in application

  - No hot spotting (**hot spotting** is when all workload is concentrated on one instance)

  - So, to prevent hot spotting, do not use **monotonically increasing key**.

- Bigtable is mainly used for:

  - Financial data

  - Time series data 


![bigtable-structure](/GCP_pictures/Study-logs/bigtable-structure/bigtable-structure.PNG "Bigtable structure")



- Inside the Bigtable, we have **column families**. Here, name and age belong to personal data column family while salary, job title, and company belong to professional data column family.



## How to use Bigtable

- Go to Bigtable and click create an Instance.

- Configure your Bigtable instance accordingly.


![bigtable-instance-creation](/GCP_pictures/Study-logs/bigtable-structure/cbt-instance-creation.PNG "CBT instance creation")


- To interact with your instance, go to Cloud Shell.


- First, check to see if cbt tool is installed in the Cloud Shell.


```
cbt version
```


- Also run the command to see if the cbtrbc file exists or not:


```
cat .cbtrc
```


![first-interaction](/GCP_pictures/Study-logs/bigtable-structure/first-interaction.PNG "First interaction with Bigtable")


- You can set your project and instance accordingly by using **echo** command:


```
echo project = $DEVSHELL_PROJECT_ID > ./.cbtrc
```

```
echo instance = [your-instance-id] >> ./.cbtrc
```


![cbtrc-file](/GCP_pictures/Study-logs/bigtable-structure/cbtrc-file.PNG "CBTRC file configuration")



- To see what's inside the Bigtable:


```
cbt ls
```


![cbt-ls](/GCP_pictures/Study-logs/bigtable-structure/cbt-ls.PNG "CBT ls command")



- You can see that there is no table.


```
cbt createtable yejin-cbt-table
```


- When you verify it, you can see that a table is created:


![table-created](/GCP_pictures/Study-logs/bigtable-structure/table-created.PNG "Table created")


- Then, you can add column family by clicking Edit table.


![edit-table](/GCP_pictures/Study-logs/bigtable-structure/bigtable-add-column.PNG "Edit table")


- Above in the picture, the garbage collection policy is like a versioning of your data. So, with RDBMS system, you just update your data and the older version is wiped out. But in Bigtable, you can set your older version of data to be stored using this feature.


- To list the table and its column family, you can use the following commands:


```
cbt ls yejin-cbt-table
```

![ls-table](/GCP_pictures/Study-logs/bigtable-structure/cbt-ls-table.PNG "List your Bigtable columns")


- To insert some data into the table:


```
cbt set yejin-cbt-table John personal_data:name=John
```

```
cbt set yejin-cbt-table John personal_data:age=38
```

- If you want to read the table, you can use the command:


```
cbt read yejin-cbt-table
```

![cbt-bigtable-read](/GCP_pictures/Study-logs/bigtable-structure/cbt-bigtable-read.PNG "Table read")


- I added additional data to the column family and it is structured this way:


![additional-column-family](/GCP_pictures/Study-logs/bigtable-structure/additional-column-family.PNG "Additional data to the column family")


- Now, we have added some data to another column family - professional data. And it will show this way:


![another-column-family](/GCP_pictures/Study-logs/bigtable-structure/another-column-family-addition.PNG "Another column family data addition")

