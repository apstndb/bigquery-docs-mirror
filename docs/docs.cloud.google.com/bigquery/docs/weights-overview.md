# BigQuery ML model weights overview

This document describes how BigQuery ML supports model weights discoverability for machine learning (ML) models.

An ML model is an artifact that is saved after running an ML algorithm on training data. The model represents the rules, numbers, and any other algorithm-specific data structures that are required to make predictions. Some examples include the following:

  - A linear regression model is comprised of a vector of coefficients that have specific values.
  - A decision tree model is comprised of one or more trees of if-then statements that have specific values.
  - A deep neural network model is comprised of a graph structure with vectors or matrixes of weights that have specific values.

In BigQuery ML, the term *model weights* is used to describe the components that a model is comprised of.

## Model weights offerings in BigQuery ML

BigQuery ML offers multiple functions that you can use to retrieve the model weights for different models.

Model category

Model types

Model weights functions

What the function does

Supervised models

[Linear & Logistic Regression](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm)

`  ML.WEIGHTS  `

Retrieves the feature coefficients and the intercept.

Unsupervised models

[Kmeans](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-kmeans)

`  ML.CENTROIDS  `

Retrieves the feature coefficients for all of the centroids.

[Matrix Factorization](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-matrix-factorization)

`  ML.WEIGHTS  `

Retrieves the weights of all of the latent factors. They represent the two decomposed matrixes, the user matrix and the item matrix.

[PCA](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-pca)

`  ML.PRINCIPAL_COMPONENTS  `

Retrieves the feature coefficients for all principal components, also known as eigenvectors.

`  ML.PRINCIPAL_COMPONENT_INFO  `

Retrieves the statistics of each principal component, such as eigenvalue.

Time series models

[ARIMA\_PLUS](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series)

`  ML.ARIMA_COEFFICIENTS  `

Retrieves the coefficients of the ARIMA model, which is used to model the trend component of the input time series. For information about other components, such as seasonal patterns that are present in the time series, use `  ML.ARIMA_EVALUATE  ` .

BigQuery ML doesn't support model weight functions for the following types of models:

  - [Boosted tree](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree)
  - [Random forest](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-random-forest)
  - [Deep neural network (DNN)](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-dnn-models)
  - [Wide-and-deep](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-wnd-models)
  - [AutoML Tables](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-automl)

To see the weights of all of these model types except for AutoML Tables models, export the model from BigQuery ML to Cloud Storage. You can then use the XGBoost library to visualize the tree structure for boosted tree and random forest models, or the TensorFlow library to visualize the graph structure for DNN and wide-and-deep models. There is no method for getting model weight information for AutoML Tables models.

For more information about exporting a model, see [`  EXPORT MODEL  ` statement](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-export-model) and [Export a BigQuery ML model for online prediction](/bigquery/docs/export-model-tutorial) .

## What's next

For more information about supported SQL statements and functions for ML models, see [End-to-end user journeys for ML models](/bigquery/docs/e2e-journey) .
