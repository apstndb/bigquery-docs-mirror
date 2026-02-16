# The EXPORT MODEL statement

To export an existing model from BigQuery ML to [Cloud Storage](/storage/docs) , use the `  EXPORT MODEL  ` statement.

For more information about supported model types, formats, and limitations, see [Export models](/bigquery/docs/exporting-models) .

For more information about supported SQL statements and functions for exportable models, see the following documents:

  - [End-to-end user journeys for ML models](/bigquery/docs/e2e-journey)
  - [End-to-end user journeys for imported models](/bigquery/docs/e2e-journey-import)

## Syntax

The following is the syntax of `  EXPORT MODEL  ` for a regular model that is not generated from BigQuery ML hyperparameter tuning.

``` text
EXPORT MODEL MODEL_NAME [OPTIONS(URI = STRING_VALUE)]
```

  - `  MODEL_NAME  ` is the name of the BigQuery ML model you're exporting. If you are exporting a model in another project, you must specify the project, dataset, and model in the following format, including backticks:
    
    ``` text
    `PROJECT.DATASET.MODEL`
    ```
    
    For example, ``  `myproject.mydataset.mymodel`  `` .
    
    If the model name does not exist in the dataset, the following error is returned:
    
    `  Error: Not found: Model myproject:mydataset.mymodel  `

  - `  STRING_VALUE  ` is the [URI of a Cloud Storage](/bigquery/docs/loading-data-cloud-storage#gcs-uri) bucket where the model is exported. This option is required for the `  EXPORT MODEL  ` statement. For example:
    
    ``` text
    URI = 'gs://bucket/path/to/saved_model/'
    ```

For a model that is generated from BigQuery ML hyperparameter tuning, `  EXPORT MODEL  ` can also export an individual trial to a destination URI. For example:

``` text
EXPORT MODEL MODEL_NAME [OPTIONS(URI = STRING_VALUE [, TRIAL_ID = INT_VALUE])]
```

  - `  INT_VALUE  ` is the numeric ID of the exporting trial. For example:
    
    ```` text
    ```sql
    TRIAL_ID = 12
    ```
    ````

  - If `  TRIAL_ID  ` is not specified, then the optimal trial is exported by default.
