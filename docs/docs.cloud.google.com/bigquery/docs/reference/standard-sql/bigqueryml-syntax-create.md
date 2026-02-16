# The CREATE MODEL statement

To create a model in BigQuery, use the BigQuery ML `  CREATE MODEL  ` statement. This statement is similar to the [`  CREATE TABLE  `](/bigquery/docs/data-definition-language#create_table_statement) DDL statement. When you run a query that contains a `  CREATE MODEL  ` statement, a [query job](/bigquery/docs/managing-jobs) is generated for you that processes the query. You can also use the Google Cloud console user interface to [create a model by using a UI](/bigquery/docs/create-machine-learning-model-console) ( [Preview](https://cloud.google.com/products#product-launch-stages) ).

For more information about supported SQL statements and functions for each model type, see the following documents:

  - [End-to-end user journeys for generative AI models](/bigquery/docs/e2e-journey-genai)
  - [End-to-end user journeys for time series forecasting models](/bigquery/docs/e2e-journey-forecast)
  - [End-to-end user journeys for ML models](/bigquery/docs/e2e-journey)
  - [End-to-end user journeys for imported models](/bigquery/docs/e2e-journey-import)
  - [Contribution analysis user journey](/bigquery/docs/contribution-analysis#contribution_analysis_user_journey)

## Required permissions

  - To create a dataset to store the model, you need the `  bigquery.datasets.create  ` IAM permission.

  - To create a model, you need the following permissions:
    
      - `  bigquery.jobs.create  `
      - `  bigquery.models.create  `
      - `  bigquery.models.getData  `
      - `  bigquery.models.updateData  `
      - `  bigquery.connections.delegate  ` (for remote models)

The following [predefined IAM roles](/bigquery/docs/access-control#bigquery) grant these permissions:

  - [BigQuery Studio Admin](/bigquery/docs/access-control#bigquery.studioAdmin)
  - [BigQuery Admin](/bigquery/docs/access-control#bigquery.admin)

For more information about IAM roles and permissions in BigQuery, see [Introduction to IAM](/bigquery/docs/access-control) .

## `     CREATE MODEL    ` syntax

**Note:** This syntax statement provides a comprehensive list of model types with their model options. When you create a model, use that model specific `  CREATE MODEL  ` statement for convenience. You can view specific `  CREATE MODEL  ` statements by clicking the `  MODEL_TYPE  ` name in the following list, in the table of contents in the left panel, or in the *create model* link in the [End-to-end user journey for each model](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-e2e-journey) .

``` sql
{CREATE MODEL | CREATE MODEL IF NOT EXISTS | CREATE OR REPLACE MODEL}
model_name
[TRANSFORM (select_list)]
[INPUT (field_name field_type)
 OUTPUT (field_name field_type)]
[REMOTE WITH CONNECTION {`connection_name` | DEFAULT}]
[OPTIONS(model_option_list)]
[AS {query_statement |
  (
    training_data AS (query_statement),
    custom_holiday AS (holiday_statement)
  )}]

model_option_list:
    MODEL_TYPE = { 'LINEAR_REG' |
      'LOGISTIC_REG' |
      'KMEANS' |
      'MATRIX_FACTORIZATION' |
      'PCA' |
      'AUTOENCODER' |
      'AUTOML_CLASSIFIER' |
      'AUTOML_REGRESSOR' |
      'BOOSTED_TREE_CLASSIFIER' |
      'BOOSTED_TREE_REGRESSOR' |
      'RANDOM_FOREST_CLASSIFIER' |
      'RANDOM_FOREST_REGRESSOR' |
      'DNN_CLASSIFIER' |
      'DNN_REGRESSOR' |
      'DNN_LINEAR_COMBINED_CLASSIFIER' |
      'DNN_LINEAR_COMBINED_REGRESSOR' |
      'ARIMA_PLUS' |
      'ARIMA_PLUS_XREG' |
      'TENSORFLOW' |
      'TENSORFLOW_LITE' |
      'ONNX' |
      'XGBOOST' |
      'CONTRIBUTION_ANALYSIS'}
    [, MODEL_REGISTRY = { 'VERTEX_AI' } ]
    [, VERTEX_AI_MODEL_ID = string_value ]
    [, VERTEX_AI_MODEL_VERSION_ALIASES = string_array ]
    [, INPUT_LABEL_COLS = string_array ]
    [, MAX_ITERATIONS = int64_value ]
    [, EARLY_STOP = { TRUE | FALSE } ]
    [, MIN_REL_PROGRESS = float64_value ]
    [, DATA_SPLIT_METHOD = { 'AUTO_SPLIT' | 'RANDOM' | 'CUSTOM' | 'SEQ' | 'NO_SPLIT' } ]
    [, DATA_SPLIT_EVAL_FRACTION = float64_value ]
    [, DATA_SPLIT_TEST_FRACTION = float64_value ]
    [, DATA_SPLIT_COL = string_value ]
    [, OPTIMIZE_STRATEGY = { 'AUTO_STRATEGY' | 'BATCH_GRADIENT_DESCENT' | 'NORMAL_EQUATION' } ]
    [, L1_REG = float64_value ]
    [, L2_REG = float64_value ]
    [, LEARN_RATE_STRATEGY = { 'LINE_SEARCH' | 'CONSTANT' } ]
    [, LEARN_RATE = float64_value ]
    [, LS_INIT_LEARN_RATE = float64_value ]
    [, WARM_START = { TRUE | FALSE } ]
    [, AUTO_CLASS_WEIGHTS = { TRUE | FALSE } ]
    [, CLASS_WEIGHTS = struct_array ]
    [, INSTANCE_WEIGHT_COL = string_value ]
    [, NUM_CLUSTERS = int64_value ]
    [, KMEANS_INIT_METHOD = { 'RANDOM' | 'KMEANS++' | 'CUSTOM' } ]
    [, KMEANS_INIT_COL = string_value ]
    [, DISTANCE_TYPE = { 'EUCLIDEAN' | 'COSINE' } ]
    [, STANDARDIZE_FEATURES = { TRUE | FALSE } ]
    [, MODEL_PATH = string_value ]
    [, BUDGET_HOURS = float64_value ]
    [, OPTIMIZATION_OBJECTIVE = { string_value | struct_value } ]
    [, FEEDBACK_TYPE = {'EXPLICIT' | 'IMPLICIT'} ]
    [, NUM_FACTORS = int64_value ]
    [, USER_COL = string_value ]
    [, ITEM_COL = string_value ]
    [, RATING_COL = string_value ]
    [, WALS_ALPHA = float64_value ]
    [, BOOSTER_TYPE = { 'gbtree' | 'dart'} ]
    [, NUM_PARALLEL_TREE = int64_value ]
    [, DART_NORMALIZE_TYPE = { 'tree' | 'forest'} ]
    [, TREE_METHOD = { 'auto' | 'exact' | 'approx' | 'hist'} ]
    [, MIN_TREE_CHILD_WEIGHT = float64_value ]
    [, COLSAMPLE_BYTREE = float64_value ]
    [, COLSAMPLE_BYLEVEL = float64_value ]
    [, COLSAMPLE_BYNODE = float64_value ]
    [, MIN_SPLIT_LOSS = float64_value ]
    [, MAX_TREE_DEPTH = int64_value ]
    [, SUBSAMPLE = float64_value ]
    [, ACTIVATION_FN = { 'RELU' | 'RELU6' | 'CRELU' | 'ELU' | 'SELU' | 'SIGMOID' | 'TANH' } ]
    [, BATCH_SIZE = int64_value ]
    [, DROPOUT = float64_value ]
    [, HIDDEN_UNITS = int_array ]
    [, OPTIMIZER = { 'ADAGRAD' | 'ADAM' | 'FTRL' | 'RMSPROP' | 'SGD' } ]
    [, TIME_SERIES_TIMESTAMP_COL = string_value ]
    [, TIME_SERIES_DATA_COL = string_value ]
    [, TIME_SERIES_ID_COL = { string_value | string_array } ]
    [, HORIZON = int64_value ]
    [, AUTO_ARIMA = { TRUE | FALSE } ]
    [, AUTO_ARIMA_MAX_ORDER = int64_value ]
    [, AUTO_ARIMA_MIN_ORDER = int64_value ]
    [, NON_SEASONAL_ORDER = (int64_value, int64_value, int64_value) ]
    [, DATA_FREQUENCY = { 'AUTO_FREQUENCY' | 'PER_MINUTE' | 'HOURLY' | 'DAILY' | 'WEEKLY' | ... } ]
    [, FORECAST_LIMIT_LOWER_BOUND = float64_value  ]
    [, FORECAST_LIMIT_UPPER_BOUND = float64_value  ]
    [, INCLUDE_DRIFT = { TRUE | FALSE } ]
    [, HOLIDAY_REGION = { 'GLOBAL' | 'NA' | 'JAPAC' | 'EMEA' | 'LAC' | 'AE' | ... } ]
    [, CLEAN_SPIKES_AND_DIPS = { TRUE | FALSE } ]
    [, ADJUST_STEP_CHANGES = { TRUE | FALSE } ]
    [, DECOMPOSE_TIME_SERIES = { TRUE | FALSE } ]
    [, HIERARCHICAL_TIME_SERIES_COLS = { string_array } ]
    [, ENABLE_GLOBAL_EXPLAIN = { TRUE | FALSE } ]
    [, APPROX_GLOBAL_FEATURE_CONTRIB = { TRUE | FALSE }]
    [, INTEGRATED_GRADIENTS_NUM_STEPS = int64_value ]
    [, CALCULATE_P_VALUES = { TRUE | FALSE } ]
    [, FIT_INTERCEPT = { TRUE | FALSE } ]
    [, CATEGORY_ENCODING_METHOD = { 'ONE_HOT_ENCODING' | 'DUMMY_ENCODING' |
      'LABEL_ENCODING' | 'TARGET_ENCODING' } ]
    [, { ENDPOINT = string_value |
      HUGGING_FACE_MODEL_ID = string_value |
      MODEL_GARDEN_MODEL_NAME = string_value} ]
    [, HUGGING_FACE_TOKEN = string_value ]
    [, MACHINE_TYPE = string_value ]
    [, MIN_REPLICA_COUNT = int64_value ]
    [, MAX_REPLICA_COUNT = int64_value ]
    [, RESERVATION_AFFINITY_TYPE = { 'NO_RESERVATION' | 'ANY_RESERVATION' | 'SPECIFIC_RESERVATION' } ]
    [, RESERVATION_AFFINITY_KEY = string_value ]
    [, RESERVATION_AFFINITY_VALUES = string_array ]
    [, ENDPOINT_IDLE_TTL = interval_value ]
    [, REMOTE_SERVICE_TYPE = { 'CLOUD_AI_VISION_V1' | 'CLOUD_AI_NATURAL_LANGUAGE_V1' |
      'CLOUD_AI_TRANSLATE_V3' } ]
    [, XGBOOST_VERSION = { '0.9' | '1.1' } ]
    [, TF_VERSION = { '1.15' | '2.8.0' } ]
    [, NUM_TRIALS = int64_value, ]
    [, MAX_PARALLEL_TRIALS = int64_value ]
    [, HPARAM_TUNING_ALGORITHM = { 'VIZIER_DEFAULT' | 'RANDOM_SEARCH' | 'GRID_SEARCH' } ]
    [, HPARAM_TUNING_OBJECTIVES = { 'R2_SCORE' | 'ROC_AUC' | ... } ]
    [, NUM_PRINCIPAL_COMPONENTS = int64_value ]
    [, PCA_EXPLAINED_VARIANCE_RATIO = float64_value ]
    [, SCALE_FEATURES = { TRUE | FALSE } ]
    [, PCA_SOLVER = { 'FULL' | 'RANDOMIZED' | 'AUTO' } ]
    [, TIME_SERIES_LENGTH_FRACTION = float64_value ]
    [, MIN_TIME_SERIES_LENGTH = int64_value ]
    [, MAX_TIME_SERIES_LENGTH = int64_value ]
    [, TREND_SMOOTHING_WINDOW_SIZE = int64_value ]
    [, SEASONALITIES = string_array ]
    [, PROMPT_COL = string_value ]
    [, LEARNING_RATE_MULTIPLIER = float64_value ]
    [, ACCELERATOR_TYPE = { 'GPU' | 'TPU' } ]
    [, EVALUATION_TASK = { 'TEXT_GENERATION' | 'CLASSIFICATION' | 'SUMMARIZATION' |
      'QUESTION_ANSWERING' | 'UNSPECIFIED' } ]
    [, DOCUMENT_PROCESSOR = string_value ]
    [, SPEECH_RECOGNIZER = string_value ]
    [, KMS_KEY_NAME = string_value ]
    [, CONTRIBUTION_METRIC = string_value ]
    [, DIMENSION_ID_COLS = string_array ]
    [, IS_TEST_COL = string_value ]
    [, MIN_APRIORI_SUPPORT = float64_value ]
    [, PRUNING_METHOD = {'NO_PRUNING', 'PRUNE_REDUNDANT_INSIGHTS'}  ]
    [, TOP_K_INSIGHTS_BY_APRIORI_SUPPORT = int64_value ]
```

### `     CREATE MODEL    `

Creates and trains a new model in the specified dataset. If the model name exists, `  CREATE MODEL  ` returns an error.

### `     CREATE MODEL IF NOT EXISTS    `

Creates and trains a new model only if the model does not exist in the specified dataset.

### `     CREATE OR REPLACE MODEL    `

Creates and trains a model and replaces an existing model with the same name in the specified dataset.

### `     model_name    `

`  model_name  ` is the name of the model you're creating or replacing. The model name must be unique per dataset: no other model or table can have the same name. The model name must follow the same naming rules as a BigQuery table. A model name can:

  - Contain up to 1,024 characters
  - Contain letters (upper or lower case), numbers, and underscores

`  model_name  ` is case-sensitive.

If you don't have a default project configured, prepend the project ID to the model name in following format, including backticks: ``  `[PROJECT_ID].[DATASET].[MODEL]`  `` ; for example, ``  `myproject.mydataset.mymodel`  `` .

### `     TRANSFORM    `

TRANSFORM lets you specify all preprocessing during model creation and have it automatically applied during prediction and evaluation.

For example, you can create the following model:

``` text
CREATE OR REPLACE MODEL `myproject.mydataset.mymodel`
  TRANSFORM(ML.FEATURE_CROSS(STRUCT(f1, f2)) as cross_f,
            ML.QUANTILE_BUCKETIZE(f3) OVER() as buckets,
            label_col)
  OPTIONS(model_type='linear_reg', input_label_cols=['label_col'])
AS SELECT * FROM t
```

During prediction, you don't need to preprocess the input again, and the same transformations are automatically restored:

``` text
SELECT * FROM ML.PREDICT(MODEL `myproject.mydataset.mymodel`, (SELECT f1, f2, f3 FROM table))
```

When the `  TRANSFORM  ` clause is present, only output columns from the `  TRANSFORM  ` clause are used in training. Any results from `  query_statement  ` that don't appear in the `  TRANSFORM  ` clause are ignored.

The input columns of the `  TRANSFORM  ` clause are the result of `  query_statement  ` . So, the final input used in training is the set of columns generated by the following query:

``` text
SELECT (select_list) FROM (query_statement);
```

Input columns of the `  TRANSFORM  ` clause can be of any SIMPLE type or ARRAY of SIMPLE type. SIMPLE types are non-STRUCT and non-ARRAY data types.

In prediction ( `  ML.PREDICT  ` ), users only need to pass in the original columns from the `  query_statement  ` that are used inside the `  TRANSFORM  ` clause. The columns dropped in `  TRANSFORM  ` don't need to be provided during prediction. `  TRANSFORM  ` is automatically applied to the input data during prediction, including the statistics used in ML analytic functions (for example, `  ML.QUANTILE_BUCKETIZE  ` ).

To learn more about feature preprocessing, see [Feature preprocessing overview](/bigquery/docs/preprocess-overview) , or try the [Feature Engineering Functions](https://github.com/GoogleCloudPlatform/bigquery-ml-utils/blob/master/notebooks/bqml-preprocessing-functions.ipynb) notebook.

To try using the `  TRANSFORM  ` clause, try the [Use the BigQuery ML `  TRANSFORM  ` clause for feature engineering](/bigquery/docs/bigqueryml-transform) tutorial or the [Create Model With Inline Transpose](https://github.com/GoogleCloudPlatform/bigquery-ml-utils/blob/master/notebooks/bqml-feature-engineering.ipynb) notebook.

### `     select_list    `

You can pass columns from `  query_statement  ` through to model training without transformation by either using `  *  ` , `  * EXCEPT()  ` , or by listing the column names directly.

Not all columns from `  query_statement  ` are required to appear in the `  TRANSFORM  ` clause, so you can drop columns appearing in `  query_statement  ` by omitting them from the `  TRANSFORM  ` clause.

You can transform inputs from `  query_statement  ` by using expressions in `  select_list  ` . `  select_list  ` is similar to a normal `  SELECT  ` statement. `  select_list  ` supports the following syntax:

  - `  *  `
  - `  * EXCEPT()  `
  - `  * REPLACE()  `
  - `  expression  `
  - `  expression.*  `

The following cannot appear inside `  select_list  ` :

  - Aggregation functions.
  - Non-BigQuery ML analytic functions. For more information about supported functions, see [Manual feature preprocessing](/bigquery/docs/manual-preprocessing) .
  - UDFs.
  - Subqueries.
  - Anonymous columns. For example, `  a + b as c  ` is allowed, while `  a + b  ` isn't.

The output columns of `  select_list  ` can be of any BigQuery supported data type.

If present, the following columns must appear in `  select_list  ` without transformation:

  - `  label  `
  - `  data_split_col  `
  - `  kmeans_init_col  `
  - `  instance_weight_col  `

If these columns are returned by `  query_statement  ` , you must reference them in `  select_list  ` by column name outside of any expression, or by using `  *  ` . You can't use aliases with these columns.

### `     INPUT    ` and `     OUTPUT    `

`  INPUT  ` and `  OUTPUT  ` clauses are used to specify input and output format for [remote models](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model) or [XGBoost models](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-xgboost) .

#### `     field_name    `

For remote models, `  INPUT  ` and `  OUTPUT  ` field names must be identical as the field names of the Vertex AI endpoint request and response. See examples in [remote model `  INPUT  ` and `  OUTPUT  ` clause](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-https#in-out-clause) .

For XGBoost models, `  INPUT  ` field names must be identical to the names in the `  feature_names  ` field if `  feature_names  ` field is populated in the XGBoost model file. See [XGBoost INPUT OUTPUT clause](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-xgboost#input_output_clause) for more details.

#### `     field_type    `

[Remote models](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-https) support the following BigQuery data types for `  INPUT  ` and `  OUTPUT  ` clauses:

  - Simple type: [BOOL](/bigquery/docs/reference/standard-sql/data-types#boolean_type) , [INT64](/bigquery/docs/reference/standard-sql/data-types#integer_types) , [FLOAT64](/bigquery/docs/reference/standard-sql/data-types#floating_point_types) , [NUMERIC](/bigquery/docs/reference/standard-sql/data-types#decimal_types) , [BIGNUMERIC](/bigquery/docs/reference/standard-sql/data-types#decimal_types) , [STRING](/bigquery/docs/reference/standard-sql/data-types#string_type)
  - [ARRAY](/bigquery/docs/reference/standard-sql/data-types#array_type) \<Simple type\>

[XGBoost models](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-xgboost) only support [numeric types](/bigquery/docs/reference/standard-sql/data-types#numeric_types) for the `  INPUT  ` field type and [`  FLOAT64  `](/bigquery/docs/reference/standard-sql/data-types#floating_point_types) for the `  OUTPUT  ` field type.

### `     connection_name    `

BigQuery uses a `  CLOUD_RESOURCE  ` [connection](/bigquery/docs/create-cloud-resource-connection) to interact with your Vertex AI endpoint. You need to grant [Vertex AI User role](/vertex-ai/docs/general/access-control#aiplatform.user) to connection's service account on your Vertex AI endpoint project.

See examples in [remote model `  CONNECTION  ` statement](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model#connection) .

To use a [default connection](/bigquery/docs/default-connections) , specify specify `  DEFAULT  ` instead of the connection name.

### `     model_option_list    `

`  CREATE MODEL  ` supports the following options:

#### `     MODEL_TYPE    `

**Syntax**

``` text
MODEL_TYPE = { 'LINEAR_REG' | 'LOGISTIC_REG' | 'KMEANS' | 'PCA' |
'MATRIX_FACTORIZATION' | 'AUTOENCODER' | 'AUTOML_REGRESSOR' |
'AUTOML_CLASSIFIER' | 'BOOSTED_TREE_CLASSIFIER' | 'BOOSTED_TREE_REGRESSOR' |
'RANDOM_FOREST_CLASSIFIER' | 'RANDOM_FOREST_REGRESSOR' |
'DNN_CLASSIFIER' | 'DNN_REGRESSOR' | 'DNN_LINEAR_COMBINED_CLASSIFIER' |
'DNN_LINEAR_COMBINED_REGRESSOR' | 'ARIMA_PLUS' | 'ARIMA_PLUS_XREG' |
'TENSORFLOW' | 'TENSORFLOW_LITE' | 'ONNX' | 'XGBOOST' | 'CONTRIBUTION_ANALYSIS'}
```

**Description**

Specify the model type. This argument is required.

**Arguments**

The argument is in the model type column.

Model category

Model type

Description

Model specific CREATE MODEL statement

Regression

`  'LINEAR_REG'  `

Linear regression for real-valued label prediction; for example, the sales of an item on a given day.

[CREATE MODEL statement for generalized linear models](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm)

`  'BOOSTED_TREE_REGRESSOR'  `

Create a boosted tree regressor model using the XGBoost library.

[CREATE MODEL statement for boosted tree models](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree)

`  'RANDOM_FOREST_REGRESSOR'  `

Create a random forest regressor model using the XGBoost library.

[CREATE MODEL statement for random forest models](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-random-forest)

`  'DNN_REGRESSOR'  `

Create a Deep Neural Network Regressor model.

[CREATE MODEL statement for DNN models](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-dnn-models)

`  'DNN_LINEAR_COMBINED_REGRESSOR'  `

Create a Wide-and-Deep Regressor model.

[CREATE MODEL statement for Wide-and-Deep models](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-wnd-models)

`  'AUTOML_REGRESSOR'  `

Create a regression model using AutoML.

[CREATE MODEL statement for AutoML models](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-automl)

Classification

`  'LOGISTIC_REG'  `

Logistic regression for binary-class or multi-class classification; for example, determining whether a customer will make a purchase.

[CREATE MODEL statement for generalized linear models](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm)

`  'BOOSTED_TREE_CLASSIFIER'  `

Create a boosted tree classifier model using the XGBoost library.

[CREATE MODEL statement for boosted tree models](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree)

`  'RANDOM_FOREST_CLASSIFIER'  `

Create a random forest classifier model using the XGBoost library.

[CREATE MODEL statement for random forest models](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-random-forest)

`  'DNN_CLASSIFIER'  `

Create a Deep Neural Network Classifier model.

[CREATE MODEL statement for DNN models](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-dnn-models)

`  'DNN_LINEAR_COMBINED_CLASSIFIER'  `

Create a Wide-and-Deep Classifier model.

[CREATE MODEL statement for Wide-and-Deep models](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-wnd-models)

`  'AUTOML_CLASSIFIER'  `

Create a classification model using AutoML.

[CREATE MODEL statement for AutoML models](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-automl)

Clustering

`  'KMEANS'  `

K-means clustering for data segmentation; for example, identifying customer segments.

[CREATE MODEL statement for K-means models](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-kmeans)

Collaborative Filtering

`  'MATRIX_FACTORIZATION'  `

Matrix factorization for recommendation systems. For example, given a set of users, items, and some ratings for a subset of the items, creates a model to predict a user's rating for items they have not rated.

[CREATE MODEL statement for matrix factorization models](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-matrix-factorization)

Dimensionality Reduction

`  'PCA'  `

Principal component analysis for dimensionality reduction.

[CREATE MODEL statement for PCA models](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-pca)

`  'AUTOENCODER'  `

Create an Autoencoder model for anomaly detection, dimensionality reduction, and embedding purposes.

[CREATE MODEL statement for Autoencoder model](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-autoencoder)

Time series forecasting

`  'ARIMA_PLUS'  ` (previously `  'ARIMA'  ` )

Univariate time-series forecasting with many modeling components under the hood such as ARIMA model for the trend, STL and ETS for seasonality, and holiday effects.

[CREATE MODEL statement for time series models](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series)

`  'ARIMA_PLUS_XREG'  `

Multivariate time-series forecasting using linear regression and ARIMA\_PLUS as the underlying techniques.

[CREATE MODEL statement for time series models](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-multivariate-time-series)

Augmented analytics

`  'CONTRIBUTION_ANALYSIS'  `

Create a contribution analysis model to find key drivers of a change.

[CREATE MODEL statement for Contribution Analysis](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-contribution-analysis)

Importing models

`  'TENSORFLOW'  `

Create a model by importing a TensorFlow model into BigQuery.

[CREATE MODEL statement for TensorFlow models](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-tensorflow)

`  'TENSORFLOW_LITE'  `

Create a model by importing a TensorFlow Lite model into BigQuery.

[CREATE MODEL statement for TensorFlow Lite models](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-tflite)

`  'ONNX'  `

Create a model by importing an ONNX model into BigQuery.

[CREATE MODEL statement for ONNX models](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-onnx)

`  'XGBOOST'  `

Create a model by importing a XGBoost model into BigQuery.

[CREATE MODEL statement for XGBoost models](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-xgboost)

Remote models

N/A

Create a model by specifying a Cloud AI service, or the endpoint for a Vertex AI model.

[CREATE MODEL statement for remote models over Google models in Vertex AI](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model)  
  
[CREATE MODEL statement for remote models over hosted models in Vertex AI](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-https)  
  
[CREATE MODEL statement for remote models over Cloud AI services](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-service)

**Note:** We are deprecating `  ARIMA  ` as the model type. While the model training pipelines of `  ARIMA  ` and `  ARIMA_PLUS  ` are the same, `  ARIMA_PLUS  ` supports more capabilities, including support for a new training option, [`  DECOMPOSE_TIME_SERIES  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create#decompose_time_series) , and table-valued functions including [`  ML.ARIMA_EVALUATE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-arima-evaluate) and [`  ML.EXPLAIN_FORECAST  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-explain-forecast) .

#### Other model options

The following table provides a comprehensive list of model options, with a brief descriptions and their applicable model types. You can find detailed description in the model specific `  CREATE MODEL  ` statement by clicking the model type in the "Applied model types" column.

When the applied model types are supervised learning models, unless "regressor" or "classifier" is explicitly listed, it means that model options apply to both the regressor and the classifier. For example, the "boosted tree" means that model option applies to both boosted tree regressor and boosted tree classifier, while the "boosted tree classifier" only applies to the classifier.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Name</th>
<th>Description</th>
<th>Applied model types</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>MODEL_REGISTRY</td>
<td>The MODEL_REGISTRY option specifies the Model Registry destination.</td>
<td>All model types are supported.</td>
</tr>
<tr class="even">
<td>VERTEX_AI_MODEL_ID</td>
<td>The Vertex AI model ID to register the model with.</td>
<td>All model types are supported.</td>
</tr>
<tr class="odd">
<td>VERTEX_AI_MODEL_VERSION_ALIASES</td>
<td>The Vertex AI model alias to register the model with.</td>
<td>All model types are supported.</td>
</tr>
<tr class="even">
<td>INPUT_LABEL_COLS</td>
<td>The label column names in the training data.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm#input_label_cols">Linear &amp; logistic regression</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree#input_label_cols">Boosted trees</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-random-forest#input_label_cols">Random forest</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-dnn-models#input_label_cols">DNN</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-wnd-models#input_label_cols">Wide &amp; Deep</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-automl#input_label_cols">AutoML</a></td>
</tr>
<tr class="odd">
<td>MAX_ITERATIONS</td>
<td>The maximum number of training iterations or steps.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm#max_iterations">Linear &amp; logistic regression</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree#max_iterations">Boosted trees</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-dnn-models#max_iterations">DNN</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-wnd-models#max_iterations">Wide &amp; Deep</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-kmeans#max_iterations">Kmeans</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-matrix-factorization#max_iterations">Matrix factorization</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-autoencoder#max_iterations">Autoencoder</a></td>
</tr>
<tr class="even">
<td>EARLY_STOP</td>
<td>Whether training should stop after the first iteration in which the relative loss improvement is less than the value specified for `MIN_REL_PROGRESS`.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm#early_stop">Linear &amp; logistic regression</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree#early_stop">Boosted trees</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-random-forest#early_stop">Random forest</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-dnn-models#early_stop">DNN</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-wnd-models#early_stop">Wide &amp; Deep</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-kmeans#early_stop">Kmeans</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-matrix-factorization#early_stop">Matrix factorization</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-autoencoder#early_stop">Autoencoder</a></td>
</tr>
<tr class="odd">
<td>MIN_REL_PROGRESS</td>
<td>The minimum relative loss improvement that is necessary to continue training when `EARLY_STOP` is set to true.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm#min_rel_progress">Linear &amp; logistic regression</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree#min_rel_progress">Boosted trees</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-random-forest#min_rel_progress">Random forest</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-dnn-models#min_rel_progress">DNN</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-wnd-models#min_rel_progress">Wide &amp; Deep</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-kmeans#min_rel_progress">Kmeans</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-matrix-factorization#min_rel_progress">Matrix factorization</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-autoencoder#min_rel_progress">Autoencoder</a></td>
</tr>
<tr class="even">
<td>DATA_SPLIT_METHOD</td>
<td>The method to split input data into training and evaluation sets when not running hyperparameter tuning, or into training, evaluation, and test sets when running hyperparameter tuning.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm#data_split_method">Linear &amp; logistic regression</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree#data_split_method">Boosted trees</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-random-forest#data_split_method">Random forest</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-dnn-models#data_split_method">DNN</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-wnd-models#data_split_method">Wide &amp; Deep</a><br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-matrix-factorization#data_split_method">Matrix factorization</a></td>
</tr>
<tr class="odd">
<td>DATA_SPLIT_EVAL_FRACTION</td>
<td>Specifies the fraction of the data used for evaluation. Accurate to two decimal places.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm#data_split_eval_fraction">Linear &amp; logistic regression</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree#data_split_eval_fraction">Boosted trees</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-random-forest#data_split_eval_fraction">Random forest</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-dnn-models#data_split_eval_fraction">DNN</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-wnd-models#data_split_eval_fraction">Wide &amp; Deep</a><br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-matrix-factorization#data_split_eval_fraction">Matrix factorization</a></td>
</tr>
<tr class="even">
<td>DATA_SPLIT_TEST_FRACTION</td>
<td>Specifies the fraction of the data used for testing when you are running hyperparameter tuning. Accurate to two decimal places.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm#data_split_test_fraction">Linear &amp; logistic regression</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree#data_split_test_fraction">Boosted trees</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-random-forest#data_split_test_fraction">Random forest</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-dnn-models#data_split_test_fraction">DNN</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-wnd-models#data_split_test_fraction">Wide &amp; Deep</a><br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-matrix-factorization#data_split_test_fraction">Matrix factorization</a></td>
</tr>
<tr class="odd">
<td>DATA_SPLIT_COL</td>
<td>Identifies the column used to split the data.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm#data_split_col">Linear &amp; logistic regression</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree#data_split_col">Boosted trees</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-random-forest#data_split_col">Random forest</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-dnn-models#data_split_col">DNN</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-wnd-models#data_split_col">Wide &amp; Deep</a><br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-matrix-factorization#data_split_col">Matrix factorization</a></td>
</tr>
<tr class="even">
<td>OPTIMIZE_STRATEGY</td>
<td>The strategy to train linear regression models.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm#optimize_strategy">Linear regression</a></td>
</tr>
<tr class="odd">
<td>L1_REG</td>
<td>The amount of <a href="https://developers.google.com/machine-learning/glossary/#L1_regularization">L1 regularization</a> applied.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm#l1_reg">Linear &amp; logistic regression</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree#l1_reg">Boosted trees</a><br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-random-forest#l1_reg">Random forest</a></td>
</tr>
<tr class="even">
<td>L2_REG</td>
<td>The amount of <a href="https://developers.google.com/machine-learning/glossary/#L2_regularization">L2 regularization</a> applied.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm#l2_reg">Linear &amp; logistic regression</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree#l2_reg">Boosted trees</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-random-forest#l2_reg">Random forest</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-matrix-factorization#l2_reg">Matrix factorization</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-multivariate-time-series#l2_reg">ARIMA_PLUS_XREG</a></td>
</tr>
<tr class="odd">
<td>LEARN_RATE_STRATEGY</td>
<td>The strategy for specifying the <a href="https://developers.google.com/machine-learning/glossary/#learning_rate">learning rate</a> during training.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm#learn_rate_strategy">Linear &amp; logistic regression</a></td>
</tr>
<tr class="even">
<td>LEARN_RATE</td>
<td>The learn rate for <a href="https://developers.google.com/machine-learning/glossary/#gradient_descent">gradient descent</a> when LEARN_RATE_STRATEGY is set to CONSTANT.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm#learn_rate">Linear &amp; logistic regression</a></td>
</tr>
<tr class="odd">
<td>LS_INIT_LEARN_RATE</td>
<td>Sets the initial learning rate that LEARN_RATE_STRATEGY=LINE_SEARCH uses.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm#ls_init_learn_rate">Linear &amp; logistic regression</a></td>
</tr>
<tr class="even">
<td>WARM_START</td>
<td>Retrain a model with new training data, new model options, or both.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm#warm_start">Linear &amp; logistic regression</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-dnn-models#warm_start">DNN</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-wnd-models#warm_start">Wide &amp; Deep</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-kmeans#warm_start">Kmeans</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-autoencoder#warm_start">Autoencoder</a></td>
</tr>
<tr class="odd">
<td>AUTO_CLASS_WEIGHTS</td>
<td>Whether to balance class labels using weights for each class in inverse proportion to the frequency of that class.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm#auto_class_weights">Logistic regression</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree#auto_class_weights">Boosted tree classifier</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-random-forest#auto_class_weights">Random forest classifier</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-dnn-models#auto_class_weights">DNN classifier</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-wnd-models#auto_class_weights">Wide &amp; Deep classifier</a></td>
</tr>
<tr class="even">
<td>CLASS_WEIGHTS</td>
<td>The weights to use for each class label. This option cannot be specified if AUTO_CLASS_WEIGHTS is specified.<br />
<br />
It takes an ARRAY of STRUCTs; each STRUCT is a (STRING, FLOAT64) pair representing a class label and the corresponding weight.<br />
<br />
A weight must be present for every class label. The weights are not required to add up to one. For example: CLASS_WEIGHTS = [STRUCT('example_label', .2)].</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm#class_weights">Logistic regression</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree#class_weights">Boosted tree classifier</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-random-forest#class_weights">Random forest classifier</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-dnn-models#class_weights">DNN classifier</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-wnd-models#class_weights">Wide &amp; Deep classifier</a></td>
</tr>
<tr class="odd">
<td>INSTANCE_WEIGHT_COL</td>
<td>Identifies the column used to specify the weights for each data point in the training dataset.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree#instance_weight_col">Boosted trees</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-random-forest#instance_weight_col">Random forest</a></td>
</tr>
<tr class="even">
<td>NUM_CLUSTERS</td>
<td>The number of clusters to identify in the input data.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-kmeans#num_clusters">Kmeans</a></td>
</tr>
<tr class="odd">
<td>KMEANS_INIT_METHOD</td>
<td>The method of initializing the clusters.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-kmeans#kmeans_init_method">Kmeans</a></td>
</tr>
<tr class="even">
<td>KMEANS_INIT_COL</td>
<td>Identifies the column used to initialize the centroids.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-kmeans#kmeans_init_col">Kmeans</a></td>
</tr>
<tr class="odd">
<td>DISTANCE_TYPE</td>
<td>The type of metric to compute the distance between two points.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-kmeans#distance_type">K-means</a></td>
</tr>
<tr class="even">
<td>STANDARDIZE_FEATURES</td>
<td>Whether to <a href="https://en.wikipedia.org/wiki/Feature_scaling">standardize numerical features</a> .</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-kmeans#standardize_features">Kmeans</a></td>
</tr>
<tr class="odd">
<td>BUDGET_HOURS</td>
<td>Sets the training budget hours.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-automl#budget_hours">AutoML</a></td>
</tr>
<tr class="even">
<td>OPTIMIZATION_OBJECTIVE</td>
<td>Sets the optimization objective function to use for AutoML.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-automl#optimization_objective">AutoML</a></td>
</tr>
<tr class="odd">
<td>MODEL_PATH</td>
<td>Specifies the location of the imported model to import.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-tensorflow#model_path">Imported TensorFlow model</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-tflite#model_path">Imported TensorFlow lite model</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-onnx#model_path">Imported ONNX model</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-xgboost#model_path">Imported XGBoost model</a></td>
</tr>
<tr class="even">
<td>FEEDBACK_TYPE</td>
<td>Specifies feedback type for matrix factorization models which changes the algorithm that is used during training.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-matrix-factorization#feedback_type">Matrix factorization</a></td>
</tr>
<tr class="odd">
<td>NUM_FACTORS</td>
<td>Specifies the number of latent factors.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-matrix-factorization#num_factors">Matrix factorization</a></td>
</tr>
<tr class="even">
<td>USER_COL</td>
<td>The user column name.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-matrix-factorization#user_col">Matrix factorization</a></td>
</tr>
<tr class="odd">
<td>ITEM_COL</td>
<td>The item column name.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-matrix-factorization#item_col">Matrix factorization</a></td>
</tr>
<tr class="even">
<td>RATING_COL</td>
<td>The rating column name.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-matrix-factorization#rating_col">Matrix factorization</a></td>
</tr>
<tr class="odd">
<td>WALS_ALPHA</td>
<td>A hyperparameter for matrix factorization models with IMPLICIT feedback.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-matrix-factorization#wals_alpha">Matrix factorization</a></td>
</tr>
<tr class="even">
<td>BOOSTER_TYPE</td>
<td>For boosted tree models, specify the booster type to use, with default value GBTREE.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree#booster_type">Boosted trees</a></td>
</tr>
<tr class="odd">
<td>NUM_PARALLEL_TREE</td>
<td>Number of parallel trees constructed during each iteration.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree#num_parallel_tree">Boosted trees</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-random-forest#num_parallel_tree">Random forest</a></td>
</tr>
<tr class="even">
<td>DART_NORMALIZE_TYPE</td>
<td>Type of normalization algorithm for DART booster.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree#dart_normalize_type">Boosted trees</a></td>
</tr>
<tr class="odd">
<td>TREE_METHOD</td>
<td>Type of tree construction algorithm.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree#tree_method">Boosted trees</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-random-forest#tree_method">Random forest</a></td>
</tr>
<tr class="even">
<td>MIN_TREE_CHILD_WEIGHT</td>
<td>Minimum sum of instance weight needed in a child for further partitioning.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree#min_tree_child_weight">Boosted trees</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-random-forest#min_tree_child_weight">Random forest</a></td>
</tr>
<tr class="odd">
<td>COLSAMPLE_BYTREE</td>
<td>Subsample ratio of columns when constructing each tree. Subsampling occurs once for every tree constructed.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree#colsample_bytree">Boosted trees</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-random-forest#colsample_bytree">Random forest</a></td>
</tr>
<tr class="even">
<td>COLSAMPLE_BYLEVEL</td>
<td>Subsample ratio of columns for each level. Subsampling occurs once for every new depth level reached in a tree.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree#colsample_bylevel">Boosted trees</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-random-forest#colsample_bylevel">Random forest</a></td>
</tr>
<tr class="odd">
<td>COLSAMPLE_BYNODE</td>
<td>Subsample ratio of columns for each node (split). Subsampling occurs once every time a new split is evaluated.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree#colsample_bynode">Boosted trees</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-random-forest#colsample_bynode">Random forest</a></td>
</tr>
<tr class="even">
<td>MIN_SPLIT_LOSS</td>
<td>Minimum loss reduction required to make a further partition on a leaf node of the tree.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree#min_split_loss">Boosted trees</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-random-forest#min_split_loss">Random forest</a></td>
</tr>
<tr class="odd">
<td>MAX_TREE_DEPTH</td>
<td>Maximum depth of a tree.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree#max_tree_depth">Boosted trees</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-random-forest#max_tree_depth">Random forest</a></td>
</tr>
<tr class="even">
<td>SUBSAMPLE</td>
<td>Subsample ratio of the training instances.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree#subsample">Boosted trees</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-random-forest#subsample">Random forest</a></td>
</tr>
<tr class="odd">
<td>ACTIVATION_FN</td>
<td>Specifies the activation function of the neural network.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-dnn-models#activation_fn">DNN</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-wnd-models#activation_fn">Wide &amp; Deep</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-autoencoder#activation_fn">Autoencoder</a></td>
</tr>
<tr class="even">
<td>BATCH_SIZE</td>
<td>Specifies the mini batch size of samples that are fed to the neural network.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-dnn-models#batch_size">DNN</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-wnd-models#batch_size">Wide &amp; Deep</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-autoencoder#batch_size">Autoencoder</a></td>
</tr>
<tr class="odd">
<td>DROPOUT</td>
<td>Specifies the dropout rate of units in the neural network.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-dnn-models#dropout">DNN</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-wnd-models#dropout">Wide &amp; Deep</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-autoencoder#dropout">Autoencoder</a></td>
</tr>
<tr class="even">
<td>HIDDEN_UNITS</td>
<td>Specifies the hidden layers of the neural network.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-dnn-models#hidden_units">DNN</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-wnd-models#hidden_units">Wide &amp; Deep</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-autoencoder#hidden_units">Autoencoder</a></td>
</tr>
<tr class="odd">
<td>OPTIMIZER</td>
<td>Specifies the optimizer for training the model.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-dnn-models#optimizer">DNN</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-wnd-models#optimizer">Wide &amp; Deep</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-autoencoder#optimizer">Autoencoder</a></td>
</tr>
<tr class="even">
<td>TIME_SERIES_TIMESTAMP_COL</td>
<td>The timestamp column name for time series models.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series#time_series_timestamp_col">ARIMA_PLUS</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-multivariate-time-series#time_series_timestamp_col">ARIMA_PLUS_XREG</a></td>
</tr>
<tr class="odd">
<td>TIME_SERIES_DATA_COL</td>
<td>The data column name for time series models.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series#time_series_data_col">ARIMA_PLUS</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-multivariate-time-series#time_series_data_col">ARIMA_PLUS_XREG</a></td>
</tr>
<tr class="even">
<td>TIME_SERIES_ID_COL</td>
<td>The ID column names for time-series models.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series#time_series_id_col">ARIMA_PLUS</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-multivariate-time-series#horizon">ARIMA_PLUS_XREG</a></td>
</tr>
<tr class="odd">
<td>HORIZON</td>
<td>The number of time points to forecast. When forecasting multiple time series at once, this parameter applies to each time series.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series#horizon">ARIMA_PLUS</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-multivariate-time-series#horizon">ARIMA_PLUS_XREG</a></td>
</tr>
<tr class="even">
<td>AUTO_ARIMA</td>
<td>Whether the training process should use auto.ARIMA or not.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series#auto_arima">ARIMA_PLUS</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-multivariate-time-series#auto_arima">ARIMA_PLUS_XREG</a></td>
</tr>
<tr class="odd">
<td>AUTO_ARIMA_MAX_ORDER</td>
<td>The maximum value for the sum of non-sesonal p and q. It controls the parameter search space in the auto.ARIMA algorithm.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series#auto_arima_max_order">ARIMA_PLUS</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-multivariate-time-series#auto_arima_max_order">ARIMA_PLUS_XREG</a></td>
</tr>
<tr class="even">
<td>AUTO_ARIMA_MIN_ORDER</td>
<td>The minimum value for the sum of non-sesonal p and q. It controls the parameter search space in the auto.ARIMA algorithm.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series#auto_arima_min_order">ARIMA_PLUS</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-multivariate-time-series#auto_arima_min_order">ARIMA_PLUS_XREG</a></td>
</tr>
<tr class="odd">
<td>NON_SEASONAL_ORDER</td>
<td>The tuple of non-seasonal p, d, and q for the ARIMA_PLUS model.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series#non_seasonal_order">ARIMA_PLUS</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-multivariate-time-series#non_seasonal_order">ARIMA_PLUS_XREG</a></td>
</tr>
<tr class="even">
<td>DATA_FREQUENCY</td>
<td>The data frequency of the input time series.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series#data_frequency">ARIMA_PLUS</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-multivariate-time-series#data_frequency">ARIMA_PLUS_XREG</a></td>
</tr>
<tr class="odd">
<td>FORECAST_LIMIT_LOWER_BOUND</td>
<td>The lower bound of the time series forecasting values.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series#forecast_limit_lower_bound">ARIMA_PLUS</a></td>
</tr>
<tr class="even">
<td>FORECAST_LIMIT_UPPER_BOUND</td>
<td>The upper bound of the time series forecasting values.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series#forecast_limit_upper_bound">ARIMA_PLUS</a></td>
</tr>
<tr class="odd">
<td>INCLUDE_DRIFT</td>
<td>Should the ARIMA_PLUS model include a linear drift term or not.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series#include_drift">ARIMA_PLUS</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-multivariate-time-series#include_drift">ARIMA_PLUS_XREG</a></td>
</tr>
<tr class="even">
<td>HOLIDAY_REGION</td>
<td>The geographical region based on which the holiday effect is applied in modeling.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series#holiday_region">ARIMA_PLUS</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-multivariate-time-series#holiday_region">ARIMA_PLUS_XREG</a></td>
</tr>
<tr class="odd">
<td>CLEAN_SPIKES_AND_DIPS</td>
<td>Whether the spikes and dips should be cleaned.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series#clean_spikes_and_dips">ARIMA_PLUS</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-multivariate-time-series#clean_spikes_and_dips">ARIMA_PLUS_XREG</a></td>
</tr>
<tr class="even">
<td>ADJUST_STEP_CHANGES</td>
<td>Whether the step changes should be adjusted.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series#adjust_step_changes">ARIMA_PLUS</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-multivariate-time-series#adjust_step_changes">ARIMA_PLUS_XREG</a></td>
</tr>
<tr class="odd">
<td>DECOMPOSE_TIME_SERIES</td>
<td>Whether the separate components of both the history and the forecast parts of the time series (such as seasonal components) should be saved.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series#decompose_time_series">ARIMA_PLUS</a></td>
</tr>
<tr class="even">
<td>HIERARCHICAL_TIME_SERIES_COLS</td>
<td>The column names used to generate hierarchical time series forecasts. The column order represents the hierarchy structure.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series#hierarchical_time_series_cols">ARIMA_PLUS</a></td>
</tr>
<tr class="odd">
<td>ENABLE_GLOBAL_EXPLAIN</td>
<td>Specifies whether to compute global explanations using explainable AI to evaluate global feature importance to the model.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm#enable_global_explain">Linear &amp; logistic regression</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree#enable_global_explain">Boosted trees</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-random-forest#enable_global_explain">Random forest</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-dnn-models#enable_global_explain">DNN</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-wnd-models#enable_global_explain">Wide &amp; Deep</a></td>
</tr>
<tr class="even">
<td>APPROX_GLOBAL_FEATURE_CONTRIB</td>
<td>Specifies whether to use fast approximation for feature contribution computation.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree#approx_global_feature_contrib">Boosted trees</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-random-forest#approx_global_feature_contrib">Random forest</a></td>
</tr>
<tr class="odd">
<td>INTEGRATED_GRADIENTS_NUM_STEPS</td>
<td>Specifies the number of steps to sample between the example being explained and its baseline for approximating the integral in integrated gradients attribution methods.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-dnn-models#integrated_gradients_num_steps">DNN</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-wnd-models#integrated_gradients_num_steps">Wide &amp; Deep</a></td>
</tr>
<tr class="even">
<td>CALCULATE_P_VALUES</td>
<td>Specifies whether to compute p-values for the model during training.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm#calculate_p_values">Linear &amp; logistic regression</a></td>
</tr>
<tr class="odd">
<td>FIT_INTERCEPT</td>
<td>Specifies whether to fit an intercept for the model during training.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm#fit_intercept">Linear &amp; logistic regression</a></td>
</tr>
<tr class="even">
<td>CATEGORY_ENCODING_METHOD</td>
<td>Specifies the default encoding method for categorical features.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm#category_encoding_method">Linear &amp; logistic regression</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree#category_encoding_method">Boosted trees</a></td>
</tr>
<tr class="odd">
<td>ENDPOINT</td>
<td>Specifies the Vertex AI endpoint to use for a remote model. This can be the name of a Google model in Vertex AI or the HTTPS endpoint of a model deployed to Vertex AI.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model#endpoint">Remote models over Google models in Vertex AI</a><br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-https#endpoint">Remote models over hosted models in Vertex AI</a><br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-open#manually-deployed">Remote models over open models</a></td>
</tr>
<tr class="even">
<td>HUGGING_FACE_MODEL_ID</td>
<td>Specifies the model ID for a supported Hugging Face model.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-open#automatically-deployed">Remote models over open models</a></td>
</tr>
<tr class="odd">
<td>MODEL_GARDEN_MODEL_NAME</td>
<td>Specifies the model ID and model version of a supported Vertex AI Model Garden model.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-open#automatically-deployed">Remote models over open models</a></td>
</tr>
<tr class="even">
<td>HUGGING_FACE_TOKEN</td>
<td>Specifies the Hugging Face User Access Token to use.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-open#automatically-deployed">Remote models over open models</a></td>
</tr>
<tr class="odd">
<td>MACHINE_TYPE</td>
<td>Specifies the machine type to use when deploying the model to Vertex AI.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-open#automatically-deployed">Remote models over open models</a></td>
</tr>
<tr class="even">
<td>MIN_REPLICA_COUNT</td>
<td>Specifies the minimum number of machine replicas used when deploying the model to Vertex AI.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-open#automatically-deployed">Remote models over open models</a></td>
</tr>
<tr class="odd">
<td>MAX_REPLICA_COUNT</td>
<td>Specifies the maximum number of machine replicas used when deploying the model to Vertex AI.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-open#automatically-deployed">Remote models over open models</a></td>
</tr>
<tr class="even">
<td>RESERVATION_AFFINITY_TYPE</td>
<td>Determines whether the deployed model uses Compute Engine reservations to provide assured virtual machine (VM) availability when serving predictions, and specifies whether the model uses VMs from all available reservations or just one specific reservation.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-open#automatically-deployed">Remote models over open models</a></td>
</tr>
<tr class="odd">
<td>RESERVATION_AFFINITY_KEY</td>
<td>The key for a Compute Engine reservation.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-open#automatically-deployed">Remote models over open models</a></td>
</tr>
<tr class="even">
<td>RESERVATION_AFFINITY_VALUES</td>
<td>Specifies the full resource name of the Compute Engine reservation.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-open#automatically-deployed">Remote models over open models</a></td>
</tr>
<tr class="odd">
<td>ENDPOINT_IDLE_TTL</td>
<td>Specifies the duration of inactivity after which a BigQuery-managed Vertex AI model is automatically undeployed from a Vertex AI endpoint.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-open#automatically-deployed">Remote models over open models</a></td>
</tr>
<tr class="even">
<td>REMOTE_SERVICE_TYPE</td>
<td>Specifies the Cloud AI service to use for a remote model.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-service#remote_service_type">Remote models over Cloud AI services</a></td>
</tr>
<tr class="odd">
<td>XGBOOST_VERSION</td>
<td>Specifies the Xgboost version for model training.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree#xgboost_version">Boosted trees</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-random-forest#xgboost_version">Random forest</a></td>
</tr>
<tr class="even">
<td>TF_VERSION</td>
<td>Specifies the TensorFlow (TF) version for model training.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-dnn-models#tf_version">DNN</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-wnd-models#tf_version">Wide &amp; Deep</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-autoencoder#tf_version">Autoencoder</a></td>
</tr>
<tr class="odd">
<td>NUM_TRIALS</td>
<td>Specifies the maximum number of submodels to train when you are running hyperparameter tuning.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm#num_trials">Linear &amp; logistic regression</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree#num_trials">Boosted trees</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-random-forest#num_trials">Random forest</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-dnn-models#num_trials">DNN</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-wnd-models#num_trials">Wide &amp; Deep</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-kmeans#num_trials">Kmeans</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-matrix-factorization#num_trials">Matrix factorization</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-autoencoder#num_trials">Autoencoder</a></td>
</tr>
<tr class="even">
<td>MAX_PARALLEL_TRIALS</td>
<td>Specifies the maximum number of trials to run at the same time when you are running hyperparameter tuning.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm#max_parallel_trials">Linear &amp; logistic regression</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree#max_parallel_trials">Boosted trees</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-random-forest#max_parallel_trials">Random forest</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-dnn-models#max_parallel_trials">DNN</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-wnd-models#max_parallel_trials">Wide &amp; Deep</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-kmeans#max_parallel_trials">Kmeans</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-matrix-factorization#max_parallel_trials">Matrix factorization</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-autoencoder#max_parallel_trials">Autoencoder</a></td>
</tr>
<tr class="odd">
<td>HPARAM_TUNING_ALGORITHM</td>
<td>Specifies the algorithm used to tune the hyperparameters when you are running hyperparameter tuning.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm#hparam_tuning_algorithm">Linear &amp; logistic regression</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree#hparam_tuning_algorithm">Boosted trees</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-random-forest#hparam_tuning_algorithm">Random forest</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-dnn-models#hparam_tuning_algorithm">DNN</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-wnd-models#hparam_tuning_algorithm">Wide &amp; Deep</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-kmeans#hparam_tuning_algorithm">Kmeans</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-matrix-factorization#hparam_tuning_algorithm">Matrix factorization</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-autoencoder#hparam_tuning_algorithm">Autoencoder</a></td>
</tr>
<tr class="even">
<td>HPARAM_TUNING_OBJECTIVES</td>
<td>Specifies the hyperparameter tuning objective for the model.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm#hparam_tuning_objectives">Linear &amp; logistic regression</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree#hparam_tuning_objectives">Boosted trees</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-random-forest#hparam_tuning_objectives">Random forest</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-dnn-models#hparam_tuning_objectives">DNN</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-wnd-models#hparam_tuning_objectives">Wide &amp; Deep</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-kmeans#hparam_tuning_objectives">Kmeans</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-matrix-factorization#hparam_tuning_objectives">Matrix factorization</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-autoencoder#hparam_tuning_objectives">Autoencoder</a></td>
</tr>
<tr class="odd">
<td>NUM_PRINCIPAL_COMPONENTS</td>
<td>The number of principal components to keep.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-pca#num_principal_components">PCA</a></td>
</tr>
<tr class="even">
<td>PCA_EXPLAINED_VARIANCE_RATIO</td>
<td>The ratio for the explained variance.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-pca#pca_explained_variance_ratio">PCA</a></td>
</tr>
<tr class="odd">
<td>SCALE_FEATURES</td>
<td>Determines whether or not to scale the numerical features to unit variance.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-pca#scale_features">PCA</a></td>
</tr>
<tr class="even">
<td>PCA_SOLVER</td>
<td>The solver to use to calculate the principal components.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-pca#pca_solver">PCA</a></td>
</tr>
<tr class="odd">
<td>TIME_SERIES_LENGTH_FRACTION</td>
<td>The fraction of the interpolated length of the time series that's used to model the time series trend component.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series#time_series_length_fraction">ARIMA_PLUS</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-multivariate-time-series#time_series_length_fraction">ARIMA_PLUS_XREG</a></td>
</tr>
<tr class="even">
<td>MIN_TIME_SERIES_LENGTH</td>
<td>The minimum number of time points that are used in modeling the trend component of the time series.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series#min_time_series_length">ARIMA_PLUS</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-multivariate-time-series#min_time_series_length">ARIMA_PLUS_XREG</a></td>
</tr>
<tr class="odd">
<td>MAX_TIME_SERIES_LENGTH</td>
<td>The maximum number of time points that are used in modeling the trend component of the time series.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series#max_time_series_length">ARIMA_PLUS</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-multivariate-time-series#max_time_series_length">ARIMA_PLUS_XREG</a></td>
</tr>
<tr class="even">
<td>TREND_SMOOTHING_WINDOW_SIZE</td>
<td>The smoothing window size for the trend component.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series#trend_smoothing_window_size">ARIMA_PLUS</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-multivariate-time-series#trend_smoothing_window_size">ARIMA_PLUS_XREG</a></td>
</tr>
<tr class="odd">
<td>SEASONALITIES</td>
<td>The seasonality of the time series data refers to the presence of variations that occur at certain regular intervals such as weekly, monthly or quarterly.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series#seasonalities">ARIMA_PLUS</a></td>
</tr>
<tr class="even">
<td>PROMPT_COL</td>
<td>The name of the prompt column in the training data table to use when performing supervised tuning.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-tuned#prompt_col">Remote models over Google models in Vertex AI</a></td>
</tr>
<tr class="odd">
<td>LEARNING_RATE_MULTIPLIER</td>
<td>A multiplier to apply to the recommended learning rate when performing supervised tuning.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-tuned#learning_rate_multiplier">Remote models over Google models in Vertex AI</a></td>
</tr>
<tr class="even">
<td>EVALUATION_TASK</td>
<td>When performing supervised tuning, the type of task that you want to tune the model to perform.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-tuned#evaluation_task">Remote models over Google models in Vertex AI</a></td>
</tr>
<tr class="odd">
<td>DOCUMENT_PROCESSOR</td>
<td>Identifies the document processor to use when the REMOTE_SERVICE_TYPE option value is <code dir="ltr" translate="no">       CLOUD_AI_DOCUMENT_V1      </code> .</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-service#document_processor">Remote models over Cloud AI services</a></td>
</tr>
<tr class="even">
<td>SPEECH_RECOGNIZER</td>
<td>Identifies the speech recognizer to use when the REMOTE_SERVICE_TYPE option value is <code dir="ltr" translate="no">       CLOUD_AI_SPEECH_TO_TEXT_V2      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-service#speech_recognizer">Remote models over Cloud AI services</a></td>
</tr>
<tr class="odd">
<td>KMS_KEY_NAME</td>
<td>Specifies the Cloud Key Management Service <a href="/kms/docs/cmek">customer-managed encryption key (CMEK)</a> to use to encrypt the model.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm#kms_key_name">Linear &amp; logistic regression</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree#kms_key_name">Boosted trees</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-random-forest#kms_key_name">Random forest</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-dnn-models#kms_key_name">DNN</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-wnd-models#kms_key_name">Wide &amp; Deep</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-automl#kms_key_name">AutoML</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-kmeans#kms_key_name">K-means</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-pca#kms_key_name">PCA</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-autoencoder#kms_key_name">Autoencoder</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-matrix-factorization#kms_key_name">Matrix factorization</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series#kms_key_name">ARIMA_PLUS</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-multivariate-time-series#kms_key_name">ARIMA_PLUS_XREG</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-onnx#kms_key_name">ONNX</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-tensorflow#kms_key_name">TensorFlow</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-tflite#kms_key_name">TensorFlow Lite</a> ,<br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-xgboost#kms_key_name">XGBoost</a></td>
</tr>
<tr class="even">
<td>CONTRIBUTION_METRIC</td>
<td>The expression to use when performing contribution analysis.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-contribution-analysis#contribution_metric">Contribution analysis</a></td>
</tr>
<tr class="odd">
<td>DIMENSION_ID_COLS</td>
<td>The names of the columns to use as dimensions when summarizing the contribution analysis metric.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-contribution-analysis#dimension_id_cols">Contribution analysis</a></td>
</tr>
<tr class="even">
<td>IS_TEST_COL</td>
<td>The name of the column to use to determine whether a given row is test data or control data.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-contribution-analysis#is_test_col">Contribution analysis</a></td>
</tr>
<tr class="odd">
<td>MIN_APRIORI_SUPPORT</td>
<td>The minimum apriori support threshold for including segments in the model output.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-contribution-analysis#min_apriori_support">Contribution analysis</a></td>
</tr>
<tr class="even">
<td>TOP_K_INSIGHTS_BY_APRIORI_SUPPORT</td>
<td>The number of top insights by apriori support to include in the model output.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-contribution-analysis#top_k_insights_by_apriori_support">Contribution analysis</a></td>
</tr>
<tr class="odd">
<td>PRUNING_METHOD</td>
<td>The pruning method to use for the contribution analysis model.</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-contribution-analysis#pruning_method">Contribution analysis</a></td>
</tr>
</tbody>
</table>

### `     AS    `

All model types support the following `  AS  ` clause syntax for specifying the training data:

``` googlesql
AS query_statement
```

For time series forecasting models that have a `  DATA_FREQUENCY  ` value of either `  DAILY  ` or `  AUTO_FREQUENCY  ` , you can optionally use the following `  AS  ` clause syntax to perform [custom holiday modeling](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series#custom_holidays) in addition to specifying the training data:

``` googlesql
AS (
  training_data AS (query_statement),
  custom_holiday AS (holiday_statement)
)
```

#### `     query_statement    `

The `  query_statement  ` argument specifies the query that is used to generate the training data. For information about the supported SQL syntax of the `  query_statement  ` clause, see [GoogleSQL query syntax](/bigquery/docs/reference/standard-sql/query-syntax#sql_syntax) .

#### `     holiday_statement    `

The `  holiday_statement  ` argument specifies the query that provides custom holiday modeling information for time series forecast models. This query must return 50,000 rows or less and must contain the following columns:

  - `  region  ` : Required. A `  STRING  ` value that identifies the region to target for holiday modeling. Use one of the following options:
    
      - An upper-case [holiday region code](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series#holiday_region) . Use this option to overwrite or supplement the holidays for the specified region. You can see the holidays for a region by running `  SELECT * FROM bigquery-public-data.ml_datasets.holidays_and_events_for_forecasting WHERE region = region  ` .
      - An arbitrary string. Use this option to specify a custom region that you want to model holidays for. For example, you could specify `  London  ` if you are only modeling holidays for that city.
    
    Be sure not to use an existing holiday region code when you are trying to model for a custom region. For example, if you want to model a holiday in California, and specify `  CA  ` as the `  region  ` value, the service recognizes that as the holiday region code for Canada and targets that region. Because the argument is case-sensitive, you could specify `  ca  ` , `  California  ` , or some other value that isn't a holiday region code.

  - `  holiday_name  ` : Required. A `  STRING  ` value that identifies the holiday to target for holiday modeling. Use one of the following options:
    
      - The holiday name as it is represented in the `  bigquery-public-data.ml_datasets.holidays_and_events_for_forecasting  ` public table, including case. Use this option to [overwrite](#change_the_metadata_for_built-in_holidays) or [supplement](#supplement_built-in_holidays_with_additional_custom_holidays) the specified holiday.
      - A string that represents a custom holiday. The string must be a valid column name so that it can be used in `  ML.EXPLAIN_FORECAST  ` output. For example, it cannot contain space. For more information on column naming, see [Column names](/bigquery/docs/schemas#column_names) .

  - `  primary_date  ` : Required. A `  DATE  ` value that specifies the date the holiday falls on.

  - `  preholiday_days  ` : Optional. An `  INT64  ` value that specifies the start of the holiday window around the holiday that is taken into account when modeling. Must be greater than or equal to `  1  ` . Defaults to `  1  ` .

  - `  postholiday_days  ` : Optional. An `  INT64  ` value that specifies the end of the holiday window around the holiday that is taken into account when modeling. Must be greater than or equal to `  1  ` . Defaults to `  1  ` .

The `  preholiday_days  ` and `  postholiday_days  ` arguments together describe the holiday window around the holiday that is taken into account when modeling. The holiday window is defined as `  [primary_date - preholiday_days, primary_date + postholiday_days]  ` and is inclusive of the pre- and post-holiday days. The value for each holiday window must be less than or equal to `  30  ` and must be the same across the given holiday. For example, if you are modeling Arbor Day for several different years, you must specify the same holiday window for all of those years.

To achieve the best holiday modeling result, provide as much historical and forecast information about the occurrences of each included holiday as possible. For example, if you have time series data from 2018 to 2022 and would like to forecast for 2023, you get the best result by providing the custom holiday information for all of those years, similar to the following:

``` text
CREATE OR REPLACE MODEL `mydataset.arima_model`
  OPTIONS (
    model_type = 'ARIMA_PLUS',
    holiday_region = 'US',...) AS (
        training_data AS (SELECT * FROM `mydataset.timeseries_data`),
        custom_holiday AS (
            SELECT
              'US' AS region,
              'Halloween' AS holiday_name,
              primary_date,
              5 AS preholiday_days,
              1 AS postholiday_days
            FROM
              UNNEST(
                [
                  DATE('2018-10-31'),
                  DATE('2019-10-31'),
                  DATE('2020-10-31'),
                  DATE('2021-10-31'),
                  DATE('2022-10-31'),
                  DATE('2023-10-31')])
                AS primary_date
          )
      )
```

## Supported inputs

The `  CREATE MODEL  ` statement supports the following data types for input label, data split columns and input feature columns.

### Supported input feature types

See [Supported input feature types](/bigquery/docs/reference/standard-sql/bigqueryml-input-feature-types) for BigQuery ML supported input feature types.

### Supported data types for input label columns

BigQuery ML supports different GoogleSQL data types depending on the model type. Supported data types for `  input_label_cols  ` include:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       Model type      </code></th>
<th><code dir="ltr" translate="no">       Supported label types      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       regression models      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/data-types#integer_types"><code dir="ltr" translate="no">        INT64       </code></a><br />
<a href="/bigquery/docs/reference/standard-sql/data-types#numeric_type"><code dir="ltr" translate="no">        NUMERIC       </code></a><br />
<a href="/bigquery/docs/reference/standard-sql/data-types#bignumeric_type"><code dir="ltr" translate="no">        BIGNUMERIC       </code></a><br />
<a href="/bigquery/docs/reference/standard-sql/data-types#floating_point_types"><code dir="ltr" translate="no">        FLOAT64       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       classification models      </code></td>
<td>Any <a href="/bigquery/docs/reference/standard-sql/data-types#data_type_properties">groupable</a> data type</td>
</tr>
</tbody>
</table>

### Supported data types for data split columns

BigQuery ML supports different GoogleSQL data types depending on the data split method. Supported data types for `  data_split_col  ` include:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><code dir="ltr" translate="no">       Data split method      </code></th>
<th><code dir="ltr" translate="no">       Supported column types      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       CUSTOM      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/data-types#boolean_type"><code dir="ltr" translate="no">        BOOL       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       SEQ      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/data-types#integer_types"><code dir="ltr" translate="no">        INT64       </code></a><br />
<a href="/bigquery/docs/reference/standard-sql/data-types#numeric_type"><code dir="ltr" translate="no">        NUMERIC       </code></a><br />
<a href="/bigquery/docs/reference/standard-sql/data-types#bignumeric_type"><code dir="ltr" translate="no">        BIGNUMERIC       </code></a><br />
<a href="/bigquery/docs/reference/standard-sql/data-types#floating_point_types"><code dir="ltr" translate="no">        FLOAT64       </code></a><br />
<a href="/bigquery/docs/reference/standard-sql/data-types#timestamp_type"><code dir="ltr" translate="no">        TIMESTAMP       </code></a></td>
</tr>
</tbody>
</table>

## Limitations

`  CREATE MODEL  ` statements must comply with the following rules:

  - Only one `  CREATE  ` statement is allowed.
  - When you use a `  CREATE MODEL  ` statement, the size of the model must be 90 MB or less or the query fails. Generally, if all categorical variables are short strings, a total feature cardinality (model dimension) of 5-10 million is supported. The dimensionality is dependent on the cardinality and length of the string variables.
  - The label column cannot contain `  NULL  ` values. If the label column contains `  NULL  ` values, then the query fails.
  - The `  CREATE MODEL IF NOT EXISTS  ` clause always updates the last modified timestamp of a model.
  - Query statements used in the `  CREATE MODEL  ` statement cannot contain `  EXTERNAL_QUERY  ` . If you want to use `  EXTERNAL_QUERY  ` , then [materialize the query result](/bigquery/docs/reference/standard-sql/data-definition-language#create_table_statement) and then use the `  CREATE MODEL  ` statement with the newly created table.

## Quotas

Troubleshoot quota for `  CREATE MODEL  ` statements.

### Maximum number of `     CREATE MODEL    ` statements

This error means that you have exceeded the quota for `  CREATE MODEL  ` statements.

**Error message**

``` text
Quota exceeded: Your project exceeded quota for CREATE MODEL queries per
 project.
```

#### Resolution

If you exceed the [quota](/bigquery/quotas#create_model_statements) for `  CREATE MODEL  ` statements, send an email to <bqml-feedback@google.com> and request a quota increase.
