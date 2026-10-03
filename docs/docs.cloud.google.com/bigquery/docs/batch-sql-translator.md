---
name: documents/docs.cloud.google.com/bigquery/docs/batch-sql-translator
uri: https://docs.cloud.google.com/bigquery/docs/batch-sql-translator
title: Migrate code with the batch SQL translator
description: Describes how to translate batches of SQL queries or scripts into GoogleSQL queries by using the BigQuery batch SQL translator.
data_source: docs.cloud.google.com
---

# Migrate code with the batch SQL translator

This document describes how to use the batch SQL translator in BigQuery to translate scripts written in other SQL dialects into GoogleSQL queries. You can submit and review the results of a translation job from the Google Cloud console or from the command line.

> **Note:** To build a custom software integration, an automated CI/CD pipeline, or another programmatic workflow, we recommend that you [call the BigQuery Migration API](https://docs.cloud.google.com/bigquery/docs/api-sql-translator) directly.

For a list of SQL dialects supported by this SQL translator, see [Supported SQL dialects](https://docs.cloud.google.com/bigquery/docs/enable-sql-translations#supported_sql_dialects) .

For a list of supported processing locations, see [Locations](https://docs.cloud.google.com/bigquery/docs/enable-sql-translations#locations) .

## Before you begin

Before you submit a translation job, do the following steps.

### Enable SQL translations

Enable the required API, and get the permissions needed to use a BigQuery SQL translator. For more information, see [Enable SQL translations](https://docs.cloud.google.com/bigquery/docs/enable-sql-translations#enable_sql_translations) .

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

### Collect source files

Source files must be text files that contain valid SQL for the source dialect. Source files can also include comments. Do your best to ensure the SQL is valid, using whatever methods are available to you.

### Create metadata files

To help the service generate more accurate translation results, we recommend that you provide metadata files. However, this isn't mandatory.

You can use the `dwh-migration-dumper` command-line extraction tool to generate the metadata information. After you prepare the metadata files, you can include them along with the source files in the translation source folder. The translator automatically detects them and leverages them to translate source files, you don't need to configure any extra settings to enable this.

To generate metadata information by using the `dwh-migration-dumper` tool, see [Generate metadata for translation](https://docs.cloud.google.com/bigquery/docs/generate-metadata) .

### Create configuration YAML files

You can optionally create and use configuration [configuration YAML files](https://docs.cloud.google.com/bigquery/docs/config-yaml-translation) to customize your batch translations. These files can be used to transform your translation output in various ways. For example, you can [create a configuration YAML file to change the case of a SQL object](https://docs.cloud.google.com/bigquery/docs/config-yaml-translation#change_object-name_case) during translation.

To use a configuration YAML file, [upload it to the Cloud Storage bucket containing the source files](https://docs.cloud.google.com/bigquery/docs/batch-sql-translator#upload-files) .

### Upload input files to Cloud Storage

Upload the source files containing the queries and scripts that you want to translate to Cloud Storage. You can also upload [any metadata files](https://docs.cloud.google.com/bigquery/docs/generate-metadata) or [configuration YAML files](https://docs.cloud.google.com/bigquery/docs/config-yaml-translation) to the same Cloud Storage bucket and directory containing the source files. For more information about creating buckets and uploading files to Cloud Storage, see [Create buckets](https://docs.cloud.google.com/storage/docs/creating-buckets) and [Upload objects from a filesystem](https://docs.cloud.google.com/storage/docs/uploading-objects) .

### Choose how to submit the translation job

You have two options for submitting a batch translation job:

- **Google Cloud console** : Configure and submit a job using a user interface.

- **Command-line tools** : Describe the job in a translation configuration file, and submit it with the Google Cloud CLI or the bq command-line tool command-line tool.

Both options require you to upload your source files to Cloud Storage, and both create the same kind of translation job. A job that you submit from the command line still appears in the translation jobs list in the Google Cloud console.

## Submit a translation job

Use one of the following options to start a translation job and view its progress. To review the results afterwards, see [Explore the translation output](https://docs.cloud.google.com/bigquery/docs/batch-sql-translator#explore_the_translation_output) .

### Console

These steps assume that you uploaded source files to a Cloud Storage bucket.

To use the Google Cloud console to submit a batch translation job, do the following steps:

1.  In the Google Cloud console, go to the **SQL Translation** page.

2.  In the **SQL translation** panel, click **Start translation** .

3.  For **Translation configuration** , enter the following:

    1.  For **Display name** , enter a name for the translation job. The name can contain letters, numbers or underscores.
    2.  For **Processing location** , select the location where you want the translation job to run. For example, if you are in Europe and you don't want your data to cross any location boundaries, select the `eu` region. The translation job performs best when you choose the same location as your source file bucket.
    3.  For **Source dialect** , select the SQL dialect that you want to translate.
    4.  For **Target dialect** , select **GoogleSQL** .

4.  Click **Next** .

5.  For **File location details** , specify the Cloud Storage paths to use for translation input and output. You can enter the paths in the format `bucket_name/folder_name/` or use the **Browse** option to navigate to a folder.

    1.  For **Output directory location** , specify a path to the destination Cloud Storage folder for the translated files. This serves as a root directory for all translation output.
    2.  Choose one or more **Input directory locations** containing the path to the SQL files to translate.
    3.  Each input directory can optionally be given an **Output subdirectory name** underneath the root output directory if necessary.

6.  Click **Next** .

7.  Select any optional settings that you need to customize metadata and any additional translation outputs.

8.  Optional: To further customize translation behavior, create configuration YAML files and place these files in the input Cloud Storage bucket. These files can be used to rename objects, enable optimizations, enhance translations with Gemini and more. For more information about configuration YAML files, see [Create a configuration YAML file](https://docs.cloud.google.com/bigquery/docs/config-yaml-translation) .

9.  Click **Create** to start the translation job.

    After you create the translation job, you can see its status in the translation jobs list.

### bq

To use the gcloud CLI or the bq command-line tool command-line tool to submit a batch translation job, do the following steps.

These steps assume that you uploaded source files to a Cloud Storage bucket.

#### Create a translation configuration file

A translation configuration file defines the path to the source files, the output destination, and the source and target dialects of your translation. You can write this file in either YAML or JSON.

> **Note:** A translation configuration file is not the same as a [configuration YAML file](https://docs.cloud.google.com/bigquery/docs/config-yaml-translation) . A translation configuration file defines the job itself. A configuration YAML file customizes how the translator transforms your SQL.

The following example shows a translation configuration YAML file for a Teradata to BigQuery translation:

```
tasks:
  translation_task:
    type: Teradata2BigQuery_Translation
    translationDetails:
      sourceTargetMapping:
      - sourceSpec:
          baseUri: gs://bq-translations/input
        targetSpec:
          relativePath: output
      targetBaseUri: gs://bq-translations
      targetTypes:
      - sql
      sourceEnvironment:
        defaultDatabase: default_db
        schemaSearchPath:
        - foo
```

The following example shows a translation configuration JSON file for a Teradata to BigQuery translation:

```
{
  "tasks": {
    "translation_task": {
      "type": "Teradata2BigQuery_Translation",
      "translationDetails": {
        "sourceTargetMapping": [
          {
            "sourceSpec": {
              "literal": {
                "literalString": "sel 1",
                "relativePath": "my_input_1"
              },
              "encoding": "UTF-8"
            }
          },
          {
            "sourceSpec": {
              "literal": {
                "literalString": "sel 2",
                "relativePath": "my_input_2"
              },
              "encoding": "UTF-8"
            }
          }
        ],
        "targetReturnLiterals": [
          "sql/my_input_1",
          "sql/my_input_2"
        ]
      }
    }
  }
}
```

#### Submit the job with the Google Cloud CLI

To create a translation job and run the workflow, use the following command:

```
gcloud bq migration-workflows create --location=LOCATION --config-file=CONFIG_FILE
```

To create and run the workflow and return immediately with a link to the workflow, add the `--async` flag:

```
gcloud bq migration-workflows create --location=LOCATION --config-file=CONFIG_FILE --async
```

To list your translation jobs, use the following command:

```
gcloud bq migration-workflows list --location=LOCATION
```

To see the details of a specific translation job, use the following command:

```
gcloud bq migration-workflows describe projects/PROJECT_ID/locations/LOCATION/workflows/WORKFLOW_ID
```

Replace the following:

- `LOCATION` : the location of the Google Cloud project that is running this translation job.
- `CONFIG_FILE` : the path to your translation configuration file.
- `PROJECT_ID` : the ID of the Google Cloud project that is running this translation job.
- `WORKFLOW_ID` : the ID of the translation job.

#### Submit the job with the bq command-line tool command-line tool

To run the translation job, use the following command:

```
bq mk --migration_workflow --location=LOCATION --config_file=CONFIG_FILE
```

To list all your translation jobs, use the following command:

```
bq ls --migration_workflow --location=LOCATION
```

To view details about a specific translation job, use the following command:

```
bq show --migration_workflow projects/PROJECT_ID/locations/LOCATION/workflows/WORKFLOW_ID
```

To remove a translation job from the list, use the following command:

```
bq rm --migration_workflow projects/PROJECT_ID/locations/LOCATION/workflows/WORKFLOW_ID
```

Replace the following:

- `LOCATION` : the location of the Google Cloud project that is running this translation job.
- `CONFIG_FILE` : the path to your translation configuration file.
- `PROJECT_ID` : the ID of the Google Cloud project that is running this translation job.
- `WORKFLOW_ID` : the ID of the translation job.

#### Retrieve the output files

The translation job writes its results to the Cloud Storage directory that you set in the `targetBaseUri` field of the translation configuration file. This target directory holds the translated files, the translation summary report, and any AI suggestion files.

To copy the output to your local machine, use the following command:

```
gcloud storage cp --recursive TARGET_URI LOCAL_DIRECTORY
```

Replace the following:

- `TARGET_URI` : your target base URI, such as `gs://my_data_bucket/teradata/output/` .
- `LOCAL_DIRECTORY` : the local directory that receives the files.

Your job also appears in the translation jobs list in the Google Cloud console, even though you submitted it from the command line. To review the quality of a translation output, see [Explore the translation output](https://docs.cloud.google.com/bigquery/docs/batch-sql-translator#explore_the_translation_output) .

## Explore the translation output

You can review the results of a translation job in the Google Cloud console, regardless of whether the job was submitted from the command line or the Google Cloud console. The batch SQL translator outputs the following files to the specified destination:

- The translated files.
- The translation summary report in CSV format.
- The AI suggestion files.

### Google Cloud console output

To see translation job details, follow these steps:

1.  In the Google Cloud console, go to the **SQL Translation** page.

2.  In the list of translation jobs, locate the job for which you want to see the translation details. Then, click the translation job name. You can see a Sankey visualization that illustrates the overall quality of the job, the number of input lines of code (excluding blank lines and comments), and a list of issues that occurred during the translation process. You should prioritize fixes from left to right. Issues in an early stage can cause additional issues in subsequent stages.

3.  Hold the pointer over the error or warning bars, and review the suggestions to determine next steps to debug the translation job.

4.  Select the **Log Summary** tab to see a summary of the translation issues, including issue categories, suggested actions, and how often each issue occurred. You can click the Sankey visualization bars to filter issues. You can also select an issue category to see log messages associated with that issue category.

5.  Select the **Log Messages** tab to see more details about each translation issue, including the issue category, the specific issue message, and a link to the file in which the issue occurred. You can click the Sankey visualization bars to filter issues. You can select an issue in the **Log Message** tab to open the [**Code tab**](https://docs.cloud.google.com/bigquery/docs/batch-sql-translator#code-tab) that displays the input and output file if applicable.

6.  Click the **Job details** tab to see the translation job configuration details.

### Summary report

The summary report is a CSV file that contains a table of all of the warning and error messages encountered during the translation job.

To see the summary file in the Google Cloud console, follow these steps:

1.  In the Google Cloud console, go to the **SQL Translation** page.

2.  In the list of translation jobs, locate the job that you are interested in, then click the job name or click **More options \> Show details** .

3.  In the **Job details** tab, in the **Translation report** section, click **translation_report.csv** .

4.  On the **Object details** page, click the value in the **Authenticated URL** row to see the file in your browser.

The following table describes the summary file columns:

| **Column**          | **Description**                                                                                                                                                                   |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Timestamp           | The timestamp at which the issue occurred.                                                                                                                                        |
| FilePath            | The path to the source file that the issue is associated with.                                                                                                                    |
| FileName            | The name of the source file that the issue is associated with.                                                                                                                    |
| ScriptLine          | The line number where the issue occurred.                                                                                                                                         |
| ScriptColumn        | The column number where the issue occurred.                                                                                                                                       |
| TranspilerComponent | The translation engine internal component where the warning or error occurred. This column might be empty.                                                                        |
| Environment         | The translation dialect environment associated with the warning or error. This column might be empty.                                                                             |
| ObjectName          | The SQL object in the source file that is associated with the warning or error. This column might be empty.                                                                       |
| Severity            | The severity of the issue, either warning or error.                                                                                                                               |
| Category            | The translation issue category.                                                                                                                                                   |
| SourceType          | The source of this issue. The value in this column can either be `SQL` , indicating an issue in the input SQL files, or `METADATA` , indicating an issue in the metadata package. |
| Message             | The translation issue warning or error message.                                                                                                                                   |
| ScriptContext       | The SQL snippet in the source file that is associated with the issue.                                                                                                             |
| Action              | The action we recommend you take to resolve the issue.                                                                                                                            |

### Code tab

The code tab lets you review further information about the input and output files for a particular translation job. In the code tab, you can examine the files used in a translation job, review a side-by-side comparison of an input file and its translation for any inaccuracies, and view log summaries and messages for a specific file in a job.

To access the code tab, follow these steps:

1.  In the Google Cloud console, go to the **SQL Translation** page.

2.  In the list of translation jobs, locate the job that you are interested in, then click the job name or click **More options \> Show details** .

3.  Select **Code tab** . The code tab consists of the following panels:

    ![View the code tab in the SQL translation page.](https://docs.cloud.google.com/static/bigquery/images/sql-translation-code-tab.png)

    - File explorer: Contains all SQL files used for translation. Click a file to view its translation input and output, and any translation issues from its translation.
    - **Gemini-enhanced input** : The input SQL that was translated by the translation engine. If you have specified Gemini customization rules for the source SQL [in the Gemini configuration](https://docs.cloud.google.com/bigquery/docs/config-yaml-translation#ai_yaml_guidelines) , then the translator transforms the original input first and then translates the Gemini-enhanced input. To view the original input, click **View original input** .
    - **Translation output** : The translation result. If you have specified Gemini customization rules for the target SQL in [the Gemini configuration](https://docs.cloud.google.com/bigquery/docs/config-yaml-translation#ai_yaml_guidelines) , then the transformation is applied to the translated result as a Gemini-enhanced output. If a Gemini-enhanced output is available, then you can click the **Gemini suggestion** button to review the Gemini-enhanced output.

4.  Optional: To view an input file and its output file in the [BigQuery interactive SQL translator](https://docs.cloud.google.com/bigquery/docs/batch-sql-translator#debug-interactive-translator) , click **Edit** . You can edit the files and save the output file back to Cloud Storage.

> **Note:** You can view log summaries and messages for the overall translation job from the [Results page](https://docs.cloud.google.com/bigquery/docs/batch-sql-translator#explore_the_translation_output)

### Configuration tab

You can add, rename, view, or edit your configuration YAML files in the **Configuration** tab. The **Schema Explorer** shows the documentation for supported configuration types to help you write your configuration YAML files. After you edit the configuration YAML files, you can rerun the job to use the new configuration.

To access the configuration tab, follow these steps:

1.  In the Google Cloud console, go to the **SQL Translation** page.

2.  In the list of translation jobs, locate the job that you are interested in, then click the job name or click **More options \> Show details** .

3.  In the **Translation details** window, click the **Configuration** tab.

![View the configuration tab in the SQL translation page.](https://docs.cloud.google.com/static/bigquery/images/sql-translation-config-tab.png)

To add a new configuration file:

1.  Click more_vert **More options** \> **Create configuration YAML file** .
2.  A panel appears where you can choose the type, location, and name of the new configuration YAML file.
3.  Click **Create** .

To edit an existing configuration file:

1.  Click the configuration YAML file.
2.  Edit the file, then click **Save** .
3.  Click **Re-run** to run a new translation job that uses the edited configuration YAML files.

You can rename an existing configuration file by clicking more_vert **More options** \> **Rename** .

### Translated files

For each source file, a corresponding output file is generated in the destination path. The output file contains the translated query.

> **Important:** Translation is done on a best effort basis. Whenever possible, validate the translated queries.

## Handling unsupported SQL functions with helper UDFs

When translating SQL from a source dialect to BigQuery, some functions might not have a direct equivalent. To address this, the BigQuery Migration Service (and the broader BigQuery community) provide helper user-defined functions (UDFs) that replicate the behavior of these unsupported source dialect functions.

These UDFs are often found in the `bqutil` public dataset, allowing translated queries to initially reference them using the format `bqutil.<dataset>.<function>()` . For example, `bqutil.fn.cw_count()` .

### Considerations for production environments

While `bqutil` offers convenient access to these helper UDFs for initial translation and testing, direct reliance on `bqutil` for production workloads is not recommended for the following reasons:

1.  Version control: The `bqutil` project hosts the latest version of these UDFs, which means their definitions can change over time. Relying directly on `bqutil` could lead to unexpected behavior or breaking changes in your production queries if a UDF's logic is updated.
2.  Dependency isolation: Deploying UDFs to your own project isolates your production environment from external changes.
3.  Customization: You might need to modify or optimize these UDFs to better suit your specific business logic or performance requirements. This is only possible if they are within your own project.
4.  Security and governance: Your organization's security policies might restrict direct access to public datasets like `bqutil` for production data processing. Copying UDFs to your controlled environment aligns with such policies.

### Deploying helper UDFs to your project

To give you full control over UDF version, customization, and access, we recommend deploying helper UDFs into your own project and dataset for reliable and stable production use. For more information about the necessary scripts and steps to deploy helper UDFs into your environment, see [Deploying the UDFs](https://github.com/GoogleCloudPlatform/bigquery-utils/tree/master/udfs#deploying-the-udfs) .

## Troubleshooting

This section describes how to debug individual queries and how to resolve the most common translation errors.

### Debug batch translated SQL queries with the interactive SQL translator

You can use the BigQuery interactive SQL translator to review or debug a SQL query using the same metadata or object mapping information as your source database. After you complete a batch translation job, BigQuery generates a translation configuration ID that contains information about the job's metadata, the object mapping, or the schema search path, as applicable to the query. You use the batch translation configuration ID with the interactive SQL translator to run SQL queries with the specified configuration.

To start an interactive SQL translation by using a batch translation configuration ID, follow these steps:

1.  In the Google Cloud console, go to the **SQL Translation** page.

2.  In the list of translation jobs, locate the job that you are interested in, and then click more_vert **More Options \> Open Interactive Translation** .

    The BigQuery interactive SQL translator now opens with the corresponding batch translation configuration ID. To view the translation configuration ID for the interactive translation, click **Tools** \> **Query translation** \> **Translation settings** in the interactive SQL translator.

To debug a batch translation file in the interactive SQL translator, follow these steps:

1.  In the Google Cloud console, go to the **SQL Translation** page.

2.  In the list of translation jobs, locate the job that you are interested in, and then click the job name or click **More options \> Show details** .

3.  In the **Translation details** window, click the **Code** tab.

4.  In the file explorer, click your filename to open the file.

5.  Next to the output filename, click **Edit** to open the files in the interactive SQL translator ( [Preview](https://cloud.google.com/products/#product-launch-stages) ).

    You see the input and output files populated in the interactive SQL translator that now uses the corresponding batch translation configuration ID.

6.  To save the edited output file back to Cloud Storage, in the interactive SQL translator click **Save \> Save To GCS** .

### Troubleshoot translation errors

The following sections describe commonly encountered errors when using the batch SQL translator.

### `RelationNotFound` or `AttributeNotFound` translation issues

After translating a query using the [batch SQL translator](https://docs.cloud.google.com/bigquery/docs/batch-sql-translator#submit_a_translation_job) , you might encounter a failed translation with the `RelationNotFound` or `AttributeNotFound` error.

You can find failed translations by going to the **Translation details** page in BigQuery in the Google Cloud console and opening the **Log Messages** tab.

Translation works best with metadata DDLs. When SQL object definitions can't be found, the translation engine raises `RelationNotFound` or `AttributeNotFound` issues. We recommend using the metadata extractor to generate metadata packages to make sure all object definitions are present. Adding metadata is the recommended first step to resolve most translation errors, because this step often fixes many other errors that are indirectly caused by a lack of metadata.

For more information, see [Generate metadata for translation and assessment](https://docs.cloud.google.com/bigquery/docs/generate-metadata) .

#### Fix translation issues with Gemini

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> **Note:** To request feedback or support for this feature, contact <bq-edw-migration-support@google.com> .

To fix failed translation jobs with the `RelationNotFound` or `AttributeNotFound` errors, you can also use Gemini to resolve these issues:

1.  Go to the **Translation details** page and open the **Log Messages** tab.

2.  Click the query that has the message `RelationNotFound` or `AttributeNotFound` in the **Category** column.

3.  To go to the file and line containing the error in the code tab, click the

    error message.

4.  In the **Action** column, click **Suggested fix** .

5.  Select one of the following options, **Apply** or **Apply and rerun** :

    - To copy the generated schema file from the output directory to the input directory, click **Apply** .
    - To copy the generated schema file from the output directory to the input directory and open a rerun window, click **Apply and rerun** .

## Quota and limits

- [BigQuery Migration API quotas](https://docs.cloud.google.com/bigquery/quotas#migration-api-limits) apply.
- Each project can have at most 10 active translation tasks.
- While there is no hard limit on the total number of source and metadata files, we recommend keeping the number of files to under 1000 for better performance.

## Pricing

There is no charge to use the batch SQL translator. However, storage used to store input and output files incurs the normal fees. For more information, see [Storage pricing](https://cloud.google.com/bigquery/pricing#storage) .

## What's next

Learn more about the following steps in data warehouse migration:

- [Migration overview](https://docs.cloud.google.com/bigquery/docs/migration/migration-overview)
- [Migration assessment](https://docs.cloud.google.com/bigquery/docs/migration-assessment)
- [Schema and data transfer overview](https://docs.cloud.google.com/bigquery/docs/migration/schema-data-overview)
- [Data pipelines](https://docs.cloud.google.com/bigquery/docs/migration/pipelines)
- [Interactive SQL translation](https://docs.cloud.google.com/bigquery/docs/interactive-sql-translator)
- [Data security and governance](https://docs.cloud.google.com/bigquery/docs/data-governance)
- [Data validation tool](https://github.com/GoogleCloudPlatform/professional-services-data-validator#data-validation-tool)
