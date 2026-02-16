# Hyperparameter tuning overview

In machine learning, hyperparameter tuning identifies a set of optimal hyperparameters for a learning algorithm. A hyperparameter is a model argument whose value is set before the learning process begins. By contrast, the values of other parameters such as coefficients of a linear model are learned.

Hyperparameter tuning lets you spend less time manually iterating hyperparameters and more time focusing on exploring insights from data.

You can specify hyperparameter tuning options for the following model types:

  - [Linear and logistic regression](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm)
  - [K-means](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-kmeans)
  - [Matrix factorization](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-matrix-factorization)
  - [Autoencoder](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-autoencoder)
  - [Boosted trees](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree)
  - [Random forest](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-random-forest)
  - [Deep neural network (DNN)](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-dnn-models)
  - [Wide & Deep network](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-wnd-models)

For these types of models, hyperparameter tuning is enabled when you specify a value for the [`  NUM_TRIALS  ` option](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create#num_trials) in the [`  CREATE MODEL  ` statement](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create) .

To try running hyperparameter tuning on a linear regression model, see [Use the BigQuery ML hyperparameter tuning to improve model performance](/bigquery/docs/hyperparameter-tuning-tutorial) .

The following models also support hyperparameter tuning but don't allow you to specify particular values:

  - [AutoML Tables models](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-automl) have automatic hyperparameter tuning embedded in the model training by default.
  - [ARIMA\_PLUS models](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series) let you set the [`  AUTO_ARIMA  ` argument](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series#auto_arima) to perform hyperparameter tuning using the auto.ARIMA algorithm. This algorithm performs hyperparameter tuning for the trend module. Hyperparameter tuning isn't supported for the entire [modeling pipeline](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series#modeling-pipeline) .

## Locations

For information about which locations support hyperparameter tuning, see [BigQuery ML locations](/bigquery/docs/locations#bqml-loc) .

## Set hyperparameters

To tune a hyperparameter, you must specify a range of values for that hyperparameter that the model can use for a set of trials. You can do this by using one of the following keywords when setting the hyperparameter in the `  CREATE MODEL  ` statement, instead of providing a single value:

  - `  HPARAM_RANGE  ` : A two-element `  ARRAY(FLOAT64)  ` value that defines the minimum and maximum bounds of the search space of continuous values for a hyperparameter. Use this option to specify a range of values for a hyperparameter, for example `  LEARN_RATE = HPARAM_RANGE(0.0001, 1.0)  ` .

  - `  HPARAM_CANDIDATES  ` : A `  ARRAY(STRUCT)  ` value that specifies the set of discrete values for the hyperparameter. Use this option to specify a set of values for a hyperparameter, for example `  OPTIMIZER = HPARAM_CANDIDATES(['ADAGRAD', 'SGD', 'FTRL'])  ` .

## Hyperparameters and objectives

The following table lists the supported hyperparameters and objectives for each model type that supports hyperparameter tuning:

Model type

Hyperparameter objectives

Hyperparameter

Valid range

Default range

Scale type

`  LINEAR_REG  `

`  MEAN_ABSOLUTE_ERROR  `  
  
`  MEAN_SQUARED_ERROR  `  
  
`  MEAN_SQUARED_LOG_ERROR  `  
  
`  MEDIAN_ABSOLUTE_ERROR  `  
  
`  R2_SCORE  ` (default)  
  
`  EXPLAINED_VARIANCE  `

`  L1_REG  `  
  
`  L2_REG  `

`  (0, ∞]  `  
  
`  (0, ∞]  `

`  (0, 10]  `  
  
`  (0, 10]  `

`  LOG  `  
  
`  LOG  `

`  LOGISTIC_REG  `

`  PRECISION  `  
  
`  RECALL  `  
  
`  ACCURACY  `  
  
`  F1_SCORE  `  
  
`  LOG_LOSS  `  
  
`  ROC_AUC  ` (default)

`  L1_REG  `  
  
`  L2_REG  `

`  (0, ∞]  `  
  
`  (0, ∞]  `

`  (0, 10]  `  
  
`  (0, 10]  `

`  LOG  `  
  
`  LOG  `

`  KMEANS  `

`  DAVIES_BOULDIN_INDEX  `

`  NUM_CLUSTERS  `

`  [2, 100]  `

`  [2, 10]  `

`  LINEAR  `

`  MATRIX_ FACTORIZATION  ` (explicit)

`  MEAN_SQUARED_ERROR  `

`  NUM_FACTORS  `  
  
`  L2_REG  `

`  [2, 200]  `  
  
`  (0, ∞)  `

`  [2, 20]  `  
  
`  (0, 10]  `

`  LINEAR  `  
  
`  LOG  `

`  MATRIX_ FACTORIZATION  ` (implicit)

`  MEAN_AVERAGE_PRECISION  ` (default)  
  
`  MEAN_SQUARED_ERROR  `  
  
`  NORMALIZED_DISCOUNTED_CUMULATIVE_GAIN  `  
  
`  AVERAGE_RANK  `

`  NUM_FACTORS  `  
  
`  L2_REG  `  
  
`  WALS_ALPHA  `

`  [2, 200]  `  
  
`  (0, ∞)  `  
  
`  [0, ∞)  `

`  [2, 20]  `  
  
`  (0, 10]  `  
  
`  [0, 100]  `

`  LINEAR  `  
  
`  LOG  `  
  
`  LINEAR  `

`  AUTOENCODER  `

`  MEAN_ABSOLUTE_ERROR  `  
  
`  MEAN_SQUARED_ERROR  ` (default)  
  
`  MEAN_SQUARED_LOG_ERROR  `

`  LEARN_RATE  `  
  
`  BATCH_SIZE  `  
  
`  L1_REG  `  
  
`  L2_REG  `  
  
`  L1_REG_ACTIVATION  `  
  
`  DROPOUT  `  
  
`  HIDDEN_UNITS  `  
  
  
`  OPTIMIZER  `  
  
  
  
`  ACTIVATION_FN  `

`  [0, 1]  `  
  
`  (0, ∞)  `  
  
`  (0, ∞)  `  
  
`  (0, ∞)  `  
  
`  (0, ∞)  `  
  
  
`  [0, 1)  `  
  
Array of `  [1, ∞)  `  
  
{ `  ADAM  ` , `  ADAGRAD  ` , `  FTRL  ` , `  RMSPROP  ` , `  SGD  ` }  
  
{ `  RELU  ` , `  RELU6  ` , `  CRELU  ` , `  ELU  ` , `  SELU  ` , `  SIGMOID  ` , `  TANH  ` }

`  [0, 1]  `  
  
`  [16, 1024]  `  
  
`  (0, 10]  `  
  
`  (0, 10]  `  
  
`  (0, 10]  `  
  
  
`  [0, 0.8]  `  
  
N/A  
  
{ `  ADAM  ` , `  ADAGRAD  ` , `  FTRL  ` , `  RMSPROP  ` , `  SGD  ` }  
  
N/A

`  LOG  `  
  
`  LOG  `  
  
`  LOG  `  
  
`  LOG  `  
  
`  LOG  `  
  
  
`  LINEAR  `  
  
N/A  
  
N/A  
  
  
  
N/A

`  DNN_CLASSIFIER  `

`  PRECISION  `  
  
`  RECALL  `  
  
`  ACCURACY  `  
  
`  F1_SCORE  `  
  
`  LOG_LOSS  `  
  
`  ROC_AUC  ` (default)

`  BATCH_SIZE  `  
  
`  DROPOUT  `  
  
`  HIDDEN_UNITS  `  
  
`  LEARN_RATE  `  
  
`  OPTIMIZER  `  
  
  
  
`  L1_REG  `  
  
`  L2_REG  `  
  
`  ACTIVATION_FN  `

`  (0, ∞)  `  
  
`  [0, 1)  `  
  
Array of `  [1, ∞)  `  
  
`  [0, 1]  `  
  
{ `  ADAM  ` , `  ADAGRAD  ` , `  FTRL  ` , `  RMSPROP  ` , `  SGD  ` }  
  
`  (0, ∞)  `  
  
`  (0, ∞)  `  
  
{ `  RELU  ` , `  RELU6  ` , `  CRELU  ` , `  ELU  ` , `  SELU  ` , `  SIGMOID  ` , `  TANH  ` }

`  [16, 1024]  `  
  
`  [0, 0.8]  `  
  
N/A  
  
`  [0, 1]  `  
  
{ `  ADAM  ` , `  ADAGRAD  ` , `  FTRL  ` , `  RMSPROP  ` , `  SGD  ` }  
  
`  (0, 10]  `  
  
`  (0, 10]  `  
  
N/A

`  LOG  `  
  
`  LINEAR  `  
  
N/A  
  
`  LINEAR  `  
  
N/A  
  
  
  
`  LOG  `  
  
`  LOG  `  
  
N/A

`  DNN_REGRESSOR  `

`  MEAN_ABSOLUTE_ERROR  `  
  
`  MEAN_SQUARED_ERROR  `  
  
`  MEAN_SQUARED_LOG_ERROR  `  
  
`  MEDIAN_ABSOLUTE_ERROR  `  
  
`  R2_SCORE  ` (default)  
  
`  EXPLAINED_VARIANCE  `

`  DNN_LINEAR_ COMBINED_ CLASSIFIER  `

`  PRECISION  `  
  
`  RECALL  `  
  
`  ACCURACY  `  
  
`  F1_SCORE  `  
  
`  LOG_LOSS  `  
  
`  ROC_AUC  ` (default)

`  BATCH_SIZE  `  
  
`  DROPOUT  `  
  
`  HIDDEN_UNITS  `  
  
`  L1_REG  `  
  
`  L2_REG  `  
  
`  ACTIVATION_FN  `

`  (0, ∞)  `  
  
`  [0, 1)  `  
  
Array of `  [1, ∞)  `  
  
`  (0, ∞)  `  
  
`  (0, ∞)  `  
  
{ `  RELU  ` , `  RELU6  ` , `  CRELU  ` , `  ELU  ` , `  SELU  ` , `  SIGMOID  ` , `  TANH  ` }

`  [16, 1024]  `  
  
`  [0, 0.8]  `  
  
N/A  
  
`  (0, 10]  `  
  
`  (0, 10]  `  
  
N/A

`  LOG  `  
  
`  LINEAR  `  
  
N/A  
  
`  LOG  `  
  
`  LOG  `  
  
N/A

`  DNN_LINEAR_ COMBINED_ REGRESSOR  `

`  MEAN_ABSOLUTE_ERROR  `  
  
`  MEAN_SQUARED_ERROR  `  
  
`  MEAN_SQUARED_LOG_ERROR  `  
  
`  MEDIAN_ABSOLUTE_ERROR  `  
  
`  R2_SCORE  ` (default)  
  
`  EXPLAINED_VARIANCE  `

`  BOOSTED_TREE_ CLASSIFIER  `

`  PRECISION  `  
  
`  RECALL  `  
  
`  ACCURACY  `  
  
`  F1_SCORE  `  
  
`  LOG_LOSS  `  
  
`  ROC_AUC  ` (default)

`  LEARN_RATE  `  
  
`  L1_REG  `  
  
`  L2_REG  `  
  
`  DROPOUT  `  
  
`  MAX_TREE_DEPTHMAX_TREE_DEPTH  `  
  
`  SUBSAMPLE  `  
  
`  MIN_SPLIT_LOSS  `  
  
`  NUM_PARALLEL_TREE  `  
  
`  MIN_TREE_CHILD_WEIGHT  `  
  
`  COLSAMPLE_BYTREE  `  
  
`  COLSAMPLE_BYLEVEL  `  
  
`  COLSAMPLE_BYNODE  `  
  
`  BOOSTER_TYPE  `  
  
`  DART_NORMALIZE_TYPE  `  
  
`  TREE_METHOD  `

`  [0, ∞)  `  
  
`  (0, ∞)  `  
  
`  (0, ∞)  `  
  
`  [0, 1]  `  
  
`  [1, 20]  `  
  
  
  
`  (0, 1]  `  
  
`  [0, ∞)  `  
  
`  [1, ∞)  `  
  
  
`  [0, ∞)  `  
  
  
`  [0, 1]  `  
  
  
`  [0, 1]  `  
  
  
`  [0, 1]  `  
  
  
{ `  GBTREE  ` , `  DART  ` }  
  
{ `  TREE  ` , `  FOREST  ` }  
  
{ `  AUTO  ` , `  EXACT  ` , `  APPROX  ` , `  HIST  ` }

`  [0, 1]  `  
  
`  (0, 10]  `  
  
`  (0, 10]  `  
  
N/A  
  
`  [1, 10]  `  
  
  
  
`  (0, 1]  `  
  
N/A  
  
N/A  
  
  
N/A  
  
  
N/A  
  
  
N/A  
  
  
N/A  
  
  
N/A  
  
N/A  
  
N/A

`  LINEAR  `  
  
`  LOG  `  
  
`  LOG  `  
  
`  LINEAR  `  
  
`  LINEAR  `  
  
  
  
`  LINEAR  `  
  
`  LINEAR  `  
  
`  LINEAR  `  
  
  
`  LINEAR  `  
  
  
`  LINEAR  `  
  
  
`  LINEAR  `  
  
  
`  LINEAR  `  
  
  
N/A  
  
N/A  
  
N/A

`  BOOSTED_TREE_ REGRESSOR  `  
  
  
  
  
  

`  MEAN_ABSOLUTE_ERROR  `  
  
`  MEAN_SQUARED_ERROR  `  
  
`  MEAN_SQUARED_LOG_ERROR  `  
  
`  MEDIAN_ABSOLUTE_ERROR  `  
  
`  R2_SCORE  ` (default)  
  
`  EXPLAINED_VARIANCE  `

`  RANDOM_FOREST_ CLASSIFIER  `

`  PRECISION  `  
  
`  RECALL  `  
  
`  ACCURACY  `  
  
`  F1_SCORE  `  
  
`  LOG_LOSS  `  
  
`  ROC_AUC  ` (default)

`  L1_REG  `  
  
`  L2_REG  `  
  
`  MAX_TREE_DEPTH  `  
  
`  SUBSAMPLE  `  
  
`  MIN_SPLIT_LOSS  `  
  
`  NUM_PARALLEL_TREE  `  
  
`  MIN_TREE_CHILD_WEIGHT  `  
  
`  COLSAMPLE_BYTREE  `  
  
`  COLSAMPLE_BYLEVEL  `  
  
`  COLSAMPLE_BYNODE  `  
  
`  TREE_METHOD  `

`  (0, ∞)  `  
  
`  (0, ∞)  `  
  
`  [1, 20]  `  
  
`  (0, 1)  `  
  
`  [0, ∞)  `  
  
`  [2, ∞)  `  
  
  
`  [0, ∞)  `  
  
  
`  [0, 1]  `  
  
  
`  [0, 1]  `  
  
  
`  [0, 1]  `  
  
{ `  AUTO  ` , `  EXACT  ` , `  APPROX  ` , `  HIST  ` }

`  (0, 10]  `  
  
`  (0, 10]  `  
  
`  [1, 20]  `  
  
`  (0, 1)  `  
  
N/A  
  
`  [2, 200]  `  
  
  
N/A  
  
  
N/A  
  
  
N/A  
  
  
N/A  
  
  
N/A

`  LOG  `  
  
`  LOG  `  
  
`  LINEAR  `  
  
`  LINEAR  `  
  
`  LINEAR  `  
  
`  LINEAR  `  
  
  
`  LINEAR  `  
  
  
`  LINEAR  `  
  
  
`  LINEAR  `  
  
  
`  LINEAR  `  
  
  
N/A

`  RANDOM_FOREST_ REGRESSOR  `  
  
  
  
  
  

`  MEAN_ABSOLUTE_ERROR  `  
  
`  MEAN_SQUARED_ERROR  `  
  
`  MEAN_SQUARED_LOG_ERROR  `  
  
`  MEDIAN_ABSOLUTE_ERROR  `  
  
`  R2_SCORE  ` (default)  
  
`  EXPLAINED_VARIANCE  `

Most `  LOG  ` scale hyperparameters use the open lower boundary of `  0  ` . You can still set `  0  ` as the lower boundary by using the `  HPARAM_RANGE  ` keyword to set the hyperparameter range. For example, in a boosted tree classifier model, you could set the range for the [`  L1_REG  ` hyperparameter](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree#l1_reg) as `  L1_REG = HPARAM_RANGE(0, 5)  ` . A value of `  0  ` gets converted to `  1e-14  ` .

Conditional hyperparameters are supported. For example, in a boosted tree regressor model, you can only tune the [`  DART_NORMALIZE_TYPE  ` hyperparameter](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree#dart_normalize_type) when the value of the [`  BOOSTER_TYPE  ` hyperparameter](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree#booster_type) is `  DART  ` . In this case, you specify both search spaces and the conditions are handled automatically, as shown in the following example:

``` text
BOOSTER_TYPE = HPARAM_CANDIDATES(['DART', 'GBTREE'])
DART_NORMALIZE_TYPE = HPARAM_CANDIDATES(['TREE', 'FOREST'])
```

## Search starting point

If you don't specify a search space for a hyperparameter by using `  HPARAM_RANGE  ` or `  HPARAM_CANDIDATES  ` , the search starts from the default value of that hyperparameter, as documented in the `  CREATE MODEL  ` topic for that model type. For example, if you are running hyperparameter tuning for a [boosted tree model](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree) , and you don't specify a value for the [`  L1_REG  ` hyperparameter](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree#l1_reg) , then the search starts from `  0  ` , the default value.

If you specify a search space for a hyperparameter by using `  HPARAM_RANGE  ` or `  HPARAM_CANDIDATES  ` , the search starting points depends on whether the specified search space includes the default value for that hyperparameter, as documented in the `  CREATE MODEL  ` topic for that model type:

  - If the specified range contains the default value, that's where the search starts. For example, if you are running hyperparameter tuning for an implicit [matrix factorization model](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-matrix-factorization) , and you specify the value `  [20, 30, 40, 50]  ` for the [`  WALS_ALPHA  ` hyperparameter](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-matrix-factorization#wals_alpha) , then the search starts at `  40  ` , the default value.
  - If the specified range doesn't contain the default value, the search starts from the point in the specified range that is closest to the default value. For example,if you specify the value `  [10, 20, 30]  ` for the `  WALS_ALPHA  ` hyperparameter, then the search starts from `  30  ` , which is the closest value to the default value of `  40  ` .

## Data split

When you specify a value for the `  NUM_TRIALS  ` option, the service identifies that you are doing hyperparameter tuning and automatically performs a 3-way split on input data to divide it into training, evaluation, and test sets. By default, the input data is randomized and then split 80% for training, 10% for evaluation, and 10% for testing.

The training and evaluation sets are used in each trial training, the same as in models that don't use hyperparameter tuning. The trial hyperparameter suggestions are calculated based on the [model evaluation metrics](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-evaluate#output) for that model type. At the end of each trial training, the test set is used to test the trial and record its metrics in the model. This ensures the objectivity of the final reporting evaluation metrics by using data that has not yet been analyzed by the model. Evaluation data is used to calculate the intermediate metrics for hyperparameter suggestion, while the test data is used to calculate the final, objective model metrics.

If you want to use only a training set, specify `  NO_SPLIT  ` for the [`  DATA_SPLIT_METHOD  ` option](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create#data_split_method) of the `  CREATE MODEL  ` statement.

If you want to use only training and evaluation sets, specify `  0  ` for the [`  DATA_SPLIT_TEST_FRACTION  ` option](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create#data_split_test_fraction) of the `  CREATE MODEL  ` statement. When the test set is empty, the evaluation set is used as the test set for the final evaluation metrics reporting.

The metrics from models that are generated from a normal training job and those from a hyperparameter tuning training job are only comparable when the data split fractions are equal. For example, the following models are comparable:

  - Non-hyperparameter tuning: `  DATA_SPLIT_METHOD='RANDOM', DATA_SPLIT_EVAL_FRACTION=0.2  `
  - Hyperparameter tuning: `  DATA_SPLIT_METHOD='RANDOM', DATA_SPLIT_EVAL_FRACTION=0.2, DATA_SPLIT_TEST_FRACTION=0  `

## Performance

Model performance when using hyperparameter tuning is typically no worse than model performance when using the default search space and not using hyperparameter tuning. A model that uses the default search space and doesn't use hyperparameter tuning always uses the default hyperparameters in the first trial.

To confirm the model performance improvements provided by hyperparameter tuning, compare the optimal trial for the hyperparameter tuning model to the first trial for the non-hyperparameter tuning model.

## Transfer learning

Transfer learning is enabled by default when you set the [`  HPARAM_TUNING_ALGORITHM  ` option](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create#hparam_tuning_algorithm) in the `  CREATE MODEL  ` statement to `  VIZIER_DEFAULT  ` . The hyperparameter tuning for a model benefits by learning from previously tuned models if it meets the following requirements:

  - It has the same model type as previously tuned models.
  - It resides in the same project as previously tuned models.
  - It use the same hyperparameter search space OR a *subset* of the hyperparameter search space of previously tuned models. A subset uses the same hyperparameter names and types, but doesn't have to have the same ranges. For example, `  (a:[0, 10])  ` is considered as a subset of `  (a:[-1, 1], b:[0, 1])  ` .

Transfer learning doesn't require that the input data be the same.

Transfer learning helps solve the cold start problem where the system performs random exploration during the first trial batch. Transfer learning provides the system with some initial knowledge about the hyperparameters and their objectives. To continuously improve the model quality, always train a new hyperparameter tuning model with the same or a subset of hyperparameters.

Transfer learning helps hyperparameter tuning converge faster, instead of helping submodels to converge.

## Error handling

Hyperparameter tuning handles errors in the following ways:

  - Cancellation: If a training job is cancelled while running, then all successful trials remain usable.

  - Invalid input: If the user input is invalid, then the service returns a user error.

  - Invalid hyperparameters: If the hyperparameters are invalid for a trial, then the trial is skipped and marked as `  INFEASIBLE  ` in the output from the `  ML.TRIAL_INFO  ` function.

  - Trial internal error: If more than 10% of the `  NUM_TRIALS  ` value fail due to `  INTERNAL_ERROR  ` , then the training job stops and returns a user error.

  - If less than 10% of the `  NUM_TRIALS  ` value fail due to `  INTERNAL_ERROR  ` , the training continues with the failed trials marked as `  FAILED  ` in the output from the `  ML.TRIAL_INFO  ` function.

## Model serving functions

You can use output models from hyperparameter tuning with a number of existing model serving functions. To use these functions, follow these rules:

  - When the function takes input data, only the result from one trial is returned. By default this is the optimal trial, but you can also choose a particular trial by specifying the `  TRIAL_ID  ` as an argument for the given function. You can get the `  TRIAL_ID  ` from the output of the `  ML.TRIAL_INFO  ` function. The following functions are supported:
    
      - [`  ML.CONFUSION_MATRIX  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-confusion)
      - [`  ML.EVALUATE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-evaluate)
      - [`  ML.PREDICT  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-predict)
      - [`  ML.RECOMMEND  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-recommend)
      - [`  ML.ROC_CURVE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-roc)

  - When the function doesn't take input data, all trial results are returned, and the first output column is `  TRIAL_ID  ` . The following functions are supported:
    
      - [`  ML.CENTROIDS  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-centroids)
      - [`  ML.EVALUATE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-evaluate)
      - [`  ML.WEIGHTS  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-weights)

The output from [`  ML.FEATURE_INFO  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-feature) doesn't change, because all trials share the same input data.

Evaluation metrics from `  ML.EVALUATE  ` and `  ML.TRIAL_INFO  ` can be different because of the way input data is split. By default, `  ML.EVALUATE  ` runs against the test data, while `  ML.TRIAL_INFO  ` runs against the evaluation data. For more information, see [Data split](#data_split) .

### Unsupported functions

The [`  ML.TRAINING_INFO  ` function](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-train) returns information for each iteration, and iteration results aren't saved in hyperparameter tuning models. Trial results are saved instead. You can use the [`  ML.TRIAL_INFO  ` function](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-trial-info) to get information about trial results.

## Model export

You can export models created with hyperparameter tuning to Cloud Storage locations using the [`  EXPORT MODEL  ` statement](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-export-model) . You can export the default optimal trial or any specified trial.

## Pricing

The cost of hyperparameter tuning training is the sum of the cost of all executed trials. The pricing of a trial is consistent with the existing [BigQuery ML pricing model](https://cloud.google.com/bigquery/pricing#bqml) .

## FAQ

This section provides answers to some frequently asked questions about hyperparameter tuning.

### How many trials do I need to tune a model?

We recommend using at least 10 trials for one hyperparameter, so the total number of trials should be at least `  10 * num_hyperparameters  ` . If you are using the default search space, refer to the **Hyperparameters** column in the [Hyperparameters and objectives](/bigquery/docs/reference/standard-sql/bigqueryml-hyperparameter-tuning#hyperparameters_and_objectives) table for the number of hyperparameters tuned by default for a given model type.

### What if I don't see performance improvements by using hyperparameter tuning?

Make sure you follow the guidance in this document to get a fair comparison. If you still don't see performance improvements, it might mean the default hyperparameters already work well for you. You might want to focus on feature engineering or try other model types before trying another round of hyperparameter tuning.

### What if I want to continue tuning a model?

Train a new hyperparameter tuning model with the same search space. The built-in transfer learning helps to continue tuning based on your previously tuned models.

### Do I need to retrain the model with all data and the optimal hyperparameters?

It depends on the following factors:

  - K-means models already use all data as the training data, so there's no need to retrain the model.

  - For matrix factorization models, you can retrain the model with the selected hyperparameters and all input data for better coverage of users and items.

  - For all other model types, retraining is usually unnecessary. The service already keeps 80% of the input data for training during the default random data split. You can still retrain the model with more training data and the selected hyperparameters if your dataset is small, but leaving little evaluation data for early stop might worsen overfitting.

## What's next

  - To try running hyperparameter tuning, see [Use the BigQuery ML hyperparameter tuning to improve model performance](/bigquery/docs/hyperparameter-tuning-tutorial) .
  - For more information about supported SQL statements and functions for ML models, see [End-to-end user journeys for ML models](/bigquery/docs/e2e-journey) .
