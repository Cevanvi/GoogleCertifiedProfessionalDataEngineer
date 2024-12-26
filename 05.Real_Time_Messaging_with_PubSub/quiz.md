### Question 1

You are about to deploy the new version of your application, but you are concerned that it may need to be rolled-back
and you want to preserve any Pub/Sub messages it may process in the meantime. What do you do?

1. [ ] Create an extra subscription to the Topic to store a back up of all messages.
2. [ ] Create a test Topic and roll out application changes against that Topic.
3. [x] Create a snapshot on the Subscription so that you can seek back to this point in time if you need to roll-back
   the application changes.
4. [ ] Deploy application changes to only a subset of users.

### Question 2

Using Cloud IAM, what is the most granular level for which you can configure access control for Pub/Sub?

1. [ ] Across individual topics, but not subscriptions
2. [ ] Across the entire organization
3. [ ] Across the entire project, including all topics and subscriptions
4. [x] Across individual topics and subscriptions

### Question 3

What is the minimum retention duration for a message in Pub/Sub?

1. [x] 10 minutes
2. [ ] 1 minute
3. [ ] 1 day
4. [ ] No minimum retention duration

### Question 4

What is the maximum total size permitted for a Publish request, including metadata and payload?

1. [ ] 1MB
2. [ ] 50MB
3. [x] 10MB
4. [ ] 5MB

### Question 5

By default, what is the retention duration for a subscription message in Pub/Sub?

1. [ ] 30 days
2. [ ] No maximum retention duration
3. [x] 7 days
4. [ ] 1 day

### Question 6

Pub/Sub is designed for what main purpose?

1. [ ] To receive, buffer and distribute events
2. [ ] To decouple services and distribute workloads
3. [ ] To enable asynchronous workflows
4. [x] All options are correct
5. [ ] To receive, buffer and distribute data

### Question 7

A push Subscription requires what as its endpoint?

1. [ ] An HTTP URL that accepts GET requests.
2. [ ] An HTTPS URL with a self-signed SSL certificate that accepts POST requests.
3. [x] An HTTPS URL with a valid SSL certificate that accepts POST requests.
4. [ ] An HTTPS URL with a self-signed SSL certificate that accepts PUT requests.
5. [ ] An HTTPS URL with a valid SSL certificate that accepts PUT requests.

### Question 8

You have multiple systems that all need to be notified of orders being processed. How should you configure Pub/Sub?

1. [x] Create a Topic for orders. Create multiple Subscriptions for this Topic, one for every system that needs to be
   notified.
2. [ ] Create a Topic for orders. Create a Subscription for this Topic that can be shared by every system that needs to
   be notified.
3. [ ] Create a new Topic for each individual order. Create a Subscription for each Topic that can be shared by every
   system that needs to be notified.
4. [ ] Create a new Topic for each individual order. Create multiple Subscriptions for each Topic, one for every system
   that needs to be notified.

### Question 9

After a period of maintenance for your application, you want to start it up again but there is a large backlog of
messages waiting in its Subscription to a Pub/Sub topic which you do not want to process. What is the best way to deal
with this?

1. [ ] Add extra compute capacity to deal with the backlog of messages and start up the application.
2. [x] Seek to a point in the future on the Subscription to effectively discard all the messages.
3. [ ] Delete the Topic and re-create it.
4. [ ] Delete the Subscription and re-create it.

### Question 10

You want to use Pub/Sub to distribute jobs to a group of Compute Engine VMs, and each VM should take the next job from
the queue. How should you configure Pub/Sub?

1. [ ] Create a Topic for jobs. Create multiple Subscriptions for this Topic, one for every Compute Engine VM in the
   group.
2. [ ] Create a new Topic for each individual job. Create a Subscription for each Topic that can be shared by every
   Compute Engine VM in the group.
3. [x] Create a Topic for jobs. Create a Subscription for this Topic that can be shared by every Compute Engine VM in
   the group.
4. [ ] Create a new Topic for each individual job. Create multiple Subscriptions for each Topic, one for every Compute
   Engine VM in the group.
