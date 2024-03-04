### [Source of this study material : Google Cloud Data Engineer by Ankit Mistry](https://www.udemy.com/course/google-cloud-gcp-professional-data-engineer-certification/)


## Data Catalog

- Most organizations today are dealing with a large and growing number of data assets.


- Data stakeholders (consumers, producers, and administrators) face a number of challenges.

  - Searching for insightful data assets

  - Understanding data

  - Making your data useful


- **Data Catalog**

- A fully managed and highly scalable **data discovery and metadata management service**.


- A single place to discover all data, assets across all projects


- Using Data Catalog, you can search data assets and tag individual data



## Data Catalog Demo

- You can simply search your data's data (field name, etc.) in Data Catalog.


- In my BigQuery dataset, I have a baseball_scatter_plots table. In that table, I have a field named TeamID.


- Suppose you don't know which table has the **TeamID** field but you know the table is in BigQuery. You can go to Data Catalog and search for **TeamID** there.


![bigquery-table](/GCP_pictures/Study-logs/data-catalog/baseball-table.PNG "Baseball table")


- And you will see that the table appears in the search result.


![data-catalog-search-result](/GCP_pictures/Study-logs/data-catalog/data-catalog-search-result.PNG "Data catalog search result")


- You can even search data across projects in your organization. You can select the projects to search data in, and get the proper result.


![select-project](/GCP_pictures/Study-logs/data-catalog/select-project.PNG "Select project")

