---
name: documents/docs.cloud.google.com/bigquery/docs/information-schema-recommendations
uri: https://docs.cloud.google.com/bigquery/docs/information-schema-recommendations
title: INFORMATION_SCHEMA.RECOMMENDATIONS view
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# INFORMATION_SCHEMA.RECOMMENDATIONS view

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

To request feedback or support for this feature, send email to <bq-recommendations+feedback@google.com> .

The `INFORMATION_SCHEMA.RECOMMENDATIONS` view contains data about all BigQuery recommendations in the current project. BigQuery retrieves recommendations for all BigQuery recommenders from the Active Assist and present it in this view.

The `INFORMATION_SCHEMA.RECOMMENDATIONS` view supports the following recommendations:

- [Partition & cluster recommendations](https://docs.cloud.google.com/bigquery/docs/view-partition-cluster-recommendations)
- [Materialized view recommendations](https://docs.cloud.google.com/bigquery/docs/manage-materialized-recommendations)
- [Role recommendations for BigQuery datasets](https://docs.cloud.google.com/policy-intelligence/docs/review-apply-role-recommendations-datasets)

The `INFORMATION_SCHEMA.RECOMMENDATIONS` view shows only BigQuery-related recommendations. You can view Google Cloud recommendations in the Active Assist.

## Required permission

To view recommendations with the `INFORMATION_SCHEMA.RECOMMENDATIONS` view, you must have the required permissions for the corresponding recommender. The `INFORMATION_SCHEMA.RECOMMENDATIONS` view only returns recommendations that you have permission to view.

Ask your administrator to grant access to view the recommendations. To see the required permissions for each recommender, see the following:

- [Partition & cluster recommender permissions](https://docs.cloud.google.com/bigquery/docs/view-partition-cluster-recommendations#required_permissions)
- [Materialized view recommendations permissions](https://docs.cloud.google.com/bigquery/docs/manage-materialized-recommendations#required_permissions)
- [Role recommendations for datasets permissions](https://docs.cloud.google.com/policy-intelligence/docs/review-apply-role-recommendations-datasets#required-permissions)

## Schema

The `INFORMATION_SCHEMA.RECOMMENDATIONS` view has the following schema:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Column name</th>
<th>Data type</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>recommendation_id</code></td>
<td><code>STRING</code></td>
<td>Base64 encoded ID that contains the RecommendationID and recommender.</td>
</tr>
<tr class="even">
<td><code>recommender</code></td>
<td><code>STRING</code></td>
<td>The type of recommendation. For example, <code>google.bigquery.table.PartitionClusterRecommender</code> for partitioning and clustering recommendations.</td>
</tr>
<tr class="odd">
<td><code>subtype</code></td>
<td><code>STRING</code></td>
<td>The subtype of the recommendation.</td>
</tr>
<tr class="even">
<td><code>project_id</code></td>
<td><code>STRING</code></td>
<td>The ID of the project.</td>
</tr>
<tr class="odd">
<td><code>project_number</code></td>
<td><code>STRING</code></td>
<td>The number of the project.</td>
</tr>
<tr class="even">
<td><code>description</code></td>
<td><code>STRING</code></td>
<td>The description about the recommendation.</td>
</tr>
<tr class="odd">
<td><code>last_updated_time</code></td>
<td><code>TIMESTAMP</code></td>
<td>This field represents the time when the recommendation was last created.</td>
</tr>
<tr class="even">
<td><code>target_resources</code></td>
<td><code>STRING</code></td>
<td>Fully qualified resource names this recommendation is targeting.</td>
</tr>
<tr class="odd">
<td><code>state</code></td>
<td><code>STRING</code></td>
<td>The state of the recommendation. For a list of possible values, see <a href="https://docs.cloud.google.com/recommender/docs/reference/rest/v1/billingAccounts.locations.recommenders.recommendations#state">State</a> .</td>
</tr>
<tr class="even">
<td><code>primary_impact</code></td>
<td><code>RECORD</code></td>
<td>The impact this recommendation can have when trying to optimize the primary category. Contains the following fields:
<ul>
<li><code>category</code> : The category this recommendation is trying to optimize. For a list of possible values, see <a href="https://docs.cloud.google.com/recommender/docs/reference/rest/v1/billingAccounts.locations.recommenders.recommendations#category">Category</a> .</li>
<li><code>cost_projection</code> : This value may be populated if the recommendation can project the cost savings from this recommendation. Only present when the category is <code>COST</code> .</li>
<li><code>security_projection</code> : Might be present when the category is <code>SECURITY</code> .</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>priority</code></td>
<td><code>STRING</code></td>
<td>The priority of the recommendation. For a list of possible values, see <a href="https://docs.cloud.google.com/recommender/docs/reference/rest/v1/billingAccounts.locations.recommenders.recommendations#priority">Priority</a> .</td>
</tr>
<tr class="even">
<td><code>associated_insight_ids</code></td>
<td><code>STRING</code></td>
<td>Full Insight names associated with the recommendation. Insight name is the Base64 encoded representation of Insight type name &amp; the Insight ID. This can be used to query Insights view.</td>
</tr>
<tr class="odd">
<td><code>additional_details</code></td>
<td><code>RECORD</code></td>
<td>Additional Details about the recommendation.
<ul>
<li><code>overview</code> : Overview of the recommendation in JSON format. The content of this field might change based on the recommender.</li>
<li><code>state_metadata</code> : Metadata about the state of the recommendation in key-value pairs.</li>
<li><code>operations</code> : List of operations the user can perform on the target resources. This contains the following fields:
<ul>
<li><code>action</code> : The type of action the user must perform. This can be a free-text set by the system while generating the recommendation. Will always be populated.</li>
<li><code>resource_type</code> : The cloud resource type.</li>
<li><code>resource</code> : Fully qualified resource name.</li>
<li><code>path</code> : Path of the target field relative to the resource.</li>
<li><code>value</code> : Value of the path field.</li>
</ul></li>
</ul></td>
</tr>
</tbody>
</table>

For stability, we recommend that you explicitly list columns in your information schema queries instead of using a wildcard ( `SELECT *` ). Explicitly listing columns prevents queries from breaking if the underlying schema changes.

## Scope and syntax

Queries against this view must include a [region qualifier](https://docs.cloud.google.com/bigquery/docs/information-schema-intro#syntax) . A project ID is optional. If no project ID is specified, the project that the query runs in is used.

| View name                                                                                              | Resource scope | Region scope |
|--------------------------------------------------------------------------------------------------------|----------------|--------------|
| `[ `` PROJECT_ID ```  .]`region-  ``` REGION ```  `.INFORMATION_SCHEMA.RECOMMENDATIONS[_BY_PROJECT] `` | Project level  | `REGION`     |

Replace the following:

- Optional: `PROJECT_ID` : the ID of your Google Cloud project. If not specified, the default project is used.

- `REGION` : any [dataset region name](https://docs.cloud.google.com/bigquery/docs/locations) . For example, `` `region-us` `` .

  > **Note:** You must use [a region qualifier](https://docs.cloud.google.com/bigquery/docs/information-schema-intro#region_qualifier) to query `INFORMATION_SCHEMA` views. The location of the query execution must match the region of the `INFORMATION_SCHEMA` view.

## Example

To run the query against a project other than your default project, add the project ID in the following format:

```
`PROJECT_ID`.`region-REGION_NAME`.INFORMATION_SCHEMA.RECOMMENDATIONS
```

Replace the following:

- `PROJECT_ID` : the ID of the project.
- `REGION_NAME` : the region for your project.

For example, `` `myproject`.`region-us`.INFORMATION_SCHEMA.RECOMMENDATIONS `` .

### View top cost saving recommendations

The following example returns top 3 `COST` category recommendations on the basis of the projected `slot_hours_saved_monthly` :

```
SELECT
   recommender,
   target_resources,
   LAX_INT64(additional_details.overview.bytesSavedMonthly) / POW(1024, 3) as est_gb_saved_monthly,
   LAX_INT64(additional_details.overview.slotMsSavedMonthly) / (1000 * 3600) as slot_hours_saved_monthly,
  last_updated_time
FROM
  `region-us`.INFORMATION_SCHEMA.RECOMMENDATIONS_BY_PROJECT
WHERE
   primary_impact.category = 'COST'
AND
   state = 'ACTIVE'
ORDER by
   slot_hours_saved_monthly DESC
LIMIT 3;
```

> **Note:** `INFORMATION_SCHEMA` view names are case sensitive.

The result is similar to the following:

```
+---------------------------------------------------+--------------------------------------------------------------------------------------------------+
|                    recommender                    |   target_resources      | est_gb_saved_monthly | slot_hours_saved_monthly |  last_updated_time
+---------------------------------------------------+--------------------------------------------------------------------------------------------------+
| google.bigquery.materializedview.Recommender      | ["project_resource"]    | 140805.38289248943   |        9613.139166666666 |  2024-07-01 13:00:00
| google.bigquery.table.PartitionClusterRecommender | ["table_resource_1"]    | 4393.7416711859405   |        56.61476777777777 |  2024-07-01 13:00:00
| google.bigquery.table.PartitionClusterRecommender | ["table_resource_2"]    |   3934.07264107652   |       10.499466666666667 |  2024-07-01 13:00:00
+---------------------------------------------------+--------------------------------------------------------------------------------------------------+
```
