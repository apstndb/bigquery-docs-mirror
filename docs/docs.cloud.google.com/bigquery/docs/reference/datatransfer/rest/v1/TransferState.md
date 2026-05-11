---
name: documents/docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/TransferState
uri: https://docs.cloud.google.com/bigquery/docs/reference/datatransfer/rest/v1/TransferState
title: TransferState
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

Represents data transfer run state.

Enums

`TRANSFER_STATE_UNSPECIFIED`

State placeholder (0).

`PENDING`

Data transfer is scheduled and is waiting to be picked up by data transfer backend (2).

`RUNNING`

Data transfer is in progress (3).

`SUCCEEDED`

Data transfer completed successfully (4).

`FAILED`

Data transfer failed (5).

`CANCELLED`

Data transfer is cancelled (6).
