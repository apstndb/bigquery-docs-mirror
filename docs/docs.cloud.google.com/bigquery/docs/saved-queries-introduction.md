---
name: documents/docs.cloud.google.com/bigquery/docs/saved-queries-introduction
uri: https://docs.cloud.google.com/bigquery/docs/saved-queries-introduction
title: Introduction to saved queries
description: Use saved queries in BigQuery Studio to manage SQL scripts, collaborate, and migrate from deprecated classic queries.
data_source: docs.cloud.google.com
---

# Introduction to saved queries

Use saved queries in BigQuery to securely store, manage, and collaborate on your SQL scripts. As you work in the query editor, your changes are automatically saved to prevent accidental work loss.

Because saved queries are [BigQuery Studio](https://docs.cloud.google.com/bigquery/docs/query-overview#bigquery-studio) code assets powered by [Dataform](https://docs.cloud.google.com/dataform/docs/overview) , they offer advanced collaboration and version control features. You can:

- **Collaborate securely:** [share saved queries](https://docs.cloud.google.com/bigquery/docs/work-with-saved-queries#share-saved-query) with specific users and groups using Identity and Access Management (IAM).
- **Track changes:** review a detailed version history of your query edits.
- **Manage versions:** branch from or revert to previous versions of a query to safely test modifications.

Saved query capabilities are available only in the Google Cloud console.

## Saved query security

You control access to saved queries by using Identity and Access Management (IAM) roles. For more information, see [Share saved queries](https://docs.cloud.google.com/bigquery/docs/work-with-saved-queries#share-saved-query) and [Security considerations for saved queries](https://docs.cloud.google.com/bigquery/docs/work-with-saved-queries#saved-queries-security) .

## Supported regions

All saved queries are stored in a default [region](https://docs.cloud.google.com/bigquery/docs/saved-queries-introduction#supported_regions) . Updating the default region changes the location for any queries created after that point. The following table lists the regions where BigQuery Studio is available:

|                  | Region description | Region name               | Details                                                                                                                                                                  |
|------------------|--------------------|---------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Africa**       |                    |                           |                                                                                                                                                                          |
|                  | Johannesburg       | `africa-south1`           |                                                                                                                                                                          |
| **Americas**     |                    |                           |                                                                                                                                                                          |
|                  | Columbus           | `us-east5`                |                                                                                                                                                                          |
|                  | Dallas             | `us-south1`               | ![leaf icon](https://cloud.google.com/sustainability/region-carbon/gleaf.svg) [Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker) |
|                  | Iowa               | `us-central1`             | ![leaf icon](https://cloud.google.com/sustainability/region-carbon/gleaf.svg) [Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker) |
|                  | Los Angeles        | `us-west2`                |                                                                                                                                                                          |
|                  | Las Vegas          | `us-west4`                |                                                                                                                                                                          |
|                  | Montréal           | `northamerica-northeast1` | ![leaf icon](https://cloud.google.com/sustainability/region-carbon/gleaf.svg) [Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker) |
|                  | N. Virginia        | `us-east4`                |                                                                                                                                                                          |
|                  | Oregon             | `us-west1`                | ![leaf icon](https://cloud.google.com/sustainability/region-carbon/gleaf.svg) [Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker) |
|                  | São Paulo          | `southamerica-east1`      | ![leaf icon](https://cloud.google.com/sustainability/region-carbon/gleaf.svg) [Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker) |
|                  | South Carolina     | `us-east1`                |                                                                                                                                                                          |
| **Asia Pacific** |                    |                           |                                                                                                                                                                          |
|                  | Hong Kong          | `asia-east2`              |                                                                                                                                                                          |
|                  | Jakarta            | `asia-southeast2`         |                                                                                                                                                                          |
|                  | Mumbai             | `asia-south1`             |                                                                                                                                                                          |
|                  | Seoul              | `asia-northeast3`         |                                                                                                                                                                          |
|                  | Singapore          | `asia-southeast1`         |                                                                                                                                                                          |
|                  | Sydney             | `australia-southeast1`    |                                                                                                                                                                          |
|                  | Taiwan             | `asia-east1`              |                                                                                                                                                                          |
|                  | Tokyo              | `asia-northeast1`         |                                                                                                                                                                          |
| **Europe**       |                    |                           |                                                                                                                                                                          |
|                  | Belgium            | `europe-west1`            | ![leaf icon](https://cloud.google.com/sustainability/region-carbon/gleaf.svg) [Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker) |
|                  | Finland            | `europe-north1`           | ![leaf icon](https://cloud.google.com/sustainability/region-carbon/gleaf.svg) [Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker) |
|                  | Frankfurt          | `europe-west3`            |                                                                                                                                                                          |
|                  | London             | `europe-west2`            | ![leaf icon](https://cloud.google.com/sustainability/region-carbon/gleaf.svg) [Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker) |
|                  | Madrid             | `europe-southwest1`       | ![leaf icon](https://cloud.google.com/sustainability/region-carbon/gleaf.svg) [Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker) |
|                  | Milan              | `europe-west8`            | ![leaf icon](https://cloud.google.com/sustainability/region-carbon/gleaf.svg) [Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker) |
|                  | Netherlands        | `europe-west4`            | ![leaf icon](https://cloud.google.com/sustainability/region-carbon/gleaf.svg) [Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker) |
|                  | Turin              | `europe-west12`           | ![leaf icon](https://cloud.google.com/sustainability/region-carbon/gleaf.svg) [Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker) |
|                  | Warsaw             | `europe-central2`         | ![leaf icon](https://cloud.google.com/sustainability/region-carbon/gleaf.svg) [Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker) |
|                  | Zürich             | `europe-west6`            | ![leaf icon](https://cloud.google.com/sustainability/region-carbon/gleaf.svg) [Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker) |
| **Middle East**  |                    |                           |                                                                                                                                                                          |
|                  | Dammam             | `me-central2`             |                                                                                                                                                                          |
|                  | Doha               | `me-central1`             |                                                                                                                                                                          |
|                  | Tel Aviv           | `me-west1`                |                                                                                                                                                                          |

## Quotas and limits

For more information, see the [saved query quotas and limits](https://docs.cloud.google.com/bigquery/quotas#saved_query_limits) .

## Limitations

Saved queries have the following limitations:

- You can [grant public access to saved queries](https://docs.cloud.google.com/bigquery/docs/manage-saved-queries#grant-public-access) only to the [`allAuthenticatedUsers`](https://docs.cloud.google.com/iam/docs/principals-overview#all-authenticated-users) principal. You can't grant access to saved queries to the [`allUsers`](https://docs.cloud.google.com/iam/docs/principals-overview#all-users) principal.
- If your Google Cloud project contains more than 2,500 classic saved queries, you can't use [batch migration](https://docs.cloud.google.com/bigquery/docs/manage-saved-queries#migrate_classic_saved_queries) to migrate classic saved queries to saved queries.

## Classic saved queries (Deprecated)

> **Deprecated:** Saved queries, available in [BigQuery Studio](https://docs.cloud.google.com/bigquery/docs/enable-assets) , will fully replace classic saved queries in the future. The deprecation timeline is being reviewed. For more information, see [Deprecation of classic saved queries](https://docs.cloud.google.com/bigquery/docs/saved-queries-introduction#classic-saved-queries-deprecation) . To learn how to migrate to saved queries, see [Migrate classic saved queries](https://docs.cloud.google.com/bigquery/docs/manage-saved-queries#migrate_classic_saved_queries) .

To edit existing classic saved queries after they are fully deprecated, you must [migrate them](https://docs.cloud.google.com/bigquery/docs/manage-saved-queries#migrate_classic_saved_queries) to BigQuery Studio.

Classic saved queries are an older method for saving and sharing SQL. Unlike BigQuery Studio saved queries, they only retain the query text and the SQL version (legacy SQL or GoogleSQL).

In the Google Cloud console, they appear in the **(Classic) Queries** folder within the **Explorer** pane. (If you haven't enabled BigQuery Studio, they appear in the **Saved queries ( ` NUMBER ` )** folder in the **Classic Explorer** pane).

There are three types of classic saved queries:

- **Personal** ( person ): visible only to the user who created them.

  - Note: If a personal query contains sensitive information, you must delete the query or remove the sensitive data prior to migration.

- **Project-level** ( people ): visible to any principal with the [required permissions](https://docs.cloud.google.com/bigquery/docs/work-with-saved-queries#required_permissions_for_classic_saved_queries) .

- **Public** ( share ): visible to anyone who has the link to the query.

### IAM roles for migration and access

The following predefined BigQuery IAM roles include the required [Dataform permissions](https://docs.cloud.google.com/dataform/docs/access-control#dataform.admin) to help you transition to BigQuery Studio saved queries:

- **[BigQuery Admin](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.admin)** ( `roles/bigquery.admin` ) includes `roles/dataform.admin` permissions.
- **[BigQuery Job User](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.jobUser)** ( `roles/bigquery.jobUser` ) and **[BigQuery User](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.user)** ( `roles/bigquery.user` ) include:
  - `dataform.locations.get`
  - `dataform.locations.list`
  - `dataform.repositories.create`
  - `dataform.repositories.list`

If you don't have one of these predefined roles, you request the [required permissions](https://docs.cloud.google.com/bigquery/docs/work-with-saved-queries#required_permissions) . [Custom roles](https://docs.cloud.google.com/iam/docs/roles-overview#custom) aren't automatically updated and must be [edited manually](https://docs.cloud.google.com/iam/docs/creating-custom-roles#edit-role) .

## What's next

- To learn how to create saved queries, see [Create saved queries](https://docs.cloud.google.com/bigquery/docs/work-with-saved-queries) .
- To learn how to manage saved queries, see [Manage saved queries](https://docs.cloud.google.com/bigquery/docs/manage-saved-queries) .
