---
name: documents/docs.cloud.google.com/bigquery/docs/query-templates
uri: https://docs.cloud.google.com/bigquery/docs/query-templates
title: Use query templates
description: Create, approve, and run predefined SQL query templates in BigQuery data clean rooms to help protect sensitive data.
data_source: docs.cloud.google.com
---

# Use query templates

BigQuery data clean room query templates let data owners and contributors publish approved queries for subscribers. Predefining these queries minimizes data exfiltration risks, ensures consistent analytical outcomes, and simplifies onboarding for analysts unfamiliar with privacy-centric SQL.

Query templates use [table-valued functions (TVFs)](https://docs.cloud.google.com/bigquery/docs/table-functions) to accept tables or specific fields as parameters and return results without exposing raw data.

## Limitations

Query templates have the following limitations:

- Query templates support a maximum of two data references—that is, the data used to define the TVF's query and the data parameter input that the TVF accepts. You can reference multiple tables or views within the TVF's query definition, but they must all belong to the same data owner or party.
- Query template TVFs support only `TABLE` and `VIEW` fixed types.
- Query template definitions are subject to [the same limitations as TVFs](https://docs.cloud.google.com/bigquery/docs/table-functions#limitations) .

## Roles

There are three main roles for using data clean room query templates. Each role has specific workflows, which are described in this document:

- **Template creator** : a user who defines the queries to be executed within the clean room. This role is analogous to any of the following Identity and Access Management (IAM) roles: [Analytics Hub Admin](https://docs.cloud.google.com/bigquery/docs/analytics-hub-grant-roles#ah-admin-role) , [Analytics Hub Publisher](https://docs.cloud.google.com/bigquery/docs/analytics-hub-grant-roles#ah-publisher-role) , or [Analytics Hub Listing Admin](https://docs.cloud.google.com/bigquery/docs/analytics-hub-grant-roles#ah-publisher-role) . For more information, see [Template creator workflows](https://docs.cloud.google.com/bigquery/docs/query-templates#template-creator-workflows) .

- **Template approver** : the owner of the data who must approve the query template's references before the template is available for use. This role is analogous to any of the following IAM roles: [Analytics Hub Admin](https://docs.cloud.google.com/bigquery/docs/analytics-hub-grant-roles#ah-admin-role) , [Analytics Hub Publisher](https://docs.cloud.google.com/bigquery/docs/analytics-hub-grant-roles#ah-publisher-role) , or [Analytics Hub Listing Admin](https://docs.cloud.google.com/bigquery/docs/analytics-hub-grant-roles#ah-publisher-role) . For more information, see [Template approver workflows](https://docs.cloud.google.com/bigquery/docs/query-templates#template-approver-workflows) .

- **Template subscriber** : a user who subscribes to the clean room and can run only the queries that are approved in the template. This role is analogous to the [Analytics Hub Subscriber](https://docs.cloud.google.com/bigquery/docs/analytics-hub-grant-roles#ah-subscriber-role) IAM role. For more information, see [Template subscriber workflows](https://docs.cloud.google.com/bigquery/docs/query-templates#template-subscriber-workflows) .

## Before you begin

To enable the Analytics Hub API for your Google Cloud project, select one of the following options:

### Console

1.  In the Google Cloud console, go to the **Analytics Hub API** page.

2.  In the Google Cloud console toolbar, select your project.

3.  If the API isn't already enabled, click **Enable** .

### gcloud

Run the [`gcloud services enable` command](https://docs.cloud.google.com/sdk/gcloud/reference/services/enable) :

```
gcloud services enable analyticshub.googleapis.com
```

### Required roles

To get the permissions that you need to perform the tasks in this document, ask your administrator to grant you the following IAM roles:

- Create or delete a TVF in a data clean room:
  - [Analytics Hub Publisher](https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.publisher) ( `roles/analyticshub.publisher` ) on the project
  - [Analytics Hub Subscriber](https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.subscriber) ( `roles/analyticshub.subscriber` ) on the project
- Authorize a TVF: [BigQuery Data Owner](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner) ( `roles/bigquery.dataOwner` ) on the project
- Add, update, or delete a TVF listing in a data clean room:
  - [Analytics Hub Publisher](https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.publisher) ( `roles/analyticshub.publisher` ) on the project
  - [Analytics Hub Subscriber](https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.subscriber) ( `roles/analyticshub.subscriber` ) on the project
- Create a query template:
  - [Analytics Hub Publisher](https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.publisher) ( `roles/analyticshub.publisher` ) on the project
  - [Analytics Hub Subscriber](https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.subscriber) ( `roles/analyticshub.subscriber` ) on the project
- Approve a query template:
  - [Analytics Hub Publisher](https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.publisher) ( `roles/analyticshub.publisher` ) on the project
  - [BigQuery Data Owner](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner) ( `roles/bigquery.dataOwner` ) on the project
- Subscribe to a data clean room with query templates:
  - [Analytics Hub Subscriber](https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.subscriber) ( `roles/analyticshub.subscriber` ) on the project
  - [Analytics Hub Subscription Owner](https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.subscriptionOwner) ( `roles/analyticshub.subscriptionOwner` ) on the project where you want to subscribe to the data clean room
- Execute the queries defined in query templates:
  - [BigQuery Data Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataViewer) ( `roles/bigquery.dataViewer` ) on the project
  - [BigQuery User](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.user) ( `roles/bigquery.user` ) on the project

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

These predefined roles contain the permissions required to perform the tasks in this document. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to perform the tasks in this document:

- Create or delete a TVF in a data clean room:
  - `bigquery.routines.create` on the project
  - `bigquery.routines.update` on the project
  - `bigquery.routines.delete` on the project
- Authorize a TVF: `bigquery.datasets.update` on the datasets that the routine accesses
- Create a query template:
  - `analyticshub.listings.subscribe` on the project
  - `analyticshub.queryTemplates.create` on the project
- Approve a query template:
  - `bigquery.routines.create` on the project
  - `bigquery.datasets.update` on the datasets that the routine accesses
  - `analyticshub.listings.create` on the project
  - `analyticshub.queryTemplates.approve` on the project
- Update an existing query template: `analyticshub.queryTemplates.update` on the query template
- Retrieve details of a query template: `analyticshub.queryTemplates.get` on the query template
- List all query templates in a data exchange: `analyticshub.queryTemplates.list` on the data exchange
- Delete a query template: `analyticshub.queryTemplates.delete` on the query template

You might also be able to get these permissions with [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Template creator workflows

As a query template creator, you can do the following:

- [Add a listing to a data clean room](https://docs.cloud.google.com/bigquery/docs/query-templates#add-listing-to-dcr) .
- [Add an existing TVF to a data clean room](https://docs.cloud.google.com/bigquery/docs/query-templates#add-existing-tvf-to-dcr) .
- [Create a query template](https://docs.cloud.google.com/bigquery/docs/query-templates#create-query-template) .
- [Update a query template](https://docs.cloud.google.com/bigquery/docs/query-templates#update-query-template) .
- [Submit a query template for review](https://docs.cloud.google.com/bigquery/docs/query-templates#submit-query-template) .
- [Delete a query template](https://docs.cloud.google.com/bigquery/docs/query-templates#delete-query-template) .

### Add a listing to a data clean room

Before creating a query template, you must add data to a data clean room. To create a listing in the data clean room, follow these steps:

1.  In the Google Cloud console, go to the **Sharing (Analytics Hub)** page.

2.  Click the display name of the data clean room where you want to create the query template.

3.  Click **Add data** and follow the steps to create a view with analysis rules configured. For detailed instructions, see [Create a listing (add data)](https://docs.cloud.google.com/bigquery/docs/data-clean-rooms#add-data) .

    To add data from other parties, share the clean room with another [trusted contributor](https://docs.cloud.google.com/bigquery/docs/data-clean-rooms#data_contributor_workflows) . This data contributor must also add data to the clean room to be eligible for use in a query template.

4.  Set [data egress](https://docs.cloud.google.com/bigquery/docs/analytics-hub-introduction#data_egress) controls for the listing.

5.  Set the metadata controls for the listing. If you want to share only the schemas and descriptions of the data added in the previous step (and not the shared data itself), select **Exclude access to listing from linked dataset** .

    > **Note:** You must have the Analytics Hub Subscriber ( `roles/analyticshub.subscriber` ) role at the data clean room exchange level before you attempt to create a query template. The Analytics Hub Subscriber role lets you view the schemas of the data added to the clean room.

    > **Note:** You can't update a listing to enable metadata controls, so create query templates on new listings. This helps prevent shared data from being exposed to template subscribers, including data contributors who need the Analytics Hub Subscriber role to view the metadata.

6.  Review the listing details.

7.  Click **Add data** . The clean room now includes the metadata of the view that you created for your data.

### Add an existing TVF to a data clean room

You can add an existing TVF to a data clean room by using the Analytics Hub API.

Use the [`projects.locations.dataExchanges.listings.create` method](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges.listings/create) .

The following example shows how to call the `projects.locations.dataExchanges.listings.create` method by using the `curl` command:

```
curl -H "Authorization: Bearer $(gcloud auth print-access-token)" -H "Content-Type: application/json" -H 'x-goog-user-project:DCR_PROJECT_ID' -X POST https://analyticshub.googleapis.com/v1/projects/DCR_PROJECT_ID/locations/LOCATION/dataExchanges/CLEAN_ROOM_ID/listings?listingId=LISTING_ID -d \
    '{"bigqueryDataset":{"dataset":"projects/PROJECT_ID/datasets/DATASET_ID","selectedResources":[{"routine":"projects/PROJECT_ID/datasets/DATASET_ID/routines/ROUTINE_ID"}]},"displayName":"LISTING_NAME"}'
```

Replace the following:

- `DCR_PROJECT_ID` : the project ID of the project where the data clean room was created.
- `LOCATION` : the location of the data clean room.
- `CLEAN_ROOM_ID` : the data clean room ID.
- `LISTING_ID` : the listing ID.
- `PROJECT_ID` : the project ID of the project that contains the source dataset.
- `DATASET_ID` : the source dataset ID.
- `ROUTINE_ID` : the routine ID.
- `LISTING_NAME` : the listing display name.

### Create a query template

To create a query template, select one of the following options:

### Console

1.  In the Google Cloud console, go to the **Sharing (Analytics Hub)** page.

2.  Click the display name of the data clean room where you want to create the query template.

3.  In the clean room, go to the **Templates** tab.

4.  Click **Create Template** .

5.  Enter a template display name and description.

    > **Note:** You can't update the query template display name after you create the query template.

6.  Click **Next** .

7.  Propose a query definition by using the schemas of the views added to the clean room:

    - Define the query by using the supported [`CREATE TABLE FUNCTION` syntax](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_table_function_statement) .

    - Pass your entire table or view with fixed definitions. You must define the full table path reference, including the project ID and dataset ID, from the data added to the clean room. For example:

      ```
          query_template1(t1 TABLE<year INT64>) AS (SELECT * FROM `project_id.dataset_id.table_id` WHERE year = table_id.year)
      ```

    - If you applied privacy analysis rules to the data, make sure that this TVF includes privacy-specific SQL syntax, such as [`SELECT WITH AGGREGATION_THRESHOLD`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/query-syntax#agg_threshold_clause) .

      > **Note:** Routine definitions are always hidden and never shared with template subscribers. Subscribers see only the table input parameter that the TVF expects.

8.  Review the template details.

9.  To save the template without submitting it for review, click **Save** . The query template now has the status of **DRAFT** .

You can [update the query template](https://docs.cloud.google.com/bigquery/docs/query-templates#update-query-template) or [submit the query template for review](https://docs.cloud.google.com/bigquery/docs/query-templates#submit-query-template) .

> **Note:** You must [authorize the TVF or routine](https://docs.cloud.google.com/bigquery/docs/authorized-routines#authorize_routines) for template subscribers to query the routine. If you modify a routine by running a `CREATE OR REPLACE` statement, such as `CREATE OR REPLACE FUNCTION` , `CREATE OR REPLACE PROCEDURE` , or `CREATE OR REPLACE TABLE FUNCTION` , you must reauthorize the routine.

### API

The following example shows how to create a query template by using the `curl` command:

```
curl -H "Authorization: Bearer $(gcloud auth print-access-token)" -H "Content-Type: application/json" -H 'x-goog-user-project:DCR_PROJECT_ID' -X POST https://analyticshub.googleapis.com/v1/projects/DCR_PROJECT_ID/locations/LOCATION/dataExchanges/CLEAN_ROOM_ID/queryTemplates?queryTemplateId=QUERY_TEMPLATE_ID -d \
'{
  "displayName": "DISPLAY_NAME",
  "routine": {
    "routineType": "TABLE_VALUED_FUNCTION",
    "definitionBody": "QUERY_TEMPLATE_ID(TVF arguments) AS (TVF_DEFINITION)"
  }
}'
```

Replace the following:

- `DCR_PROJECT_ID` : the project ID of the project where the data clean room was created.
- `LOCATION` : the location of the data clean room.
- `CLEAN_ROOM_ID` : the data clean room ID.
- `QUERY_TEMPLATE_ID` : the query template ID.
- `DISPLAY_NAME` : the display name of the query template. You can't update the query template display name after you create the query template.
- `TVF_DEFINITION` : the TVF definition.

The following code sample shows a `definition_body` example for the API call. You must define the full table path reference, including the project ID and dataset ID, from the data added to the clean room:

```
  query_template1(t1 TABLE<year INT64>) AS (SELECT * FROM `project_id.dataset_id.table_id` WHERE year = table_id.year)
```

The `definition_body` is analogous to the definition of a routine. The preceding `definition_body` translates to the following routine:

```
  CREATE OR REPLACE TABLE FUNCTION APPROVERS_DATASET.query_template1(t1 TABLE, y INT64)
  AS (SELECT * FROM t1 WHERE year > y)
```

Replace `APPROVERS_DATASET` with the ID of the dataset where the template approver creates the routine.

You can [update the query template](https://docs.cloud.google.com/bigquery/docs/query-templates#update-query-template) or [submit the query template for review](https://docs.cloud.google.com/bigquery/docs/query-templates#submit-query-template) .

### Update a query template

You can update a query template only if it's in the **DRAFT** status. After you submit a query template for review, you can no longer modify it.

To update a query template, select one of the following options:

### Console

1.  In the Google Cloud console, go to the **Sharing (Analytics Hub)** page.

2.  Click the display name of the data clean room that contains the query template.

3.  In the clean room, go to the **Templates** tab.

4.  In the row for the template that you want to update, click **Actions \> Edit template** .

5.  Update the description and primary contact as needed.

    > **Note:** You can't update the query template display name after you create the query template.

6.  Click **Next** .

7.  Review the template details.

8.  To save the template without submitting it for review, click **Save** .

> **Note:** You must [authorize the TVF or routine](https://docs.cloud.google.com/bigquery/docs/authorized-routines#authorize_routines) for template subscribers to query the routine. If you modify a routine by running a `CREATE OR REPLACE` statement, such as `CREATE OR REPLACE FUNCTION` , `CREATE OR REPLACE PROCEDURE` , or `CREATE OR REPLACE TABLE FUNCTION` , you must reauthorize the routine.

### API

The following example shows how to update a query template by using the `curl` command:

```
curl -H "Authorization: Bearer $(gcloud auth print-access-token)" \
 -H "Content-Type: application/json" \
 -H 'x-goog-user-project:DCR_PROJECT_ID' \
 -X PATCH "https://analyticshub.googleapis.com/v1/projects/DCR_PROJECT_ID/locations/LOCATION/dataExchanges/CLEAN_ROOM_ID/queryTemplates/QUERY_TEMPLATE_ID?updateMask=description" \
 -d '{
   "description": "New query template"
 }'
```

Replace the following:

- `DCR_PROJECT_ID` : the project ID of the project where the data clean room was created.
- `LOCATION` : the location of the data clean room.
- `CLEAN_ROOM_ID` : the data clean room ID.
- `QUERY_TEMPLATE_ID` : the query template ID.

> **Note:** You can't update the query template display name after you create the query template.

### Submit a query template for review

To submit a query template for review, select one of the following options:

### Console

1.  In the Google Cloud console, go to the **Sharing (Analytics Hub)** page.

2.  Click the display name of the data clean room that contains the query template.

3.  In the clean room, go to the **Templates** tab.

4.  In the row for the template that you want to submit for review, click **Actions \> Submit for review** . The template now has the status of **Requires review** .

    > **Note:** After you submit a query template for review, you can no longer modify it.

    > **Note:** You must [authorize the TVF or routine](https://docs.cloud.google.com/bigquery/docs/authorized-routines#authorize_routines) for template subscribers to query the routine. If you modify a routine by running a `CREATE OR REPLACE` statement, such as `CREATE OR REPLACE FUNCTION` , `CREATE OR REPLACE PROCEDURE` , or `CREATE OR REPLACE TABLE FUNCTION` , you must reauthorize the routine.

### API

The following example shows how to submit a query template for review by using the `curl` command:

```
curl -H "Authorization: Bearer $(gcloud auth print-access-token)" -H "Content-Type: application/json" -H 'x-goog-user-project:DCR_PROJECT_ID' -X POST https://analyticshub.googleapis.com/v1/projects/DCR_PROJECT_ID/locations/LOCATION/dataExchanges/CLEAN_ROOM_ID/queryTemplates/QUERY_TEMPLATE_ID:submit
```

Replace the following:

- `DCR_PROJECT_ID` : the project ID of the project where the data clean room was created.
- `LOCATION` : the location of the data clean room.
- `CLEAN_ROOM_ID` : the data clean room ID.
- `QUERY_TEMPLATE_ID` : the query template ID.

### Delete a query template

You can delete a query template only if it's in the **DRAFT** status. After you submit a query template for review, you can no longer delete it.

To delete a query template, select one of the following options:

### Console

1.  In the Google Cloud console, go to the **Sharing (Analytics Hub)** page.

2.  Click the display name of the data clean room that contains the query template.

3.  In the clean room, go to the **Templates** tab.

4.  In the row for the template that you want to delete, click **Actions \> Delete template** .

### API

The following example shows how to delete a query template by using the `curl` command:

```
curl -H "Authorization: Bearer $(gcloud auth print-access-token)" -H "Content-Type: application/json" -H 'x-goog-user-project:DCR_PROJECT_ID' -X DELETE https://analyticshub.googleapis.com/v1/projects/DCR_PROJECT_ID/locations/LOCATION/dataExchanges/CLEAN_ROOM_ID/queryTemplates/QUERY_TEMPLATE_ID
```

Replace the following:

- `DCR_PROJECT_ID` : the project ID of the project where the data clean room was created.
- `LOCATION` : the location of the data clean room.
- `CLEAN_ROOM_ID` : the data clean room ID.
- `QUERY_TEMPLATE_ID` : the query template ID.

## Template approver workflows

As a query template approver, you can [approve a query template](https://docs.cloud.google.com/bigquery/docs/query-templates#approve-query-template) .

> **Important:** When a query template is submitted for review, all the [data contributors](https://docs.cloud.google.com/bigquery/docs/data-clean-rooms#roles) of the data clean room can view the query template, but only data contributors who have access to the data referenced in the query can approve the template.

When a TVF references data that you don't own—for example, another contributor's data—only that data's owner can approve the query template. If you're creating a TVF that references only your data for sharing in one direction, you can approve the query template yourself.

### Approve a query template

To approve a query template, select one of the following options:

### Console

1.  In the Google Cloud console, go to the **Sharing (Analytics Hub)** page.

2.  Click the display name of the data clean room that contains the query template.

3.  In the clean room, go to the **Templates** tab.

4.  In the row for the template that requires your review, click **Approval Status \> Requires review** .

5.  Click **Approve** .

6.  Select the template location. This location is where the TVF is created for sharing.

7.  Review the proposed query template.

8.  To approve the query template for use in the data clean room, click **Approve** .

### API

1.  Create the routine from the query template by calling the [`jobs.query` method](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query) :

    ```
    curl -H "Authorization: Bearer $(gcloud auth print-access-token)" -H "Content-Type: application/json" -L -X POST https://bigquery.googleapis.com/bigquery/v2/projects/ROUTINE_PROJECT_ID/queries --data '{"query":"ROUTINE_CREATION_QUERY","useLegacySql":false}'
    ```

    Replace the following:

    - `ROUTINE_PROJECT_ID` : the project ID of the project where the routine was created.
    - `ROUTINE_CREATION_QUERY` : the query to create the routine.

2.  Add the routine that you created to the data clean room:

    ```
    curl -H "Authorization: Bearer $(gcloud auth print-access-token)" -H "Content-Type: application/json" -H 'x-goog-user-project:DCR_PROJECT_ID' -X POST https://analyticshub.googleapis.com/v1/projects/DCR_PROJECT_ID/locations/LOCATION/dataExchanges/CLEAN_ROOM_ID/listings?listingId=LISTING_ID -d \
    '{"bigqueryDataset":{"dataset":"projects/PROJECT_ID/datasets/DATASET_ID","selectedResources":[{"routine":"projects/PROJECT_ID/datasets/DATASET_ID/routines/ROUTINE_ID"}]},"displayName":"LISTING_NAME"}'
    ```

    Replace the following:

    - `DCR_PROJECT_ID` : the project ID of the project where the data clean room was created.
    - `LOCATION` : the location of the data clean room.
    - `CLEAN_ROOM_ID` : the data clean room ID.
    - `LISTING_ID` : the listing ID.
    - `PROJECT_ID` : the project ID of the project that contains the source dataset.
    - `DATASET_ID` : the source dataset ID.
    - `ROUTINE_ID` : the routine ID.
    - `LISTING_NAME` : the listing display name.

3.  Update the query template status to `APPROVED` :

    ```
    curl -H "Authorization: Bearer $(gcloud auth print-access-token)" -H "Content-Type: application/json" -L -X POST https://analyticshub.googleapis.com/v1/projects/DCR_PROJECT_ID/locations/LOCATION/dataExchanges/CLEAN_ROOM_ID/queryTemplates/QUERY_TEMPLATE_ID:approve  --data '{}'
    ```

    Replace the following:

    - `DCR_PROJECT_ID` : the project ID of the project where the data clean room was created.
    - `LOCATION` : the location of the data clean room.
    - `CLEAN_ROOM_ID` : the data clean room ID.
    - `QUERY_TEMPLATE_ID` : the query template ID.

### Reject a query template

In the Google Cloud console, you can reject a query template by not approving the submitted query template under review.

## Template subscriber workflows

A query template subscriber can view and subscribe to a data clean room. If only the query template is added to the clean room, subscribing to the clean room grants access only to the corresponding TVF, not to the underlying shared data.

### Subscribe to a query template

To subscribe to a query template, select one of the following options:

### Console

You subscribe to a query template by [subscribing to the data clean room](https://docs.cloud.google.com/bigquery/docs/data-clean-rooms#subscribe_to_a_data_clean_room) . Subscribing grants access to all the listings that have the [**Exclude access to listing from linked dataset** setting disabled](https://docs.cloud.google.com/bigquery/docs/query-templates#add-listing-to-dcr) .

After you subscribe to the data clean room, follow these steps to run a query template:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the **Explorer** pane, go to the linked dataset that you created when you subscribed to the clean room.

3.  Open the routine or TVF that's shared in the linked dataset.

4.  Click **Invoke table function** .

5.  Replace the parameter with the accepted input, which is the table name or a field.

6.  Click **Run** .

If you can't view the TVF nested as a child element of the linked dataset in the **Explorer** pane, you can query the TVF directly on the linked dataset:

```
SELECT * FROM `my_project.dcr_linked_dataset.mytvf`(TABLE myTable);
```

### API

Use the [`projects.locations.dataExchanges.subscribe` method](https://docs.cloud.google.com/bigquery/docs/reference/analytics-hub/rest/v1/projects.locations.dataExchanges/subscribe) .

The following example shows how to call the `projects.locations.dataExchanges.subscribe` method by using the `curl` command:

```
curl -H "Authorization: Bearer $(gcloud auth print-access-token)" -H "Content-Type: application/json" -L -X POST https://analyticshub.googleapis.com/v1/projects/DCR_PROJECT_ID/locations/LOCATION/dataExchanges/CLEAN_ROOM_ID:subscribe  --data '{"destination":"projects/SUBSCRIBER_PROJECT_ID/locations/LOCATION","subscription":"SUBSCRIPTION"}'
```

Replace the following:

- `DCR_PROJECT_ID` : the project ID of the project where the data clean room was created.
- `LOCATION` : the location of the data clean room.
- `CLEAN_ROOM_ID` : the data clean room ID.
- `SUBSCRIBER_PROJECT_ID` : the project ID of the template subscriber project.
- `SUBSCRIPTION` : the name of your subscription.

After you've subscribed to the query template, you can query the TVF directly on the linked dataset:

```
SELECT * FROM `my_project.dcr_linked_dataset.mytvf`(TABLE myTable);
```

## Example scenarios

You can use query templates to facilitate different forms of data collaboration within a data clean room. The following sections describe example scenarios.

### Single-direction sharing scenario

A data publisher creates a query template so that subscribing partners can run only the queries that the publisher defines. Query template creators self-approve the query templates because no other contributor is added to the clean room.

In this scenario, user A is a data clean room owner who creates a data clean room called `campaign_analysis` and adds a dataset named `my_campaign` with a `campaigns` table. User A configures an aggregation threshold policy and metadata controls so that only the metadata schema is visible and template subscribers can't access the source data. User A then creates a query template by defining a TVF from the `campaigns` table, restricting subscribers of the linked dataset to execute only the TVF.

This is the TVF syntax:

```
campaigns_template(t1 TABLE<campaign_ID STRING>) AS (
SELECT WITH AGGREGATION_THRESHOLD company_id, company, sum(impressions) FROM my_project.my_campaign.campaigns
group by company_id, company
);
```

Because user A has the appropriate permissions for the `campaigns` table with the BigQuery Data Owner role, user A can immediately self-approve the query template after submitting it for review.

### Multiple-party collaboration sharing

A clean room owner invites a trusted contributor to propose queries to run against each other's data. Both parties can safely propose queries by viewing only metadata schemas, without accessing the underlying shared data. When a query definition references data that doesn't belong to the template proposer, only that data's owner can approve the query template.

In this scenario, user A invites user B, who is a data clean room contributor, to the `campaign_analysis` clean room. User B wants to propose a query template to join their own data to the `campaigns` table by viewing the table's metadata schema.

This is the TVF syntax:

```
campaigns_template(t1 TABLE<campaign_ID STRING>) AS (
SELECT WITH AGGREGATION_THRESHOLD company_id, company, sum(impressions) FROM my_project.my_campaign.campaigns
group by company_id, company
);
```

Because user B didn't add or doesn't own the `campaigns` table, only user A can approve the query template after it's submitted for review. To use the query template, user B must subscribe to the clean room and invoke the TVF. User B passes their own table with a field named `campaign_ID` as the table parameter, and they can execute the privacy-centric SQL defined in the query template. User B doesn't need to add their data to the clean room.

User B also adds a dataset named `my_transactions` to the clean room that has a `transactions` table and a `products` table. User B configures an aggregation threshold policy and metadata controls so that only the metadata schema is visible and template subscribers can't access the source data.

User A can now propose various query templates to join their own data to the `transactions` table by viewing the table's metadata schema. The following are examples of TVF syntax:

```
transactions_template(t1 TABLE<user_ID STRING>) AS (
SELECT WITH AGGREGATION_THRESHOLD company_id, company, campaign_id, sku, category, date, sum(amount) FROM my_project.my_transactions.transactions
group by company_id, company, campaign_id, sku, category, date
);
```

```
transactions_template_with_join(t1 TABLE<user_ID STRING>) AS (
SELECT WITH AGGREGATION_THRESHOLD t.company_id, t.company, t.campaign_id, t.sku, t.date, p.product_name, p.product_category, sum(t.amount) FROM my_project.my_transactions.transactions t
left join my_project.my_transactions.products p
on t.product_id = p.product_id
group by t.company_id, t.company, t.campaign_id, t.sku, t.date, p.product_name, p.product_category
);
```

> **Note:** Within the TVF query syntax, you can reference only tables owned by the same party. For more details, see [Limitations](https://docs.cloud.google.com/bigquery/docs/query-templates#limitations) .

Because user A didn't add or doesn't own the `transactions` and `products` tables, only user B can approve the query template after it's submitted for review. To use the query template, user A must subscribe to the clean room and invoke the TVF. User A passes their own table with a field named `user_ID` as the table parameter, and they can execute the privacy-centric SQL defined in the query template. User A doesn't need to add their data to the clean room.

## Pricing

The following table summarizes pricing for BigQuery data clean room query templates:

| Role                | Pricing details                                                                                                            |
|---------------------|----------------------------------------------------------------------------------------------------------------------------|
| Data contributor    | Charged only for [data storage](https://cloud.google.com/bigquery/pricing#storage) .                                       |
| Template subscriber | Charged only for [compute (analysis)](https://cloud.google.com/bigquery/pricing#overview_of_pricing) when running queries. |

## What's next

- To learn more about data clean rooms, see [Share sensitive data with data clean rooms](https://docs.cloud.google.com/bigquery/docs/data-clean-rooms) .
- To learn more about subscriptions, see [Subscribe to a data clean room](https://docs.cloud.google.com/bigquery/docs/data-clean-rooms#subscribe_to_a_data_clean_room) .
- To learn more about TVFs, see [Table functions](https://docs.cloud.google.com/bigquery/docs/table-functions) .
- To learn more about data egress for BigQuery shared datasets, see [Data egress options](https://docs.cloud.google.com/bigquery/docs/analytics-hub-introduction#data_egress) .
