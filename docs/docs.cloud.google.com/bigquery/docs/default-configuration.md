---
name: documents/docs.cloud.google.com/bigquery/docs/default-configuration
uri: https://docs.cloud.google.com/bigquery/docs/default-configuration
title: Manage default configuration settings
description: Learn how to specify, remove, and retrieve default configuration settings at the organization and project levels in BigQuery.
data_source: docs.cloud.google.com
---

# Manage default configuration settings

Default configuration settings in BigQuery can help your organization enforce security, control costs, and optimize query performance. As a BigQuery administrator or project owner, you can specify, remove, and retrieve these defaults at the organization and project levels, or override them for individual sessions and jobs.

## Required roles

To get the permissions that you need to specify or retrieve configuration settings, ask your administrator to grant you the following IAM roles:

- Specify configuration settings: [BigQuery Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin) ( `roles/bigquery.admin` ) on your organization or project
- Retrieve configuration settings: [BigQuery Job User](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.jobUser) ( `roles/bigquery.jobUser` ) on the specified project

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

These predefined roles contain the permissions required to specify or retrieve configuration settings. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to specify or retrieve configuration settings:

- Specify configuration settings: `bigquery.config.update` on your organization or project
- Retrieve configuration settings: `bigquery.config.get` on the specified project

You might also be able to get these permissions with [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

For more information about IAM roles and permissions in BigQuery, see [Predefined roles and permissions](https://docs.cloud.google.com/bigquery/access-control) .

## Specify global settings

Global settings apply across all locations and don't use a `region- `` REGION `` .` prefix. In contrast, [regional settings](https://docs.cloud.google.com/bigquery/docs/default-configuration#specify-regional-settings) apply only to a specific location. You can specify global settings at the organization or project level. The default location ( `default_location` ) is the only global setting that you can configure.

If you don't [explicitly specify a location](https://docs.cloud.google.com/bigquery/docs/locations#specify_locations) , the location is determined in one of the following ways:

- The location of the datasets referenced in the request. For example, if a query references a table or view in a dataset stored in the `asia-northeast1` region, the query job runs in `asia-northeast1` .
- The region specified for a connection referenced in a request.
- The location of a destination table.

If the location isn't explicitly specified, and it can't be determined from the resources in the request, the default location is used. If default location isn't set, the job runs in the `US` multi-region.

### Limitations

Global configuration settings are subject to the following limitations:

- Global organization and project settings aren't supported in BigQuery Omni [locations](https://docs.cloud.google.com/bigquery/docs/locations#omni-loc) . You can't set `default_location` to a BigQuery Omni location, or configure or view global settings in a BigQuery Omni location.
- You can't mix global and regional settings in the same `ALTER ORGANIZATION SET OPTIONS` or `ALTER PROJECT SET OPTIONS` DDL statement.
- When you modify the `default_location` global setting, the change can take up to 10 minutes to propagate. Until the setting propagates, BigQuery might route jobs that rely on the default location to the previous default location.

### Configure global organization settings

You can configure global settings at the organization level by using the [`ALTER ORGANIZATION SET OPTIONS` DDL statement](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_organization_set_options_statement) . The default location ( `default_location` ) is the only global setting that you can configure at the organization level. All other organization-level settings are [regional settings](https://docs.cloud.google.com/bigquery/docs/default-configuration#specify-regional-settings) .

The `ALTER ORGANIZATION SET OPTIONS` DDL statement applies to the organization that the current project belongs to.

To configure the `default_location` setting at the organization level, follow these steps:

### Console

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  To open the query editor, click search_insights **Untitled query** .

3.  To configure the `default_location` setting, enter the following DDL statement into the query editor:

    ```
    ALTER ORGANIZATION
      SET OPTIONS (
      `default_location` = 'LOCATION'
      );
    ```

    Replace `LOCATION` with a BigQuery [region or multi-region location](https://docs.cloud.google.com/bigquery/docs/locations) . This value is the location that BigQuery uses to run jobs when the job location can't be inferred from the request—for example, when a query doesn't reference any datasets or connections.

4.  Alternatively, to remove the `default_location` setting at the organization level, enter the following DDL statement into the query editor:

    ```
    ALTER ORGANIZATION
      SET OPTIONS (
      `default_location` = NULL
      );
    ```

5.  Click **Run** .

### bq

To configure the `default_location` setting at the organization level, enter the [`bq query` command](https://docs.cloud.google.com/bigquery/docs/reference/bq-cli-reference#bq_query) with the `--use_legacy_sql` flag set to `false` , and supply the following DDL statement as the query parameter:

```
ALTER ORGANIZATION
  SET OPTIONS (
  `default_location` = 'LOCATION'
  );
```

Replace `LOCATION` with a BigQuery [region or multi-region location](https://docs.cloud.google.com/bigquery/docs/locations) . This value is the location that BigQuery uses to run jobs when the job location can't be inferred from the request—for example, when a query doesn't reference any datasets or connections.

Alternatively, to remove the `default_location` setting at the organization level, enter the [`bq query` command](https://docs.cloud.google.com/bigquery/docs/reference/bq-cli-reference#bq_query) with the `--use_legacy_sql` flag set to `false` , and supply the following DDL statement as the query parameter:

```
ALTER ORGANIZATION
  SET OPTIONS (
  `default_location` = NULL
  );
```

### API

Call the [`jobs.query`](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query) method and supply the DDL statement in the request body's `query` property.

### Configure global project settings

You can configure global settings at the project level by using the [`ALTER PROJECT SET OPTIONS` DDL statement](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_project_set_options_statement) . The default location ( `default_location` ) is the only global setting that you can configure at the project level. All other project-level settings are [regional settings](https://docs.cloud.google.com/bigquery/docs/default-configuration#specify-regional-settings) .

The `ALTER PROJECT SET OPTIONS` DDL statement optionally accepts the `PROJECT_ID` variable. If you don't specify `PROJECT_ID` , then the statement defaults to the project where you run the `ALTER PROJECT` DDL statement.

Project-level configurations override organization-level configurations. In turn, [session-level configurations](https://docs.cloud.google.com/bigquery/docs/sessions-write-queries) can override project-level configurations, and [job-level configurations](https://docs.cloud.google.com/bigquery/docs/running-queries) can override session-level configurations.

To configure the `default_location` setting at the project level, follow these steps:

### Console

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  To open the query editor, click search_insights **Untitled query** .

3.  To configure the `default_location` setting, enter the following DDL statement into the query editor:

    ```
    ALTER PROJECT PROJECT_ID
      SET OPTIONS (
      `default_location` = 'LOCATION'
      );
    ```

    Replace the following:

    - `PROJECT_ID` : the project ID.

    - `LOCATION` : a BigQuery [region or multi-region location](https://docs.cloud.google.com/bigquery/docs/locations) . This value is the location that BigQuery uses to run jobs when the job location can't be inferred from the request—for example, when a query doesn't reference any datasets or connections.

4.  Alternatively, to remove the `default_location` setting at the project level, enter the following DDL statement into the query editor:

    ```
    ALTER PROJECT PROJECT_ID
      SET OPTIONS (
      `default_location` = NULL
      );
    ```

    If you remove the `default_location` setting at the project level, then BigQuery uses the organization-level default setting, if one exists, or the system default setting.

5.  Click **Run** .

### bq

To configure the `default_location` setting at the project level, enter the [`bq query` command](https://docs.cloud.google.com/bigquery/docs/reference/bq-cli-reference#bq_query) with the `--use_legacy_sql` flag set to `false` , and supply the following DDL statement as the query parameter:

```
ALTER PROJECT PROJECT_ID
  SET OPTIONS (
  `default_location` = 'LOCATION'
  );
```

Replace the following:

- `PROJECT_ID` : the project ID.
- `LOCATION` : a BigQuery [region or multi-region location](https://docs.cloud.google.com/bigquery/docs/locations) . This value is the location that BigQuery uses to run jobs when the job location can't be inferred from the request—for example, when a query doesn't reference any datasets or connections.

Alternatively, to remove the `default_location` setting at the project level, enter the [`bq query` command](https://docs.cloud.google.com/bigquery/docs/reference/bq-cli-reference#bq_query) with the `--use_legacy_sql` flag set to `false` , and supply the following DDL statement as the query parameter:

```
ALTER PROJECT PROJECT_ID
  SET OPTIONS (
  `default_location` = NULL
  );
```

If you remove the `default_location` setting at the project level, then BigQuery uses the organization-level default setting, if one exists, or the system default setting.

### API

Call the [`jobs.query`](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query) method and supply the DDL statement in the request body's `query` property.

## Specify regional settings

Regional settings apply to a specific location and require a `region- `` REGION `` .` prefix. You can configure regional settings at the organization or project level.

### Reservation and billing controls

You can configure regional project-level settings to control how queries use reservations or on-demand billing. These settings help ensure cost predictability by either allowing flexible reservation usage or requiring that queries use reservation slots.

Common reservation and billing controls include `reservation_override_mode` ( [Preview](https://docs.cloud.google.com/products#product-launch-stages) ) and `disable_on_demand_billing` ( [Preview](https://docs.cloud.google.com/products#product-launch-stages) ). To configure these settings, see [Configure regional project settings](https://docs.cloud.google.com/bigquery/docs/default-configuration#configure-project-settings) . For a complete list of project options, see the [`ALTER PROJECT SET OPTIONS` options list](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#project_set_options_list) .

### Configure regional organization settings

You can configure regional settings at the organization level by using the [`ALTER ORGANIZATION SET OPTIONS` DDL statement](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_organization_set_options_statement) . You must specify the region where each organization setting applies. You can use only one region in a statement.

The examples in this section specify the following default regional organization settings:

- Time zone: `America/Chicago`
- Cloud KMS key: a user-defined key
- Query timeout: 30 minutes (1,800,000 milliseconds)
- Interactive query queue timeout: 10 minutes (600,000 milliseconds)
- Batch query queue timeout: 20 minutes (1,200,000 milliseconds)
- Table storage and search index `INFORMATION_SCHEMA` views ( `enable_info_schema_storage` ): enabled

For more information about all regional organization settings, see [`organization_set_options_list`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#organization_set_options_list) .

To configure regional organization settings, follow these steps:

### Console

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  To open the query editor, click search_insights **Untitled query** .

3.  To configure the regional organization settings, enter the following DDL statement into the query editor:

    ```
    ALTER ORGANIZATION
      SET OPTIONS (
      `region-REGION.default_time_zone`= 'America/Chicago',
      -- Ensure all service accounts under the organization have permission to KMS_KEY
      `region-REGION.default_kms_key_name` = KMS_KEY,
      `region-REGION.default_query_job_timeout_ms` = 1800000,
      `region-REGION.default_interactive_query_queue_timeout_ms` = 600000,
      `region-REGION.default_batch_query_queue_timeout_ms` = 1200000,
      `region-REGION.enable_info_schema_storage` = true);
    ```

    Replace the following:

    - `REGION` : the [BigQuery region](https://docs.cloud.google.com/bigquery/docs/locations#regions) associated with your project or organization—for example, `us` or `europe-west6` . The value for `REGION` must be the same for each option in the command.
    - `KMS_KEY` : a user-defined Cloud KMS key. For more information, see [Customer-managed Cloud KMS keys](https://docs.cloud.google.com/bigquery/docs/customer-managed-encryption) .

4.  Alternatively, to remove the regional organization settings, enter the following DDL statement into the query editor:

    ```
    ALTER ORGANIZATION
      SET OPTIONS (
      `region-REGION.default_time_zone` = NULL,
      `region-REGION.default_kms_key_name` = NULL,
      `region-REGION.default_query_job_timeout_ms` = NULL,
      `region-REGION.default_interactive_query_queue_timeout_ms` = NULL,
      `region-REGION.default_batch_query_queue_timeout_ms` = NULL,
      `region-REGION.enable_info_schema_storage` = NULL);
    ```

5.  Click **Run** .

### bq

To configure the regional organization settings, enter the [`bq query` command](https://docs.cloud.google.com/bigquery/docs/reference/bq-cli-reference#bq_query) with the `--use_legacy_sql` flag set to `false` , and supply the following DDL statement as the query parameter:

```
ALTER ORGANIZATION
  SET OPTIONS (
  `region-REGION.default_time_zone`= 'America/Chicago',
  -- Ensure all service accounts under the organization have permission to KMS_KEY
  `region-REGION.default_kms_key_name` = KMS_KEY,
  `region-REGION.default_query_job_timeout_ms` = 1800000,
  `region-REGION.default_interactive_query_queue_timeout_ms` = 600000,
  `region-REGION.default_batch_query_queue_timeout_ms` = 1200000,
  `region-REGION.enable_info_schema_storage` = true);
```

Replace the following:

- `REGION` : the [BigQuery region](https://docs.cloud.google.com/bigquery/docs/locations#regions) associated with your project or organization—for example, `us` or `europe-west6` . The value for `REGION` must be the same for each option in the command.
- `KMS_KEY` : a user-defined Cloud KMS key. For more information, see [Customer-managed Cloud KMS keys](https://docs.cloud.google.com/bigquery/docs/customer-managed-encryption) .

Alternatively, to remove the regional organization settings, enter the [`bq query` command](https://docs.cloud.google.com/bigquery/docs/reference/bq-cli-reference#bq_query) with the `--use_legacy_sql` flag set to `false` , and supply the following DDL statement as the query parameter:

```
ALTER ORGANIZATION
  SET OPTIONS (
  `region-REGION.default_time_zone` = NULL,
  `region-REGION.default_kms_key_name` = NULL,
  `region-REGION.default_query_job_timeout_ms` = NULL,
  `region-REGION.default_interactive_query_queue_timeout_ms` = NULL,
  `region-REGION.default_batch_query_queue_timeout_ms` = NULL,
  `region-REGION.enable_info_schema_storage` = NULL);
```

### API

Call the [`jobs.query`](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query) method and supply the DDL statement in the request body's `query` property.

### Configure regional project settings

You can configure regional settings at the project level by using the [`ALTER PROJECT SET OPTIONS` DDL statement](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_project_set_options_statement) . You must specify the region where each project setting applies. You can use only one region in a statement.

Project-level configurations override organization-level configurations. In turn, [session-level configurations](https://docs.cloud.google.com/bigquery/docs/sessions-write-queries) can override project-level configurations, and [job-level configurations](https://docs.cloud.google.com/bigquery/docs/running-queries) can override session-level configurations.

The `ALTER PROJECT SET OPTIONS` DDL statement optionally accepts the `PROJECT_ID` variable. If you don't specify `PROJECT_ID` , then the statement defaults to the project where you run the `ALTER PROJECT` DDL statement.

The examples in this section specify the following default regional project settings:

- Time zone: `America/Los_Angeles`
- Cloud KMS key: a user-defined key
- Query timeout: 1 hour (3,600,000 milliseconds)
- Interactive query queue timeout: 10 minutes (600,000 milliseconds)
- Batch query queue timeout: 20 minutes (1,200,000 milliseconds)
- Reservation-based fairness: enabled
- Global queries: enabled for running and for accessing data
- Table storage and search index `INFORMATION_SCHEMA` views ( `enable_info_schema_storage` ): enabled

For more information about all regional project settings, see [`project_set_options_list`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#project_set_options_list) .

To configure regional project settings, follow these steps:

### Console

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  To open the query editor, click search_insights **Untitled query** .

3.  To configure the regional project settings, enter the following DDL statement into the query editor:

    ```
    ALTER PROJECT PROJECT_ID
     SET OPTIONS (
     `region-REGION.default_time_zone` = 'America/Los_Angeles',
     -- Ensure all service accounts under the project have permission to KMS_KEY
     `region-REGION.default_kms_key_name` = KMS_KEY,
     `region-REGION.default_query_job_timeout_ms` = 3600000,
     `region-REGION.default_interactive_query_queue_timeout_ms` = 600000,
     `region-REGION.default_batch_query_queue_timeout_ms` = 1200000,
     `region-REGION.enable_reservation_based_fairness` = true,
     `region-REGION.enable_global_queries_execution` = true,
     `region-REGION.enable_global_queries_data_access` = true,
     `region-REGION.enable_info_schema_storage` = true);
    ```

    Replace the following:

    - `PROJECT_ID` : the project ID.
    - `REGION` : the [BigQuery region](https://docs.cloud.google.com/bigquery/docs/locations#regions) associated with your project or organization—for example, `us` or `europe-west6` . The value for `REGION` must be the same for each option in the command.
    - `KMS_KEY` : a user-defined Cloud KMS key. For more information, see [Customer-managed Cloud KMS keys](https://docs.cloud.google.com/bigquery/docs/customer-managed-encryption) .

4.  Alternatively, to remove the regional project settings, enter the following DDL statement into the query editor:

    ```
    ALTER PROJECT PROJECT_ID
      SET OPTIONS (
      `region-REGION.default_time_zone` = NULL,
      `region-REGION.default_kms_key_name` = NULL,
      `region-REGION.default_query_job_timeout_ms` = NULL,
      `region-REGION.default_interactive_query_queue_timeout_ms` = NULL,
      `region-REGION.default_batch_query_queue_timeout_ms` = NULL,
      `region-REGION.enable_reservation_based_fairness` = false,
      `region-REGION.enable_global_queries_execution` = NULL,
      `region-REGION.enable_global_queries_data_access` = NULL,
      `region-REGION.enable_info_schema_storage` = NULL);
    ```

5.  Click **Run** .

### bq

To configure the regional project settings, enter the [`bq query` command](https://docs.cloud.google.com/bigquery/docs/reference/bq-cli-reference#bq_query) with the `--use_legacy_sql` flag set to `false` , and supply the following DDL statement as the query parameter:

```
ALTER PROJECT PROJECT_ID
  SET OPTIONS (
  `region-REGION.default_time_zone` = 'America/Los_Angeles',
  -- Ensure all service accounts under the project have permission to KMS_KEY
  `region-REGION.default_kms_key_name` = KMS_KEY,
  `region-REGION.default_query_job_timeout_ms` = 3600000,
  `region-REGION.default_interactive_query_queue_timeout_ms` = 600000,
  `region-REGION.default_batch_query_queue_timeout_ms` = 1200000,
  `region-REGION.enable_reservation_based_fairness` = true,
  `region-REGION.enable_global_queries_execution` = true,
  `region-REGION.enable_global_queries_data_access` = true,
  `region-REGION.enable_info_schema_storage` = true);
```

Replace the following:

- `PROJECT_ID` : the project ID.
- `REGION` : the [BigQuery region](https://docs.cloud.google.com/bigquery/docs/locations#regions) associated with your project or organization—for example, `us` or `europe-west6` . The value for `REGION` must be the same for each option in the command.
- `KMS_KEY` : a user-defined Cloud KMS key. For more information, see [Customer-managed Cloud KMS keys](https://docs.cloud.google.com/bigquery/docs/customer-managed-encryption) .

Alternatively, to remove the regional project settings, enter the [`bq query` command](https://docs.cloud.google.com/bigquery/docs/reference/bq-cli-reference#bq_query) with the `--use_legacy_sql` flag set to `false` , and supply the following DDL statement as the query parameter:

```
ALTER PROJECT PROJECT_ID
  SET OPTIONS (
  `region-REGION.default_time_zone` = NULL,
  `region-REGION.default_kms_key_name` = NULL,
  `region-REGION.default_query_job_timeout_ms` = NULL,
  `region-REGION.default_interactive_query_queue_timeout_ms` = NULL,
  `region-REGION.default_batch_query_queue_timeout_ms` = NULL,
  `region-REGION.enable_reservation_based_fairness` = false,
  `region-REGION.enable_global_queries_execution` = NULL,
  `region-REGION.enable_global_queries_data_access` = NULL,
  `region-REGION.enable_info_schema_storage` = NULL);
```

### API

Call the [`jobs.query`](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query) method and supply the DDL statement in the request body's `query` property.

## Retrieve configuration settings

You can view the configuration settings for an organization or project by using the following [`INFORMATION_SCHEMA`](https://docs.cloud.google.com/bigquery/docs/information-schema-intro) views:

- [`INFORMATION_SCHEMA.PROJECT_OPTIONS`](https://docs.cloud.google.com/bigquery/docs/information-schema-project-options) : the configurations applied to a project.
- [`INFORMATION_SCHEMA.EFFECTIVE_PROJECT_OPTIONS`](https://docs.cloud.google.com/bigquery/docs/information-schema-effective-project-options) : the effective configurations applied to a project. Effective configurations include all configurations set at the project level as well as all settings inherited by the project from an organization.
- [`INFORMATION_SCHEMA.ORGANIZATION_OPTIONS`](https://docs.cloud.google.com/bigquery/docs/information-schema-organization-options) : the configurations applied to an organization.

New configurations can take a few minutes to take effect and appear in the `INFORMATION_SCHEMA` views.

### Query examples to retrieve settings

Use the following query examples to retrieve your project and organization settings from the `INFORMATION_SCHEMA` views.

#### View global settings

To view all global organization settings, run the following query:

```
SELECT * FROM INFORMATION_SCHEMA.ORGANIZATION_OPTIONS;
```

To view only the `default_location` organization setting, run the following query:

```
SELECT
    option_value
FROM INFORMATION_SCHEMA.ORGANIZATION_OPTIONS
WHERE option_name = 'default_location'
```

To view all effective global configurations for your default project, run the following query:

```
SELECT * FROM INFORMATION_SCHEMA.EFFECTIVE_PROJECT_OPTIONS;
```

To view only the effective `default_location` setting for your default project, run the following query:

```
SELECT
    option_value
FROM INFORMATION_SCHEMA.EFFECTIVE_PROJECT_OPTIONS
WHERE option_name = 'default_location'
```

To view all global configurations for your default project, run the following query:

```
SELECT * FROM INFORMATION_SCHEMA.PROJECT_OPTIONS;
```

To view only the `default_location` setting for your default project, run the following query:

```
SELECT
    option_value
FROM INFORMATION_SCHEMA.PROJECT_OPTIONS
WHERE option_name = 'default_location'
```

#### View regional settings

To view the configurations under an organization in the `us` region, run the following query:

```
SELECT * FROM region-us.INFORMATION_SCHEMA.ORGANIZATION_OPTIONS;
```

To view the effective configurations under your default project in the `us` region, run the following query:

```
SELECT * FROM region-us.INFORMATION_SCHEMA.EFFECTIVE_PROJECT_OPTIONS;
```

To view the configurations under your default project in the `us` region, run the following query:

```
SELECT * FROM region-us.INFORMATION_SCHEMA.PROJECT_OPTIONS;
```

## Default configuration settings

The following sections describe the configuration settings that you can specify.

### Query and job execution settings

Use the following settings to control how queries are executed, timed, and queued.

- `default_batch_query_queue_timeout_ms` : The default amount of time, in milliseconds, that a batch query waits in a [query queue](https://docs.cloud.google.com/bigquery/docs/query-queues) . If unset, the default is 24 hours. The minimum value is 1 millisecond. The maximum value is 48 hours. To turn off batch query queueing, set the value to `-1` .

- `default_interactive_query_queue_timeout_ms` : The default amount of time in milliseconds that an interactive query waits in a [query queue](https://docs.cloud.google.com/bigquery/docs/query-queues) . If unset, then the default is 6 hours. The minimum value is 1 millisecond, and the maximum value is 48 hours. To turn off interactive query queueing, set the value to `-1` .

- `default_query_job_timeout_ms` : The default time after which a query job times out, including the time the job is queued and the time spent running. The timeout period must be between 5 minutes and 48 hours. This timeout only applies to individual query jobs and the child jobs of scripts. To set a timeout for script jobs, use the [`jobs.insert`](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/jobs/insert) API method and set the `jobTimeoutMs` field.

  > **Note:** The `default_query_job_timeout_ms` setting also applies to [continuous query](https://docs.cloud.google.com/bigquery/docs/continuous-queries-introduction) jobs. To override this project-level setting for an individual continuous query, assign a [job timeout](https://docs.cloud.google.com/bigquery/docs/continuous-queries#run_a_continuous_query_by_using_a_service_account) to the continuous query in question. Continuous queries still adhere to [maximum runtimes](https://docs.cloud.google.com/bigquery/docs/continuous-queries-introduction#authorization) .

- `default_location` : The [`default_location` configuration setting](https://docs.cloud.google.com/bigquery/docs/default-configuration#global-settings) is used to run jobs when the location isn't set or can't be determined. If `default_location` isn't set, the job runs in the `US` multi-region. For more information, see [Specify locations](https://docs.cloud.google.com/bigquery/docs/locations#specify_locations) .

- `enable_reservation_based_fairness` : The option that determines how idle slots are shared. For administration projects created after October 10, 2026, this option is enabled ( `TRUE` ) by default. For projects created before October 10, 2026, default value is `FALSE` , which means that idle slots are distributed equally across all query projects. If you enable this option, then idle slots are shared equally across all reservations first, and then across projects within each reservation. For more information, see [reservation-based fairness](https://docs.cloud.google.com/bigquery/docs/slots#fairness) . This option is only supported at the project level. You can't specify it at the organization or job level.

- `default_time_zone` : The default time zone to use in time zone-dependent GoogleSQL functions, when a time zone is not specified as an argument. This configuration does not apply to [time-unit column partitioned tables](https://docs.cloud.google.com/bigquery/docs/partitioned-tables#date_timestamp_partitioned_tables) (which use UTC as the time zone), the [Storage Transfer Service schedule transfers](https://docs.cloud.google.com/storage-transfer/docs/schedule-transfer-jobs) , or [loading data with the bq command-line tool](https://docs.cloud.google.com/bigquery/docs/bq-command-line-tool#loading_data) . For more information, see [time zones](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-types#time_zones) .

  > **Note:** If you want to set a default time zone, then ensure that any existing queries that use `DATETIME` literals aren't affected. Affected queries include those that use the explicit `DATETIME` keyword, implicitly converted string literals passed to time functions such as `DATETIME_DIFF('2022-10-01', ...)` , and the `PARSE_DATETIME()` function. For this reason, it's safer to set the `default_time_zone` setting only on new projects.

- `default_query_optimizer_options` : The history-based query optimizations. This option can be one of the following:

  - `'adaptive=on'` : Use history-based query optimizations.
  - `'adaptive=off'` : Don't use history-based query optimizations.
  - `NULL` (default): Use the default history-based query optimizations setting, which is equivalent to `'adaptive=on'` .

- `default_sql_dialect_option` : The default SQL query dialect for executing query jobs using the bq command-line tool or BigQuery API. Changing this setting doesn't affect the default dialect in the console. This option can be one of the following:

  - `'default_legacy_sql'` (default): Use legacy SQL if the query dialect isn't specified at the job level.
  - `'default_google_sql'` : Use GoogleSQL if the query dialect isn't specified at the job level.
  - `'only_google_sql'` : Use GoogleSQL if the query dialect isn't specified at the job level. Reject jobs with query dialect set to legacy SQL.
  - `NULL` : Use the default query dialect setting, which is equivalent to `'default_legacy_sql'` .

- `enable_global_queries_execution` : The option that determines whether [global queries](https://docs.cloud.google.com/bigquery/docs/global-queries) can run. The default value is `FALSE` , which means that global queries are not enabled.

- `enable_global_queries_data_access` : The option that determines whether [global queries](https://docs.cloud.google.com/bigquery/docs/global-queries) can access data stored in the region. The default value is `FALSE` , which means that global queries can't copy data from this region regardless of the project in which they run.

- `reusable_column_aliases_mode` : The option that determines whether reusable column aliases are enabled for queries. The default value is `off` , which means that reusable column aliases aren't enabled. For more information, see [Reusable column aliases](https://docs.cloud.google.com/bigquery/docs/column-aliases) .

### Data management settings

Use the following settings to define rules for data creation, security, and lifecycle.

- `default_column_name_character_map` : The default scope and handling of characters in column names. If unset, load jobs that use unsupported characters in column names fail with an error message. Some older tables might be set to replace unsupported characters in column names. For more information, see [`load_option_list`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/load-statements#load_option_list) .

- `default_data_policy_projects` : The default list of projects whose [data policies](https://docs.cloud.google.com/bigquery/docs/column-level-security-intro) are evaluated when accessing columns protected by [data governance tags](https://docs.cloud.google.com/bigquery/docs/tags#data-governance-tags) . By default, only the data policies of the table's project are evaluated. When you configure a default data policy project at the organization level, BigQuery evaluates both the data policies of the table's project and those of the default data policy project. If conflicting policies exist in both projects, the data policies in the table's project take precedence. You can configure this setting only at the organization level by using the [`ALTER ORGANIZATION SET OPTIONS` statement](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_organization_set_options_statement) —for example, `region-us.default_data_policy_projects = ["my_default_project"]` . For more information, see [Configure a default data policy project](https://docs.cloud.google.com/bigquery/docs/tags#configure-default-data-policy-project) .

- `default_kms_key_name` : The default Cloud Key Management Service key for encrypting table data, including temporary or anonymous tables. For more information, see [Customer-managed Cloud KMS keys](https://docs.cloud.google.com/bigquery/docs/customer-managed-encryption) .

  > **Note:** to set a default Cloud KMS key, you must grant the Encrypter/Decrypter role to all BigQuery service accounts that are used within the project or organization. If a service account within the project or organization doesn't have appropriate permissions, all queries run by the service account fail. For information about assigning the Encrypter/Decrypter role, see [Assign the Encrypter/Decrypter role](https://docs.cloud.google.com/bigquery/docs/customer-managed-encryption#assign_role) . If you set a default Cloud KMS key without first assigning the appropriate roles, you can remove the default key by setting the value to `NULL` . For examples, see [Configure regional organization settings](https://docs.cloud.google.com/bigquery/docs/default-configuration#configure-organization-settings) and [Configure regional project settings](https://docs.cloud.google.com/bigquery/docs/default-configuration#configure-project-settings) .

- `default_max_time_travel_hours` : The default time travel window in hours for new datasets. This duration must be within the range of 48 to 168, inclusive, and must be divisible by 24. Changing the default max time travel hours does not affect existing datasets. For more information, see [Time Travel and data retention](https://docs.cloud.google.com/bigquery/docs/time-travel#time_travel) .

- `enable_info_schema_storage` : The option that provides access to [`INFORMATION_SCHEMA.TABLE_STORAGE`](https://docs.cloud.google.com/bigquery/docs/information-schema-table-storage) and [`SEARCH_INDEXES`](https://docs.cloud.google.com/bigquery/docs/information-schema-indexes) views and their variants. By default, this option isn't enabled. If you query these views for the first time without setting this option to `TRUE` , then the query fails and provides instructions to enable the option. After you enable this option, queries succeed immediately and return data generated from that point forward. A complete backfill of historical data can take approximately one day to become available in the views. If you used these views before this setting was introduced, then this option is already enabled.

### Cost and resource settings

Use the following settings to determine how resources are billed and connected.

- `default_storage_billing_model` : The default storage billing model for new datasets. Set the value to `PHYSICAL` to use physical bytes when calculating storage charges or to `LOGICAL` to use logical bytes. Changing the default storage billing model doesn't affect existing datasets. For more information, see [Storage billing models](https://docs.cloud.google.com/bigquery/docs/datasets-intro#dataset_storage_billing_models) .
- `default_cloud_resource_connection_id` : The default connection to use when you create tables and models. Specify only the connection's ID or name, and exclude the attached project ID and region prefixes. When you use default connections, BigQuery might update the permissions granted to the connection's service account, depending on the type of table or model that you're creating. For more information, see the [Default connection overview](https://docs.cloud.google.com/bigquery/docs/default-connections) .
- `reservation_override_mode` ( [Preview](https://docs.cloud.google.com/products#product-launch-stages) ): Specifies how query reservations can be overridden in the region (for example, `'ALLOW_ANY_OVERRIDE'` ). For details, see the [`ALTER PROJECT SET OPTIONS` options list](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#project_set_options_list) .
- `disable_on_demand_billing` ( [Preview](https://docs.cloud.google.com/products#product-launch-stages) ): Determines whether on-demand billing is disabled for queries in the region. If `true` , all queries must use an assigned reservation or they fail. For details, see the [`ALTER PROJECT SET OPTIONS` options list](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#project_set_options_list) .
- `preflight_fluid_autoscaling_reservations` : The list of reservations that are opted in to fluid scaling for per-second billing with no minimum duration. For more information, see [Understand reservations](https://docs.cloud.google.com/bigquery/docs/reservations-workload-management) .

## Pricing

There is no additional charge to use the BigQuery configuration service. For more information, see [BigQuery pricing](https://cloud.google.com/bigquery/pricing) .
