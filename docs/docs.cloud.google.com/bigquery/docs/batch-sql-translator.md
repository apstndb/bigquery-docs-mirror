# Migrate code with the batch SQL translator

**Note:** For API-based translations, including new batch translations, we recommend that you use the [BigQuery Migration API](/bigquery/docs/api-sql-translator) to translate your SQL scripts. The BigQuery Migration API works much like the batch SQL translator, but without the need to install or use client code.

This document describes how to use the batch SQL translator in BigQuery to translate scripts written in other SQL dialects into GoogleSQL queries. This document is intended for users who are familiar with the [Google Cloud console](/bigquery/docs/bigquery-web-ui) .

## Before you begin

Before you submit a translation job, complete the following steps:

1.  Ensure that you have all the required permissions.
2.  Enable the BigQuery Migration API.
3.  Collect the source files containing the SQL scripts and queries to be translated.
4.  Optional. Create a metadata file to improve the accuracy of the translation.
5.  Optional. Decide if you need to map SQL object names in the source files to new names in BigQuery. Determine what name mapping rules to use if this is necessary.
6.  Decide what method to use to submit the translation job.
7.  Upload the source files to Cloud Storage.

### Required permissions

You must have the following permissions on the project to enable the BigQuery Migration Service:

  - `  resourcemanager.projects.get  `
  - `  serviceusage.services.enable  `
  - `  serviceusage.services.get  `

You need the following permissions on the project to access and use the BigQuery Migration Service:

  - `  bigquerymigration.workflows.create  `

  - `  bigquerymigration.workflows.get  `

  - `  bigquerymigration.workflows.list  `

  - `  bigquerymigration.workflows.delete  `

  - `  bigquerymigration.subtasks.get  `

  - `  bigquerymigration.subtasks.list  `
    
    Alternatively, you can use the following roles to get the same permissions:
    
      - `  bigquerymigration.viewer  ` - Read only access.
      - `  bigquerymigration.editor  ` - Read/write access.

To access the Cloud Storage buckets for input and output files:

  - `  storage.objects.get  ` on the source Cloud Storage bucket.
  - `  storage.objects.list  ` on the source Cloud Storage bucket.
  - `  storage.objects.create  ` on the destination Cloud Storage bucket.

You can have all the above necessary Cloud Storage permissions from the following roles:

  - `  roles/storage.objectAdmin  `
  - `  roles/storage.admin  `

### Enable the BigQuery Migration API

If your Google Cloud CLI project was created before February 15, 2022, enable the BigQuery Migration API as follows:

1.  In the Google Cloud console, go to the **BigQuery Migration API** page.

2.  Click **Enable** .

**Note:** Projects created after February 15, 2022 have this API enabled automatically.

### Collect source files

Source files must be text files that contain valid SQL for the source dialect. Source files can also include comments. Do your best to ensure the SQL is valid, using whatever methods are available to you.

### Create metadata files

To help the service generate more accurate translation results, we recommend that you provide metadata files. However, this isn't mandatory.

You can use the `  dwh-migration-dumper  ` command-line extraction tool to generate the metadata information, or you can provide your own metadata files. Once metadata files are prepared, you can include them along with the source files in the translation source folder. The translator automatically detects them and leverages them to translate source files, you don't need to configure any extra settings to enable this.

To generate metadata information by using the `  dwh-migration-dumper  ` tool, see [Generate metadata for translation](/bigquery/docs/generate-metadata) .

To provide your own metadata, collect the data definition language (DDL) statements for the SQL objects in your source system into separate text files.

### Decide how to submit the translation job

