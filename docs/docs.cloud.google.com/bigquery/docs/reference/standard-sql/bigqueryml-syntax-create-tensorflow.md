# The CREATE MODEL statement for importing TensorFlow models

This document describes the `  CREATE MODEL  ` statement for importing [TensorFlow](https://www.tensorflow.org/) models into BigQuery by using SQL. Alternatively, you can use the Google Cloud console user interface to [create a model by using a UI](/bigquery/docs/create-machine-learning-model-console) ( [Preview](https://cloud.google.com/products#product-launch-stages) ) instead of constructing the SQL statement yourself.

For more information about supported SQL statements and functions for this model, see [End-to-end user journeys for imported models](/bigquery/docs/e2e-journey-import) .

## `     CREATE MODEL    ` syntax

``` sql
{CREATE MODEL | CREATE MODEL IF NOT EXISTS | CREATE OR REPLACE MODEL}
model_name
OPTIONS(MODEL_TYPE = 'TENSORFLOW', MODEL_PATH = string_value
  [, KMS_KEY_NAME = string_value ]
);
```

### `     CREATE MODEL    `

Creates and trains a new model in the specified dataset. If the model name exists, `  CREATE MODEL  ` returns an error.

### `     CREATE MODEL IF NOT EXISTS    `

Creates and trains a new model only if the model doesn't exist in the specified dataset.

### `     CREATE OR REPLACE MODEL    `

Creates and trains a model and replaces an existing model with the same name in the specified dataset.

### `     model_name    `

The name of the model you're creating or replacing. The model name must be unique in the dataset: no other model or table can have the same name. The model name must follow the same naming rules as a BigQuery table. A model name can:

  - Contain up to 1,024 characters
  - Contain letters (upper or lower case), numbers, and underscores

`  model_name  ` is case-sensitive.

If you don't have a default project configured, then you must prepend the project ID to the model name in the following format, including backticks:

\`\[PROJECT\_ID\].\[DATASET\].\[MODEL\]\`

For example, \`myproject.mydataset.mymodel\`.

### `     MODEL_TYPE    `

**Syntax**

``` text
MODEL_TYPE = 'TENSORFLOW'
```

**Description**

Specifies the model type. This option is required.

### `     MODEL_PATH    `

**Syntax**

``` text
MODEL_PATH = string_value
```

**Description**

Specifies the [Cloud Storage URI](/bigquery/docs/loading-data-cloud-storage#gcs-uri) of the TensorFlow model to import. This option is required.

**Arguments**

A `  STRING  ` value specifying the URI of a Cloud Storage bucket that contains the model to import.

BigQuery ML imports the model from Cloud Storage by using the credentials of the user who runs the `  CREATE MODEL  ` statement.

**Example**

``` text
MODEL_PATH = 'gs://bucket/path/to/saved_model/*'
```

### `     KMS_KEY_NAME    `

**Syntax**

`  KMS_KEY_NAME = string_value  `

**Description**

The Cloud Key Management Service [customer-managed encryption key (CMEK)](/kms/docs/cmek) to use to encrypt the model.

**Arguments**

A `  STRING  ` value containing the fully-qualified name of the CMEK. For example,

``` text
'projects/my_project/locations/my_location/keyRings/my_ring/cryptoKeys/my_key'
```

## Supported data types for input and output columns

BigQuery ML converts some TensorFlow model input and output columns to BigQuery ML types, and some [TensorFlow types](https://www.tensorflow.org/api_docs/python/tf/dtypes/DType) aren't supported. Supported data types for input and output columns include the following:

<table>
<thead>
<tr class="header">
<th>TensorFlow types</th>
<th>Supported</th>
<th>BigQuery ML type</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       tf.int8, tf.int16, tf.int32, tf.int64, tf.uint8, tf.uint16, tf.uint32, tf.uint64      </code></td>
<td>Supported</td>
<td><a href="/bigquery/docs/reference/standard-sql/data-types#integer_types"><code dir="ltr" translate="no">        INT64       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       tf.float16, tf.float32, tf.float64, tf.bfloat16      </code></td>
<td>Supported</td>
<td><a href="/bigquery/docs/reference/standard-sql/data-types#floating_point_types"><code dir="ltr" translate="no">        FLOAT64       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       tf.complex64, tf.complex128      </code></td>
<td>Unsupported</td>
<td>N/a</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       tf.qint8, tf.quint8, tf.qint16, tf.quint16, tf.qint32      </code></td>
<td>Unsupported</td>
<td>N/A</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       tf.bool      </code></td>
<td>Supported</td>
<td><a href="/bigquery/docs/reference/standard-sql/data-types#boolean_type"><code dir="ltr" translate="no">        BOOL       </code></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       tf.string      </code></td>
<td>Supported</td>
<td><a href="/bigquery/docs/reference/standard-sql/data-types#string_type"><code dir="ltr" translate="no">        STRING       </code></a></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       tf.resource      </code></td>
<td>Unsupported</td>
<td>N/A</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       tf.variant      </code></td>
<td>Unsupported</td>
<td>N/A</td>
</tr>
<tr class="odd">
<td><a href="https://www.tensorflow.org/api_docs/python/tf/sparse/SparseTensor"><code dir="ltr" translate="no">        SparseTensor       </code></a> of a supported TensorFlow type</td>
<td>Supported</td>
<td>A <code dir="ltr" translate="no">       NULL      </code> , the associated BigQuery ML type, or an <a href="/bigquery/docs/reference/standard-sql/data-types#array_type"><code dir="ltr" translate="no">        ARRAY       </code></a> of the associated BigQuery ML type.</td>
</tr>
<tr class="even">
<td><a href="https://www.tensorflow.org/tutorials/load_data/tfrecord#tftrainexample"><code dir="ltr" translate="no">        tf.train.Example       </code></a> containing supported TensorFlow types</td>
<td>Supported</td>
<td>BigQuery ML automatically takes features and converts into a <code dir="ltr" translate="no">       tf.train.Example      </code> .</td>
</tr>
</tbody>
</table>

The model input columns can be either dense Tensors or SparseTensors; RaggedTensors aren't supported. You can pass SparseTensors as dense arrays and BigQuery ML automatically converts them into Sparse format to pass into TensorFlow.

If the model expects input columns in [`  tf.train.Example  ` format](https://www.tensorflow.org/tutorials/load_data/tfrecord#tftrainexample) , then BigQuery ML automatically determines the feature names and converts the input BigQuery columns into the model's expected format.

## Locations

For information about supported locations, see [Locations for non-remote models](/bigquery/docs/locations#locations-for-non-remote-models) .

## Limitations

Imported TensorFlow models have the following limitations:

  - The TensorFlow model must already exist before you can import it into BigQuery ML.
  - Models must be stored in Cloud Storage.
  - Models are frozen at the time of model creation.
  - TensorFlow models must be in [SavedModel format](https://www.tensorflow.org/api_docs/python/tf/saved_model) .
  - The following functions don't support TensorFlow models:
      - `  ML.CONFUSION  `
      - `  ML.EVALUATE  `
      - `  ML.FEATURE  `
      - `  ML.ROC_CURVE  `
      - `  ML.TRAINING_INFO  `
      - `  ML.WEIGHTS  `
  - Models are limited to 450 MB in size.
  - Models trained using a version of GraphDef earlier than version 20 aren't supported.
  - Models trained using an unreleased version of TensorFlow aren't supported.
  - Only core TensorFlow operations are supported; models that use custom or `  tf.contrib  ` operations aren't supported.
  - RaggedTensors aren't supported.
  - You can only use an imported TensorFlow model with an object table when you use capacity-based pricing through reservations. On-demand pricing isn't supported.

## Example

The following example imports a TensorFlow model into BigQuery ML as a BigQuery ML model. The example assumes that there is an existing TensorFlow model located at `  gs://bucket/path/to/saved_model/*  ` .

``` text
CREATE MODEL `project_id.mydataset.mymodel`
 OPTIONS(MODEL_TYPE='TENSORFLOW',
         MODEL_PATH="gs://bucket/path/to/saved_model/*")
```
