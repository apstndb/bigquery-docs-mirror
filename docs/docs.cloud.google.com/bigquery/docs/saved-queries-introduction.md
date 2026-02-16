# Introduction to saved queries

This document provides an introduction to saved queries in BigQuery. You can use saved queries to create and manage SQL scripts. Changes to a saved query are automatically saved so that you don't lose your work when you close the query editor. Saved queries improve collaboration and query management with the following options:

  - [Share saved queries](/bigquery/docs/work-with-saved-queries#share-saved-query) with specific users and groups by using Identity and Access Management (IAM).
  - Review the query version history.
  - Revert to or branch from previous versions of the query.

Saved queries are [BigQuery Studio](/bigquery/docs/query-overview#bigquery-studio) code assets powered by [Dataform](/dataform/docs/overview) . [Notebooks](/bigquery/docs/notebooks-introduction) are also code assets. All code assets are stored in a default [region](#supported_regions) . Updating the default region changes the region for all code assets created after that point.

Saved query capabilities are available only in the Google Cloud console.

### Saved query security

You control access to saved queries by using Identity and Access Management (IAM) roles. For more information, see [Share saved queries](/bigquery/docs/work-with-saved-queries#share-saved-query) .

### Supported regions

BigQuery Studio lets you save, share, and manage saved queries. The following table lists the regions where BigQuery Studio is available:

Region description

Region name

Details

**Africa**

Johannesburg

`  africa-south1  `

**Americas**

Columbus

`  us-east5  `

Dallas

`  us-south1  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Iowa

`  us-central1  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Las Vegas

`  us-west4  `

Los Angeles

`  us-west2  `

Mexico

`  northamerica-south1  `

Montréal

`  northamerica-northeast1  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

North Virginia

`  us-east4  `

Oklahoma

`  us-central2  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Oregon

`  us-west1  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Salt Lake City

`  us-west3  `

Santiago

`  southamerica-west1  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

São Paulo

`  southamerica-east1  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

South Carolina

`  us-east1  `

Toronto

`  northamerica-northeast2  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

**Asia Pacific**

Bangkok

`  asia-southeast3  `

Delhi

`  asia-south2  `

Hong Kong

`  asia-east2  `

Jakarta

`  asia-southeast2  `

Melbourne

`  australia-southeast2  `

Mumbai

`  asia-south1  `

Osaka

`  asia-northeast2  `

Seoul

`  asia-northeast3  `

Singapore

`  asia-southeast1  `

Sydney

`  australia-southeast1  `

Taiwan

`  asia-east1  `

Tokyo

`  asia-northeast1  `

**Europe**

Belgium

`  europe-west1  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Berlin

`  europe-west10  `

Finland

`  europe-north1  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Frankfurt

`  europe-west3  `

London

`  europe-west2  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Madrid

`  europe-southwest1  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Milan

`  europe-west8  `

Netherlands

`  europe-west4  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Paris

`  europe-west9  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Stockholm

`  europe-north2  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Turin

`  europe-west12  `

Warsaw

`  europe-central2  `

Zürich

`  europe-west6  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

**Middle East**

Dammam

`  me-central2  `

Doha

`  me-central1  `

Tel Aviv

`  me-west1  `

### Quotas and limits

For more information, see [Saved query quotas and limits](/bigquery/quotas#saved_query_limits) .

### Limitations

Saved queries have the following limitations:

  - You can [grant public access to saved queries](/bigquery/docs/manage-saved-queries#grant-public-access) only to the [`  allAuthenticatedUsers  `](/iam/docs/principals-overview#all-authenticated-users) principal. You can't grant access to saved queries to the [`  allUsers  `](/iam/docs/principals-overview#all-users) principal.
  - If your Google Cloud project contains more than 2500 classic saved queries, you can't use [batch migration](/bigquery/docs/manage-saved-queries#migrate_classic_saved_queries) to migrate classic saved queries to saved queries.

## Classic saved queries

**Deprecated:** Saved queries, available in [BigQuery Studio](/bigquery/docs/enable-assets) , will fully replace classic saved queries in the future. The deprecation timeline is being reviewed. For more information, see [Deprecation of classic saved queries](/bigquery/docs/saved-queries-introduction#classic-saved-queries-deprecation) . To learn how to migrate to saved queries, see [Migrate classic saved queries](/bigquery/docs/manage-saved-queries#migrate_classic_saved_queries) .

Classic saved queries are an earlier way of saving and sharing SQL queries. Classic saved queries provide the query text, and the only query setting retained by a classic saved query is the SQL version. This setting governs whether the query uses legacy SQL or GoogleSQL. To query the data, users must have access to the data that the saved query accesses.

You can see classic saved queries in the **(Classic) Queries** folder in the **Classic Explorer** pane:

**Note:** If you have not enabled BigQuery Studio, classic saved queries appear in the **Saved queries ( NUMBER )** folder in the **Classic Explorer** pane, instead of the **(Classic) Queries** folder.

There are 3 types of classic saved queries:

  - **Personal.** Personal classic saved queries are visible only to the user who creates them. They are identified with the person icon.
  - **Project-level.** Project-level saved queries are visible to principals that have the required [permissions](/bigquery/docs/work-with-saved-queries#required_permissions_for_classic_saved_queries) . They are identified with the people icon.
  - **Public.** Public classic saved queries are visible to anyone with a link to the query. They are identified with the share icon.

You can [migrate](/bigquery/docs/manage-saved-queries#migrate_classic_saved_queries) classic saved queries to saved queries to take advantage of the new capabilities, or [continue to maintain them](/bigquery/docs/work-with-saved-queries#update_classic_saved_queries) as classic saved queries until deprecation. The timeline for deprecation is being reviewed.

The classic saved query feature is available only in the Google Cloud console.

## Deprecation of classic saved queries

The saved queries feature of [BigQuery Studio](/bigquery/docs/enable-assets) is replacing classic saved queries. The deprecation timeline is being reviewed. To edit existing classic saved queries after deprecation, you must [migrate classic queries](/bigquery/docs/manage-saved-queries#migrate_classic_saved_queries) to BigQuery Studio saved queries.

If users, including yourself, have personal queries with information that shouldn't be made available to others with access to data in the project, then the query's owner must delete the queries or the information before completing the migration.

To support this transition, the following BigQuery IAM roles were updated in February 2024:

  - [BigQuery Admin](/bigquery/docs/access-control#bigquery.admin) ( `  roles/bigquery.admin  ` ) gets [Dataform Admin](/dataform/docs/access-control#dataform.admin) ( `  roles/dataform.admin  ` ) permissions.

  - [BigQuery Job User](/bigquery/docs/access-control#bigquery.jobUser) ( `  roles/bigquery.jobUser  ` ) gets the following permissions:
    
      - `  dataform.locations.get  `
      - `  dataform.locations.list  `
      - `  dataform.repositories.create  `
      - `  dataform.repositories.list  `

  - [BigQuery User](/bigquery/docs/access-control#bigquery.user) ( `  roles/bigquery.user  ` ) gets the following permissions:
    
      - `  dataform.locations.get  `
      - `  dataform.locations.list  `
      - `  dataform.repositories.create  `
      - `  dataform.repositories.list  `

**Warning:** Visibility for code assets is governed by project-level Dataform permissions. Users with the `  dataform.repositories.list  ` permission—which is included in standard BigQuery roles such as [BigQuery Job User](/bigquery/docs/access-control#bigquery.jobUser) , [BigQuery Studio User](/bigquery/docs/access-control#bigquery.studioUser) , and [BigQuery User](/bigquery/docs/access-control#bigquery.user) —can see all code assets in the **Explorer** panel of the Google Cloud project, regardless of whether they created these assets or these assets were shared with them. To restrict visibility, you can create [custom roles](/iam/docs/creating-custom-roles) that exclude the `  dataform.repositories.list  ` permission.

To let users without the BigQuery Admin, BigQuery Job User, or BigQuery User roles use saved queries, grant them the [required permissions](/bigquery/docs/work-with-saved-queries#required_permissions) in IAM.

[Custom roles](/iam/docs/roles-overview#custom) won't be automatically updated. To update a custom role with the [required permissions](/bigquery/docs/work-with-saved-queries#required_permissions) , see [Edit an existing custom role](/iam/docs/creating-custom-roles#edit-role) .

## What's next

  - To learn how to create saved queries, see [Create saved queries](/bigquery/docs/work-with-saved-queries) .
  - To learn how to manage saved queries, see [Manage saved queries](/bigquery/docs/manage-saved-queries) .
