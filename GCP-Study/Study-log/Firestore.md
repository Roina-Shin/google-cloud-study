### [Source of this study material : Google Cloud Data Engineer by Ankit Mistry](https://www.udemy.com/course/google-cloud-gcp-professional-data-engineer-certification/)


## Cloud Firestore/Datastore

- Highly scalable NoSQL database

- Serverless

- Document kind data storage - MongoDB

- SQL like queries - GQL

- Support ACID transaction

- Multiple indexes

- Data replication across different regions

- Use case:

  - Session info

  - Product catalog

- Export data from gcloud utility only


## How to use Datastore


- Go to Datastore and click create Entity.


![datastore-ui](/GCP_pictures/Study-logs/firestore/datastore-ui.PNG "Datastore UI")


- Put in some kind name (kind = table) and properties as well.


![entity-creation](/GCP_pictures/Study-logs/firestore/entity-creation.PNG "Entity creation")


- Once again, click create Entity again.


- Now, you have 2 entities created.


![two-entities-created](/GCP_pictures/Study-logs/firestore/two-entities-created.PNG "2 entities created")


- You can use GQL to query inside the Kind.


![use-GQL](/GCP_pictures/Study-logs/firestore/use-gql.PNG "Use GQL")



## How to use Firestore


- When you first go to Firestore, you are prompted to choose either Native or Datastore mode. Go with the Native mode.


![firestore-ui](/GCP_pictures/Study-logs/firestore/firestore-ui.PNG "Firestore UI")


- Then select region and go ahead to create a database.


- Now, you are prompted to start a collection. Here, collections are like **talbes**.


- Start a collection and add a document inside it.


![start-collection-and-document](/GCP_pictures/Study-logs/firestore/firestore-document-addition.PNG "Start collection and document")


- So, inside the **user** collection, we have **ZVGBJmwRjkS2M4p6LNp7** document, and inside the document, we have userName and userID fields.


![document-structure](/GCP_pictures/Study-logs/firestore/document-structure.PNG "Document structure")


- Inside the collection, you can add more documents as you like. 


![add-more-documents](/GCP_pictures/Study-logs/firestore/add-more-documents.PNG "Add more documents")


