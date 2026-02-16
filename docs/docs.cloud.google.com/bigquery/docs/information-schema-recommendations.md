# INFORMATION\_SCHEMA.RECOMMENDATIONS view

**Preview**

This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

To request feedback or support for this feature, send email to <bq-recommendations+feedback@google.com> .

The `  INFORMATION_SCHEMA.RECOMMENDATIONS  ` view contains data about all BigQuery recommendations in the current project. BigQuery retrieves recommendations for all BigQuery recommenders from the Active Assist and present it in this view.

The `  INFORMATION_SCHEMA.RECOMMENDATIONS  ` view supports the following recommendations:

  - [Partition & cluster recommendations](/bigquery/docs/view-partition-cluster-recommendations)
  - [Materialized view recommendations](/bigquery/docs/manage-materialized-recommendations)
  - [Role recommendations for BigQuery datasets](/policy-intelligence/docs/review-apply-role-recommendations-datasets)

The `  INFORMATION_SCHEMA.RECOMMENDATIONS  ` view shows only BigQuery-related recommendations. You can view Google Cloud recommendations in the Active Assist.

## Required permission

To view recommendations with the `  INFORMATION_SCHEMA.RECOMMENDATIONS  ` view, you must have the required permissions for the corresponding recommender. The `  INFORMATION_SCHEMA.RECOMMENDATIONS  ` view only returns recommendations that you have permission to view.

Ask your administrator to grant access to view the recommendations. To see the required permissions for each recommender, see the following:

  - [Partition & cluster recommender permissions](/bigquery/docs/view-partition-cluster-recommendations#required_permissions)
  - [Materialized view recommendations permissions](/bigquery/docs/manage-materialized-recommendations#required_permissions)
  - [Role recommendations for datasets permissions](/policy-intelligence/docs/review-apply-role-recommendations-datasets#required-permissions)

## Schema

The `  INFORMATION_SCHEMA.RECOMMENDATIONS  ` view has the following schema:

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
<td><code dir="ltr" translate="no">       recommendation_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Base64 encoded ID that contains the RecommendationID and recommender.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       recommender      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The type of recommendation. For example, <code dir="ltr" translate="no">       google.bigquery.table.PartitionClusterRecommender      </code> for partitioning and clustering recommendations.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       subtype      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The subtype of the recommendation.</td>
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
<td>This field represents the time when the recommendation was last created.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       target_resources      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Fully qualified resource names this recommendation is targeting.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       state      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The state of the recommendation. For a list of possible values, see <a href="/recommender/docs/reference/rest/v1/billingAccounts.locations.recommenders.recommendations#state">State</a> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       primary_impact      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
<td>The impact this recommendation can have when trying to optimize the primary category. Contains the following fields:
<ul>
<li><code dir="ltr" translate="no">         category        </code> : The category this recommendation is trying to optimize. For a list of possible values, see <a href="/recommender/docs/reference/rest/v1/billingAccounts.locations.recommenders.recommendations#category">Category</a> .</li>
<li><code dir="ltr" translate="no">         cost_projection        </code> : This value may be populated if the recommendation can project the cost savings from this recommendation. Only present when the category is <code dir="ltr" translate="no">         COST        </code> .</li>
<li><code dir="ltr" translate="no">         security_projection        </code> : Might be present when the category is <code dir="ltr" translate="no">         SECURITY        </code> .</li>
</ul></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       priority      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>The priority of the recommendation. For a list of possible values, see <a href="/recommender/docs/reference/rest/v1/billingAccounts.locations.recommenders.recommendations#priority">Priority</a> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       associated_insight_ids      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Full Insight names associated with the recommendation.Insight name is the Base64 encoded representation of Insight type name &amp; the Insight ID. This can be used to query Insights view.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       additional_details      </code></td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
<td>Additional Details about the recommendation.
<code dir="ltr" translate="no">         overview        </code> : Overview of the recommendation in JSON format. The content of this field might change based on the recommender.
<code dir="ltr" translate="no">         state_metadata        </code> : Metadata about the state of the recommendation in key-value pairs.
<code dir="ltr" translate="no">         operations        </code> : List of operations the user can perform on the target resources. This contains the following fields:
<ul>
<li><code dir="ltr" translate="no">          action         </code> : The type of action the user must perform. This can be a free-text set by the system while generating the recommendation. Will always be populated.</li>
<li><code dir="ltr" translate="no">          resource_type         </code> : The cloud resource type.</li>
<li><code dir="ltr" translate="no">          resource         </code> : Fully qualified resource name.</li>
<li><code dir="ltr" translate="no">          path         </code> : Path of the target field relative to the resource.</li>
<li><code dir="ltr" translate="no">          value         </code> : Value of the path field.</li>
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
<td><code dir="ltr" translate="no">       [               PROJECT_ID              .]`region-               REGION              `.INFORMATION_SCHEMA.RECOMMENDATIONS[_BY_PROJECT]      </code></td>
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
`PROJECT_ID`.`region-REGION_NAME`.INFORMATION_SCHEMA.RECOMMENDATIONS
```

Replace the following:

  - `  PROJECT_ID  ` : the ID of the project.
  - `  REGION_NAME  ` : the region for your project.

For example, ``  `myproject`.`region-us`.INFORMATION_SCHEMA.RECOMMENDATIONS  `` .

### View top cost saving recommendations

The following example returns top 3 `  COST  ` category recommendations on the basis of the projected `  slot_hours_saved_monthly  ` :

``` text
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

**Note:** `  INFORMATION_SCHEMA  ` view names are case sensitive.

The result is similar to the following:

``` text
+---------------------------------------------------+--------------------------------------------------------------------------------------------------+
|                    recommender                    |   target_resources      | est_gb_saved_monthly | slot_hours_saved_monthly |  last_updated_time
+---------------------------------------------------+--------------------------------------------------------------------------------------------------+
| google.bigquery.materializedview.Recommender      | ["project_resource"]    | 140805.38289248943   |        9613.139166666666 |  2024-07-01 13:00:00
| google.bigquery.table.PartitionClusterRecommender | ["table_resource_1"]    | 4393.7416711859405   |        56.61476777777777 |  2024-07-01 13:00:00
| google.bigquery.table.PartitionClusterRecommender | ["table_resource_2"]    |   3934.07264107652   |       10.499466666666667 |  2024-07-01 13:00:00
+---------------------------------------------------+--------------------------------------------------------------------------------------------------+
```
