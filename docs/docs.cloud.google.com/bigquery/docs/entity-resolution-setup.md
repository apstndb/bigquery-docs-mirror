---
name: documents/docs.cloud.google.com/bigquery/docs/entity-resolution-setup
uri: https://docs.cloud.google.com/bigquery/docs/entity-resolution-setup
title: Configure and use entity resolution in BigQuery
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# Configure and use entity resolution in BigQuery

[Entity resolution](https://docs.cloud.google.com/bigquery/docs/entity-resolution-intro) in BigQuery lets you match, deduplicate, and augment records across datasets without moving your underlying data. As an end user, you can connect your BigQuery datasets to an identity provider such as LiveRamp or TransUnion and call a remote function to resolve identities in place. As an identity provider, you can configure remote function endpoints and publish your entity resolution services on Google Cloud Marketplace.

## Configure entity resolution for end users

To resolve entities as an end user, you prepare input and output datasets in BigQuery, grant dataset access to your identity provider, and invoke their matching service. For more information about the architecture, see [Entity resolution architecture](https://docs.cloud.google.com/bigquery/docs/entity-resolution-intro#architecture) .

### Before you begin

1.  Contact an identity provider. BigQuery supports entity resolution with [LiveRamp](mailto:LiveRampIdentitySupport@liveramp.com) and [TransUnion](mailto:PDLtucloudappsupport@transunion.com) .
2.  Get the following items from the identity provider:
    - Service account credentials
    - Remote function signature
3.  Create the following datasets in your Google Cloud project:
    - Input dataset
    - Output dataset

### Required roles

To ensure that the identity provider's service account has the necessary permissions to read the input dataset and write to the output dataset, ask your administrator to grant the following IAM roles to the identity provider's service account:

> **Important:** You must grant these roles to the identity provider's service account, *not* to your user account. Failure to grant the roles to the correct principal might result in permission errors.

- [BigQuery Data Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataViewer) ( `roles/bigquery.dataViewer` ) on the input dataset
- [BigQuery Data Editor](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor) ( `roles/bigquery.dataEditor` ) on the output dataset

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

Your administrator might also be able to give the identity provider's service account the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

### Resolve entities with an identity provider

After you create your datasets and grant the required roles, you can configure your tables and run matching jobs with your chosen identity provider. The following table summarizes the integration method and required tables for each supported identity provider:

| Identity provider | Integration method                                            | Required tables in your dataset                                                             | Job invocation                         |
|-------------------|---------------------------------------------------------------|---------------------------------------------------------------------------------------------|----------------------------------------|
| **LiveRamp**      | LiveRamp Embedded Identity                                    | Input table with RampIDs, metadata table                                                    | Email request to LiveRamp support      |
| **TransUnion**    | TruAudience remote function over BigQuery external connection | Input table with entity attributes, metadata table, job status table, matching output table | SQL stored procedure call using `CALL` |

Select an identity provider to view specific setup and job execution instructions:

### LiveRamp

#### LiveRamp prerequisites

Before you configure LiveRamp entity resolution in BigQuery, complete the following prerequisites:

- Configure LiveRamp Embedded Identity in BigQuery. For more information, see [Enabling LiveRamp Embedded Identity in BigQuery](https://docs.liveramp.com/identity/en/liveramp-embedded-identity-in-bigquery.html#enabling-liveramp-embedded-identity-in-bigquery) .
- Coordinate with LiveRamp to enable API credentials that work with Embedded Identity. For more information, see [Authentication](https://docs.liveramp.com/identity/en/liveramp-embedded-identity-in-bigquery.html#id74765) .

#### Set up LiveRamp entity resolution

When you use LiveRamp Embedded Identity for the first time, complete the following setup steps. For subsequent runs, you only need to update your input table and metadata table.

##### Create a LiveRamp input table

Create a table in your input dataset and populate it with the following columns:

- RampIDs
- Target domains
- Target types

For more information about the input table schema, see [Input Table Columns and Descriptions](https://docs.liveramp.com/identity/en/perform-rampid-transcoding-in-bigquery.html#input-table-columns-and-descriptions) .

##### Create a LiveRamp metadata table

To control the execution of LiveRamp Embedded Identity in BigQuery, create a metadata table in your input dataset. Populate the metadata table with the following configuration columns:

- Client IDs
- Execution modes
- Target domains
- Target types

For more information about the metadata table schema, see [Metadata Table Columns and Descriptions](https://docs.liveramp.com/identity/en/perform-rampid-transcoding-in-bigquery.html#metadata-table-columns-and-descriptions) .

#### Grant dataset access to LiveRamp

After you create the required tables, grant LiveRamp access to view and process data in your input dataset. Grant dataset access to the LiveRamp Google Cloud service account. For more information about sharing datasets, see [Share Tables and Datasets with LiveRamp](https://docs.liveramp.com/identity/en/perform-rampid-transcoding-in-bigquery.html#share-tables-and-datasets-with-liveramp-71) .

#### Run a LiveRamp entity resolution job

After you configure your tables and grant dataset access, run an entity resolution job with LiveRamp in BigQuery:

1.  In your input table, confirm that all RampIDs for your domain are present.
2.  Before you run the job, confirm that your metadata table configuration is accurate.
3.  To submit a job processing request, send an email to <LiveRampIdentitySupport@liveramp.com> . In your request, include the project ID, dataset ID, and any applicable table IDs for your input table, metadata table, and output dataset.

LiveRamp typically delivers the matching results to your output dataset within three business days.

#### Get LiveRamp support and billing information

LiveRamp manages technical support and billing for Embedded Identity in BigQuery:

- **Technical support** : contact [LiveRamp Identity Support](mailto:LiveRampIdentitySupport@liveramp.com) for assistance with setup or job execution.
- **Billing** : [LiveRamp](https://cloud.google.com/find-a-partner/partner/liveramp) bills you directly for entity resolution usage.

### TransUnion

#### TransUnion prerequisites

Before you configure TransUnion entity resolution in BigQuery, send an email to [TransUnion Cloud Support](mailto:PDLtucloudappsupport@transunion.com) to sign a service access agreement. In your request, provide the following information:

- Your Google Cloud project ID
- Input data types
- Intended use case
- Estimated data volume

After TransUnion Cloud Support approves your request, they enable the service for your Google Cloud project and share an implementation guide that includes available output schemas.

#### Set up TransUnion entity resolution

When you use the TransUnion TruAudience Identity Resolution and Enrichment service in BigQuery for the first time, complete the following setup steps.

##### Create an external connection

To connect your Google Cloud account to the identity resolution service hosted in the TransUnion Google Cloud account, [create a Cloud resource connection](https://docs.cloud.google.com/bigquery/docs/create-cloud-resource-connection#create-cloud-resource-connection) . When you configure the connection, select **Vertex AI remote models, remote functions and BigLake (Cloud Resource)** as the connection type.

After you create the connection, copy the connection ID and service account ID, and then share these identifiers with the TransUnion customer delivery team.

##### Create a remote function

To pass schema mappings and configuration metadata to the TransUnion service orchestrator endpoint, [create a remote function](https://docs.cloud.google.com/bigquery/docs/remote-functions#create-a-remote-function) . When you create the remote function, specify the connection ID from your external connection and the Cloud Run function endpoint URL that the TransUnion customer delivery team shared with you.

##### Create a TransUnion input table

Create an input table in your input dataset. TransUnion supports the following entity attributes as input columns:

- Name
- Postal address
- Email address
- Phone number
- Date of birth
- IPv4 address
- Device ID

Follow the schema and formatting guidelines in the implementation guide that TransUnion shared with you. If you map each input table to a distinct `config_id` parameter in your metadata table, you can use multiple input tables.

##### Create a TransUnion metadata table

To store the schema mappings and configuration that the identity resolution service requires, create a metadata table in your input dataset. For more information about the metadata schema, see the implementation guide that TransUnion shared with you.

##### Create a job status table

To receive batch processing updates, create a job status table in your dataset. To monitor jobs and trigger downstream processes in your pipeline, query this job status table. The table records the following statuses:

- `RUNNING` : the identity resolution service is processing the batch.
- `COMPLETED` : the service finished processing the batch and wrote the results to the output table.
- `ERROR` : the service encountered an error while processing the batch.

##### Create the service invocation procedure

The `TransUnion_get_identities` stored procedure packages your configuration metadata and invokes the TransUnion Cloud Run function endpoint. To create this stored procedure, run the following SQL statement:

```
-- create service invocation procedure
CREATE OR REPLACE
  PROCEDURE
    `PROJECT_ID.DATASET_ID.TransUnion_get_identities`(metadata_table STRING, config_id STRING)
      begin
        declare sql_query STRING;

declare json_result STRING;
declare base64_result STRING;

SET sql_query =
  '''select to_json_string(array_agg(struct(config_id,key,value))) from `''' || metadata_table
  || '''` where  config_id="''' || config_id || '''" ''';

EXECUTE immediate sql_query INTO json_result;

SET base64_result = (SELECT to_base64(CAST(json_result AS bytes)));

SELECT
  `PROJECT_ID.DATASET_ID.remote_call_TransUnion_er`(
    base64_result);
END;
```

Replace the following:

- `PROJECT_ID` : your Google Cloud project ID.
- `DATASET_ID` : the ID of the dataset where you create the procedure and remote function.

##### Create the matching output table

The matching output table stores the entity resolution results from TransUnion, including match flags, linkage scores, persistent individual IDs, and household IDs. To create the matching output table, run the following SQL statement:

```
-- create output table
CREATE TABLE `PROJECT_ID.DATASET_ID.TransUnion_identity_output`(
  batchid STRING,
  uniqueid STRING,
  ekey STRING,
  hhid STRING,
  collaborationid STRING,
  firstnamematch STRING,
  lastnamematch STRING,
  addressmatches STRING,
  addresslinkagescores STRING,
  phonematches STRING,
  phonelinkagescores STRING,
  emailmatches STRING,
  emaillinkagescores STRING,
  dobmatches STRING,
  doblinkagescore STRING,
  ipmatches STRING,
  iplinkagescore STRING,
  devicematches STRING,
  devicelinkagescore STRING,
  lastprocessed STRING);
```

Replace the following:

- `PROJECT_ID` : your Google Cloud project ID.
- `DATASET_ID` : the ID of the dataset where you create the matching output table.

##### Configure schema mapping metadata

To map your input schema to the TransUnion application schema, follow the instructions in the implementation guide that TransUnion shared with you. This metadata also configures how the service generates collaboration IDs, which are shareable, non-persistent identifiers that you can use in [data clean rooms](https://docs.cloud.google.com/bigquery/docs/data-clean-rooms) .

#### Grant dataset access to TransUnion

After you create the required tables and stored procedure, grant TransUnion access to read your input data and write matching results. Obtain the Apache Spark connection service account ID from the TransUnion customer delivery team. Then, grant that service account the BigQuery Data Editor role ( `roles/bigquery.dataEditor` ) on the dataset that contains your input and output tables.

#### Run a TransUnion entity resolution job

After you configure your tables and grant dataset access, you can start an entity resolution batch run. To invoke the entity resolution service, call the `TransUnion_get_identities` stored procedure:

```
CALL `PROJECT_ID.DATASET_ID.TransUnion_get_identities`(
  "PROJECT_ID.DATASET_ID.TransUnion_er_metadata",
  "CONFIG_ID");
```

Replace the following:

- `PROJECT_ID` : your Google Cloud project ID.
- `DATASET_ID` : the ID of the dataset that contains your metadata table and stored procedure.
- `CONFIG_ID` : the configuration ID for the batch run, such as `"1"` .

#### Get TransUnion support and billing information

For assistance with technical issues or billing inquiries related to TruAudience Identity Resolution and Enrichment in BigQuery, contact TransUnion directly:

- **Technical support** : contact [TransUnion Cloud Support](mailto:PDLtucloudappsupport@transunion.com) for assistance with setup, schema mapping, or troubleshooting.
- **Billing** : TransUnion tracks service usage for billing purposes. Contact your TransUnion delivery representative for account and pricing details.

## Configure entity resolution for identity providers

As an identity provider, you can offer your entity resolution service to BigQuery end users. This architecture helps protect your intellectual property because you don't expose your proprietary identity graph or matching logic.

To configure your service, you deploy an orchestrator endpoint, create a BigQuery remote function, grant the required roles, and share the remote function signature with your end users. For more information about the architecture, see [Entity resolution architecture](https://docs.cloud.google.com/bigquery/docs/entity-resolution-intro#architecture) .

### Before you begin

Before you configure your entity resolution service in BigQuery, ensure that you have the following:

- An identity graph dataset and matching logic that are deployed in your Google Cloud project or in an external database.
- End-user principal identifiers, such as user, service account, or Google Group email addresses, that you obtained from your end users.

### Required roles

To ensure that the identity provider's service account has the necessary permissions to run entity resolution jobs, ask your administrator to grant the following IAM roles to the identity provider's service account:

> **Important:** You must grant these roles to the identity provider's service account, *not* to your user account. Failure to grant the roles to the correct principal might result in permission errors.

- For the service account that's associated with your function to read and write to associated datasets and launch jobs:
  - [BigQuery Data Editor](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor) ( `roles/bigquery.dataEditor` ) on the project
  - [BigQuery Job User](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.jobUser) ( `roles/bigquery.jobUser` ) on the project
- For the end-user principal to see and connect to the remote function:
  - [BigQuery Connection User](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.connectionUser) ( `roles/bigquery.connectionUser` ) on the connection
  - [BigQuery Data Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataViewer) ( `roles/bigquery.dataViewer` ) on the control plane dataset with the remote function

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

Your administrator might also be able to give the identity provider's service account the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

### Set up the remote function endpoint

To process entity resolution requests from end users, deploy an orchestrator endpoint and connect it to a BigQuery remote function:

1.  To process matching requests from your remote function, create a [Cloud Run](https://docs.cloud.google.com/run/docs/overview/what-is-cloud-run) job or a [Cloud Run function](https://docs.cloud.google.com/functions/docs/concepts/overview) . You can use either option for your endpoint.

2.  To find the service account email address that's associated with your Cloud Run job or Cloud Run function, complete these steps:

    1.  In the Google Cloud console, go to the **Cloud Functions** page.

    2.  To open the function details, click the name of your function, and then click the **Details** tab.

    3.  In the **General Information** pane, find and record the service account email address for the remote function.

3.  In your control plane dataset, [create a remote function](https://docs.cloud.google.com/bigquery/docs/remote-functions#create-a-remote-function) that connects to your Cloud Run job or Cloud Run function endpoint.

### Share the entity resolution remote function

After you create the remote function and grant the required roles to your end users, share the following remote function signature with them. End users call this remote function to start an entity resolution job.

```
`PARTNER_PROJECT_ID.DATASET_ID.match`(LIST_OF_PARAMETERS)
```

Replace the following:

- `PARTNER_PROJECT_ID` : the Google Cloud project ID of the identity provider.
- `DATASET_ID` : the ID of the dataset that contains the remote function.
- `LIST_OF_PARAMETERS` : the list of parameters to pass to the remote function.

### Optional: Provide entity resolution job metadata

To provide job metadata to your end users, you can expose a separate remote function or write a job status table to the end user's output dataset. For example, you can report execution statuses such as `RUNNING` , `COMPLETED` , or `ERROR` , along with processing metrics.

### Integrate with Cloud Marketplace for billing

To manage customer billing and onboarding through Google, integrate your entity resolution service with [Cloud Marketplace](https://docs.cloud.google.com/marketplace) . This integration lets you configure a [pricing model](https://docs.cloud.google.com/marketplace/docs/partners/integrated-saas/select-pricing) based on entity resolution job usage while Google handles billing for your service. For more information, see [Offering software as a service (SaaS) products](https://docs.cloud.google.com/marketplace/docs/partners/integrated-saas) .

## What's next

- Learn about [entity resolution in BigQuery sharing](https://docs.cloud.google.com/bigquery/docs/entity-resolution-intro) .
- Learn how to [create a remote function](https://docs.cloud.google.com/bigquery/docs/remote-functions#create_a_remote_function) .
- Learn how to [create a Cloud resource connection](https://docs.cloud.google.com/bigquery/docs/create-cloud-resource-connection) .
- For identity providers, learn how to [make your entity resolution service available on Google Cloud Marketplace](https://docs.cloud.google.com/marketplace/docs/partners/integrated-saas) .
