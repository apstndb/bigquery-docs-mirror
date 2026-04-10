# Automatic feature preprocessing

BigQuery ML performs automatic preprocessing during training by using the [`  CREATE MODEL  ` statement](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create) . Automatic preprocessing consists of [missing value imputation](https://docs.cloud.google.com/bigquery/docs/auto-preprocessing#imputation) and [feature transformations](https://docs.cloud.google.com/bigquery/docs/auto-preprocessing#feature-transform) .

For information about feature preprocessing support in BigQuery ML, see [Feature preprocessing overview](https://docs.cloud.google.com/bigquery/docs/preprocess-overview) .

## Missing data imputation

In statistics, imputation is used to replace missing data with substituted values. When you train a model in BigQuery ML, `  NULL  ` values are treated as missing data. When you predict outcomes in BigQuery ML, missing values can occur when BigQuery ML encounters a `  NULL  ` value or a previously unseen value. BigQuery ML handles missing data differently, based on the type of data in the column.

| Column type                | Imputation method                                                                                                                                                                                                                                                                                                                                                                 |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Numeric                    | In both training and prediction, `        NULL       ` values in numeric columns are replaced with the mean value of the given column, as calculated by the feature column in the original input data.                                                                                                                                                                            |
| One-hot/Multi-hot encoded  | In both training and prediction, `        NULL       ` values in the encoded columns are mapped to an additional category that is added to the data. Previously unseen data is assigned a weight of 0 during prediction.                                                                                                                                                          |
| `        TIMESTAMP       ` | `        TIMESTAMP       ` columns use a mixture of imputation methods from both standardized and one-hot encoded columns. For the generated Unix time column, BigQuery ML replaces values with the mean Unix time across the original columns. For other generated values, BigQuery ML assigns them to the respective `        NULL       ` category for each extracted feature. |
| `        STRUCT       `    | In both training and prediction, each field of the `        STRUCT       ` is imputed according to its type.                                                                                                                                                                                                                                                                      |

## Feature transformations

By default, BigQuery ML transforms input features as follows:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Input data type</th>
<th>Transformation method</th>
<th>Details</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-types#integer_types"><code dir="ltr" translate="no">        INT64       </code></a><br />
<a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-types#numeric_type"><code dir="ltr" translate="no">        NUMERIC       </code></a><br />
<a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-types#bignumeric_type"><code dir="ltr" translate="no">        BIGNUMERIC       </code></a><br />
<a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-types#floating_point_types"><code dir="ltr" translate="no">        FLOAT64       </code></a></td>
<td><a href="https://en.wikipedia.org/wiki/Feature_scaling#Standardization">Standardization</a></td>
<td>For most models, BigQuery ML standardizes and centers numerical columns at zero before passing it into training. The exceptions are boosted tree and random forest models, for which no standardization occurs, and k-means models, where the <code dir="ltr" translate="no">       STANDARDIZE_FEATURES      </code> option controls whether numerical features are standardized.</td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-types#boolean_type"><code dir="ltr" translate="no">        BOOL       </code></a><br />
<a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-types#string_type"><code dir="ltr" translate="no">        STRING       </code></a><br />
<a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-types#bytes_type"><code dir="ltr" translate="no">        BYTES       </code></a><br />
<a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-types#date_type"><code dir="ltr" translate="no">        DATE       </code></a><br />
<a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-types#datetime_type"><code dir="ltr" translate="no">        DATETIME       </code></a><br />
<a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-types#time_type"><code dir="ltr" translate="no">        TIME       </code></a></td>
<td><a href="https://developers.google.com/machine-learning/glossary/#one-hot_encoding">One-hot encoded</a></td>
<td>For all non-numerical, non-array columns other than <code dir="ltr" translate="no">       TIMESTAMP      </code> , BigQuery ML performs a one-hot encoding transformation for all models other than boosted tree and random forest models. This transformation generates a separate feature for each unique value in the column. Label encoding transformation is applied to train boosted tree and random forest models to convert each unique value into a numerical value.</td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-types#array_type"><code dir="ltr" translate="no">        ARRAY       </code></a></td>
<td>Multi-hot encoded</td>
<td>For all non-numerical <code dir="ltr" translate="no">       ARRAY      </code> columns, BigQuery ML performs a multi-hot encoding transformation. This transformation generates a separate feature for each unique element in the <code dir="ltr" translate="no">       ARRAY      </code> .</td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-types#timestamp_type"><code dir="ltr" translate="no">        TIMESTAMP       </code></a></td>
<td>Timestamp transformation</td>
<td>When a linear or logistic regression model encounters a <code dir="ltr" translate="no">       TIMESTAMP      </code> column, it extracts a set of components from the <code dir="ltr" translate="no">       TIMESTAMP      </code> and performs a mix of standardization and one-hot encoding on the extracted components. For the Unix epoch time in seconds component, BigQuery ML uses standardization. For all other components, it uses one-hot encoding.<br />
<br />
For more information, see the following <a href="https://docs.cloud.google.com/bigquery/docs/auto-preprocessing#timestamp-transform">timestamp feature transformation table</a> .</td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-types#struct_type"><code dir="ltr" translate="no">        STRUCT       </code></a></td>
<td>Struct expansion</td>
<td>When BigQuery ML encounters a <code dir="ltr" translate="no">       STRUCT      </code> column, it expands the fields inside the <code dir="ltr" translate="no">       STRUCT      </code> to create a single column. It requires all fields of <code dir="ltr" translate="no">       STRUCT      </code> to be named. Nested <code dir="ltr" translate="no">       STRUCT      </code> s are not allowed. The column names after expansion are in the format of <code dir="ltr" translate="no">       {struct_name}_{field_name}      </code> .</td>
</tr>
<tr class="even">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-types#array_type"><code dir="ltr" translate="no">        ARRAY       </code></a> of <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-types#struct_type"><code dir="ltr" translate="no">        STRUCT       </code></a></td>
<td>No transformation</td>
<td></td>
</tr>
<tr class="odd">
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-types#array_type"><code dir="ltr" translate="no">        ARRAY       </code></a> of <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-types#numeric_types"><code dir="ltr" translate="no">        NUMERIC       </code></a></td>
<td>No transformation</td>
<td></td>
</tr>
</tbody>
</table>

### `     TIMESTAMP    ` feature transformation

The following table shows the components extracted from `  TIMESTAMP  ` columns and the corresponding transformation method.

| `        TIMESTAMP       ` component | `        processed_input       ` result | Transformation method |
| ------------------------------------ | --------------------------------------- | --------------------- |
| Unix epoch time in seconds           | `        [COLUMN_NAME]       `          | Standardization       |
| Day of month                         | `        _TS_DOM_[COLUMN_NAME]       `  | One-hot encoding      |
| Day of week                          | `        _TS_DOW_[COLUMN_NAME]       `  | One-hot encoding      |
| Month of year                        | `        _TS_MOY_[COLUMN_NAME]       `  | One-hot encoding      |
| Hour of day                          | `        _TS_HOD_[COLUMN_NAME]       `  | One-hot encoding      |
| Minute of hour                       | `        _TS_MOH_[COLUMN_NAME]       `  | One-hot encoding      |
| Week of year (weeks begin on Sunday) | `        _TS_WOY_[COLUMN_NAME]       `  | One-hot encoding      |
| Year                                 | `        _TS_YEAR_[COLUMN_NAME]       ` | One-hot encoding      |

## Category feature encoding

For features that are one-hot encoded, you can specify a different default encoding method by using the model option `  CATEGORY_ENCODING_METHOD  ` . For generalized linear models (GLM) models, you can set `  CATEGORY_ENCODING_METHOD  ` to one of the following values:

  - [`  ONE_HOT_ENCODING  `](https://docs.cloud.google.com/bigquery/docs/auto-preprocessing#one_hot_encoding)
  - [`  DUMMY_ENCODING  `](https://docs.cloud.google.com/bigquery/docs/auto-preprocessing#dummy_encoding)
  - [`  LABEL_ENCODING  `](https://docs.cloud.google.com/bigquery/docs/auto-preprocessing#label_encoding)
  - [`  TARGET_ENCODING  `](https://docs.cloud.google.com/bigquery/docs/auto-preprocessing#dummy_encoding)

### One-hot encoding

One-hot encoding maps each category that a feature has to its own binary feature, where `  0  ` represents the absence of the feature and `  1  ` represents the presence (known as a *dummy variable* ). This mapping creates `  N  ` new feature columns, where `  N  ` is the number of unique categories for the feature across the training table.

For example, suppose your training table has a feature column that's called `  fruit  ` with the categories `  Apple  ` , `  Banana  ` , and `  Cranberry  ` , such as the following:

| Row | fruit     |
| --- | --------- |
| 1   | Apple     |
| 2   | Banana    |
| 3   | Cranberry |

In this case, the `  CATEGORY_ENCODING_METHOD='ONE_HOT_ENCODING'  ` option transforms the table to the following internal representation:

| Row | fruit\_Apple | fruit\_Banana | fruit\_Cranberry |
| --- | ------------ | ------------- | ---------------- |
| 1   | 1            | 0             | 0                |
| 2   | 0            | 1             | 0                |
| 3   | 0            | 0             | 1                |

One-hot encoding is supported by [linear and logistic regression](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm) and [boosted tree](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree) models.

### Dummy encoding

[Dummy encoding](https://en.wikiversity.org/wiki/Dummy_variable_\(statistics\)) is similar to one-hot encoding, where a categorical feature is transformed into a set of placeholder variables. Dummy encoding uses `  N-1  ` placeholder variables instead of `  N  ` placeholder variables to represent `  N  ` categories for a feature. For example, if you set `  CATEGORY_ENCODING_METHOD  ` to `  'DUMMY_ENCODING'  ` for the same `  fruit  ` feature column shown in the preceding one-hot encoding example, then the table is transformed to the following internal representation:

| Row | fruit\_Apple | fruit\_Banana |
| --- | ------------ | ------------- |
| 1   | 1            | 0             |
| 2   | 0            | 1             |
| 3   | 0            | 0             |

The category with the most occurrences in the training dataset is dropped. When multiple categories have the most occurrences, a random category within that set is dropped.

The final set of weights from [`  ML.WEIGHTS  `](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-weights) still includes the dropped category, but its weight is always `  0.0  ` . For [`  ML.ADVANCED_WEIGHTS  `](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-advanced-weights) , the standard error and p-value for the dropped variable is `  NaN  ` .

If `  warm_start  ` is used on a model that was initially trained with `  'DUMMY_ENCODING'  ` , the same placeholder variable is dropped from the first training run. Models cannot change encoding methods between training runs.

Dummy encoding is supported by [linear and logistic regression models](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm) .

### Label encoding

Label encoding transforms the value of a categorical feature to an `  INT64  ` value in `  [0, <number of categories>]  ` .

For example, if you had a book dataset like the following:

| Title  | Genre   |
| ------ | ------- |
| Book 1 | Fantasy |
| Book 2 | Cooking |
| Book 3 | History |
| Book 4 | Cooking |

The label encoded values might look similar to the following:

| Title  | Genre (text) | Genre (numeric) |
| ------ | ------------ | --------------- |
| Book 1 | Fantasy      | 1               |
| Book 2 | Cooking      | 2               |
| Book 3 | History      | 3               |
| Book 4 | Cooking      | 2               |

The encoding vocabulary is sorted alphabetically. `  NULL  ` values and categories that aren't in the vocabulary are encoded to `  0  ` .

Label encoding is supported by [boosted tree models](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree) .

### Target encoding

Target encoding replaces the categorical feature value with the probability of the target for classification models, or with the expected value of the target for regression models.

Features that have been target encoded might look similar to the following example:

    # Classification model
    +------------------------+----------------------+
    | original value         | target encoded value |
    +------------------------+----------------------+
    | (category_1, target_1) |     0.5              |
    | (category_1, target_2) |     0.5              |
    | (category_2, target_1) |     0.0              |
    +------------------------+----------------------+
    
    # Regression model
    +------------------------+----------------------+
    | original value         | target encoded value |
    +------------------------+----------------------+
    | (category_1, 2)        |     2.5              |
    | (category_1, 3)        |     2.5              |
    | (category_2, 1)        |     1.5              |
    | (category_2, 2)        |     1.5              |
    +------------------------+----------------------+

Target encoding is supported by [boosted tree models](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree) .

## What's next

For more information about supported SQL statements and functions for models that support automatic feature preprocessing, see the following documents:

  - [End-to-end user journeys for ML models](https://docs.cloud.google.com/bigquery/docs/e2e-journey)
  - [End-to-end user journeys for time series forecasting models](https://docs.cloud.google.com/bigquery/docs/e2e-journey-forecast)
