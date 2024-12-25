### Question 1

What is a sensible way to test a Cloud Dataflow pipeline before deploying it to production?

1. [x] Remove DataflowRunner from PipelineOptions, to allow the pipeline to run locally.
2. [ ] Tune PipelineOptions to use the smallest amount of compute resources possible.
3. [ ] Stop the Dataflow job half way through to minimize costs.

<details>
  <summary>NOTE</summary>

```
Instead of running your pipeline on managed cloud resources, you can choose to execute your pipeline locally. 
Local execution has certain advantages for testing, debugging, or running your pipeline over small data sets.
```

</details>

### Question 2

What method could you use to help compute running averages when dealing with unbounded/streaming data?

1. [ ] Fixed-time windows
2. [ ] Change the input data to be batched/bounded to make it easier to compute averages
3. [ ] Session windows
4. [x] Sliding windows

<details>
  <summary>NOTE</summary>

```
A sliding time window represents time intervals in the data stream; however, sliding time windows can overlap. 
This kind of windowing is useful for taking running averages of data. 
For example, using sliding time windows you could compute a running average of the past 60 seconds’ worth of data, updated every 30 seconds. 
```

</details>

### Question 3

What is the compute model of Cloud Dataflow?

1. [x] Dataflow fully manages Compute Engine services to run jobs.
2. [ ] Dataflow manages Cloud Storage but requires a pre-built Compute Engine cluster to run jobs.
3. [ ] Dataflow does not manage any resources, they must be pre-built manually before running jobs.
4. [ ] Dataflow manages Cloud Storage but requires a pre-built Kubernetes Engine cluster to run jobs.
5. [ ] Dataflow requires a pre-built Cloud Dataproc cluster to run jobs.

<details>
  <summary>NOTE</summary>

```
The Dataflow service fully manages Google Cloud services such as Compute Engine to run your Dataflow job, 
automatically spinning up and tearing down the necessary resources.
```

</details>

### Question 4

What is the name given to a dataset that can be acted upon within a Cloud Dataflow pipeline?

1. [ ] Database
2. [ ] Aggregation
3. [ ] ParDo
4. [ ] Bucket
5. [x] PCollection

<details>
  <summary>NOTE</summary>

```
A PCollection represents a potentially distributed, multi-element dataset that acts as the pipeline's data. 
Apache Beam transforms use PCollection objects as inputs and outputs for each step in your pipeline.
```

</details>

### Question 5

Which big data programming model is implemented with Cloud Dataflow?

1. [x] Apache Beam
2. [ ] Apache Airflow
3. [ ] Apache Spark
4. [ ] Apache NiFi

<details>
  <summary>NOTE</summary>

```
Apache Beam is an open source, unified model for defining both batch and streaming data parallel-processing pipelines.
Cloud Dataflow is a distributed processing backend for Apache Beam.
```

</details>

### Question 6

What would be the most secure way to grant access from Dataflow in Project A to a Cloud Storage bucket in Project B?

1. [ ] Grant storage viewer access for the bucket in Project B to the default compute service account in Project A.
2. [x] Create a custom service account to use as the Dataflow controller service account in Project A. Grant storage
   viewer access for the bucket in Project B to the custom service account in Project A.
3. [ ] Copy data from the bucket in Project B to a new bucket in Project A.

<details>
  <summary>NOTE</summary>

```
By default, compute workers use your project’s Compute Engine service account as the controller service account. 
For more fine-grained access and control, you can use a custom service account from your job's project as the user-managed 
controller service account, then grant the necessary permissions to that service account from the other project.
```

</details>

### Question 7

What is the purpose of a trigger in Cloud Dataflow?

1. [ ] Triggers determine when to emit output data, but only apply to bounded/batch input data.
2. [ ] Triggers determine when to initiate the processing of a pipeline.
3. [ ] Triggers determine when to emit output data, but only apply to unbounded/streaming input data.
4. [x] Triggers determine when to emit output data, and behave differently for bounded and unbounded data.

<details>
  <summary>NOTE</summary>

```
Triggers determine when to emit aggregated results as data arrives. 
For bounded data, results are emitted after all of the input has been processed. 
For unbounded data, results are emitted when the watermark passes the end of the window,
indicating that the system believes all input data for that window has been processed.
```

</details>

### Question 8

Which transformation can be used to process collections of key/value pairs, in a similar fashion to the shuffle phase of
a map/shuffle/reduce-style algorithm?

1. [ ] Combine
2. [ ] Partition
3. [ ] CoGroupByKey
4. [X] GroupByKey

<details>
  <summary>NOTE</summary>

```
GroupByKey is a Beam transform for processing collections of key/value pairs.
It’s a parallel reduction operation, analogous to the Shuffle phase of a Map/Shuffle/Reduce-style algorithm.
CoGroupByKey performs a relational join of two or more key/value PCollections that have the same key type.
Combine simply combines elements, and Partition splits elements into smaller collections.
```

</details>

### Question 9

Which operation can be used to invoke a user-specified function of each element of an input PCollection?

1. [ ] Combine
2. [ ] CoGroupByKey
3. [x] ParDo
4. [ ] GroupByKey
5. [ ] User-defined functions (UDFs)

<details>
  <summary>NOTE</summary>

```
ParDo is a Beam transform for generic parallel processing. 
The ParDo processing paradigm is similar to the 'Map' phase of a Map/Shuffle/Reduce-style algorithm: 
a ParDo transform considers each element in the input PCollection, performs some processing function (your user code) 
on that element, and emits zero, one, or multiple elements to an output PCollection.
```

</details>

### Question 10

What is a pipeline in the context of Cloud Dataflow?

1. [ ] A pipeline represents the compute resources required to ingest the data prior to sending it to Cloud Dataflow.
2. [ ] A pipeline represents a collection of data being prepared for transformation.
3. [ ] A pipeline could be any of these.
4. [x] A pipeline represents the entire series of steps involved in ingesting data, transforming that data and writing
   output.

<details>
  <summary>NOTE</summary>

```
In Cloud Dataflow, a pipeline encapsulates the entire series of computations involved in reading input data, 
transforming that data, and writing output data.
```

</details>



