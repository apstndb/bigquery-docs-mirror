# Transfer data into BigLake Iceberg table in BigQuery

**Preview**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

**Note:** To get support or provide feedback for this feature, contact <dts-preview-support@google.com> .

You can use the BigQuery Data Transfer Service to transfer data from external sources, such as Amazon Simple Storage Service (Amazon S3), Azure Blob Storage, or Cloud Storage into BigLake Iceberg table in BigQuery.

## Data sources supported

You can specify BigLake Iceberg table in BigQuery as the destination table type when you set up your transfer configuration for these data sources:

  - [Amazon S3](/bigquery/docs/s3-transfer)
  - [Azure Blob Storage](/bigquery/docs/blob-storage-transfer)
  - [Cloud Storage](/bigquery/docs/cloud-storage-transfer)

## Limitations

Transfers to BigLake Iceberg table in BigQuery are subject to the following limitations:

  - **Append-only:** Data is only appended to the destination table. Overwriting, updating, or deleting existing data is not supported.
  - **No partitioning:** The destination BigLake Iceberg table in BigQuery cannot be partitioned.
  - **No backfills:** Transfers do not support [backfills](/bigquery/docs/samples/bigquerydatatransfer-schedule-backfill) .

## Pricing

For information on BigQuery Data Transfer Service pricing, see the [Pricing](https://cloud.google.com/bigquery/pricing#data-transfer-service-pricing) page.

After data is transferred to BigLake Iceberg table in BigQuery, standard storage and query [pricing](/bigquery/docs/iceberg-tables#pricing) applies.
