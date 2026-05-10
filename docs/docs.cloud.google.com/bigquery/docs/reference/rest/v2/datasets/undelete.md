---
name: documents/docs.cloud.google.com/bigquery/docs/reference/rest/v2/datasets/undelete
uri: https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/datasets/undelete
title: 'Method: datasets.undelete'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
update_time: "2025-10-17T21:03:18Z"
---

  - [HTTP request](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/datasets/undelete#body.HTTP_TEMPLATE)
  - [Path parameters](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/datasets/undelete#body.PATH_PARAMETERS)
  - [Request body](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/datasets/undelete#body.request_body)
  - [Response body](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/datasets/undelete#body.response_body)
  - [Authorization scopes](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/datasets/undelete#body.aspect)
  - [Try it\!](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/datasets/undelete#try-it)

Undeletes a dataset which is within time travel window based on datasetId. If a time is specified, the dataset version deleted at that time is undeleted, else the last live version is undeleted.

### HTTP request

`POST https://bigquery.googleapis.com/bigquery/v2/projects/{projectId}/datasets/{datasetId}:undelete`

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`projectId`

`string`

Required. Project ID of the dataset to be undeleted

`datasetId`

`string`

Required. Dataset ID of dataset being deleted

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  Dataset  ` .

### Authorization scopes

Requires one of the following OAuth scopes:

  - `https://www.googleapis.com/auth/bigquery`
  - `https://www.googleapis.com/auth/cloud-platform`

For more information, see the [Authentication Overview](https://docs.cloud.google.com/docs/authentication#authorization-gcp) .
