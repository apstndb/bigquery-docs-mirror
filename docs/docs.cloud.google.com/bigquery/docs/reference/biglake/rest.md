The BigLake API provides access to BigLake Metastore, a serverless, fully managed, and highly available metastore for open-source data that can be used for querying Apache Iceberg tables in BigQuery.

  - [REST Resource: v1alpha1.projects.locations.catalogs](#v1alpha1.projects.locations.catalogs)
  - [REST Resource: v1alpha1.projects.locations.catalogs.databases](#v1alpha1.projects.locations.catalogs.databases)
  - [REST Resource: v1alpha1.projects.locations.catalogs.databases.locks](#v1alpha1.projects.locations.catalogs.databases.locks)
  - [REST Resource: v1alpha1.projects.locations.catalogs.databases.tables](#v1alpha1.projects.locations.catalogs.databases.tables)
  - [REST Resource: v1.projects.locations.catalogs](#v1.projects.locations.catalogs)
  - [REST Resource: v1.projects.locations.catalogs.databases](#v1.projects.locations.catalogs.databases)
  - [REST Resource: v1.projects.locations.catalogs.databases.tables](#v1.projects.locations.catalogs.databases.tables)

## Service: biglake.googleapis.com

To call this service, we recommend that you use the Google-provided [client libraries](https://cloud.google.com/apis/docs/client-libraries-explained) . If your application needs to use your own libraries to call this service, use the following information when you make the API requests.

### Discovery document

A [Discovery Document](https://developers.google.com/discovery/v1/reference/apis) is a machine-readable specification for describing and consuming REST APIs. It is used to build client libraries, IDE plugins, and other tools that interact with Google APIs. One service may provide multiple discovery documents. This service provides the following discovery documents:

  - <https://biglake.googleapis.com/$discovery/rest?version=v1>
  - <https://biglake.googleapis.com/$discovery/rest?version=v1alpha1>

### Service endpoint

A [service endpoint](https://cloud.google.com/apis/design/glossary#api_service_endpoint) is a base URL that specifies the network address of an API service. One service might have multiple service endpoints. This service has the following service endpoint and all URIs below are relative to this service endpoint:

  - `  https://biglake.googleapis.com  `

## REST Resource: [v1alpha1.projects.locations.catalogs](/bigquery/docs/reference/biglake/rest/v1alpha1/projects.locations.catalogs)

Methods

`  create  `

`  POST /v1alpha1/{parent=projects/*/locations/*}/catalogs  `  
Creates a new catalog.

`  delete  `

`  DELETE /v1alpha1/{name=projects/*/locations/*/catalogs/*}  `  
Deletes an existing catalog specified by the catalog ID.

`  get  `

`  GET /v1alpha1/{name=projects/*/locations/*/catalogs/*}  `  
Gets the catalog specified by the resource name.

`  list  `

`  GET /v1alpha1/{parent=projects/*/locations/*}/catalogs  `  
List all catalogs in a specified project.

## REST Resource: [v1alpha1.projects.locations.catalogs.databases](/bigquery/docs/reference/biglake/rest/v1alpha1/projects.locations.catalogs.databases)

Methods

`  create  `

`  POST /v1alpha1/{parent=projects/*/locations/*/catalogs/*}/databases  `  
Creates a new database.

`  delete  `

`  DELETE /v1alpha1/{name=projects/*/locations/*/catalogs/*/databases/*}  `  
Deletes an existing database specified by the database ID.

`  get  `

`  GET /v1alpha1/{name=projects/*/locations/*/catalogs/*/databases/*}  `  
Gets the database specified by the resource name.

`  list  `

`  GET /v1alpha1/{parent=projects/*/locations/*/catalogs/*}/databases  `  
List all databases in a specified catalog.

`  patch  `

`  PATCH /v1alpha1/{database.name=projects/*/locations/*/catalogs/*/databases/*}  `  
Updates an existing database specified by the database ID.

## REST Resource: [v1alpha1.projects.locations.catalogs.databases.locks](/bigquery/docs/reference/biglake/rest/v1alpha1/projects.locations.catalogs.databases.locks)

Methods

`  check  `

`  POST /v1alpha1/{name=projects/*/locations/*/catalogs/*/databases/*/locks/*}:check  `  
Checks the state of a lock specified by the lock ID.

`  create  `

`  POST /v1alpha1/{parent=projects/*/locations/*/catalogs/*/databases/*}/locks  `  
Creates a new lock.

`  delete  `

`  DELETE /v1alpha1/{name=projects/*/locations/*/catalogs/*/databases/*/locks/*}  `  
Deletes an existing lock specified by the lock ID.

`  list  `

`  GET /v1alpha1/{parent=projects/*/locations/*/catalogs/*/databases/*}/locks  `  
List all locks in a specified database.

## REST Resource: [v1alpha1.projects.locations.catalogs.databases.tables](/bigquery/docs/reference/biglake/rest/v1alpha1/projects.locations.catalogs.databases.tables)

Methods

`  create  `

`  POST /v1alpha1/{parent=projects/*/locations/*/catalogs/*/databases/*}/tables  `  
Creates a new table.

`  delete  `

`  DELETE /v1alpha1/{name=projects/*/locations/*/catalogs/*/databases/*/tables/*}  `  
Deletes an existing table specified by the table ID.

`  get  `

`  GET /v1alpha1/{name=projects/*/locations/*/catalogs/*/databases/*/tables/*}  `  
Gets the table specified by the resource name.

`  list  `

`  GET /v1alpha1/{parent=projects/*/locations/*/catalogs/*/databases/*}/tables  `  
List all tables in a specified database.

`  patch  `

`  PATCH /v1alpha1/{table.name=projects/*/locations/*/catalogs/*/databases/*/tables/*}  `  
Updates an existing table specified by the table ID.

`  rename  `

`  POST /v1alpha1/{name=projects/*/locations/*/catalogs/*/databases/*/tables/*}:rename  `  
Renames an existing table specified by the table ID.

## REST Resource: [v1.projects.locations.catalogs](/bigquery/docs/reference/biglake/rest/v1/projects.locations.catalogs)

Methods

`  create  `

`  POST /v1/{parent=projects/*/locations/*}/catalogs  `  
Creates a new catalog.

`  delete  `

`  DELETE /v1/{name=projects/*/locations/*/catalogs/*}  `  
Deletes an existing catalog specified by the catalog ID.

`  get  `

`  GET /v1/{name=projects/*/locations/*/catalogs/*}  `  
Gets the catalog specified by the resource name.

`  list  `

`  GET /v1/{parent=projects/*/locations/*}/catalogs  `  
List all catalogs in a specified project.

## REST Resource: [v1.projects.locations.catalogs.databases](/bigquery/docs/reference/biglake/rest/v1/projects.locations.catalogs.databases)

Methods

`  create  `

`  POST /v1/{parent=projects/*/locations/*/catalogs/*}/databases  `  
Creates a new database.

`  delete  `

`  DELETE /v1/{name=projects/*/locations/*/catalogs/*/databases/*}  `  
Deletes an existing database specified by the database ID.

`  get  `

`  GET /v1/{name=projects/*/locations/*/catalogs/*/databases/*}  `  
Gets the database specified by the resource name.

`  list  `

`  GET /v1/{parent=projects/*/locations/*/catalogs/*}/databases  `  
List all databases in a specified catalog.

`  patch  `

`  PATCH /v1/{database.name=projects/*/locations/*/catalogs/*/databases/*}  `  
Updates an existing database specified by the database ID.

## REST Resource: [v1.projects.locations.catalogs.databases.tables](/bigquery/docs/reference/biglake/rest/v1/projects.locations.catalogs.databases.tables)

Methods

`  create  `

`  POST /v1/{parent=projects/*/locations/*/catalogs/*/databases/*}/tables  `  
Creates a new table.

`  delete  `

`  DELETE /v1/{name=projects/*/locations/*/catalogs/*/databases/*/tables/*}  `  
Deletes an existing table specified by the table ID.

`  get  `

`  GET /v1/{name=projects/*/locations/*/catalogs/*/databases/*/tables/*}  `  
Gets the table specified by the resource name.

`  list  `

`  GET /v1/{parent=projects/*/locations/*/catalogs/*/databases/*}/tables  `  
List all tables in a specified database.

`  patch  `

`  PATCH /v1/{table.name=projects/*/locations/*/catalogs/*/databases/*/tables/*}  `  
Updates an existing table specified by the table ID.

`  rename  `

`  POST /v1/{name=projects/*/locations/*/catalogs/*/databases/*/tables/*}:rename  `  
Renames an existing table specified by the table ID.
