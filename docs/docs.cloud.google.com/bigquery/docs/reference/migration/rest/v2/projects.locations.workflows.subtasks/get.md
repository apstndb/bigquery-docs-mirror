---
name: documents/docs.cloud.google.com/bigquery/docs/reference/migration/rest/v2/projects.locations.workflows.subtasks/get
uri: https://docs.cloud.google.com/bigquery/docs/reference/migration/rest/v2/projects.locations.workflows.subtasks/get
title: 'Method: projects.locations.workflows.subtasks.get'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

  - [HTTP request](https://docs.cloud.google.com/bigquery/docs/reference/migration/rest/v2/projects.locations.workflows.subtasks/get#body.HTTP_TEMPLATE)
  - [Path parameters](https://docs.cloud.google.com/bigquery/docs/reference/migration/rest/v2/projects.locations.workflows.subtasks/get#body.PATH_PARAMETERS)
  - [Query parameters](https://docs.cloud.google.com/bigquery/docs/reference/migration/rest/v2/projects.locations.workflows.subtasks/get#body.QUERY_PARAMETERS)
  - [Request body](https://docs.cloud.google.com/bigquery/docs/reference/migration/rest/v2/projects.locations.workflows.subtasks/get#body.request_body)
  - [Response body](https://docs.cloud.google.com/bigquery/docs/reference/migration/rest/v2/projects.locations.workflows.subtasks/get#body.response_body)
  - [Authorization scopes](https://docs.cloud.google.com/bigquery/docs/reference/migration/rest/v2/projects.locations.workflows.subtasks/get#body.aspect)
  - [IAM Permissions](https://docs.cloud.google.com/bigquery/docs/reference/migration/rest/v2/projects.locations.workflows.subtasks/get#body.aspect_1)
  - [Try it\!](https://docs.cloud.google.com/bigquery/docs/reference/migration/rest/v2/projects.locations.workflows.subtasks/get#try-it)

Gets a previously created migration subtask.

### HTTP request

Choose an endpoint:

global asia-northeast1 asia-south1 asia-south2 asia-southeast1 australia-southeast1 europe-west1 europe-west2 europe-west3 europe-west4 europe-west6 europe-west8 europe-west9 me-central2 northamerica-northeast1 northamerica-northeast2 southamerica-east1 us-central1 us-central2 us-east1 us-east4 us-east5 us-east7 us-south1 us-west1 us-west2 us-west3 us-west4 us-west8

  
`GET https://bigquerymigration.googleapis.com/v2/{name=projects/*/locations/*/workflows/*/subtasks/*}`

The URLs use [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`name`

`string`

Required. The unique identifier for the migration subtask. Example: `projects/123/locations/us/workflows/1234/subtasks/543`

### Query parameters

Parameters

`readMask`

` string ( FieldMask  ` format)

Optional. The list of fields to be retrieved.

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  MigrationSubtask  ` .

### Authorization scopes

Requires the following OAuth scope:

  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .

### IAM Permissions

Requires the following [IAM](https://cloud.google.com/iam/docs) permission on the `name` resource:

  - `bigquerymigration.subtasks.get`

For more information, see the [IAM documentation](https://cloud.google.com/iam/docs) .
