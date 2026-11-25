---
name: documents/docs.cloud.google.com/bigquery/docs/tabfm-model
uri: https://docs.cloud.google.com/bigquery/docs/tabfm-model
title: The TabFM model
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# The TabFM model

> **Preview**
>
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> **Note:** For support during the preview, contact <bqml-feedback@google.com> .

This document describes BigQuery's built-in TabFM tabular regression and classification model.

The built-in TabFM model is an implementation of Google Research's open source [TabFM model](https://github.com/google-research/tabfm) . The Google Research TabFM model is a foundation model for tabular data that enables zero-shot regression and classification on structured data through in-context learning. Because the TabFM model is pre-trained on hundreds of millions of synthetic datasets generated using structural causal models, it captures complex feature interactions and generalizes well to unseen real-world tables across many domains.

## Functions supported by the TabFM model

You can use the TabFM model with the [`AI.PREDICT` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-predict) to perform regression and classification on structured data in a single forward pass without having to train a model, optimize hyperparameters, or engineer features. The prediction results are comparable to conventional supervised tree-based algorithms such as XGBoost and random forests. If you want more model tuning options than the TabFM model offers, you can train a supervised model such as a [boosted tree](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree) or [random forest](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-random-forest) model and use it with the [`ML.PREDICT` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-predict) instead.

To generate predictions with the TabFM model on tabular data, use the [`AI.PREDICT` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-predict) .

To evaluate predicted values from the TabFM model against the actual values, use the [`AI.EVALUATE` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-evaluate) .

## TabFM 1.1 capabilities

TabFM 1.1 is the default model used by the `AI.PREDICT` and `AI.EVALUATE` functions, providing improved accuracy, lower latency, and higher scale for tabular workloads. The following table lists the capabilities of the TabFM 1.1 model:

| Capability                    | TabFM 1.1                                              |
|-------------------------------|--------------------------------------------------------|
| **Supported Tasks**           | Regression and classification (up to 10 classes)       |
| **Max Feature Columns**       | 128                                                    |
| **Max Sampled Training Rows** | Up to 80,000 rows                                      |
| **Configurable Ensembling**   | Supported (default value is 4; valid range is 1 to 32) |

## Additional resources

To learn more about the Google Research TabFM model, use the following resources:

- [Google Research blog](https://research.google/blog/introducing-tabfm-a-zero-shot-foundation-model-for-tabular-data/)
- [Google Cloud blog](https://cloud.google.com/blog/products/data-analytics/tabfm-adds-predictive-ml-to-bigquery)
- [GitHub repository](https://github.com/google-research/tabfm)
- [Hugging Face page](https://huggingface.co/google/tabfm-1.0.0-pytorch)

## Terms of service

When you use TabFM through BigQuery, your usage is governed by the [Google Cloud Terms of Service](https://cloud.google.com/terms) and allows for commercial uses. The non-commercial license associated with the publicly downloadable TabFM weights on GitHub and Hugging Face applies only to self-hosted downloads and does not restrict usage within BigQuery.

## Pricing

BigQuery TabFM uses token-based pricing in addition to standard [BigQuery compute pricing](https://cloud.google.com/bigquery/pricing#compute-pricing-models) . You are charged for two components:

- **TabFM tokens** : tokens consumed by the TabFM model in your query. For rates, see [BigQuery ML pricing](https://cloud.google.com/bigquery/pricing#bigquery-ml-pricing) .
- **BigQuery compute** : slots used under Enterprise or Enterprise Plus edition, or bytes processed under on-demand pricing, for the rest of the query.
