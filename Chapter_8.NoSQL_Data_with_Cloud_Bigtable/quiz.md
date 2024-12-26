### Question 1

If you have 2 replicating clusters in your Bigtable instance, how can you ensure that your application will be
guaranteed strong consistency for its transactions?

1. [ ] Refactor your application so that it expects to wait 2-3 seconds after every mutation for data to become
   eventually consistent.
2. [x] Use an application profile that specifies single-cluster routing.
3. [ ] Use an application profile that specifies multi-cluster routing, but place both clusters within the same region.
4. [ ] Refactor your application so that strong consistency is no longer required.

<details>
  <summary>NOTE</summary>

```
Strong consistency can only be achieved using single-cluster routing. 
Eventual consistency is normally quick but can take several minutes depending on the distance between clusters. 
If your application requires strong consistency, refactoring is unlikely to be an option without a complete redesign.
```

</details>

### Question 2

For which types of data workload would Bigtable not be a good fit?

1. [ ] Financial data
2. [ ] Internet of things data
3. [x] Small datasets below 300GB in size
4. [ ] Time-series data
5. [x] Relational data requiring SQL-type queries

<details>
  <summary>NOTE</summary>

```
Cloud Bigtable does not support SQL queries or the multiple indexes required for true relational data.
If your dataset is too small, Bigtable won't be able to balance tables in a way that optimizes performance.
```

</details>

### Question 3

How does Bigtable manage the storage of tablets?

1. [ ] Tablets are stored in Google Colossus, so storage capacity is not an issue when defining nodes.
2. [ ] Tablets are stored on cluster nodes, but storage can dynamically grow as part of the managed service.
3. [ ] Tablets are stored in Google Colossus, but a cluster node has a limit on how much storage it can process.
4. [ ] Tablets are stored on cluster nodes, which must be sized accordingly for their storage needs.

<details>
  <summary>NOTE</summary>

```
Data is never stored in Cloud Bigtable nodes themselves; each node has pointers to a set of tablets that are stored on Colossus. 
However, CPU resources are required for a node to manage all of its associated tablets.
```

</details>

### Question 4

How does Bigtable manage rows, tables, and tablets?

1. [ ] Tables contain unsorted rows and are stored in a single tablet.
2. [x] Tables are sorted into contiguous rows and are sharded into tablets.
3. [ ] Tables are sorted into contiguous rows and are stored in a single tablet.
4. [ ] Tables contain unsorted rows, which are sharded into tablets.

<details>
  <summary>NOTE</summary>

```
A Cloud Bigtable table is sharded into blocks of contiguous rows, called tablets, to help balance the workload of queries.
```

</details>

### Question 5

Which of these identifiers would make a bad component of a row key?

1. [ ] String relating to a logical group of devices.
2. [x] Timestamp at the start of a multi-component row key.
3. [ ] String relating to a logical namespace.
4. [x] Sequential numeric ID.
5. [ ] Timestamp at the end of a multi-component row key.

<details>
  <summary>NOTE</summary>

```
Good row key design is essential.
Cloud Bigtable queries use the row key, a row key prefix, or a row range to retrieve the data.
Other types of queries trigger a full table scan, which is much less efficient.
```

</details>

### Question 6

What kind of database is Bigtable?

1. [x] NoSQL wide-column tabular database
2. [ ] NoSQL document store
3. [ ] Managed SQL-like relational database
4. [ ] Unmanaged SQL-like relational database

<details>
  <summary>NOTE</summary>

```
Cloud Bigtable is a petabyte-scale, fully managed NoSQL database service for 
large analytical and operational workloads that typically uses wide-column tables.
```

</details>

### Question 7

What action should you take if you observe that Bigtable performance is poor on a subset of queries?

1. [ ] Add more nodes to the cluster to increase the overall storage capacity.
2. [ ] Add debugging steps to your application to identify the problematic queries.
3. [x] Use the Key Visualizer tool to identify hot spots and consider changing how the row key distributes rows.
4. [ ] Add an additional cluster to the instance to increase the read and write throughput.

<details>
  <summary>NOTE</summary>

```
If a subset of queries are performing poorly, there is likely a hot spot being caused by the row key design.
Key Visualizer provides a heatmap of the load across your entire table in a way that is 
difficult to understand using standard debugging techniques.
Increasing the size of a cluster is not a long term solution, and adding additional clusters will not affect write throughput.
```

</details>

### Question 8

In a region with 4 zones, what is the maximum number of Bigtable clusters available?

1. [x] 4
2. [ ] 3
3. [ ] 5
4. [ ] There is no limit, providing you are within the Compute Engine quotas of your GCP project.

<details>
  <summary>NOTE</summary>

```
In a region with 4 zones, a Bigtable instance can contain up to 4 clusters.
Compute Engine is a red herring, it has nothing to do with Cloud Bigtable.
```

</details>

### Question 9

Bigtable is compatible with which open source project's client library for Java?

1. [x] Apache HBase
2. [ ] Apache Cassandra
3. [ ] MongoDB
4. [ ] Apache Kafka

<details>
  <summary>NOTE</summary>

```
Cloud Bigtable is exposed to applications through multiple client libraries, including a supported extension to the 
Apache HBase library for Java. As a result, it integrates with the existing 
Apache ecosystem of open-source Big Data software.
```

</details>

### Question 10

Which of these identifiers would make a good component of a row key?

1. [x] Reverse domain name
2. [x] String identifier
3. [ ] 64-character UUID
4. [ ] Domain name
5. [ ] Hashed string identifier

<details>
  <summary>NOTE</summary>

```
A reverse domain name would make a good row key, especially if each row's data overlaps with adjacent rows. This allows Cloud Bigtable to compress your data more efficiently.

See: https://cloud.google.com/bigtable/docs/schema-design

Good row key design is essential. 
Cloud Bigtable queries use the row key, a row key prefix, or a row range to retrieve the data.
Other types of queries trigger a full table scan, which is much less efficient.
Using human-readable values makes it much easier to troubleshoot issues with Cloud Bigtable. 
See: https://cloud.google.com/bigtable/docs/schema-design
```

</details>


