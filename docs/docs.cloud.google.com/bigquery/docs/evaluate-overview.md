---
name: documents/docs.cloud.google.com/bigquery/docs/evaluate-overview
uri: https://docs.cloud.google.com/bigquery/docs/evaluate-overview
title: BigQuery ML model evaluation overview
description: Learn how to evaluate BigQuery ML models.
data_source: docs.cloud.google.com
---

# BigQuery ML model evaluation overview

This document describes how BigQuery ML supports machine learning (ML) model evaluation.

## Overview of model evaluation

You can use ML model evaluation metrics for the following purposes:

- To assess the quality of the fit between the model and the data.
- To compare different models.
- To predict how accurately you can expect each model to perform on a specific dataset, in the context of model selection.

Supervised and unsupervised learning model evaluations work differently:

- For supervised learning models, model evaluation is well-defined. An evaluation set, which is data that hasn't been analyzed by the model, is typically excluded from the training set and then used to evaluate model performance. We recommend that you don't use the training set for evaluation because this causes the model to perform poorly when generalizing the prediction results for new data. This outcome is known as *overfitting* .
- For unsupervised learning models, model evaluation is less defined and typically varies from model to model. Because unsupervised learning models don't reserve an evaluation set, the evaluation metrics are calculated using the whole input dataset.

## Model evaluation offerings

BigQuery ML provides the following functions to calculate evaluation metrics for ML models:

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Model category</th>
<th>Model types</th>
<th>Model evaluation functions</th>
<th>What the function does</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Supervised learning</td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm">Linear regression</a><br />
<br />
<a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree">Boosted trees regressor</a><br />
<br />
<a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-random-forest">Random forest regressor</a><br />
<br />
<a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-dnn-models">DNN regressor</a><br />
<br />
<a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-wnd-models">Wide-and-deep regressor</a><br />
<br />
<a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-automl">AutoML Tables regressor</a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-evaluate"><code>ML.EVALUATE</code></a></td>
<td>Reports the following metrics:<br />

<ul>
<li>mean absolute error</li>
<li>mean squared error</li>
<li>mean squared log error</li>
<li>median absolute error</li>
<li>r2 score</li>
<li>explained variance</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm">Logistic regression</a><br />
<br />
<a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree">Boosted trees classifier</a><br />
<br />
<a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-random-forest">Random forest classifier</a><br />
<br />
<a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-dnn-models">DNN classifier</a><br />
<br />
<a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-wnd-models">Wide-and-deep classifier</a><br />
<br />
<a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-automl">AutoML Tables classifier</a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-evaluate"><code>ML.EVALUATE</code></a></td>
<td>Reports the following metrics:<br />

<ul>
<li>precision</li>
<li>recall</li>
<li>accuracy</li>
<li>F1 score</li>
<li>log loss</li>
<li>roc auc</li>
</ul></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-confusion"><code>ML.CONFUSION_MATRIX</code></a></td>
<td>Reports the <a href="https://en.wikipedia.org/wiki/Confusion_matrix">confusion matrix</a> .</td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-roc"><code>ML.ROC_CURVE</code></a></td>
<td>Reports metrics for different threshold values, including the following:<br />

<ul>
<li>recall</li>
<li>false positive rate</li>
<li>true positives</li>
<li>false positives</li>
<li>true negatives</li>
<li>false negatives</li>
</ul>
<br />
Only applies to binary-class classification models.</td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Unsupervised learning</td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-kmeans">K-means</a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-evaluate"><code>ML.EVALUATE</code></a></td>
<td>Reports the <a href="https://en.wikipedia.org/wiki/Davies%E2%80%93Bouldin_index">Davies-Bouldin index</a> , and the mean squared distance between data points and the centroids of the assigned clusters.</td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-matrix-factorization">Matrix factorization</a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-evaluate"><code>ML.EVALUATE</code></a></td>
<td>For <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-matrix-factorization#feedback_type">explicit feedback</a> -based models, reports the following metrics:<br />

<ul>
<li>mean absolute error</li>
<li>mean squared error</li>
<li>mean squared log error</li>
<li>median absolute error</li>
<li>r2 score</li>
<li>explained variance</li>
</ul></td>
<td></td>
</tr>
<tr class="odd">
<td>For <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-matrix-factorization#feedback_type">implicit feedback</a> -based models, reports the following metrics:<br />

