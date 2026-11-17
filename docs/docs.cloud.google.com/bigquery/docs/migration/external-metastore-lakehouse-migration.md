---
name: documents/docs.cloud.google.com/bigquery/docs/migration/external-metastore-lakehouse-migration
uri: https://docs.cloud.google.com/bigquery/docs/migration/external-metastore-lakehouse-migration
title: Migrate metadata from external data catalogs to Lakehouse REST catalog tables for Apache Iceberg
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# Migrate metadata from external data catalogs to Lakehouse REST catalog tables for Apache Iceberg

> **Preview**
>
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> **Note:** To get support or provide feedback for this feature, contact <da-migrations-feedback@google.com> .

This document shows you how to migrate metadata from external data catalogs to [Lakehouse REST catalog tables for Apache Iceberg](https://docs.cloud.google.com/biglake/docs/biglake-iceberg-tables) . The BigQuery Migration Service supports the migration of metadata from the following external metastores:

- Apache Hive Metastore
- Apache Iceberg REST Catalogs

## Limitations

> **Warning:** Modifying data on both the source and destination tables after a migration can lead to data loss.

- Metadata migrations from external data catalogs to Lakehouse REST catalog tables for Apache Iceberg are a one-time sync. This feature doesn't support continuous or periodic syncs, so any writes made after migration aren't visible until you migrate again.
- Nested namespaces aren't supported.
- The Iceberg REST catalog only supports Parquet data files.
- Borderless Lakehouse doesn't support Apache Iceberg V3 tables.
- Metadata migrations from external data catalogs to Lakehouse REST catalog tables for Apache Iceberg don't support the use of organization policies to enforce [domain-restricted sharing](https://docs.cloud.google.com/organization-policy/domain-restricted-sharing) .

## Before you begin

Before you can migrate metadata from your external data catalogs, you must do the steps in the following sections.

### Enable APIs

Enable the BigLake, BigQuery Data Transfer, BigQuery Migration, Secret Manager, Storage Transfer APIs, if any are not already enabled.

**Roles required to enable APIs**

To enable APIs, you need the `serviceusage.services.enable` permission. If you created the project, then you likely already have this permission through the Owner role ( `roles/owner` ). Otherwise, you can get this permission through the Service Usage Admin role ( `roles/serviceusage.serviceUsageAdmin` ). [Learn how to grant roles](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

A [service agent](https://docs.cloud.google.com/bigquery/docs/enable-transfer-service#service_agent) is created when you enable the Data Transfer API.

### Configure permissions

To migrate metadata from an external data catalog to Lakehouse REST catalog tables for Apache Iceberg, you must grant the required permissions to the following user accounts and service agents.

By default, the Google Cloud console IAM page hides Google-managed service agents, including the BigQuery migration service agent and the BigQuery Data Transfer Service agent. To include these service agents, click the service account and under **Principals with access** , select **Include Google-provided role grants** .

![Include Google-provided role grants](https://docs.cloud.google.com/static/bigquery/images/lakehouse-migration-enable-service-account.png)

#### Grant user account permissions

To get the permissions that you need to select and attach the custom service account to the migration job in the console, ask your administrator to grant you the following IAM roles on the custom service account at the resource level:

- [Service Account User](https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.serviceAccountUser) ( `roles/iam.serviceAccountUser` )
- [Migration Management Editor](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.migrationEditor) ( `roles/bigquerymigration.migrationEditor` )

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

#### Grant custom service account permissions

To ensure that the custom service account has the necessary permissions to instantiate the transfer configuration, ask your administrator to grant the following IAM roles to the custom service account:

> **Important:** You must grant these roles to the custom service account, *not* to your user account. Failure to grant the roles to the correct principal might result in permission errors.

- Allow access to the network attachment: [Compute Network Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/compute#compute.networkAdmin) ( `roles/compute.networkAdmin` ) on the custom service account
- Access to the BigQuery Data Transfer Service: [BigQuery Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin) ( `roles/bigquery.admin` ) on the custom service account
- Allow access to Lakehouse resources: [BigLake Editor](https://docs.cloud.google.com/iam/docs/roles-permissions/biglake#biglake.editor) ( `roles/biglake.editor` ) on the custom service account
- Access to secrets: [Secret Manager Secret Accessor](https://docs.cloud.google.com/iam/docs/roles-permissions/secretmanager#secretmanager.secretAccessor) ( `roles/secretmanager.secretAccessor` ) on the customer-provided secret

For more information about granting roles to service accounts, see [Manage access to service accounts](https://docs.cloud.google.com/iam/docs/manage-access-service-accounts) .

#### Grant BigQuery migration service agent permissions

To ensure that the BigQuery migration service agent has the necessary permissions to impersonate the custom service account to authorize against the Dataproc Metastore during discovery, ask your administrator to grant the [Service Account Token Creator](https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.serviceAccountTokenCreator) ( `roles/iam.serviceAccountTokenCreator` ) IAM role to the BigQuery migration service agent on the custom service account at the resource level.

> **Important:** You must grant this role to the BigQuery migration service agent, *not* to your user account. Failure to grant the role to the correct principal might result in permission errors.

For more information about granting roles to service agents, see [Manage access to service accounts](https://docs.cloud.google.com/iam/docs/manage-access-service-accounts) .

You must also [create a service identity](https://docs.cloud.google.com/sdk/gcloud/reference/beta/services/identity/create) for the BigQuery Migration Service and grant it the `roles/iam.serviceAccountTokenCreator` role. To create the service identity, run the following command:

```
  gcloud beta services identity create --service=bigquerymigration.googleapis.com --project=PROJECT_ID
```

Replace `PROJECT_ID` with your project ID.

#### Grant BigQuery Data Transfer Service agent permissions

To ensure that the BigQuery Data Transfer Service agent has the necessary permissions to register tables into Lakehouse and orchestrate the transferring of files, ask your administrator to grant the following IAM roles to the BigQuery Data Transfer Service agent on the project level:

> **Important:** You must grant these roles to the BigQuery Data Transfer Service agent, *not* to your user account. Failure to grant the roles to the correct principal might result in permission errors.

- [BigLake Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/biglake#biglake.admin) ( `roles/biglake.admin` )
- [Storage Transfer Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/storagetransfer#storagetransfer.admin) ( `roles/storagetransfer.admin` )
- [Storage Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/storage#storage.admin) ( `roles/storage.admin` )
- [Service Usage Consumer](https://docs.cloud.google.com/iam/docs/roles-permissions/serviceusage#serviceusage.serviceUsageConsumer) ( `roles/serviceusage.serviceUsageConsumer` )

For more information about granting roles to service agents, see [Manage access to service accounts](https://docs.cloud.google.com/iam/docs/manage-access-service-accounts) .

### Configure secret

If you are migrating to an Apache Iceberg REST catalog, you must create a secret to authorize the migration. The secret must be formatted in the following format:

```
{
  "client_id": "CLIENT_ID",
  "client_secret": "CLIENT_SECRET",
  "polaris_realm": "POLARIS_REALM",
  "scope": "SCOPE"
}
```

Replace the following:

- `CLIENT_ID` : the OAuth 2.0 client ID
- `CLIENT_SECRET` : the OAuth 2.0 client secret
- `POLARIS_REALM` : the realm for the Polaris catalog. This field is required only for Apache Polaris. For example, `FINANCE` .
- `SCOPE` : (Optional) the OAuth 2.0 scope. Default value is `PRINCIPAL_ROLE:ALL` .

## Create a Lakehouse catalog

[Create a Lakehouse catalog](https://docs.cloud.google.com/biglake/docs/use-biglake-metastore-iceberg-rest-catalog#create-biglake-catalog) . The migrated metadata is stored in the Cloud Storage bucket that you specified when you create the catalog.

## Migrate metadata

To start a metadata migration to Lakehouse Iceberg REST catalog tables, do the following:

1.  In the Google Cloud console, go to the **Migration** \> **Services** page.

2.  Under **Register or Migrate Open Lakehouse** , click **Create migration** .

3.  Under **Migration configuration** , do the following:

    1.  For catalog type, select an external catalog.

    2.  For **Region** , select a region. The selected region determines where the migration orchestration and the data transfer is run. It also determines where the migration service uses or creates any resources, such as network attachments or secrets.

        Only [regional secrets](https://docs.cloud.google.com/secret-manager/regional-secrets/create-regional-secret) are supported. The region of the secret must match the region in this field.

    3.  For **Migration display name** , enter a name for this migration.

4.  Under **Source system configuration** , do the following:

    1.  For **URL** , enter the base endpoint URL that acts as the entry point for the Apache Iceberg or Apache Hive metastore.
    2.  For **Service account** , select a service account from the list. If not specified, this migration runs using the user credential.
    3.  (Optional) For **Network attachment** , select a network attachment.

5.  Click **Continue** .

When the metadata migration completes, the metadata from your external catalogs is stored in the Cloud Storage bucket that you specified when you [created the Lakehouse catalog](https://docs.cloud.google.com/biglake/docs/use-biglake-metastore-iceberg-rest-catalog#create-biglake-catalog) .

## Pricing

There is no cost to transfer metadata to Lakehouse Iceberg REST catalog tables. Once metadata is transferred, [Lakehouse pricing](https://cloud.google.com/products/biglake/pricing) applies.
