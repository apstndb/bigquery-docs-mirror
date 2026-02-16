# Specify ObjectRef columns in table schemas

**Preview**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

**Note:** To provide feedback or request support for this feature, send an email to <bq-objectref-feedback@google.com>

This document describes how to define a BigQuery standard table schema with columns that can store `  ObjectRef  ` values.

`  ObjectRef  ` values provide metadata and connection information for objects in Cloud Storage. Use `  ObjectRef  ` values when you need to integrate unstructured data into a standard table. For example, in a products table, you could store product images in the same row with the rest of the product information by adding a column containing `  ObjectRef  ` values. You can store `  ObjectRef  ` values in `  STRUCT  ` columns that use the [`  ObjectRef  ` format](/bigquery/docs/reference/standard-sql/objectref_functions#objectref) , which is `  STRUCT<uri STRING, version STRING, authorizer STRING, details JSON>  ` .

For more information about working with multimodal data, see [Analyze multimodal data](/bigquery/docs/analyze-multimodal-data) . For a tutorial that shows how to work with `  ObjectRef  ` data, see [Analyze multimodal data with SQL](/bigquery/docs/multimodal-data-sql-tutorial) . For information about working with multimodal data in Python, see [Analyze multimodal data in Python with BigQuery DataFrames](/bigquery/docs/multimodal-data-dataframes-tutorial) .

**Note:** The examples in this document use the [`  CREATE OR REPLACE TABLE  ` statement](/bigquery/docs/reference/standard-sql/data-definition-language#create_table_statement) to create and populate an `  ObjectRef  ` column in a single operation, but you can also use the [`  ALTER TABLE ADD COLUMN  ` statement](/bigquery/docs/reference/standard-sql/data-definition-language#alter_table_add_column_statement) to add a `  STRUCT  ` column to an existing table and then use the [`  UPDATE  ` statement](/bigquery/docs/reference/standard-sql/dml-syntax#update_statement) to populate that column in a separate operation.

## Prerequisites

To populate and update `  ObjectRef  ` values in a standard table, the table must have a `  STRING  ` column that contains URI information for the related Cloud Storage objects.

You must have a Cloud Storage bucket that contains the same objects that are identified in the URI data of the target standard table. If you want to [maintain `  ObjectRef  ` values in a standard table](#maintaining_objectref_values) by using an [object table](/bigquery/docs/object-table-introduction) , you must also have an object table that represents the objects in that bucket.

## Maintaining `     ObjectRef    ` values

You can use an object table to populate and update `  ObjectRef  ` values in a standard table. If you are on the allowlist for the preview, any object tables you create have a `  ref  ` column that contains an `  ObjectRef  ` value for the given object. You can use the object URI to join the standard table to the object table in order to populate and update `  ObjectRef  ` values. We recommend this approach for scalability, because it avoids the need to retrieve object metadata from Cloud Storage.

If you don't want to create an object table, you can use the [`  OBJ.FETCH_METADATA  `](/bigquery/docs/reference/standard-sql/objectref_functions#objfetch_metadata) and [`  OBJ.MAKE_REF  `](/bigquery/docs/reference/standard-sql/objectref_functions#objmake_ref) functions to populate and update `  ObjectRef  ` values by fetching object metadata directly from Cloud Storage. This approach might be less scalable, because it requires the retrieval of object metadata from Cloud Storage.

## Create an `     ObjectRef    ` column

To create and populate an `  ObjectRef  ` column in a standard table, select one of the following options:

### Object table

Create and populate an `  ObjectRef  ` column based on data from an object table `  ref  ` column:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    CREATE OR REPLACE TABLE PROJECT_ID.DATASET_ID.TABLE_NAME
    AS
    SELECT TABLE_NAME.*, OBJECT_TABLE.ref AS objectrefcolumn
    FROM DATASET_ID.TABLE_NAME
    INNER JOIN DATASET_ID.OBJECT_TABLE
    ON OBJECT_TABLE.uri = TABLE_NAME.uri;
    ```
    
    Replace the following:
    
      - `  PROJECT_ID  ` : your project ID. You can skip this argument if you are creating the table in your current project.
      - `  DATASET_ID  ` : the ID of the dataset that you are creating.
      - `  TABLE_NAME  ` : the name of the standard table that you are recreating.
      - `  OBJECT_TABLE  ` : the name of the object table that contains the object data that you want to integrate into the standard table.

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

### SQL functions

Create and populate an `  ObjectRef  ` column based on output from the `  OBJ.FETCH_METADATA  ` and `  OBJ.MAKE_REF  ` functions:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    CREATE OR REPLACE TABLE PROJECT_ID.DATASET_ID.TABLE_NAME
    AS
    SELECT TABLE_NAME.*,
    OBJ.FETCH_METADATA(OBJ.MAKE_REF(uri, 'CONNECTION_ID')) AS objectrefcolumn
    FROM DATASET_ID.TABLE_NAME;
    ```
    
    Replace the following:
    
      - `  PROJECT_ID  ` : your project ID. You can skip this argument if you are creating the table in your current project.
    
      - `  DATASET_ID  ` : the ID of the dataset that you are creating.
    
      - `  TABLE_NAME  ` : the name of the standard table that you are recreating.
    
      - `  CONNECTION_ID  ` : A `  STRING  ` value that contains a [Cloud resource connection](/bigquery/docs/create-cloud-resource-connection) that the service can use to access the objects in Cloud Storage, in the format `  location.connection_id  ` . For example, `  us-west1.myconnection  ` . You can get the connection ID by [viewing the connection details](/bigquery/docs/working-with-connections#view-connections) in the Google Cloud console and copying the value in the last section of the fully qualified connection ID that is shown in **Connection ID** . For example, `  projects/myproject/locations/connection_location/connections/ myconnection  ` .
        
        You must grant the Storage Object User ( `  roles/storage.objectUser  ` ) role to the connection's service account on any Cloud Storage bucket where you are using it to access objects.
        
        The connection must be in the same project and region as the query where you are calling the function.

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

## Create an `     ARRAY<ObjectRef>    ` column

You can create an `  ARRAY<STRUCT<uri STRING, version STRING, authorizer STRING, details JSON>>  ` column to contain arrays of `  ObjectRef  ` values. For example, you could chunk a video into separate images, and then store these images as an array of `  ObjectRef  ` values.

You can use the [`  ARRAY_AGG  ` function](/bigquery/docs/reference/standard-sql/aggregate_functions#array_agg) to aggregate arrays of `  ObjectRef  ` values, including using the `  ORDER BY  ` clause preserve object order if necessary. You can use the [`  UNNEST  ` operator](/bigquery/docs/reference/standard-sql/query-syntax#unnest_operator) to parse an array of `  ObjectRef  ` values into individual `  ObjectRef  ` values, including using the `  WITH OFFSET  ` clause to preserve object order if necessary. You can use object metadata, like the URI path and object filename, to map `  ObjectRef  ` values that represent object chunks to an `  ObjectRef  ` value that represents the original object.

To see an example of how to work with arrays of `  ObjectRef  ` values, see the [Process ordered multimodal data using `  ARRAY<ObjectRef>  ` values](/bigquery/docs/multimodal-data-sql-tutorial#process_ordered_multimodal_data_using_arrays_of_objectref_values) section of the [Analyze multimodal data with SQL](/bigquery/docs/multimodal-data-sql-tutorial) tutorial.

## Update an `     ObjectRef    ` column

To update an `  ObjectRef  ` column in a standard table, select one of the following options:

### Object table

Update an `  ObjectRef  ` column by using data from an object table `  ref  ` column:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    UPDATE PROJECT_ID.DATASET_ID.TABLE_NAME
    SET objectrefcolumn = (SELECT ref FROM DATASET_ID.OBJECT_TABLE WHERE OBJECT_TABLE.uri = TABLE_NAME.uri)
    WHERE uri != "";
    ```
    
    Replace the following:
    
      - `  PROJECT_ID  ` : your project ID. You can skip this argument if you are creating the table in your current project.
      - `  DATASET_ID  ` : the ID of the dataset that you are creating.
      - `  TABLE_NAME  ` : the name of the standard table that you are recreating.
      - `  OBJECT_TABLE  ` : the name of the object table that contains the same object data as the standard table `  ObjectRef  ` column.

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

### SQL functions

Update an `  ObjectRef  ` column by using output from the `  OBJ.FETCH_METADATA  ` and `  OBJ.MAKE_REF  ` functions:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` text
    UPDATE PROJECT_ID.DATASET_ID.TABLE_NAME
    SET objectrefcolumn = (SELECT OBJ.FETCH_METADATA(OBJ.MAKE_REF(uri, 'CONNECTION_ID')))
    WHERE uri != "";
    ```
    
    Replace the following:
    
      - `  PROJECT_ID  ` : your project ID. You can skip this argument if you are creating the table in your current project.
    
      - `  DATASET_ID  ` : the ID of the dataset that you are creating.
    
      - `  TABLE_NAME  ` : the name of the standard table that you are recreating.
    
      - `  CONNECTION_ID  ` : A `  STRING  ` value that contains a [Cloud resource connection](/bigquery/docs/create-cloud-resource-connection) that the service can use to access the objects in Cloud Storage, in the format `  location.connection_id  ` . For example, `  us-west1.myconnection  ` . You can get the connection ID by [viewing the connection details](/bigquery/docs/working-with-connections#view-connections) in the Google Cloud console and copying the value in the last section of the fully qualified connection ID that is shown in **Connection ID** . For example, `  projects/myproject/locations/connection_location/connections/ myconnection  ` .
        
        You must grant the Storage Object User ( `  roles/storage.objectUser  ` ) role to the connection's service account on any Cloud Storage bucket where you are using it to access objects.
        
        The connection must be in the same project and region as the query where you are calling the function.

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](/bigquery/docs/running-queries#queries) .

## What's next

  - [Analyze multimodal data](/bigquery/docs/analyze-multimodal-data) .
  - [Analyze multimodal data with SQL](/bigquery/docs/multimodal-data-sql-tutorial) .
  - [Analyze multimodal data in Python with BigQuery DataFrames](/bigquery/docs/multimodal-data-dataframes-tutorial) .
