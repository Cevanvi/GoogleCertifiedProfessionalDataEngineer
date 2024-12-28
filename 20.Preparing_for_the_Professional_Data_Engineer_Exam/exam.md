### Question 1

In order to protect live customer data, your organization needs to maintain separate operating environments
development/test, staging, and production to meet the needs of running experiments, deploying new features, and serving
production customers. What is the best practice for isolating these environments while at the same time maintaining
operability?

1. [ ] Place all three environments in the same project, however, use separate Cloud Storage buckets, Cloud ML Engine
   clusters, and other services for each environment
2. [ ] Place resources into the same project. but use object versioning in Cloud Storage in order to separate data by
   environment.
3. [ ] Create a separate project for dev/test, staging, and production. Migrate relevant data between projects when
   ready for the next stage.
4. [ ] Create separate organization accounts for each environment, and use domain wide IAM roles to allow access between
   each organization environment to share data as needed.

Best practices are to maintain separate projects for each environment for full isolation. You will then want to migrate
data between environments in separate projects using proper CI/CD orchestration tools. [Creating and Managing Projects |
Resource Manager Documentation](https://cloud.google.com/resource-manager/docs/creating-managing-projects)

### Question 2

You need to run analytical queries using SQL syntax against data formatted in JSON format. What should you do? Choose
the best answer.

1. [ ] Load your JSON data into Cloud SQL, and run queries against it in that service.
2. [ ] Import the data into Bigtable and use Bigtable for your queries.
3. [ ] Load your JSON data into Cloud Storage. Add your JSON table as an external read source in BigQuery, since
   BigQuery is unable to store data in JSON format.
4. [x] Import the data in JSON format into BigQuery as a table, and run queries against it.

While Cloud SQL can store data in JSON format, BigQuery is better suited to the task of running analytical queries
against JSON data. BigQuery can natively store and query JSON data. You could read from Cloud Storage as an external
source, but it is not necessary. Bigtable does not use SQL format for querying data. [BigQuery documentation | Google
Cloud](https://cloud.google.com/bigquery/docs)

## Question 3

You need to design a data pipeline that will allow you to ingest TBs data for later analysis as both large-scale SQL
aggregations and small range-scan lookups. What would be a good approach to this?

1. [x] Ingest data through Cloud Dataflow. Use multiple transformations to output to BigQuery for SQL aggregate queries,
   and Bigtable for range-scan queries.
2. [ ] Ingest data through Cloud Dataflow. Output to Cloud Datastore to support both use cases.
3. [ ] Create a copy of all incoming data and ingest through two separate Cloud Dataflow pipelines, one for each use
   case.
4. [ ] Ingest data through Cloud Dataflow. Output to Cloud Spanner to support both use cases.

Large scale aggregated SQL queries are best run on BigQuery, whereas small range-scan lookups across TBs of data work
best on Cloud Bigtable. By using a single Cloud Dataflow pipeline you can ingest data into both systems at the same time
and have your choice of query method. Datastore and Spanner would not support both types of query. Cloud Solutions
[Architecture Reference](https://gcp.solutions/diagram/bd-data-lake)

## Question 4

You want to load a set of authors into a Cloud Spanner database and then perform indexed searches based on their name or
primary writing genre. How would you design this and implement it efficiently?

1. [ ] When creating the table, use a unique ID for each record as your primary key. Later, when loading the data, use
   secondary indexes for both your author-name field and your genre field.
2. [ ] Use the author name as the primary key, and add genre as a secondary index once the data is loaded.
3. [ ] When creating the table, use a unique ID for each record as your primary key. Later, when loading the data, use a
   secondary index for the author-name field. Add the genre field later only if necessary.
4. [x] When creating the table, use a unique ID for each record as your primary key, and use secondary indexes for both
   your author-name field and your genre field.

When creating any database table for a relational database like Spanner, you definitely want to have a unique ID (
typically numeric) for each record as your primary key (which is automatically indexed) rather than something like "
author name," since it's entirely possible you could have two (or twenty!) authors with the same name. So, you would
want secondary indexes for both your author-name field and your genre field. The exam question hinges on what's the most
efficient method to do that. Google docs say that "The most efficient time to add a secondary index is when you create
the table. To create a table and its indexes at the same time, send the DDL statements for the new table and the new
indexes in a single request to Spanner."
Reference: [Secondary Indexes](https://cloud.google.com/spanner/docs/secondary-indexes)

## Question 5

You need to ingest streaming and batch data into BigQuery, but each row must be annotated with a unique identifier that
is created by a 3rd party HTTP system. What is the best way to achieve this?

1. [ ] Write a Cloud Function that calls the external HTTP service for the unique identifier and then writes the record
   to BigQuery. Stream data through Cloud Pub/Sub and call the Cloud Function for each row.
2. [ ] Use a Javascript User Defined Function in BigQuery to populate the unique identifier once the data has been
   loaded.
3. [ ] Write a batch script that runs on Compute Engine that can annotate the unique identifers for all data records,
   then send the final data to BigQuery.
4. [x] Create a DoFn function in Cloud Dataflow that calls out to the external HTTP service for the unique identifier.

The most efficient way to achieve this outcome is by calling the 3rd party HTTP service from within a DoFn function in
Cloud Dataflow. This can be done as part of the data pipeline in Dataflow during ingestion, without requiring external
compute resources or Cloud
Functions. [Beam Programming Guide](https://beam.apache.org/documentation/programming-guide/#core-beam-transforms)

## Question 6

You are designing a system to send log messages into GCP for later analysis in BigQuery. Messages will be ingested via
Cloud Pub/Sub to allow for buffering and availability, but the publishing order of messages will be an important part of
the final searches performed on the data. How can you approach this?

1. [ ] Rely on the order of rows in BigQuery for message ordering, but alter searches to compensate for the occasional
   duplicate message.
2. [ ] Use an Apache Kafka instance on Compute Engine instead of Cloud Pub/Sub to guarantee the order of messages.
3. [x] Attach a timestamp to every message in the publishing system.
4. [ ] Process the messages through Cloud Dataflow to attach a timestamp at the point of ingestion.

If you are designing the ingestion system and are able to do so, attaching a timestamp that can be read later is the
quickest way to ensure that the publishing order of messages can be understood, even if the order of delivery is not
guaranteed by Pub/Sub. The order of rows will not provide the publishing order, and Kafka is not required.[ Ordering
messages | Cloud Pub/Sub Documentation | Google Cloud](https://cloud.google.com/pubsub/docs/ordering)

## Question 7

You are migrating a Hadoop cluster to Cloud Dataproc using GCS for storage. After migration, some of your existing, more
complex Spark jobs (in Parquet format) are performing noticeably worse than your on-premises cluster. You are using
mostly preemptible VMs (with a few required non-preemptible VMs) in order to save on costs. What is the best way to
address the performance issue?

1. [ ] Increase the size of your cluster by twice as many preemptible VMs.
2. [ ] Change your file format to CSV format.
3. [ ] Switch your disks from HDD to SSD, and run the job in HDFS before copying the results back to GCS.
4. [x] For the non-preemptible worker nodes, switch the disks from HDD to SSD. Change the default preemptible VM
   settings to increase the size of the boot disk.

By default, preemptible node disk sizes are limited to 100 GB or the size of the non-preemptible node disk sizes,
whichever is smaller. However, you can override the default preemptible disk size to any requested size. Since the
majority of our cluster is using preemptible nodes, the size of the disk used for caching operations will see a
noticeable performance improvement using a larger disk. SSDs will perform better than HDDs, but SSDs are not
available on preemptible worker nodes. CSV format would perform worse than Parquet. Increasing the cluster size may
also improve performance, but at a greater additional cost than these other steps. [Dataproc Documentation | Google
Cloud](https://cloud.google.com/dataproc/docs)

## Question 8

Your customer is looking to migrate their time-series database to Google Cloud Platform. Their developers are very
familiar with Apache HBase. Which managed database service would you recommend?

1. [ ] Cloud SQL
2. [ ] BigQuery
3. [x] Cloud Bigtable
4. [ ] Cloud Spanner

Cloud Bigtable is an ideal choice for time-series data and offers an HBase-compliant API. Spanner, Cloud SQL and
BigQuery are relational databases that are not suitable for time-series data. [Cloud Bigtable and the HBase API | Cloud
Bigtable Documentation](https://cloud.google.com/bigtable/docs/hbase-bigtable)

## Question 9

You are building a data pipeline on Google Cloud. You need to prepare source data for a machine-learning model. This
involves quickly de-duplicating rows from three input tables and also removing outliers from data columns where you do
not know the data distribution. What should you do?

1. [ ] Use Cloud Dataprep to preview the data distributions in sample source data table columns. Write a recipe to
   transform the data and add it to the Cloud Dataprep job.
2. [ ] Write an Apache Spark job with a series of steps for Cloud Dataproc. The first step will examine the source data,
   and the second and third steps will perform data transformations.
3. [ ] Write an Apache Spark job with a series of steps for Cloud Dataflow. The first step will examine the source data,
   and the second and third steps will perform data transformations.
4. [x] Use Cloud Dataprep to preview the data distributions in sample source data table columns. Click on each column
   name, click on each appropriate suggested transformation, and then click Add to add each transformation to the Cloud
   Dataprep job.

Dataprep is the correct choice because of the requirements to prepare/clean source data. For de-duplication, using the
suggestion transformation would be easier and quicker than writing a recipe, which is more work than
needed. [Dataprep by
Trifacta documentation](https://cloud.google.com/dataprep/docs)

## Question 10

Your customer has multiple systems that all need to be notified of orders being processed. How should you configure
Pub/Sub?

1. [ ] Create a new Topic for each individual order. Create a Subscription for each Topic that can be shared by every
   system that needs to be notified.
2. [ ] Create a new Topic for each individual order. Create multiple Subscriptions for each Topic, one for every system
   that needs to be notified.
3. [x] Create a Topic for orders. Create multiple Subscriptions for this Topic, one for every system that needs to be
   notified.
4. [ ] Create a Topic for orders. Create a Subscription for this Topic that can be shared by every system that needs to
   be notified.

Cloud Pub/Sub guarantees to deliver messages at least once to every subscriber. As multiple systems need to be notified
of every order, you should create one topic and use multiple subscribers. [Pub/Sub: A Google-Scale Messaging Service |
Cloud Pub/Sub](https://cloud.google.com/pubsub/architecture)

## Question 11

You want to use Pub/Sub to distribute jobs to a group of Compute Engine VMs, which should each take the next job from
the queue. How should you configure Pub/Sub?

1. [ ] Create a Topic for jobs. Create multiple Subscriptions for this Topic, one for every Compute Engine VM in the
   group.
2. [ ] Create a new Topic for each individual job. Create a Subscription for each Topic that can be shared by every
   Compute Engine VM in the group.
3. [x] Create a Topic for jobs. Create a Subscription for this Topic that can be shared by every Compute Engine VM in
   the group.
4. [ ] Create a new Topic for each individual job. Create multiple Subscriptions for each Topic, one for every Compute
   Engine VM in the group.

Each Compute Engine VM should take the next job from the queue in the Cloud Pub/Sub topic. To avoid duplication of
tasks, all the VMs should share the same
subscription. [Pub/Sub: A Google-Scale Messaging Service | Cloud Pub/Sub](https://cloud.google.com/pubsub/architecture)

## Question 12

You are designing storage for event data as part of building a data pipeline on Google Cloud. Your input data is in CSV
format. You want to minimize the cost of querying individual values over time windows. Which storage service and schema
design should you use?

1. [x] Use Cloud Bigtable for storage. Design tall and narrow tables, and use a new row for each single event version.
2. [ ] Use Cloud Storage for storage. Join the raw file data with a BigQuery log table.
3. [ ] Use Cloud Storage for storage. Write a Cloud Dataprep job to split the data into partitioned tables.
4. [ ] Use Cloud Bigtable for storage. Design short and wide tables, and use a new column for each single event version.

You will want to use Bigtable for this 'values over time' scenario. Using tall and narrow tables is the best practice
for this use case, using a new row, not a new column for each event. You should not use Cloud Storage or BigQuery for
this scenario. [Concepts | Cloud Bigtable Documentation | Google Cloud](https://cloud.google.com/bigtable/docs/concepts)

## Question 13

Your customer is a financial organization that requires a transactionally consistent relational database that can be
accessed from multiple regions. Which database solution would you recommend?

1. [ ] Cloud Bigtable
2. [x] Cloud Spanner
3. [ ] Cloud SQL for MySQL with multi-regional read replicas
4. [ ] Cloud SQL for Postgres with multiple masters and custom replication

Cloud Spanner is the only database service that guarantees strong transactional consistency when accessed across
multiple regions.
[Cloud Spanner: TrueTime and external consistency](https://cloud.google.com/spanner/docs/true-time-external-consistency)

## Question 14

As part of your backup plan, you create regular boot-disk snapshots of Compute Engine instances that are running. You
want to be able to restore these snapshots using the fewest possible steps for replacement instances. What should you
do?

1. [ ] Export the snapshots to Cloud Storage. Create disks from the exported snapshot files. Create images from the new
   disks.
2. [x] Use the snapshots to create replacement instances as needed.
3. [ ] Use the snapshots to create replacement disks. Use the disks to create instances as needed.
4. [ ] Export the snapshots to Cloud Storage. Create images from the exported snapshot files.

Exporting an image to Cloud Storage is considered best practices for disaster recovery scenarios, but not for the above
requirements. It would also require more steps than necessary. You can recreate instances directly from a boot-disk
snapshot, and snapshots let you recreate instances in the fewest
steps. [Restoring and deleting persistent disk snapshots](https://cloud.google.com/compute/docs/disks/restore-and-delete-snapshots)

## Question 15

Which of these open source frameworks is best suited to process simultaneous batch and streaming in a single data
pipeline?

1. [ ] Apache Kafka
2. [ ] Apache Hadoop
3. [ ] Kubernetes
4. [x] Apache Beam

Apache Beam is the open source SDK for batch and stream
processing. [Programming model for Apache Beam](https://cloud.google.com/dataflow/docs/concepts/beam-programming-model)

## Question 16

You are setting up Cloud Dataproc to perform some data transformations using Apache Spark jobs. The data will be used
for a new set of non-critical experiments in your marketing group. You want to set up a cluster that can transform a
large amount of data in the most cost-effective way. What should you do?

1. [x] Set up a cluster in Standard mode with high-memory machine types. Add 10 additional Preemptible worker nodes.
2. [ ] Set up a cluster in High Availability mode with high-memory machine types. Add 10 additional local SSDs.
3. [ ] Set up a cluster in High Availability mode with default machine types. Add 10 additional Preemptible worker
   nodes.
4. [ ] Set up a cluster in Standard mode with the default machine types. Add 10 additional local SSDs.

High availability mode is not necessary for non-mission critical workloads and is higher cost than necessary. Since this
is a non-critical workload, using standard mode instead of high availability, and using preemptible nodes can both help
save costs. High-memory machine types that are geared toward workloads that require a higher ratio of RAM to vCPU are
useful when transforming a large amount of data. Local SSD's are also an additional, non-needed cost. High availability
mode is not necessary for non-mission critical workloads and is higher cost than necessary. Local SSD's are also an
additional, non-needed cost. [Dataproc Documentation | Google Cloud](https://cloud.google.com/dataproc/docs)

## Question 17

Your production Bigtable instance is currently using four nodes. Due to the increased size of your table, you need to
add additional nodes to offer better performance. How should you accomplish this without the risk of data loss?

1. [x] Edit instance details and increase the number of nodes. Save your changes. Data will re-distribute with no
   downtime.
2. [ ] Export your Bigtable data as sequence files into Cloud Storage, then import the data into a new Bigtable instance
   with additional nodes added.
3. [ ] Power off your Bigtable instance, then increase the node count, then power back on. Be sure to schedule downtime
   in advance.
4. [ ] Use the node migration service to add additional nodes.

You can add/remove nodes to Bigtable with no downtime necessary. [Overview of Cloud Bigtable | Cloud Bigtable
Documentation](https://cloud.google.com/bigtable/docs/overview)

## Question 18

You have a Dataflow job that keeps failing due to errors in your input data. What steps can you take to improve pipeline
reliability and output the failed data for later analysis using a service that allows data integration pipelines to
ingest and distribute data?

1. [ ] Implement a try-catch block that transforms both the good and bad data, and extract the incorrect entries from
   Stackdriver Logging.
2. [x] Implement a try-catch block that transforms both the good and bad data. Create an additional output to use a new
   PCollection that can be output to Pub/Sub for later analysis.
3. [ ] Implement a try-catch block that transforms both the good and bad data. Publish the erroneous data to Pub/Sub,
   which can then be placed into GCS for further analysis.
4. [ ] Filter out errors as they occur, and view error entries using Stackdriver Logging.

Your pipeline needs to use an additional side output, within a try-catch block, that uses a PCollection to output
erroneous data to Pub/Sub. Pub/Sub is used for streaming analytics and data integration pipelines to ingest and
distribute data.
GCP Documentation:
[What is Pub/Sub?. Dataflow documentation | Cloud Dataflow | Google Cloud](https://cloud.google.com/pubsub/docs/overview)

## Question 19

You are setting up multiple MySQL databases on Compute Engine. You need to collect logs from your MySQL applications for
audit purposes. How should you approach this?

1. [x] Install the Stackdriver Logging agent on your database instances and configure the fluentd plugin to read and
   export your MySQL logs into Stackdriver Logging.
2. [ ] Install the Stackdriver Monitoring agent on your instances, configure the MySQL plugin, and export logs to
   Stackdriver Monitoring.
3. [ ] Configure Cloud Composer to monitor and report on instance performance metrics.
4. [ ] Configure Stackdriver Logging to natively monitor application logs, which will appear in Stackdriver Logging.

Cloud Composer is used for managing workflows, not logging. The Stackdriver Logging agent requires the fluentd plugin to
be configured to read logs from your database application. Stackdriver Monitoring is useful for measuring performance
metrics and alerts, but not for
logs. [About the Logging agent | Cloud Logging | Google Cloud](https://cloud.google.com/logging/docs/agent)

## Question 20

You have a long-running, streaming Dataflow pipeline that you need to shut down. You do not need to preserve data
currently in the processing pipeline and need it shut down as soon as possible. Which shutdown option should you use to
complete the shutdown process?

1. [ ] Stop
2. [ ] Drain
3. [x] Cancel
4. [ ] Graceful shutdown

Graceful Shutdown is not a valid option. Cancel will shut down the pipeline without allowing buffered jobs to complete.
Stop is not a valid option. Drain will stop new data from flowing in but will leave the processing pipeline running to
process buffered data, which is not what we want. [Deploying a pipeline | Cloud Dataflow | Google Cloud Dataflow
documentation | Cloud Dataflow | Google Cloud
](https://cloud.google.com/dataflow/docs/guides/deploying-a-pipeline)

## Question 21

You are running Spark jobs on Cloud Dataproc clusters using HDFS storage. You have enabled auto-scaling to deal with the
varying demands of the jobs, but some jobs are failing. What can you change to remedy this?

1. [x] Use Cloud Storage instead of HDFS.
2. [ ] Add high availability to the cluster to ensure there is sufficient processing power for all Spark jobs.
3. [ ] Turn off autoscaling and size the cluster for the most demanding Spark job.
4. [ ] Turn off autoscaling and size the cluster for the least demanding Spark job.

Autoscaling and HDFS are not a good combination in Cloud Dataproc, as when a cluster scales down some data stored in
HDFS may be lost, unless the minimum required storage space can be provided by the minimum number of nodes in the
cluster. In this scenario it is far easier to use the GCS connector for storage.
[Cloud Storage connector | Dataproc Documentation | Google Cloud Autoscaling clusters | Dataproc Documentation | Google Cloud](https://cloud.google.com/dataproc/docs/concepts/configuring-clusters/autoscaling)

## Question 22

You want to make changes to a Cloud Dataflow pipeline that is currently in production, which reads data from Cloud
Storage and writes the output back to Cloud Storage. What is the easiest and safest way to test changes while in
development?

1. [ ] Use a separate Cloud Dataflow configuration, and a staging storage bucket
2. [ ] Use a separate GCP project for development
3. [x] Use a DirectRunner to test-run the pipeline using local compute power, and a staging storage bucket
4. [ ] Update the Cloud Dataflow configuration in production to test changes, but make backups of all data that would
   normally be processed by the pipeline in case you need to run it again

Using a DirectRunner configuration with a staging storage bucket is the quickest and easiest way of testing a new
pipeline, without risking changes to a pipeline that is currently in
production. [Direct Runner](https://beam.apache.org/documentation/runners/direct/)

## Question 23

The field devices department in your organization would like to collect metrics from multiple groups of IoT devices to
be stored in a time-series database as a series of individual events. Each event key should be identifiable by its
timestamp and serial number. What would be the optimal design for a row key in Bigtable?

1. [ ] timestamp#serialnumber#devicegroup
2. [ ] serialnumber#devicegroup#timestamp
3. [ ] timestamp#devicegroup#serialnumber
4. [x] devicegroup#serialnumber#timestamp

A good Bigtable row key design should use field promotion to group together contiguous rows - especially in the case of
time-series data - while also providing as close to uniform distribution across the table as possible. The use of 3
fields in the key will also allow for fast indexed searches. [Schema Design for Time Series Data | Cloud Bigtable
Documentation](https://cloud.google.com/bigtable/docs/schema-design-time-series#patterns_for_row_key_design)

## Question 24

You are monitoring a streaming data pipeline that ingests streaming data into Cloud Pub/Sub, processed by Cloud
Dataflow, and inserted into a BigQuery table. Your Pub/Sub topic has a substantially higher than acceptable number of
undelivered messages. Why might this be happening?

1. [ ] Your Audit Logs do not have sufficient access to your Pub/Sub topic, causing delays in delivering.
2. [x] The subscriber is not acknowledging messages as they are pulled.
3. [x] Your Dataflow subscriber is unable to keep up with the rate of incoming messages.
4. [ ] Your Publishers' message throughput is too low.

Publisher throughput being low would have the opposite effect of a Pub/Sub backlog. If your subscriber is not
acknowledging pulled messages, Pub/Sub will not know to drop them from the queue. Your subscriber may be
under-provisioned to keep up with the compute needs necessary to keep the Pub/Sub backlog empty. [Cloud Pub/Sub
Documentation | Google Cloud](https://cloud.google.com/pubsub/docs)

## Question 25

Your company stores data in BigQuery for long-term and short-term analytics queries. Most of the jobs only need to study
the last 7 days of data. Over time, the cost of queries keeps going up. How can you redesign the database to lower the
cost of the most frequent queries?

1. [x] Use DATE partitioned tables.
2. [ ] Use Integer range partitioned tables.
3. [ ] Create a new table every 7 days. Use JOIN statements to conduct long-term analytics queries.
4. [ ] Create a new table every 7 days. Maintain a separate table that duplicates the weekly tables to contain all data.

Using DATE partitioned tables means that you are able to limit the total data being queried, which will reduce query
costs. Creating new tables is not necessary.
[Introduction to partitioned tables | BigQuery | Google Cloud](https://cloud.google.com/bigquery/docs/partitioned-tables#date_timestamp_partitioned_tables)

## Question 26

You want to update a Cloud Dataflow pipeline to use the same PTransform on 2 PCollections, which are both of the same
type of CSV row data. What is the best way to achieve this?

1. [x] Use a Flatten transform on the PCollections to merge them prior to the PTransform
2. [ ] Use a Join transform on the PCollections to merge them prior to the PTransform
3. [ ] Run the PTransform on each PCollection individually, but then run the write transform to the same location for
   both PCollections
4. [ ] Run the PTransform on each PCollection individually, then use a Join transform before a write transform

The Flatten transformation merges multiple PCollection objects into a single logical PCollection, whereas Join
transforms like CoGroupByKey attempt to merge data where there are related keys in the two datasets. [Beam Programming
Guide](https://beam.apache.org/documentation/programming-guide/#core-beam-transforms)

## Question 27

Your BigQuery dataset contains 1500 tables. When conducting a query, you are limited to a maximum of 1000 tables that
you can query at once. You need to query data across all 1500 tables. What should you do?

1. [x] If possible, merge the 1500 tables to bring the total number below 1000. You may still partition single tables to
   divide data for queries.
2. [ ] Place tables into separate datasets.
3. [ ] Create multiple views of chunks of the 1500 tables, then query the multiple views.
4. [ ] Export the data to Bigtable, and conduct your query inside of Bigtable.

If you have over 1000 tables, you need to bring that number to below 1000 to query all of them at once. Merge tables,
then use table partitioning to divide single tables into segments (called partitions), as long they are partitioned by
time. [BigQuery documentation | Google Cloud](https://cloud.google.com/bigquery/docs)

## Question 28

You are working in the updated BigQuery interface. While conducting BigQuery queries against a large table with many
columns, in the job Execution Details section, you notice you have an excessively high read time in the first stage of
your query execution. How can you troubleshoot this to increase performance and reduce costs?

1. [ ] Reduce the number of read operations by adding a LIMIT clause to your query.
2. [x] Partition or separate your large table into smaller pieces. Conduct a query against your smaller (or partitioned)
   tables to reduce read times.
3. [ ] Reduce the number of write operations by optimizing the complexity of your query functions.
4. [x] Restrict the number of columns in your SELECT field for those needed. This will reduce read times on your query.

Restricting queries to specific columns or partitions will reduce the total data read, and the total read time. LIMIT
clauses do not impact how much data is read, only how much is viewed.
[BigQuery documentation | Google Cloud](https://cloud.google.com/bigquery/docs)

## Question 29

You want to display aggregate view counts for your YouTube channel data in Data Studio. You want to see the video titles
and view counts summarized over the last 30 days. You also want to divide the data by the Country Code using the fewest
possible steps. What should you do?

Export your YouTube views to Cloud Storage. Set up a Cloud Storage data source for Data Studio. Set Views as the metric
and set Video Title and Country Code as report dimensions.
Set up a YouTube data source for your channel data for Data Studio. Set Views as the metric and set Video Title as a
report dimension. Set Country Code as a filter.
Export your YouTube views to Cloud Storage. Set up a Cloud Storage data source for Data Studio. Set Views as the metric
and set Video Title as a report dimension. Set Country Code as a filter.
Set up a YouTube data source for your channel data for Data Studio. Set Views as the metric and set Video Title and
Country Code as report dimensions.

Using Views as the metric and setting Video Title and Country Code as the report dimensions is the better option.
Country Code is a dimension because it's a string and should be displayed as such, that is, showing all countries,
instead of filtering.
[Reference: Getting Started Using Data Studio | BI Engine | Google Cloud](https://cloud.google.com/bi-engine/docs/getting-started-data-studio)

## Question 30

The analysts in your data team need to run a BigQuery job that will use JOINs. What advice can you give them on
designing this query to follow best practices?

1. [ ] Use LIMIT to reduce the number of rows being processed by the JOIN.
2. [ ] Order tables appropriately in the query, with the smaller table on the left side of the JOIN and the larger table
   of the right side of the JOIN.
3. [x] Order tables appropriately in the query, with the larger table on the left side of the JOIN and the smaller table
   of the right side of the JOIN.
4. [ ] Ensure the data analysts do not use FULL JOINs.

When you create a query by using a JOIN, consider the order in which you are merging the data. The standard SQL query
optimizer can determine which table should be on which side of the join, but it is still recommended to order your
joined tables appropriately. The best practice is to place the largest table first, followed by the smallest, and then
by decreasing size.
[Optimizing query computation | BigQuery | Google Cloud](https://cloud.google.com/bigquery/docs/best-practices-performance-compute#optimize_your_join_patterns)

## Question 31

Which of these is NOT a type of trigger that applies to Dataflow?

1. [ ] Element count
2. [ ] Combinations of other triggers
3. [x] Element size in bytes
4. [ ] Timestamp

Element size is not a type of trigger; therefore, it is the correct answer. Dataflow is basically an Apache Beam-managed
service. The triggers that apply to Dataflow are: event time triggers, processing time triggers, data-driven triggers,
composite triggers, Pub/Sub topics, and Cloud Functions.
[Dataflow Documentation](https://cloud.google.com/dataflow/docs/concepts/streaming-pipelines#triggers)

## Question 32

You want to train your machine learning model on AI Platform while saving costs. Which scaling tier would you choose?

1. [ ] PREMIUM_1
2. [ ] CUSTOM
3. [x] BASIC
4. [ ] STANDARD_1

BASIC tier uses a single instance and is the lowest cost. CUSTOM can use different configurations, but BASIC is still
cheaper with a single instance. STANDARD_1 and PREMIUM_1 all use multiple worker and parameter servers are more
expensive. [AI Platform documentation | Google Cloud](https://cloud.google.com/ai-platform/docs)

## Question 33

You wish to build an AutoML Natural Language model for classifying some documents with user-defined labels. How can you
ensure you are providing quality training data for the model?

1. [ ] Ensure you provide at minimum 100 training documents per label, but ideally 10 times more documents for the most
   common label than for the least common label.
2. [x] Ensure you provide at minimum 10 training documents per label, but ideally 100 times more documents for the most
   common label than for the least common label.
3. [ ] Aim to provide over 1,000,000 documents in total.
4. [ ] Minimize the diversity of documents in the training data. Ensure documents are by the same author and of the same
   length wherever possible.

To achieve the best results when preparing training data for AutoML Natural Language classification models, the minimum
number of documents per label is 10, and ideally you should have at least 100 times more documents for the most common
label than for the least common label.
[Preparing your training data | AutoML Natural Language | Google Cloud](https://cloud.google.com/natural-language/automl/docs/prepare#classification)

## Question 34

You are training a facial detection machine learning model. Your model is suffering from overfitting your training data.
What steps can you take to solve this problem?

1. [ ] Use a larger set of features
2. [x] Use a smaller set of features
3. [ ] Reduce the number of training examples
4. [x] Increase the number of training examples

Reducing the number of unneeded features can help reduce overfitting. More data is one of the best methods to increase
the variety of samples and better generalize your model.
[Machine learning workflow | AI Platform | Google Cloud](https://cloud.google.com/ai-platform/docs/ml-solutions-overview)

## Question 35

You are developing an application that will only recognize and tag specific business to business product logos in
images. You do not have an extensive background working with machine learning models, but need to get your application
working. What is the current best method to accomplish this task?

1. [x] Use the AutoML Vision service to train a custom model using the Vision API
2. [ ] Create a custom machine learning model to recognize specific logos in photos, then train it on AI Platform.
3. [ ] Use the Cloud Vision API to recognize all logos in images, then use the Cloud Natural Language API to recognize
   specific logos by name.
4. [ ] Use the Cloud Vision API to recognize logos in the images.

Cloud Vision API can recognize common logos, but would struggle to find specific business logos on its own. The best
option is AutoML, which allows you to take the pre-trained Vision API and apply it to custom images. Creating a custom
ML model from scratch would be time-consuming and is not necessary when you can build on existing models. [Cloud Auto ML
Vision](https://cloud.google.com/vision/automl/docs)

## Question 36

You have in your possession a database of financial transactions, which include a user's name, location, purchase
location, and purchase amount. Each transaction is also labeled whether or not the transaction was fraudulent. With this
data, what two types of machine learning can potentially applied to this dataset?

1. [ ] Apply unsupervised learning to label which transactions are likely to be fraudulent.
2. [ ] Apply reinforcement learning to predict the location of purchase.
3. [x] Using the applied fraudulent/non-fraudulent labels, apply supervised classification learning to predict which
   future transactions are likely to be fraudulent
4. [x] Unsupervised learning to identify patterns (clustering) in the data to predict the location of future purchases.

Reinforcement learning uses reward systems to complete a task. Predicting the location would be an example of using
unsupervised learning to find patterns. Unsupervised learning does not use labels but does look for patterns (or
clustering) of data in order to make predictions based on the patterns it learns. Supervised learning takes labeled
training data to predict future results on new test data. Classification models apply categorized variables (i.e. "
fraudulent", "not fraudulent").
[Machine learning workflow | AI Platform | Google Cloud](https://cloud.google.com/ai-platform/docs/ml-solutions-overview)

## Question 37

You are creating a machine learning model for predicting a person's income given a variety of factors such as age,
occupation, and others. What type of problem are we trying to solve in our prediction values?

1. [ ] Classification
2. [ ] Clustering
3. [x] Regression
4. [ ] Unsupervised learning

Regression problems are problems where we are trying to predict a numerical value, in this case, a person's income.

## Question 38

Your organization needs to develop their machine learning model to control topology definitions. There are a large
number of possible configurations to achieve the best results. What components of their machine learning model would
they adjust to account for increased complexity?

1. [x] Hidden layers
2. [x] Neurons
3. [ ] Learning rate
4. [ ] Epoch

Learning rate is a hyperparameter, not related to adjusting to training data. An Epoch is a pass through the training
dataset, not related to complexity. Adding additional neurons allows combining more input values, and hidden layers
allow for passing outputs to another layer of neurons for more complex calculations. [Machine learning workflow | AI
Platform | Google Cloud](https://cloud.google.com/ai-platform/docs/ml-solutions-overview)

## Question 39

Your model is performing very well on training data, but very poorly on new or unknown data. What could be the problem?

1. [ ] There is not enough data in the test set - the model has an implicit bias.
2. [ ] There is not enough data in the validation set - the loss function cannot be minimized.
3. [ ] There are insufficient infrastructure resources assigned to the model.
4. [x] There is not enough data in the training set - the model has been overfitted.

The model has been too well trained on the training data and will fit it too closely, so it will perform badly when
exposed to real-world data for predictions. Increasing the amount of data can help to reduce this overfitting. The loss
function, biases and infrastructure resources are not directly relevant to an overfitting problem.
[Generalization: Peril of Overfitting | Machine Learning Crash Course](https://developers.google.com/machine-learning/crash-course/generalization/peril-of-overfitting)

## Question 40

You have decided to train your machine learning model locally before training on cloud resources, why do you want to do
this?

1. [x] Save costs.
2. [ ] Faster training with scaling resources.
3. [ ] Restrict access to other parties.
4. [x] Faster testing for the best hyperparameters for the model

Cloud-based resources are better for scaled training. Local training allows you to make faster tests of the right
hyperparameters for the model as you can make quicker adjustments on the fly. Training locally does not cost money on
the cloud when running.
[Machine learning workflow | AI Platform | Google Cloud](https://cloud.google.com/ai-platform/docs/ml-solutions-overview)

## Question 41

You are creating a machine learning model to predict the likelihood of fraud from credit card transaction data. The end
result will be predicting the percent confidence of two results: "Fraud" and "Not Fraud". What type of learning model
problem is this?

1. [ ] Hyperparameter
2. [x] Classification
3. [ ] Regression
4. [ ] Clustering

Categorical is for a set of finite categories, such as 'yes' or 'no' - fraud is a yes/no output, so this fits.
[Machine learning workflow.](https://cloud.google.com/ai-platform/docs/ml-solutions-overview)

## Question 42

What will happen to your data in a Bigtable instance if a node goes down?

1. [ ] Lost data will automatically rebuild itself from Cloud Storage backups when the node comes back online.
2. [ ] Data will be lost, which makes regular backups to Cloud Storage necessary.
3. [ ] Bigtable will attempt to rebuild the data from RAID disk configuration when the node comes back online.
4. [x] Nothing, as the storage is separated from the node compute.

Rebuilding from RAID is not a valid Bigtable function. Storage and compute are separate, so a node going down may affect
performance, but not data integrity; nodes only store pointers to storage as metadata. [Overview of Cloud Bigtable |
Cloud Bigtable Documentation](https://cloud.google.com/bigtable/docs/overview)

## Question 43

The data team in your organization has created a Cloud Dataflow job that processes CSV files from Cloud Storage using a
user-managed controller service account. The job creates a worker, but then fails. What could be the problem?

1. [ ] The Cloud Dataflow job has been under-provisioned with too few workers.
2. [x] The user-managed service account does not have the necessary storage IAM role for the Cloud Storage bucket.
3. [ ] The user-managed service account does not have the Project Editor role.
4. [ ] Cloud Dataflow is the wrong tool for the job. Refactor the pipeline using Apache Kafka in Kubernetes Engine.

If you are using user-managed controller service accounts for Cloud Dataflow, you need to make sure that those service
accounts have all the necessary roles and permissions, including access to Cloud Storage in this scenario. With that in
mind you should use the principle of least privilege, and not grant broad roles such as Project Editor.
[This problem is not a provisioning issue. Cloud Dataflow security and permissions | Google Cloud](https://cloud.google.com/dataflow/docs/concepts/security-and-permissions#security_and_permissions_for_pipelines_on_google_cloud_platform)

## Question 44

Your business continuity planner wants to minimize disruption to the business that might be caused by the availability
of Cloud SQL. How can you facilitate this?

1. [ ] Enable Auto Backups, do not specify a maintenance window, and use an HA configuration to ensure a failover event
   occurs when there is automated maintenance.
2. [ ] Enable Auto Backups, but do not specify a maintenance window as GCP will auto-detect the best time for disruptive
   updates.
3. [ ] Enable Auto Backups, specify a maintenance window, and use an HA configuration to ensure a failover event occurs
   when there is automated maintenance.
4. [x] Enable Auto Backups, and specify a maintenance window that does not conflict with core business hours.

Backups are essential for business continuity, but in this scenario the options presented for high availability won't
actually improve continuity when scheduled maintenance occurs, as scheduled maintenance is not considered a failover
event by GCP. Therefore, specifying an agreeable maintenance window is more important. [Overview of maintenance on Cloud
SQL instances | Cloud SQL for MySQL](https://cloud.google.com/sql/docs/mysql/maintenance)

## Question 45

You regularly use prefetch caching with a Data Studio report to visualize the results of BigQuery queries. You want to
minimize service costs. What should you do?

1. [ ] Set up the report to use the Viewer's credentials to access the underlying data in BigQuery, and also set it up
   to be a view-only report.
2. [ ] Set up the report to use the Viewer's credentials to access the underlying data in BigQuery, and verify that the
   Enable cache checkbox is not selected for the report.
3. [x] Set up the report to use the Owner's credentials to access the underlying data in BigQuery, and verify that the
   Enable cache checkbox is selected for the report.
4. [ ] Set up the report to use the Owner's credentials to access the underlying data in BigQuery, and direct the users
   to view the report only once per business day (24-hour period).

You must set Owner credentials to use the enable cache option in BigQuery. It is also a Google best practice to use the
enable cache option when the business scenario calls for using prefetch caching.Cache auto-expires after 12 hours.
24-hour cache is not a valid option. Prefetch cache is only for data sources that use the Owner's credentials (not the
Viewer's credentials).
[Visualizing BigQuery data using Data Studio | Google Cloud](https://cloud.google.com/bigquery/docs/visualize-data-studio)

## Question 46

You have data stored in a Cloud Storage bucket and also in a BigQuery dataset. You need to secure the data and provide 3
different types of access levels for your Google Cloud Platform users: administrator, read/write, and read-only. You
want to follow Google-recommended practices. What should you do?

1. [x] Use the appropriate pre-defined IAM roles for each of the access levels needed for Cloud Storage and BigQuery.
   Add your users to those roles for each of the services.
2. [ ] Create 3 custom IAM roles with appropriate policies for the access levels needed for Cloud Storage and BigQuery.
   Add your users to the appropriate roles.
3. [ ] At the Organization level, add your administrator user accounts to the Owner role, add your read/write user
   accounts to the Editor role, and add your read-only user accounts to the Viewer role.
4. [ ] At the Project level, add your administrator user accounts to the Owner role, add your read/write user accounts
   to the Editor role, and add your read-only user accounts to the Viewer role.

Organization level roles are way too broad for this scenario. It is best practice to use pre-created roles over custom
roles with associated policies when they match your requirements, which they do in this scenario, and the principle of
least privilege favors using pre-defined roles for granular access.
[BigQuery documentation | Google Cloud](https://cloud.google.com/bigquery/docs)

## Question 47

What types of Bigtable row keys can lead to hot-spotting?

1. [x] Leading with a non-reversed timestamp.
2. [ ] Reverse timestamps.
3. [x] Standard domain names (non-reversed).
4. [ ] Non-sequential numeric IDs.

Like sequential IDs, timestamps will read and write from the same node, causing increased load. Non-reversed domain
names at the start of a row key can lead to hot-spotting. If you need to use domain names, reverse it. Reverse
timestamps will spread the load for reads and writes between nodes, making this an incorrect answer for this question.
Randomized IDs will spread the load for reads and writes between nodes, making this an incorrect answer for this
question.
[Overview of Cloud Bigtable | Cloud Bigtable Documentation](https://practice-exam.acloud.guru/gcp-certified-professional-data-engineer/result/69396268-7a35-4ab5-a081-b6925c425dca#:~:text=for%20this%20question.-,Overview%20of%20Cloud%20Bigtable%20%7C%20Cloud%20Bigtable%20Documentation,-Non%2Dsequential%20numeric)

## Question 48

Your organization has a security policy which mandates that the security department must own and manage encryption keys
for data stored in Cloud Storage buckets. Analysts and developers need to store data that is encrypted with these keys
without access to the keys themselves. How can this be achieved?

1. [x] Use Cloud KMS for the security team to manage their own encryption keys in a dedicated project. Grant the Cloud
   KMS CryptoKey Encrypter/Decrypter role for the keys to the Cloud Storage service accounts in the other projects.
2. [ ] Create a process where the security team encrypts data stored in a bucket once it has been written by an analyst
   or developer.
3. [ ] Create a staging bucket for analysts and developers to store data. Create a process where the security team can
   move data from the staging bucket to a secure bucket managed by their own keys.
4. [ ] Create a process where the security team can be requested to encrypt or decrypt data in a storage bucket by an
   analyst or developer.

Cloud KMS allows you to create and manage your own encryption keys which can then be used by service accounts in other
projects. Developers in those projects can then access services without any access to the underlying keys. A staging
area is not required, neither is any other manual intervention by the security team. [Using customer-managed encryption
keys | Cloud Storage | Google Cloud](https://cloud.google.com/storage/docs/encryption/using-customer-managed-keys)

## Question 49

Which of these is NOT a valid reason to choose an HDD storage type over SSD in a Bigtable instance?

1. [x] You need to integrate Bigtable with Cloud Storage.
2. [ ] You plan on running batch workloads instead of frequently executing random reads across a small number of rows.
3. [x] HDDs always make Bigtable workloads cheaper.
4. [ ] You need to store over 10 TB of data.

Bigtable can integrate with Cloud Storage regardless of the type of disk in use by the instance. The other reasons are
valid for choosing HDD as an outlying case, but in general, SSD disks are preferred, as HDD disks will cause a
significant drop in performance.
[Reference: Overview of Cloud Bigtable | Cloud Bigtable Documentation](https://cloud.google.com/bigtable/docs/overview)

HDDs often don't help lower Bigtable costs due to the need for more nodes to keep up with demand.

## Question 50

Your organization has just recently started using Google Cloud. Everyone in the company has access to all datasets in
BigQuery, using it as they see fit without documenting their use cases. You need to implement a formal security policy,
but need to first determine what everyone has been doing in BigQuery. What is your first step to do so?

1. [x] Use Stackdriver Logging to review data access.
2. [ ] Inspect the IAM policy of each table.
3. [ ] Export billing into Cloud Storage, and view BigQuery related records to determine user activity.
4. [ ] View the usage of BigQuery query slots in Stackdriver Monitoring.

Stackdriver Logging will record the audit logs of jobs and queries of each individual user's actions. [Reference: Google
Cloud BigQuery Documentation](https://cloud.google.com/bigquery/docs)





