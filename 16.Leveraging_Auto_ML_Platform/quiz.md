### Question 1

You wish to build an AutoML Natural Language model for classifying some documents with user-defined labels. How can you
ensure you are providing quality training data for the model?

1. [x] Ensure you provide at minimum 10 training documents per label, but ideally 100 times more documents for the most
   common label than for the least common label.
2. [ ] Ensure you provide at minimum 100 training documents per label, but ideally 10 times more documents for the most
   common label than for the least common label.
3. [ ] Aim to provide over 1,000,000 documents in total.
4. [ ] Minimize the diversity of documents in the training data. Ensure documents are by the same author and of the same
   length wherever possible.

<details>
  <summary>NOTE</summary>

```
Quality training data for an AutoML Natural Language classification model should contain varied input documents,
with a minimum of 10 documents per label, and ideally 100 times more documents for the most common label than for
the least common label. The maximum number of documents for training data is 1,000,000.
```

</details>

### Question 2

Which AutoML Vision feature would you use to detect multiple objects in an image?

1. [ ] Confidence threshold curves
2. [x] Object localization
3. [ ] Object classification
4. [ ] Human labeling

<details>
  <summary>NOTE</summary>

```
Object localization detects multiple objects in an image and provides information about 
the object and where the object was found in the image.
```

</details>

### Question 3

You're developing a mobile application that allows a food processing business to detect fruit that has gone bad. Staff
at warehouses will use mobile devices to take pictures of fruit to determine whether it should be discarded. Which GCP
services could you use to train a custom classification model using image data in the quickest possible way, allowing
the model to be deployed to Android and iOS devices?

1. [ ] Train an AutoML Vision model using unlabeled images of fruit that has gone bad. Use AutoML Vision Edge in ML
   Kit (now custom model API) to deploy the custom model to mobile devices using ML Kit client libraries.
2. [ ] Train an AutoML Vision model using labeled images of fruit that has gone bad. Use AutoML Vision Edge in ML Kit (
   now custom model API) to deploy the custom model to mobile devices using ML Kit client libraries.
3. [ ] Train an AutoML Vision model using labeled images of fruit that has gone bad. Export the model as a container
   image. Deploy an API on Kubernetes Engine to provide a backend for a mobile scanning application.
4. [ ] Train an AutoML Vision model using unlabeled images of fruit that has gone bad. Export the model with TensorFlow
   Lite. Deploy an API on App Engine to provide a backend for a mobile scanning application.

<details>
  <summary>NOTE</summary>

```
The AutoML Vision service is the quickest way to train a custom classification model using image data, and the Vision Edge 
in ML Kit (now part of the custom model API) will allow the model to be deployed to Android and iOS devices. 
Images must be labelled in order for the model to be trained. There is no need to use Kubernetes Engine or App Engine. 
AutoML Vision API Tutorial | Cloud AutoML Vision | Google Cloud.
```

</details>

### Question 4

You have a large number of images that you wish to process through a custom AutoML Vision model. Time is not a factor,
but cost is. Which approach should you take?

1. [x] Make an asynchronous prediction request for the entire batch of images using the batchPredict method.
2. [ ] Send each image a synchronous online prediction request.
3. [ ] Sort the images into small batches, and make an asynchronous prediction request for each batch using the
   batchPredict method.
4. [ ] Select a random subset of the images and send each as a synchronous online prediction request.

<details>
  <summary>NOTE</summary>

```
Batch prediction often offers a lower cost per inference and higher throughput than synchronous (online) prediction.
However, batch prediction produces a long-running operation (LRO), meaning that results are only available once the LRO has completed.
```

</details>

### Question 5

How can you import training data into an AutoML Natural Language dataset?

1. [ ] As TXT, PDF, TIF or ZIP files, from a Cloud Storage bucket.
2. [x] As TXT, PDF, TIF or ZIP files, or as a CSV containing references to documents and training labels, from a local
   upload or Cloud Storage bucket.
3. [ ] From existing datasets in BigQuery or Cloud Bigtable.
4. [ ] As TXT, PDF, TIF or ZIP files, from a local upload or Cloud Storage bucket.

<details>
  <summary>NOTE</summary>

```
You can import document URIs and labels for documents from a CSV file stored in a Cloud Storage bucket,
and upload training documents directly from your local computer or a Cloud Storage bucket.
```

</details>
