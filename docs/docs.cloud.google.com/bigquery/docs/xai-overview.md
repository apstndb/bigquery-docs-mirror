---
name: documents/docs.cloud.google.com/bigquery/docs/xai-overview
uri: https://docs.cloud.google.com/bigquery/docs/xai-overview
title: BigQuery Explainable AI overview
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# BigQuery Explainable AI overview

This document describes how BigQuery ML supports Explainable artificial intelligence (AI), sometimes called XAI.

Explainable AI helps you understand the results that your predictive machine learning model generates for classification and regression tasks by defining how each feature in a row of data contributed to the predicted result. This information is often referred to as feature attribution. You can use this information to verify that the model is behaving as expected, to recognize biases in your models, and to inform ways to improve your model and your training data.

## Local versus global explainability

There are two types of explainability: local explainability and global explainability. These are also known respectively as *local feature importance* and *global feature importance* .

  - Local explainability returns feature attribution values for each explained example. These values describe how much a particular feature affected the prediction relative to the baseline prediction.
  - Global explainability returns the feature's overall influence on the model and is often obtained by aggregating the feature attributions over the entire dataset. A higher absolute value indicates the feature had a greater influence on the model's predictions.

## Explainable AI offerings in BigQuery ML

Explainable AI in BigQuery ML supports a variety of machine learning models, including both time series and non-time series models. Each of the models takes advantage of a different explainability method.

Model category

Model types

Explainability method

Basic explanation of the method

Local explain functions

Global explain functions

Supervised models

[Linear & Logistic Regression](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm)

[Shapley values](https://christophm.github.io/interpretable-ml-book/shapley.html#the-shapley-value-in-detail)

Shapley values for linear models are equal to `model weight * feature value` , where feature values are standardized and model weights are trained with the standardized feature values.

[`ML.EXPLAIN_PREDICT` <sup>1</sup>](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-explain-predict)

[`ML.GLOBAL_EXPLAIN` <sup>2</sup>](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-global-explain)

[Standard Errors](https://en.wikipedia.org/wiki/Standard_error) and [P-values](https://en.wikipedia.org/wiki/P-value)

Standard errors and p-values are used for significance testing against the model weights.

N/A

[`ML.ADVANCED_WEIGHTS` <sup>4</sup>](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-advanced-weights)

[Boosted trees](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree)  
  
[Random forest](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-random-forest)

[Tree SHAP](https://docs.seldon.io/projects/alibi/en/stable/methods/TreeSHAP.html)

Tree SHAP is an algorithm to compute exact [SHAP values](https://christophm.github.io/interpretable-ml-book/shap.html) for decision tree-based models.

[`ML.EXPLAIN_PREDICT` <sup>1</sup>](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-explain-predict)

[`ML.GLOBAL_EXPLAIN` <sup>2</sup>](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-global-explain)

[Approximate Feature Contribution](http://blog.datadive.net/interpreting-random-forests/)

Approximates the feature contribution values. It is faster and simpler compared to Tree SHAP.

[`ML.EXPLAIN_PREDICT` <sup>1</sup>](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-explain-predict)

[`ML.GLOBAL_EXPLAIN` <sup>2</sup>](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-global-explain)

[Gini Index-based feature importance](https://xgboost.readthedocs.io/en/latest/python/python_api.html?#xgboost.XGBRegressor.feature_importances_)

A global feature importance score that indicates how useful or valuable each feature was in the construction of the boosted tree or random forest model during training.

N/A

[`ML.FEATURE_IMPORTANCE`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-importance)

[AutoML Tables](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-automl)

[Sampled Shapley](https://docs.cloud.google.com/vertex-ai/docs/explainable-ai/overview#compare-methods)

Sampled Shapley assigns credit for the model's outcome to each feature, and considers different permutations of the features. This method provides a sampling approximation of exact Shapley values.

N/A

[`ML.GLOBAL_EXPLAIN`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-global-explain) <sup>2</sup>

Time series models

[ARIMA\_PLUS](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series)

[Time series decomposition](https://otexts.com/fpp2/decomposition.html)

Decomposes the time series into multiple components if those components are present in the time series. The components include trend, seasonal, holiday, step changes, and spike and dips. See ARIMA\_PLUS [modeling pipeline](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series#modeling-pipeline) for more details.

[`ML.EXPLAIN_FORECAST` <sup>3</sup>](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-explain-forecast)

N/A

[ARIMA\_PLUS\_XREG](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-multivariate-time-series)

[Time series decomposition](https://otexts.com/fpp2/decomposition.html)  
and  
[Shapley values](https://christophm.github.io/interpretable-ml-book/shapley.html#the-shapley-value-in-detail)

Decomposes the time series into multiple components, including trend, seasonal, holiday, step changes, and spike and dips (similar to [ARIMA\_PLUS](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series) ). Attribution of each external regressor is calculated based on Shapley Values, which is equal to `model weight * feature value` .

[`ML.EXPLAIN_FORECAST` <sup>3</sup>](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-explain-forecast)

N/A

<sup>1</sup> `ML_EXPLAIN_PREDICT` is an extended version of `ML.PREDICT` .

<sup>2</sup> `ML.GLOBAL_EXPLAIN` returns the global explainability obtained by taking the mean absolute attribution that each feature receives for all the rows in the evaluation dataset.

<sup>3</sup> `ML.EXPLAIN_FORECAST` is an extended version of `ML.FORECAST` .

<sup>4</sup> `ML.ADVANCED_WEIGHTS` is an extended version of `ML.WEIGHTS` .

## What's next

  - For more information about supported SQL statements and functions for models that support explainability, see [End-to-end user journeys for ML models](https://docs.cloud.google.com/bigquery/docs/e2e-journey) .
