# End-to-end user journeys for ML models

This document describes the user journeys for machine learning (ML) models that are trained in BigQuery ML, including the statements and functions that you can use to work with ML models. BigQuery ML offers the following types of ML models:

  - [Supervised learning](https://developers.google.com/machine-learning/glossary/fundamentals#supervised-machine-learning) models:
    
      - [Linear and logistic regression](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm)
      - [Deep neural network (DNN)](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-dnn-models)
      - [Wide & Deep](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-wnd-models)
      - [Boosted trees](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree)
      - [Random forest](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-random-forest)
      - [AutoML](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-automl)

  - [Unsupervised learning](https://developers.google.com/machine-learning/glossary/fundamentals#unsupervised-machine-learning) models:
    
      - [K-means clustering](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-kmeans)
      - [Matrix factorization](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-matrix-factorization)
      - [Autoencoder](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-autoencoder)
      - [Principal component analysis (PCA)](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-pca)

  - [Transform-only](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-transform) models: Transform-only models aren't typical ML models but are instead artifacts that transform raw data into features.

## Model creation user journeys

The following table describes the statements and functions you can use to create and tune models:

Model category

Model type

Model creation

[Feature preprocessing](/bigquery/docs/preprocess-overview)

[Hyperparameter tuning](/bigquery/docs/hp-tuning-overview) <sup>1</sup>

[Model weights](/bigquery/docs/weights-overview)

Feature & training info

Tutorials

Supervised learning

Linear & logistic regression

[`  CREATE MODEL  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-glm)

[Automatic preprocessing](/bigquery/docs/auto-preprocessing)  
  
[Manual preprocessing](/bigquery/docs/manual-preprocessing)

[Hyperparameter tuning](/bigquery/docs/hp-tuning-overview)  
  
[`  ML.TRIAL _INFO  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-trial-info)

[`  ML.WEIGHTS  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-weights)

[`  ML.FEATURE _INFO  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-feature)  
  
[`  ML.TRAINING _INFO  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-train)

[Use linear regression to predict penguin weight](/bigquery/docs/linear-regression-tutorial)  
  
[Perform classification with a logistic regression model](/bigquery/docs/logistic-regression-prediction)

Deep neural networks (DNN)

[`  CREATE MODEL  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-dnn-models)

[Automatic preprocessing](/bigquery/docs/auto-preprocessing)  
  
[Manual preprocessing](/bigquery/docs/manual-preprocessing)

[Hyperparameter tuning](/bigquery/docs/hp-tuning-overview)  
  
[`  ML.TRIAL _INFO  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-trial-info)

N/A <sup>2</sup>

[`  ML.FEATURE _INFO  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-feature)  
  
[`  ML.TRAINING _INFO  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-train)

N/A

Wide & Deep networks

[`  CREATE MODEL  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-wnd-models)

[Automatic preprocessing](/bigquery/docs/auto-preprocessing)  
  
[Manual preprocessing](/bigquery/docs/manual-preprocessing)

[Hyperparameter tuning](/bigquery/docs/hp-tuning-overview)  
  
[`  ML.TRIAL _INFO  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-trial-info)

N/A <sup>2</sup>

[`  ML.FEATURE _INFO  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-feature)  
  
[`  ML.TRAINING _INFO  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-train)

N/A

Boosted trees

[`  CREATE MODEL  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree)

[Automatic preprocessing](/bigquery/docs/auto-preprocessing)  
  
[Manual preprocessing](/bigquery/docs/manual-preprocessing)

[Hyperparameter tuning](/bigquery/docs/hp-tuning-overview)  
  
[`  ML.TRIAL _INFO  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-trial-info)

N/A <sup>2</sup>

[`  ML.FEATURE _INFO  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-feature)  
  
[`  ML.TRAINING _INFO  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-train)

[Perform classification with a boosted trees model](/bigquery/docs/boosted-tree-classifier-tutorial)

Random forest

[`  CREATE MODEL  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-random-forest)

[Automatic preprocessing](/bigquery/docs/auto-preprocessing)  
  
[Manual preprocessing](/bigquery/docs/manual-preprocessing)

[Hyperparameter tuning](/bigquery/docs/hp-tuning-overview)  
  
[`  ML.TRIAL _INFO  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-trial-info)

N/A <sup>2</sup>

[`  ML.FEATURE _INFO  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-feature)  
  
[`  ML.TRAINING _INFO  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-train)

N/A

AutoML classification & regression

[`  CREATE MODEL  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-automl)

AutoML automatically performs feature engineering

AutoML automatically performs hyperparameter tuning

N/A <sup>2</sup>

[`  ML.FEATURE _INFO  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-feature)  
  
[`  ML.TRAINING _INFO  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-train)

N/A

Unsupervised learning

K-means

[`  CREATE MODEL  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-kmeans)

[Automatic preprocessing](/bigquery/docs/auto-preprocessing)  
  
[Manual preprocessing](/bigquery/docs/manual-preprocessing)

[Hyperparameter tuning](/bigquery/docs/hp-tuning-overview)  
  
[`  ML.TRIAL _INFO  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-trial-info)

[`  ML.CENTROIDS  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-centroids)

[`  ML.FEATURE _INFO  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-feature)  
  
[`  ML.TRAINING _INFO  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-train)

[Find clusters in bike station data](/bigquery/docs/kmeans-tutorial)

Matrix factorization

[`  CREATE MODEL  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-matrix-factorization)

N/A

[Hyperparameter tuning](/bigquery/docs/hp-tuning-overview)  
  
[`  ML.TRIAL _INFO  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-trial-info)

[`  ML.WEIGHTS  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-weights)

[`  ML.FEATURE _INFO  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-feature)  
  
[`  ML.TRAINING _INFO  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-train)

[Generate movie recommendations using explicit feedback](/bigquery/docs/bigqueryml-mf-explicit-tutorial)  
  
[Generate content recommendations using implicit feedback](/bigquery/docs/bigqueryml-mf-implicit-tutorial)

Principal component analysis (PCA)

[`  CREATE MODEL  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-pca)

[Automatic preprocessing](/bigquery/docs/auto-preprocessing)  
  
[Manual preprocessing](/bigquery/docs/manual-preprocessing)

N/A

[`  ML.PRINCIPAL _COMPONENTS  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-principal-components)  
  
[`  ML.PRINCIPAL _COMPONENT _INFO  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-principal-component-info)

[`  ML.FEATURE _INFO  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-feature)  
  
[`  ML.TRAINING _INFO  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-train)

N/A

Autoencoder

[`  CREATE MODEL  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-autoencoder)

[Automatic preprocessing](/bigquery/docs/auto-preprocessing)  
  
[Manual preprocessing](/bigquery/docs/manual-preprocessing)

[Hyperparameter tuning](/bigquery/docs/hp-tuning-overview)  
  
[`  ML.TRIAL _INFO  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-trial-info)

N/A <sup>2</sup>

[`  ML.FEATURE _INFO  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-feature)  
  
[`  ML.TRAINING _INFO  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-train)

N/A

Transform-only

Transform-only

[`  CREATE MODEL  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-transform)

[Manual preprocessing](/bigquery/docs/manual-preprocessing)

N/A

N/A

[`  ML.FEATURE _INFO  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-feature)

N/A

<sup>1</sup> For a step-by-step example of using hyperparameter tuning, see [Improve model performance with hyperparameter tuning](/bigquery/docs/hyperparameter-tuning-tutorial) .

<sup>2</sup> BigQuery ML doesn't offer a function to retrieve the weights for this model. To see the weights of the model, you can export the model from BigQuery ML to Cloud Storage and then use the XGBoost library or the TensorFlow library to visualize the tree structure for tree models or the graph structure for neural networks. For more information, see [`  EXPORT MODEL  `](/bigquery/docs/exporting-models) and [Export a BigQuery ML model for online prediction](/bigquery/docs/export-model-tutorial) .

## Model use user journeys

The following table describes the statements and functions you can use to evaluate, explain, and get predictions from models:

Model category

Model type

[Evaluation](/bigquery/docs/evaluate-overview)

[Inference](/bigquery/docs/inference-overview)

[AI explanation](/bigquery/docs/xai-overview)

[Model monitoring](/bigquery/docs/model-monitoring-overview)

Supervised learning

Linear & logistic regression

[`  ML.EVALUATE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-evaluate)  
  
[`  ML.CONFUSION _MATRIX  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-confusion) <sup>1</sup>  
  
[`  ML.ROC_CURVE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-roc) <sup>2</sup>

[`  ML.PREDICT  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-predict)  
  
[`  ML.TRANSFORM  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-transform)

[`  ML.EXPLAIN_PREDICT  ` <sup>3</sup>](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-explain-predict)  
  
[`  ML.GLOBAL_EXPLAIN  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-global-explain)  
  
[`  ML.ADVANCED_WEIGHTS  ` <sup>5</sup>](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-advanced-weights)

[`  ML.DESCRIBE_DATA  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-describe-data)  
  
[`  ML.VALIDATE_DATA _DRIFT  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-validate-data-drift)  
  
[`  ML.VALIDATE_DATA _SKEW  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-validate-data-skew)  
  
[`  ML.TFDV_DESCRIBE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-tfdv-describe)  
  
[`  ML.TFDV_VALIDATE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-tfdv-validate)

Deep neural networks (DNN)

[`  ML.EVALUATE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-evaluate)  
  
[`  ML.CONFUSION _MATRIX  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-confusion) <sup>1</sup>  
  
[`  ML.ROC_CURVE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-roc) <sup>2</sup>

[`  ML.PREDICT  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-predict)  
  
[`  ML.TRANSFORM  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-transform)

[`  ML.EXPLAIN_PREDICT  ` <sup>3</sup>](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-explain-predict)  
  
[`  ML.GLOBAL_EXPLAIN  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-global-explain)  
  
[`  ML.ADVANCED_WEIGHTS  ` <sup>5</sup>](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-advanced-weights)

[`  ML.DESCRIBE_DATA  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-describe-data)  
  
[`  ML.VALIDATE_DATA _DRIFT  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-validate-data-drift)  
  
[`  ML.VALIDATE_DATA _SKEW  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-validate-data-skew)  
  
[`  ML.TFDV_DESCRIBE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-tfdv-describe)  
  
[`  ML.TFDV_VALIDATE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-tfdv-validate)

Wide & Deep networks

[`  ML.EVALUATE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-evaluate)  
  
[`  ML.CONFUSION _MATRIX  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-confusion) <sup>1</sup>  
  
[`  ML.ROC_CURVE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-roc) <sup>2</sup>

[`  ML.PREDICT  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-predict)  
  
[`  ML.TRANSFORM  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-transform)

[`  ML.EXPLAIN_PREDICT  ` <sup>3</sup>](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-explain-predict)  
  
[`  ML.GLOBAL_EXPLAIN  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-global-explain)  
  
[`  ML.ADVANCED_WEIGHTS  ` <sup>5</sup>](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-advanced-weights)

[`  ML.DESCRIBE_DATA  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-describe-data)  
  
[`  ML.VALIDATE_DATA _DRIFT  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-validate-data-drift)  
  
[`  ML.VALIDATE_DATA _SKEW  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-validate-data-skew)  
  
[`  ML.TFDV_DESCRIBE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-tfdv-describe)  
  
[`  ML.TFDV_VALIDATE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-tfdv-validate)

Boosted trees

[`  ML.EVALUATE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-evaluate)  
  
[`  ML.CONFUSION _MATRIX  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-confusion) <sup>1</sup>  
  
[`  ML.ROC_CURVE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-roc) <sup>2</sup>

[`  ML.PREDICT  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-predict)  
  
[`  ML.TRANSFORM  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-transform)

[`  ML.EXPLAIN_PREDICT  ` <sup>3</sup>](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-explain-predict)  
  
[`  ML.GLOBAL_EXPLAIN  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-global-explain)  
  
[`  ML.FEATURE_IMPORTANCE  ` <sup>4</sup>](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-importance)

[`  ML.DESCRIBE_DATA  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-describe-data)  
  
[`  ML.VALIDATE_DATA _DRIFT  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-validate-data-drift)  
  
[`  ML.VALIDATE_DATA _SKEW  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-validate-data-skew)  
  
[`  ML.TFDV_DESCRIBE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-tfdv-describe)  
  
[`  ML.TFDV_VALIDATE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-tfdv-validate)

Random forest

[`  ML.EVALUATE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-evaluate)  
  
[`  ML.CONFUSION _MATRIX  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-confusion) <sup>1</sup>  
  
[`  ML.ROC_CURVE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-roc) <sup>2</sup>

[`  ML.PREDICT  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-predict)  
  
[`  ML.TRANSFORM  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-transform)

[`  ML.EXPLAIN_PREDICT  ` <sup>3</sup>](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-explain-predict)  
  
[`  ML.GLOBAL_EXPLAIN  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-global-explain)  
  
[`  ML.FEATURE_IMPORTANCE  ` <sup>4</sup>](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-importance)

[`  ML.DESCRIBE_DATA  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-describe-data)  
  
[`  ML.VALIDATE_DATA _DRIFT  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-validate-data-drift)  
  
[`  ML.VALIDATE_DATA _SKEW  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-validate-data-skew)  
  
[`  ML.TFDV_DESCRIBE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-tfdv-describe)  
  
[`  ML.TFDV_VALIDATE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-tfdv-validate)

AutoML classification & regression

[`  ML.EVALUATE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-evaluate)  
  
[`  ML.CONFUSION _MATRIX  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-confusion) <sup>1</sup>  
  
[`  ML.ROC_CURVE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-roc) <sup>2</sup>

[`  ML.PREDICT  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-predict)

[`  ML.GLOBAL_EXPLAIN  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-global-explain)

[`  ML.DESCRIBE_DATA  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-describe-data)  
  
[`  ML.VALIDATE_DATA _DRIFT  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-validate-data-drift)  
  
[`  ML.VALIDATE_DATA _SKEW  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-validate-data-skew)  
  
[`  ML.TFDV_DESCRIBE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-tfdv-describe)  
  
[`  ML.TFDV_VALIDATE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-tfdv-validate)

Unsupervised learning

K-means

[`  ML.EVALUATE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-evaluate)

[`  ML.PREDICT  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-predict)  
[`  ML.DETECT _ANOMALIES  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-detect-anomalies)  
  
[`  ML.TRANSFORM  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-transform)

N/A

[`  ML.DESCRIBE_DATA  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-describe-data)  
  
[`  ML.VALIDATE_DATA _DRIFT  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-validate-data-drift)  
  
[`  ML.VALIDATE_DATA _SKEW  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-validate-data-skew)  
  
[`  ML.TFDV_DESCRIBE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-tfdv-describe)  
  
[`  ML.TFDV_VALIDATE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-tfdv-validate)

Matrix factorization

[`  ML.EVALUATE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-evaluate)

[`  ML.RECOMMEND  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-recommend)  
  
[`  ML.GENERATE _EMBEDDING  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-generate-embedding)

N/A

N/A

Principal component analysis (PCA)

[`  ML.EVALUATE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-evaluate)

[`  ML.PREDICT  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-predict)  
[`  ML.GENERATE _EMBEDDING  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-generate-embedding)  
[`  ML.DETECT _ANOMALIES  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-detect-anomalies)  
  
[`  ML.TRANSFORM  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-transform)

N/A

[`  ML.DESCRIBE_DATA  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-describe-data)  
  
[`  ML.VALIDATE_DATA _DRIFT  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-validate-data-drift)  
  
[`  ML.VALIDATE_DATA _SKEW  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-validate-data-skew)  
  
[`  ML.TFDV_DESCRIBE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-tfdv-describe)  
  
[`  ML.TFDV_VALIDATE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-tfdv-validate)

Autoencoder

[`  ML.EVALUATE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-evaluate)

[`  ML.PREDICT  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-predict)  
  
[`  ML.GENERATE _EMBEDDING  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-generate-embedding)  
[`  ML.DETECT _ANOMALIES  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-detect-anomalies)  
  
[`  ML.RECONSTRUCTION _LOSS  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-reconstruction-loss)  
  
[`  ML.TRANSFORM  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-transform)

N/A

[`  ML.DESCRIBE_DATA  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-describe-data)  
  
[`  ML.VALIDATE_DATA _DRIFT  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-validate-data-drift)  
  
[`  ML.VALIDATE_DATA _SKEW  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-validate-data-skew)  
  
[`  ML.TFDV_DESCRIBE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-tfdv-describe)  
  
[`  ML.TFDV_VALIDATE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-tfdv-validate)

Transform-only

Transform-only

N/A

[`  ML.TRANSFORM  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-transform)

N/A

N/A

<sup>1</sup> `  ML.CONFUSION_MATRIX  ` is only applicable to classification models.

<sup>2</sup> `  ML.ROC_CURVE  ` is only applicable to binary classification models.

<sup>3</sup> The `  ML.EXPLAIN_PREDICT  ` function encompasses the `  ML.PREDICT  ` function because its output is a superset of the results of `  ML.PREDICT  ` .

<sup>4</sup> To understand the difference between `  ML.GLOBAL_EXPLAIN  ` and `  ML.FEATURE_IMPORTANCE  ` , see the [Explainable AI overview](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-xai-overview) .

<sup>5</sup> The `  ML.ADVANCED_WEIGHTS  ` function encompasses the `  ML.WEIGHTS  ` function because its output is a superset of the results of `  ML.WEIGHTS  ` .
