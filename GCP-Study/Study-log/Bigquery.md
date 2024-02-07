### [Source of this study material : Google Cloud Data Engineer by Ankit Mistry](https://www.udemy.com/course/google-cloud-gcp-professional-data-engineer-certification/)


## Bigquery

- Fully managed, serverless, scalable data warehouse

- Supports both batch & streaming data ingestion

- Results are cached

- Supports for AI/ML models

  - Build ML model directly with SQL

  - Integrated with Tensorflow


## Bigquery Usecase

- Using public data (Newyork citibike), group by **gender** and count the number of each gender.


![count-query](/GCP_pictures/Study-logs/bigquery/count-query.PNG "Count query")


- **Extract** the year of stoptime and list the gender of the users where their birth_year = 1988.


![extract-query](/GCP_pictures/Study-logs/bigquery/extract-query.PNG "Extract query")


- Create a dataset.


![dataset-creation](/GCP_pictures/Study-logs/bigquery/dataset-creation.PNG "Dataset creation")


- Using the Cloud Shell, you can also create a dataset:


```
bq mk [new_dataset]
```


![bq-command](/GCP_pictures/Study-logs/bigquery/bq-command.PNG "bq command - dataset creation")



- To list the dataset, use the command:


```
bq ls --format=prettyjson
```


![bq-ls-prettyjson](/GCP_pictures/Study-logs/bigquery/bq-ls-prettyjson.PNG "bq ls --format=prettyjson")


- To import a table from the Cloud Storage, first click Create a Table:


![import-table-from-gcs](/GCP_pictures/Study-logs/bigquery/import-table-from-gcs.PNG "Import table from GCS")



## Bigquery Partition


- One of the reasons why we use partition in Bigquery is because it reduces **data scanning cost**. 

- When you scan a large dataset, you have to pay for the scanning even if you specified a certain limit to the data range.

- In that case, **partitioning your data** can help reduce the cost.

- The following case asks for you a large data scan fee for just looking for data **where date = 2017-11-19 12:22:00 UTC**.


![large-dataset](/GCP_pictures/Study-logs/bigquery/large-dataset.PNG "Large dataset")



- So we are going to create our own table to put the public dataset into, while using Cloud Shell:


```
bq query \
  --use_leagacy_sql=false \
  --destination_table [dataset_name].[table_name] \
  --time_partitioning_field [field_name_on_which_you_want_to_partition] \
  --time_partitioning_type [data_type_that_you_want_to_partition] \
 'SELECT * FROM `bigquery-public-data.chicago_crime.crime`'
```


```
bq query \
  --use_leagacy_sql=false \
  --destination_table yejin_bq_partition.public_crime \
  --time_partitioning_field date \
  --time_partitioning_type MONTH \
 'SELECT * FROM `bigquery-public-data.chicago_crime.crime`'
 ```


- Keep in mine that your dataset is living in the same region as the public dataset. Otherwise, it will result in error.


![bq-partition-query](/GCP_pictures/Study-logs/bigquery/bq-partition-command.PNG "bq partition query")



- Now, you can see that the partitioned table is loaded onto our dataset from public dataset.



![partitioned_data](/GCP_pictures/Study-logs/bigquery/partitioned_table.PNG "Partitioned table")


- If you go to your copied table and try to query the same thing as on the public dataset, you will see that the query cost is drastically reduced now:


![query-cost-reduced](/GCP_pictures/Study-logs/bigquery/query-cost-reduced.PNG "Query cost reduced")



![simple-data-query](/GCP_pictures/Study-logs/bigquery/simple-data-query.PNG "Simple data query")


- To know the number of partitions in your table, you can query:


```
SELECT  *
FROM
  `storied-polymer-406703.yejin_bq_partition.INFORMATION_SCHEMA.PARTITIONS`
WHERE
  table_name = 'public_crime'
```


![partition-number-query](/GCP_pictures/Study-logs/bigquery/partition-number-query.PNG "Querying the number of partitions in the table")


- The number of partitions here is 277.


![277-partitions](/GCP_pictures/Study-logs/bigquery/277-partitions.PNG "277 partitions")



## Bigquery Clustering


- With number type data (INTEGER, DATE...) partitioning helps reduce the cost of data scan. 

- Now, with the text type data, you can use **clustering** in the same way.


```
bq query \
  --use_legacy_sql=false \
  --clustering_fields primary_type \
  --destination_table yejin_bq_partition.clustered_crime \
  --time_partitioning_field date \
  --time_partitioning_type MONTH \
 'SELECT * FROM `bigquery-public-data.chicago_crime.crime`'
```

- With the same public dataset, we are going to divide the data by **primary_type** which is crime type.

  - theft, narcotics, prostitution, etc.


- After firing that cluster query, you will see that a new table is added to your dataset that is **clustered by** primary_type.


![clustering-query](/GCP_pictures/Study-logs/bigquery/clustering-query.PNG "Clustering query")


![clustered-table](/GCP_pictures/Study-logs/bigquery/clustered-table.PNG "Clustered table")


- Now, when you do the query on both the clustered table and the public dataset table, you will see the difference in costs:


![clustered-reduced-cost](/GCP_pictures/Study-logs/bigquery/reduced-cost-clustered.PNG "Clustered reduced cost")


![public-huge-cost](/GCP_pictures/Study-logs/bigquery/public-huge-cost.PNG "Public dataset table with huge cost")


