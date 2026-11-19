---
name: documents/docs.cloud.google.com/bigquery/docs/information-schema-row-access-policies
uri: https://docs.cloud.google.com/bigquery/docs/information-schema-row-access-policies
title: ROW_ACCESS_POLICIES view
description: Query the BigQuery INFORMATION_SCHEMA.ROW_ACCESS_POLICIES view to retrieve real-time metadata about active row-level access policies in a dataset or region.
data_source: docs.cloud.google.com
---

# ROW_ACCESS_POLICIES view

The `INFORMATION_SCHEMA.ROW_ACCESS_POLICIES` view contains one row for each active row access policy in the dataset or region that you specify. You can query this view to audit row access policies and inspect filter predicates across tables in BigQuery. For more information about row-level security, see [Introduction to BigQuery row-level security](https://docs.cloud.google.com/bigquery/docs/row-level-security-intro) .

## Required roles

To get the permissions that you need to query the `INFORMATION_SCHEMA.ROW_ACCESS_POLICIES` view, ask your administrator to grant you the following IAM roles on the dataset or project:

- [BigQuery Data Owner](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner) ( `roles/bigquery.dataOwner` )
- [BigQuery Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin) ( `roles/bigquery.admin` )
- [BigQuery Security Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin) ( `roles/bigquery.securityAdmin` )

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

These predefined roles contain the permissions required to query the `INFORMATION_SCHEMA.ROW_ACCESS_POLICIES` view. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to query the `INFORMATION_SCHEMA.ROW_ACCESS_POLICIES` view:

- `bigquery.rowAccessPolicies.get`
- `bigquery.rowAccessPolicies.list`

You might also be able to get these permissions with [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

For more information about IAM roles and permissions in BigQuery, see [Predefined roles and permissions](https://docs.cloud.google.com/bigquery/docs/access-control) .

## Schema

When you query the `INFORMATION_SCHEMA.ROW_ACCESS_POLICIES` view, the query results contain one row for each active row access policy in the resource scope that you specify.

The `INFORMATION_SCHEMA.ROW_ACCESS_POLICIES` view has the following schema:

| Column name              | Data type   | Value                                                                                        |
|--------------------------|-------------|----------------------------------------------------------------------------------------------|
| `table_catalog`          | `STRING`    | The ID of the project that contains the row access policy.                                   |
| `table_schema`           | `STRING`    | The name of the dataset that contains the row access policy.                                 |
| `table_name`             | `STRING`    | The name of the table that contains the row access policy.                                   |
| `row_access_policy_name` | `STRING`    | The name of the row access policy.                                                           |
| `filter_predicate`       | `STRING`    | The SQL boolean expression that defines which rows are accessible by this row access policy. |
| `creation_time`          | `TIMESTAMP` | The time when the row access policy was created.                                             |
| `last_modified_time`     | `TIMESTAMP` | The time when the row access policy was last modified.                                       |

For stability, we recommend that you explicitly list columns in your information schema queries instead of using a wildcard ( `SELECT *` ). Explicitly listing columns prevents queries from breaking if the underlying schema changes.

## Scope and syntax

Queries against this view must include a dataset or a region qualifier. For queries with a dataset qualifier, you must have permissions for the dataset. For queries with a region qualifier, you must have permissions for the project. For more information about view syntax, see [Syntax](https://docs.cloud.google.com/bigquery/docs/information-schema-intro#syntax) . The following table explains the region and resource scopes for this view:

| View name                                                                                     | Resource scope | Region scope     |
|-----------------------------------------------------------------------------------------------|----------------|------------------|
| `[ `` PROJECT_ID ```  .]`region-  ``` REGION ```  `.INFORMATION_SCHEMA.ROW_ACCESS_POLICIES `` | Project level  | `REGION`         |
| `[ `` PROJECT_ID `` .] `` DATASET_ID `` .INFORMATION_SCHEMA.ROW_ACCESS_POLICIES`              | Dataset level  | Dataset location |

> **Note:** `INFORMATION_SCHEMA` view names are case-sensitive.

Replace the following:

- Optional: `PROJECT_ID` : the ID of your Google Cloud project. If not specified, the default project is used.

- `REGION` : any [dataset region name](https://docs.cloud.google.com/bigquery/docs/locations) . For example, `` `region-us` `` .

- `DATASET_ID` : the ID of your dataset. For more information, see [Dataset qualifier](https://docs.cloud.google.com/bigquery/docs/information-schema-intro#dataset_qualifier) .

  > **Note:** You must use [a region qualifier](https://docs.cloud.google.com/bigquery/docs/information-schema-intro#region_qualifier) to query `INFORMATION_SCHEMA` views. The location of the query execution must match the region of the `INFORMATION_SCHEMA` view.

## Limitations

The `INFORMATION_SCHEMA.ROW_ACCESS_POLICIES` view has the following limitations:

- The view doesn't include grantee information or a `ddl` column because row access policy grantees are stored in IAM policy bindings rather than BigQuery catalog metadata. To view the principals granted access by a row access policy, see [List table row-level access policies](https://docs.cloud.google.com/bigquery/docs/managing-row-level-security#list-policy) .
- Results don't include row access policies in [hidden datasets](https://docs.cloud.google.com/bigquery/docs/datasets#hidden_datasets) or BigLake datasets.

## Examples

The following examples show how to query the `INFORMATION_SCHEMA.ROW_ACCESS_POLICIES` view.

### Query row access policies in a region

The following example retrieves metadata for all active row access policies in the `us` region for your default project:

```
SELECT
  table_catalog,
  table_schema,
  table_name,
  row_access_policy_name,
  filter_predicate,
  creation_time,
  last_modified_time
FROM
  `region-us`.INFORMATION_SCHEMA.ROW_ACCESS_POLICIES;
```

The result is similar to the following:

```
+---------------+--------------+------------+------------------------+--------------------+-----------------------------+-----------------------------+
| table_catalog | table_schema | table_name | row_access_policy_name | filter_predicate   | creation_time               | last_modified_time          |
+---------------+--------------+------------+------------------------+--------------------+-----------------------------+-----------------------------+
| my_project    | my_dataset   | my_table   | apac_filter            | region = 'APAC'    | 2026-03-10 14:22:05.123 UTC | 2026-03-10 14:22:05.123 UTC |
| my_project    | my_dataset   | my_table   | us_filter              | region = 'US'      | 2026-03-10 14:25:18.456 UTC | 2026-03-12 09:15:42.789 UTC |
+---------------+--------------+------------+------------------------+--------------------+-----------------------------+-----------------------------+
```

### Query row access policies in a dataset

The following example retrieves metadata for all active row access policies in a specific dataset named `my_dataset` :

```
SELECT
  table_name,
  row_access_policy_name,
  filter_predicate,
  creation_time,
  last_modified_time
FROM
  my_dataset.INFORMATION_SCHEMA.ROW_ACCESS_POLICIES;
```

The result is similar to the following:

```
+------------+------------------------+--------------------+-----------------------------+-----------------------------+
| table_name | row_access_policy_name | filter_predicate   | creation_time               | last_modified_time          |
+------------+------------------------+--------------------+-----------------------------+-----------------------------+
| my_table   | apac_filter            | region = 'APAC'    | 2026-03-10 14:22:05.123 UTC | 2026-03-10 14:22:05.123 UTC |
| my_table   | us_filter              | region = 'US'      | 2026-03-10 14:25:18.456 UTC | 2026-03-12 09:15:42.789 UTC |
+------------+------------------------+--------------------+-----------------------------+-----------------------------+
```

### Count row access policies on a table

The following example counts the number of active row access policies on the `my_table` table in `my_project.my_dataset` :

```
SELECT
  COUNT(1) AS total_policies
FROM
  my_project.my_dataset.INFORMATION_SCHEMA.ROW_ACCESS_POLICIES
WHERE
  table_name = 'my_table';
```

The result is similar to the following:

```
+----------------+
| total_policies |
+----------------+
| 2              |
+----------------+
```
