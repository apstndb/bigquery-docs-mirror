---
name: documents/docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-predict
uri: https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-predict
title: The AI.PREDICT function
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# The AI.PREDICT function

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> **Note:** For support during the preview, contact <bqml-feedback@google.com> .

This document describes the `AI.PREDICT` function, which uses a pre-trained foundation model for tabular data, [TabFM](https://docs.cloud.google.com/bigquery/docs/tabfm-model) , to perform regression and classification tasks on structured data.

## Syntax

```
AI.PREDICT(
  { TABLE TRAINING_TABLE | (TRAINING_QUERY)  },
  { TABLE PREDICTION_TABLE | (PREDICTION_QUERY)  }
  [, label_col => 'LABEL_COL' ]
  [, n_ensembles => NUM_ENSEMBLES]
)
```

### Arguments

`AI.PREDICT` takes the following arguments:

- `TRAINING_TABLE | TRAINING_QUERY` : the table or query that contains the training data. The table or query result must contain a column named `label` or the column that you specify in the `LABEL_COL` argument. Every other column is considered a feature column. The feature and label columns must be one of the following types: `STRING` , `BOOL` , `INT64` , `FLOAT64` , `NUMERIC` or `BIGNUMERIC` . All feature columns in `TRAINING_TABLE` (except `label_col` ) must be present in `PREDICTION_TABLE` with the exact same data type. Column ordering doesn't have to match.

- `PREDICTION_TABLE | PREDICTION_QUERY` : the table or query that contains the data to run prediction on. The table or query result must contain all of the feature columns in the training data and can optionally contain additional columns.

- `LABEL_COL` : a `STRING` value that specifies the name of the label column in the training data. The default value is `'label'` . If the column is of type `STRING` or `BOOL` , then classification is evaluated. If the column is of type `INT64` , `FLOAT64` , `NUMERIC` or `BIGNUMERIC` , then regression is evaluated.

- `NUM_ENSEMBLES` : an `INT64` value between `1` and `32` that specifies the number of in-context ensemble members to run and average. The default value is `4` . Increasing `n_ensembles` improves prediction accuracy and stability with a linear increase in token consumption. Setting the value to `1` or `2` reduces latency and cost.

## Output

`AI.PREDICT` returns the columns from the training table or query result in addition to the following columns:

- If the label column is of type `INT64` , `FLOAT64` , `NUMERIC` or `BIGNUMERIC` , then `AI.PREDICT` performs a regression task and returns the following column:

  - `predicted_<label_column_name>` : contains the predicted numerical values. The data type is the same as the label column in the training data.

- If the label column is of type `BOOL` or `STRING` , then `AI.PREDICT` performs a classification task and returns the following columns:

  - `predicted_<label_column_name>` : contains the predicted values. The data type is the same as the label column in the training data.
  - `predicted_<label_column_name>_probs` : an `ARRAY<STRUCT<label STRING, prob FLOAT64>>` value that contains each possible label and the probability of assignment to that label.

## Examples

The following examples show how to use the `AI.PREDICT` function for regression and classification tasks.

### Perform regression

The following query uses `AI.PREDICT` to perform regression to predict the body mass of penguins:

```
WITH prepared_data AS (
  SELECT *, RAND() <= 0.8 AS training
  FROM `bigquery-public-data.ml_datasets.penguins`
  WHERE body_mass_g > 0
)
SELECT
  *
FROM AI.PREDICT(
  # Training data
  (SELECT * EXCEPT(training) FROM prepared_data WHERE training),
  # Prediction data
  (SELECT * EXCEPT(training) FROM prepared_data WHERE NOT training),
  label_col => 'body_mass_g');
```

The result is similar to the following:

```
+-------------------+--------+------------------+-----------------+-------------------+-------------+--------+-----------------------+
| species           | island | culmen_length_mm | culmen_depth_mm | flipper_length_mm | body_mass_g | sex    | predicted_body_mass_g |
+-------------------+--------+------------------+-----------------+-------------------+-------------+--------+-----------------------+
| Adelie Penguin... | Dream  | 40.9             | 18.9            | 184.0             | 3900.0      | MALE   | 3904.0                |
| Adelie Penguin... | Dream  | 37.0             | 16.9            | 185.0             | 3000.0      | FEMALE | 3168.0                |
| ...               | ...    | ...              | ...             | ...               | ...         | ...    | ...                   |
+-------------------+--------+------------------+-----------------+-------------------+-------------+--------+-----------------------+
```

The following query uses `AI.PREDICT` to perform regression with the TabFM model. `n_ensembles` is set to `8` to predict the body mass of penguins using the `body_mass_g` numerical column:

```
WITH
  prepared_data AS (
    SELECT
      species,
      island,
      culmen_length_mm,
      culmen_depth_mm,
      flipper_length_mm,
      sex,
      body_mass_g,
      ROW_NUMBER()
        OVER (
          ORDER BY
            species,
            island,
            culmen_length_mm,
            culmen_depth_mm,
            flipper_length_mm,
            sex,
            body_mass_g
        ) AS row_num
    FROM
      `bigquery-public-data.ml_datasets.penguins`
    WHERE
      body_mass_g IS NOT NULL
  )
SELECT
  *
FROM
  AI.PREDICT(
    -- 1. Training Data
    (
      SELECT
        species,
        island,
        culmen_length_mm,
        culmen_depth_mm,
        flipper_length_mm,
        sex,
        body_mass_g
      FROM
        prepared_data
      WHERE
        row_num <= 292
    ),
    -- 2. Prediction Data
    (
      SELECT
        species,
        island,
        culmen_length_mm,
        culmen_depth_mm,
        flipper_length_mm,
        sex
      FROM
        prepared_data
      WHERE
        row_num > 292
    ),
    -- 3. Options
    label_col => 'body_mass_g',
    n_ensembles => 8);
```

The result is similar to the following:

```
+-------------------+--------+------------------+-----------------+-------------------+--------+-----------------------+
| species           | island | culmen_length_mm | culmen_depth_mm | flipper_length_mm | sex    | predicted_body_mass_g |
+-------------------+--------+------------------+-----------------+-------------------+--------+-----------------------+
| Gentoo penguin... | Biscoe | 48.4             | 14.4            | 203.0             | FEMALE | 4614.56                |
| Gentoo penguin... | Biscoe | 48.4             | 14.6            | 213.0             | MALE   | 5149.17                |
| ...               | ...    | ...              | ...             | ...               | ...    | ...                   |
+-------------------+--------+------------------+-----------------+-------------------+--------+-----------------------+
```

### Calculate prediction accuracy

You can compute regression metrics for the predictions using the [`ML.METRICS` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-metrics) :

```
WITH prepared_data AS (
  SELECT *, RAND() <= 0.8 AS training
  FROM `bigquery-public-data.ml_datasets.penguins`
  WHERE body_mass_g > 0
)
SELECT *
FROM ML.METRICS(
  (
    SELECT
    *
    FROM
    AI.PREDICT(
      # Training data
      (SELECT * EXCEPT(training) FROM prepared_data WHERE training),
      # Prediction data
      (SELECT * EXCEPT(training) FROM prepared_data WHERE NOT training),
      label_col => 'body_mass_g')
  ),
  predicted_col => 'predicted_body_mass_g',
  actual_col => 'body_mass_g',
  task_type => 'regression');
```

The result is similar to the following:

```
+---------------------+--------------------+------------------------+-----------------------+---------------------+---------------------+
| mean_absolute_error | mean_squared_error | mean_squared_log_error | median_absolute_error | r2_score            | explained_variance  |
+---------------------+--------------------+------------------------+-----------------------+---------------------+---------------------+
| 158.33734939759032  | 46334.843373493975 | 0.0027285838904596953  | 104.0                 | 0.91609072642998024 | 0.91803270745448851 |
+---------------------+--------------------+------------------------+-----------------------+---------------------+---------------------+
```

### Perform classification

The following query uses `AI.PREDICT` to perform classification to predict the sex of a penguin:

```
WITH prepared_data AS (
  SELECT *, RAND() <= 0.8 AS training
  FROM `bigquery-public-data.ml_datasets.penguins`
  WHERE sex IS NOT NULL and sex != "."
)
SELECT
 *
FROM
 AI.PREDICT(
  # Training data
  (SELECT * EXCEPT(training) FROM prepared_data WHERE training),
  # Prediction data
  (SELECT * EXCEPT(training) FROM prepared_data WHERE NOT training),
  label_col => 'sex');
```

The result is similar to the following:

```
+----------------------+--------+------------------+-----+--------+---------------+---------------------------+--------------------------+
| species                | island | culmen_length_mm | ... | sex    | predicted_sex | predicted_sex_probs.label | predicted_sex_probs.prob |
+----------------------+--------+------------------+-----+--------+---------------+---------------------------+--------------------------+
| Chinstrap Penguin... | Dream  | 40.9             | ... | FEMALE | FEMALE        | MALE                      | 0.006192990157855187     |
|                      |        |                  |     |        |               | FEMALE                    | 0.99380700984214487      |
| Adelie Penguin...    | Dream  | 37.0             | ... | MALE   | MALE          | MALE                      | 0.99561766335926927      |
|                      |        |                  |     |        |               | FEMALE                    | 0.0043823366407307451    |
| ...                  | ...    | ...              | ... |        | ...           | ...                       | ...                      |
+----------------------+--------+------------------+-----+--------+---------------+---------------------------+--------------------------+
```

## Locations

`AI.PREDICT` and the TabFM model are available in all [supported BigQuery ML locations](https://docs.cloud.google.com/bigquery/docs/locations#locations-for-non-remote-models) .

### Data processing and residency

Data processing and residency for `AI.PREDICT` depend on your query location:

- Queries run in the `US` multi-region or any US single region are processed in the US.
- Queries run in the `EU` multi-region or any EU single region other than `europe-west2` (London) and `europe-west6` (Switzerland) are processed in the EU.
- All other locations, including `europe-west2` (London) and `europe-west6` (Switzerland), have no data residency commitment, and data might be processed outside your query region.

## Pricing

`AI.PREDICT` usage is billed at the evaluation, inspection, and prediction rate documented in the **BigQuery ML on-demand pricing** section of the [BigQuery ML pricing](https://cloud.google.com/bigquery/pricing#bigquery-ml-pricing) page.

BigQuery TabFM uses token-based pricing in addition to standard [BigQuery compute pricing](https://cloud.google.com/bigquery/pricing#compute-pricing-models) . You are charged for two components:

- **TabFM tokens** : tokens consumed by the TabFM model in your query. For rates, see [BigQuery ML pricing](https://cloud.google.com/bigquery/pricing#bigquery-ml-pricing) .
- **BigQuery compute** : slots used under Enterprise or Enterprise Plus edition, or bytes processed under on-demand pricing, for the rest of the query.

## Limitations

The following limitations apply to `AI.PREDICT` :

- Your training data can include up to 80,000 sampled training rows.
- Your data can include up to 128 feature columns. If you need to use more than 128 feature columns, contact <bqml-feedback@google.com> .
- You can classify data into at most 10 different categories.
- `AI.PREDICT` can't be used in [Assured Workloads](https://docs.cloud.google.com/assured-workloads/docs/overview) projects.

## What's next

- Evaluate the performance of the TabFM model by using the [`AI.EVALUATE` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-evaluate) .
- Learn more about [regression](https://docs.cloud.google.com/bigquery/docs/regression-overview) and [classification](https://docs.cloud.google.com/bigquery/docs/classification-overview) in BigQuery.
