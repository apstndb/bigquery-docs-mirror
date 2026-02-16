# Export models

This page shows you how to export BigQuery ML models. You can export BigQuery ML models to Cloud Storage, and use them for online prediction, or edit them in Python. You can export a BigQuery ML model by:

  - Using the [Google Cloud console](/bigquery/docs/exporting-models) .
  - Using the [`  EXPORT MODEL  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-export-model) statement.
  - Using the `  bq extract  ` command in the bq command-line tool.
  - Submitting an [`  extract  `](/bigquery/docs/reference/rest/v2/Job#JobConfiguration) job through the API or client libraries.

You can export the following model types:

  - `  AUTOENCODER  `
  - `  AUTOML_CLASSIFIER  `
  - `  AUTOML_REGRESSOR  `
  - `  BOOSTED_TREE_CLASSIFIER  `
  - `  BOOSTED_TREE_REGRESSOR  `
  - `  DNN_CLASSIFIER  `
  - `  DNN_REGRESSOR  `
  - `  DNN_LINEAR_COMBINED_CLASSIFIER  `
  - `  DNN_LINEAR_COMBINED_REGRESSOR  `
  - `  KMEANS  `
  - `  LINEAR_REG  `
  - `  LOGISTIC_REG  `
  - `  MATRIX_FACTORIZATION  `
  - `  RANDOM_FOREST_CLASSIFIER  `
  - `  RANDOM_FOREST_REGRESSOR  `
  - `  TENSORFLOW  ` (imported TensorFlow models)
  - `  PCA  `
  - `  TRANSFORM_ONLY  `

## Export model formats and samples

The following table shows the export destination formats for each BigQuery ML model type and provides a sample of files that get written in the Cloud Storage bucket.

Model type

Export model format

Exported files sample

AUTOML\_CLASSIFIER

[TensorFlow SavedModel](https://www.tensorflow.org/guide/saved_model) (TF 2.1.0)

`  gcs_bucket/ assets/ f1.txt f2.txt saved_model.pb variables/ variables.data-00-of-01 variables.index  `

AUTOML\_REGRESSOR

AUTOENCODER

[TensorFlow SavedModel](https://www.tensorflow.org/guide/saved_model) (TF 1.15 or higher)

DNN\_CLASSIFIER

DNN\_REGRESSOR

DNN\_LINEAR\_COMBINED\_CLASSIFIER

DNN\_LINEAR\_COMBINED\_REGRESSOR

KMEANS

LINEAR\_REGRESSOR

LOGISTIC\_REG

MATRIX\_FACTORIZATION

PCA

TRANSFORM\_ONLY

BOOSTED\_TREE\_CLASSIFIER

Booster (XGBoost 0.82)

`  gcs_bucket/ assets/ 0.txt 1.txt model_metadata.json main.py model.bst xgboost_predictor-0.1.tar.gz .... predictor.py ....  `  
  
`  main.py  ` is for local run. See [Model deployment](#model-deployment) for more details.

BOOSTED\_TREE\_REGRESSOR

RANDOM\_FOREST\_REGRESSOR

RANDOM\_FOREST\_REGRESSOR

TENSORFLOW (imported)

[TensorFlow SavedModel](https://www.tensorflow.org/guide/saved_model)

Exactly the same files that were present when importing the model

**Note:** The [automatic data preprocessing](/bigquery/docs/auto-preprocessing) performed during model creation, such as standardization and label encoding, is saved in the exported files as part of the graph for TensorFlow SavedModel, and in the external files for Booster. Explicit preprocessing is unneeded before passing data for prediction. Input should generally match that used for BigQuery ML [`  ML.PREDICT  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-predict) . All numerical values in the exported model signatures are cast as data type `  FLOAT64  ` . Also, all `  STRUCT  ` fields must be expanded into separate fields. For example, field `  f1  ` in `  STRUCT f2  ` should be renamed as `  f2_f1  ` and passed as a separate column.

## Export model trained with `     TRANSFORM    `

