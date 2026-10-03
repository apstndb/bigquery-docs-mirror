---
name: documents/docs.cloud.google.com/bigquery/docs/editions-intro
uri: https://docs.cloud.google.com/bigquery/docs/editions-intro
title: Understand BigQuery editions
description: Gives an overview of the different editions available in BigQuery and their associated features.
data_source: docs.cloud.google.com
---

# Understand BigQuery editions

BigQuery provides three editions which support different types of workloads and the features associated with them. You can enable editions when you [reserve BigQuery capacity](https://docs.cloud.google.com/bigquery/docs/reservations-intro#reservations) . BigQuery also provides an [on-demand (per TiB processed) model](https://cloud.google.com/bigquery/pricing#on_demand_pricing) . You can choose to use editions and the on-demand model at the same time on a per-project basis. For more information about BigQuery editions pricing, see [BigQuery pricing](https://cloud.google.com/bigquery/pricing) .

Each edition provides a set of capabilities at a different price point to meet the requirements of different types of organizations. You can create a [reservation](https://docs.cloud.google.com/bigquery/docs/reservations-intro) or a [capacity commitment](https://docs.cloud.google.com/bigquery/docs/reservations-details#commitments) associated with an edition. To change the edition associated with a reservation, you must delete and recreate the reservation with the new edition type. For more information, see [Update a reservation](https://docs.cloud.google.com/bigquery/docs/reservations-tasks#update_reservations) . Reservations configured to use [slots autoscaling](https://docs.cloud.google.com/bigquery/docs/slots-autoscaling-intro) automatically scale to accommodate the demands of their workloads. Capacity commitments are not required to purchase slots, but can reduce costs. Because BigQuery editions are a property of compute power, not storage, you can query datasets regardless of how they are stored provided your edition supports the capabilities that you want to use. Slots from all editions are subject to the same quota. Your quota is not fulfilled on a per-edition basis. For more information about quotas, see [Quotas and limits](https://docs.cloud.google.com/bigquery/quotas#reservations) .

## BigQuery editions features

The following tables lists the features available in each edition. Features outside of your edition are blocked or lack capabilities.

Don't use edition tiers to restrict access to specific features, because the features assigned to each edition can change over time. For example, don't assign projects to Standard edition reservations as a way of disallowing access to BigQuery ML.

### Administration features

|                                                                                                                                                   | **Standard**                                                                                                                                                                                                                                                       | **Enterprise**                                                                                                                                                                                                                                      | **Enterprise Plus**                                                                                                                                                                                                                                 | **On-demand pricing**                                                                                                                                                                                                                                            |
|---------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **[Pricing model](https://cloud.google.com/bigquery/pricing#analysis_pricing_models)**                                                            | Slot-hours (1 minute minimum by default; opt in to [BigQuery fluid scaling](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#reservation_option_list) for no minimum duration)                                          | Slot-hours (1 minute minimum by default; opt in to [BigQuery fluid scaling](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#reservation_option_list) for no minimum duration)                           | Slot-hours (1 minute minimum by default; opt in to [BigQuery fluid scaling](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#reservation_option_list) for no minimum duration)                           | Pay per query with free tier                                                                                                                                                                                                                                     |
| **[Monthly Service Level Objective (SLO)](https://cloud.google.com/bigquery/sla)**                                                                | \>=99.9%                                                                                                                                                                                                                                                           | \>=99.99%                                                                                                                                                                                                                                           | \>=99.99%                                                                                                                                                                                                                                           | \>=99.99%                                                                                                                                                                                                                                                        |
| **[Compliance controls](https://docs.cloud.google.com/assured-workloads/docs/supported-products)**                                                | No access to compliance controls through Assured Workloads                                                                                                                                                                                                         | No access to compliance controls through Assured Workloads                                                                                                                                                                                          | [Compliance controls through Assured Workloads](https://docs.cloud.google.com/assured-workloads/docs/supported-products)                                                                                                                            | [Compliance controls through Assured Workloads](https://docs.cloud.google.com/assured-workloads/docs/supported-products)                                                                                                                                         |
| **[Business Intelligence acceleration](https://docs.cloud.google.com/bigquery/docs/bi-engine-intro)**                                             | No access to [query acceleration through BI Engine](https://docs.cloud.google.com/bigquery/docs/bi-engine-reserve-capacity)                                                                                                                                        | [Query acceleration through BI Engine](https://docs.cloud.google.com/bigquery/docs/bi-engine-reserve-capacity)                                                                                                                                      | [Query acceleration through BI Engine](https://docs.cloud.google.com/bigquery/docs/bi-engine-reserve-capacity)                                                                                                                                      | [Query acceleration through BI Engine](https://docs.cloud.google.com/bigquery/docs/bi-engine-reserve-capacity)                                                                                                                                                   |
| **[Workload management](https://docs.cloud.google.com/bigquery/docs/reservations-intro)**                                                         | Users cannot set the [maximum concurrency target](https://docs.cloud.google.com/bigquery/docs/query-queues#set_the_maximum_concurrency_target)                                                                                                                     | Advanced workload management ( [idle capacity sharing](https://docs.cloud.google.com/bigquery/docs/slots#idle_slots) , [target concurrency](https://docs.cloud.google.com/bigquery/docs/query-queues) )                                             | Advanced workload management ( [idle capacity sharing](https://docs.cloud.google.com/bigquery/docs/slots#idle_slots) , [target concurrency](https://docs.cloud.google.com/bigquery/docs/query-queues) )                                             | On-demand users don't have access to Advanced workload management                                                                                                                                                                                                |
| **[Compute model](https://docs.cloud.google.com/bigquery/docs/reservations-intro)**                                                               | [Autoscaling](https://docs.cloud.google.com/bigquery/docs/slots-autoscaling-intro)                                                                                                                                                                                 | [Autoscaling + Baseline](https://docs.cloud.google.com/bigquery/docs/slots-autoscaling-intro)                                                                                                                                                       | [Autoscaling + Baseline](https://docs.cloud.google.com/bigquery/docs/slots-autoscaling-intro)                                                                                                                                                       | On-demand                                                                                                                                                                                                                                                        |
| **[Maximum reservation size](https://docs.cloud.google.com/bigquery/docs/reservations-workload-management)**                                      | 1,600 slots                                                                                                                                                                                                                                                        | [Quota](https://docs.cloud.google.com/bigquery/quotas#reservations)                                                                                                                                                                                 | [Quota](https://docs.cloud.google.com/bigquery/quotas#reservations)                                                                                                                                                                                 | [Quota](https://docs.cloud.google.com/bigquery/quotas#reservations)                                                                                                                                                                                              |
| **[Maximum reservations per administration project](https://docs.cloud.google.com/bigquery/docs/reservations-workload-management#admin-project)** | 10 reservations per administration project, up to 16,000 slots per organization                                                                                                                                                                                    | 200                                                                                                                                                                                                                                                 | 200                                                                                                                                                                                                                                                 | No access to reservations                                                                                                                                                                                                                                        |
| **[Commitment plans](https://docs.cloud.google.com/bigquery/docs/reservations-details)**                                                          | No access to capacity commitments                                                                                                                                                                                                                                  | [1-year commitment at 20% discount or 3-year commitment at 40% discount](https://docs.cloud.google.com/bigquery/docs/reservations-details#annual_commitments)                                                                                       | [1-year commitment at 20% discount or 3-year commitment at 40% discount](https://docs.cloud.google.com/bigquery/docs/reservations-details#annual_commitments)                                                                                       | No access to capacity commitments                                                                                                                                                                                                                                |
| **[Assignments](https://docs.cloud.google.com/bigquery/docs/reservations-assignments)**                                                           | [Project assignments](https://docs.cloud.google.com/bigquery/docs/reservations-assignments)                                                                                                                                                                        | [Project, folder, or organization assignments](https://docs.cloud.google.com/bigquery/docs/reservations-assignments)                                                                                                                                | [Project, folder, or organization assignments](https://docs.cloud.google.com/bigquery/docs/reservations-assignments)                                                                                                                                | No assignments                                                                                                                                                                                                                                                   |
| **[Supported assignment types](https://docs.cloud.google.com/bigquery/docs/reservations-assignments)**                                            | `QUERY` , `PIPELINE`                                                                                                                                                                                                                                               | `QUERY` , `CONTINUOUS` , `PIPELINE` , `ML_EXTERNAL` , `BACKGROUND` , `BACKGROUND_COLUMN_METADATA_INDEX` , `BACKGROUND_CHANGE_DATA_CAPTURE` , `BACKGROUND_SEARCH_INDEX_REFRESH`                                                                      | `QUERY` , `CONTINUOUS` , `PIPELINE` , `ML_EXTERNAL` , `BACKGROUND` , `BACKGROUND_COLUMN_METADATA_INDEX` , `BACKGROUND_CHANGE_DATA_CAPTURE` , `BACKGROUND_SEARCH_INDEX_REFRESH`                                                                      | On-demand pricing doesn't support assignments                                                                                                                                                                                                                    |
| **[Managed disaster recovery](https://docs.cloud.google.com/bigquery/docs/managed-disaster-recovery)**                                            | No access to [managed disaster recovery](https://docs.cloud.google.com/bigquery/docs/managed-disaster-recovery)                                                                                                                                                    | No access to [managed disaster recovery](https://docs.cloud.google.com/bigquery/docs/managed-disaster-recovery)                                                                                                                                     | [Managed disaster recovery](https://docs.cloud.google.com/bigquery/docs/managed-disaster-recovery)                                                                                                                                                  | No access to [managed disaster recovery](https://docs.cloud.google.com/bigquery/docs/managed-disaster-recovery)                                                                                                                                                  |
| **[Data export](https://docs.cloud.google.com/bigquery/docs/export-intro)**                                                                       | No access to [exporting data to Bigtable](https://docs.cloud.google.com/bigquery/docs/export-to-bigtable) , [Spanner](https://docs.cloud.google.com/bigquery/docs/export-to-spanner) , or [AlloyDB](https://docs.cloud.google.com/bigquery/docs/export-to-alloydb) | [Exporting data to Bigtable](https://docs.cloud.google.com/bigquery/docs/export-to-bigtable) , [Spanner](https://docs.cloud.google.com/bigquery/docs/export-to-spanner) or [AlloyDB](https://docs.cloud.google.com/bigquery/docs/export-to-alloydb) | [Exporting data to Bigtable](https://docs.cloud.google.com/bigquery/docs/export-to-bigtable) , [Spanner](https://docs.cloud.google.com/bigquery/docs/export-to-spanner) or [AlloyDB](https://docs.cloud.google.com/bigquery/docs/export-to-alloydb) | No access to [exporting data to Bigtable](https://docs.cloud.google.com/bigquery/docs/export-to-bigtable) , [Spanner](https://docs.cloud.google.com/bigquery/docs/export-to-spanner) or [AlloyDB](https://docs.cloud.google.com/bigquery/docs/export-to-alloydb) |

> **Note:** BigQuery Enterprise Plus edition supports [Assured Workloads platform controls](https://docs.cloud.google.com/assured-workloads/docs/supported-products) for regulatory compliance regimes, including FedRAMP, CJIS, IL4, and ITAR.

### Analysis features

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th><strong>Standard</strong></th>
<th><strong>Enterprise</strong></th>
<th><strong>Enterprise Plus</strong></th>
<th><strong>On-demand pricing</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong><a href="https://docs.cloud.google.com/bigquery/docs/analytics-hub-introduction">Data sharing</a></strong></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/entity-resolution-intro">Entity resolution framework</a></p>
<p><a href="https://docs.cloud.google.com/bigquery/docs/analytics-hub-introduction">Publish and subscribe to datasets</a></p>
<p><a href="https://docs.cloud.google.com/bigquery/docs/data-clean-rooms#subscriber_workflows">Data clean room subscriptions</a></p>
<p><a href="https://docs.cloud.google.com/bigquery/docs/analytics-hub-introduction#data_egress">Egress controls</a></p></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/entity-resolution-intro">Entity resolution framework</a></p>
<p><a href="https://docs.cloud.google.com/bigquery/docs/analytics-hub-introduction">Publish and subscribe to datasets</a></p>
<p><a href="https://docs.cloud.google.com/bigquery/docs/data-clean-rooms#subscriber_workflows">Data clean room subscriptions</a></p>
<p><a href="https://docs.cloud.google.com/bigquery/docs/analytics-hub-introduction#data_egress">Egress controls</a></p></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/entity-resolution-intro">Entity resolution framework</a></p>
<p><a href="https://docs.cloud.google.com/bigquery/docs/analytics-hub-introduction">Publish and subscribe to datasets</a></p>
<p><a href="https://docs.cloud.google.com/bigquery/docs/data-clean-rooms#subscriber_workflows">Data clean room subscriptions</a></p>
<p><a href="https://docs.cloud.google.com/bigquery/docs/analytics-hub-introduction#data_egress">Egress controls</a></p></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/entity-resolution-intro">Entity resolution framework</a></p>
<p><a href="https://docs.cloud.google.com/bigquery/docs/analytics-hub-introduction">Publish and subscribe to datasets</a></p>
<p><a href="https://docs.cloud.google.com/bigquery/docs/data-clean-rooms#subscriber_workflows">Data clean room subscriptions</a></p>
<p><a href="https://docs.cloud.google.com/bigquery/docs/analytics-hub-introduction#data_egress">Egress controls</a></p></td>
</tr>
<tr class="even">
<td><strong><a href="https://docs.cloud.google.com/bigquery/docs/materialized-views-intro">Materialized views</a></strong></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/materialized-views-use#query">Query existing materialized views directly</a></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/materialized-views-create">Create materialized views</a></p>
<p><a href="https://docs.cloud.google.com/bigquery/docs/materialized-views-manage#automatic-refresh">Automatic refresh of materialized views</a></p>
<p><a href="https://docs.cloud.google.com/bigquery/docs/materialized-views-manage#manual-refresh">Manual refresh of materialized views</a></p>
<p><a href="https://docs.cloud.google.com/bigquery/docs/materialized-views-use#query">Direct query of materialized views</a></p>
<p><a href="https://docs.cloud.google.com/bigquery/docs/materialized-views-use#smart_tuning">Smart tuning</a></p></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/materialized-views-create">Create materialized views</a></p>
<p><a href="https://docs.cloud.google.com/bigquery/docs/materialized-views-manage#automatic-refresh">Automatic refresh of materialized views</a></p>
<p><a href="https://docs.cloud.google.com/bigquery/docs/materialized-views-manage#manual-refresh">Manual refresh of materialized views</a></p>
<p><a href="https://docs.cloud.google.com/bigquery/docs/materialized-views-use#query">Direct query of materialized views</a></p>
<p><a href="https://docs.cloud.google.com/bigquery/docs/materialized-views-use#smart_tuning">Smart tuning</a></p></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/materialized-views-create">Create materialized views</a></p>
<p><a href="https://docs.cloud.google.com/bigquery/docs/materialized-views-manage#automatic-refresh">Automatic refresh of materialized views</a></p>
<p><a href="https://docs.cloud.google.com/bigquery/docs/materialized-views-manage#manual-refresh">Manual refresh of materialized views</a></p>
<p><a href="https://docs.cloud.google.com/bigquery/docs/materialized-views-use#query">Direct query of materialized views</a></p>
<p><a href="https://docs.cloud.google.com/bigquery/docs/materialized-views-use#smart_tuning">Smart tuning</a></p></td>
</tr>
<tr class="odd">
<td><strong><a href="https://docs.cloud.google.com/bigquery/docs/cached-results">Cached results</a></strong></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/cached-results">Single-user caching</a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/cached-results#cross-user-caching">Cross-user caching</a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/cached-results#cross-user-caching">Cross-user caching</a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/cached-results">Single-user caching</a></td>
</tr>
<tr class="even">
<td><strong><a href="https://docs.cloud.google.com/bigquery/docs/continuous-queries-introduction">Continuous queries</a></strong></td>
<td>No access to <a href="https://docs.cloud.google.com/bigquery/docs/continuous-queries-introduction">continuous queries</a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/continuous-queries-introduction">Continuous queries</a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/continuous-queries-introduction">Continuous queries</a></td>
<td>No access to <a href="https://docs.cloud.google.com/bigquery/docs/continuous-queries-introduction">continuous queries</a></td>
</tr>
<tr class="odd">
<td><strong><a href="https://docs.cloud.google.com/bigquery/docs/search-index">Search</a></strong></td>
<td>Access to the <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/search_functions#search"><code>SEARCH</code> function</a> without access to <a href="https://docs.cloud.google.com/bigquery/docs/search-index">search indexes</a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/search-index">Query acceleration with search indexes</a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/search-index">Query acceleration with search indexes</a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/search-index">Query acceleration with search indexes</a></td>
</tr>
<tr class="even">
<td><strong><a href="https://docs.cloud.google.com/bigquery/docs/vector-search-intro">Vector search</a></strong></td>
<td>Access to the <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/search_functions#vector_search"><code>VECTOR_SEARCH</code> function</a> without access to <a href="https://docs.cloud.google.com/bigquery/docs/vector-index">vector indexes</a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/vector-index">Query acceleration with vector indexes</a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/vector-index">Query acceleration with vector indexes</a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/vector-index">Query acceleration with vector indexes</a></td>
</tr>
<tr class="odd">
<td><strong><a href="https://docs.cloud.google.com/bigquery/docs/object-table-introduction">Unstructured data</a></strong></td>
<td>Run SQL queries on object tables</td>
<td>Perform ML inference on object tables using remote models:
<ul>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model">Google models hosted in Gemini Enterprise Agent Platform</a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-service">Cloud AI services</a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-https">Custom models deployed to Agent Platform</a></li>
</ul></td>
<td>Perform ML inference on object tables using remote models:
<ul>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model">Google models hosted in Agent Platform</a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-service">Cloud AI services</a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-https">Custom models deployed to Agent Platform</a></li>
</ul></td>
<td>Perform ML inference on object tables using remote models:
<ul>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model">Google models hosted in Agent Platform</a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-service">Cloud AI services</a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-https">Custom models deployed to Agent Platform</a></li>
</ul></td>
</tr>
<tr class="even">
<td><strong><a href="https://docs.cloud.google.com/bigquery/docs/omni-introduction">Multi-cloud analytics</a></strong></td>
<td>Not available</td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/omni-introduction">BigQuery Omni support</a></td>
<td>Not available</td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/omni-introduction">BigQuery Omni support</a></td>
</tr>
<tr class="odd">
<td><strong><a href="https://docs.cloud.google.com/bigquery/docs/bqml-introduction">Integrated machine learning</a></strong></td>
<td>No access to <a href="https://docs.cloud.google.com/bigquery/docs/bqml-introduction">BigQuery ML</a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/bqml-introduction">BigQuery ML</a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/bqml-introduction">BigQuery ML</a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/bqml-introduction">BigQuery ML</a></td>
</tr>
<tr class="even">
<td><strong><a href="https://docs.cloud.google.com/bigquery/docs/reservations-intro">Workload management</a></strong></td>
<td>Users cannot set the <a href="https://docs.cloud.google.com/bigquery/docs/query-queues#set_the_maximum_concurrency_target">maximum concurrency target</a></td>
<td>Advanced workload management ( <a href="https://docs.cloud.google.com/bigquery/docs/slots#idle_slots">idle capacity sharing</a> , <a href="https://docs.cloud.google.com/bigquery/docs/query-queues">target concurrency</a> )</td>
<td>Advanced workload management ( <a href="https://docs.cloud.google.com/bigquery/docs/slots#idle_slots">idle capacity sharing</a> , <a href="https://docs.cloud.google.com/bigquery/docs/query-queues">target concurrency</a> )</td>
<td><p>On-demand users don't have access to Advanced workload management</p></td>
</tr>
<tr class="odd">
<td><strong><a href="https://docs.cloud.google.com/bigquery/docs/reservations-assignments">Supported assignment types</a></strong></td>
<td><code>QUERY</code> ,<br />
<code>PIPELINE</code></td>
<td><code>QUERY</code> ,<br />
<code>CONTINUOUS</code> ,<br />
<code>PIPELINE</code> ,<br />
<code>ML_EXTERNAL</code> ,<br />
<code>BACKGROUND</code> ,<br />
<code>BACKGROUND_COLUMN_METADATA_INDEX</code> ,<br />
<code>BACKGROUND_CHANGE_DATA_CAPTURE</code> ,<br />
<code>BACKGROUND_SEARCH_INDEX_REFRESH</code></td>
<td><code>QUERY</code> ,<br />
<code>CONTINUOUS</code> ,<br />
<code>PIPELINE</code> ,<br />
<code>ML_EXTERNAL</code> ,<br />
<code>BACKGROUND</code> ,<br />
<code>BACKGROUND_COLUMN_METADATA_INDEX</code> ,<br />
<code>BACKGROUND_CHANGE_DATA_CAPTURE</code> ,<br />
<code>BACKGROUND_SEARCH_INDEX_REFRESH</code></td>
<td>On-demand pricing doesn't support assignments</td>
</tr>
<tr class="even">
<td><strong><a href="https://docs.cloud.google.com/vpc-service-controls">VPC Service Controls</a></strong></td>
<td>No <a href="https://docs.cloud.google.com/vpc-service-controls/docs/supported-products#table_bigquery">VPC Service Controls Support</a></td>
<td><a href="https://docs.cloud.google.com/vpc-service-controls/docs/supported-products#table_bigquery">VPC Service Controls Support</a></td>
<td><a href="https://docs.cloud.google.com/vpc-service-controls/docs/supported-products#table_bigquery">VPC Service Controls Support</a></td>
<td><a href="https://docs.cloud.google.com/vpc-service-controls/docs/supported-products#table_bigquery">VPC Service Controls Support</a></td>
</tr>
<tr class="odd">
<td><strong><a href="https://docs.cloud.google.com/bigquery/docs/export-intro">Data export</a></strong></td>
<td>No access to <a href="https://docs.cloud.google.com/bigquery/docs/export-to-bigtable">exporting data to Bigtable</a> , <a href="https://docs.cloud.google.com/bigquery/docs/export-to-spanner">exporting data to Spanner</a> , or <a href="https://docs.cloud.google.com/bigquery/docs/export-to-alloydb">exporting data to AlloyDB for PostgreSQL</a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/export-to-bigtable">Exporting data to Bigtable</a> , <a href="https://docs.cloud.google.com/bigquery/docs/export-to-spanner">exporting data to Spanner</a> , or <a href="https://docs.cloud.google.com/bigquery/docs/export-to-alloydb">exporting data to AlloyDB for PostgreSQL</a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/export-to-bigtable">Exporting data to Bigtable</a> , <a href="https://docs.cloud.google.com/bigquery/docs/export-to-spanner">exporting data to Spanner</a> , or <a href="https://docs.cloud.google.com/bigquery/docs/export-to-alloydb">exporting data to AlloyDB for PostgreSQL</a></td>
<td>No access to <a href="https://docs.cloud.google.com/bigquery/docs/export-to-bigtable">exporting data to Bigtable</a> , <a href="https://docs.cloud.google.com/bigquery/docs/export-to-spanner">exporting data to Spanner</a> , or <a href="https://docs.cloud.google.com/bigquery/docs/export-to-alloydb">exporting data to AlloyDB for PostgreSQL</a></td>
</tr>
<tr class="even">
<td><strong><a href="https://docs.cloud.google.com/bigquery/docs/encryption-at-rest">Storage encryption</a></strong></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/encryption-at-rest">Google-owned and Google-managed encryption keys</a></p></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/customer-managed-encryption">Customer-managed keys (CMEK)</a></p>
<p><a href="https://docs.cloud.google.com/bigquery/docs/encryption-at-rest">Google-owned and Google-managed encryption keys</a></p></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/customer-managed-encryption">Customer-managed keys (CMEK)</a></p>
<p><a href="https://docs.cloud.google.com/bigquery/docs/encryption-at-rest">Google-owned and Google-managed encryption keys</a></p></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/customer-managed-encryption">Customer-managed keys (CMEK)</a></p>
<p><a href="https://docs.cloud.google.com/bigquery/docs/encryption-at-rest">Google-owned and Google-managed encryption keys</a></p></td>
</tr>
<tr class="odd">
<td><strong><a href="https://docs.cloud.google.com/bigquery/docs/data-governance">Fine-grained security controls</a></strong></td>
<td>No access to fine-grained security controls</td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/column-level-security-intro">Column-level access control</a></p>
<p><a href="https://docs.cloud.google.com/bigquery/docs/row-level-security-intro">Row-level security</a></p>
<p><a href="https://docs.cloud.google.com/bigquery/docs/column-data-masking-intro">Dynamic data masking</a></p>
<p><a href="https://docs.cloud.google.com/bigquery/docs/user-defined-functions#custom-mask">Custom data masking</a></p></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/column-level-security-intro">Column-level access control</a></p>
<p><a href="https://docs.cloud.google.com/bigquery/docs/row-level-security-intro">Row-level security</a></p>
<p><a href="https://docs.cloud.google.com/bigquery/docs/column-data-masking-intro">Dynamic data masking</a></p>
<p><a href="https://docs.cloud.google.com/bigquery/docs/user-defined-functions#custom-mask">Custom data masking</a></p></td>
<td><p><a href="https://docs.cloud.google.com/bigquery/docs/column-level-security-intro">Column-level access control</a></p>
<p><a href="https://docs.cloud.google.com/bigquery/docs/row-level-security-intro">Row-level security</a></p>
<p><a href="https://docs.cloud.google.com/bigquery/docs/column-data-masking-intro">Dynamic data masking</a></p>
<p><a href="https://docs.cloud.google.com/bigquery/docs/user-defined-functions#custom-mask">Custom data masking</a></p></td>
</tr>
<tr class="even">
<td><strong><a href="https://docs.cloud.google.com/bigquery/docs/graph-overview">BigQuery Graph</a></strong></td>
<td>No access to <a href="https://docs.cloud.google.com/bigquery/docs/graph-overview">BigQuery Graph</a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/graph-overview">BigQuery Graph</a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/graph-overview">BigQuery Graph</a></td>
<td>Create graphs, call <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/graph-sql-queries#graph_expand"><code>GRAPH_EXPAND</code></a> , and <a href="https://docs.cloud.google.com/bigquery/docs/graph-measures">use measures</a> . No support for GQL queries.</td>
</tr>
</tbody>
</table>

> **Note:** BigQuery [automatically encrypts all data](https://docs.cloud.google.com/bigquery/docs/encryption-at-rest) at rest. By default, Google manages the encryption keys used to protect your data. You can also use [customer-managed encryption keys (CMEK)](https://docs.cloud.google.com/bigquery/docs/customer-managed-encryption) in the Enterprise edition and Enterprise Plus edition.

## What's next

- For more information on slots autoscaling, see [Introduction to slots autoscaling](https://docs.cloud.google.com/bigquery/docs/slots-autoscaling-intro) .
- For more information on reservations, see [Introduction to Reservations](https://docs.cloud.google.com/bigquery/docs/reservations-intro) .
