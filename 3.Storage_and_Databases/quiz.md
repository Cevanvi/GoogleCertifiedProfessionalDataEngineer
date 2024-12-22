### Question 1

A customer has 90TB of archive data to move to Google Cloud Storage, but has restrictions on connecting their private
network to the public Internet. How could you facilitate this?

1. [ ] Create bastion hosts that connect to the private network and Google Cloud, and start a single upload to GCS using
   gsutil
2. [ ] Create bastion hosts that connect to the private network and Google Cloud, and start multiple uploads to GCS
   using
   gsutil
3. [ ] Create Cloud VPN links between a GCP project and the customer's private network to facilitate the upload via
   gsutil
4. [x] Use the 100TB Transfer Appliance

### Question 2

Your application requires access to a Cloud Storage bucket. What is the best way to achieve this?

1. [x] Create a custom service account with only the required permissions for the application
2. [ ] Make the bucket open to the public so no authentication is required
3. [ ] Include a user's Google credentials in the application code so it can authenticate with Cloud Storage
4. [ ] Make the application prompt a user for their Google credentials to authenticate with Cloud Storage

### Question 3

What storage class would be the most cost effective for data that is accessed only once per month?

1. [ ] Regional
2. [ ] Low Availability
3. [x] Nearline
4. [ ] Coldline

### Question 4

Cloud Storage bucket names must be unique within:

1. [ ] A zone
2. [ ] A region
3. [ ] A project
4. [x] All GCP projects

### Question 5

A customer needs a JSON document store NoSQL database to help them develop a new application. Which GCP product should
they choose?

1. [ ] Cloud Memorystore
2. [x] Cloud Firestore
3. [ ] Cloud SQL
4. [ ] Cloud Bigtable

### Question 6

Cloud Memorystore is essentially a managed service based on which open-source project?

1. [ ] Memcached
2. [ ] Apache Kafka
3. [ ] MongoDB
4. [x] Redis

### Question 7

High Availability for Cloud SQL PostgreSQL instances works because:

1. [ ] Instances replicate data directly between themselves for automatic failover
2. [ ] Cloud SQL for PostgreSQL does not support high availability
3. [x] Instances share a regional replicated persistent disk
4. [ ] Google SREs are on call and can quickly bring up a new instance in the event of a failure

### Question 8

What is the best way to grant someone temporary access to a file if they do not have a Google account?

1. [ ] Make the file publicly accessible but ask the user not to share the link
2. [x] Use a signed URL with a specific expiry
3. [ ] Ask the user to create a Google account
4. [ ] Use a long and complex name for the bucket and object

### Question 9

A customer has a 400 GB MySQL database running in a data center. Which product would you choose for migrating this
database to GCP?

1. [ ] Compute Engine managed instance group of MySQL VMs
2. [x] Cloud SQL for MySQL, Second Generation
3. [ ] Cloud Spanner
4. [ ] Cloud SQL for PostgreSQL
5. [ ] Cloud Firestore

### Question 10

If Cloud Spanner has to break one of the 3 features of the CAP Theorem, which one will it be?

1. [ ] Persistence
2. [ ] Consistency
3. [ ] Cloud Spanner never breaks any of these features
4. [x] Availability