If the model is trained with the [`  TRANSFORM  ` clause](/bigquery/docs/bigqueryml-transform) , then an additional preprocessing model performs the same logic in the [`  TRANSFORM  ` clause](/bigquery/docs/bigqueryml-transform) and is saved in the TensorFlow SavedModel format under the subdirectory `  transform  ` . You can deploy a model trained with the [`  TRANSFORM  ` clause](/bigquery/docs/bigqueryml-transform) to Vertex AI as well as locally. For more information, see [model deployment](/bigquery/docs/exporting-models#model-deployment) .

Export model format

Exported files sample

Prediction model: [TensorFlow SavedModel](https://www.tensorflow.org/guide/saved_model) or Booster (XGBoost 0.82).  
Preprocessing model for TRANSFORM clause: [TensorFlow SavedModel](https://www.tensorflow.org/guide/saved_model) (TF 2.5 or higher)

`  gcs_bucket/ ....(model files) transform/ assets/ f1.txt/ f2.txt/ saved_model.pb variables/ variables.data-00-of-01 variables.index  `

The model doesn't contain the information about the feature engineering performed outside the [`  TRANSFORM  ` clause](/bigquery/docs/bigqueryml-transform) during training. For example, anything in the `  SELECT  ` statement . So you would need to manually convert the input data before feeding into the preprocessing model.

### Supported data types

When exporting models trained with the [`  TRANSFORM  ` clause](/bigquery/docs/bigqueryml-transform) , the following data types are supported for feeding into the [`  TRANSFORM  ` clause](/bigquery/docs/bigqueryml-transform) .

<table>
<thead>
<tr class="header">
<th>TRANSFORM input type</th>
<th>TRANSFORM input samples</th>
<th>Exported preprocessing model input samples</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>INT64</td>
<td><code dir="ltr" translate="no">       10,              11      </code></td>
<td><code dir="ltr" translate="no">       tf.constant(              [10, 11],              dtype=tf.int64)      </code></td>
</tr>
<tr class="even">
<td>NUMERIC</td>
<td><code dir="ltr" translate="no">       NUMERIC 10,              NUMERIC 11      </code></td>
<td><code dir="ltr" translate="no">       tf.constant(              [10, 11],              dtype=tf.float64)      </code></td>
</tr>
<tr class="odd">
<td>BIGNUMERIC</td>
<td><code dir="ltr" translate="no">       BIGNUMERIC 10,              BIGNUMERIC 11      </code></td>
<td><code dir="ltr" translate="no">       tf.constant(              [10, 11],              dtype=tf.float64)      </code></td>
</tr>
<tr class="even">
<td>FLOAT64</td>
<td><code dir="ltr" translate="no">       10.0,              11.0      </code></td>
<td><code dir="ltr" translate="no">       tf.constant(              [10, 11],              dtype=tf.float64)      </code></td>
</tr>
<tr class="odd">
<td>BOOL</td>
<td><code dir="ltr" translate="no">       TRUE,              FALSE      </code></td>
<td><code dir="ltr" translate="no">       tf.constant(              [True, False],              dtype=tf.bool)      </code></td>
</tr>
<tr class="even">
<td>STRING</td>
<td><code dir="ltr" translate="no">       'abc',              'def'      </code></td>
<td><code dir="ltr" translate="no">       tf.constant(              ['abc', 'def'],              dtype=tf.string)      </code></td>
</tr>
<tr class="odd">
<td>BYTES</td>
<td><code dir="ltr" translate="no">       b'abc',              b'def'      </code></td>
<td><code dir="ltr" translate="no">       tf.constant(              ['abc', 'def'],              dtype=tf.string)      </code></td>
</tr>
<tr class="even">
<td>DATE</td>
<td><code dir="ltr" translate="no">       DATE '2020-09-27',              DATE '2020-09-28'      </code></td>
<td><code dir="ltr" translate="no">       tf.constant(              [              '2020-09-27',              '2020-09-28'              ],              dtype=tf.string)               "%F" format      </code></td>
</tr>
<tr class="odd">
<td>DATETIME</td>
<td><code dir="ltr" translate="no">       DATETIME '2023-02-02 02:02:01.152903',              DATETIME '2023-02-03 02:02:01.152903'      </code></td>
<td><code dir="ltr" translate="no">       tf.constant(              [              '2023-02-02 02:02:01.152903',              '2023-02-03 02:02:01.152903'              ],              dtype=tf.string)               "%F %H:%M:%E6S" format      </code></td>
</tr>
<tr class="even">
<td>TIME</td>
<td><code dir="ltr" translate="no">       TIME '16:32:36.152903',              TIME '17:32:36.152903'      </code></td>
<td><code dir="ltr" translate="no">       tf.constant(              [              '16:32:36.152903',              '17:32:36.152903'              ],              dtype=tf.string)               "%H:%M:%E6S" format      </code></td>
</tr>
<tr class="odd">
<td>TIMESTAMP</td>
<td><code dir="ltr" translate="no">       TIMESTAMP '2017-02-28 12:30:30.45-08',              TIMESTAMP '2018-02-28 12:30:30.45-08'      </code></td>
<td><code dir="ltr" translate="no">       tf.constant(              [              '2017-02-28 20:30:30.4 +0000',              '2018-02-28 20:30:30.4 +0000'              ],              dtype=tf.string)               "%F %H:%M:%E1S %z" format      </code></td>
</tr>
<tr class="even">
<td>ARRAY</td>
<td><code dir="ltr" translate="no">       ['a', 'b'],              ['c', 'd']      </code></td>
<td><code dir="ltr" translate="no">       tf.constant(              [['a', 'b'], ['c', 'd']],              dtype=tf.string)      </code></td>
</tr>
<tr class="odd">
<td>ARRAY&lt; STRUCT&lt; INT64, FLOAT64&gt;&gt;</td>
<td><code dir="ltr" translate="no">       [(1, 1.0), (2, 1.0)],              [(2, 1.0), (3, 1.0)]      </code></td>
<td><code dir="ltr" translate="no">       tf.sparse.from_dense(              tf.constant(              [              [0, 1.0, 1.0, 0],              [0, 0, 1.0, 1.0]              ],              dtype=tf.float64))      </code></td>
</tr>
<tr class="even">
<td>NULL</td>
<td><code dir="ltr" translate="no">       NULL,              NULL      </code></td>
<td><code dir="ltr" translate="no">       tf.constant(              [123456789.0e10, 123456789.0e10],              dtype=tf.float64)               tf.constant(              [1234567890000000000, 1234567890000000000],              dtype=tf.int64)               tf.constant(              [' __MISSING__ ', ' __MISSING__ '],              dtype=tf.string)      </code></td>
</tr>
</tbody>
</table>

### Supported SQL functions

When exporting models trained with the [`  TRANSFORM  ` clause](/bigquery/docs/bigqueryml-transform) , you can use the following SQL functions inside the [`  TRANSFORM  ` clause](/bigquery/docs/bigqueryml-transform) .

  - [Operators](/bigquery/docs/reference/standard-sql/operators)
      - `  +  ` , `  -  ` , `  *  ` , `  /  ` , `  =  ` , `  <  ` , `  >  ` , `  <=  ` , `  >=  ` , `  !=  ` , `  <>  ` , `  [NOT] BETWEEN  ` , `  [NOT] IN  ` , `  IS [NOT] NULL  ` , `  IS [NOT] TRUE  ` , `  IS [NOT] FALSE  ` , `  NOT  ` , `  AND  ` , `  OR  ` .
  - [Conditional expressions](/bigquery/docs/reference/standard-sql/conditional_expressions)
      - `  CASE expr  ` , `  CASE  ` , `  COALESCE  ` , `  IF  ` , `  IFNULL  ` , `  NULLIF  ` .
  - [Mathematical functions](/bigquery/docs/reference/standard-sql/mathematical_functions)
      - `  ABS  ` , `  ACOS  ` , `  ACOSH  ` , `  ASINH  ` , `  ATAN  ` , `  ATAN2  ` , `  ATANH  ` , `  CBRT  ` , `  CEIL  ` , `  CEILING  ` , `  COS  ` , `  COSH  ` , `  COT  ` , `  COTH  ` , `  CSC  ` , `  CSCH  ` , `  EXP  ` , `  FLOOR  ` , `  IS_INF  ` , `  IS_NAN  ` , `  LN  ` , `  LOG  ` , `  LOG10  ` , `  MOD  ` , `  POW  ` , `  POWER  ` , `  SEC  ` , `  SECH  ` , `  SIGN  ` , `  SIN  ` , `  SINH  ` , `  SQRT  ` , `  TAN  ` , `  TANH  ` .
  - [Conversion functions](/bigquery/docs/reference/standard-sql/conversion_functions)
      - `  CAST AS INT64  ` , `  CAST AS FLOAT64  ` , `  CAST AS NUMERIC  ` , `  CAST AS BIGNUMERIC  ` , `  CAST AS STRING  ` , `  SAFE_CAST AS INT64  ` , `  SAFE_CAST AS FLOAT64  `
  - [String functions](/bigquery/docs/reference/standard-sql/string_functions)
      - `  CONCAT  ` , `  LEFT  ` , `  LENGTH  ` , `  LOWER  ` , `  REGEXP_REPLACE  ` , `  RIGHT  ` , `  SPLIT  ` , `  SUBSTR  ` , `  SUBSTRING  ` , `  TRIM  ` , `  UPPER  ` .
  - [Date functions](/bigquery/docs/reference/standard-sql/date_functions)
      - `  Date  ` , `  DATE_ADD  ` , `  DATE_SUB  ` , `  DATE_DIFF  ` , `  DATE_TRUNC  ` , `  EXTRACT  ` , `  FORMAT_DATE  ` , `  PARSE_DATE  ` , `  SAFE.PARSE_DATE  ` .
  - [Datetime functions](/bigquery/docs/reference/standard-sql/datetime_functions)
      - `  DATETIME  ` , `  DATETIME_ADD  ` , `  DATETIME_SUB  ` , `  DATETIME_DIFF  ` , `  DATETIME_TRUNC  ` , `  EXTRACT  ` , `  PARSE_DATETIME  ` , `  SAFE.PARSE_DATETIME  ` .
  - [Time functions](/bigquery/docs/reference/standard-sql/time_functions)
      - `  TIME  ` , `  TIME_ADD  ` , `  TIME_SUB  ` , `  TIME_DIFF  ` , `  TIME_TRUNC  ` , `  EXTRACT  ` , `  FORMAT_TIME  ` , `  PARSE_TIME  ` , `  SAFE.PARSE_TIME  ` .
  - [Timestamp functions](/bigquery/docs/reference/standard-sql/timestamp_functions)
      - `  TIMESTAMP  ` , `  TIMESTAMP_ADD  ` , `  TIMESTAMP_SUB  ` , `  TIMESTAMP_DIFF  ` , `  TIMESTAMP_TRUNC  ` , `  FORMAT_TIMESTAMP  ` , `  PARSE_TIMESTAMP  ` , `  SAFE.PARSE_TIMESTAMP  ` , `  TIMESTAMP_MICROS  ` , `  TIMESTAMP_MILLIS  ` , `  TIMESTAMP_SECONDS  ` , `  EXTRACT  ` , `  STRING  ` , `  UNIX_MICROS  ` , `  UNIX_MILLIS  ` , `  UNIX_SECONDS  ` .
  - [Manual preprocessing functions](/bigquery/docs/manual-preprocessing)
      - `  ML.IMPUTER  ` , `  ML.HASH_BUCKETIZE  ` , `  ML.LABEL_ENCODER  ` , `  ML.MULTI_HOT_ENCODER  ` , `  ML.NGRAMS  ` , `  ML.ONE_HOT_ENCODER  ` , `  ML.BUCKETIZE  ` , `  ML.MAX_ABS_SCALER  ` , `  ML.MIN_MAX_SCALER  ` , `  ML.NORMALIZER  ` , `  ML.QUANTILE_BUCKETIZE  ` , `  ML.ROBUST_SCALER  ` , `  ML.STANDARD_SCALER  ` .

## Limitations

The following limitations apply when exporting models:

  - Model export is not supported if any of the following features were used during training:
    
      - `  ARRAY  ` , `  TIMESTAMP  ` , or `  GEOGRAPHY  ` feature types were present in the input data.

  - Exported models for model types `  AUTOML_REGRESSOR  ` and `  AUTOML_CLASSIFIER  ` do not support Vertex AI deployment for online prediction.

  - The model size limit is 1 GB for matrix factorization model export. The model size is roughly proportional to `  num_factors  ` , so you can reduce `  num_factors  ` during training to shrink the model size if you reach the limit.

  - For models trained with the [BigQuery ML `  TRANSFORM  ` clause](/bigquery/docs/bigqueryml-transform) for [manual feature preprocessing](/bigquery/docs/manual-preprocessing) , see the [data types](/bigquery/docs/exporting-models#export-transform-types) and [functions](/bigquery/docs/exporting-models#export-transform-functions) supported for exporting.

  - Models trained with the [BigQuery ML `  TRANSFORM  ` clause](/bigquery/docs/bigqueryml-transform) before 18 September 2023 must be re-trained before they can be [deployed through Model Registry](/bigquery/docs/managing-models-vertex) for online prediction.

  - During model export, `  ARRAY<STRUCT<INT64, FLOAT64>>  ` , `  ARRAY  ` and `  TIMESTAMP  ` are supported as pre-transformed data, but are not supported as post-transformed data.

## Export BigQuery ML models

To export a model, select one of the following:

### Console

1.  Open the BigQuery page in the Google Cloud console.  

2.  In the left pane, click explore **Explorer** :
    
    If you don't see the left pane, click last\_page **Expand left pane** to open the pane.

3.  In the **Explorer** pane, expand your project, click **Datasets** , and then click your dataset.

4.  Click **Overview \> Models** and click the model name that you're exporting.

5.  Click **More \> Export** :

6.  In the **Export model to Google Cloud Storage** dialog:
    
      - For **Select GCS location** , browse for the bucket or folder location where you want to to export the model, and click **Select** .
      - Click **Submit** to export the model.

To check on the progress of the job, in the **Explorer** pane, click **Job history** , and look for an **EXTRACT** type job.

### SQL

The `  EXPORT MODEL  ` statement lets you export BigQuery ML models to [Cloud Storage](/storage/docs) using [GoogleSQL](/bigquery/docs/reference/standard-sql) query syntax.

To export a BigQuery ML model in the Google Cloud console by using the `  EXPORT MODEL  ` statement, follow these steps:

1.  In the Google Cloud console, open the BigQuery page.

2.  Click **Compose new query** .

3.  In the **Query editor** field, type your [`  EXPORT MODEL  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-export-model) statement.
    
    The following query exports a model named `  myproject.mydataset.mymodel  ` to a Cloud Storage bucket with [URI](/bigquery/docs/batch-loading-data#gcs-uri) `  gs://bucket/path/to/saved_model/  ` .
    
    ``` text
     EXPORT MODEL `myproject.mydataset.mymodel`
     OPTIONS(URI = 'gs://bucket/path/to/saved_model/')
     
    ```

4.  Click **Run** . When the query is complete, the following appears in the **Query results** pane: `  Successfully exported model  ` .

### bq

**Note:** To export a model using the bq command-line tool, you must have bq tool version 2.0.56 or later, which is included with gcloud CLI [version 287.0.0](/sdk/docs/release-notes#28700_2020-04-01) and later. To see your installed bq tool version, use [`  bq version  `](/bigquery/docs/bq-command-line-tool#getting_help) and, if needed, update the gcloud CLI using [`  gcloud components update  `](/sdk/gcloud/reference/components/update) .

Use the `  bq extract  ` command with the `  --model  ` flag.

(Optional) Supply the `  --destination_format  ` flag and pick the format of the model exported. (Optional) Supply the `  --location  ` flag and set the value to your [location](/bigquery/docs/locations) .

``` text
bq --location=location extract \
--destination_format format \
--model project_id:dataset.model \
gs://bucket/model_folder
```

Where:

  - location is the name of your location. The `  --location  ` flag is optional. For example, if you are using BigQuery in the Tokyo region, you can set the flag's value to `  asia-northeast1  ` . You can set a default value for the location using the [.bigqueryrc file](/bigquery/docs/bq-command-line-tool#setting_default_values_for_command-line_flags) .
  - destination\_format is the format for the exported model: `  ML_TF_SAVED_MODEL  ` (default), or `  ML_XGBOOST_BOOSTER  ` .
  - project\_id is your project ID.
  - dataset is the name of the source dataset.
  - model is the model you're exporting.
  - bucket is the name of the Cloud Storage bucket to which you're exporting the data. The BigQuery dataset and the Cloud Storage bucket must be in the same [location](/bigquery/docs/locations) .
  - model\_folder is the name of the folder where the exported model files will be written.

Examples:

For example, the following command exports `  mydataset.mymodel  ` in TensorFlow SavedModel format to a Cloud Storage bucket named `  mymodel_folder  ` .

``` text
bq extract --model \
'mydataset.mymodel' \
gs://example-bucket/mymodel_folder
```

The default value of destination\_format is `  ML_TF_SAVED_MODEL  ` .

The following command exports `  mydataset.mymodel  ` in XGBoost Booster format to a Cloud Storage bucket named `  mymodel_folder  ` .

``` text
bq extract --model \
--destination_format ML_XGBOOST_BOOSTER \
'mydataset.mytable' \
gs://example-bucket/mymodel_folder
```

### API

To export model, create an `  extract  ` job and populate the job configuration.

(Optional) Specify your location in the `  location  ` property in the `  jobReference  ` section of the [job resource](/bigquery/docs/reference/rest/v2/jobs) .

1.  Create an extract job that points to the BigQuery ML model and the Cloud Storage destination.

2.  Specify the source model by using the `  sourceModel  ` configuration object that contains the project ID, dataset ID, and model ID.

3.  The `  destination URI(s)  ` property must be fully-qualified, in the format gs:// bucket / model\_folder .

4.  Specify the destination format by setting the `  configuration.extract.destinationFormat  ` property. For example, to export a boosted tree model, set this property to the value `  ML_XGBOOST_BOOSTER  ` .

5.  To check the job status, call [jobs.get( job\_id )](/bigquery/docs/reference/v2/jobs/get) with the ID of the job returned by the initial request.
    
      - If `  status.state = DONE  ` , the job completed successfully.
      - If the `  status.errorResult  ` property is present, the request failed, and that object will include information describing what went wrong.
      - If `  status.errorResult  ` is absent, the job finished successfully, although there might have been some non-fatal errors. Non-fatal errors are listed in the returned job object's `  status.errors  ` property.

**API notes:**

  - As a best practice, generate a unique ID and pass it as `  jobReference.jobId  ` when calling `  jobs.insert  ` to create a job. This approach is more robust to network failure because the client can poll or retry on the known job ID.

  - Calling `  jobs.insert  ` on a given job ID is idempotent; in other words, you can retry as many times as you like on the same job ID, and at most one of those operations will succeed.

### Java

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` java
import com.google.cloud.bigquery.BigQuery;
import com.google.cloud.bigquery.BigQueryException;
import com.google.cloud.bigquery.BigQueryOptions;
import com.google.cloud.bigquery.ExtractJobConfiguration;
import com.google.cloud.bigquery.Job;
import com.google.cloud.bigquery.JobInfo;
import com.google.cloud.bigquery.ModelId;

// Sample to extract model to GCS bucket
public class ExtractModel {

  public static void main(String[] args) throws InterruptedException {
    // TODO(developer): Replace these variables before running the sample.
    String projectName = "bigquery-public-data";
    String datasetName = "samples";
    String modelName = "model";
    String bucketName = "MY-BUCKET-NAME";
    String destinationUri = "gs://" + bucketName + "/path/to/file";
    extractModel(projectName, datasetName, modelName, destinationUri);
  }

  public static void extractModel(
      String projectName, String datasetName, String modelName, String destinationUri)
      throws InterruptedException {
    try {
      // Initialize client that will be used to send requests. This client only needs to be created
      // once, and can be reused for multiple requests.
      BigQuery bigquery = BigQueryOptions.getDefaultInstance().getService();

      ModelId modelId = ModelId.of(projectName, datasetName, modelName);

      ExtractJobConfiguration extractConfig =
          ExtractJobConfiguration.newBuilder(modelId, destinationUri).build();

      Job job = bigquery.create(JobInfo.of(extractConfig));

      // Blocks until this job completes its execution, either failing or succeeding.
      Job completedJob = job.waitFor();
      if (completedJob == null) {
        System.out.println("Job not executed since it no longer exists.");
        return;
      } else if (completedJob.getStatus().getError() != null) {
        System.out.println(
            "BigQuery was unable to extract due to an error: \n" + job.getStatus().getError());
        return;
      }
      System.out.println("Model extract successful");
    } catch (BigQueryException ex) {
      System.out.println("Model extraction job was interrupted. \n" + ex.toString());
    }
  }
}
```

## Model deployment

You can deploy the exported model to Vertex AI as well as locally. If the model's [`  TRANSFORM  ` clause](/bigquery/docs/bigqueryml-transform) contains Date functions, Datetime functions, Time functions or Timestamp functions, you must use [bigquery-ml-utils library](https://pypi.org/project/bigquery-ml-utils/) in the container. The exception is if you are [deploying through Model Registry](/bigquery/docs/managing-models-vertex) , which does not need exported models or serving containers.

### Vertex AI deployment

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Export model format</th>
<th>Deployment</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>TensorFlow SavedModel (non-AutoML models)</td>
<td><a href="/vertex-ai/docs/general/deployment">Deploy a TensorFlow SavedModel</a> . You must create the SavedModel file using a <a href="/vertex-ai/docs/supported-frameworks-list#tensorflow">supported version</a> of TensorFlow.</td>
</tr>
<tr class="even">
<td>TensorFlow SavedModel (AutoML models)</td>
<td>Not supported.</td>
</tr>
<tr class="odd">
<td>XGBoost Booster</td>
<td>Use a <a href="/vertex-ai/docs/predictions/custom-prediction-routines">custom prediction routine</a> . For XGBoost Booster models, preprocessing and postprocessing information is saved in the exported files, and a custom prediction routine lets you deploy the model with the extra exported files.<br />
<br />
You must create the model files using a <a href="/vertex-ai/docs/supported-frameworks-list#xgboost_2">supported version</a> of XGBoost.</td>
</tr>
</tbody>
</table>

### Local deployment

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Export model format</th>
<th>Deployment</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>TensorFlow SavedModel (non-AutoML models)</td>
<td>SavedModel is a standard format, and you can deploy them in <a href="https://www.tensorflow.org/tfx/serving/serving_basic">TensorFlow Serving docker container</a> .<br />
<br />
You can also leverage the <a href="/vertex-ai/docs/training/containerize-run-code-local">local run</a> of Vertex AI online prediction.</td>
</tr>
<tr class="even">
<td>TensorFlow SavedModel (AutoML models)</td>
<td><a href="/vertex-ai/docs/training/containerize-run-code-local">Containerize and run the model</a> .</td>
</tr>
<tr class="odd">
<td>XGBoost Booster</td>
<td>To run XGBoost Booster models locally, you can use the exported <code dir="ltr" translate="no">       main.py      </code> file:
<ol>
<li>Download all of the files from Cloud Storage to the local directory.</li>
<li>Unzip the <code dir="ltr" translate="no">         predictor.py        </code> file from <code dir="ltr" translate="no">         xgboost_predictor-0.1.tar.gz        </code> to the local directory.</li>
<li>Run <code dir="ltr" translate="no">         main.py        </code> (see instructions in <code dir="ltr" translate="no">         main.py        </code> ).</li>
</ol></td>
</tr>
</tbody>
</table>

## Prediction output format

This section provides the prediction output format of the exported models for each model type. All exported models support batch prediction; they can handle multiple input rows at a time. For example, there are two input rows in each of the following output format examples.

### AUTOENCODER

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Prediction output format</th>
<th>Output sample</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded=""><code>+------------------------+------------------------+------------------------+
|      LATENT_COL_1      |      LATENT_COL_2      |           ...          |
+------------------------+------------------------+------------------------+
|       [FLOAT]          |         [FLOAT]        |           ...          |
+------------------------+------------------------+------------------------+
        </code></pre></td>
<td><pre class="text" dir="ltr" data-is-upgraded=""><code>+------------------+------------------+------------------+------------------+
|   LATENT_COL_1   |   LATENT_COL_2   |   LATENT_COL_3   |   LATENT_COL_4   |
+------------------------+------------+------------------+------------------+
|    0.21384512    |    0.93457112    |    0.64978097    |    0.00480489    |
+------------------+------------------+------------------+------------------+
        </code></pre></td>
</tr>
</tbody>
</table>

### AUTOML\_CLASSIFIER

Prediction output format

Output sample

``` text
+------------------------------------------+
| predictions                              |
+------------------------------------------+
| [{"scores":[FLOAT], "classes":[STRING]}] |
+------------------------------------------+
        
```

``` text
+---------------------------------------------+
| predictions                                 |
+---------------------------------------------+
| [{"scores":[1, 2], "classes":['a', 'b']},   |
|  {"scores":[3, 0.2], "classes":['a', 'b']}] |
+---------------------------------------------+
        
```

### AUTOML\_REGRESSOR

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Prediction output format</th>
<th>Output sample</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded=""><code>+-----------------+
| predictions     |
+-----------------+
| [FLOAT]         |
+-----------------+
        </code></pre></td>
<td><pre class="text" dir="ltr" data-is-upgraded=""><code>+-----------------+
| predictions     |
+-----------------+
| [1.8, 2.46]     |
+-----------------+
        </code></pre></td>
</tr>
</tbody>
</table>

### BOOSTED\_TREE\_CLASSIFIER and RANDOM\_FOREST\_CLASSIFIER

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Prediction output format</th>
<th>Output sample</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded=""><code>+-------------+--------------+-----------------+
| LABEL_PROBS | LABEL_VALUES | PREDICTED_LABEL |
+-------------+--------------+-----------------+
| [FLOAT]     | [STRING]     | STRING          |
+-------------+--------------+-----------------+
        </code></pre></td>
<td><pre class="text" dir="ltr" data-is-upgraded=""><code>+-------------+--------------+-----------------+
| LABEL_PROBS | LABEL_VALUES | PREDICTED_LABEL |
+-------------+--------------+-----------------+
| [0.1, 0.9]  | [&#39;a&#39;, &#39;b&#39;]   | [&#39;b&#39;]           |
+-------------+--------------+-----------------+
| [0.8, 0.2]  | [&#39;a&#39;, &#39;b&#39;]   | [&#39;a&#39;]           |
+-------------+--------------+-----------------+
        </code></pre></td>
</tr>
</tbody>
</table>

### BOOSTED\_TREE\_REGRESSOR AND RANDOM\_FOREST\_REGRESSOR

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Prediction output format</th>
<th>Output sample</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded=""><code>+-----------------+
| predicted_label |
+-----------------+
| FLOAT           |
+-----------------+
        </code></pre></td>
<td><pre class="text" dir="ltr" data-is-upgraded=""><code>+-----------------+
| predicted_label |
+-----------------+
| [1.8]           |
+-----------------+
| [2.46]          |
+-----------------+
        </code></pre></td>
</tr>
</tbody>
</table>

### DNN\_CLASSIFIER

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Prediction output format</th>
<th>Output sample</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded=""><code>+---------------+-------------+-----------+---------+------------------------+--------+---------------+
| ALL_CLASS_IDS | ALL_CLASSES | CLASS_IDS | CLASSES | LOGISTIC (binary only) | LOGITS | PROBABILITIES |
+---------------+-------------+-----------+---------+------------------------+--------+---------------+
| [INT64]       | [STRING]    | INT64     | STRING  | FLOAT                  | [FLOAT]| [FLOAT]       |
+---------------+-------------+-----------+---------+------------------------+--------+---------------+
        </code></pre></td>
<td><pre class="text" dir="ltr" data-is-upgraded=""><code>+---------------+-------------+-----------+---------+------------------------+--------+---------------+
| ALL_CLASS_IDS | ALL_CLASSES | CLASS_IDS | CLASSES | LOGISTIC (binary only) | LOGITS | PROBABILITIES |
+---------------+-------------+-----------+---------+------------------------+--------+---------------+
| [0, 1]        | [&#39;a&#39;, &#39;b&#39;]  | [0]       | [&#39;a&#39;]   | [0.36]                 | [-0.53]| [0.64, 0.36]  |
+---------------+-------------+-----------+---------+------------------------+--------+---------------+
| [0, 1]        | [&#39;a&#39;, &#39;b&#39;]  | [0]       | [&#39;a&#39;]   | [0.2]                  | [-1.38]| [0.8, 0.2]    |
+---------------+-------------+-----------+---------+------------------------+--------+---------------+
        </code></pre></td>
</tr>
</tbody>
</table>

### DNN\_REGRESSOR

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Prediction output format</th>
<th>Output sample</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded=""><code>+-----------------+
| PREDICTED_LABEL |
+-----------------+
| FLOAT           |
+-----------------+
        </code></pre></td>
<td><pre class="text" dir="ltr" data-is-upgraded=""><code>+-----------------+
| PREDICTED_LABEL |
+-----------------+
| [1.8]           |
+-----------------+
| [2.46]          |
+-----------------+
        </code></pre></td>
</tr>
</tbody>
</table>

### DNN\_LINEAR\_COMBINED\_CLASSIFIER

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Prediction output format</th>
<th>Output sample</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded=""><code>+---------------+-------------+-----------+---------+------------------------+--------+---------------+
| ALL_CLASS_IDS | ALL_CLASSES | CLASS_IDS | CLASSES | LOGISTIC (binary only) | LOGITS | PROBABILITIES |
+---------------+-------------+-----------+---------+------------------------+--------+---------------+
| [INT64]       | [STRING]    | INT64     | STRING  | FLOAT                  | [FLOAT]| [FLOAT]       |
+---------------+-------------+-----------+---------+------------------------+--------+---------------+
        </code></pre></td>
<td><pre class="text" dir="ltr" data-is-upgraded=""><code>+---------------+-------------+-----------+---------+------------------------+--------+---------------+
| ALL_CLASS_IDS | ALL_CLASSES | CLASS_IDS | CLASSES | LOGISTIC (binary only) | LOGITS | PROBABILITIES |
+---------------+-------------+-----------+---------+------------------------+--------+---------------+
| [0, 1]        | [&#39;a&#39;, &#39;b&#39;]  | [0]       | [&#39;a&#39;]   | [0.36]                 | [-0.53]| [0.64, 0.36]  |
+---------------+-------------+-----------+---------+------------------------+--------+---------------+
| [0, 1]        | [&#39;a&#39;, &#39;b&#39;]  | [0]       | [&#39;a&#39;]   | [0.2]                  | [-1.38]| [0.8, 0.2]    |
+---------------+-------------+-----------+---------+------------------------+--------+---------------+
        </code></pre></td>
</tr>
</tbody>
</table>

### DNN\_LINEAR\_COMBINED\_REGRESSOR

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Prediction output format</th>
<th>Output sample</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded=""><code>+-----------------+
| PREDICTED_LABEL |
+-----------------+
| FLOAT           |
+-----------------+
        </code></pre></td>
<td><pre class="text" dir="ltr" data-is-upgraded=""><code>+-----------------+
| PREDICTED_LABEL |
+-----------------+
| [1.8]           |
+-----------------+
| [2.46]          |
+-----------------+
        </code></pre></td>
</tr>
</tbody>
</table>

### KMEANS

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Prediction output format</th>
<th>Output sample</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded=""><code>+--------------------+--------------+---------------------+
| CENTROID_DISTANCES | CENTROID_IDS | NEAREST_CENTROID_ID |
+--------------------+--------------+---------------------+
| [FLOAT]            | [INT64]      | INT64               |
+--------------------+--------------+---------------------+
        </code></pre></td>
<td><pre class="text" dir="ltr" data-is-upgraded=""><code>+--------------------+--------------+---------------------+
| CENTROID_DISTANCES | CENTROID_IDS | NEAREST_CENTROID_ID |
+--------------------+--------------+---------------------+
| [1.2, 1.3]         | [1, 2]       | [1]                 |
+--------------------+--------------+---------------------+
| [0.4, 0.1]         | [1, 2]       | [2]                 |
+--------------------+--------------+---------------------+
        </code></pre></td>
</tr>
</tbody>
</table>

### LINEAR\_REG

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Prediction output format</th>
<th>Output sample</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded=""><code>+-----------------+
| PREDICTED_LABEL |
+-----------------+
| FLOAT           |
+-----------------+
        </code></pre></td>
<td><pre class="text" dir="ltr" data-is-upgraded=""><code>+-----------------+
| PREDICTED_LABEL |
+-----------------+
| [1.8]           |
+-----------------+
| [2.46]          |
+-----------------+
       </code></pre></td>
</tr>
</tbody>
</table>

### LOGISTIC\_REG

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Prediction output format</th>
<th>Output sample</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded=""><code>+-------------+--------------+-----------------+
| LABEL_PROBS | LABEL_VALUES | PREDICTED_LABEL |
+-------------+--------------+-----------------+
| [FLOAT]     | [STRING]     | STRING          |
+-------------+--------------+-----------------+
        </code></pre></td>
<td><pre class="text" dir="ltr" data-is-upgraded=""><code>+-------------+--------------+-----------------+
| LABEL_PROBS | LABEL_VALUES | PREDICTED_LABEL |
+-------------+--------------+-----------------+
| [0.1, 0.9]  | [&#39;a&#39;, &#39;b&#39;]   | [&#39;b&#39;]           |
+-------------+--------------+-----------------+
| [0.8, 0.2]  | [&#39;a&#39;, &#39;b&#39;]   | [&#39;a&#39;]           |
+-------------+--------------+-----------------+
        </code></pre></td>
</tr>
</tbody>
</table>

### MATRIX\_FACTORIZATION

**Note:** We only support taking an input user and output top 50 (predicted\_rating, predicted\_item) pairs sorted by predicted\_rating in descending order.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Prediction output format</th>
<th>Output sample</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded=""><code>+--------------------+--------------+
| PREDICTED_RATING | PREDICTED_ITEM |
+------------------+----------------+
| [FLOAT]          | [STRING]       |
+------------------+----------------+
        </code></pre></td>
<td><pre class="text" dir="ltr" data-is-upgraded=""><code>+--------------------+--------------+
| PREDICTED_RATING | PREDICTED_ITEM |
+------------------+----------------+
| [5.5, 1.7]       | [&#39;A&#39;, &#39;B&#39;]     |
+------------------+----------------+
| [7.2, 2.7]       | [&#39;B&#39;, &#39;A&#39;]     |
+------------------+----------------+
        </code></pre></td>
</tr>
</tbody>
</table>

### TENSORFLOW (imported)

<table>
<thead>
<tr class="header">
<th>Prediction output format</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Same as the imported model</td>
</tr>
</tbody>
</table>

### PCA

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Prediction output format</th>
<th>Output sample</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded=""><code>+-------------------------+---------------------------------+
| PRINCIPAL_COMPONENT_IDS | PRINCIPAL_COMPONENT_PROJECTIONS |
+-------------------------+---------------------------------+
|       [INT64]           |             [FLOAT]             |
+-------------------------+---------------------------------+
        </code></pre></td>
<td><pre class="text" dir="ltr" data-is-upgraded=""><code>+-------------------------+---------------------------------+
| PRINCIPAL_COMPONENT_IDS | PRINCIPAL_COMPONENT_PROJECTIONS |
+-------------------------+---------------------------------+
|       [1, 2]            |             [1.2, 5.0]          |
+-------------------------+---------------------------------+
        </code></pre></td>
</tr>
</tbody>
</table>

### TRANSFORM\_ONLY

<table>
<thead>
<tr class="header">
<th>Prediction output format</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Same as the columns specified in the model's <code dir="ltr" translate="no">       TRANSFORM      </code> clause</td>
</tr>
</tbody>
</table>

## XGBoost model visualization

You can visualize the boosted trees using the [plot\_tree](https://xgboost.readthedocs.io/en/latest/python/python_api.html#xgboost.plot_tree) Python API after model export. For example, you can leverage [Colab](https://colab.research.google.com/) without installing the dependencies:

1.  Export the boosted tree model to a Cloud Storage bucket.

2.  Download the `  model.bst  ` file from the Cloud Storage bucket.

3.  In a [Colab noteboook](https://colab.sandbox.google.com/notebooks/welcome.ipynb) , upload the `  model.bst  ` file to `  Files  ` .

4.  Run the following code in the notebook:
    
    ``` text
    import xgboost as xgb
    import matplotlib.pyplot as plt
    
    model = xgb.Booster(model_file="model.bst")
    num_iterations = <iteration_number>
    for tree_num in range(num_iterations):
      xgb.plot_tree(model, num_trees=tree_num)
    plt.show
    ```

This example plots multiple trees (one tree per iteration):

**Note:** We use the label encoder to encode categorical features, so you can get the corresponding category for a split value from the vocabulary file in the 'assets/' directory inside the model export Cloud Storage bucket. For example, when you see "f0 \< 2.95" in a node, you can find the corresponding category in the vocabulary file by looking for the 3rd item.

We don't save feature names in the model, so you will see names such as "f0", "f1", and so on. You can find the corresponding feature names in the `  assets/model_metadata.json  ` exported file using these names (such as "f0") as indexes.

## Required permissions

To export a BigQuery ML model to Cloud Storage, you need permissions to access the BigQuery ML model, permissions to run an extract job, and permissions to write the data to the Cloud Storage bucket.

**BigQuery permissions**

  - At a minimum, to export model, you must be granted `  bigquery.models.export  ` permissions. The following predefined Identity and Access Management (IAM) roles are granted `  bigquery.models.export  ` permissions:
    
      - `  bigquery.dataViewer  `
      - `  bigquery.dataOwner  `
      - `  bigquery.dataEditor  `
      - `  bigquery.admin  `

  - At a minimum, to run an export [job](/bigquery/docs/managing-jobs) , you must be granted `  bigquery.jobs.create  ` permissions. The following predefined IAM roles are granted `  bigquery.jobs.create  ` permissions:
    
      - `  bigquery.user  `
      - `  bigquery.jobUser  `
      - `  bigquery.admin  `

**Cloud Storage permissions**

  - To write the data to an existing Cloud Storage bucket, you must be granted `  storage.objects.create  ` permissions. The following predefined IAM roles are granted `  storage.objects.create  ` permissions:
    
      - `  storage.objectCreator  `
      - `  storage.objectAdmin  `
      - `  storage.admin  `

For more information on IAM roles and permissions in BigQuery ML, see [Access control](/bigquery/docs/access-control) .

## Move BigQuery data between locations

You cannot change the location of a dataset after it is created, but you can [make a copy of the dataset](/bigquery/docs/copying-datasets) .

## Quota policy

For information on extract job quotas, see [Extract jobs](/bigquery/quotas#export_jobs) on the Quotas and limits page.

## Pricing

There is no charge for exporting BigQuery ML models, but exports are subject to BigQuery's [Quotas and limits](/bigquery/quotas) . For more information on BigQuery pricing, see the [Pricing](https://cloud.google.com/bigquery/pricing) page.

After the data is exported, you are charged for storing the data in Cloud Storage. For more information on Cloud Storage pricing, see the Cloud Storage [Pricing](https://cloud.google.com/storage/pricing) page.

## What's next

  - Walk through the [Export a BigQuery ML model for online prediction](/bigquery/docs/export-model-tutorial) tutorial.
