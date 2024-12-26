### Question 1

Your model is performing very well on training data, but very poorly on new or unknown data. What could be the problem?

1. [ ] There are insufficient infrastructure resources assigned to the model.
2. [x] There is not enough data in the training set - the model has been overfitted.
3. [ ] There is not enough data in the test set - the model has an implicit bias.
4. [ ] There is not enough data in the validation set - the loss function cannot be minimized.

<details>
  <summary>NOTE</summary>

```
Overfitting results when a model performs well on the training set, generating only a small error,
but struggles with new or unknown data. In other words, the model overfits itself to the data.
Instead of training a model to pick out general features in a given type of data, an overtrained model learns only how
to pick out specific features found in the training set.
```

</details>

### Question 2

Which statement correctly describes the relationship between Keras and TensorFlow?

1. [x] Keras is a high-level deep-learning Python library that includes support for TensorFlow functionality.
2. [ ] TensorFlow is a high-level deep-learning Python library that includes support for Keras functionality.
3. [ ] Keras is a high-level deep-learning Python library that can only function with TensorFlow.
4. [ ] Keras is a high-level deep-learning Python library that has nothing to do with TensorFlow.

<details>
  <summary>NOTE</summary>

```
Keras is a high-level neural networks API, written in Python and capable of running on top of TensorFlow, CNTK, or Theano.
```

</details>

### Question 3

What are hyperparameters used for in machine learning?

1. [ ] Hyperparameters are configuration values specific to GCP machine learning services.
2. [ ] Hyperparameters are the variables that your chosen machine learning technique uses to adjust data, such as weight
   values.
3. [ ] Hyperparameters represent the data used during training to configure a model to make accurate predictions.
4. [x] Hyperparameters are the variables that govern the training process itself.

<details>
  <summary>NOTE</summary>

```
Your hyperparameters are the variables that govern the training process itself.
They are configuration variables, not directly related to the training data.
```

</details>

### Question 4

Which of these problems would require a regression model?

1. [ ] Recognizing faces in a picture.
2. [x] Estimating the price of a house in 5 years time.
3. [ ] Deciding if an image is real or faked.
4. [ ] Identifying changes in a series of images.

<details>
  <summary>NOTE</summary>

```
Regression models attempt to predict numerical output based on known historical data and features.
```

</details>

### Question 5

In the context of TensorFlow, what is a Tensor?

1. [ ] A custom type of data set used in a machine learning pipeline input.
2. [ ] A 2-dimensional matrix of vectors.
3. [x] A multi-dimensional matrix.
4. [x] A representation of an input to a neural network.

<details>
  <summary>NOTE</summary>

```
A Tensor is a multi-dimensional array. In TensorFlow, tf.
Tensor objects have a data type and a shape and can be stored in accelerator memory (ie. GPU memory).
```

</details>

### Question 6

Which of these problems would require a classification model?

1. [ ] Estimating the cost of a taxi fare at a specific time of the year.
2. [ ] Estimating the likelihood of bad weather in a fortnight.
3. [x] Deciding if a picture contains a cat or a dog.
4. [ ] Predicting the value of shares in 12 months time.

<details>
  <summary>NOTE</summary>

```
Classification models attempt to determine if an input maps to a specific known category.
```

</details>

