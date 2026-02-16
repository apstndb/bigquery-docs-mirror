# Manage materialized view recommendations

**Preview**

This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

**Note:** To request access to this preview feature, complete the [Materialized view recommendations sign-up form](https://forms.gle/M3V75cWZZsHmDBCr6) . It might take up to a week from the request being accepted to when you can view your materialized view recommendations. To provide feedback or ask questions that are related to this preview release, contact <bq-mv-help@google.com> .

This document describes how the materialized view recommender works, and also shows you how to view and apply any materialized view recommendations.

## Introduction

The BigQuery materialized view recommender can help you improve workload performance and save workload execution cost. These recommendations are based on historical query execution characteristics from the past 30 days.

[Materialized views](/bigquery/docs/materialized-views-intro) are precomputed views that periodically cache the results of a query for increased performance and efficiency. Materialized views use [smart tuning](/bigquery/docs/materialized-views-use#smart_tuning) to transparently rewrite queries against source tables to use existing materialized views for better performance and efficiency.

### How the recommender works

The recommender generates recommendations daily for each project that executes query jobs in BigQuery. Recommendations are based on the analysis of the workload execution over the past 30 days. The materialized view recommender looks for repetitive query patterns and computes any savings that could be made if the repetitive subquery could be moved to an incremental materialized view. The recommender takes into account any savings at query time and account maintenance cost for the materialized view. If these combined factors show a significant positive outcome, then the recommender makes a recommendation.

Consider the following query example:

``` text
WITH revenue   AS
(SELECT l_suppkey as supplier_no,
        sum(l_extendedprice * (1 - l_discount)) as total_revenue
  FROM lineitem
  WHERE
    l_shipdate >= date '1996-01-01'
    AND l_shipdate < date_add(date '1996-01-01', interval 3 MONTH)
  GROUP BY l_suppkey)
SELECT s_suppkey,
      s_name,
      s_address,
      s_phone,
      total_revenue
FROM
supplier,
revenue
WHERE s_suppkey = supplier_no
AND total_revenue =
  (SELECT max(total_revenue)
    FROM revenue)
ORDER BY s_suppkey
```

This query example shows information about the top supplier. The query contains a common table expression (CTE) named `  revenue  ` which represents the total revenue per every supplier ( `  l_suppkey  ` ). `  revenue  ` is joined with the supplier table on the condition that the supplier's `  total_revenue  ` matches `  max(total_revenue)  ` across all suppliers. As a result, the query computes information ( `  l_suppkey  ` , `  s_name  ` , `  s_address  ` , `  s_phone  ` , `  total_revenue  ` ) about the supplier with the maximum total revenue.

The whole query itself is too complicated to be put into an incremental materialized view. However, the `  supplier  ` CTE is an aggregation over a single table — a query pattern which is supported by incremental materialized views. The `  supplier  ` CTE is also the most computationally expensive part of the query. Therefore, if the example query was run repeatedly over constantly changing source tables, then the materialized view recommender might suggest putting the `  supplier  ` CTE into a materialized view. The materialized view recommendation for the preceding sample query might look similar to the following:

``` text
CREATE MATERIALIZED VIEW mv AS
SELECT l_suppkey as supplier_no,
         sum(l_extendedprice * (1 - l_discount)) as total_revenue
  FROM lineitem
  WHERE
    l_shipdate >= date '1996-01-01'
    AND l_shipdate < date_add(date '1996-01-01', interval 3 MONTH)
  GROUP BY l_suppkey
```

The Recommender API also returns query execution information in the form of *insights* . [Insights](/recommender/docs/insights/using-insights) are findings that help you understand your project's workload, providing more context on how a materialized view recommendation might improve workload costs.

## Limitations

  - The materialized view recommender doesn't support the standard process to [opt out of data processing](/recommender/docs/opt-out) . To stop receiving materialized view recommendations, follow the instructions in the [Materialized view recommendations sign-up form](https://forms.gle/M3V75cWZZsHmDBCr6) .
  - The materialized view recommendations can't be [exported to BigQuery](/recommender/docs/bq-export/export-recommendations-to-bq) .

## Before you begin

Before you can view or apply materialized view recommendations, you need to [enable the Recommender API](/recommender/docs/enabling) .

### Required permissions

To get the permissions that you need to access materialized view recommendations, ask your administrator to grant you the [BigQuery Materialized View Recommender Viewer](/iam/docs/roles-permissions/recommender#recommender.bigqueryMaterializedViewViewer) ( `  roles/recommender.bigqueryMaterializedViewViewer  ` ) IAM role. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

This predefined role contains the permissions required to access materialized view recommendations. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to access materialized view recommendations:

  - `  recommender.bigqueryMaterializedViewRecommendations.get  `
  - `  recommender.bigqueryMaterializedViewRecommendations.list  `

You might also be able to get these permissions with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

For more information about IAM roles and permissions in BigQuery, see [Introduction to IAM](/bigquery/docs/access-control) .

## View materialized view recommendations

This section describes how to view materialized view recommendations and insights using the Google Cloud console, the Google Cloud CLI or the Recommender API.

Select one of the following options:

### Console

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the navigation menu, click **Recommendations** .

3.  The **BigQuery Recommendations** pane opens. Under **Optimize BigQuery workload cost** , click **View details** .

4.  A recommendation list appears, showing all recommendations generated for the current project. To see more information about a specific materialized view recommendation or table insight, click **Details** .

Alternatively, you can view all recommendations available for your project or organization by clicking **Recommendations** in the navigation menu.

### gcloud

To view materialized view recommendations for a specific project, use the [`  gcloud recommender recommendations list  ` command](/sdk/gcloud/reference/recommender/recommendations/list) :

``` text
gcloud recommender recommendations list \
    --project=PROJECT_NAME \
    --location=REGION_NAME \
    --recommender=google.bigquery.materializedview.Recommender \
    --format=FORMAT_TYPE \
```

Replace the following:

  - `  PROJECT_NAME  ` : the name of the project that executes query jobs
  - `  REGION_NAME  ` : the region in which query jobs are executed
  - `  FORMAT_TYPE  ` : a supported [gcloud CLI output format](/sdk/gcloud/reference#--format) —for example, JSON

The following table describes the important fields from the \`recommendations\` response:

<table>
<thead>
<tr class="header">
<th>Property</th>
<th>Relevant for subtype</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         recommenderSubtype        </code></td>
<td><code dir="ltr" translate="no">         CREATE_MATERIALIZED_VIEW        </code></td>
<td>The type of recommendation.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         content.overview.sql        </code></td>
<td><code dir="ltr" translate="no">         CREATE_MATERIALIZED_VIEW        </code></td>
<td>Suggested DDL statement that creates a materialized view.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         content.overview.slotMsSavedMonthly        </code></td>
<td><code dir="ltr" translate="no">         CREATE_MATERIALIZED_VIEW        </code></td>
<td>Estimated slot milliseconds to be saved monthly by suggested view.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         content.overview.bytesSavedMonthly        </code></td>
<td><code dir="ltr" translate="no">         CREATE_MATERIALIZED_VIEW        </code></td>
<td>Estimated bytes scanned to be saved monthly by suggested view.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         content.overview.baseTables        </code></td>
<td><code dir="ltr" translate="no">         CREATE_MATERIALIZED_VIEW        </code></td>
<td>Reserved for future use.</td>
</tr>
</tbody>
</table>

  - For more information about other fields in the `  recommendations  ` response, see [REST Resource: `  projects.locations.recommenders.recommendation  `](/recommender/docs/reference/rest/v1/projects.locations.recommenders.recommendations#resource:-recommendation) .
  - For more information about using the Recommender API, see [Using the API - Recommendations](/recommender/docs/using-api) .

To view insights that prompted materialized view recommendations using the gcloud CLI, use the [`  gcloud recommender insights list  ` command](/sdk/gcloud/reference/recommender/insights/list) :

``` text
gcloud recommender insights list \
    --project=PROJECT_NAME \
    --location=REGION_NAME \
    --insight-type=google.bigquery.materializedview.Insight \
    --format=FORMAT_TYPE \
```

Replace the following:

  - `  PROJECT_NAME  ` : the name of the project that executes query jobs
  - `  REGION_NAME  ` : the region in which query jobs are executed
  - `  FORMAT_TYPE  ` : a supported [gcloud CLI output format](/sdk/gcloud/reference#--format) —for example, JSON

The following table describes the important fields from the insights API response:

<table>
<thead>
<tr class="header">
<th>Property</th>
<th>Relevant for subtype</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         content.queryCount        </code></td>
<td><code dir="ltr" translate="no">         CREATE_MATERIALIZED_VIEW        </code></td>
<td>Number of queries in the observation period with repetitive pattern that can be optimized using materialized view.</td>
</tr>
</tbody>
</table>

  - For more information about other fields in the insights response, see [REST Resource: `  projects.locations.insightTypes.insights  `](/recommender/docs/reference/rest/v1/projects.locations.insightTypes.insights#resource:-insight) .
  - For more information about using insights, see [Using the API - Insights](/recommender/docs/insights/using-api) .

### REST API

To view materialized view recommendations for a specific project, use the REST API. With each command, you must provide an authentication token, which you can get using the gcloud CLI. For more information about getting an authentication token, see [Methods for getting an ID token](/docs/authentication/get-id-token) .

You can use the `  curl list  ` request to view all recommendations for a specific project:

``` text
$ curl
-H "Authorization: Bearer $(gcloud auth print-access-token)"
-H "x-goog-user-project: PROJECT_NAME" https://recommender.googleapis.com/v1/projects/PROJECT_NAME/locations/LOCATION/recommenders/google.bigquery.materializedview.Recommender/recommendations
```

Replace the following:

  - `  PROJECT_NAME  ` : the name of the project containing your BigQuery table
  - `  LOCATION  ` : the location where the project is located.

The following table describes the important fields from the \`recommendations\` response:

<table>
<thead>
<tr class="header">
<th>Property</th>
<th>Relevant for subtype</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         recommenderSubtype        </code></td>
<td><code dir="ltr" translate="no">         CREATE_MATERIALIZED_VIEW        </code></td>
<td>The type of recommendation.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         content.overview.sql        </code></td>
<td><code dir="ltr" translate="no">         CREATE_MATERIALIZED_VIEW        </code></td>
<td>Suggested DDL statement that creates a materialized view.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         content.overview.slotMsSavedMonthly        </code></td>
<td><code dir="ltr" translate="no">         CREATE_MATERIALIZED_VIEW        </code></td>
<td>Estimated slot milliseconds to be saved monthly by suggested view.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">         content.overview.bytesSavedMonthly        </code></td>
<td><code dir="ltr" translate="no">         CREATE_MATERIALIZED_VIEW        </code></td>
<td>Estimated bytes scanned to be saved monthly by suggested view.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">         content.overview.baseTables        </code></td>
<td><code dir="ltr" translate="no">         CREATE_MATERIALIZED_VIEW        </code></td>
<td>Reserved for future use.</td>
</tr>
</tbody>
</table>

  - For more information about other fields in the `  recommendations  ` response, see [REST Resource: `  projects.locations.recommenders.recommendation  `](/recommender/docs/reference/rest/v1/projects.locations.recommenders.recommendations#resource:-recommendation) .
  - For more information about using the Recommender API, see [Using the API - Recommendations](/recommender/docs/using-api) .

To view insights that prompted materialized view recommendations using REST API run the following command:

``` text
$ curl
-H "Authorization: Bearer $(gcloud auth print-access-token)"
-H "x-goog-user-project: PROJECT_NAME" https://recommender.googleapis.com/v1/projects/PROJECT_NAME/locations/LOCATION/insightTypes/google.bigquery.materializedview.Insight/insights
```

Replace the following:

  - `  PROJECT_NAME  ` : the name of the project containing your BigQuery table
  - `  LOCATION  ` : the location where the project is located.

The following table describes the important fields from the insights API response:

<table>
<thead>
<tr class="header">
<th>Property</th>
<th>Relevant for subtype</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         content.queryCount        </code></td>
<td><code dir="ltr" translate="no">         CREATE_MATERIALIZED_VIEW        </code></td>
<td>Number of queries in the observation period with repetitive pattern that can be optimized using materialized view.</td>
</tr>
</tbody>
</table>

  - For more information about other fields in the insights response, see [REST Resource: `  projects.locations.insightTypes.insights  `](/recommender/docs/reference/rest/v1/projects.locations.insightTypes.insights#resource:-insight) .
  - For more information about using insights, see [Using the API - Insights](/recommender/docs/insights/using-api) .

### View recommendations with `     INFORMATION_SCHEMA    `

You can also view your recommendations and insights using `  INFORMATION_SCHEMA  ` views. For example, you can use the `  INFORMATION_SCHEMA.RECOMMENDATIONS  ` view to view your top three recommendations based on slots savings, as seen in the following example:

``` text
SELECT
   recommender,
   target_resources,
   LAX_INT64(additional_details.overview.bytesSavedMonthly) / POW(1024, 3) as est_gb_saved_monthly,
   LAX_INT64(additional_details.overview.slotMsSavedMonthly) / (1000 * 3600) as slot_hours_saved_monthly,
  last_updated_time
FROM
  `region-us`.INFORMATION_SCHEMA.RECOMMENDATIONS
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

For more information, see the following resources:

  - [`  INFORMATION_SCHEMA.RECOMMENDATIONS  ` view](/bigquery/docs/information-schema-recommendations)
  - [`  INFORMATION_SCHEMA.RECOMMENDATIONS_BY_ORGANIZATION  ` view](/bigquery/docs/information-schema-recommendations-by-org)
  - [`  INFORMATION_SCHEMA.INSIGHTS  ` view](/bigquery/docs/information-schema-insights)

## Apply materialized view recommendations

You can apply a recommendation to create a materialized view by executing the suggested `  CREATE MATERIALIZED VIEW  ` type DDL statement in the Google Cloud console.

**Note:** To execute the suggested `  CREATE MATERIALIZED VIEW  ` DDL statement, you must have the [required permissions](/bigquery/docs/materialized-views-create#required_permissions) in all the following locations:

  - The query project
  - The dataset containing the source tables
  - The dataset containing the materialized view

<!-- end list -->

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the navigation menu, click **Recommendations** .

3.  The **BigQuery Recommendations** pane opens. Under **Optimize BigQuery workload cost** , click **View details** .

4.  A recommendation list appears, showing all recommendations generated for the current project or organization, depending on the selected scope. Locate a materialized view recommendation and click **Details** .

5.  Click **View in BigQuery Studio** . A SQL editor opens containing a `  CREATE MATERIALIZED VIEW  ` DDL statement.

6.  In the provided `  CREATE MATERIALIZED VIEW  ` statement, modify the `  MATERIALIZED_VIEW  ` placeholder with a unique materialized view name.

7.  Run the `  CREATE MATERIALIZED VIEW  ` DDL statement to create a recommended materialized view.

## Troubleshoot recommendation issues

**Issue:** No recommendations appear for a specific table.

Materialized view recommendations might not appear under the following circumstances:

  - There aren't any recurring query patterns found among query jobs executed by a project.
  - Recurring query patterns don't satisfy [limitations for incremental materialized views](/bigquery/docs/materialized-views-create#supported-mvs) and cannot be put into a materialized view suitable for smart tuning.
  - Potential materialized view would have a high maintenance cost. For example, source tables are often modified by data manipulation language (DML) operations, and therefore a materialized view would undergo full refresh, incurring further costs.
  - There is an insufficient number of queries that have a common recurring pattern.
  - The estimated monthly savings is too insignificant (less than 1 slot).
  - Query jobs executed by the project already use materialized views.

## Pricing

There is no cost or adverse impact on workload performance when you view recommendations.

When you apply recommendations by creating materialized views, you can incur storage, maintenance, and querying costs. For more information, see [Materialized Views Pricing](/bigquery/docs/materialized-views-intro#materialized_views_pricing) .
