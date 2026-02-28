# Migrate Hive managed tables to Google Cloud

**Preview**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

**Note:** To get support or provide feedback for this feature, contact <bigquery-permission-migration-support@google.com> .

This document shows you how to migrate your Hive managed tables to Google Cloud.

You can use the Hive managed tables migration connector in the BigQuery Data Transfer Service to seamlessly migrate your tables managed by Hive metastore, supporting both Hive and Iceberg formats from on-premises and cloud environments to Google Cloud. The Hive managed tables migration connector supports files stored in the following data sources:

  - HDFS
  - Amazon S3
  - Azure Blob Storage or Azure Data Lake Storage Gen2

With the Hive managed tables migration connector, you can register your Hive managed tables with [Dataproc Metastore](/dataproc-metastore/docs/overview) , [BigLake metastore](/bigquery/docs/about-blms) , or [BigLake metastore Iceberg REST Catalog](/bigquery/docs/blms-rest-catalog) while using Cloud Storage as the file storage.

This connector supports both full and metadata-only transfers. Full transfers will transfer both your data and metadata from your source tables to your target metastore. You can make a metadata-only transfer if you already have your data migrated to Cloud Storage.

The following diagram provides an overview of the table migration process from Hadoop cluster.

## Limitations

Hive managed tables transfers are subject to the following limitations:

  - To migrate Apache Iceberg tables, you must register the tables with BigLake metastore to allow write access for open-source engines (such as Apache Spark or Flink), and to allow read access for BigQuery.
  - To migrate Hive managed tables, you must register the tables with Dataproc Metastore to allow write access for open-source engines, and to allow read access for BigQuery.
  - You must use the bq command-line tool to migrate Hive managed tables to BigQuery.

## Before you begin

Before you schedule Hive managed tables transfer, you must perform the following:

### Generate metadata file for Apache Hive

