### [Source of this study material : GCP Fundamentals for Beginners by Janakiram MSV](https://www.udemy.com/course/google-cloud-platform-gcp-fundamentals-for-beginners/)


Cloud Bigtable is Google's NoSQL Big Data database service. 

Bigtable is a sparse, distributed, persistent storage system for structured data.

Bigtable doesn't support RDBMS concept.

Google Map, Google Earth, Gmail and YouTube fare all powered by Bigtables.

* Features of Bigtable

It can efficiently handle large scale of data: petabytes and across thousands of commodities.

No schema database.

Suitable for handling semi structured data.

Self-managed and handle massive workload with consistent low latency and high throughput.

Bigtable is a sparse, distributed, persistent multidimensional sorted map.

Map is indexed by a row key, column key, and a timestamp; 
each value in the map is an uninterpreted array of bytes.

HBase uses a data model very similar to that of Bigtable. 
Users store data rows in labeled tables. 
(HBase is an open source and you need to manage data in the HBase.)

A data row has a sortable key and an arbitrary number of columns.
-> The number of columns for each row is not defined.

Map :

At it's core both Bigtable and Hbase are map.

An abstract data type composed of a collection of keys and values,
where each key is associated with one value.

e.g.)

{
    "zzzzz" : "woot"
    "xyz" : "hello"
    "1" : "x"
    "aaaa" : "y"
}

- persistent
Persistent means data created in Bigtable will persist after the program which created it finished.

- distributed
Bigtable uses the distributed file system, so that underlying file system is spread on multiple nodes.

Data is also replicated across participating nodes which saves us against the cluster failing.

- sorted
Map implementations in Bigtable keep the key/value pairs in strict alphabetical order.

Bigtable only supports the string type data.
But it doesn't mean you can't store numbers.
It just means the internal data type is string but you can store anything as 'string'.

Bigtable system tends to be huge and distributed that its sorting feature is important.

This ensures that when you scan the table,
the items of greatest interest are near each other.

e.g.)

{
    "1" : "x"
    "aaaaa" : "y"
    "aaaab" : "world"
    "xyz" : "hello"
    "zzzzz" : "woot"
}

Remember! Row key is always sorted in a strict alphabetical order.


* Advantages of Bigtable

1) Incredibly scalable : 
Cloud Bigtable scales in direct proportion to the number of machines in your cluster.

2) Simple administration :
Cloud Bigtable handles upgrades and restarts transparently, and it automatically maintains
high data durability. 

To replicate your data, simply add a second cluster to your instance,
and replication starts automatically.

3) Cluster resizing without downtime :
You can increase the size of a Cloud Bigtable cluster for a few hours to handle a large load,
then reduce the cluster's size again--all without any downtime.

* Use cases of Bigtable

Bigtable is ideal for applications that need very high throughput and scalability
for key/value data, where each value is typically no larger than 10MB.

Time-series data, such as CPU and memory usage over time for multiple servers.

Marketing data, such as purchase histories and customer preferences.

Financial data, such as transaction histories, stock prices, and currency exchange rates.

Internet of things data, such as usage reports from energy meters and home appliances.

Graph data, such as information about how users are connected to one another.


-------------


Cloud Bigtable stores data in massively scalable tables, each of which is a sorted key/value map.

Table is composed of rows, each of which typically describes a single entity,
and columns, which contain individual values for each row.

Each row is indexed by a single row key, and columns that are related to one another
are typically grouped together into a column family.

Unlike traditional RDBMS implementation where ach row is stored contiguous on disk,
Bigtable on the other hand stores each column contiguously on disk.

Column oriented layout is also very effective to store very sparse data
(many cells have NULL value) as well as multi-value cell.


In the Bigtable mode, the basic data storage unit is a cell.

User can addreess a data element by the row id, column name and the timestamp.

At the configuration level, Bigtable allows the user to specify how many versions can be
stored within each cell either by count (how many) or by freshness (how old).

Data within a column family usually has a similar pattern, data compression can be very effective.

Write happens by first appending a transaction entry to a log file
followed by writing the data into an in-memory Memtable.

So whenever you are sending a write request to the Bigtable,
that request will be noted down to a log file with the transaction entry.

And then Bigtable picks up the data from that particular log file in the Memtable
and it will be returned down to the shared table (or SSTable).

All the latest update stored in the Memtable which will grow until reaching a size threshold,
then it will flush the Memtable to the disk as an SSTable (sorted by the string key).

Over a period of time there will be multiple SSTables on the disk that store the data.


- Read :
On read request, system will first look up the Memtable by its row key to see if
it contains the data. 

If not, it will look at the on-disk SSTable to see if the row-key is there.

Cloud Bigtable instance is a container for data.
Instances have one or more clusters, located in different zones.
Each cluster has at least 1 node.

A table belongs to an instance, not to a cluster or node.

When a user creates an instance, the user must choose whether the instance's clusters
will store data on solid-state drives (SSD) or hard disk drives (HDD).

SSD is recommended disk for Bigtable.

Bigtable uses the instance to store application profiles.
For instances that use replication, app profiles control how your applications connect
to the instance's clusters.



---------------


- Columnar Database : a columnar database is a type of database that stores data
using a column oriented model.

Columnar databse uses a concept called a keyspace. 
A keyspace is kind of like a schema in the relational model.

The keyspace contains all the column families (kind of like tables in the relational model)
which contain rows and columns.

A column family consists of multiple rows.

- Row Key. Each row has a unique key which is a unique identifier for that row.

- Column. Each column contains a name, value, and timestamp.


--------------


Cloud Bigtable delivers highly predictable performance that is linearly scalable.

Each Cloud Bigtable node can provide the following approximate throughput, depending on
which type of storage the cluster uses:

SSD - up to 10,000 rows per second

HHD - up to 500 rows per second

Cluster's performance increases linearly as you add nodes to the cluster.

Replication improves read throughput, especially in multi-cluster routing.

Replication does not increase write throughput. Write throughput might actually go down
because replication requires each cluster to do additional work.

Replicated clusters in different regions will typically have higher replication latency
than replicated in the same region.

