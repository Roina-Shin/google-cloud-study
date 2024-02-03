### [Source of this study material : Google Cloud Data Engineer by Ankit Mistry](https://www.udemy.com/course/google-cloud-gcp-professional-data-engineer-certification/)


## Cloud Spanner

- Distributed & scalable solution for RDBMS in GCP

- Recommended for use where your data size is > 2 TB

- Cloud Spanner is Cloud SQL + **horizontal scalability**


## Cloud Spanner Demo

1. Create Spanner instance.

2. Create database edu_db.

3. Create 2 tables.

  - Author

    - AuthorID

    - AuthorName


  - Book

    - BookID

    - BookName

    - AuthorID


- Let's see how to configure the above in Cloud Spanner.


- Go to Cloud Spanner and click create a Spanner instance.


![cloud-spanner-instance](/GCP_pictures/Study-logs/cloud-spanner/spanner-instance.PNG "Spanner instance creation")


- Then, click Create a Database and choose **Create > Table** in the Define your schema section.


![create-db-and-table](/GCP_pictures/Study-logs/cloud-spanner/create-db-and-table.PNG "Create a db and table")



- Give a structure to the **author** table like below:


```
CREATE TABLE author (
  authorID INT64,
  authorName STRING(100)
) PRIMARY KEY (authorID);
```


![table-structure](/GCP_pictures/Study-logs/cloud-spanner/table-structure.PNG "Table structure")



- Then create the database.


- Also, click create table again and there follow the below structure:


![create-book-table](/GCP_pictures/Study-logs/cloud-spanner/interleave-tables.PNG "Interleave tables")


- Because this book table is dependent upon the author table, use the **Interleave in Parent** syntax to tell the Spanner instance to keep both tables in the same node so that the retrieval and join operations become smooth.


- In addition, add **ON DELETE CASCADE** after the Interleave in Parent syntax so that whenever you delete a record from the parent author table, the corresponding record in the book table also can be deleted.


![on-delete-cascade](/GCP_pictures/Study-logs/cloud-spanner/on-delete-cascade.PNG "On Delete Cascade")


- Then click submit to complete the creation of the book table.


- You can always check the equivalent DDL operations script after you created your table.


![ddl-operations-script](/GCP_pictures/Study-logs/cloud-spanner/ddl-operation-script.PNG "DDL Operations script")


```
CREATE TABLE author (
  authorID INT64,
  authorName STRING(100),
) PRIMARY KEY(authorID);

CREATE TABLE book (
  authorID INT64,
  bookID INT64,
  bookName STRING(200),
) PRIMARY KEY(authorID, bookID),
  INTERLEAVE IN PARENT author ON DELETE CASCADE;
```


- Now, you can insert some data into the author table.


- Go inside the author table and click Data on the left side bar. Then click Insert.


- Insert your first record as instructed on the shell. Then click Run.


![first-record-insertion0](/GCP_pictures/Study-logs/cloud-spanner/insert-first-record.PNG "Insert first record")


- Add several more records.


- Then verify it by running select query:


![select-query](/GCP_pictures/Study-logs/cloud-spanner/select-query.PNG "Select query")


- Now go back to your Spanner instance and go to book table this time.


![book-table-insert](/GCP_pictures/Study-logs/cloud-spanner/book-table-insert.PNG "Book table insert")


- In the same way, insert some data into the book table.


- Now using only the selected query run, run the query. You will see something like below:


![selected-query-run](/GCP_pictures/Study-logs/cloud-spanner/verify-book-table.PNG "Verify Book table")


- If you go to the Data section, you can see the whole data of the table:


![go-to-data](/GCP_pictures/Study-logs/cloud-spanner/go-to-data.PNG "Go to Data")


- Select one record using the **checkbox** and click Edit.


![update-table](/GCP_pictures/Study-logs/cloud-spanner/update-table.PNG "Update table")


- That is how you update your table.


- After using the Spanner, make sure you delete the Spanner instance. Otherwise, it will consume up all the free trial point.


![spanner-deletion](/GCP_pictures/Study-logs/cloud-spanner/spanner-deletion.PNG "Spanner deletion")
