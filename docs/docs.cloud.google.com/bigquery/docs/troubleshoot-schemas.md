---
name: documents/docs.cloud.google.com/bigquery/docs/troubleshoot-schemas
uri: https://docs.cloud.google.com/bigquery/docs/troubleshoot-schemas
title: Troubleshoot schema errors
description: Troubleshoot BigQuery schema mismatch and nesting depth limit errors (HTTP 400 invalid), including missing fields, type or mode changes, and RECORD nesting.
data_source: docs.cloud.google.com
---

# Troubleshoot schema errors

This document helps you diagnose and resolve HTTP `400 Bad Request` errors that occur when you modify BigQuery table schemas or when you define or load deeply nested schema structures. For information about how to use `INFORMATION_SCHEMA` views to troubleshoot BigQuery performance, see [Troubleshoot with information schema](https://docs.cloud.google.com/bigquery/docs/info-schema-troubleshoot) .

## Troubleshoot schema mismatch errors

BigQuery returns a `Provided Schema does not match Table` error ( `reason: invalid` ) when one of the following operations supplies a schema that conflicts with the target table's existing schema:

- A load job
- A query job with a destination table
- A copy job
- An `ALTER TABLE` DDL statement
- A table metadata update ( `tables.update` or `tables.patch` )

To identify the specific cause and resolution, match your error message to one of the following scenarios.

### Field is missing in new schema

**Error message**

```
Provided Schema does not match Table PROJECT_ID:DATASET.TABLE. Field FIELD_NAME is missing in new schema
```

#### Diagnosis

One of the following operations provides a schema definition that omits one or more columns that already exist in the destination table:

- A load job
- A DataFrame write operation
- A `tables.update` or `tables.patch` API call

#### Resolution

BigQuery doesn't allow dropping columns implicitly by omitting them from an API schema payload or load job configuration. To resolve this error, do one of the following:

- Update your pipeline or API request so that the provided schema includes all existing columns in the target table.

- If you intend to remove the column from the table, run a [`DROP COLUMN` DDL statement](https://docs.cloud.google.com/bigquery/docs/managing-table-schemas#delete_a_column) instead of omitting the column from a load or patch request:

  ```
  ALTER TABLE `PROJECT_ID.DATASET.TABLE`
  DROP COLUMN FIELD_NAME;
  ```

  Replace the following:

  - `PROJECT_ID` : the ID of the project that contains the table.
  - `DATASET` : the name of the dataset that contains the table.
  - `TABLE` : the name of the table.
  - `FIELD_NAME` : the name of the column to drop.

### Field has changed type

**Error message**

```
Provided Schema does not match Table PROJECT_ID:DATASET.TABLE. Field FIELD_NAME has changed type from EXISTING_TYPE to NEW_TYPE
```

#### Diagnosis

Your request attempts to change an existing column's data type (for example, from `STRING` to `INT64` ) in place during a load job or schema update.

#### Resolution

To resolve this error, do one of the following:

- If the type change is a supported [column data type conversion](https://docs.cloud.google.com/bigquery/docs/managing-table-schemas#change_a_columns_data_type) (such as `INT64` to `NUMERIC` , `INT64` to `FLOAT64` , or `NUMERIC` to `BIGNUMERIC` ), use an `ALTER TABLE ... ALTER COLUMN` DDL statement:

  ```
  ALTER TABLE `PROJECT_ID.DATASET.TABLE`
  ALTER COLUMN FIELD_NAME SET DATA TYPE NEW_TYPE;
  ```

  Replace the following:

  - `PROJECT_ID` : the ID of the project that contains the table.
  - `DATASET` : the name of the dataset that contains the table.
  - `TABLE` : the name of the table.
  - `FIELD_NAME` : the name of the column to modify.
  - `NEW_TYPE` : the target data type.

- If the type conversion isn't supported in place, query the existing data with an explicit `CAST` expression and write the results to a new table or overwrite the existing table. For more information, see [Change a column's data type](https://docs.cloud.google.com/bigquery/docs/managing-table-schemas#change_a_columns_data_type) .

### Field has changed mode

**Error message**

```
Provided Schema does not match Table PROJECT_ID:DATASET.TABLE. Field FIELD_NAME has changed mode from EXISTING_MODE to NEW_MODE
```

#### Diagnosis

Your request attempts an unsupported column mode change (for example, changing `NULLABLE` to `REQUIRED` or `REPEATED` to `NULLABLE` ). This error also occurs if you use an inline schema definition in the bq command-line tool when relaxing a `REQUIRED` column on a table that contains `REPEATED` columns, because inline schema definitions in the bq command-line tool don't support modifying tables with `REPEATED` columns.

#### Resolution

The only mode change supported by in-place BigQuery schema updates is relaxing a column's mode from `REQUIRED` to `NULLABLE` . To resolve this error, do one of the following:

- If you are relaxing a column from `REQUIRED` to `NULLABLE` , run an `ALTER TABLE ... ALTER COLUMN ... DROP NOT NULL` DDL statement in GoogleSQL, or supply a JSON schema file if you are updating the schema with the `bq update` command or the `tables.patch` API method. For instructions, see [Change a column's mode](https://docs.cloud.google.com/bigquery/docs/managing-table-schemas#change_a_columns_mode) .
- To change a column's mode from `NULLABLE` to `REQUIRED` or from `REPEATED` to `NULLABLE` , create a new table with the updated schema and copy or load the data into the new table. For instructions, see [Modifying table schemas](https://docs.cloud.google.com/bigquery/docs/managing-table-schemas) .

### Cannot add fields

**Error message**

```
Provided Schema does not match Table PROJECT_ID:DATASET.TABLE. Cannot add fields (field: FIELD_NAME)
```

#### Diagnosis

A load job or query job includes a column ( `FIELD_NAME` ) that doesn't exist in the destination table, and schema addition isn't enabled in the job configuration.

#### Resolution

Enable schema addition on the load or query job:

- In the REST API or client libraries, include `ALLOW_FIELD_ADDITION` in the `schemaUpdateOptions` property of your load or query job configuration.
- In the bq command-line tool, pass the `--schema_update_option=ALLOW_FIELD_ADDITION` flag.
- Alternatively, add the column before running the job by using [`ALTER TABLE ... ADD COLUMN`](https://docs.cloud.google.com/bigquery/docs/managing-table-schemas#add_an_empty_column) .

### Cannot add required fields to an existing schema

**Error message**

```
Provided Schema does not match Table PROJECT_ID:DATASET.TABLE. Cannot add required fields to an existing schema. (field: FIELD_NAME)
```

#### Diagnosis

Your request appends a new column to an existing table with the column mode set to `REQUIRED` ( `NOT NULL` ). Because existing rows in the table would receive `NULL` values for the newly added column, BigQuery rejects adding `REQUIRED` columns directly through schema updates.

#### Resolution

To resolve this error, do one of the following:

- Add the new column with mode `NULLABLE` instead of `REQUIRED` , and then run a DML `UPDATE` statement to populate values for existing rows.

- To add the column and assign a [default value](https://docs.cloud.google.com/bigquery/docs/default-values) , complete the following steps:

  1.  Add the column as a `NULLABLE` column.

  2.  Set the column's default value so that future inserts receive a value automatically.

  3.  Update existing rows to populate the default value:

      ```
      ALTER TABLE `PROJECT_ID.DATASET.TABLE`
      ADD COLUMN FIELD_NAME DATA_TYPE;

      ALTER TABLE `PROJECT_ID.DATASET.TABLE`
      ALTER COLUMN FIELD_NAME SET DEFAULT DEFAULT_EXPRESSION;

      UPDATE `PROJECT_ID.DATASET.TABLE`
      SET FIELD_NAME = DEFAULT_EXPRESSION
      WHERE TRUE;
      ```

      Replace the following:

      - `PROJECT_ID` : the ID of the project that contains the table.
      - `DATASET` : the name of the dataset that contains the table.
      - `TABLE` : the name of the table.
      - `FIELD_NAME` : the name of the new column.
      - `DATA_TYPE` : the column's data type.
      - `DEFAULT_EXPRESSION` : the default value expression for the column.

### Field already exists in schema

**Error message**

```
Field FIELD_NAME already exists in schema
```

#### Diagnosis

The schema provided in the API request, JSON schema file, or source file header (such as CSV or Parquet) contains duplicate column names. Column names in BigQuery are case-insensitive, so specifying both `Field_A` and `field_a` in the same schema triggers this error.

#### Resolution

Inspect the source schema and remove or rename duplicate column names, including any case-insensitive name collisions.

### Updating field collation is not supported

**Error message**

```
Provided Schema does not match Table PROJECT_ID:DATASET.TABLE. Invalid schema update. Updating field collation is not supported. Field FIELD_NAME has changed collation from "EXISTING_COLLATION" to "NEW_COLLATION"
```

#### Diagnosis

You can't modify or remove the [collation specification](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/collation-concepts) of an existing column during a schema update. This error commonly occurs when an application fetches a table's schema, modifies another field, and writes the schema back using an older client library version that doesn't preserve the `collation` field property (sending `""` instead of `"und:ci"` ).

#### Resolution

To resolve this error, do the following:

- Upgrade your BigQuery client library to the latest version so that existing `collation` attributes are preserved when reading and patching table metadata.
- If you construct JSON schema payloads manually, ensure that the `collation` property on existing columns matches the table's current schema.

### Narrowing type parameters is not compatible

**Error message**

```
Provided Schema does not match Table PROJECT_ID:DATASET.TABLE. Narrowing type parameters is not compatible
```

#### Diagnosis

Your `ALTER TABLE ... ALTER COLUMN ... SET DATA TYPE` statement attempts to reduce the maximum length, precision, or scale of a [parameterized data type](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-types#parameterized_data_types) —for example, changing `STRING(100)` to `STRING(50)` or reducing `NUMERIC(P, S)` parameters.

#### Resolution

BigQuery only allows widening type parameters on an existing column in place (such as increasing `STRING(50)` to `STRING(100)` ). To enforce narrower type parameters, create a new table defined with the narrower type parameter and copy or load the data into the new table by using a `SELECT` query that makes values fit the narrower type (for example, `LEFT(FIELD_NAME, 50)` for a `STRING` column). Writing a `STRING` or `BYTES` value longer than the column's maximum length, or a `NUMERIC` value with more digits than its precision allows, returns an error. `NUMERIC` values with more decimal digits than the column's scale are rounded. For more information, see [Modifying table schemas](https://docs.cloud.google.com/bigquery/docs/managing-table-schemas) .

### Adding a field with a default value is not supported

**Error message**

```
Provided Schema does not match Table PROJECT_ID:DATASET.TABLE. Add field with default value to an existing table schema is not supported; Field: FIELD_NAME. ...
```

#### Diagnosis

Your load job or `tables.patch` or `tables.update` API request attempts to add a new column to an existing table while specifying `defaultValueExpression` in the API schema payload. You can't add a new column with a default value to an existing table in a single API schema update.

#### Resolution

Instead of specifying `defaultValueExpression` when you add the column in the API request, add the column first and then set its default value (for more information, see [Limitations](https://docs.cloud.google.com/bigquery/docs/default-values#limitations) ):

- If you haven't added the column yet, run the following statements, and then resume your loads without `defaultValueExpression` :

  ```
  ALTER TABLE `PROJECT_ID.DATASET.TABLE`
  ADD COLUMN FIELD_NAME DATA_TYPE;

  ALTER TABLE `PROJECT_ID.DATASET.TABLE`
  ALTER COLUMN FIELD_NAME SET DEFAULT DEFAULT_EXPRESSION;

  UPDATE `PROJECT_ID.DATASET.TABLE`
  SET FIELD_NAME = DEFAULT_EXPRESSION
  WHERE TRUE;
  ```

  Replace the following:

  - `PROJECT_ID` : the ID of the project that contains the table.
  - `DATASET` : the name of the dataset that contains the table.
  - `TABLE` : the name of the table.
  - `FIELD_NAME` : the name of the new column.
  - `DATA_TYPE` : the column's data type.
  - `DEFAULT_EXPRESSION` : the default value expression for the column.

- If you already added the column by resubmitting the request without `defaultValueExpression` , run only the `ALTER COLUMN ... SET DEFAULT` and `UPDATE` statements from the preceding example.

### Updating an existing identity column's attributes is not supported

**Error message**

```
Provided Schema does not match Table PROJECT_ID:DATASET.TABLE. Updating an existing identity column's attributes is not supported. Field FIELD_NAME already has identity column info.
```

#### Diagnosis

Your request attempts to modify the attributes of an existing identity column through a schema update or API patch.

#### Resolution

Identity column properties can't be modified in place after creation. Keep the existing identity column definition unchanged in your schema update payload, or create a new table with the updated identity column configuration and copy or load the data into the new table. For instructions, see [Modifying table schemas](https://docs.cloud.google.com/bigquery/docs/managing-table-schemas) .

### Incompatible field change within RECORD column

**Error message**

```
Provided Schema does not match Table PROJECT_ID:DATASET.TABLE. Incompatible field change within RECORD column
```

#### Diagnosis

Your `ALTER TABLE ... ALTER COLUMN ... SET DATA TYPE` statement specifies a `STRUCT` type that isn't compatible with the column's existing type. For example, the new type adds or removes subfields, changes a subfield to an unsupported type, or narrows a subfield's type parameters.

#### Resolution

Compare the `STRUCT` type in your `ALTER TABLE` statement with the column's existing schema, and then do one of the following:

- Keep the same subfields in the same order, and change subfield types only in ways that are supported for [column data type changes](https://docs.cloud.google.com/bigquery/docs/managing-table-schemas#change_a_columns_data_type) .
- DDL can't add nested subfields to an existing `RECORD` column. Instead, update the schema by using a JSON schema file with `bq update` or the `tables.patch` method. For more information, see [Add a nested column to a `RECORD` column](https://docs.cloud.google.com/bigquery/docs/managing-table-schemas#add_a_nested_column_to_a_record_column) .
- To remove or restructure nested subfields, see [Modify nested column types](https://docs.cloud.google.com/bigquery/docs/managing-table-schemas#modify_nested_column_types) .

### Maximum limit on diverging physical schemas reached

**Error message**

```
Provided Schema does not match Table PROJECT_ID:DATASET.TABLE. Maximum limit on diverging physical schemas reached.
```

#### Diagnosis

Certain table schema modifications, such as dropping or renaming columns, can cause tables to have identical logical schemas in the API while having different underlying physical schema representations. When you copy data into a destination table across too many diverging physical schema versions, the table copy job can fail with this error. For more information, see [Limitations on copying tables](https://docs.cloud.google.com/bigquery/docs/managing-tables#limitations_on_copying_tables) .

#### Resolution

Use the [`CREATE TABLE LIKE` DDL statement](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_table_like) to recreate the destination table so that its physical schema representation matches the source table's schema, and then copy or insert the data:

```
CREATE OR REPLACE TABLE `PROJECT_ID.DATASET.DESTINATION_TABLE`
LIKE `PROJECT_ID.DATASET.SOURCE_TABLE`;

INSERT INTO `PROJECT_ID.DATASET.DESTINATION_TABLE`
SELECT * FROM `PROJECT_ID.DATASET.SOURCE_TABLE`;
```

Replace the following:

- `PROJECT_ID` : the ID of the project that contains the tables.
- `DATASET` : the name of the dataset that contains the tables.
- `DESTINATION_TABLE` : the name of the destination table to recreate.
- `SOURCE_TABLE` : the name of the source table.

## Troubleshoot schema, file, and routine nesting limit errors

BigQuery enforces a maximum nesting depth of 15 levels for `STRUCT` ( `RECORD` ) columns, structured load files, and nested routine argument and return types. Exceeding this 15-level limit returns an HTTP `400 Bad Request` error with one of the following messages (where `MAX_DEPTH` and `MAX_LEVEL` are `15` ). For errors caused by exceeding the 16-level nesting limit on logical views or persistent user-defined functions (UDFs), see [Too many nested views or persistent user-defined functions](https://docs.cloud.google.com/bigquery/docs/troubleshoot-queries#ts-nested-views-udfs) .

**Error messages**

- `Schema nested too deeply.`
- `Schema nested too deeply for field `` FIELD_NAME `` , maximum allowed depth is `` MAX_DEPTH `` .`
- `Field ' `` FIELD_NAME `` ' is nested too deeply. It has definition level `` LEVEL `` while maximum allowed definition level is `` MAX_LEVEL `` .`
- `Schema nested too deeply, at least `` LEVEL `` compared to the maximum allowed level of 15.`
- `Routine `` TYPE_DESCRIPTION `` nested too deeply; max allowed depth: `` MAX_DEPTH`

### Diagnosis

Columns of type `STRUCT` ( `RECORD` ) can contain nested `RECORD` fields up to a maximum depth of [15 levels](https://docs.cloud.google.com/bigquery/docs/nested-repeated#limitations) , regardless of whether the fields are scalar ( `NULLABLE` or `REQUIRED` ) or array-based ( `REPEATED` ). Similarly, JSON, Parquet, and Avro load jobs and external tables enforce the nesting limit when they parse nested structures. For Parquet files, the limit is expressed as a maximum definition level and a maximum repetition level.

In routine errors, `TYPE_DESCRIPTION` identifies the nested type: `argument type` , `return type` , or `return table type` .

### Resolution

This limit can't be increased. To resolve this error, do one of the following:

- **Flatten the schema or routine type definition.** Break deeply nested `STRUCT` or `ARRAY` hierarchies in your table schema or routine argument and return types into separate related tables and join them at query time, or promote deeply nested attributes to higher-level columns.
- **Use the built-in `JSON` data type.** If your data requires more than 15 levels of nesting, store the deeply nested subtrees in a column of type [`JSON`](https://docs.cloud.google.com/bigquery/docs/json-data) (or `STRING` ). A `JSON` column is stored as a single column in the table schema—avoiding the 15-level `RECORD` schema limit—while still allowing you to extract deeply nested paths at query time by using JSON field access operators and functions.
- **Preprocess input files before loading.** If the error occurs during a load job from JSON, Parquet, or Avro files in Cloud Storage, add an upstream preprocessing step to flatten or serialize structures deeper than 15 levels before loading them into BigQuery.