<ul>
<li><a href="https://en.wikipedia.org/wiki/Evaluation_measures_(information_retrieval)#Mean_average_precision">mean average precision</a></li>
<li>mean squared error</li>
<li><a href="https://en.wikipedia.org/wiki/Discounted_cumulative_gain#Normalized_DCG">normalized discounted cumulative gain</a></li>
<li>average rank</li>
</ul></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-pca">PCA</a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-evaluate"><code>ML.EVALUATE</code></a></td>
<td>Reports the total explained variance ratio.</td>
<td></td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-autoencoder">Autoencoder</a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-evaluate"><code>ML.EVALUATE</code></a></td>
<td>Reports the following metrics:<br />

<ul>
<li>mean absolute error</li>
<li>mean squared error</li>
<li>mean squared log error</li>
</ul></td>
<td></td>
</tr>
<tr class="even">
<td>Time series</td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series">ARIMA_PLUS</a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-evaluate"><code>ML.EVALUATE</code></a></td>
<td>Reports the following metrics:<br />

<ul>
<li>mean absolute error</li>
<li>mean squared error</li>
<li>mean absolute percentage error</li>
<li>symmetric mean absolute percentage error</li>
</ul>
<br />
This function requires new data as input.</td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-arima-evaluate"><code>ML.ARIMA_EVALUATE</code></a></td>
<td>Reports the following metrics for all ARIMA candidate models characterized by different (p, d, q, has_drift) tuples:<br />

<ul>
<li><a href="https://en.wikipedia.org/wiki/Likelihood_function#Log-likelihood">log_likelihood</a></li>
<li><a href="https://en.wikipedia.org/wiki/Akaike_information_criterion">AIC</a></li>
<li>variance</li>
</ul>
<br />
It also reports other information about seasonality, holiday effects, and spikes-and-dips outliers.<br />
<br />
This function doesn't require new data as input.</td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

## Automatic evaluation in `CREATE MODEL` statements

BigQuery ML supports automatic evaluation during model creation. Depending on the model type, the data split training options, and whether you're using hyperparameter tuning, the evaluation metrics are calculated upon the reserved evaluation dataset, the reserved test dataset, or the entire input dataset.

- For k-means, PCA, autoencoder, and ARIMA_PLUS models, BigQuery ML uses all of the input data as training data, and evaluation metrics are calculated against the entire input dataset.

- For linear and logistic regression, boosted tree, random forest, DNN, Wide-and-deep, and matrix factorization models, evaluation metrics are calculated against the dataset that's specified by the following `CREATE MODEL` options:

  - [`DATA_SPLIT_METHOD`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm#data_split_method)
  - [`DATA_SPLIT_EVAL_FRACTION`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm#data_split_eval_fraction)
  - [`DATA_SPLIT_COL`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm#data_split_col)

  When you train these types of models using hyperparameter tuning, the [`DATA_SPLIT_TEST_FRACTION`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-hyperparameter-tuning#data_split) option also helps define the dataset that the evaluation metrics are calculated against. For more information, see [Data split](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-hyperparameter-tuning#data_split) .

- For AutoML Tables models, see [About data splits for AutoML models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/ml-use) .

To get evaluation metrics calculated during model creation, use evaluation functions such as `ML.EVALUATE` on the model with no input data specified. For an example, see [`ML.EVALUATE` with no input data specified](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-evaluate#mlevaluate_with_no_input_data_specified) .

## Evaluation with a new dataset

After model creation, you can specify new datasets for evaluation. To provide a new dataset, use evaluation functions like `ML.EVALUATE` on the model with input data specified. For an example, see [`ML.EVALUATE` with a custom threshold and input data](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-evaluate#mlevaluate_with_a_custom_threshold_and_input_data) .

## Evaluate the results of any regression or classification model

The [`ML.METRICS` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-metrics) lets you compute evaluation metrics for ML classification or regression tasks on any table or query that contains actual and predicted values. This function lets you evaluate predictions without needing to create or reference a stored model.

## What's next

For more information about supported SQL statements and functions for models that support evaluation, see the following documents:

- [End-to-end user journeys for generative AI models](https://docs.cloud.google.com/bigquery/docs/e2e-journey-genai)
- [End-to-end user journeys for ML models](https://docs.cloud.google.com/bigquery/docs/e2e-journey)
