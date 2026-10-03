---
name: documents/docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc
uri: https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc
title: BigQuery Connection API
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

Allows users to manage BigQuery connections to external data sources.

## Service: bigqueryconnection.googleapis.com

The Service name `bigqueryconnection.googleapis.com` is needed to create RPC client stubs.

## [`google.cloud.bigquery.connection.v1.ConnectionService`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ConnectionService)

| Methods                                                                                                                                                                                                           |                                                                  |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------|
| [`CreateConnection`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ConnectionService.CreateConnection)     | Creates a new connection.                                        |
| [`DeleteConnection`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ConnectionService.DeleteConnection)     | Deletes connection and associated credential.                    |
| [`GetConnection`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ConnectionService.GetConnection)           | Returns specified connection.                                    |
| [`GetIamPolicy`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ConnectionService.GetIamPolicy)             | Gets the access control policy for a resource.                   |
| [`ListConnections`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ConnectionService.ListConnections)       | Returns a list of connections in the given project.              |
| [`SetIamPolicy`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ConnectionService.SetIamPolicy)             | Sets the access control policy on the specified resource.        |
| [`TestIamPermissions`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ConnectionService.TestIamPermissions) | Returns permissions that a caller has on the specified resource. |
| [`UpdateConnection`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1#google.cloud.bigquery.connection.v1.ConnectionService.UpdateConnection)     | Updates the specified connection.                                |

## [`google.cloud.bigquery.connection.v1beta1.ConnectionService`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.ConnectionService)

| Methods                                                                                                                                                                                                                                     |                                                                  |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------|
| [`CreateConnection`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.ConnectionService.CreateConnection)                     | Creates a new connection.                                        |
| [`DeleteConnection`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.ConnectionService.DeleteConnection)                     | Deletes connection and associated credential.                    |
| [`GetConnection`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.ConnectionService.GetConnection)                           | Returns specified connection.                                    |
| [`GetIamPolicy`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.ConnectionService.GetIamPolicy)                             | Gets the access control policy for a resource.                   |
| [`ListConnections`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.ConnectionService.ListConnections)                       | Returns a list of connections in the given project.              |
| [`SetIamPolicy`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.ConnectionService.SetIamPolicy)                             | Sets the access control policy on the specified resource.        |
| [`TestIamPermissions`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.ConnectionService.TestIamPermissions)                 | Returns permissions that a caller has on the specified resource. |
| [`UpdateConnection`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.ConnectionService.UpdateConnection)                     | Updates the specified connection.                                |
| [`UpdateConnectionCredential`](https://docs.cloud.google.com/bigquery/docs/reference/bigqueryconnection/rpc/google.cloud.bigquery.connection.v1beta1#google.cloud.bigquery.connection.v1beta1.ConnectionService.UpdateConnectionCredential) | Sets the credential for the specified connection.                |
