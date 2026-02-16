  - [Resource: Model](#Model)
      - [JSON representation](#Model.SCHEMA_REPRESENTATION)
  - [ModelReference](#ModelReference)
      - [JSON representation](#ModelReference.SCHEMA_REPRESENTATION)
  - [ModelType](#ModelType)
  - [TrainingRun](#TrainingRun)
      - [JSON representation](#TrainingRun.SCHEMA_REPRESENTATION)
  - [TrainingOptions](#TrainingOptions)
      - [JSON representation](#TrainingOptions.SCHEMA_REPRESENTATION)
  - [LossType](#LossType)
  - [DataSplitMethod](#DataSplitMethod)
  - [LearnRateStrategy](#LearnRateStrategy)
  - [DistanceType](#DistanceType)
  - [OptimizationStrategy](#OptimizationStrategy)
  - [BoosterType](#BoosterType)
  - [DartNormalizeType](#DartNormalizeType)
  - [TreeMethod](#TreeMethod)
  - [FeedbackType](#FeedbackType)
  - [KmeansInitializationMethod](#KmeansInitializationMethod)
  - [ArimaOrder](#ArimaOrder)
      - [JSON representation](#ArimaOrder.SCHEMA_REPRESENTATION)
  - [DataFrequency](#DataFrequency)
  - [HolidayRegion](#HolidayRegion)
  - [HparamTuningObjective](#HparamTuningObjective)
  - [EncodingMethod](#EncodingMethod)
  - [PcaSolver](#PcaSolver)
  - [ModelRegistry](#ModelRegistry)
  - [IterationResult](#IterationResult)
      - [JSON representation](#IterationResult.SCHEMA_REPRESENTATION)
  - [ClusterInfo](#ClusterInfo)
      - [JSON representation](#ClusterInfo.SCHEMA_REPRESENTATION)
  - [ArimaResult](#ArimaResult)
      - [JSON representation](#ArimaResult.SCHEMA_REPRESENTATION)
  - [ArimaModelInfo](#ArimaModelInfo)
      - [JSON representation](#ArimaModelInfo.SCHEMA_REPRESENTATION)
  - [ArimaCoefficients](#ArimaCoefficients)
      - [JSON representation](#ArimaCoefficients.SCHEMA_REPRESENTATION)
  - [ArimaFittingMetrics](#ArimaFittingMetrics)
      - [JSON representation](#ArimaFittingMetrics.SCHEMA_REPRESENTATION)
  - [SeasonalPeriodType](#SeasonalPeriodType)
  - [PrincipalComponentInfo](#PrincipalComponentInfo)
      - [JSON representation](#PrincipalComponentInfo.SCHEMA_REPRESENTATION)
  - [EvaluationMetrics](#EvaluationMetrics)
      - [JSON representation](#EvaluationMetrics.SCHEMA_REPRESENTATION)
  - [RegressionMetrics](#RegressionMetrics)
      - [JSON representation](#RegressionMetrics.SCHEMA_REPRESENTATION)
  - [BinaryClassificationMetrics](#BinaryClassificationMetrics)
      - [JSON representation](#BinaryClassificationMetrics.SCHEMA_REPRESENTATION)
  - [AggregateClassificationMetrics](#AggregateClassificationMetrics)
      - [JSON representation](#AggregateClassificationMetrics.SCHEMA_REPRESENTATION)
  - [BinaryConfusionMatrix](#BinaryConfusionMatrix)
      - [JSON representation](#BinaryConfusionMatrix.SCHEMA_REPRESENTATION)
  - [MultiClassClassificationMetrics](#MultiClassClassificationMetrics)
      - [JSON representation](#MultiClassClassificationMetrics.SCHEMA_REPRESENTATION)
  - [ConfusionMatrix](#ConfusionMatrix)
      - [JSON representation](#ConfusionMatrix.SCHEMA_REPRESENTATION)
  - [Row](#Row)
      - [JSON representation](#Row.SCHEMA_REPRESENTATION)
  - [Entry](#Entry)
      - [JSON representation](#Entry.SCHEMA_REPRESENTATION)
  - [ClusteringMetrics](#ClusteringMetrics)
      - [JSON representation](#ClusteringMetrics.SCHEMA_REPRESENTATION)
  - [Cluster](#Cluster)
      - [JSON representation](#Cluster.SCHEMA_REPRESENTATION)
  - [FeatureValue](#FeatureValue)
      - [JSON representation](#FeatureValue.SCHEMA_REPRESENTATION)
  - [CategoricalValue](#CategoricalValue)
      - [JSON representation](#CategoricalValue.SCHEMA_REPRESENTATION)
  - [CategoryCount](#CategoryCount)
      - [JSON representation](#CategoryCount.SCHEMA_REPRESENTATION)
  - [RankingMetrics](#RankingMetrics)
      - [JSON representation](#RankingMetrics.SCHEMA_REPRESENTATION)
  - [ArimaForecastingMetrics](#ArimaForecastingMetrics)
      - [JSON representation](#ArimaForecastingMetrics.SCHEMA_REPRESENTATION)
  - [ArimaSingleModelForecastingMetrics](#ArimaSingleModelForecastingMetrics)
      - [JSON representation](#ArimaSingleModelForecastingMetrics.SCHEMA_REPRESENTATION)
  - [DimensionalityReductionMetrics](#DimensionalityReductionMetrics)
      - [JSON representation](#DimensionalityReductionMetrics.SCHEMA_REPRESENTATION)
  - [DataSplitResult](#DataSplitResult)
      - [JSON representation](#DataSplitResult.SCHEMA_REPRESENTATION)
  - [GlobalExplanation](#GlobalExplanation)
      - [JSON representation](#GlobalExplanation.SCHEMA_REPRESENTATION)
  - [Explanation](#Explanation)
      - [JSON representation](#Explanation.SCHEMA_REPRESENTATION)
  - [TransformColumn](#TransformColumn)
      - [JSON representation](#TransformColumn.SCHEMA_REPRESENTATION)
  - [HparamSearchSpaces](#HparamSearchSpaces)
      - [JSON representation](#HparamSearchSpaces.SCHEMA_REPRESENTATION)
  - [DoubleHparamSearchSpace](#DoubleHparamSearchSpace)
      - [JSON representation](#DoubleHparamSearchSpace.SCHEMA_REPRESENTATION)
  - [DoubleRange](#DoubleRange)
      - [JSON representation](#DoubleRange.SCHEMA_REPRESENTATION)
  - [DoubleCandidates](#DoubleCandidates)
      - [JSON representation](#DoubleCandidates.SCHEMA_REPRESENTATION)
  - [IntHparamSearchSpace](#IntHparamSearchSpace)
      - [JSON representation](#IntHparamSearchSpace.SCHEMA_REPRESENTATION)
  - [IntRange](#IntRange)
      - [JSON representation](#IntRange.SCHEMA_REPRESENTATION)
  - [IntCandidates](#IntCandidates)
      - [JSON representation](#IntCandidates.SCHEMA_REPRESENTATION)
  - [IntArrayHparamSearchSpace](#IntArrayHparamSearchSpace)
      - [JSON representation](#IntArrayHparamSearchSpace.SCHEMA_REPRESENTATION)
  - [IntArray](#IntArray)
      - [JSON representation](#IntArray.SCHEMA_REPRESENTATION)
  - [StringHparamSearchSpace](#StringHparamSearchSpace)
      - [JSON representation](#StringHparamSearchSpace.SCHEMA_REPRESENTATION)
  - [HparamTuningTrial](#HparamTuningTrial)
      - [JSON representation](#HparamTuningTrial.SCHEMA_REPRESENTATION)
  - [TrialStatus](#TrialStatus)
  - [RemoteModelInfo](#RemoteModelInfo)
      - [JSON representation](#RemoteModelInfo.SCHEMA_REPRESENTATION)
  - [RemoteServiceType](#RemoteServiceType)
  - [Methods](#METHODS_SUMMARY)

## Resource: Model

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;etag&quot;: string,
  &quot;modelReference&quot;: {
    object (ModelReference)
  },
  &quot;creationTime&quot;: string,
  &quot;lastModifiedTime&quot;: string,
  &quot;description&quot;: string,
  &quot;friendlyName&quot;: string,
  &quot;labels&quot;: {
    string: string,
    ...
  },
  &quot;expirationTime&quot;: string,
  &quot;location&quot;: string,
  &quot;encryptionConfiguration&quot;: {
    object (EncryptionConfiguration)
  },
  &quot;modelType&quot;: enum (ModelType),
  &quot;trainingRuns&quot;: [
    {
      object (TrainingRun)
    }
  ],
  &quot;featureColumns&quot;: [
    {
      object (StandardSqlField)
    }
  ],
  &quot;labelColumns&quot;: [
    {
      object (StandardSqlField)
    }
  ],
  &quot;transformColumns&quot;: [
    {
      object (TransformColumn)
    }
  ],
  &quot;hparamSearchSpaces&quot;: {
    object (HparamSearchSpaces)
  },
  &quot;bestTrialId&quot;: string,
  &quot;defaultTrialId&quot;: string,
  &quot;hparamTrials&quot;: [
    {
      object (HparamTuningTrial)
    }
  ],
  &quot;optimalTrialIds&quot;: [
    string
  ],
  &quot;remoteModelInfo&quot;: {
    object (RemoteModelInfo)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  etag  `

`  string  `

Output only. A hash of this resource.

`  modelReference  `

`  object ( ModelReference  ` )

Required. Unique identifier for this model.

`  creationTime  `

`  string ( int64 format)  `

Output only. The time when this model was created, in millisecs since the epoch.

`  lastModifiedTime  `

`  string ( int64 format)  `

Output only. The time when this model was last modified, in millisecs since the epoch.

`  description  `

`  string  `

Optional. A user-friendly description of this model.

`  friendlyName  `

`  string  `

Optional. A descriptive name for this model.

`  labels  `

`  map (key: string, value: string)  `

The labels associated with this model. You can use these to organize and group your models. Label keys and values can be no longer than 63 characters, can only contain lowercase letters, numeric characters, underscores and dashes. International characters are allowed. Label values are optional. Label keys must start with a letter and each label in the list must have a different key.

`  expirationTime  `

`  string ( int64 format)  `

Optional. The time when this model expires, in milliseconds since the epoch. If not present, the model will persist indefinitely. Expired models will be deleted and their storage reclaimed. The defaultTableExpirationMs property of the encapsulating dataset can be used to set a default expirationTime on newly created models.

`  location  `

`  string  `

Output only. The geographic location where the model resides. This value is inherited from the dataset.

`  encryptionConfiguration  `

`  object ( EncryptionConfiguration  ` )

Custom encryption configuration (e.g., Cloud KMS keys). This shows the encryption configuration of the model data while stored in BigQuery storage. This field can be used with models.patch to update encryption key for an already encrypted model.

`  modelType  `

`  enum ( ModelType  ` )

Output only. Type of the model resource.

`  trainingRuns[]  `

`  object ( TrainingRun  ` )

Information for all training runs in increasing order of startTime.

`  featureColumns[]  `

`  object ( StandardSqlField  ` )

Output only. Input feature columns for the model inference. If the model is trained with TRANSFORM clause, these are the input of the TRANSFORM clause.

`  labelColumns[]  `

`  object ( StandardSqlField  ` )

Output only. Label columns that were used to train this model. The output of the model will have a "predicted\_" prefix to these columns.

`  transformColumns[]  `

`  object ( TransformColumn  ` )

Output only. This field will be populated if a TRANSFORM clause was used to train a model. TRANSFORM clause (if used) takes featureColumns as input and outputs transformColumns. transformColumns then are used to train the model.

`  hparamSearchSpaces  `

`  object ( HparamSearchSpaces  ` )

Output only. All hyperparameter search spaces in this model.

`  bestTrialId (deprecated)  `

`  string ( int64 format)  `

This item is deprecated\!

The best trialId across all training runs.

`  defaultTrialId  `

`  string ( int64 format)  `

Output only. The default trialId to use in TVFs when the trialId is not passed in. For single-objective [hyperparameter tuning](https://cloud.google.com/bigquery-ml/docs/reference/standard-sql/bigqueryml-syntax-hp-tuning-overview) models, this is the best trial ID. For multi-objective [hyperparameter tuning](https://cloud.google.com/bigquery-ml/docs/reference/standard-sql/bigqueryml-syntax-hp-tuning-overview) models, this is the smallest trial ID among all Pareto optimal trials.

`  hparamTrials[]  `

`  object ( HparamTuningTrial  ` )

Output only. Trials of a [hyperparameter tuning](https://cloud.google.com/bigquery-ml/docs/reference/standard-sql/bigqueryml-syntax-hp-tuning-overview) model sorted by trialId.

`  optimalTrialIds[]  `

`  string ( int64 format)  `

Output only. For single-objective [hyperparameter tuning](https://cloud.google.com/bigquery-ml/docs/reference/standard-sql/bigqueryml-syntax-hp-tuning-overview) models, it only contains the best trial. For multi-objective [hyperparameter tuning](https://cloud.google.com/bigquery-ml/docs/reference/standard-sql/bigqueryml-syntax-hp-tuning-overview) models, it contains all Pareto optimal trials sorted by trialId.

`  remoteModelInfo  `

`  object ( RemoteModelInfo  ` )

Output only. Remote model info

## ModelReference

Id path of a model.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;projectId&quot;: string,
  &quot;datasetId&quot;: string,
  &quot;modelId&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  projectId  `

`  string  `

Required. The ID of the project containing this model.

`  datasetId  `

`  string  `

Required. The ID of the dataset containing this model.

`  modelId  `

`  string  `

Required. The ID of the model. The ID must contain only letters (a-z, A-Z), numbers (0-9), or underscores (\_). The maximum length is 1,024 characters.

## ModelType

Indicates the type of the Model.

Enums

`  MODEL_TYPE_UNSPECIFIED  `

Default value.

`  LINEAR_REGRESSION  `

Linear regression model.

`  LOGISTIC_REGRESSION  `

Logistic regression based classification model.

`  KMEANS  `

K-means clustering model.

`  MATRIX_FACTORIZATION  `

Matrix factorization model.

`  DNN_CLASSIFIER  `

DNN classifier model.

`  TENSORFLOW  `

An imported TensorFlow model.

`  DNN_REGRESSOR  `

DNN regressor model.

`  XGBOOST  `

An imported XGBoost model.

`  BOOSTED_TREE_REGRESSOR  `

Boosted tree regressor model.

`  BOOSTED_TREE_CLASSIFIER  `

Boosted tree classifier model.

`  ARIMA  `

ARIMA model.

`  AUTOML_REGRESSOR  `

AutoML Tables regression model.

`  AUTOML_CLASSIFIER  `

AutoML Tables classification model.

`  PCA  `

Prinpical Component Analysis model.

`  DNN_LINEAR_COMBINED_CLASSIFIER  `

Wide-and-deep classifier model.

`  DNN_LINEAR_COMBINED_REGRESSOR  `

Wide-and-deep regressor model.

`  AUTOENCODER  `

Autoencoder model.

`  ARIMA_PLUS  `

New name for the ARIMA model.

`  ARIMA_PLUS_XREG  `

ARIMA with external regressors.

`  RANDOM_FOREST_REGRESSOR  `

Random forest regressor model.

`  RANDOM_FOREST_CLASSIFIER  `

Random forest classifier model.

`  TENSORFLOW_LITE  `

An imported TensorFlow Lite model.

`  ONNX  `

An imported ONNX model.

`  TRANSFORM_ONLY  `

Model to capture the columns and logic in the TRANSFORM clause along with statistics useful for ML analytic functions.

`  CONTRIBUTION_ANALYSIS  `

The contribution analysis model.

## TrainingRun

Information about a single training query run for the model.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;trainingOptions&quot;: {
    object (TrainingOptions)
  },
  &quot;trainingStartTime&quot;: string,
  &quot;startTime&quot;: string,
  &quot;results&quot;: [
    {
      object (IterationResult)
    }
  ],
  &quot;evaluationMetrics&quot;: {
    object (EvaluationMetrics)
  },
  &quot;dataSplitResult&quot;: {
    object (DataSplitResult)
  },
  &quot;modelLevelGlobalExplanation&quot;: {
    object (GlobalExplanation)
  },
  &quot;classLevelGlobalExplanations&quot;: [
    {
      object (GlobalExplanation)
    }
  ],
  &quot;vertexAiModelId&quot;: string,
  &quot;vertexAiModelVersion&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  trainingOptions  `

`  object ( TrainingOptions  ` )

Output only. Options that were used for this training run, includes user specified and default options that were used.

`  trainingStartTime (deprecated)  `

`  string ( int64 format)  `

This item is deprecated\!

Output only. The start time of this training run, in milliseconds since epoch.

`  startTime  `

`  string ( Timestamp  ` format)

Output only. The start time of this training run.

`  results[]  `

`  object ( IterationResult  ` )

Output only. Output of each iteration run, results.size() \<= maxIterations.

`  evaluationMetrics  `

`  object ( EvaluationMetrics  ` )

Output only. The evaluation metrics over training/eval data that were computed at the end of training.

`  dataSplitResult  `

`  object ( DataSplitResult  ` )

Output only. Data split result of the training run. Only set when the input data is actually split.

`  modelLevelGlobalExplanation  `

`  object ( GlobalExplanation  ` )

Output only. Global explanation contains the explanation of top features on the model level. Applies to both regression and classification models.

`  classLevelGlobalExplanations[]  `

`  object ( GlobalExplanation  ` )

Output only. Global explanation contains the explanation of top features on the class level. Applies to classification models only.

`  vertexAiModelId  `

`  string  `

The model id in the [Vertex AI Model Registry](https://cloud.google.com/vertex-ai/docs/model-registry/introduction) for this training run.

`  vertexAiModelVersion  `

`  string  `

Output only. The model version in the [Vertex AI Model Registry](https://cloud.google.com/vertex-ai/docs/model-registry/introduction) for this training run.

## TrainingOptions

Options used in model training.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;maxIterations&quot;: string,
  &quot;lossType&quot;: enum (LossType),
  &quot;learnRate&quot;: number,
  &quot;l1Regularization&quot;: number,
  &quot;l2Regularization&quot;: number,
  &quot;minRelativeProgress&quot;: number,
  &quot;warmStart&quot;: boolean,
  &quot;earlyStop&quot;: boolean,
  &quot;inputLabelColumns&quot;: [
    string
  ],
  &quot;dataSplitMethod&quot;: enum (DataSplitMethod),
  &quot;dataSplitEvalFraction&quot;: number,
  &quot;dataSplitColumn&quot;: string,
  &quot;learnRateStrategy&quot;: enum (LearnRateStrategy),
  &quot;initialLearnRate&quot;: number,
  &quot;labelClassWeights&quot;: {
    string: number,
    ...
  },
  &quot;userColumn&quot;: string,
  &quot;itemColumn&quot;: string,
  &quot;distanceType&quot;: enum (DistanceType),
  &quot;numClusters&quot;: string,
  &quot;modelUri&quot;: string,
  &quot;optimizationStrategy&quot;: enum (OptimizationStrategy),
  &quot;hiddenUnits&quot;: [
    string
  ],
  &quot;batchSize&quot;: string,
  &quot;dropout&quot;: number,
  &quot;maxTreeDepth&quot;: string,
  &quot;subsample&quot;: number,
  &quot;minSplitLoss&quot;: number,
  &quot;boosterType&quot;: enum (BoosterType),
  &quot;numParallelTree&quot;: string,
  &quot;dartNormalizeType&quot;: enum (DartNormalizeType),
  &quot;treeMethod&quot;: enum (TreeMethod),
  &quot;minTreeChildWeight&quot;: string,
  &quot;colsampleBytree&quot;: number,
  &quot;colsampleBylevel&quot;: number,
  &quot;colsampleBynode&quot;: number,
  &quot;numFactors&quot;: string,
  &quot;feedbackType&quot;: enum (FeedbackType),
  &quot;walsAlpha&quot;: number,
  &quot;kmeansInitializationMethod&quot;: enum (KmeansInitializationMethod),
  &quot;kmeansInitializationColumn&quot;: string,
  &quot;timeSeriesTimestampColumn&quot;: string,
  &quot;timeSeriesDataColumn&quot;: string,
  &quot;autoArima&quot;: boolean,
  &quot;nonSeasonalOrder&quot;: {
    object (ArimaOrder)
  },
  &quot;dataFrequency&quot;: enum (DataFrequency),
  &quot;calculatePValues&quot;: boolean,
  &quot;includeDrift&quot;: boolean,
  &quot;holidayRegion&quot;: enum (HolidayRegion),
  &quot;holidayRegions&quot;: [
    enum (HolidayRegion)
  ],
  &quot;timeSeriesIdColumn&quot;: string,
  &quot;timeSeriesIdColumns&quot;: [
    string
  ],
  &quot;forecastLimitLowerBound&quot;: number,
  &quot;forecastLimitUpperBound&quot;: number,
  &quot;horizon&quot;: string,
  &quot;autoArimaMaxOrder&quot;: string,
  &quot;autoArimaMinOrder&quot;: string,
  &quot;numTrials&quot;: string,
  &quot;maxParallelTrials&quot;: string,
  &quot;hparamTuningObjectives&quot;: [
    enum (HparamTuningObjective)
  ],
  &quot;decomposeTimeSeries&quot;: boolean,
  &quot;cleanSpikesAndDips&quot;: boolean,
  &quot;adjustStepChanges&quot;: boolean,
  &quot;enableGlobalExplain&quot;: boolean,
  &quot;sampledShapleyNumPaths&quot;: string,
  &quot;integratedGradientsNumSteps&quot;: string,
  &quot;categoryEncodingMethod&quot;: enum (EncodingMethod),
  &quot;tfVersion&quot;: string,
  &quot;instanceWeightColumn&quot;: string,
  &quot;trendSmoothingWindowSize&quot;: string,
  &quot;timeSeriesLengthFraction&quot;: number,
  &quot;minTimeSeriesLength&quot;: string,
  &quot;maxTimeSeriesLength&quot;: string,
  &quot;xgboostVersion&quot;: string,
  &quot;approxGlobalFeatureContrib&quot;: boolean,
  &quot;fitIntercept&quot;: boolean,
  &quot;numPrincipalComponents&quot;: string,
  &quot;pcaExplainedVarianceRatio&quot;: number,
  &quot;scaleFeatures&quot;: boolean,
  &quot;pcaSolver&quot;: enum (PcaSolver),
  &quot;autoClassWeights&quot;: boolean,
  &quot;activationFn&quot;: string,
  &quot;optimizer&quot;: string,
  &quot;budgetHours&quot;: number,
  &quot;standardizeFeatures&quot;: boolean,
  &quot;l1RegActivation&quot;: number,
  &quot;modelRegistry&quot;: enum (ModelRegistry),
  &quot;vertexAiModelVersionAliases&quot;: [
    string
  ],
  &quot;dimensionIdColumns&quot;: [
    string
  ],
  &quot;contributionMetric&quot;: string,
  &quot;isTestColumn&quot;: string,
  &quot;minAprioriSupport&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  maxIterations  `

`  string ( int64 format)  `

The maximum number of iterations in training. Used only for iterative training algorithms.

`  lossType  `

`  enum ( LossType  ` )

Type of loss function used during training run.

`  learnRate  `

`  number  `

Learning rate in training. Used only for iterative training algorithms.

`  l1Regularization  `

`  number  `

L1 regularization coefficient.

`  l2Regularization  `

`  number  `

L2 regularization coefficient.

`  minRelativeProgress  `

`  number  `

When earlyStop is true, stops training when accuracy improvement is less than 'minRelativeProgress'. Used only for iterative training algorithms.

`  warmStart  `

`  boolean  `

Whether to train a model from the last checkpoint.

`  earlyStop  `

`  boolean  `

Whether to stop early when the loss doesn't improve significantly any more (compared to minRelativeProgress). Used only for iterative training algorithms.

`  inputLabelColumns[]  `

`  string  `

Name of input label columns in training data.

`  dataSplitMethod  `

`  enum ( DataSplitMethod  ` )

The data split type for training and evaluation, e.g. RANDOM.

`  dataSplitEvalFraction  `

`  number  `

The fraction of evaluation data over the whole input data. The rest of data will be used as training data. The format should be double. Accurate to two decimal places. Default value is 0.2.

`  dataSplitColumn  `

`  string  `

The column to split data with. This column won't be used as a feature. 1. When dataSplitMethod is CUSTOM, the corresponding column should be boolean. The rows with true value tag are eval data, and the false are training data. 2. When dataSplitMethod is SEQ, the first DATA\_SPLIT\_EVAL\_FRACTION rows (from smallest to largest) in the corresponding column are used as training data, and the rest are eval data. It respects the order in Orderable data types: <https://cloud.google.com/bigquery/docs/reference/standard-sql/data-types#data_type_properties>

`  learnRateStrategy  `

`  enum ( LearnRateStrategy  ` )

The strategy to determine learn rate for the current iteration.

`  initialLearnRate  `

`  number  `

Specifies the initial learning rate for the line search learn rate strategy.

`  labelClassWeights  `

`  map (key: string, value: number)  `

Weights associated with each label class, for rebalancing the training data. Only applicable for classification models.

`  userColumn  `

`  string  `

User column specified for matrix factorization models.

`  itemColumn  `

`  string  `

Item column specified for matrix factorization models.

`  distanceType  `

`  enum ( DistanceType  ` )

Distance type for clustering models.

`  numClusters  `

`  string ( int64 format)  `

Number of clusters for clustering models.

`  modelUri  `

`  string  `

Google Cloud Storage URI from which the model was imported. Only applicable for imported models.

`  optimizationStrategy  `

`  enum ( OptimizationStrategy  ` )

Optimization strategy for training linear regression models.

`  hiddenUnits[]  `

`  string ( int64 format)  `

Hidden units for dnn models.

`  batchSize  `

`  string ( int64 format)  `

Batch size for dnn models.

`  dropout  `

`  number  `

Dropout probability for dnn models.

`  maxTreeDepth  `

`  string ( int64 format)  `

Maximum depth of a tree for boosted tree models.

`  subsample  `

`  number  `

Subsample fraction of the training data to grow tree to prevent overfitting for boosted tree models.

`  minSplitLoss  `

`  number  `

Minimum split loss for boosted tree models.

`  boosterType  `

`  enum ( BoosterType  ` )

Booster type for boosted tree models.

`  numParallelTree  `

`  string ( Int64Value format)  `

Number of parallel trees constructed during each iteration for boosted tree models.

`  dartNormalizeType  `

`  enum ( DartNormalizeType  ` )

Type of normalization algorithm for boosted tree models using dart booster.

`  treeMethod  `

`  enum ( TreeMethod  ` )

Tree construction algorithm for boosted tree models.

`  minTreeChildWeight  `

`  string ( Int64Value format)  `

Minimum sum of instance weight needed in a child for boosted tree models.

`  colsampleBytree  `

`  number  `

Subsample ratio of columns when constructing each tree for boosted tree models.

`  colsampleBylevel  `

`  number  `

Subsample ratio of columns for each level for boosted tree models.

`  colsampleBynode  `

`  number  `

Subsample ratio of columns for each node(split) for boosted tree models.

`  numFactors  `

`  string ( int64 format)  `

Num factors specified for matrix factorization models.

`  feedbackType  `

`  enum ( FeedbackType  ` )

Feedback type that specifies which algorithm to run for matrix factorization.

`  walsAlpha  `

`  number  `

Hyperparameter for matrix factoration when implicit feedback type is specified.

`  kmeansInitializationMethod  `

`  enum ( KmeansInitializationMethod  ` )

The method used to initialize the centroids for kmeans algorithm.

`  kmeansInitializationColumn  `

`  string  `

The column used to provide the initial centroids for kmeans algorithm when kmeansInitializationMethod is CUSTOM.

`  timeSeriesTimestampColumn  `

`  string  `

Column to be designated as time series timestamp for ARIMA model.

`  timeSeriesDataColumn  `

`  string  `

Column to be designated as time series data for ARIMA model.

`  autoArima  `

`  boolean  `

Whether to enable auto ARIMA or not.

`  nonSeasonalOrder  `

`  object ( ArimaOrder  ` )

A specification of the non-seasonal part of the ARIMA model: the three components (p, d, q) are the AR order, the degree of differencing, and the MA order.

`  dataFrequency  `

`  enum ( DataFrequency  ` )

The data frequency of a time series.

`  calculatePValues  `

`  boolean  `

Whether or not p-value test should be computed for this model. Only available for linear and logistic regression models.

`  includeDrift  `

`  boolean  `

Include drift when fitting an ARIMA model.

`  holidayRegion  `

`  enum ( HolidayRegion  ` )

The geographical region based on which the holidays are considered in time series modeling. If a valid value is specified, then holiday effects modeling is enabled.

`  holidayRegions[]  `

`  enum ( HolidayRegion  ` )

A list of geographical regions that are used for time series modeling.

`  timeSeriesIdColumn  `

`  string  `

The time series id column that was used during ARIMA model training.

`  timeSeriesIdColumns[]  `

`  string  `

The time series id columns that were used during ARIMA model training.

`  forecastLimitLowerBound  `

`  number  `

The forecast limit lower bound that was used during ARIMA model training with limits. To see more details of the algorithm: <https://otexts.com/fpp2/limits.html>

`  forecastLimitUpperBound  `

`  number  `

The forecast limit upper bound that was used during ARIMA model training with limits.

`  horizon  `

`  string ( int64 format)  `

The number of periods ahead that need to be forecasted.

`  autoArimaMaxOrder  `

`  string ( int64 format)  `

The max value of the sum of non-seasonal p and q.

`  autoArimaMinOrder  `

`  string ( int64 format)  `

The min value of the sum of non-seasonal p and q.

`  numTrials  `

`  string ( int64 format)  `

Number of trials to run this hyperparameter tuning job.

`  maxParallelTrials  `

`  string ( int64 format)  `

Maximum number of trials to run in parallel.

`  hparamTuningObjectives[]  `

`  enum ( HparamTuningObjective  ` )

The target evaluation metrics to optimize the hyperparameters for.

`  decomposeTimeSeries  `

`  boolean  `

If true, perform decompose time series and save the results.

`  cleanSpikesAndDips  `

`  boolean  `

If true, clean spikes and dips in the input time series.

`  adjustStepChanges  `

`  boolean  `

If true, detect step changes and make data adjustment in the input time series.

`  enableGlobalExplain  `

`  boolean  `

If true, enable global explanation during training.

`  sampledShapleyNumPaths  `

`  string ( int64 format)  `

Number of paths for the sampled Shapley explain method.

`  integratedGradientsNumSteps  `

`  string ( int64 format)  `

Number of integral steps for the integrated gradients explain method.

`  categoryEncodingMethod  `

`  enum ( EncodingMethod  ` )

Categorical feature encoding method.

`  tfVersion  `

`  string  `

Based on the selected TF version, the corresponding docker image is used to train external models.

`  instanceWeightColumn  `

`  string  `

Name of the instance weight column for training data. This column isn't be used as a feature.

`  trendSmoothingWindowSize  `

`  string ( int64 format)  `

Smoothing window size for the trend component. When a positive value is specified, a center moving average smoothing is applied on the history trend. When the smoothing window is out of the boundary at the beginning or the end of the trend, the first element or the last element is padded to fill the smoothing window before the average is applied.

`  timeSeriesLengthFraction  `

`  number  `

The fraction of the interpolated length of the time series that's used to model the time series trend component. All of the time points of the time series are used to model the non-trend component. This training option accelerates modeling training without sacrificing much forecasting accuracy. You can use this option with `  minTimeSeriesLength  ` but not with `  maxTimeSeriesLength  ` .

`  minTimeSeriesLength  `

`  string ( int64 format)  `

The minimum number of time points in a time series that are used in modeling the trend component of the time series. If you use this option you must also set the `  timeSeriesLengthFraction  ` option. This training option ensures that enough time points are available when you use `  timeSeriesLengthFraction  ` in trend modeling. This is particularly important when forecasting multiple time series in a single query using `  timeSeriesIdColumn  ` . If the total number of time points is less than the `  minTimeSeriesLength  ` value, then the query uses all available time points.

`  maxTimeSeriesLength  `

`  string ( int64 format)  `

The maximum number of time points in a time series that can be used in modeling the trend component of the time series. Don't use this option with the `  timeSeriesLengthFraction  ` or `  minTimeSeriesLength  ` options.

`  xgboostVersion  `

`  string  `

User-selected XGBoost versions for training of XGBoost models.

`  approxGlobalFeatureContrib  `

`  boolean  `

Whether to use approximate feature contribution method in XGBoost model explanation for global explain.

`  fitIntercept  `

`  boolean  `

Whether the model should include intercept during model training.

`  numPrincipalComponents  `

`  string ( int64 format)  `

Number of principal components to keep in the PCA model. Must be \<= the number of features.

`  pcaExplainedVarianceRatio  `

`  number  `

The minimum ratio of cumulative explained variance that needs to be given by the PCA model.

`  scaleFeatures  `

`  boolean  `

If true, scale the feature values by dividing the feature standard deviation. Currently only apply to PCA.

`  pcaSolver  `

`  enum ( PcaSolver  ` )

The solver for PCA.

`  autoClassWeights  `

`  boolean  `

Whether to calculate class weights automatically based on the popularity of each label.

`  activationFn  `

`  string  `

Activation function of the neural nets.

`  optimizer  `

`  string  `

Optimizer used for training the neural nets.

`  budgetHours  `

`  number  `

Budget in hours for AutoML training.

`  standardizeFeatures  `

`  boolean  `

Whether to standardize numerical features. Default to true.

`  l1RegActivation  `

`  number  `

L1 regularization coefficient to activations.

`  modelRegistry  `

`  enum ( ModelRegistry  ` )

The model registry.

`  vertexAiModelVersionAliases[]  `

`  string  `

The version aliases to apply in Vertex AI model registry. Always overwrite if the version aliases exists in a existing model.

`  dimensionIdColumns[]  `

`  string  `

Optional. Names of the columns to slice on. Applies to contribution analysis models.

`  contributionMetric  `

`  string  `

The contribution metric. Applies to contribution analysis models. Allowed formats supported are for summable and summable ratio contribution metrics. These include expressions such as `  SUM(x)  ` or `  SUM(x)/SUM(y)  ` , where x and y are column names from the base table.

`  isTestColumn  `

`  string  `

Name of the column used to determine the rows corresponding to control and test. Applies to contribution analysis models.

`  minAprioriSupport  `

`  number  `

The apriori support minimum. Applies to contribution analysis models.

## LossType

Loss metric to evaluate model training performance.

Enums

`  LOSS_TYPE_UNSPECIFIED  `

Default value.

`  MEAN_SQUARED_LOSS  `

Mean squared loss, used for linear regression.

`  MEAN_LOG_LOSS  `

Mean log loss, used for logistic regression.

## DataSplitMethod

Indicates the method to split input data into multiple tables.

Enums

`  DATA_SPLIT_METHOD_UNSPECIFIED  `

Default value.

`  RANDOM  `

Splits data randomly.

`  CUSTOM  `

Splits data with the user provided tags.

`  SEQUENTIAL  `

Splits data sequentially.

`  NO_SPLIT  `

Data split will be skipped.

`  AUTO_SPLIT  `

Splits data automatically: Uses NO\_SPLIT if the data size is small. Otherwise uses RANDOM.

## LearnRateStrategy

Indicates the learning rate optimization strategy to use.

Enums

`  LEARN_RATE_STRATEGY_UNSPECIFIED  `

Default value.

`  LINE_SEARCH  `

Use line search to determine learning rate.

`  CONSTANT  `

Use a constant learning rate.

## DistanceType

Distance metric used to compute the distance between two points.

Enums

`  DISTANCE_TYPE_UNSPECIFIED  `

Default value.

`  EUCLIDEAN  `

Eculidean distance.

`  COSINE  `

Cosine distance.

## OptimizationStrategy

Indicates the optimization strategy used for training.

Enums

`  OPTIMIZATION_STRATEGY_UNSPECIFIED  `

Default value.

`  BATCH_GRADIENT_DESCENT  `

Uses an iterative batch gradient descent algorithm.

`  NORMAL_EQUATION  `

Uses a normal equation to solve linear regression problem.

## BoosterType

Booster types supported. Refer to booster parameter in XGBoost.

Enums

`  BOOSTER_TYPE_UNSPECIFIED  `

Unspecified booster type.

`  GBTREE  `

Gbtree booster.

`  DART  `

Dart booster.

## DartNormalizeType

Type of normalization algorithm for boosted tree models using dart booster. Refer to normalize\_type in XGBoost.

Enums

`  DART_NORMALIZE_TYPE_UNSPECIFIED  `

Unspecified dart normalize type.

`  TREE  `

New trees have the same weight of each of dropped trees.

`  FOREST  `

New trees have the same weight of sum of dropped trees.

## TreeMethod

Tree construction algorithm used in boosted tree models. Refer to treeMethod in XGBoost.

Enums

`  TREE_METHOD_UNSPECIFIED  `

Unspecified tree method.

`  AUTO  `

Use heuristic to choose the fastest method.

`  EXACT  `

Exact greedy algorithm.

`  APPROX  `

Approximate greedy algorithm using quantile sketch and gradient histogram.

`  HIST  `

Fast histogram optimized approximate greedy algorithm.

## FeedbackType

Indicates the training algorithm to use for matrix factorization models.

Enums

`  FEEDBACK_TYPE_UNSPECIFIED  `

Default value.

`  IMPLICIT  `

Use weighted-als for implicit feedback problems.

`  EXPLICIT  `

Use nonweighted-als for explicit feedback problems.

## KmeansInitializationMethod

Indicates the method used to initialize the centroids for KMeans clustering algorithm.

Enums

`  KMEANS_INITIALIZATION_METHOD_UNSPECIFIED  `

Unspecified initialization method.

`  RANDOM  `

Initializes the centroids randomly.

`  CUSTOM  `

Initializes the centroids using data specified in kmeansInitializationColumn.

`  KMEANS_PLUS_PLUS  `

Initializes with kmeans++.

## ArimaOrder

Arima order, can be used for both non-seasonal and seasonal parts.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;p&quot;: string,
  &quot;d&quot;: string,
  &quot;q&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  p  `

`  string ( Int64Value format)  `

Order of the autoregressive part.

`  d  `

`  string ( Int64Value format)  `

Order of the differencing part.

`  q  `

`  string ( Int64Value format)  `

Order of the moving-average part.

## DataFrequency

Type of supported data frequency for time series forecasting models.

Enums

`  DATA_FREQUENCY_UNSPECIFIED  `

Default value.

`  AUTO_FREQUENCY  `

Automatically inferred from timestamps.

`  YEARLY  `

Yearly data.

`  QUARTERLY  `

Quarterly data.

`  MONTHLY  `

Monthly data.

`  WEEKLY  `

Weekly data.

`  DAILY  `

Daily data.

`  HOURLY  `

Hourly data.

`  PER_MINUTE  `

Per-minute data.

## HolidayRegion

Type of supported holiday regions for time series forecasting models.

Enums

`  HOLIDAY_REGION_UNSPECIFIED  `

Holiday region unspecified.

`  GLOBAL  `

Global.

`  NA  `

North America.

`  JAPAC  `

Japan and Asia Pacific: Korea, Greater China, India, Australia, and New Zealand.

`  EMEA  `

Europe, the Middle East and Africa.

`  LAC  `

Latin America and the Caribbean.

`  AE  `

United Arab Emirates

`  AR  `

Argentina

`  AT  `

Austria

`  AU  `

Australia

`  BE  `

Belgium

`  BR  `

Brazil

`  CA  `

Canada

`  CH  `

Switzerland

`  CL  `

Chile

`  CN  `

China

`  CO  `

Colombia

`  CS  `

Czechoslovakia

`  CZ  `

Czech Republic

`  DE  `

Germany

`  DK  `

Denmark

`  DZ  `

Algeria

`  EC  `

Ecuador

`  EE  `

Estonia

`  EG  `

Egypt

`  ES  `

Spain

`  FI  `

Finland

`  FR  `

France

`  GB  `

Great Britain (United Kingdom)

`  GR  `

Greece

`  HK  `

Hong Kong

`  HU  `

Hungary

`  ID  `

Indonesia

`  IE  `

Ireland

`  IL  `

Israel

`  IN  `

India

`  IR  `

Iran

`  IT  `

Italy

`  JP  `

Japan

`  KR  `

Korea (South)

`  LV  `

Latvia

`  MA  `

Morocco

`  MX  `

Mexico

`  MY  `

Malaysia

`  NG  `

Nigeria

`  NL  `

Netherlands

`  NO  `

Norway

`  NZ  `

New Zealand

`  PE  `

Peru

`  PH  `

Philippines

`  PK  `

Pakistan

`  PL  `

Poland

`  PT  `

Portugal

`  RO  `

Romania

`  RS  `

Serbia

`  RU  `

Russian Federation

`  SA  `

Saudi Arabia

`  SE  `

Sweden

`  SG  `

Singapore

`  SI  `

Slovenia

`  SK  `

Slovakia

`  TH  `

Thailand

`  TR  `

Turkey

`  TW  `

Taiwan

`  UA  `

Ukraine

`  US  `

United States

`  VE  `

Venezuela

`  VN  `

Vietnam

`  ZA  `

South Africa

## HparamTuningObjective

Available evaluation metrics used as hyperparameter tuning objectives.

Enums

`  HPARAM_TUNING_OBJECTIVE_UNSPECIFIED  `

Unspecified evaluation metric.

`  MEAN_ABSOLUTE_ERROR  `

Mean absolute error. meanAbsoluteError = AVG(ABS(label - predicted))

`  MEAN_SQUARED_ERROR  `

Mean squared error. meanSquaredError = AVG(POW(label - predicted, 2))

`  MEAN_SQUARED_LOG_ERROR  `

Mean squared log error. meanSquaredLogError = AVG(POW(LN(1 + label) - LN(1 + predicted), 2))

`  MEDIAN_ABSOLUTE_ERROR  `

Mean absolute error. medianAbsoluteError = APPROX\_QUANTILES(absolute\_error, 2)\[OFFSET(1)\]

`  R_SQUARED  `

R^2 score. This corresponds to r2\_score in ML.EVALUATE. rSquared = 1 - SUM(squared\_error)/(COUNT(label)\*VAR\_POP(label))

`  EXPLAINED_VARIANCE  `

Explained variance. explainedVariance = 1 - VAR\_POP(label\_error)/VAR\_POP(label)

`  PRECISION  `

Precision is the fraction of actual positive predictions that had positive actual labels. For multiclass this is a macro-averaged metric treating each class as a binary classifier.

`  RECALL  `

Recall is the fraction of actual positive labels that were given a positive prediction. For multiclass this is a macro-averaged metric.

`  ACCURACY  `

Accuracy is the fraction of predictions given the correct label. For multiclass this is a globally micro-averaged metric.

`  F1_SCORE  `

The F1 score is an average of recall and precision. For multiclass this is a macro-averaged metric.

`  LOG_LOSS  `

Logarithmic Loss. For multiclass this is a macro-averaged metric.

`  ROC_AUC  `

Area Under an ROC Curve. For multiclass this is a macro-averaged metric.

`  DAVIES_BOULDIN_INDEX  `

Davies-Bouldin Index.

`  MEAN_AVERAGE_PRECISION  `

Mean Average Precision.

`  NORMALIZED_DISCOUNTED_CUMULATIVE_GAIN  `

Normalized Discounted Cumulative Gain.

`  AVERAGE_RANK  `

Average Rank.

## EncodingMethod

Supported encoding methods for categorical features.

Enums

`  ENCODING_METHOD_UNSPECIFIED  `

Unspecified encoding method.

`  ONE_HOT_ENCODING  `

Applies one-hot encoding.

`  LABEL_ENCODING  `

Applies label encoding.

`  DUMMY_ENCODING  `

Applies dummy encoding.

## PcaSolver

Enums for supported PCA solvers.

Enums

`  UNSPECIFIED  `

Default value.

`  FULL  `

Full eigen-decoposition.

`  RANDOMIZED  `

Randomized SVD.

`  AUTO  `

Auto.

## ModelRegistry

Enums for supported model registries.

Enums

`  MODEL_REGISTRY_UNSPECIFIED  `

Default value.

`  VERTEX_AI  `

Vertex AI.

## IterationResult

Information about a single iteration of the training run.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;index&quot;: integer,
  &quot;durationMs&quot;: string,
  &quot;trainingLoss&quot;: number,
  &quot;evalLoss&quot;: number,
  &quot;learnRate&quot;: number,
  &quot;clusterInfos&quot;: [
    {
      object (ClusterInfo)
    }
  ],
  &quot;arimaResult&quot;: {
    object (ArimaResult)
  },
  &quot;principalComponentInfos&quot;: [
    {
      object (PrincipalComponentInfo)
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  index  `

`  integer  `

Index of the iteration, 0 based.

`  durationMs  `

`  string ( Int64Value format)  `

Time taken to run the iteration in milliseconds.

`  trainingLoss  `

`  number  `

Loss computed on the training data at the end of iteration.

`  evalLoss  `

`  number  `

Loss computed on the eval data at the end of iteration.

`  learnRate  `

`  number  `

Learn rate used for this iteration.

`  clusterInfos[]  `

`  object ( ClusterInfo  ` )

Information about top clusters for clustering models.

`  arimaResult  `

`  object ( ArimaResult  ` )

Arima result.

`  principalComponentInfos[]  `

`  object ( PrincipalComponentInfo  ` )

The information of the principal components.

## ClusterInfo

Information about a single cluster for clustering model.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;centroidId&quot;: string,
  &quot;clusterRadius&quot;: number,
  &quot;clusterSize&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  centroidId  `

`  string ( int64 format)  `

Centroid id.

`  clusterRadius  `

`  number  `

Cluster radius, the average distance from centroid to each point assigned to the cluster.

`  clusterSize  `

`  string ( Int64Value format)  `

Cluster size, the total number of points assigned to the cluster.

## ArimaResult

(Auto-)arima fitting result. Wrap everything in ArimaResult for easier refactoring if we want to use model-specific iteration results.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;arimaModelInfo&quot;: [
    {
      object (ArimaModelInfo)
    }
  ],
  &quot;seasonalPeriods&quot;: [
    enum (SeasonalPeriodType)
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  arimaModelInfo[]  `

`  object ( ArimaModelInfo  ` )

This message is repeated because there are multiple arima models fitted in auto-arima. For non-auto-arima model, its size is one.

`  seasonalPeriods[]  `

`  enum ( SeasonalPeriodType  ` )

Seasonal periods. Repeated because multiple periods are supported for one time series.

## ArimaModelInfo

Arima model information.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;nonSeasonalOrder&quot;: {
    object (ArimaOrder)
  },
  &quot;arimaCoefficients&quot;: {
    object (ArimaCoefficients)
  },
  &quot;arimaFittingMetrics&quot;: {
    object (ArimaFittingMetrics)
  },
  &quot;hasDrift&quot;: boolean,
  &quot;timeSeriesId&quot;: string,
  &quot;timeSeriesIds&quot;: [
    string
  ],
  &quot;seasonalPeriods&quot;: [
    enum (SeasonalPeriodType)
  ],
  &quot;hasHolidayEffect&quot;: boolean,
  &quot;hasSpikesAndDips&quot;: boolean,
  &quot;hasStepChanges&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  nonSeasonalOrder  `

`  object ( ArimaOrder  ` )

Non-seasonal order.

`  arimaCoefficients  `

`  object ( ArimaCoefficients  ` )

Arima coefficients.

`  arimaFittingMetrics  `

`  object ( ArimaFittingMetrics  ` )

Arima fitting metrics.

`  hasDrift  `

`  boolean  `

Whether Arima model fitted with drift or not. It is always false when d is not 1.

`  timeSeriesId  `

`  string  `

The timeSeriesId value for this time series. It will be one of the unique values from the timeSeriesIdColumn specified during ARIMA model training. Only present when timeSeriesIdColumn training option was used.

`  timeSeriesIds[]  `

`  string  `

The tuple of timeSeriesIds identifying this time series. It will be one of the unique tuples of values present in the timeSeriesIdColumns specified during ARIMA model training. Only present when timeSeriesIdColumns training option was used and the order of values here are same as the order of timeSeriesIdColumns.

`  seasonalPeriods[]  `

`  enum ( SeasonalPeriodType  ` )

Seasonal periods. Repeated because multiple periods are supported for one time series.

`  hasHolidayEffect  `

`  boolean  `

If true, holiday\_effect is a part of time series decomposition result.

`  hasSpikesAndDips  `

`  boolean  `

If true, spikes\_and\_dips is a part of time series decomposition result.

`  hasStepChanges  `

`  boolean  `

If true, step\_changes is a part of time series decomposition result.

## ArimaCoefficients

Arima coefficients.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;autoRegressiveCoefficients&quot;: [
    number
  ],
  &quot;movingAverageCoefficients&quot;: [
    number
  ],
  &quot;interceptCoefficient&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  autoRegressiveCoefficients[]  `

`  number  `

Auto-regressive coefficients, an array of double.

`  movingAverageCoefficients[]  `

`  number  `

Moving-average coefficients, an array of double.

`  interceptCoefficient  `

`  number  `

Intercept coefficient, just a double not an array.

## ArimaFittingMetrics

ARIMA model fitting metrics.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;logLikelihood&quot;: number,
  &quot;aic&quot;: number,
  &quot;variance&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  logLikelihood  `

`  number  `

Log-likelihood.

`  aic  `

`  number  `

AIC.

`  variance  `

`  number  `

Variance.

## SeasonalPeriodType

Seasonal period type.

Enums

`  SEASONAL_PERIOD_TYPE_UNSPECIFIED  `

Unspecified seasonal period.

`  NO_SEASONALITY  `

No seasonality

`  DAILY  `

Daily period, 24 hours.

`  WEEKLY  `

Weekly period, 7 days.

`  MONTHLY  `

Monthly period, 30 days or irregular.

`  QUARTERLY  `

Quarterly period, 90 days or irregular.

`  YEARLY  `

Yearly period, 365 days or irregular.

## PrincipalComponentInfo

Principal component infos, used only for eigen decomposition based models, e.g., PCA. Ordered by explainedVariance in the descending order.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;principalComponentId&quot;: string,
  &quot;explainedVariance&quot;: number,
  &quot;explainedVarianceRatio&quot;: number,
  &quot;cumulativeExplainedVarianceRatio&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  principalComponentId  `

`  string ( Int64Value format)  `

Id of the principal component.

`  explainedVariance  `

`  number  `

Explained variance by this principal component, which is simply the eigenvalue.

`  explainedVarianceRatio  `

`  number  `

Explained\_variance over the total explained variance.

`  cumulativeExplainedVarianceRatio  `

`  number  `

The explainedVariance is pre-ordered in the descending order to compute the cumulative explained variance ratio.

## EvaluationMetrics

Evaluation metrics of a model. These are either computed on all training data or just the eval data based on whether eval data was used during training. These are not present for imported models.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{

  // Union field metrics can be only one of the following:
  &quot;regressionMetrics&quot;: {
    object (RegressionMetrics)
  },
  &quot;binaryClassificationMetrics&quot;: {
    object (BinaryClassificationMetrics)
  },
  &quot;multiClassClassificationMetrics&quot;: {
    object (MultiClassClassificationMetrics)
  },
  &quot;clusteringMetrics&quot;: {
    object (ClusteringMetrics)
  },
  &quot;rankingMetrics&quot;: {
    object (RankingMetrics)
  },
  &quot;arimaForecastingMetrics&quot;: {
    object (ArimaForecastingMetrics)
  },
  &quot;dimensionalityReductionMetrics&quot;: {
    object (DimensionalityReductionMetrics)
  }
  // End of list of possible types for union field metrics.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `  metrics  ` . Metrics. `  metrics  ` can be only one of the following:

`  regressionMetrics  `

`  object ( RegressionMetrics  ` )

Populated for regression models and explicit feedback type matrix factorization models.

`  binaryClassificationMetrics  `

`  object ( BinaryClassificationMetrics  ` )

Populated for binary classification/classifier models.

`  multiClassClassificationMetrics  `

`  object ( MultiClassClassificationMetrics  ` )

Populated for multi-class classification/classifier models.

`  clusteringMetrics  `

`  object ( ClusteringMetrics  ` )

Populated for clustering models.

`  rankingMetrics  `

`  object ( RankingMetrics  ` )

Populated for implicit feedback type matrix factorization models.

`  arimaForecastingMetrics  `

`  object ( ArimaForecastingMetrics  ` )

Populated for ARIMA models.

`  dimensionalityReductionMetrics  `

`  object ( DimensionalityReductionMetrics  ` )

Evaluation metrics when the model is a dimensionality reduction model, which currently includes PCA.

## RegressionMetrics

Evaluation metrics for regression and explicit feedback type matrix factorization models.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;meanAbsoluteError&quot;: number,
  &quot;meanSquaredError&quot;: number,
  &quot;meanSquaredLogError&quot;: number,
  &quot;medianAbsoluteError&quot;: number,
  &quot;rSquared&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  meanAbsoluteError  `

`  number  `

Mean absolute error.

`  meanSquaredError  `

`  number  `

Mean squared error.

`  meanSquaredLogError  `

`  number  `

Mean squared log error.

`  medianAbsoluteError  `

`  number  `

Median absolute error.

`  rSquared  `

`  number  `

R^2 score. This corresponds to r2\_score in ML.EVALUATE.

## BinaryClassificationMetrics

Evaluation metrics for binary classification/classifier models.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;aggregateClassificationMetrics&quot;: {
    object (AggregateClassificationMetrics)
  },
  &quot;binaryConfusionMatrixList&quot;: [
    {
      object (BinaryConfusionMatrix)
    }
  ],
  &quot;positiveLabel&quot;: string,
  &quot;negativeLabel&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  aggregateClassificationMetrics  `

`  object ( AggregateClassificationMetrics  ` )

Aggregate classification metrics.

`  binaryConfusionMatrixList[]  `

`  object ( BinaryConfusionMatrix  ` )

Binary confusion matrix at multiple thresholds.

`  positiveLabel  `

`  string  `

Label representing the positive class.

`  negativeLabel  `

`  string  `

Label representing the negative class.

## AggregateClassificationMetrics

Aggregate metrics for classification/classifier models. For multi-class models, the metrics are either macro-averaged or micro-averaged. When macro-averaged, the metrics are calculated for each label and then an unweighted average is taken of those values. When micro-averaged, the metric is calculated globally by counting the total number of correctly predicted rows.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;precision&quot;: number,
  &quot;recall&quot;: number,
  &quot;accuracy&quot;: number,
  &quot;threshold&quot;: number,
  &quot;f1Score&quot;: number,
  &quot;logLoss&quot;: number,
  &quot;rocAuc&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  precision  `

`  number  `

Precision is the fraction of actual positive predictions that had positive actual labels. For multiclass this is a macro-averaged metric treating each class as a binary classifier.

`  recall  `

`  number  `

Recall is the fraction of actual positive labels that were given a positive prediction. For multiclass this is a macro-averaged metric.

`  accuracy  `

`  number  `

Accuracy is the fraction of predictions given the correct label. For multiclass this is a micro-averaged metric.

`  threshold  `

`  number  `

Threshold at which the metrics are computed. For binary classification models this is the positive class threshold. For multi-class classification models this is the confidence threshold.

`  f1Score  `

`  number  `

The F1 score is an average of recall and precision. For multiclass this is a macro-averaged metric.

`  logLoss  `

`  number  `

Logarithmic Loss. For multiclass this is a macro-averaged metric.

`  rocAuc  `

`  number  `

Area Under a ROC Curve. For multiclass this is a macro-averaged metric.

## BinaryConfusionMatrix

Confusion matrix for binary classification models.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;positiveClassThreshold&quot;: number,
  &quot;truePositives&quot;: string,
  &quot;falsePositives&quot;: string,
  &quot;trueNegatives&quot;: string,
  &quot;falseNegatives&quot;: string,
  &quot;precision&quot;: number,
  &quot;recall&quot;: number,
  &quot;f1Score&quot;: number,
  &quot;accuracy&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  positiveClassThreshold  `

`  number  `

Threshold value used when computing each of the following metric.

`  truePositives  `

`  string ( Int64Value format)  `

Number of true samples predicted as true.

`  falsePositives  `

`  string ( Int64Value format)  `

Number of false samples predicted as true.

`  trueNegatives  `

`  string ( Int64Value format)  `

Number of true samples predicted as false.

`  falseNegatives  `

`  string ( Int64Value format)  `

Number of false samples predicted as false.

`  precision  `

`  number  `

The fraction of actual positive predictions that had positive actual labels.

`  recall  `

`  number  `

The fraction of actual positive labels that were given a positive prediction.

`  f1Score  `

`  number  `

The equally weighted average of recall and precision.

`  accuracy  `

`  number  `

The fraction of predictions given the correct label.

## MultiClassClassificationMetrics

Evaluation metrics for multi-class classification/classifier models.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;aggregateClassificationMetrics&quot;: {
    object (AggregateClassificationMetrics)
  },
  &quot;confusionMatrixList&quot;: [
    {
      object (ConfusionMatrix)
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  aggregateClassificationMetrics  `

`  object ( AggregateClassificationMetrics  ` )

Aggregate classification metrics.

`  confusionMatrixList[]  `

`  object ( ConfusionMatrix  ` )

Confusion matrix at different thresholds.

## ConfusionMatrix

Confusion matrix for multi-class classification models.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;confidenceThreshold&quot;: number,
  &quot;rows&quot;: [
    {
      object (Row)
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  confidenceThreshold  `

`  number  `

Confidence threshold used when computing the entries of the confusion matrix.

`  rows[]  `

`  object ( Row  ` )

One row per actual label.

## Row

A single row in the confusion matrix.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;actualLabel&quot;: string,
  &quot;entries&quot;: [
    {
      object (Entry)
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  actualLabel  `

`  string  `

The original label of this row.

`  entries[]  `

`  object ( Entry  ` )

Info describing predicted label distribution.

## Entry

A single entry in the confusion matrix.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;predictedLabel&quot;: string,
  &quot;itemCount&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  predictedLabel  `

`  string  `

The predicted label. For confidenceThreshold \> 0, we will also add an entry indicating the number of items under the confidence threshold.

`  itemCount  `

`  string ( Int64Value format)  `

Number of items being predicted as this label.

## ClusteringMetrics

Evaluation metrics for clustering models.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;daviesBouldinIndex&quot;: number,
  &quot;meanSquaredDistance&quot;: number,
  &quot;clusters&quot;: [
    {
      object (Cluster)
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  daviesBouldinIndex  `

`  number  `

Davies-Bouldin index.

`  meanSquaredDistance  `

`  number  `

Mean of squared distances between each sample to its cluster centroid.

`  clusters[]  `

`  object ( Cluster  ` )

Information for all clusters.

## Cluster

Message containing the information about one cluster.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;centroidId&quot;: string,
  &quot;featureValues&quot;: [
    {
      object (FeatureValue)
    }
  ],
  &quot;count&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  centroidId  `

`  string ( int64 format)  `

Centroid id.

`  featureValues[]  `

`  object ( FeatureValue  ` )

Values of highly variant features for this cluster.

`  count  `

`  string ( Int64Value format)  `

Count of training data rows that were assigned to this cluster.

## FeatureValue

Representative value of a single feature within the cluster.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;featureColumn&quot;: string,

  // Union field value can be only one of the following:
  &quot;numericalValue&quot;: number,
  &quot;categoricalValue&quot;: {
    object (CategoricalValue)
  }
  // End of list of possible types for union field value.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  featureColumn  `

`  string  `

The feature column name.

Union field `  value  ` . Value. `  value  ` can be only one of the following:

`  numericalValue  `

`  number  `

The numerical feature value. This is the centroid value for this feature.

`  categoricalValue  `

`  object ( CategoricalValue  ` )

The categorical feature value.

## CategoricalValue

Representative value of a categorical feature.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;categoryCounts&quot;: [
    {
      object (CategoryCount)
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  categoryCounts[]  `

`  object ( CategoryCount  ` )

Counts of all categories for the categorical feature. If there are more than ten categories, we return top ten (by count) and return one more CategoryCount with category "\_OTHER\_" and count as aggregate counts of remaining categories.

## CategoryCount

Represents the count of a single category within the cluster.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;category&quot;: string,
  &quot;count&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  category  `

`  string  `

The name of category.

`  count  `

`  string ( Int64Value format)  `

The count of training samples matching the category within the cluster.

## RankingMetrics

Evaluation metrics used by weighted-ALS models specified by feedbackType=implicit.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;meanAveragePrecision&quot;: number,
  &quot;meanSquaredError&quot;: number,
  &quot;normalizedDiscountedCumulativeGain&quot;: number,
  &quot;averageRank&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  meanAveragePrecision  `

`  number  `

Calculates a precision per user for all the items by ranking them and then averages all the precisions across all the users.

`  meanSquaredError  `

`  number  `

Similar to the mean squared error computed in regression and explicit recommendation models except instead of computing the rating directly, the output from evaluate is computed against a preference which is 1 or 0 depending on if the rating exists or not.

`  normalizedDiscountedCumulativeGain  `

`  number  `

A metric to determine the goodness of a ranking calculated from the predicted confidence by comparing it to an ideal rank measured by the original ratings.

`  averageRank  `

`  number  `

Determines the goodness of a ranking by computing the percentile rank from the predicted confidence and dividing it by the original rank.

## ArimaForecastingMetrics

Model evaluation metrics for ARIMA forecasting models.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;nonSeasonalOrder&quot;: [
    {
      object (ArimaOrder)
    }
  ],
  &quot;arimaFittingMetrics&quot;: [
    {
      object (ArimaFittingMetrics)
    }
  ],
  &quot;seasonalPeriods&quot;: [
    enum (SeasonalPeriodType)
  ],
  &quot;hasDrift&quot;: [
    boolean
  ],
  &quot;timeSeriesId&quot;: [
    string
  ],
  &quot;arimaSingleModelForecastingMetrics&quot;: [
    {
      object (ArimaSingleModelForecastingMetrics)
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  nonSeasonalOrder[] (deprecated)  `

`  object ( ArimaOrder  ` )

This item is deprecated\!

Non-seasonal order.

`  arimaFittingMetrics[] (deprecated)  `

`  object ( ArimaFittingMetrics  ` )

This item is deprecated\!

Arima model fitting metrics.

`  seasonalPeriods[] (deprecated)  `

`  enum ( SeasonalPeriodType  ` )

This item is deprecated\!

Seasonal periods. Repeated because multiple periods are supported for one time series.

`  hasDrift[] (deprecated)  `

`  boolean  `

This item is deprecated\!

Whether Arima model fitted with drift or not. It is always false when d is not 1.

`  timeSeriesId[] (deprecated)  `

`  string  `

This item is deprecated\!

Id to differentiate different time series for the large-scale case.

`  arimaSingleModelForecastingMetrics[]  `

`  object ( ArimaSingleModelForecastingMetrics  ` )

Repeated as there can be many metric sets (one for each model) in auto-arima and the large-scale case.

## ArimaSingleModelForecastingMetrics

Model evaluation metrics for a single ARIMA forecasting model.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;nonSeasonalOrder&quot;: {
    object (ArimaOrder)
  },
  &quot;arimaFittingMetrics&quot;: {
    object (ArimaFittingMetrics)
  },
  &quot;hasDrift&quot;: boolean,
  &quot;timeSeriesId&quot;: string,
  &quot;timeSeriesIds&quot;: [
    string
  ],
  &quot;seasonalPeriods&quot;: [
    enum (SeasonalPeriodType)
  ],
  &quot;hasHolidayEffect&quot;: boolean,
  &quot;hasSpikesAndDips&quot;: boolean,
  &quot;hasStepChanges&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  nonSeasonalOrder  `

`  object ( ArimaOrder  ` )

Non-seasonal order.

`  arimaFittingMetrics  `

`  object ( ArimaFittingMetrics  ` )

Arima fitting metrics.

`  hasDrift  `

`  boolean  `

Is arima model fitted with drift or not. It is always false when d is not 1.

`  timeSeriesId  `

`  string  `

The timeSeriesId value for this time series. It will be one of the unique values from the timeSeriesIdColumn specified during ARIMA model training. Only present when timeSeriesIdColumn training option was used.

`  timeSeriesIds[]  `

`  string  `

The tuple of timeSeriesIds identifying this time series. It will be one of the unique tuples of values present in the timeSeriesIdColumns specified during ARIMA model training. Only present when timeSeriesIdColumns training option was used and the order of values here are same as the order of timeSeriesIdColumns.

`  seasonalPeriods[]  `

`  enum ( SeasonalPeriodType  ` )

Seasonal periods. Repeated because multiple periods are supported for one time series.

`  hasHolidayEffect  `

`  boolean  `

If true, holiday\_effect is a part of time series decomposition result.

`  hasSpikesAndDips  `

`  boolean  `

If true, spikes\_and\_dips is a part of time series decomposition result.

`  hasStepChanges  `

`  boolean  `

If true, step\_changes is a part of time series decomposition result.

## DimensionalityReductionMetrics

Model evaluation metrics for dimensionality reduction models.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;totalExplainedVarianceRatio&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  totalExplainedVarianceRatio  `

`  number  `

Total percentage of variance explained by the selected principal components.

## DataSplitResult

Data split result. This contains references to the training and evaluation data tables that were used to train the model.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;trainingTable&quot;: {
    object (TableReference)
  },
  &quot;evaluationTable&quot;: {
    object (TableReference)
  },
  &quot;testTable&quot;: {
    object (TableReference)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  trainingTable  `

`  object ( TableReference  ` )

Table reference of the training data after split.

`  evaluationTable  `

`  object ( TableReference  ` )

Table reference of the evaluation data after split.

`  testTable  `

`  object ( TableReference  ` )

Table reference of the test data after split.

## GlobalExplanation

Global explanations containing the top most important features after training.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;explanations&quot;: [
    {
      object (Explanation)
    }
  ],
  &quot;classLabel&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  explanations[]  `

`  object ( Explanation  ` )

A list of the top global explanations. Sorted by absolute value of attribution in descending order.

`  classLabel  `

`  string  `

Class label for this set of global explanations. Will be empty/null for binary logistic and linear regression models. Sorted alphabetically in descending order.

## Explanation

Explanation for a single feature.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;featureName&quot;: string,
  &quot;attribution&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  featureName  `

`  string  `

The full feature name. For non-numerical features, will be formatted like `  <column_name>.<encoded_feature_name>  ` . Overall size of feature name will always be truncated to first 120 characters.

`  attribution  `

`  number  `

Attribution of feature.

## TransformColumn

Information about a single transform column.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;name&quot;: string,
  &quot;type&quot;: {
    object (StandardSqlDataType)
  },
  &quot;transformSql&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  name  `

`  string  `

Output only. Name of the column.

`  type  `

`  object ( StandardSqlDataType  ` )

Output only. Data type of the column after the transform.

`  transformSql  `

`  string  `

Output only. The SQL expression used in the column transform.

## HparamSearchSpaces

Hyperparameter search spaces. These should be a subset of trainingOptions.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;learnRate&quot;: {
    object (DoubleHparamSearchSpace)
  },
  &quot;l1Reg&quot;: {
    object (DoubleHparamSearchSpace)
  },
  &quot;l2Reg&quot;: {
    object (DoubleHparamSearchSpace)
  },
  &quot;numClusters&quot;: {
    object (IntHparamSearchSpace)
  },
  &quot;numFactors&quot;: {
    object (IntHparamSearchSpace)
  },
  &quot;hiddenUnits&quot;: {
    object (IntArrayHparamSearchSpace)
  },
  &quot;batchSize&quot;: {
    object (IntHparamSearchSpace)
  },
  &quot;dropout&quot;: {
    object (DoubleHparamSearchSpace)
  },
  &quot;maxTreeDepth&quot;: {
    object (IntHparamSearchSpace)
  },
  &quot;subsample&quot;: {
    object (DoubleHparamSearchSpace)
  },
  &quot;minSplitLoss&quot;: {
    object (DoubleHparamSearchSpace)
  },
  &quot;walsAlpha&quot;: {
    object (DoubleHparamSearchSpace)
  },
  &quot;boosterType&quot;: {
    object (StringHparamSearchSpace)
  },
  &quot;numParallelTree&quot;: {
    object (IntHparamSearchSpace)
  },
  &quot;dartNormalizeType&quot;: {
    object (StringHparamSearchSpace)
  },
  &quot;treeMethod&quot;: {
    object (StringHparamSearchSpace)
  },
  &quot;minTreeChildWeight&quot;: {
    object (IntHparamSearchSpace)
  },
  &quot;colsampleBytree&quot;: {
    object (DoubleHparamSearchSpace)
  },
  &quot;colsampleBylevel&quot;: {
    object (DoubleHparamSearchSpace)
  },
  &quot;colsampleBynode&quot;: {
    object (DoubleHparamSearchSpace)
  },
  &quot;activationFn&quot;: {
    object (StringHparamSearchSpace)
  },
  &quot;optimizer&quot;: {
    object (StringHparamSearchSpace)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  learnRate  `

`  object ( DoubleHparamSearchSpace  ` )

Learning rate of training jobs.

`  l1Reg  `

`  object ( DoubleHparamSearchSpace  ` )

L1 regularization coefficient.

`  l2Reg  `

`  object ( DoubleHparamSearchSpace  ` )

L2 regularization coefficient.

`  numClusters  `

`  object ( IntHparamSearchSpace  ` )

Number of clusters for k-means.

`  numFactors  `

`  object ( IntHparamSearchSpace  ` )

Number of latent factors to train on.

`  hiddenUnits  `

`  object ( IntArrayHparamSearchSpace  ` )

Hidden units for neural network models.

`  batchSize  `

`  object ( IntHparamSearchSpace  ` )

Mini batch sample size.

`  dropout  `

`  object ( DoubleHparamSearchSpace  ` )

Dropout probability for dnn model training and boosted tree models using dart booster.

`  maxTreeDepth  `

`  object ( IntHparamSearchSpace  ` )

Maximum depth of a tree for boosted tree models.

`  subsample  `

`  object ( DoubleHparamSearchSpace  ` )

Subsample the training data to grow tree to prevent overfitting for boosted tree models.

`  minSplitLoss  `

`  object ( DoubleHparamSearchSpace  ` )

Minimum split loss for boosted tree models.

`  walsAlpha  `

`  object ( DoubleHparamSearchSpace  ` )

Hyperparameter for matrix factoration when implicit feedback type is specified.

`  boosterType  `

`  object ( StringHparamSearchSpace  ` )

Booster type for boosted tree models.

`  numParallelTree  `

`  object ( IntHparamSearchSpace  ` )

Number of parallel trees for boosted tree models.

`  dartNormalizeType  `

`  object ( StringHparamSearchSpace  ` )

Dart normalization type for boosted tree models.

`  treeMethod  `

`  object ( StringHparamSearchSpace  ` )

Tree construction algorithm for boosted tree models.

`  minTreeChildWeight  `

`  object ( IntHparamSearchSpace  ` )

Minimum sum of instance weight needed in a child for boosted tree models.

`  colsampleBytree  `

`  object ( DoubleHparamSearchSpace  ` )

Subsample ratio of columns when constructing each tree for boosted tree models.

`  colsampleBylevel  `

`  object ( DoubleHparamSearchSpace  ` )

Subsample ratio of columns for each level for boosted tree models.

`  colsampleBynode  `

`  object ( DoubleHparamSearchSpace  ` )

Subsample ratio of columns for each node(split) for boosted tree models.

`  activationFn  `

`  object ( StringHparamSearchSpace  ` )

Activation functions of neural network models.

`  optimizer  `

`  object ( StringHparamSearchSpace  ` )

Optimizer of TF models.

## DoubleHparamSearchSpace

Search space for a double hyperparameter.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{

  // Union field search_space can be only one of the following:
  &quot;range&quot;: {
    object (DoubleRange)
  },
  &quot;candidates&quot;: {
    object (DoubleCandidates)
  }
  // End of list of possible types for union field search_space.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `  search_space  ` . Search space. `  search_space  ` can be only one of the following:

`  range  `

`  object ( DoubleRange  ` )

Range of the double hyperparameter.

`  candidates  `

`  object ( DoubleCandidates  ` )

Candidates of the double hyperparameter.

## DoubleRange

Range of a double hyperparameter.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;min&quot;: number,
  &quot;max&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  min  `

`  number  `

Min value of the double parameter.

`  max  `

`  number  `

Max value of the double parameter.

## DoubleCandidates

Discrete candidates of a double hyperparameter.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;candidates&quot;: [
    number
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  candidates[]  `

`  number  `

Candidates for the double parameter in increasing order.

## IntHparamSearchSpace

Search space for an int hyperparameter.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{

  // Union field search_space can be only one of the following:
  &quot;range&quot;: {
    object (IntRange)
  },
  &quot;candidates&quot;: {
    object (IntCandidates)
  }
  // End of list of possible types for union field search_space.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `  search_space  ` . Search space. `  search_space  ` can be only one of the following:

`  range  `

`  object ( IntRange  ` )

Range of the int hyperparameter.

`  candidates  `

`  object ( IntCandidates  ` )

Candidates of the int hyperparameter.

## IntRange

Range of an int hyperparameter.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;min&quot;: string,
  &quot;max&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  min  `

`  string ( Int64Value format)  `

Min value of the int parameter.

`  max  `

`  string ( Int64Value format)  `

Max value of the int parameter.

## IntCandidates

Discrete candidates of an int hyperparameter.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;candidates&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  candidates[]  `

`  string ( Int64Value format)  `

Candidates for the int parameter in increasing order.

## IntArrayHparamSearchSpace

Search space for int array.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;candidates&quot;: [
    {
      object (IntArray)
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  candidates[]  `

`  object ( IntArray  ` )

Candidates for the int array parameter.

## IntArray

An array of int.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;elements&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  elements[]  `

`  string ( int64 format)  `

Elements in the int array.

## StringHparamSearchSpace

Search space for string and enum.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;candidates&quot;: [
    string
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  candidates[]  `

`  string  `

Canididates for the string or enum parameter in lower case.

## HparamTuningTrial

Training info of a trial in [hyperparameter tuning](https://cloud.google.com/bigquery-ml/docs/reference/standard-sql/bigqueryml-syntax-hp-tuning-overview) models.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;trialId&quot;: string,
  &quot;startTimeMs&quot;: string,
  &quot;endTimeMs&quot;: string,
  &quot;hparams&quot;: {
    object (TrainingOptions)
  },
  &quot;evaluationMetrics&quot;: {
    object (EvaluationMetrics)
  },
  &quot;status&quot;: enum (TrialStatus),
  &quot;errorMessage&quot;: string,
  &quot;trainingLoss&quot;: number,
  &quot;evalLoss&quot;: number,
  &quot;hparamTuningEvaluationMetrics&quot;: {
    object (EvaluationMetrics)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  trialId  `

`  string ( int64 format)  `

1-based index of the trial.

`  startTimeMs  `

`  string ( int64 format)  `

Starting time of the trial.

`  endTimeMs  `

`  string ( int64 format)  `

Ending time of the trial.

`  hparams  `

`  object ( TrainingOptions  ` )

The hyperprameters selected for this trial.

`  evaluationMetrics  `

`  object ( EvaluationMetrics  ` )

Evaluation metrics of this trial calculated on the test data. Empty in Job API.

`  status  `

`  enum ( TrialStatus  ` )

The status of the trial.

`  errorMessage  `

`  string  `

Error message for FAILED and INFEASIBLE trial.

`  trainingLoss  `

`  number  `

Loss computed on the training data at the end of trial.

`  evalLoss  `

`  number  `

Loss computed on the eval data at the end of trial.

`  hparamTuningEvaluationMetrics  `

`  object ( EvaluationMetrics  ` )

Hyperparameter tuning evaluation metrics of this trial calculated on the eval data. Unlike evaluationMetrics, only the fields corresponding to the hparamTuningObjectives are set.

## TrialStatus

Current status of the trial.

Enums

`  TRIAL_STATUS_UNSPECIFIED  `

Default value.

`  NOT_STARTED  `

Scheduled but not started.

`  RUNNING  `

Running state.

`  SUCCEEDED  `

The trial succeeded.

`  FAILED  `

The trial failed.

`  INFEASIBLE  `

The trial is infeasible due to the invalid params.

`  STOPPED_EARLY  `

Trial stopped early because it's not promising.

## RemoteModelInfo

Remote Model Info

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;connection&quot;: string,
  &quot;maxBatchingRows&quot;: string,
  &quot;remoteModelVersion&quot;: string,

  // Union field remote_service can be only one of the following:
  &quot;endpoint&quot;: string,
  &quot;remoteServiceType&quot;: enum (RemoteServiceType)
  // End of list of possible types for union field remote_service.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  connection  `

`  string  `

Output only. Fully qualified name of the user-provided connection object of the remote model. Format: `  "projects/{projectId}/locations/{locationId}/connections/{connectionId}"  `

`  maxBatchingRows  `

`  string ( int64 format)  `

Output only. Max number of rows in each batch sent to the remote service. If unset, the number of rows in each batch is set dynamically.

`  remoteModelVersion  `

`  string  `

Output only. The model version for LLM.

Union field `  remote_service  ` . Remote services are services outside of BigQuery used by remote models for predictions. A remote service is backed by either an arbitrary endpoint or a selected remote service type, but not both. `  remote_service  ` can be only one of the following:

`  endpoint  `

`  string  `

Output only. The endpoint for remote model.

`  remoteServiceType  `

`  enum ( RemoteServiceType  ` )

Output only. The remote service type for remote model.

## RemoteServiceType

Supported service type for remote model.

Enums

`  REMOTE_SERVICE_TYPE_UNSPECIFIED  `

Unspecified remote service type.

`  CLOUD_AI_TRANSLATE_V3  `

V3 Cloud AI Translation API. See more details at [Cloud Translation API](https://cloud.google.com/translate/docs/reference/rest) .

`  CLOUD_AI_VISION_V1  `

V1 Cloud AI Vision API See more details at [Cloud Vision API](https://cloud.google.com/vision/docs/reference/rest) .

`  CLOUD_AI_NATURAL_LANGUAGE_V1  `

V1 Cloud AI Natural Language API. See more details at [REST Resource: documents](https://cloud.google.com/natural-language/docs/reference/rest/v1/documents) .

## Methods

### `             delete           `

Deletes the model specified by modelId from the dataset.

### `             get           `

Gets the specified model resource by model ID.

### `             list           `

Lists all models in the specified dataset.

### `             patch           `

Patch specific fields in the specified model.