Run the `  dwh-migration-dumper  ` tool to [extract metadata](/bigquery/docs/hadoop-metadata#apache-hive) for Apache Hive. The tool generates a file named `  hive-dumper-output.zip  ` to a Cloud Storage bucket, referred to in this document as `  DUMPER_BUCKET  ` .

### Enable APIs

[Enable the following APIs](/endpoints/docs/openapi/enable-api) in your Google Cloud project:

  - Data Transfer API
  - Storage Transfer API

A [service agent](/bigquery/docs/enable-transfer-service#service_agent) is created when you enable the Data Transfer API.

### Configure permissions

1.  Create a service account and grant it the BigQuery Admin role ( `  roles/bigquery.admin  ` ). This service account is used to create the transfer configuration.

2.  A [service agent](/bigquery/docs/enable-transfer-service#service_agent) (P4SA) is created upon enabling the Data Transfer API. Grant it the following roles:
    
      - `  roles/metastore.metadataOwner  `
      - `  roles/storagetransfer.admin  `
      - `  roles/serviceusage.serviceUsageConsumer  `
      - `  roles/storage.objectAdmin  `
          - If you are migrating metadata for BigLake Iceberg tables, you must also grant the `  roles/bigquery.admin  ` role.
          - If you are migrating metadata to BigLake metastore Iceberg REST Catalog, you must also grant the `  roles/biglake.admin  ` role.

3.  Grant the service agent the `  roles/iam.serviceAccountTokenCreator  ` role with the following command:
    
    ``` text
    gcloud iam service-accounts add-iam-policy-binding SERVICE_ACCOUNT --member serviceAccount:service-PROJECT_NUMBER@gcp-sa-bigquerydatatransfer.iam.gserviceaccount.com --role roles/iam.serviceAccountTokenCreator
    ```

### Configure your Storage Transfer Agent for HDFS data lakes

Required when the file is stored in HDFS. To set up the storage transfer agent required for an HDFS data lake transfer, do the following:

1.  [Configure permissions](/storage-transfer/docs/file-system-permissions) to run the storage transfer agent on your Hadoop cluster.
2.  [Install Docker](/storage-transfer/docs/on-prem-set-up#install_docker) on on-premises agent machines.
3.  [Create a Storage Transfer Service agent pool](/storage-transfer/docs/on-prem-agent-pools#create-pool) in your Google Cloud project.
4.  [Install agents](/storage-transfer/docs/create-transfers/agent-based/hdfs#install_agents) on your on-premises agent machines.

### Configure Storage Transfer Service permissions for Amazon S3

Required when the file is stored in Amazon S3. Transfers from Amazon S3 are agentless transfers, which require specific permissions. To configure the Storage Transfer Service for a Amazon S3 transfer, do the following:

1.  [Configure agentless transfer permissions](/storage-transfer/docs/iam-cloud) .
2.  [Setup access credentials for AWS Amazon S3](/storage-transfer/docs/source-amazon-s3#access_credentials) .
      - Note the access key ID and secret access key after setting up your access credentials.
3.  [Add IP ranges](/storage-transfer/docs/source-amazon-s3#ip_restrictions) used by Storage Transfer Service workers to your list of allowed IPs if your AWS project uses IP restrictions.

### Configure Storage Transfer Service permissions for Microsoft Azure Storage

Required when the file is stored in Azure Blob Storage or Azure Data Lake Storage Gen2. Transfers from Microsoft Azure Storage are agentless transfers, which require specific permissions. To configure the Storage Transfer Service for a Microsoft Azure Storage transfer, do the following:

1.  [Configure agentless transfer permissions](/storage-transfer/docs/iam-cloud) .
2.  [Generate a Shared Access Signature (SAS) token](/storage-transfer/docs/source-microsoft-azure#sas-token) for your Microsoft Azure storage account.
      - Note the SAS token after generating it.
3.  [Add IP ranges](/storage-transfer/docs/source-microsoft-azure#ip_restrictions) used by Storage Transfer Service workers to your list of allowed IPs if your Microsoft Azure storage account uses IP restrictions.

## Schedule Hive managed tables transfer

Select one of the following options:

### Console

1.  Go to the Data transfers page in the Google Cloud console.

2.  Click add **Create transfer** .

3.  In the **Source type** section, select **Hive Managed Tables** from the **Source** list.

4.  For **Location** , select a location type, and then select a region.

5.  In the **Transfer config name** section, for **Display name** , enter a name for the data transfer.

6.  In the **Schedule options** section, do the following:
    
      - In the **Repeat frequency** list, select an option to specify how often this data transfer runs. To specify a custom repeat frequency, select **Custom** . If you select **On-demand** , then this transfer runs when you [manually trigger the transfer](/bigquery/docs/working-with-transfers#manually_trigger_a_transfer) .
      - If applicable, select either **Start now** or **Start at set time** , and provide a start date and run time.

7.  In the **Data source details** section, do the following:
    
    1.  For **Transfer strategy** , select one of the following:
        
          - `  FULL_TRANSFER  ` : Transfer all data and register metadata with the target metastore. This is the default option.
          - `  METADATA_ONLY  ` : Register metadata only. You must have data already present in the correct Cloud Storage location referenced in the metadata.
    
    2.  For **Table name patterns** , specify HDFS data lake tables to transfer by providing table names or patterns that matches tables in the HDFS database. You must use Java regular expression syntax to specify table patterns. For example:
        
          - `  db1..*  ` matches all tables in db1.
          - `  db1.table1;db2.table2  ` matches table1 in db1 and table2 in db2.
    
    3.  For **BQMS discovery dump gcs path** , enter the path to the bucket that contains the `  hive-dumper-output.zip  ` file that you generated when [creating a metadata file for Apache Hive](#generate-metadata-dump-for-apache-hive) .
    
    4.  Choose the Metastore type from the drop-down list:
        
          - `  DATAPROC_METASTORE  ` : Select this option to store your metadata in Dataproc Metastore. You must provide the URL for the Dataproc Metastore in **Dataproc metastore url** .
          - `  BIGLAKE_METASTORE  ` : Select this option to store your metadata in BigLake metastore. You must provide a BigQuery dataset in **BigQuery dataset** .
          - `  BIGLAKE_REST_CATALOG  ` : Select this option to store your metadata in the BigLake metastore Iceberg REST catalog.
    
    5.  For **Destination gcs path** , enter a path to a Cloud Storage bucket to store your migrated data.
    
    6.  Optional: For **Service account** , enter a service account to use with this data transfer. The service account should belong to the same Google Cloud project where the transfer configuration and destination dataset is created.
    
    7.  Optional: You can enable **Use translation output** to set up a unique Cloud Storage path and database for each table being migrated. To do this, provide the path to the Cloud Storage folder containing the translation results in the **BQMS translation output gcs path** field. For more information, see [Configure Translation output](#configure-translation-output) . This field is only available if **Transfer strategy** is set to `  FULL_TRANSFER  ` .
        
          - If you specify a Translation output Cloud Storage path, the destination Cloud Storage path and BigQuery dataset will be sourced from the files in that path.
    
    8.  For **Storage type** , select one of the following options. This field is only available if **Transfer strategy** is set to `  FULL_TRANSFER  ` :
        
          - `  HDFS  ` : Select this option if your file storage is `  HDFS  ` . In the **STS agent pool name** field, you must provide the name of the agent pool that you created when you [configured your Storage Transfer Agent](#configure-storage-transfer-agent-hdfs) .
          - `  S3  ` : Select this option if your file storage is `  Amazon S3  ` . In the **Access key ID** and **Secret access key** fields, you must provide the access key ID and secret access key that you created when you [set up your access credentials](#configure-storage-transfer-permission-s3) .
          - `  AZURE  ` : Select this option if your file storage is `  Azure Blob Storage  ` . In the **SAS token** field, you must provide the SAS token that you created when you [set up your access credentials](#configure-storage-transfer-permission-azure) .

### bq

To schedule Hive managed tables transfer, enter the `  bq mk  ` command and supply the transfer creation flag `  --transfer_config  ` :

``` text
  bq mk --transfer_config
  --data_source=hadoop
  --display_name='TRANSFER_NAME'
  --service_account_name='SERVICE_ACCOUNT'
  --project_id='PROJECT_ID'
  --location='REGION'
  --params='{
    "transfer_strategy":"TRANSFER_STRATEGY",
    "table_name_patterns":"LIST_OF_TABLES",
    "table_metadata_path":"gs://DUMPER_BUCKET/hive-dumper-output.zip",
    "target_gcs_file_path":"gs://MIGRATION_BUCKET",
    "metastore":"METASTORE",
    "destination_dataproc_metastore":"DATAPROC_METASTORE_URL",
    "destination_bigquery_dataset":"BIGLAKE_METASTORE_DATASET",
    "translation_output_gcs_path":"gs://TRANSLATION_OUTPUT_BUCKET/metadata/config/default_database/",
    "storage_type":"STORAGE_TYPE",
    "agent_pool_name":"AGENT_POOL_NAME",
    "aws_access_key_id":"AWS_ACCESS_KEY_ID",
    "aws_secret_access_key":"AWS_SECRET_ACCESS_KEY",
    "azure_sas_token":"AZURE_SAS_TOKEN"
    }'
```

Replace the following:

  - `  TRANSFER_NAME  ` : the display name for the transfer configuration. The transfer name can be any value that lets you identify the transfer if you need to modify it later.
  - `  SERVICE_ACCOUNT  ` : the service account name used to authenticate your transfer. The service account should be owned by the same `  project_id  ` used to create the transfer and it should have all of the required permissions.
  - `  PROJECT_ID  ` : your Google Cloud project ID. If `  --project_id  ` isn't supplied to specify a particular project, the default project is used.
  - `  REGION  ` : location of this transfer configuration.
  - `  TRANSFER_STRATEGY  ` : (Optional) Specify one of the following values:
      - `  FULL_TRANSFER  ` : Transfer all data and register metadata with the target metastore. This is the default value.
      - `  METADATA_ONLY  ` : Register metadata only. You must have data already present in the correct Cloud Storage location referenced in the metadata.
  - `  LIST_OF_TABLES  ` : a list of entities to be transferred. Use a hierarchical naming spec - `  database . table  ` . This field supports RE2 regular expression to specify tables. For example:
      - `  db1..*  ` : specifies all tables in the database
      - `  db1.table1;db2.table2  ` : a list of tables
  - `  DUMPER_BUCKET  ` : the Cloud Storage bucket containing the `  hive-dumper-output.zip  ` file.
  - `  MIGRATION_BUCKET  ` : Destination GCS path to which all underlying files will be loaded. Available only if `  transfer_strategy  ` is `  FULL_TRANSFER  ` .
  - `  METASTORE  ` : The type of metastore to migrate to. Set this to one of the following values:
      - `  DATAPROC_METASTORE  ` : To transfer metadata to Dataproc Metastore.
      - `  BIGLAKE_METASTORE  ` : To transfer metadata to BigLake metastore.
      - `  BIGLAKE_REST_CATALOG  ` : To transfer metadata to BigLake metastore Iceberg REST Catalog.
  - `  DATAPROC_METASTORE_URL  ` : The URL of your Dataproc Metastore. Required if `  metastore  ` is `  DATAPROC_METASTORE  ` .
  - `  BIGLAKE_METASTORE_DATASET  ` : The BigQuery dataset for your BigLake metastore. Required if `  metastore  ` is `  BIGLAKE_METASTORE  ` and `  transfer_strategy  ` is `  FULL_TRANSFER  ` .
  - `  TRANSLATION_OUTPUT_BUCKET  ` : (Optional) Specify a Cloud Storage bucket for the translation output. For more information, see [Using Translation output](/bigquery/docs/hadoop-transfer#configure-translation-output) . Available only if `  transfer_strategy  ` is `  FULL_TRANSFER  ` .
  - `  STORAGE_TYPE  ` : Specify the underlying file storage for your tables. Supported types are `  HDFS  ` , `  S3  ` , and `  AZURE  ` . Required if `  transfer_strategy  ` is `  FULL_TRANSFER  ` .
  - `  AGENT_POOL_NAME  ` : the name of the agent pool used for creating agents. Required if `  storage_type  ` is `  HDFS  ` .
  - `  AWS_ACCESS_KEY_ID  ` : the access key ID from [access credentials](#configure-storage-transfer-permission-s3) . Required if `  storage_type  ` is `  S3  ` .
  - `  AWS_SECRET_ACCESS_KEY  ` : the secret access key from [access credentials](#configure-storage-transfer-permission-s3) . Required if `  storage_type  ` is `  S3  ` .
  - `  AZURE_SAS_TOKEN  ` : the SAS token from [access credentials](#configure-storage-transfer-permission-azure) . Required if `  storage_type  ` is `  AZURE  ` .

Run this command to create the transfer configuration and start the Hive managed tables transfer. Transfers are scheduled to run every 24 hours by default, but can be configured with [transfer scheduling options](#transfer_scheduling_options) .

When the transfer is complete, your tables in Hadoop cluster will be migrated to `  MIGRATION_BUCKET  ` .

## Data ingestion options

The following sections provide more information about how you can configure your Hive managed tables transfers.

### Incremental transfers

When a transfer configuration is set up with a recurring schedule, every subsequent transfer updates the table on Google Cloud with the latest updates made to the source table. For example, all insert, delete, or update operations with schema changes are reflected in Google Cloud with each transfer.

### Transfer scheduling options

By default, transfers are scheduled to run every 24 hours by default. To configure how often transfers are run, add the `  --schedule  ` flag to the transfer configuration, and specify a transfer schedule using [the `  schedule  ` syntax](/appengine/docs/flexible/scheduling-jobs-with-cron-yaml#formatting_the_schedule) . Hive managed tables transfers must have a minimum of 24 hours between transfer runs.

For one-time transfers, you can add the `  end_time  ` flag to the transfer configuration to only run the transfer once.

### Configure Translation output

You can configure a unique Cloud Storage path and database for each migrated table. To do so, perform the following steps to generate a tables mapping YAML file that you can use in your transfer configuration.

1.  Create a configuration YAML file (suffixed with `  config.yaml  ` ) in the `  DUMPER_BUCKET  ` that contains the following:
    
    ``` text
        type: object_rewriter
        relation:
        - match:
            relationRegex: ".*"
          external:
            location_expression: "'gs://MIGRATION_BUCKET/' + table.schema + '/' + table.name"
    ```
    
      - Replace `  MIGRATION_BUCKET  ` with the name of the Cloud Storage bucket that is the destination for your migrated table files. The `  location_expression  ` field is a [common expression language (CEL)](https://github.com/google/cel-spec?tab=readme-ov-file#common-expression-language) expression.

2.  Create another configuration YAML file (suffixed with `  config.yaml  ` ) in the `  DUMPER_BUCKET  ` that contains the following:
    
    ``` text
        type: experimental_object_rewriter
        relation:
          - match:
              schema: SOURCE_DATABASE
            outputName:
              database: null
              schema: TARGET_DATABASE
    ```
    
      - Replace `  SOURCE_DATABASE  ` and `  TARGET_DATABASE  ` with the name of source database name and Dataproc Metastore database or BigQuery dataset depending on the chosen metastore. Ensure that the BigQuery dataset exists if you are configuring the database for BigLake metastore.
    
    For more information about these configuration YAML, see [Guidelines to create a configuration YAML file](/bigquery/docs/config-yaml-translation#yaml_guidelines) .

3.  Generate tables mapping YAML file using the following command:
    
    ``` text
    curl -d '{
      "tasks": {
          "string": {
            "type": "HiveQL2BigQuery_Translation",
            "translation_details": {
                "target_base_uri": "TRANSLATION_OUTPUT_BUCKET",
                "source_target_mapping": {
                  "source_spec": {
                      "base_uri": "DUMPER_BUCKET"
                  }
                },
                "target_types": ["metadata"]
            }
          }
      }
      }' \
      -H "Content-Type:application/json" \
      -H "Authorization: Bearer TOKEN" -X POST https://bigquerymigration.googleapis.com/v2alpha/projects/PROJECT_ID/locations/LOCATION/workflows
    ```
    
    Replace the following:
    
      - `  TRANSLATION_OUTPUT_BUCKET  ` : (Optional) Specify a Cloud Storage bucket for the translation output. For more information, see [Using Translation output](/bigquery/docs/hadoop-transfer#metadata_migration) .
      - `  DUMPER_BUCKET  ` : the base URI for Cloud Storage bucket that contains the `  hive-dumper-output.zip  ` and configuration YAML file.
      - `  TOKEN  ` : the OAuth token. You can generate this in the command line with the command `  gcloud auth print-access-token  ` .
      - `  PROJECT_ID  ` : the project to process the translation.
      - `  LOCATION  ` : the location where the job is processed. For example, `  eu  ` or `  us  ` .

4.  [Monitor the status of this job](/bigquery/docs/api-sql-translator#explore_the_translation_output) . When completed, a mapping file is generated for each table in database within a predefined path in `  TRANSLATION_OUTPUT_BUCKET  ` .

### Orchestrate dumper execution by using the `     cron    ` command

You can automate incremental transfers by using a [`  cron  `](https://man7.org/linux/man-pages/man8/cron.8.html) job to execute the `  dwh-migration-dumper  ` tool. By automating metadata extraction, you ensure that an up-to-date dump from Hadoop is available for subsequent incremental transfer runs.

#### Before you begin

Before using this automation script, complete the [dumper installation prerequisites](/bigquery/docs/generate-metadata#prerequisites) . To run the script, you must have the dwh-migration-dumper tool installed and the necessary IAM permissions configured.

#### Scheduling the automation

1.  Save the following script to a local file. This script is designed to be configured and executed by a `  cron  ` daemon to automate the extraction and upload process of dumper output:
    
    ``` text
    #!/bin/bash
    
    # Exit immediately if a command exits with a non-zero status.
    set -e
    # Treat unset variables as an error when substituting.
    set -u
    # Pipelines return the exit status of the last command to exit with a non-zero status.
    set -o pipefail
    
    # These values are used if not overridden by command-line options.
    DUMPER_EXECUTABLE="DUMPER_PATH/dwh-migration-dumper"
    GCS_BASE_PATH="gs://PATH_TO_DUMPER_OUTPUT"
    LOCAL_BASE_DIR="LOCAL_BASE_DIRECTORY_PATH"
    
    # Function to display usage information
    usage() {
      echo "Usage: $0 [options]"
      echo ""
      echo "Runs the dwh-migration-dumper tool and uploads its output to provided GCS path."
      echo ""
      echo "Options:"
      echo "  --dumper-executable   The full path to the dumper executable. (Required)"
      echo "  --gcs-base-path       The base GCS path for output files. (Required)"
      echo "  --local-base-dir      The local base directory for logs and temp files. (Required)"
      echo "  -h, --help                  Display this help message and exit."
      exit 1
    }
    
    # This loop processes command-line options and overrides the default configuration.
    while [[ "$#" -gt 0 ]]; do
      case $1 in
          --dumper-executable)
              DUMPER_EXECUTABLE="$2"
              shift # past argument
              shift # past value
              ;;
          --gcs-base-path)
              GCS_BASE_PATH="$2"
              shift
              shift
              ;;
          --local-base-dir)
              LOCAL_BASE_DIR="$2"
              shift
              shift
              ;;
          -h|--help)
              usage
              ;;
          *)
              echo "Unknown option: $1"
              usage
              ;;
      esac
    done
    
    # This runs AFTER parsing arguments to ensure no placeholder values are left.
    if [[ "$DUMPER_EXECUTABLE" == "DUMPER_PATH"* || "$GCS_BASE_PATH" == "gs://PATH_TO_DUMPER_OUTPUT" || "$LOCAL_BASE_DIR" == "LOCAL_BASE_DIRECTORY_PATH" ]]; then
      echo "ERROR: One or more configuration variables have not been set. Please provide them as command-line arguments or edit the script." >&2
      echo "Run with --help for more information." >&2
      exit 1
    fi
    
    # Create unique timestamp and directories for this run
    EPOCH=$(date +%s)
    LOCAL_LOG_DIR="${LOCAL_BASE_DIR}/logs"
    mkdir -p "${LOCAL_LOG_DIR}" # Ensures the base and logs directories exist
    
    # Define the unique log and zip file path for this run
    LOG_FILE="${LOCAL_LOG_DIR}/dumper_execution_${EPOCH}.log"
    ZIP_FILE_NAME="dts-cron-dumper-output_${EPOCH}.zip"
    LOCAL_ZIP_PATH="${LOCAL_BASE_DIR}/${ZIP_FILE_NAME}"
    
    echo "Script execution started. All subsequent output will be logged to: ${LOG_FILE}"
    
    # --- Helper Functions ---
    
    log() { echo "$(date '+%Y-%m-%d %H:%M:%S') - $@" >> "${LOG_FILE}"; }
    
    cleanup() {
      local path_to_remove="$1"
      log "Cleaning up local file/directory: ${path_to_remove}..."
      rm -rf "${path_to_remove}"
    }
    
    # This function is called when the script exits to ensure cleanup and logging happen reliably.
    handle_exit() {
      local exit_code=$?
      # Only run the failure logic if the script is exiting with an error
      if [[ ${exit_code} -ne 0 ]]; then
          log "ERROR: Script is exiting with a failure code (${exit_code})."
          local gcs_log_path_on_failure="${GCS_BASE_PATH}/logs/$(basename "${LOG_FILE}")"
          log "Uploading log file to ${gcs_log_path_on_failure} for debugging..."
          # Attempt to upload the log file on failure, but don't let this command cause the script to exit.
          gsutil cp "${LOG_FILE}" "${gcs_log_path_on_failure}" > /dev/null 2>&1 || log "WARNING: Failed to upload log file to GCS."
    
      else
          # SUCCESS PATH
          log "Script finished successfully. Now cleaning up local zip file...."
          # Clean up the local zip file ONLY on success
          cleanup "${LOCAL_ZIP_PATH}"
      fi
    
      log "*****Script End*****"
      exit ${exit_code}
    }
    
    # Trap the EXIT signal to run the handle_exit function, ensuring cleanup always happens.
    trap handle_exit EXIT
    
    # Validates the dumper log file based on a strict set of rules.
    validate_dumper_output() {
      local log_file_to_check="$1"
    
      # Check for the specific success message from the dumper tool.
      if grep -q "Dumper execution: SUCCEEDED" "${log_file_to_check}"; then
          log "Validation Successful: Found 'Dumper execution: SUCCEEDED' message."
          return 0 # Success
      else
          log "ERROR: Validation failed. The 'Dumper execution: SUCCEEDED' message was not found."
          return 1 # Failure
      fi
    }
    
    # --- Main Script Logic ---
    
    log "*****Script Start*****"
    log "Dumper Executable: ${DUMPER_EXECUTABLE}"
    log "GCS Base Path: ${GCS_BASE_PATH}"
    log "Local Base Directory: ${LOCAL_BASE_DIR}"
    
    # Use an array to build the command safely
    dumper_command_args=(
      "--connector" "hiveql"
      "--output" "${LOCAL_ZIP_PATH}"
    )
    
    log "Starting dumper tool execution..."
    log "COMMAND: ${DUMPER_EXECUTABLE} ${dumper_command_args[*]}"
    
    "${DUMPER_EXECUTABLE}" "${dumper_command_args[@]}" >> "${LOG_FILE}" 2>&1
    
    log "Dumper process finished."
    
    # Validate the output from the dumper execution for success or failure.
    validate_dumper_output "${LOG_FILE}"
    
    # Upload the ZIP file to GCS
    gcs_zip_path="${GCS_BASE_PATH}/${ZIP_FILE_NAME}"
    log "Uploading ${LOCAL_ZIP_PATH} to ${gcs_zip_path}..."
    
    if [ ! -f "${LOCAL_ZIP_PATH}" ]; then
      log "ERROR: Expected ZIP file ${LOCAL_ZIP_PATH} not found after dumper execution."
      # The script will exit here with an error code, and the trap will run.
      exit 1
    fi
    
    gsutil cp "${LOCAL_ZIP_PATH}" "${gcs_zip_path}" >> "${LOG_FILE}" 2>&1
    log "Upload to GCS successful."
    
    # The script will now exit with code 0. The trap will call cleanup and log the script end.
    ```

2.  Run the following command to make the script executable:
    
    ``` text
    chmod +x PATH_TO_SCRIPT
    ```

3.  Schedule the script using `  crontab  ` , replacing the variables with appropriate values for your job. Add an entry to schedule the job. The following example runs the script every day at 2:30 AM:
    
    ``` text
    # Run the Hive dumper daily at 2:30 AM for incremental BigQuery transfer.
    30 2 * * * PATH_TO_SCRIPT \
      --dumper-executable PATH_TO_DUMPER_EXECUTABLE \
      --gcs-base-path GCS_PATH_TO_UPLOAD_DUMPER_OUTPUT \
      --local-base-dir LOCAL_PATH_TO_SAVE_INTERMEDIARY_FILES
    ```

4.  When creating the transfer, ensure the `  table_metadata_path  ` field is set to the same Cloud Storage path you configured for `  GCS_PATH_TO_UPLOAD_DUMPER_OUTPUT  ` . This is the path containing the dumper output ZIP files.

#### Scheduling Considerations

To avoid data staleness, the metadata dump must be ready before your scheduled transfer begins. Configure the `  cron  ` job frequency accordingly.

We recommend performing a few trial runs of the script manually to determine the average time it takes for the dumper tool to generate its output. Use this timing to set a `  cron  ` schedule that safely precedes your DTS transfer run and ensures freshness.

**Note:** This orchestration is not compatible with translation output. If translation output is enabled, you must run the dumper tool manually.

## Monitor Hive managed tables transfers

After you schedule Hive managed tables transfer, you can monitor the transfer job with bq command-line tool commands. For information about monitoring your transfer jobs, see [View your transfers](/bigquery/docs/working-with-transfers#view_your_transfers) .

### Track table migration status

You can also run the `  dwh-dts-status  ` tool to monitor the status of all transferred tables within a transfer configuration or a particular database. You can also use the `  dwh-dts-status  ` tool to list all transfer configurations in a project.

#### Before you begin

Before you can use the `  dwh-dts-status  ` tool, do the following:

1.  Get the `  dwh-dts-status  ` tool by downloading the `  dwh-migration-tool  ` package from the [`  dwh-migration-tools  ` GitHub repository](https://github.com/google/dwh-migration-tools/releases) .

2.  Authenticate your account to Google Cloud with the following command:
    
    ``` text
    gcloud auth application-default login
    ```
    
    For more information, see [How Application Default Credentials work](/docs/authentication/application-default-credentials) .

3.  Verify that the user has the `  bigquery.admin  ` and `  logging.viewer  ` role. For more information about IAM roles, see [Access control reference](/bigquery/docs/access-control) .

#### List all transfer configurations in a project

To list all transfer configurations in a project, use the following command:

``` text
  ./dwh-dts-status --list-transfer-configs --project-id=[PROJECT_ID] --location=[LOCATION]
```

Replace the following:

  - `  PROJECT_ID  ` : the Google Cloud project ID that is running the transfers.
  - `  LOCATION  ` : the location where the transfer configuration was created.

This command outputs a table with a list of transfer configuration names and IDs.

#### View statuses of all tables in a configuration

To view the status of all tables included in a transfer configuration, use the following command:

``` text
  ./dwh-dts-status --list-status-for-config --project-id=[PROJECT_ID] --config-id=[CONFIG_ID] --location=[LOCATION]
```

Replace the following:

  - `  PROJECT_ID  ` : the Google Cloud project ID that is running the transfers.
  - `  LOCATION  ` : the location where the transfer configuration was created.
  - `  CONFIG_ID  ` : the ID of the specified transfer configuration.

This command outputs a table with a list of tables, and their transfer status, in the specified transfer configuration. The transfer status can be one of the following values: `  PENDING  ` , `  RUNNING  ` , `  SUCCEEDED  ` , `  FAILED  ` , `  CANCELLED  ` .

#### View statuses of all tables in a database

To view the status of all tables transferred from a specific database, use the following command:

``` text
  ./dwh-dts-status --list-status-for-database --project-id=[PROJECT_ID] --database=[DATABASE]
```

Replace the following:

  - `  PROJECT_ID  ` : the Google Cloud project ID that is running the transfers.
  - `  DATABASE  ` :the name of the specified database.

This command outputs a table with a list of tables, and their transfer status, in the specified database. The transfer status can be one of the following values: `  PENDING  ` , `  RUNNING  ` , `  SUCCEEDED  ` , `  FAILED  ` , `  CANCELLED  ` .
