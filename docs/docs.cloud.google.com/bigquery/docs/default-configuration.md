# Manage configuration settings

BigQuery administrators and project owners can manage configuration settings at the organization and project levels. You can set configurations to enforce security, control costs, and optimize query performance across your entire data infrastructure. By setting default values, you can ensure consistent compliance and operational efficiency, making it easier to manage your BigQuery environment.

## Specify configuration settings

The following sections describe how to specify default configuration settings. Default settings are configured at an organization or project level but can be overridden at the session or job level. To enforce default behavior, you can configure default settings in combination with related [organizational policies](/resource-manager/docs/organization-policy/overview) .

### Required roles

To get the permission that you need to specify a configuration setting, ask your administrator to grant you the [BigQuery Admin](/iam/docs/roles-permissions/bigquery#bigquery.admin) ( `  roles/bigquery.admin  ` ) IAM role. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

This predefined role contains the `  bigquery.config.update  ` permission, which is required to specify a configuration setting.

You might also be able to get this permission with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

For more information on IAM roles and permissions in BigQuery, see [Predefined roles and permissions](/bigquery/access-control) .

### Configure organization settings

You can configure settings at the organization level by using the following GoogleSQL statements. When you specify the configuration, you must specify the region where it applies. You can only use one region for each statement.

To configure organization settings, use the [`  ALTER ORGANIZATION SET OPTIONS  ` DDL statement](/bigquery/docs/reference/standard-sql/data-definition-language#alter_organization_set_options_statement) . The following example specifies several default configurations, including the following:

  - Time zone: `  America/Chicago  `
  - Cloud KMS key: a user-defined key
  - Query timeout: 30 minutes (1800000 milliseconds)
  - Interactive query queue timeout: 10 minutes (600000 milliseconds)
  - Batch query queue timeout: 20 minutes (1200000 milliseconds)

<!-- end list -->

``` text
ALTER ORGANIZATION
SET OPTIONS (
  `region-REGION.default_time_zone`= 'America/Chicago',
  -- Ensure all service accounts under the organization have permission to KMS_KEY
  `region-REGION.default_kms_key_name` = KMS_KEY,
  `region-REGION.default_query_job_timeout_ms` = 1800000,
  `region-REGION.default_interactive_query_queue_timeout_ms` = 600000,
  `region-REGION.default_batch_query_queue_timeout_ms` = 1200000,
  `region-REGION.default_storage_billing_model`= BILLING_MODEL,
  `region-REGION.default_max_time_travel_hours` = 72);
```

Replace the following:

  - `  REGION  ` : the [region](/bigquery/docs/locations#regions) associated with your project or organization—for example, `  us  ` or `  europe-west6  ` .
  - `  KMS_KEY  ` : a user-defined Cloud KMS key. For more information, see [Customer-managed Cloud KMS keys](/bigquery/docs/customer-managed-encryption) .
  - `  BILLING_MODEL  ` : the storage model for new datasets—for example, `  PHYSICAL  ` for physical bytes.

The following example clears all organization-level default settings:

``` text
ALTER ORGANIZATION
SET OPTIONS (
  `region-REGION.default_time_zone` = NULL,
  `region-REGION.default_kms_key_name` = NULL,
  `region-REGION.default_query_job_timeout_ms` = NULL,
  `region-REGION.default_interactive_query_queue_timeout_ms` = NULL,
  `region-REGION.default_batch_query_queue_timeout_ms` = NULL,
  `region-REGION.default_storage_billing_model`= NULL,
  `region-REGION.default_max_time_travel_hours` = NULL,
  `region-REGION.default_cloud_resource_connection_id` = NULL,
  `region-REGION.default_sql_dialect_option` = NULL,
  `region-REGION.enable_reservation_based_fairness` = NULL,
  `region-REGION.enable_global_queries_execution` = NULL,
  `region-REGION.enable_global_queries_data_access` = NULL);
```

### Configure project settings

You can configure settings at the project level by using the following GoogleSQL statements. When you specify the configuration, you must specify the region where it applies. You can only use one region for each statement.

To configure project settings, use the [`  ALTER PROJECT SET OPTIONS  ` DDL statement](/bigquery/docs/reference/standard-sql/data-definition-language#alter_project_set_options_statement) . The `  ALTER PROJECT SET OPTIONS  ` DDL statement optionally accepts the `  PROJECT_ID  ` variable. If the `  PROJECT_ID  ` is not specified, it defaults to the current project where the query runs. The following example specifies several default configurations:

  - Time zone: `  America/Los_Angeles  `
  - Cloud KMS key: an example key
  - Query timeout: 1 hour
  - Interactive query queue timeout: 10 minutes
  - Batch query queue timeout: 20 minutes
  - Reservation-based fairness: enabled
  - Global queries: enabled for running and for accessing data

<!-- end list -->

``` text
ALTER PROJECT PROJECT_ID
SET OPTIONS (
  `region-REGION.default_time_zone` = 'America/Los_Angeles',
  -- Ensure all service accounts under the project have permission to KMS_KEY
  `region-REGION.default_kms_key_name` = KMS_KEY,
  `region-REGION.default_query_job_timeout_ms` = 3600000,
  `region-REGION.default_interactive_query_queue_timeout_ms` = 600000,
  `region-REGION.default_batch_query_queue_timeout_ms` = 1200000,
  `region-REGION.default_storage_billing_model`= BILLING_MODEL,
  `region-REGION.default_max_time_travel_hours` = 72,
  `region-REGION.default_cloud_resource_connection_id` = CONNECTION_ID,
  `region-REGION.default_sql_dialect_option` = 'default_google_sql',
  `region-REGION.enable_reservation_based_fairness` = true,
  `region-REGION.enable_global_queries_execution` = true,
  `region-REGION.enable_global_queries_data_access` = true);
```

Replace the following:

  - `  PROJECT_ID  ` : the ID of the project.
  - `  REGION  ` : the [region](/bigquery/docs/locations#regions) associated with your project or organization—for example, `  us  ` or `  europe-west6  ` .
  - `  KMS_KEY  ` : a user-defined Cloud KMS key. For more information, see [Customer-managed Cloud KMS keys](/bigquery/docs/customer-managed-encryption) .
  - `  BILLING_MODEL  ` : the storage model for new datasets—for example, `  PHYSICAL  ` for physical bytes.
  - `  CONNECTION_ID  ` : the ID of the connection to use as the default connection for tables and models.

The following example clears all project-level default settings. The default settings use any organization-level default settings, if they exist. Otherwise, all default settings are set to the global default.

``` text
ALTER PROJECT PROJECT_ID
SET OPTIONS (
  `region-REGION.default_time_zone` = NULL,
  `region-REGION.default_kms_key_name` = NULL,
  `region-REGION.default_query_job_timeout_ms` = NULL,
  `region-REGION.default_interactive_query_queue_timeout_ms` = NULL,
  `region-REGION.default_batch_query_queue_timeout_ms` = NULL,
  `region-REGION.default_storage_billing_model`= NULL,
  `region-REGION.default_max_time_travel_hours` = NULL,
  `region-REGION.default_cloud_resource_connection_id` = NULL,
  `region-REGION.default_sql_dialect_option` = NULL,
  `region-REGION.enable_reservation_based_fairness` = NULL,
  `region-REGION.enable_global_queries_execution` = NULL,
  `region-REGION.enable_global_queries_data_access` = NULL);
```

Project-level configurations override organization-level configurations. Project-level configurations can in turn be overridden by [session-level configurations](/bigquery/docs/sessions-write-queries) , which can be overridden by [job-level configurations](/bigquery/docs/running-queries) .

## Retrieve configuration settings

You can view the configuration settings for an organization or project by using the following [`  INFORMATION_SCHEMA  `](/bigquery/docs/information-schema-intro) views:

  - [`  INFORMATION_SCHEMA.PROJECT_OPTIONS  `](/bigquery/docs/information-schema-project-options) : the configurations applied to a project.
  - [`  INFORMATION_SCHEMA.EFFECTIVE_PROJECT_OPTIONS  `](/bigquery/docs/information-schema-effective-project-options) : the effective configurations applied to a project. Effective configurations include all configurations set at the project level as well as all settings inherited by the project from an organization.
  - [`  INFORMATION_SCHEMA.ORGANIZATION_OPTIONS  `](/bigquery/docs/information-schema-organization-options) : the configurations applied to an organization.

It may take a few minutes for new configurations to become effective and reflected within the `  INFORMATION_SCHEMA  ` view.

### Required roles

To get the permission that you need to retrieve configuration settings, ask your administrator to grant you the [BigQuery Job User](/iam/docs/roles-permissions/bigquery#bigquery.jobUser) ( `  roles/bigquery.jobUser  ` ) IAM role on the specified project. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

This predefined role contains the `  bigquery.config.get  ` permission, which is required to retrieve configuration settings.

You might also be able to get this permission with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

For more information on IAM roles and permissions in BigQuery, see [Predefined roles and permissions](/bigquery/access-control) .

### Examples

To view the configurations under an organization in the `  us  ` region, run the following query:

``` text
SELECT * FROM region-us.INFORMATION_SCHEMA.ORGANIZATION_OPTIONS;
```

To view the effective configurations under your default project in the `  us  ` region, run the following query:

``` text
SELECT * FROM region-us.INFORMATION_SCHEMA.EFFECTIVE_PROJECT_OPTIONS;
```

To view the configurations under your default project in the `  us  ` region, run the following query:

``` text
SELECT * FROM region-us.INFORMATION_SCHEMA.PROJECT_OPTIONS;
```

## Configuration settings

The following sections describe the configuration settings that you can specify.

### Query and job execution settings

Use the following settings to control how queries are executed, timed, and queued.

  - `  default_batch_query_queue_timeout_ms  ` : The default amount of time, in milliseconds, that a batch query is [queued](/bigquery/docs/query-queues) . If unset, the default is 24 hours. The minimum value is 1 millisecond. The maximum value is 48 hours. To turn off batch query queueing, set the value to `  -1  ` .

  - `  default_interactive_query_queue_timeout_ms  ` : The default amount of time, in milliseconds, that an interactive query is [queued](/bigquery/docs/query-queues) . If unset, the default is six hours. The minimum value is 1 millisecond. The maximum value is 48 hours. To turn off interactive query queueing, set the value to `  -1  ` .

  - `  default_query_job_timeout_ms  ` : The default time after which a query job times out, including the time the job is queued and the time spent running. The timeout period must be between 5 minutes and 48 hours. This timeout only applies to individual query jobs and the child jobs of scripts. To set a timeout for script jobs, you should use the [jobs.insert](/bigquery/docs/reference/rest/v2/jobs/insert) API method and set the `  jobTimeoutMs  ` field.
    
    **Note:** The `  default_query_job_timeout_ms  ` setting also applies to [continuous query](/bigquery/docs/continuous-queries-introduction) jobs. To override this project-level setting for an individual continuous query, assign a [job timeout](/bigquery/docs/continuous-queries#run_a_continuous_query_by_using_a_service_account) to the continuous query in question. Continuous queries still adhere to [maximum runtimes](/bigquery/docs/continuous-queries-introduction#authorization) .

  - `  enable_reservation_based_fairness  ` : The option that determines how idle slots are shared. The default value is false, which means idle slots are equally distributed across all query projects. If enabled, the idle slots are shared equally across all reservations first, and then across projects within the reservation. For more information, see [reservation-based fairness](/bigquery/docs/slots#fairness) . This option is only supported at the project level. You can't specify it at the organization or job level.

  - `  default_time_zone  ` : The default time zone to use in time zone-dependent GoogleSQL functions, when a time zone is not specified as an argument. This configuration does not apply to [time-unit column partitioned tables](/bigquery/docs/partitioned-tables#date_timestamp_partitioned_tables) (which use UTC as the time zone), the [Storage Transfer Service schedule transfers](/storage-transfer/docs/schedule-transfer-jobs) , or [loading data with the bq command-line tool](/bigquery/docs/bq-command-line-tool#loading_data) . For more information, see [time zones](/bigquery/docs/reference/standard-sql/data-types#time_zones) .
    
    **Note:** If you want to set a default time zone, ensure any existing queries that use `  DATETIME  ` literals aren't affected. This includes queries with the explicit `  DATETIME  ` keyword, implicitly converted string literals passed as a parameter to time functions like `  DATETIME_DIFF('2022-10-01', ...)  ` , the `  PARSE_DATETIME()  ` function, and more. For this reason, it is safer to only set the `  default_time_zone  ` parameter on new projects.

  - `  default_query_optimizer_options  ` : The history-based query optimizations. This option can be one of the following:
    
      - `  'adaptive=on'  ` : Use history-based query optimizations.
      - `  'adaptive=off'  ` : Don't use history-based query optimizations.
      - `  NULL  ` (default): Use the default history-based query optimizations setting, which is equivalent to `  'adaptive=on'  ` .

  - `  default_sql_dialect_option  ` : The default SQL query dialect for executing query jobs using the bq command-line tool or BigQuery API. Changing this setting doesn't affect the default dialect in the console. This option can be one of the following:
    
      - `  'default_legacy_sql'  ` (default): Use legacy SQL if the query dialect isn't specified at the job level.
      - `  'default_google_sql'  ` : Use GoogleSQL if the query dialect isn't specified at the job level.
      - `  'only_google_sql'  ` : Use GoogleSQL if the query dialect isn't specified at the job level. Reject jobs with query dialect set to legacy SQL.
      - `  NULL  ` : Use the default query dialect setting, which is equivalent to `  'default_legacy_sql'  ` .

  - `  enable_global_queries_execution  ` : The option that determines if [global queries](/bigquery/docs/global-queries) can be run. The default value is `  FALSE  ` , which means that global queries are not enabled.

  - `  enable_global_queries_data_access  ` : The option that determines if [global queries](/bigquery/docs/global-queries) can access data stored in the region. The default value is `  FALSE  ` , which means that global queries can't copy data from this region regardless of the project in which they run.

### Data management settings

Use the following settings to define rules for data creation, security, and lifecycle.

  - `  default_column_name_character_map  ` : The default scope and handling of characters in column names. If unset, load jobs that use unsupported characters in column names fail with an error message. Some older tables might be set to replace unsupported characters in column names. For more information, see [`  load_option_list  `](/bigquery/docs/reference/standard-sql/load-statements#load_option_list) .

  - `  default_kms_key_name  ` : The default Cloud Key Management Service key for encrypting table data, including temporary or anonymous tables. For more information, see [Customer-managed Cloud KMS keys](/bigquery/docs/customer-managed-encryption) .
    
    **Note:** to set a default Cloud KMS key, you must grant the Encrypter/Decrypter role to all BigQuery service accounts that are used within the project or organization. If a service account within the project or organization doesn't have appropriate permissions, all queries run by the service account fail. For information about assigning the Encrypter/Decrypter role, see [Assign the Encrypter/Decrypter role](/bigquery/docs/customer-managed-encryption#assign_role) . If you set a default Cloud KMS key without first assigning the appropriate roles, you can clear the default key by setting the value to `  NULL  ` . For examples, see [Configure organization settings](#configure-organization-settings) and [Configure project settings](#configure-project-settings) .

  - `  default_max_time_travel_hours  ` : The default time travel window in hours for new datasets. This duration must be within the range of 48 to 168, inclusive, and must be divisible by 24. Changing the default max time travel hours does not affect existing datasets. For more information, see [Time Travel and data retention](/bigquery/docs/time-travel#time_travel) .

### Cost and resource settings

Use the following settings to determine how resources are billed and connected.

  - `  default_storage_billing_model  ` : The default storage billing model for new datasets. Set the value to `  PHYSICAL  ` to use physical bytes when calculating storage charges or to `  LOGICAL  ` to use logical bytes. Note that changing the default storage billing model does not affect existing datasets. For more information, see [Storage billing models](/bigquery/docs/datasets-intro#dataset_storage_billing_models) .
  - `  default_cloud_resource_connection_id  ` : The default connection to use when creating tables and models. Only specify the connection's ID or name, and exclude the attached project ID and region prefixes. Using default connections can cause the permissions granted to the connection's service account to be updated, depending on the type of table or model you're creating. For more information, see the [Default connection overview](/bigquery/docs/default-connections) .

## Pricing

There is no additional charge to use the BigQuery configuration service. For more information, see [Pricing](https://cloud.google.com/bigquery/pricing) .
