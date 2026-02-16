# Automatic feature preprocessing

BigQuery ML performs automatic preprocessing during training by using the [`  CREATE MODEL  ` statement](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create) . Automatic preprocessing consists of [missing value imputation](/bigquery/docs/auto-preprocessing#imputation) and [feature transformations](/bigquery/docs/auto-preprocessing#feature-transform) .

For information about feature preprocessing support in BigQuery ML, see [Feature preprocessing overview](/bigquery/docs/preprocess-overview) .

## Missing data imputation

In statistics, imputation is used to replace missing data with substituted values. When you train a model in BigQuery ML, `  NULL  ` values are treated as missing data. When you predict outcomes in BigQuery ML, missing values can occur when BigQuery ML encounters a `  NULL  ` value or a previously unseen value. BigQuery ML handles missing data differently, based on the type of data in the column.

<table>
<thead>
<tr class="header">
<th>Column type</th>
<th>Imputation method</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Numeric</td>
<td>In both training and prediction, <code dir="ltr" translate="no">       NULL      </code> values in numeric columns are replaced with the mean value of the given column, as calculated by the feature column in the original input data.</td>
</tr>
<tr class="even">
<td>One-hot/Multi-hot encoded</td>
<td>In both training and prediction, <code dir="ltr" translate="no">       NULL      </code> values in the encoded columns are mapped to an additional category that is added to the data. Previously unseen data is assigned a weight of 0 during prediction.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code> columns use a mixture of imputation methods from both standardized and one-hot encoded columns. For the generated Unix time column, BigQuery ML replaces values with the mean Unix time across the original columns. For other generated values, BigQuery ML assigns them to the respective <code dir="ltr" translate="no">       NULL      </code> category for each extracted feature.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       STRUCT      </code></td>
<td>In both training and prediction, each field of the <code dir="ltr" translate="no">       STRUCT      </code> is imputed according to its type.</td>
</tr>
</tbody>
</table>

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
<td><a href="/bigquery/docs/reference/standard-sql/data-types#integer_types"><code dir="ltr" translate="no">        INT64       </code></a><br />
<a href="/bigquery/docs/reference/standard-sql/data-types#numeric_type"><code dir="ltr" translate="no">        NUMERIC       </code></a><br />
<a href="/bigquery/docs/reference/standard-sql/data-types#bignumeric_type"><code dir="ltr" translate="no">        BIGNUMERIC       </code></a><br />
<a href="/bigquery/docs/reference/standard-sql/data-types#floating_point_types"><code dir="ltr" translate="no">        FLOAT64       </code></a></td>
<td><a href="https://en.wikipedia.org/wiki/Feature_scaling#Standardization">Standardization</a></td>
<td>For most models, BigQuery ML standardizes and centers numerical columns at zero before passing it into training. The exceptions are boosted tree and random forest models, for which no standardization occurs, and k-means models, where the <code dir="ltr" translate="no">       STANDARDIZE_FEATURES      </code> option controls whether numerical features are standardized.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/data-types#boolean_type"><code dir="ltr" translate="no">        BOOL       </code></a><br />
<a href="/bigquery/docs/reference/standard-sql/data-types#string_type"><code dir="ltr" translate="no">        STRING       </code></a><br />
<a href="/bigquery/docs/reference/standard-sql/data-types#bytes_type"><code dir="ltr" translate="no">        BYTES       </code></a><br />
<a href="/bigquery/docs/reference/standard-sql/data-types#date_type"><code dir="ltr" translate="no">        DATE       </code></a><br />
<a href="/bigquery/docs/reference/standard-sql/data-types#datetime_type"><code dir="ltr" translate="no">        DATETIME       </code></a><br />
<a href="/bigquery/docs/reference/standard-sql/data-types#time_type"><code dir="ltr" translate="no">        TIME       </code></a></td>
<td><a href="https://developers.google.com/machine-learning/glossary/#one-hot_encoding">One-hot encoded</a></td>
<td>For all non-numerical, non-array columns other than <code dir="ltr" translate="no">       TIMESTAMP      </code> , BigQuery ML performs a one-hot encoding transformation for all models other than boosted tree and random forest models. This transformation generates a separate feature for each unique value in the column. Label encoding transformation is applied to train boosted tree and random forest models to convert each unique value into a numerical value.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/data-types#array_type"><code dir="ltr" translate="no">        ARRAY       </code></a></td>
<td>Multi-hot encoded</td>
<td>For all non-numerical <code dir="ltr" translate="no">       ARRAY      </code> columns, BigQuery ML performs a multi-hot encoding transformation. This transformation generates a separate feature for each unique element in the <code dir="ltr" translate="no">       ARRAY      </code> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/data-types#timestamp_type"><code dir="ltr" translate="no">        TIMESTAMP       </code></a></td>
<td>Timestamp transformation</td>
<td>When a linear or logistic regression model encounters a <code dir="ltr" translate="no">       TIMESTAMP      </code> column, it extracts a set of components from the <code dir="ltr" translate="no">       TIMESTAMP      </code> and performs a mix of standardization and one-hot encoding on the extracted components. For the Unix epoch time in seconds component, BigQuery ML uses standardization. For all other components, it uses one-hot encoding.<br />
<br />
For more information, see the following <a href="/bigquery/docs/auto-preprocessing#timestamp-transform">timestamp feature transformation table</a> .</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/data-types#struct_type"><code dir="ltr" translate="no">        STRUCT       </code></a></td>
<td>Struct expansion</td>
<td>When BigQuery ML encounters a <code dir="ltr" translate="no">       STRUCT      </code> column, it expands the fields inside the <code dir="ltr" translate="no">       STRUCT      </code> to create a single column. It requires all fields of <code dir="ltr" translate="no">       STRUCT      </code> to be named. Nested <code dir="ltr" translate="no">       STRUCT      </code> s are not allowed. The column names after expansion are in the format of <code dir="ltr" translate="no">       {struct_name}_{field_name}      </code> .</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/data-types#array_type"><code dir="ltr" translate="no">        ARRAY       </code></a> of <a href="/bigquery/docs/reference/standard-sql/data-types#struct_type"><code dir="ltr" translate="no">        STRUCT       </code></a></td>
<td>No transformation</td>
<td></td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/data-types#array_type"><code dir="ltr" translate="no">        ARRAY       </code></a> of <a href="/bigquery/docs/reference/standard-sql/data-types#numeric_types"><code dir="ltr" translate="no">        NUMERIC       </code></a></td>
<td>No transformation</td>
<td></td>
</tr>
</tbody>
</table>

### `     TIMESTAMP    ` feature transformation

The following table shows the components extracted from `  TIMESTAMP  ` columns and the corresponding transformation method.

<table>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       TIMESTAMP      </code> component</th>
<th><code dir="ltr" translate="no">       processed_input      </code> result</th>
<th>Transformation method</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Unix epoch time in seconds</td>
<td><code dir="ltr" translate="no">       [COLUMN_NAME]      </code></td>
<td>Standardization</td>
</tr>
<tr class="even">
<td>Day of month</td>
<td><code dir="ltr" translate="no">       _TS_DOM_[COLUMN_NAME]      </code></td>
<td>One-hot encoding</td>
</tr>
<tr class="odd">
<td>Day of week</td>
<td><code dir="ltr" translate="no">       _TS_DOW_[COLUMN_NAME]      </code></td>
<td>One-hot encoding</td>
</tr>
<tr class="even">
<td>Month of year</td>
<td><code dir="ltr" translate="no">       _TS_MOY_[COLUMN_NAME]      </code></td>
<td>One-hot encoding</td>
</tr>
<tr class="odd">
<td>Hour of day</td>
<td><code dir="ltr" translate="no">       _TS_HOD_[COLUMN_NAME]      </code></td>
<td>One-hot encoding</td>
</tr>
<tr class="even">
<td>Minute of hour</td>
<td><code dir="ltr" translate="no">       _TS_MOH_[COLUMN_NAME]      </code></td>
<td>One-hot encoding</td>
</tr>
<tr class="odd">
<td>Week of year (weeks begin on Sunday)</td>
<td><code dir="ltr" translate="no">       _TS_WOY_[COLUMN_NAME]      </code></td>
<td>One-hot encoding</td>
</tr>
<tr class="even">
<td>Year</td>
<td><code dir="ltr" translate="no">       _TS_YEAR_[COLUMN_NAME]      </code></td>
<td>One-hot encoding</td>
</tr>
</tbody>
</table>

## Category feature encoding

For features that are one-hot encoded, you can specify a different default encoding method by using the model option `  CATEGORY_ENCODING_METHOD  ` . For generalized linear models (GLM) models, you can set `  CATEGORY_ENCODING_METHOD  ` to one of the following values:

  - [`  ONE_HOT_ENCODING  `](#one_hot_encoding)
  - [`  DUMMY_ENCODING  `](#dummy_encoding)
  - [`  LABEL_ENCODING  `](#label_encoding)
  - [`  TARGET_ENCODING  `](#dummy_encoding)

### One-hot encoding

One-hot encoding maps each category that a feature has to its own binary feature, where `  0  ` represents the absence of the feature and `  1  ` represents the presence (known as a *dummy variable* ). This mapping creates `  N  ` new feature columns, where `  N  ` is the number of unique categories for the feature across the training table.

For example, suppose your training table has a feature column that's called `  fruit  ` with the categories `  Apple  ` , `  Banana  ` , and `  Cranberry  ` , such as the following:

<table>
<thead>
<tr class="header">
<th>Row</th>
<th>fruit</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>1</td>
<td>Apple</td>
</tr>
<tr class="even">
<td>2</td>
<td>Banana</td>
</tr>
<tr class="odd">
<td>3</td>
<td>Cranberry</td>
</tr>
</tbody>
</table>

In this case, the `  CATEGORY_ENCODING_METHOD='ONE_HOT_ENCODING'  ` option transforms the table to the following internal representation:

<table>
<thead>
<tr class="header">
<th>Row</th>
<th>fruit_Apple</th>
<th>fruit_Banana</th>
<th>fruit_Cranberry</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>1</td>
<td>1</td>
<td>0</td>
<td>0</td>
</tr>
<tr class="even">
<td>2</td>
<td>0</td>
<td>1</td>
<td>0</td>
</tr>
<tr class="odd">
<td>3</td>
<td>0</td>
<td>0</td>
<td>1</td>
</tr>
</tbody>
</table>

One-hot encoding is supported by [linear and logistic regression](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm) and [boosted tree](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree) models.

### Dummy encoding

[Dummy encoding](https://en.wikiversity.org/wiki/Dummy_variable_\(statistics\)) is similar to one-hot encoding, where a categorical feature is transformed into a set of placeholder variables. Dummy encoding uses `  N-1  ` placeholder variables instead of `  N  ` placeholder variables to represent `  N  ` categories for a feature. For example, if you set `  CATEGORY_ENCODING_METHOD  ` to `  'DUMMY_ENCODING'  ` for the same `  fruit  ` feature column shown in the preceding one-hot encoding example, then the table is transformed to the following internal representation:

<table>
<thead>
<tr class="header">
<th>Row</th>
<th>fruit_Apple</th>
<th>fruit_Banana</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>1</td>
<td>1</td>
<td>0</td>
</tr>
<tr class="even">
<td>2</td>
<td>0</td>
<td>1</td>
</tr>
<tr class="odd">
<td>3</td>
<td>0</td>
<td>0</td>
</tr>
</tbody>
</table>

The category with the most occurrences in the training dataset is dropped. When multiple categories have the most occurrences, a random category within that set is dropped.

The final set of weights from [`  ML.WEIGHTS  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-weights) still includes the dropped category, but its weight is always `  0.0  ` . For [`  ML.ADVANCED_WEIGHTS  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-advanced-weights) , the standard error and p-value for the dropped variable is `  NaN  ` .

If `  warm_start  ` is used on a model that was initially trained with `  'DUMMY_ENCODING'  ` , the same placeholder variable is dropped from the first training run. Models cannot change encoding methods between training runs.

Dummy encoding is supported by [linear and logistic regression models](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm) .

### Label encoding

Label encoding transforms the value of a categorical feature to an `  INT64  ` value in `  [0, <number of categories>]  ` .

For example, if you had a book dataset like the following:

<table>
<thead>
<tr class="header">
<th>Title</th>
<th>Genre</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Book 1</td>
<td>Fantasy</td>
</tr>
<tr class="even">
<td>Book 2</td>
<td>Cooking</td>
</tr>
<tr class="odd">
<td>Book 3</td>
<td>History</td>
</tr>
<tr class="even">
<td>Book 4</td>
<td>Cooking</td>
</tr>
</tbody>
</table>

The label encoded values might look similar to the following:

<table>
<thead>
<tr class="header">
<th>Title</th>
<th>Genre (text)</th>
<th>Genre (numeric)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Book 1</td>
<td>Fantasy</td>
<td>1</td>
</tr>
<tr class="even">
<td>Book 2</td>
<td>Cooking</td>
<td>2</td>
</tr>
<tr class="odd">
<td>Book 3</td>
<td>History</td>
<td>3</td>
</tr>
<tr class="even">
<td>Book 4</td>
<td>Cooking</td>
<td>2</td>
</tr>
</tbody>
</table>

The encoding vocabulary is sorted alphabetically. `  NULL  ` values and categories that aren't in the vocabulary are encoded to `  0  ` .

Label encoding is supported by [boosted tree models](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree) .

### Target encoding

Target encoding replaces the categorical feature value with the probability of the target for classification models, or with the expected value of the target for regression models.

Features that have been target encoded might look similar to the following example:

``` text
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
```

Target encoding is supported by [boosted tree models](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree) .

## What's next

For more information about supported SQL statements and functions for models that support automatic feature preprocessing, see the following documents:

  - [End-to-end user journeys for ML models](/bigquery/docs/e2e-journey)
  - [End-to-end user journeys for time series forecasting models](/bigquery/docs/e2e-journey-forecast)
