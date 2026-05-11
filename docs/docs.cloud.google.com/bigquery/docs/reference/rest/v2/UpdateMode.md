---
name: documents/docs.cloud.google.com/bigquery/docs/reference/rest/v2/UpdateMode
uri: https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/UpdateMode
title: UpdateMode
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

UpdateMode specifies which dataset fields is updated.

Enums

`UPDATE_MODE_UNSPECIFIED`

The default value. Default to the UPDATE\_FULL.

`UPDATE_METADATA`

Includes metadata information for the dataset, such as friendlyName, description, labels, etc.

`UPDATE_ACL`

Includes ACL information for the dataset, which defines dataset access for one or more entities.

`UPDATE_FULL`

Includes both dataset metadata and ACL information.
