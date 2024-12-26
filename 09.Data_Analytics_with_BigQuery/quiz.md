### Question 1

How can you ensure that table modifications in BigQuery are ACID compliant?

1. [ ] Maintain a separate table that records transactions themselves so changes can be re-applied if any are lost.
2. [ ] Enforce ordering of SQL statements to ensure the operation completes atomically.
3. [x] No special accommodations are required, BigQuery table modifications are ACID compliant by design.
4. [ ] Add a nominal wait time to any application queries following an update to allow for eventual consistency.

<details>
  <summary>NOTE</summary>

```
All table modifications in BigQuery are ACID compliant.
This applies to DML operations, queries with destination tables, and load jobs.
A table that goes through inserts, updates, and deletes while serving user queries handles the concurrency
gracefully and transitions from one state to the next in an atomic fashion.
```

</details>

### Question 2

What is a federated data source?

1. [ ] A BigQuery data set that belongs to a different GCP project, used in an SQL statement.
2. [ ] A BigQuery table that belongs to a different data set, used in an SQL statement.
3. [x] An external data source that can be queried directly even though the data is not stored in BigQuery.
4. [ ] A public BigQuery data set.

<details>
  <summary>NOTE</summary>

```
An external data source (also known as a federated data source) is a data source that you can query directly even
though the data is not stored in BigQuery. Instead of loading or streaming the data,
you create a table that references the external data source.
```

</details>

### Question 3

What could you consider to improve BigQuery performance for queries that use filters or aggregation against particular
columns?

1. [ ] Normalize data based on commonly used filters.
2. [ ] Use partitioned tables
3. [x] Use clustered partitioned tables
4. [ ] Use clustering on non-partitioned tables.

<details>
  <summary>NOTE</summary>

```
Clustering can improve the performance of certain types of queries such as queries that use filter clauses and queries 
that aggregate data. 
When you submit a query that contains a clause that filters data based on the clustering columns, 
BigQuery uses the sorted blocks to eliminate scans of unnecessary data.
```

</details>

### Question 4

Your company stores data in BigQuery for long-term and short-term analytics queries. Most of the jobs only need to study
the last 7 days of data. Over time, the cost of queries keeps going up. How can you redesign the database to lower the
cost of the most frequent queries?

1. [ ] Create a new table every 7 days. Maintain a separate table that duplicates the weekly tables to contain all data.
2. [ ] Use Integer range partitioned tables.
3. [x] Use DATE partitioned tables.
4. [ ] Create a new table every 7 days. Use JOIN statements to conduct long-term analytics queries.

<details>
  <summary>NOTE</summary>

```
A partitioned table is a special table that is divided into segments, called partitions, 
that make it easier to manage and query your data.
By dividing a large table into smaller partitions, you can improve query performance, and you can control costs by 
reducing the number of bytes read by a query.
```

</details>

### Question 5

You are required to load a large volume of data into BigQuery that does contain some duplication. What should you do to
ensure the best query performance once the data is loaded?

1. [x] Denormalize the data by using nested or repeated fields.
2. [ ] Normalize the data to eliminate duplicates from being stored, and reformat the data as JSON.
3. [ ] Break up the data into multiple CSV files.
4. [ ] Normalize the data to eliminate duplicates from being stored, and reformat the data as Avro.

<details>
  <summary>NOTE</summary>

```
BigQuery performs best when your data is denormalized.
Rather than preserving a relational schema, such as a star or snowflake schema, you can improve performance by denormalizing 
your data and taking advantage of nested and repeated fields.
```

</details>

### Question 6

What steps do you need to take to set up BigQuery before use?

1. [ ] You must create processing nodes in Compute Engine.
2. [ ] You must create storage buckets for BigQuery to use.
3. [ ] You must create a BigQuery cluster.
4. [x] BigQuery is a serverless product and all compute and storage resources are managed for you.

<details>
  <summary>NOTE</summary>

```
BigQuery is a serverless product for storing and querying massive data sets without configuring or managing hardware or software.
```

</details>

### Question 7

Which option shown below is true regarding BigQuery jobs?

1. [ ] Jobs run for all scheduled actions, but not for interactive queries in the BigQuery UI.
2. [ ] Jobs run for most actions, including those in the BigQuery UI, but only if they are submitted with DML.
3. [x] Jobs are actions that BigQuery runs to load, export, query, or copy data.
4. [ ] Jobs run for large batch operations but not for interactive queries in the BigQuery UI.

<details>
  <summary>NOTE</summary>

```
When you use the Cloud Console, the classic BigQuery web UI, or the CLI to load, export, query, or copy data, 
a job resource is automatically created, scheduled, and run.
```

</details>

### Question 8

You are required to share a subset of data from a BigQuery data set with a 3rd party analytics team. The data may change
over time, and you should not grant unnecessary projects permissions to this team if you can avoid it. How should you
proceed?

1. [ ] Add the team to your GCP project and assign them the BigQuery Data Editor IAM role for the data set.
2. [ ] Create an export of the data subset to a Cloud Storage bucket. Provide a signed URL for the team to download the data from the bucket.
3. [x] Create an authorized view based on a specific query for the subset of data, and provide access for the team only to that view.
4. [ ] Add the team to your GCP project and assign them the BigQuery Data Viewer IAM role for the data set.

<details>
  <summary>NOTE</summary>

```
An authorized view allows you to share query results with particular users and groups without giving them access to the underlying tables.
```

</details>

### Question 9

When you run a query in BigQuery, what happens to the results?

1. [ ] Query results are stored in a results table, however it can not be used for querying cached results.
2. [ ] Query results exist only in BigQuery memory and are not stored in a table.
3. [ ] Query results exist only within the BigQuery UI and are not stored in a table.
4. [x] Query results are either written to a destination table specified by the user, or to a temporary cached results table.

<details>
  <summary>NOTE</summary>

```
BigQuery writes all query results to a table.
The table is either explicitly identified by the user (a destination table), or it is a temporary, cached results table.
```

</details>

### Question 10
What are some ways to help control costs in BigQuery?


1. [ ] There are no ways to control the cost of BigQuery.
2. [x] Use the query validator in the Cloud Console.
3. [x] Only query specific columns, avoiding SELECT *.
4. [ ] Split data across multiple projects to benefit from multiple free tier allowances.
5. [ ] Use LIMIT clauses in SQL queries.

<details>
  <summary>NOTE</summary>

```
Using the query validator and only querying the data you need will help you to predict and control costs. Control costs in BigQuery

Querying only the data you need and using the query validator will help you to predict and control costs. Control costs in BigQuery
```

</details>





