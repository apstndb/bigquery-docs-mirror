---
name: documents/docs.cloud.google.com/bigquery/docs/api-sql-translator
uri: https://docs.cloud.google.com/bigquery/docs/api-sql-translator
title: Translate SQL queries with the translation API
description: Describes how to translate SQL queries or scripts into GoogleSQL queries by using the translation API.
data_source: docs.cloud.google.com
---

# Translate SQL queries with the translation API

This document describes how to use the BigQuery Migration API in BigQuery to translate scripts written in other SQL dialects into GoogleSQL queries.

> **Note:** To run a translation job from the Google Cloud console or from the command line, see [Translate SQL queries with the batch SQL translator](https://docs.cloud.google.com/bigquery/docs/batch-sql-translator) . Use the BigQuery Migration API described on this page only if you are building custom software integrations, automated CI/CD pipelines, or programmatic workflows.

For a list of SQL dialects supported by this SQL translator, and a list of supported processing locations, see [Supported SQL dialects](https://docs.cloud.google.com/bigquery/docs/enable-sql-translations#supported_sql_dialects) and [Locations](https://docs.cloud.google.com/bigquery/docs/enable-sql-translations#locations) .

## Before you begin

Before you submit a translation job, complete the following steps.

### Choose a translation mode

The BigQuery Migration API supports two translation modes. Both modes use the same API method and run as asynchronous jobs. The modes differ in how you provide the source SQL and how you receive the translated SQL:

- **Batch translation** : The API reads source files from Cloud Storage and writes the translated files and reports to Cloud Storage. Use batch translation to translate many files at once —for example, when you migrate an entire codebase.
- **Interactive translation** : You pass your SQL as string literals in the request body and read the translated SQL from the workflow response. You don't need to store your SQL or the translation output in Cloud Storage. Use interactive translation to translate individual queries on demand —for example, when translating queries from an application or a developer tool.

### Enable translations

Enable the required BigQuery Migration API. For more information, see [Enable SQL translations](https://docs.cloud.google.com/bigquery/docs/enable-sql-translations#enable-api) .

### Required permissions

To get the permissions that you need to create translation jobs with the interactor translator, the translation API, or the batch SQL translator, ask your administrator to grant you the following IAM roles on the `parent` resource:

- Viewing and monitoring migration jobs: [MigrationWorkflow Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.viewer) ( `roles/bigquerymigration.viewer` )
- Submitting migration jobs: [MigrationWorkflow Editor](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.editor) ( `roles/bigquerymigration.editor` )
- Access the Cloud Storage buckets for input and files: Storage Object Admin ( `roles/storage.objectAdmin` ) - on the source and destination Cloud Storage bucket.

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

These predefined roles contain the permissions required to create translation jobs with the interactor translator, the translation API, or the batch SQL translator. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to create translation jobs with the interactor translator, the translation API, or the batch SQL translator:

- `bigquerymigration.workflows.create`
- `bigquerymigration.workflows.get`
- `bigquerymigration.workflows.list`
- `bigquerymigration.workflows.delete`
- `bigquerymigration.subtasks.get`
- `bigquerymigration.subtasks.list`
- `storage.objects.get`
- `storage.objects.list`
- `storage.objects.create`

You might also be able to get these permissions with [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

### Upload input files to Cloud Storage

For batch translation jobs, you must upload the source files containing the queries and scripts you want to translate to Cloud Storage. You can also upload [any metadata files](https://docs.cloud.google.com/bigquery/docs/generate-metadata) or [configuration YAML files](https://docs.cloud.google.com/bigquery/docs/config-yaml-translation) to the same Cloud Storage bucket containing the source files.

For more information about creating buckets and uploading files to Cloud Storage, see [Create buckets](https://docs.cloud.google.com/storage/docs/creating-buckets) and [Upload objects from a filesystem](https://docs.cloud.google.com/storage/docs/uploading-objects) .

### Unsupported SQL functions

If your source queries reference SQL functions that don't have direct equivalents in GoogleSQL, you can use helper user-defined functions (UDFs). For more information, see [Handling unsupported SQL functions with helper UDFs](https://docs.cloud.google.com/bigquery/docs/batch-sql-translator#handling_unsupported_sql_functions_with_helper_udfs) .

## Submit a translation job

To submit a translation job using the BigQuery Migration API, use the [`projects.locations.workflows.create`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rest/v2/projects.locations.workflows/create) method and supply an instance of the [`MigrationWorkflow`](https://docs.cloud.google.com/bigquery/docs/reference/migration/rest/v2/projects.locations.workflows#resource:-migrationworkflow) resource with a [supported task type](https://docs.cloud.google.com/bigquery/docs/enable-sql-translations#supported_sql_dialects) .

After you submit the job, you can [poll for job status](https://docs.cloud.google.com/bigquery/docs/api-sql-translator#check_job_status) .

### Create a batch translation

The following `curl` command creates a batch translation job where the input and output files are stored in Cloud Storage. The `source_target_mapping` field contains a list that maps the source directories to an optional relative path for the target output.

```
curl -d "{
  \"tasks\": {
      string: {
        \"type\": \"TYPE\",
        \"translation_details\": {
            \"target_base_uri\": \"TARGET_BASE\",
            \"source_target_mapping\": {
              \"source_spec\": {
                  \"base_uri\": \"BASE\"
              }
            },
            \"target_types\": \"TARGET_TYPES\",
        }
      }
  }
  }" \
  -H "Content-Type:application/json" \
  -H "Authorization: Bearer TOKEN" -X POST https://bigquerymigration.googleapis.com/v2/projects/PROJECT_ID/locations/LOCATION/workflows
```

Replace the following:

- `TYPE` : the [task type](https://docs.cloud.google.com/bigquery/docs/enable-sql-translations#supported_sql_dialects) of the translation, which determines the source and target dialect.

- `TARGET_BASE` : the base URI for all translation outputs.

- `BASE` : the base URI for all files read as sources for translation.

- `TARGET_TYPES` (optional): the generated output types. If not specified, SQL is generated.

  - `sql` (default): The translated SQL query files.
  - `suggestion` : AI generated suggestions.

  The output is stored in a subfolder in the output directory. The subfolder is named based on the value in `TARGET_TYPES` .

- `TOKEN` : the token for authentication. To generate a token, use the `gcloud auth print-access-token` command or the [OAuth 2.0 playground](https://developers.google.com/oauthplayground/) (use the scope `https://www.googleapis.com/auth/cloud-platform` ).

- `PROJECT_ID` : the project to process the translation.

- `LOCATION` : the [location](https://docs.cloud.google.com/bigquery/docs/enable-sql-translations#locations) where the job is processed.

The preceding command returns a response that includes a workflow ID written in the format `projects/ `` PROJECT_ID `` /locations/ `` LOCATION `` /workflows/ `` WORKFLOW_ID` .

#### Example batch translation

To translate the Teradata SQL scripts in the Cloud Storage directory `gs://my_data_bucket/teradata/input/` and store the results in the Cloud Storage directory `gs://my_data_bucket/teradata/output/` , you might use the following query:

```
{
  "tasks": {
     "task_name": {
       "type": "Teradata2BigQuery_Translation",
       "translation_details": {
         "target_base_uri": "gs://my_data_bucket/teradata/output/",
           "source_target_mapping": {
             "source_spec": {
               "base_uri": "gs://my_data_bucket/teradata/input/"
             }
          },
       }
    }
  }
}
```

> **Note:** The string `"task_name"` in this example is an identifier for the translation task and can be set to any value you prefer.

This call will return a message containing the created workflow ID in the `"name"` field:

```
{
  "name": "projects/123456789/locations/us/workflows/12345678-9abc-def1-2345-6789abcdef00",
  "tasks": {
    "task_name": { /*...*/ }
  },
  "state": "RUNNING"
}
```

To get the updated status for the workflow, [run a `GET` query](https://docs.cloud.google.com/bigquery/docs/api-sql-translator#check_job_status) . The job sends outputs to Cloud Storage as it progresses. The job `state` changes to `COMPLETED` after all the requested `target_types` are generated. If the task succeeds, you can find the translated SQL query in `gs://my_data_bucket/teradata/output` .

#### Example batch translation with AI suggestions

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> **Note:** The translation API can call Gemini using BigQuery Agent Platform integration to generate suggestions to your translated SQL query based on your AI configuration YAML file.

The following example translates the Teradata SQL scripts located in the `gs://my_data_bucket/teradata/input/` Cloud Storage directory and stores results in the Cloud Storage directory `gs://my_data_bucket/teradata/output/` with additional AI suggestion:

```
{
  "tasks": {
     "task_name": {
       "type": "Teradata2BigQuery_Translation",
       "translation_details": {
         "target_base_uri": "gs://my_data_bucket/teradata/output/",
           "source_target_mapping": {
             "source_spec": {
               "base_uri": "gs://my_data_bucket/teradata/input/"
             }
          },
          "target_types": "suggestion",
       }
    }
  }
}
```

> **Note:** To generate AI suggestions, the Cloud Storage source directory must contain at least one configuration YAML file with a suffix of `.ai_config.yaml` . To learn how to write the configuration YAML file for AI suggestions, see [Create a Gemini-based configuration YAML file](https://docs.cloud.google.com/bigquery/docs/config-yaml-translation#ai_yaml_guidelines) .

After the task runs successfully, AI suggestions can be found in `gs://my_data_bucket/teradata/output/suggestion` Cloud Storage directory.

### Create an interactive translation

The following `curl` command creates an interactive translation job with string literal inputs and outputs. The `source_target_mapping` field contains a list that maps the source `literal` entries to an optional relative path for the target output.

```
curl -d "{
  \"tasks\": {
      string: {
        \"type\": \"TYPE\",
        \"translation_details\": {
        \"source_target_mapping\": {
            \"source_spec\": {
              \"literal\": {
              \"relative_path\": \"PATH\",
              \"literal_string\": \"STRING\"
              }
            }
        },
        \"target_return_literals\": \"TARGETS\",
        }
      }
  }
  }" \
  -H "Content-Type:application/json" \
  -H "Authorization: Bearer TOKEN" -X POST https://bigquerymigration.googleapis.com/v2/projects/PROJECT_ID/locations/LOCATION/workflows
```

Replace the following:

- `TYPE` : the [task type](https://docs.cloud.google.com/bigquery/docs/enable-sql-translations#supported_sql_dialects) of the translation, which determines the source and target dialect.
- `PATH` : the identifier of the literal entry, similar to a filename or path.
- `STRING` : string of literal input data (for example, SQL) to be translated.
- `TARGETS` : the expected targets that the user wants to be directly returned in the response in the `literal` format. These should be in the target URI format (for example, ` GENERATED_DIR ` + `target_spec.relative_path` + `source_spec.literal.relative_path` ). Anything not in this list is not returned in the response. The generated directory, ` GENERATED_DIR ` for general SQL translations is `sql/` .
- `TOKEN` : the token for authentication. To generate a token, use the `gcloud auth print-access-token` command or the [OAuth 2.0 playground](https://developers.google.com/oauthplayground/) (use the scope `https://www.googleapis.com/auth/cloud-platform` ).
- `PROJECT_ID` : the project to process the translation.
- `LOCATION` : the [location](https://docs.cloud.google.com/bigquery/docs/enable-sql-translations#locations) where the job is processed.

The preceding command returns a response that includes a workflow ID written in the format `projects/ `` PROJECT_ID `` /locations/ `` LOCATION `` /workflows/ `` WORKFLOW_ID` .

After the workflow is created, view the results by [checking the job status](https://docs.cloud.google.com/bigquery/docs/api-sql-translator#check_job_status) .

#### Example interactive translation

To translate the Apache Hive SQL string `select 1` interactively, you might use the following query:

```
"tasks": {
  string: {
    "type": "HiveQL2BigQuery_Translation",
    "translation_details": {
      "source_target_mapping": {
        "source_spec": {
          "literal": {
            "relative_path": "input_file",
            "literal_string": "select 1"
          }
        }
      },
      "target_return_literals": "sql/input_file",
    }
  }
}
```

> **Note:** The string `"task_name"` in this example is an identifier for the translation task and can be set to any value you prefer.

You can use any `relative_path` you would like for your literal, but the translated literal will only appear in the results if you include `sql/$relative_path` in your `target_return_literals` . You can also include multiple literals in a single query, in which case each of their relative paths must be included in `target_return_literals` .

This call will return a message containing the created workflow ID in the `"name"` field:

```
{
  "name": "projects/123456789/locations/us/workflows/12345678-9abc-def1-2345-6789abcdef00",
  "tasks": {
    "task_name": { /*...*/ }
  },
  "state": "RUNNING"
}
```

To get the updated status for the workflow, [check the job status](https://docs.cloud.google.com/bigquery/docs/api-sql-translator#check_job_status) . The job is complete when `"state"` changes to `COMPLETED` . If the task succeeds, you will find the translated SQL in the response message:

```
{
  "name": "projects/123456789/locations/us/workflows/12345678-9abc-def1-2345-6789abcdef00",
  "tasks": {
    "string": {
      "id": "0fedba98-7654-3210-1234-56789abcdef",
      "type": "HiveQL2BigQuery_Translation",
      /* ... */
      "taskResult": {
        "translationTaskResult": {
          "translatedLiterals": [
            {
              "relativePath": "sql/input_file",
              "literalString": "-- Translation time: 2023-10-05T21:50:49.885839Z\n-- Translation job ID: projects/123456789/locations/us/workflows/12345678-9abc-def1-2345-6789abcdef00\n-- Source: input_file\n-- Translated from: Hive\n-- Translated to: BigQuery\n\nSELECT\n    1\n;\n"
            }
          ],
          "reportLogMessages": [
            ...
          ]
        }
      },
      /* ... */
    }
  },
  "state": "COMPLETED",
  "createTime": "2023-10-05T21:50:49.543221Z",
  "lastUpdateTime": "2023-10-05T21:50:50.462758Z"
}
```

## Check job status

Translation jobs run asynchronously. After you submit a workflow, retrieve its status by sending a `GET` request with the workflow ID:

```
curl \
  -H "Content-Type:application/json" \
  -H "Authorization:Bearer TOKEN" \
  -X GET https://bigquerymigration.googleapis.com/v2/projects/PROJECT_ID/locations/LOCATION/workflows/WORKFLOW_ID
```

Replace the following:

- `TOKEN` : the token for authentication. To generate a token, use the `gcloud auth print-access-token` command or the [OAuth 2.0 playground](https://developers.google.com/oauthplayground/) (use the scope `https://www.googleapis.com/auth/cloud-platform` ).
- `PROJECT_ID` : the project that is running the translation job.
- `LOCATION` : the [location](https://docs.cloud.google.com/bigquery/docs/enable-sql-translations#locations) where the job is processed.
- `WORKFLOW_ID` : the workflow ID returned when you created the translation workflow.

### Workflow states

The response includes a `state` field that indicates the current status of the workflow:

- `STATE_UNSPECIFIED` : The workflow state is unspecified.
- `RUNNING` : The workflow is actively running. Poll the endpoint periodically until the state changes.
- `PAUSED` : The workflow is paused.
- `COMPLETED` : The workflow finished successfully. You can now retrieve the results.
- `FAILED` : The workflow encountered errors. Inspect the `taskResult` and `reportLogMessages` fields in the response for error details.

When the workflow `state` reaches `COMPLETED` or `FAILED` , you can stop polling.

## Retrieve results

How you retrieve results depends on whether you submitted a [batch translation or an interactive translation](https://docs.cloud.google.com/bigquery/docs/api-sql-translator#translation-modes) :

- **Batch translations** : The translated files, summary reports, and any AI suggestions are written to the Cloud Storage destination directory that you specified in `target_base_uri` . You can read these files directly from Cloud Storage using gcloud CLI storage commands, the Cloud Storage client libraries, or the REST API:

  ```
  gcloud storage cp --recursive TARGET_URI LOCAL_DIRECTORY
  ```

  Replace the following:

  - `TARGET_URI` : your target base URI, such as `gs://my_data_bucket/teradata/output/` .
  - `LOCAL_DIRECTORY` : the local directory that receives the files.

  For details on the files generated in the destination bucket, see [Explore the translation output](https://docs.cloud.google.com/bigquery/docs/batch-sql-translator#explore_the_translation_output) .

- **Interactive translations** : For jobs configured with string literal inputs and `target_return_literals` , the translated query is returned directly in the workflow response under the `translatedLiterals` field:

  ```
  "taskResult": {
    "translationTaskResult": {
      "translatedLiterals": [
        {
          "relativePath": "sql/input_file",
          "literalString": "SELECT 1;\n"
        }
      ]
    }
  }
  ```

  Extract the `literalString` field for each entry in `translatedLiterals` to obtain the translated query.
