### [Source of this study material : GCP Fundamentals for Beginners by Janakiram MSV](https://www.udemy.com/course/google-cloud-platform-gcp-fundamentals-for-beginners/)


Google Cloud Storage is a RESTful online file storage web service for storing and accessing data
on Google Cloud Platform infrastructure.

++++

* What is REST and RESTful?

REST allows clients to perform operations on the resources.

In the context of REST, reousrces are any object in your domain like documents, users, orders,
reservations, and tasks.

So, the endpoints in a RESTful API represent resources.
RESTful API needs to allow clients to act on a resource, to change some state in the system,
like creating a new reservation or updating a user's details.

After the state has been updated on the server, 
some representation of that new state needs to be returned to the client.

That's where the name Representational State Transfer (REST) comes from.

++++

It is an Infrastructure as a Service (IaaS), comparable to Amazon S3 online storage service.

Cloud Storage is a persistent storage, it is durable, replicated and also made globally available via HTTP URL.

Cloud Storage is auto scalable service.

Cloud Storage is not a file syste, because each item in Cloud Storage has unique URL.



* Key Terms of Cloud Storage

1) Buckets : Buckets are basic containers that hold your data.

Everthing that you store in Google Cloud Storage must be contained in a bucket.

You can use buckets to organize your data and control access to your data, but unlike
directories and folders, you cannot nest buckets.

2) Bucket Labels : Bucket labels are key:value metadata pairs that allow you to group your buckets.

3) Objects : Objects are the individual pieces of data that you store in Google Cloud Storage.

4) Objects have 2 components - object data and object metadata.

5) Object data component is usually a file that you store in Google Cloud Storage while
Object Metadata component is a collection of name-vale pairs that describe various object qualities.

6) Object Versioning needs to be enabled explicitly.
In absence of Object Versioning, new objects terminate the old ones.



* How to use Cloud Storage

1) Go to Cloud Storage and create a bucket

2) You can make it public over the Internet by using access control edit feature.



* How to use Cloud Storage using CLI

1) Open a Cloud Shell. Enter the following command to create a bucket:

gsutil mb gs://[your new bucket name]

2) To put in your bucket, upload some files within the CLI

3) To put a specific file to your bucket:

gsutil cp [your file name] gs://[your bucket name]

4) To copy some files in one bucket to another bucket:

gsutil cp gs://[your source bucket]/* gs://[your destination bucket]

5) To list all files within your bucket:

gsutil ls gs://[your bucket name]

6) To see if versioning is enabled in your bucket:

gsutil versioning get gs://[your bucket name]

7) To set versioning on your bucket:

gsutil versioning set on gs://[your bucket name]



======================================================


Q15. Your company is designing a disaster recovery architecture using Google Cloud Storage,
to store backup files that contain customer data.

These files will be accessed very rarely. Which storage option is most suitable?


A : Coldline Storage.

Because coldline storage is the most efficient storage class for backup files.

Coldline Storage is a better choice than Standard Storage or nearline Storage.

It is specifically designed for data that is rarely accessed and has a lower cost compared to the other storage options.

But it provides cost-efficient storage for backup files that are accessed very rarely but still need to be stored securely.

