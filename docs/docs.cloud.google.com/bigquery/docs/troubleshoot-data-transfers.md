---
name: documents/docs.cloud.google.com/bigquery/docs/troubleshoot-data-transfers
uri: https://docs.cloud.google.com/bigquery/docs/troubleshoot-data-transfers
title: Troubleshoot data transfers
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# Troubleshoot data transfers

This page explains how to troubleshoot issues when you transfer or load data into BigQuery. You can resolve common errors related to BigQuery Data Transfer Service, network connections across Google Cloud, Amazon Web Services (AWS), Cloud SQL, and Virtual Private Cloud (VPC) networks, as well as CSV data load jobs from Cloud Storage.

## Troubleshoot transfer configurations

For information about resolving issues with BigQuery Data Transfer Service, see [Troubleshoot transfer configurations](https://docs.cloud.google.com/bigquery/docs/transfer-troubleshooting) .

If you set up or run transfers transfers from external or partner data sources, see [Troubleshoot third-party transfer setup](https://docs.cloud.google.com/bigquery/docs/third-party-transfer#troubleshoot_third_party_transfer_setup) .

## Diagnose jobs with `INFORMATION_SCHEMA` views

You can query the [`INFORMATION_SCHEMA.JOBS`](https://docs.cloud.google.com/bigquery/docs/information-schema-jobs) view to diagnose failed or slow load jobs and transfer queries in near real time. When a load job or transfer query fails, inspect the `error_result` and `errors` columns to identify the root cause, such as schema mismatches, quota limits, or permission errors.

The following example queries `INFORMATION_SCHEMA.JOBS` to retrieve error details for failed load jobs over the past 24 hours:

    SELECT
      job_id,
      creation_time,
      user_email,
      error_result.reason AS error_reason,
      error_result.message AS error_message,
      errors
    FROM
      `region-REGION`.INFORMATION_SCHEMA.JOBS
    WHERE
      job_type = 'LOAD'
      AND state = 'DONE'
      AND error_result IS NOT NULL
      AND creation_time > TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 1 DAY)
    ORDER BY
      creation_time DESC;

Replace `<var>REGION</var>` with the dataset region name, such as `us` or `europe-west1` .

## Troubleshoot transfer network connections

When you transfer data from external cloud providers or private database instances, network routing or firewall rules can block connectivity. Use the following sections to troubleshoot VPN attachments and private network connections.

### AWS-Google Cloud VPN and network attachments

If you're having issues setting up your network attachment, do the following:

  - Ensure that the VPN connections are up and running in both the AWS console and the Google Cloud console.
  - Check the VPN logs for errors or dropped packets.
  - Verify that the routing tables in both AWS and Google Cloud are correctly configured.
  - Ensure that the necessary ports are open in both the AWS security groups and the Google Cloud firewall rules.

For more information about configuring VPN attachments, see [Create an AWS-Google Cloud VPN and network attachment](https://docs.cloud.google.com/bigquery/docs/aws-vpn-network-attachment) .

### Cloud SQL instance access

If you're having issues setting up your network configuration, do the following:

  - Ensure that VPC peering is established and that routes are correctly configured.
  - Verify that the firewall rules allow for traffic on the required ports.
  - Check the Cloud SQL proxy logs for errors and ensure that it's running correctly.
  - Ensure that the network attachment is correctly configured and connected.

For more information about configuring private database access, see [Connect to a Cloud SQL instance](https://docs.cloud.google.com/bigquery/docs/cloud-sql-instance-access) .

## Troubleshoot load CSV files

When you load CSV data from Cloud Storage into BigQuery, jobs can fail due to formatting errors, file size limits, or schema auto-detection issues. Use the following sections to resolve common CSV loading errors.

### Troubleshoot parsing errors

If there's a problem parsing your CSV files, then the load job's [`errors` resource](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/ErrorProto) is populated with the error details.

Generally, these errors identify the start of the problematic line with a byte offset. For uncompressed files, you can use `gcloud storage` with the `--recursive` argument to access the relevant line.

For example, you run the [`bq load` command](https://docs.cloud.google.com/bigquery/docs/reference/bq-cli-reference#bq_load) and receive an error:

```sh
bq load
    --skip_leading_rows=1 \
    --source_format=CSV \
    mydataset.mytable \
    gs://my-bucket/mytable.csv \
    'Number:INTEGER,Name:STRING,TookOffice:STRING,LeftOffice:STRING,Party:STRING'
```

The error in the output is similar to the following:

```sh
Waiting on bqjob_r5268069f5f49c9bf_0000018632e903d7_1 ... (0s)
Current status: DONE
BigQuery error in load operation: Error processing job
'myproject:bqjob_r5268069f5f49c9bf_0000018632e903d7_1': Error while reading
data, error message: Error detected while parsing row starting at position: 1405.
Error: Data between close quote character (") and field separator.
File: gs://my-bucket/mytable.csv
Failure details:
- gs://my-bucket/mytable.csv: Error while reading data,
error message: Error detected while parsing row starting at
position: 1405. Error: Data between close quote character (") and
field separator. File: gs://my-bucket/mytable.csv
- Error while reading data, error message: CSV processing encountered
too many errors, giving up. Rows: 22; errors: 1; max bad: 0; error
percent: 0
```

Based on the preceding error, there's a format error in the file. To view the file's content, run the [`gcloud storage cat` command](https://docs.cloud.google.com/sdk/gcloud/reference/storage/cat) :

```sh
gcloud storage cat 1405-1505 gs://my-bucket/mytable.csv --recursive
```

The output is similar to the following:

```sh
16,Abraham Lincoln,"March 4, 1861","April 15, "1865,Republican
18,Ulysses S. Grant,"March 4, 1869",
...
```

Based on the output of the file, the problem is a misplaced quotation mark in `"April 15, "1865` .

#### Compressed CSV files

Debugging parsing errors is more challenging for compressed CSV files, because the reported byte offset refers to the location in the *uncompressed* file. The following [`gcloud storage cat` command](https://docs.cloud.google.com/sdk/gcloud/reference/storage/cat) streams the file from Cloud Storage, decompresses the file, identifies the appropriate byte offset, and prints the line with the format error:

```sh
gcloud storage cat gs://my-bucket/mytable.csv.gz | gunzip - | tail -c +1406 | head -n 1
```

The output is similar to the following:

```sh
16,Abraham Lincoln,"March 4, 1861","April 15, "1865,Republican
```

<span id="ts-load-csv-files-quota"></span>

### Troubleshoot quota errors

Use the information in this section to troubleshoot quota or limit errors related to loading CSV files into BigQuery.

If you load a large CSV file using the `bq load` command with the [`--allow_quoted_newlines` flag](https://docs.cloud.google.com/bigquery/docs/reference/bq-cli-reference#flags_and_arguments_9) , you might encounter this error.

**Error message**

    Input CSV files are not splittable and at least one of the files is larger than
    the maximum allowed size. Size is: ...

#### Resolution

To resolve this quota error, do the following:

  - Set the `--allow_quoted_newlines` flag to `false` .
  - Split the CSV file into smaller chunks that are each less than 4 GB.

For more information about limits that apply when you load data into BigQuery, see [Load jobs](https://docs.cloud.google.com/bigquery/quotas#load_jobs) .

### Troubleshoot schema auto-detection

When auto-detecting schema for CSV files, you might encounter the following error:

**Error:** `Error while reading data, error message: CSV processing encountered too many errors, giving up.`

This error can occur when your CSV file has a header row with string values, and BigQuery didn't detect it as a header. You can use the `--skip_leading_rows` option to skip the header row.
