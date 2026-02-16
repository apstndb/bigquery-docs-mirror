# INFORMATION\_SCHEMA.INSIGHTS view

**Preview**

This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

To request feedback or support for this feature, send email to <bq-recommendations+feedback@google.com> .

The `  INFORMATION_SCHEMA.INSIGHTS  ` view contains insights about all BigQuery recommendations in the current project. BigQuery retrieves insights for all BigQuery insight types from the Active Assist and present it in this view. BigQuery insights are always associated with a recommendation.

The `  INFORMATION_SCHEMA.INSIGHTS  ` view supports the following recommendations:

  - [Partition and cluster recommendations](/bigquery/docs/view-partition-cluster-recommendations)
  - [Materialized view recommendations](/bigquery/docs/manage-materialized-recommendations)
  - [Role recommendations for BigQuery datasets](/policy-intelligence/docs/review-apply-role-recommendations-datasets)

## Required permission

To view insights with the `  INFORMATION_SCHEMA.INSIGHTS  ` view, you must have the required permissions for the corresponding recommender. The `  INFORMATION_SCHEMA.INSIGHTS  ` view only returns insights from recommendations that you have permission to view.

Ask your administrator to grant access to view insights. To see the required permissions for each recommender, see the following:

  - [Partition & cluster recommender permissions](/bigquery/docs/view-partition-cluster-recommendations#required_permissions)
  - [Materialized view recommendations permissions](/bigquery/docs/manage-materialized-recommendations#required_permissions)
  - [Role recommendations for datasets permissions](/policy-intelligence/docs/review-apply-role-recommendations-datasets#required-permissions)

## Schema

The `  INFORMATION_SCHEMA.INSIGHTS  ` view has the following schema:

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
<td><code dir="ltr" translate="no">       insight_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Base64 encoded ID that contains the insight type and insight ID</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       insight_type      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The type of the Insight. For example, <code dir="ltr" translate="no">       google.bigquery.materializedview.Insight      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       subtype      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The subtype of the insight.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       project_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The ID of the project.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       project_number      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The number of the project.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       description      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The description about the recommendation.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       last_updated_time      </code></td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td>This field represents the time when the insight was last refreshed.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       category      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The optimization category of the impact.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       target_resources      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Fully qualified resource names this insight is targeting.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       state      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The state of the insight. For a list of possible values, see <a href="/recommender/docs/reference/rest/v1/billingAccounts.locations.insightTypes.insights#Insight.State">Value</a> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       severity      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The severity of the Insight. For a list of possible values, see <a href="/recommender/docs/reference/rest/v1/billingAccounts.locations.insightTypes.insights#severity">Severity</a> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       associated_recommendation_ids      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Full recommendation names this insight is associated with. Recommendation name is the Base64 encoded representation of recommender type and the recommendations ID.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       additional_details      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
<td>Additional details about the insight.
<ul>
<li><code dir="ltr" translate="no">         content        </code> : Insight content in JSON format.</li>
<li><code dir="ltr" translate="no">         state_metadata        </code> : Metadata about the state of the Insight. Contains key-value pairs.</li>
<li><code dir="ltr" translate="no">         observation_period_seconds        </code> : Observation Period for generating the insight.</li>
</ul></td>
</tr>
</tbody>
</table>

For stability, we recommend that you explicitly list columns in your information schema queries instead of using a wildcard ( `  SELECT *  ` ). Explicitly listing columns prevents queries from breaking if the underlying schema changes.

## Scope and syntax

Queries against this view must include a [region qualifier](/bigquery/docs/information-schema-intro#syntax) . A project ID is optional. If no project ID is specified, the project that the query runs in is used.

<table>
<thead>
<tr class="header">
<th>View name</th>
<th>Resource scope</th>
<th>Region scope</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]`region-               REGION              `.INFORMATION_SCHEMA.INSIGHTS[_BY_PROJECT]      </code></td>
<td>Project level</td>
<td><code dir="ltr" translate="no">         REGION       </code></td>
</tr>
</tbody>
</table>

Replace the following:

  - Optional: `  PROJECT_ID  ` : the ID of your Google Cloud project. If not specified, the default project is used.
  - `  REGION  ` : any [dataset region name](/bigquery/docs/locations) . For example, ``  `region-us`  `` .
    **Note:** You must use [a region qualifier](/bigquery/docs/information-schema-intro#region_qualifier) to query `  INFORMATION_SCHEMA  ` views. The location of the query execution must match the region of the `  INFORMATION_SCHEMA  ` view.

## Example

To run the query against a project other than your default project, add the project ID in the following format:

``` text
`PROJECT_ID`.`region-REGION_NAME`.INFORMATION_SCHEMA.INSIGHTS
```

Replace the following:

  - `  PROJECT_ID  ` : the ID of the project.
  - `  REGION_NAME  ` : the region for your project.

For example, ``  `myproject`.`region-us`.INFORMATION_SCHEMA.INSIGHTS  `` .

### View active insights with cost savings

The following example joins insights view with the recommendations view to return 3 recommendations for the insights that are ACTIVE in COST category:

``` text
WITH 
 insights as (SELECT * FROM `region-us`.INFORMATION_SCHEMA.INSIGHTS),
 recs as (SELECT recommender, recommendation_id, additional_details FROM `region-us`.INFORMATION_SCHEMA.RECOMMENDATIONS)

SELECT  
   recommender,
   target_resources,
   LAX_INT64(recs.additional_details.overview.bytesSavedMonthly) / POW(1024, 3) as est_gb_saved_monthly,
   LAX_INT64(recs.additional_details.overview.slotMsSavedMonthly) / (1000 * 3600) as slot_hours_saved_monthly,
   insights.additional_details.observation_period_seconds / 86400 as observation_period_days,
   last_updated_time
FROM 
  insights 
JOIN recs 
ON 
  recommendation_id in UNNEST(associated_recommendation_ids) 
WHERE 
  state = 'ACTIVE' 
AND
  category = 'COST'
LIMIT 3;
```

**Note:** `  INFORMATION_SCHEMA  ` view names are case sensitive.

The result is similar to the following:

``` text
+---------------------------------------------------+---------------------+--------------------+--------------------------+-------------------------+---------------------+
|                    recommender                    |   target_resource   |  gb_saved_monthly  | slot_hours_saved_monthly | observation_period_days |  last_updated_time  |
+---------------------------------------------------+---------------------+--------------------+--------------------------+-------------------------+---------------------+
| google.bigquery.table.PartitionClusterRecommender | ["table_resource1"] |   3934.07264107652 |       10.499466666666667 |                    30.0 | 2024-07-01 16:41:25 |
| google.bigquery.table.PartitionClusterRecommender | ["table_resource2"] | 4393.7416711859405 |        56.61476777777777 |                    30.0 | 2024-07-01 16:41:25 |
| google.bigquery.materializedview.Recommender      | ["project_resource"]| 140805.38289248943 |        9613.139166666666 |                     2.0 | 2024-07-01 13:00:31 |
+---------------------------------------------------+---------------------+--------------------+--------------------------+-------------------------+---------------------+
```
