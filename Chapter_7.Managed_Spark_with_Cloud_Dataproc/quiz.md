### Question 1

Which native output connectors are supported by Dataproc?

1. [x] Cloud Storage
2. [ ] Cloud SQL
3. [x] Cloud Bigtable
4. [ ] Cloud Firestore
5. [x] BigQuery

<details>
  <summary>NOTE</summary>

```
Cloud Dataproc has built-in integration with BigQuery, Cloud Storage, Cloud Bigtable, Stackdriver Logging, and Stackdriver Monitoring.
```

</details>

### Question 2

Your customer would like to use Dataproc, but the standard image does not contain some additional Spark components
required to run their jobs on the ephemeral clusters. What would you recommend?

1. [ ] Split the customer workloads into 2 clusters. Where the extra components are not required, use Dataproc. Where
   extra components are required, build a custom image and use it to deploy a custom Spark cluster using Compute Engine.
2. [x] Create custom Dataproc image that fulfils the customer requirements and use it to deploy a Dataproc cluster.
3. [ ] Create an image that fulfils the customer requirements and use it to deploy a custom Spark cluster using Compute
   Engine.
4. [ ] Use a Dataproc cluster, but specify an initialization action that installs all of the additional components.

<details>
  <summary>NOTE</summary>

```
Cloud Dataproc clusters can be provisioned with a custom image that includes a user's pre-installed packages. 
You could alternatively use initialization actions to install the additional components, 
but this would be less efficient and incur more running time for ephemeral clusters.
```

</details>

### Question 3

Which features are not compatible with Dataproc autoscaling?

1. [ ] Preemptible Workers
2. [x] Spark Structured Streaming
3. [ ] High-Availability Clusters
4. [x] YARN Node Labels
5. [ ] MapReduce Tasks

<details>
  <summary>NOTE</summary>

```
Autoscaling is not compatible with Spark Structured Streaming since Spark Structured Streaming currently
does not support dynamic allocation.

Autoscaling does not support YARN node labels, nor the property `dataproc:am.primary_only`. 
YARN incorrectly reports cluster metrics when node labels are used. 

https://cloud.google.com/dataproc/docs/concepts/configuring-clusters/autoscaling
```

</details>

### Question 4

Which primary Apache services does Dataproc run?

1. [ ] Dataflow
2. [x] Hadoop
3. [ ] Kafka
4. [x] Spark
5. [ ] Cassandra

<details>
  <summary>NOTE</summary>

```
Cloud Dataproc is a managed Spark and Hadoop service that lets you take advantage of open source data tools
for batch processing, querying, streaming, and machine learning.
```

</details>

### Question 5

True of False: Preemptible workers in a Dataproc cluster cannot store HDFS data.

1. [x] True
2. [ ] False

<details>
  <summary>NOTE</summary>

```
Since preemptibles can be reclaimed at any time, preemptible workers do not store data.
```

</details>

### Question 6

A customer wants to run Spark jobs on a low-cost ephemeral Dataproc cluster, utilizing preemptible workers wherever
possible, but needs to store the results of Dataproc jobs persistently. What would you recommend?

1. [ ] Use a secondary group of preemptible worker nodes, but ensure there is enough persistent storage on the primary (
   non-preemptible) worker nodes to store all of the data.
2. [ ] Do not use preemptible workers at all, it will prevent you from choosing any persistent storage option.
3. [ ] Use a secondary group of preemptible worker nodes, but add custom code to a job that copies its results to Cloud
   Storage.
4. [x] Use the Cloud Storage connector, and specify GCS locations for the input and output of jobs.

<details>
  <summary>NOTE</summary>

```
The Cloud Storage connector lets you run Apache Hadoop or Apache Spark jobs directly on data 
in Cloud Storage and offers a number of other benefits over HDFS.
```

</details>

### Question 7

Which GCP product implements the Apache Beam SDK and is sometimes recommended as an alternative to Dataproc particularly
for streaming data?

1. [ ] Cloud Composer
2. [ ] Cloud Data Fusion
3. [x] Cloud Dataflow
4. [ ] Cloud Datalab

<details>
  <summary>NOTE</summary>

```
The Apache Beam SDK is an open source programming model that enables you to develop both batch and streaming pipelines.
You create your pipelines with an Apache Beam program and then run them on the Dataflow service.
```

</details>