You have three options for submitting a batch translation job:

  - **Batch translation client** : Configure a job by changing settings in a configuration file, and submit the job using the command line. This approach doesn't require you to manually upload source files to Cloud Storage. The client still uses Cloud Storage to store files during translation job processing.
    
    The legacy batch translation client is an open-source Python client that lets you translate source files located on your local machine and have the translated files output to a local directory. You configure the client for basic use by changing a few settings in its configuration file. If you choose to, you can also configure the client to address more complex tasks like macro replacement, and pre- and postprocessing of translation inputs and outputs. For more information, see the batch translation client [readme](https://github.com/google/dwh-migration-tools/blob/main/client/README.md) .

  - **Google Cloud console** : Configure and submit a job using a user interface. This approach requires you to upload source files to Cloud Storage.

### Create configuration YAML files

You can optionally create and use configuration [configuration YAML files](/bigquery/docs/config-yaml-translation) to customize your batch translations. These files can be used to transform your translation output in various ways. For example, you can [create a configuration YAML file to change the case of a SQL object](/bigquery/docs/config-yaml-translation#change_object-name_case) during translation.

If you want to use the Google Cloud console or the BigQuery Migration API for a batch translation job, you can [upload the configuration YAML file to the Cloud Storage bucket containing the source files](#upload-files) .

If you want to use the batch translation client, you can place the configuration YAML file in the local translation input folder.

### Upload input files to Cloud Storage

If you want to use the Google Cloud console or the BigQuery Migration API to perform a translation job, you must upload the source files containing the queries and scripts you want to translate to Cloud Storage. You can also upload [any metadata files](/bigquery/docs/generate-metadata) or [configuration YAML files](/bigquery/docs/config-yaml-translation) to the same Cloud Storage bucket and directory containing the source files. For more information about creating buckets and uploading files to Cloud Storage, see [Create buckets](/storage/docs/creating-buckets) and [Upload objects from a filesystem](/storage/docs/uploading-objects) .

## Supported SQL dialects

The batch SQL translator is part of the BigQuery Migration Service. The batch SQL translator can translate the following SQL dialects into GoogleSQL:

  - Amazon Redshift SQL
  - Apache HiveQL and Beeline CLI
  - IBM Netezza SQL and NZPLSQL
  - Teradata and Teradata Vantage:
      - SQL
      - Basic Teradata Query (BTEQ)
      - Teradata Parallel Transport (TPT)

Additionally, translation of the following SQL dialects is supported in [preview](https://cloud.google.com/products/#product-launch-stages) :

  - Apache Impala SQL
  - Apache Spark SQL
  - Azure Synapse T-SQL
  - GoogleSQL (BigQuery)
  - Greenplum SQL
  - IBM DB2 SQL
  - MySQL SQL
  - Oracle SQL, PL/SQL, Exadata
  - PostgreSQL SQL
  - Trino or PrestoSQL
  - Snowflake SQL
  - SQL Server T-SQL
  - SQLite
  - Vertica SQL

**Important:** Translation is done on a best effort basis. Translation success can vary, depending on the uniqueness and complexity of the SQL statements in your source scripts. You might need to manually translate some scripts. Use the **Actions** tab in the [Google Cloud console output](#output) to diagnose and correct translation issues.

### Handling unsupported SQL functions with helper UDFs

When translating SQL from a source dialect to BigQuery, some functions might not have a direct equivalent. To address this, the BigQuery Migration Service (and the broader BigQuery community) provide helper user-defined functions (UDFs) that replicate the behavior of these unsupported source dialect functions.

These UDFs are often found in the `  bqutil  ` public dataset, allowing translated queries to initially reference them using the format `  bqutil.<dataset>.<function>()  ` . For example, `  bqutil.fn.cw_count()  ` .

#### Important considerations for production environments:

While `  bqutil  ` offers convenient access to these helper UDFs for initial translation and testing, direct reliance on `  bqutil  ` for production workloads is not recommended for several reasons:

1.  Version control: The `  bqutil  ` project hosts the latest version of these UDFs, which means their definitions can change over time. Relying directly on `  bqutil  ` could lead to unexpected behavior or breaking changes in your production queries if a UDF's logic is updated.
2.  Dependency isolation: Deploying UDFs to your own project isolates your production environment from external changes.
3.  Customization: You might need to modify or optimize these UDFs to better suit your specific business logic or performance requirements. This is only possible if they are within your own project.
4.  Security and governance: Your organization's security policies might restrict direct access to public datasets like `  bqutil  ` for production data processing. Copying UDFs to your controlled environment aligns with such policies.

#### Deploying helper UDFs to your project:

For reliable and stable production use, you should deploy these helper UDFs into your own project and dataset. This gives you full control over their version, customization, and access. For detailed instructions on how to deploy these UDFs, refer to the [UDFs deployment guide on GitHub](https://github.com/GoogleCloudPlatform/bigquery-utils/tree/master/udfs#deploying-the-udfs) . This guide provides the necessary scripts and steps to copy the UDFs into your environment.

## Locations

The batch SQL translator is available in the following processing locations:

**Region description**

**Region name**

**Details**

**Asia Pacific**

Delhi

`  asia-south2  `

Hong Kong

`  asia-east2  `

Jakarta

`  asia-southeast2  `

Melbourne

`  australia-southeast2  `

Mumbai

`  asia-south1  `

Osaka

`  asia-northeast2  `

Seoul

`  asia-northeast3  `

Singapore

`  asia-southeast1  `

Sydney

`  australia-southeast1  `

Taiwan

`  asia-east1  `

Tokyo

`  asia-northeast1  `

**Europe**

Belgium

`  europe-west1  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Berlin

`  europe-west10  `

EU multi-region

`  eu  `

Finland

`  europe-north1  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Frankfurt

`  europe-west3  `

London

`  europe-west2  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Madrid

`  europe-southwest1  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Milan

`  europe-west8  `

Netherlands

`  europe-west4  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Paris

`  europe-west9  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Stockholm

`  europe-north2  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Turin

`  europe-west12  `

Warsaw

`  europe-central2  `

Zürich

`  europe-west6  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

**Americas**

Columbus, Ohio

`  us-east5  `

Dallas

`  us-south1  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Iowa

`  us-central1  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Las Vegas

`  us-west4  `

Los Angeles

`  us-west2  `

Mexico

`  northamerica-south1  `

Northern Virginia

`  us-east4  `

Oregon

`  us-west1  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Québec

`  northamerica-northeast1  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

São Paulo

`  southamerica-east1  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Salt Lake City

`  us-west3  `

Santiago

`  southamerica-west1  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

South Carolina

`  us-east1  `

Toronto

`  northamerica-northeast2  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

US multi-region

`  us  `

**Africa**

Johannesburg

`  africa-south1  `

**MiddleEast**

Dammam

`  me-central2  `

Doha

`  me-central1  `

Israel

`  me-west1  `

## Submit a translation job

Follow these steps to start a translation job, view its progress, and see the results.

### Console

These steps assume you have source files uploaded into a Cloud Storage bucket already.

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the navigation menu, click **Tools and guide** .

3.  In the **Translate SQL** panel, click **Translate** \> **Batch translation** .

4.  The translation configuration page opens. Enter the following details:
    
    1.  For **Display name** , type a name for the translation job. The name can contain letters, numbers or underscores.
    2.  For **Processing location** , select the location where you want the translation job to run. For example, if you are in Europe and you don't want your data to cross any location boundaries, select the `  eu  ` region. The translation job performs best when you choose the same location as your source file bucket.
    3.  For **Source dialect** , select the SQL dialect that you want to translate.
    4.  For **Target dialect** , select **BigQuery** .

5.  Click **Next** .

6.  For **Source location** , specify the path to the Cloud Storage folder containing the files to translate. You can type the path in the format `  bucket_name/folder_name/  ` or use the **Browse** option.

7.  Click **Next** .

8.  For **Target location** , specify the path to the destination Cloud Storage folder for the translated files. You can type the path in the format `  bucket_name/folder_name/  ` or use the **Browse** option.

9.  If you're doing translations that don't need to have default object names or source-to-target name mapping specified, skip to Step 11. Otherwise, click **Next** .

10. Fill in the optional settings that you need.
    
    1.  Optional. For **Default database** , type a [default database name](/bigquery/docs/output-name-mapping#default_database) to use with the source files. The translator uses this default database name to resolve SQL objects' [fully qualified names](/bigquery/docs/output-name-mapping#name_parts) where the database name is missing.
    
    2.  Optional. For **Schema search path** , specify a schema to search when the translator needs to resolve SQL objects' [fully qualified names](/bigquery/docs/output-name-mapping#name_parts) in the source files where the schema name is missing. If the source files use a number of different schema names, click **Add Schema Name** and add a value for each schema name that might be referenced.
        
        The translator searches through the metadata files you provided to validate tables with their schema names. If a definite option can't be determined from the metadata, the first schema name you enter is used as the default. For more information on how the default schema name is used, see [default schema](/bigquery/docs/output-name-mapping#default_schema) .
    
    3.  Optional. If you want to specify [name mapping rules](/bigquery/docs/output-name-mapping) to rename SQL objects between the source system and BigQuery during translation, you can either provide a [JSON file](/bigquery/docs/output-name-mapping#json_file_format) with the name mapping pair, or you can use the Google Cloud console to specify the values to map.
        
        To use a JSON file:
        
        1.  Click **Upload JSON file for name mapping** .
        
        2.  Browse to the location of a name mapping file in the [appropriate format](/bigquery/docs/output-name-mapping#json_file_format) , select it, and click **Open** .
            
            Note that the file size must be less than 5 MB.
        
        To use the Google Cloud console:
        
        1.  Click **Add name mapping pair** .
        2.  Add the appropriate parts of the source object name in the **Database** , **Schema** , **Relationship** , and **Attribute** fields in the **Source** column.
        3.  Add the parts of the target object name in BigQuery in the fields in the **Target** column.
        4.  For **Type** , select the object type that describes the object you are mapping.
        5.  Repeat Steps 1 - 4 until you have specified all of the name mapping pairs that you need. Note that you can only specify up to 25 name mapping pairs when using the Google Cloud console.
    
    4.  Optional. To generate translation AI suggestions using the Gemini model, select the **Gemini AI suggestions** checkbox. Suggestions are based on the configuration YAML file ending in `  .ai_config.yaml  ` and located in the Cloud Storage directory. Each type of suggestion output is saved in its own sub-directory within your output folder with the naming pattern `  REWRITE TARGET SUGGESTION_TYPE _suggestion  ` . For example, suggestions for the Gemini-enhanced target SQL customization is stored in `  target_sql_query_customization_suggestion  ` and the translation explanation generated by Gemini is stored in `  translation_explanation_suggestion  ` . To learn how to write the configuration YAML file for AI suggestions, see [Create a Gemini-based configuration YAML file](/bigquery/docs/config-yaml-translation#ai_yaml_guidelines) .

11. Click **Create** to start the translation job.

Once the translation job is created, you can see its status in the translation jobs list.

### Batch translation client

**Note:** We recommend that new translations use the [BigQuery Migration API](/bigquery/docs/api-sql-translator) instead of the batch translation client.

1.  [Install the batch translation client and the Google Cloud CLI](https://github.com/google/dwh-migration-tools/blob/main/client/README.md#installation) .

2.  [Generate a gcloud CLI credential file](https://github.com/google/dwh-migration-tools/blob/main/client/README.md#optional-gcloud-login-and-authentication) .

3.  In the batch translation client installation directory, use the text editor of your choice to open the `  config.yaml  ` file and modify the following settings:
    
      - `  project_number  ` : Type the project number of the project you want to use for the batch translation job. You can find this in the **Project info** pane on the [Google Cloud console welcome page](https://console.cloud.google.com/welcome) for the project.
      - `  gcs_bucket  ` : Type the name of the Cloud Storage bucket that the batch translation client uses to store files during translation job processing.
      - `  input_directory  ` : Type the absolute or relative path to the directory containing the source files and any metadata files.
      - `  output_directory  ` : Type the absolute or relative path to the target directory for the translated files.

4.  Save the changes and close the `  config.yaml  ` file.

5.  Place your source and metadata files in the input directory.

6.  Run the batch translation client using the following command:
    
    ``` text
    bin/dwh-migration-client
    ```

7.  Create a translation job.
    
      - The following example shows a command to create a translation job. The command will run the workflow and show output if this workflow is successful.
        
        ``` text
        gcloud bq migration-workflows create --location=us --config-file=CONFIG_FILE_NAME.json
        ```
    
      - The following example shows a command to create and run the workflow with the `  --async  ` flag. The command will create and run the workflow and return immediately with a link to the workflow.
        
        ``` text
        gcloud bq migration-workflows create --location=LOCATION  --config-file=CONFIG_FILE_NAME.json --async
        ```
    
      - The following example shows a command to list your translation jobs:
        
        ``` text
        gcloud bq migration-workflows list --location=LOCATION
        ```
    
    Replace the following:
    
      - `  LOCATION  ` : the location of the Google Cloud project that is running this translation job.
      - `  CONFIG_FILE_NAME  ` : the name of the `  config.yaml  ` file. Once the translation job is created, you can see its status in the translation jobs list in the Google Cloud console.

8.  Optional. Once the translation job is completed, delete the files that the job created in the Cloud Storage bucket you specified, in order to avoid storage costs.

### BigQuery CLI

You can run the batch SQL translator using the bq command-line tool command-line tool with the following steps:

1.  Create a translation configuration file in either YAML or JSON. In this file, you must define the path to the source file, the output destination, and the source and target dialects of your translation.
    
    The following example shows a translation configuration YAML file for a Teradata to BigQuery translation:
    
    ``` text
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
    
    ``` text
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

2.  Once the translation configuration is created, run the following command to run the translation job.
    
    ``` text
    bq mk --migration_workflow --location=LOCATION --config_file=CONFIG_FILE_NAME.json
    ```
    
    Replace the following:
    
      - `  LOCATION  ` : the location of the Google Cloud project that is running this translation job.
      - `  CONFIG_FILE_NAME  ` : the name of the `  config.yaml  ` file.

<!-- end list -->

  - To view details about a specific translation job, run the following command:
    
    ``` text
    bq show --migration_workflow projects/PROJECT_ID/ locations/us/workflows/WORKFLOW_ID
    ```
    
    Replace the following:
    
      - `  PROJECT_ID  ` : the ID of the Google Cloud project that is running this translation job.
      - `  WORKFLOW_ID  ` : the ID of the translation job.

  - To see the results of a specific translation job, run the following command:
    
    ``` text
    gcloud bq migration-workflows describe projects/PROJECT_ID    /locations/us/workflows/WORKFLOW_ID
    ```

  - To remove a translation job from the list, run the following command:
    
    ``` text
    bq rm --migration_workflow projects/PROJECT_ID/locations/us/workflows/WORKFLOW_ID
    ```

  - To list all your translation jobs, run the following command:
    
    ``` text
    bq ls --migration_workflow --location=LOCATION
    ```

## Explore the translation output

After running the translation job, you can see information about the job in the Google Cloud console. If you used the Google Cloud console to run the job, you can see job results in the destination Cloud Storage bucket that you specified. If you used the batch translation client to run the job, you can see job results in the output directory that you specified. The batch SQL translator outputs the following files to the specified destination:

  - The translated files.
  - The translation summary report in CSV format.
  - The consumed output name mapping in JSON format.
  - The AI suggestion files.

### Google Cloud console output

To see translation job details, follow these steps:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the navigation menu, click **SQL translation** .

3.  In the list of translation jobs, locate the job for which you want to see the translation details. Then, click the translation job name. You can see a Sankey visualization that illustrates the overall quality of the job, the number of input lines of code (excluding blank lines and comments), and a list of issues that occurred during the translation process. You should prioritize fixes from left to right. Issues in an early stage can cause additional issues in subsequent stages.

4.  Hold the pointer over the error or warning bars, and review the suggestions to determine next steps to debug the translation job.

5.  Select the **Log Summary** tab to see a summary of the translation issues, including issue categories, suggested actions, and how often each issue occurred. You can click the Sankey visualization bars to filter issues. You can also select an issue category to see log messages associated with that issue category.

6.  Select the **Log Messages** tab to see more details about each translation issue, including the issue category, the specific issue message, and a link to the file in which the issue occurred. You can click the Sankey visualization bars to filter issues. You can select an issue in the **Log Message** tab to open the [**Code tab**](/bigquery/docs/batch-sql-translator#code-tab) that displays the input and output file if applicable.

7.  Click the **Job details** tab to see the translation job configuration details.

### Summary report

The summary report is a CSV file that contains a table of all of the warning and error messages encountered during the translation job.

To see the summary file in the Google Cloud console, follow these steps:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the navigation menu, click **SQL translation** .

3.  In the list of translation jobs, locate the job that you are interested in, then click the job name or click **More options \> Show details** .

4.  In the **Job details** tab, in the **Translation report** section, click **translation\_report.csv** .

5.  On the **Object details** page, click the value in the **Authenticated URL** row to see the file in your browser.

The following table describes the summary file columns:

<table>
<thead>
<tr class="header">
<th><strong>Column</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Timestamp</td>
<td>The timestamp at which the issue occurred.</td>
</tr>
<tr class="even">
<td>FilePath</td>
<td>The path to the source file that the issue is associated with.</td>
</tr>
<tr class="odd">
<td>FileName</td>
<td>The name of the source file that the issue is associated with.</td>
</tr>
<tr class="even">
<td>ScriptLine</td>
<td>The line number where the issue occurred.</td>
</tr>
<tr class="odd">
<td>ScriptColumn</td>
<td>The column number where the issue occurred.</td>
</tr>
<tr class="even">
<td>TranspilerComponent</td>
<td>The translation engine internal component where the warning or error occurred. This column might be empty.</td>
</tr>
<tr class="odd">
<td>Environment</td>
<td>The translation dialect environment associated with the warning or error. This column might be empty.</td>
</tr>
<tr class="even">
<td>ObjectName</td>
<td>The SQL object in the source file that is associated with the warning or error. This column might be empty.</td>
</tr>
<tr class="odd">
<td>Severity</td>
<td>The severity of the issue, either warning or error.</td>
</tr>
<tr class="even">
<td>Category</td>
<td>The translation issue category.</td>
</tr>
<tr class="odd">
<td>SourceType</td>
<td>The source of this issue. The value in this column can either be <code dir="ltr" translate="no">       SQL      </code> , indicating an issue in the input SQL files, or <code dir="ltr" translate="no">       METADATA      </code> , indicating an issue in the metadata package.</td>
</tr>
<tr class="even">
<td>Message</td>
<td>The translation issue warning or error message.</td>
</tr>
<tr class="odd">
<td>ScriptContext</td>
<td>The SQL snippet in the source file that is associated with the issue.</td>
</tr>
<tr class="even">
<td>Action</td>
<td>The action we recommend you take to resolve the issue.</td>
</tr>
</tbody>
</table>

### Code tab

The code tab lets you review further information about the input and output files for a particular translation job. In the code tab, you can examine the files used in a translation job, review a side-by-side comparison of an input file and its translation for any inaccuracies, and view log summaries and messages for a specific file in a job.

To access the code tab, follow these steps:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the navigation menu, click **SQL translation** .

3.  In the list of translation jobs, locate the job that you are interested in, then click the job name or click **More options \> Show details** .

4.  Select **Code tab** . The code tab consists of the following panels:
    
      - File explorer: Contains all SQL files used for translation. Click a file to view its translation input and output, and any translation issues from its translation.
      - **Gemini-enhanced input** : The input SQL that was translated by the translation engine. If you have specified Gemini customization rules for the source SQL [in the Gemini configuration](/bigquery/docs/config-yaml-translation#ai_yaml_guidelines) , then the translator transforms the original input first and then translates the Gemini-enhanced input. To view the original input, click **View original input** .
      - **Translation output** : The translation result. If you have specified Gemini customization rules for the target SQL in [the Gemini configuration](/bigquery/docs/config-yaml-translation#ai_yaml_guidelines) , then the transformation is applied to the translated result as a Gemini-enhanced output. If a Gemini-enhanced output is available, then you can click the **Gemini suggestion** button to review the Gemini-enhanced output.

5.  Optional: To view an input file and its output file in the [BigQuery interactive SQL translator](#debug-interactive-translator) , click **Edit** . You can edit the files and save the output file back to Cloud Storage.

**Note:** You can view log summaries and messages for the overall translation job from the [Results page](/bigquery/docs/batch-sql-translator#explore_the_translation_output)

### Configuration tab

You can add, rename, view, or edit your configuration YAML files in the **Configuration** tab.The **Schema Explorer** shows the documentation for supported configuration types to help you write your configuration YAML files. After you edit the configuration YAML files, you can rerun the job to use the new configuration.

To access the configuration tab, follow these steps:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the navigation menu, click **SQL translation** .

3.  In the list of translation jobs, locate the job that you are interested in, then click the job name or click **More options \> Show details** .

4.  In the **Translation details** window, click the **Configuration** tab.

To add a new configuration file:

1.  Click more\_vert **More options** \> **Create configuration YAML file** .
2.  A panel appears where you can choose the type, location, and name of the new configuration YAML file.
3.  Click **Create** .

To edit an existing configuration file:

1.  Click on the configuration YAML file.
2.  Edit the file, then click **Save** .
3.  Click **Re-run** to run a new translation job that uses the edited configuration YAML files.

You can rename an existing configuration file by clicking more\_vert **More options** \> **Rename** .

### Consumed output name mapping file

This JSON file contains the output name mapping rules that were used by the translation job. The rules in this file might differ from the [output name mapping](/bigquery/docs/output-name-mapping) rules that you specified for the translation job, due to either conflicts in the name mapping rules, or lack of name mapping rules for SQL objects that were identified during translation. Review this file to determine whether the name mapping rules need correction. If they do, create new output name mapping rules that address any issues you identify, and run a new translation job.

### Translated files

For each source file, a corresponding output file is generated in the destination path. The output file contains the translated query.

**Important:** Translation is done on a best effort basis. Whenever possible, validate the translated queries.

## Debug batch translated SQL queries with the interactive SQL translator

You can use the BigQuery interactive SQL translator to review or debug a SQL query using the same metadata or object mapping information as your source database. After you complete a batch translation job, BigQuery generates a translation configuration ID that contains information about the job's metadata, the object mapping, or the schema search path, as applicable to the query. You use the batch translation configuration ID with the interactive SQL translator to run SQL queries with the specified configuration.

To start an interactive SQL translation by using a batch translation configuration ID, follow these steps:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the navigation menu, click **SQL translation** .

3.  In the list of translation jobs, locate the job that you are interested in, and then click more\_vert **More Options \> Open Interactive Translation** .
    
    The BigQuery interactive SQL translator now opens with the corresponding batch translation configuration ID. To view the translation configuration ID for the interactive translation, click **More \> Translation settings** in the interactive SQL translator.

To debug a batch translation file in the interactive SQL translator, follow these steps:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the navigation menu, click **SQL translation** .

3.  In the list of translation jobs, locate the job that you are interested in, and then click the job name or click **More options \> Show details** .

4.  In the **Translation details** window, click the **Code** tab.

5.  In the file explorer, click your filename to open the file.

6.  Next to the output filename, click **Edit** to open the files in the interactive SQL translator ( [Preview](https://cloud.google.com/products/#product-launch-stages) ).
    
    You see the input and output files populated in the interactive SQL translator that now uses the corresponding batch translation configuration ID.

7.  To save the edited output file back to Cloud Storage, in the interactive SQL translator click **Save \> Save To GCS** .

## Limitations

The translator can't translate user-defined functions (UDFs) from languages other than SQL, because it can't parse them to determine their input and output data types. This causes translation of SQL statements that reference these UDFs to be inaccurate. To make sure non-SQL UDFs are properly referenced during translation, use valid SQL to create placeholder UDFs with the same signatures.

For example, say you have a UDF written in C that calculates the sum of two integers. To make sure that SQL statements that reference this UDF are correctly translated, create a placeholder SQL UDF that shares the same signature as the C UDF, as shown in the following example:

``` text
CREATE FUNCTION Test.MySum (a INT, b INT)
  RETURNS INT
  LANGUAGE SQL
  RETURN a + b;
```

Save this placeholder UDF in a text file, and include that file as one of the source files for the translation job. This enables the translator to learn the UDF definition and identify the expected input and output data types.

## Quota and limits

  - [BigQuery Migration API quotas](/bigquery/quotas#migration-api-limits) apply.
  - Each project can have at most 10 active translation tasks.
  - While there is no hard limit on the total number of source and metadata files, we recommend keeping the number of files to under 1000 for better performance.

## Troubleshoot translation errors

### `     RelationNotFound    ` or `     AttributeNotFound    ` translation issues

After translating a querying using the [batch SQL translator](/bigquery/docs/batch-sql-translator#submit_a_translation_job) , you might encounter a failed translation with the `  RelationNotFound  ` or `  AttributeNotFound  ` error.

You can find failed translations by navigating to the **Translation details** page and opening the **Log Messages** tab.

Translation works best with metadata DDLs. When SQL object definitions cannot be found, the translation engine raises `  RelationNotFound  ` or `  AttributeNotFound  ` issues. We recommend using the metadata extractor to generate metadata packages to make sure all object definitions are present. Adding metadata is the recommended first step to resolve most translation errors, as it often can fix many other errors that are indirectly caused from a lack of metadata.

For more information, see [Generate metadata for translation and assessment](/bigquery/docs/generate-metadata) .

#### Fix translation issues with Gemini

**Preview**

This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

**Note:** To request feedback or support for this feature, contact <bq-edw-migration-support@google.com> .

To fixed failed translation jobs with the `  RelationNotFound  ` or `  AttributeNotFound  ` errors, you can also use Gemini to try to resolve these issues with the following steps.

1.  Navigate to the **Translation details** page and open the **Log Messages** tab.

2.  Click the query that has the message `  RelationNotFound  ` or `  AttributeNotFound  ` in the **Category** column.

3.  Click the error message to navigate to the file and line containing the error in the code tab.

4.  In the **Action** column, click **Suggested fix** .

5.  Select one of the following options: **Apply** or **Apply and rerun** :
    
      - Click **Apply** to copy the generated schema file from the output directory to the input directory.
      - Click **Apply and rerun** to copy the generated schema file from the output directory to the input directory and opens a rerun window.

## Pricing

There is no charge to use the batch SQL translator. However, storage used to store input and output files incurs the normal fees. For more information, see [Storage pricing](https://cloud.google.com/bigquery/pricing#storage) .

## What's next

Learn more about the following steps in data warehouse migration:

  - [Migration overview](/bigquery/docs/migration/migration-overview)
  - [Migration assessment](/bigquery/docs/migration-assessment)
  - [Schema and data transfer overview](/bigquery/docs/migration/schema-data-overview)
  - [Data pipelines](/bigquery/docs/migration/pipelines)
  - [Interactive SQL translation](/bigquery/docs/interactive-sql-translator)
  - [Data security and governance](/bigquery/docs/data-governance)
  - [Data validation tool](https://github.com/GoogleCloudPlatform/professional-services-data-validator#data-validation-tool)
