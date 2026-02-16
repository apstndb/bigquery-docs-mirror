# Understand BigQuery editions

BigQuery provides three editions which support different types of workloads and the features associated with them. You can enable editions when you [reserve BigQuery capacity](/bigquery/docs/reservations-intro#reservations) . BigQuery also provides an [on-demand (per TiB processed) model](https://cloud.google.com/bigquery/pricing#on_demand_pricing) . You can choose to use editions and the on-demand model at the same time on a per-project basis. For more information about BigQuery editions pricing, see [BigQuery pricing](https://cloud.google.com/bigquery/pricing) .

Each edition provides a set of capabilities at a different price point to meet the requirements of different types of organizations. You can create a [reservation](/bigquery/docs/reservations-intro) or a [capacity commitment](/bigquery/docs/reservations-details#commitments) associated with an edition. To change the edition associated with a reservation, you must delete and recreate the reservation with the new edition type. For more information, see [Update a reservation](/bigquery/docs/reservations-tasks#update_reservations) . Reservations configured to use [slots autoscaling](/bigquery/docs/slots-autoscaling-intro) automatically scale to accommodate the demands of their workloads. Capacity commitments are not required to purchase slots, but can reduce costs. Because BigQuery editions are a property of compute power, not storage, you can query datasets regardless of how they are stored provided your edition supports the capabilities that you want to use. Slots from all editions are subject to the same quota. Your quota is not fulfilled on a per-edition basis. For more information about quotas, see [Quotas and limits](/bigquery/quotas#reservations) .

## BigQuery editions features

The following tables lists the features available in each edition. Features outside of your edition are blocked or lack capabilities.

Don't use edition tiers to restrict access to specific features, because the features assigned to each edition can change over time. For example, don't assign projects to Standard edition reservations as a way of disallowing access to BigQuery ML.

### Administration features

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
<td><strong><a href="https://cloud.google.com/bigquery/pricing#analysis_pricing_models">Pricing model</a></strong></td>
<td>Slot-hours (1 minute minimum)</td>
<td>Slot-hours (1 minute minimum)</td>
<td>Slot-hours (1 minute minimum)</td>
<td>Pay per query with free tier</td>
</tr>
<tr class="even">
<td><strong><a href="https://cloud.google.com/bigquery/sla">Monthly Service Level Objective (SLO)</a></strong><br />
</td>
<td>&gt;=99.9%</td>
<td>&gt;=99.99%</td>
<td>&gt;=99.99%</td>
<td>&gt;=99.99%</td>
</tr>
<tr class="odd">
<td><strong><a href="/assured-workloads/docs/supported-products">Compliance controls</a></strong></td>
<td>No access to compliance controls through Assured Workloads</td>
<td>No access to compliance controls through Assured Workloads</td>
<td><a href="/assured-workloads/docs/supported-products">Compliance controls through Assured Workloads</a></td>
<td><a href="/assured-workloads/docs/supported-products">Compliance controls through Assured Workloads</a></td>
</tr>
<tr class="even">
<td><strong><a href="/bigquery/docs/bi-engine-intro">Business Intelligence acceleration</a></strong></td>
<td>No access to <a href="/bigquery/docs/bi-engine-reserve-capacity">query acceleration through BI Engine</a></td>
<td><a href="/bigquery/docs/bi-engine-reserve-capacity">Query acceleration through BI Engine</a></td>
<td><a href="/bigquery/docs/bi-engine-reserve-capacity">Query acceleration through BI Engine</a></td>
<td><a href="/bigquery/docs/bi-engine-reserve-capacity">Query acceleration through BI Engine</a></td>
</tr>
<tr class="odd">
<td><strong><a href="/bigquery/docs/reservations-intro">Workload management</a></strong></td>
<td>Users cannot set the <a href="/bigquery/docs/query-queues#set_the_maximum_concurrency_target">maximum concurrency target</a></td>
<td>Advanced workload management ( <a href="/bigquery/docs/slots#idle_slots">idle capacity sharing</a> , <a href="/bigquery/docs/query-queues">target concurrency</a> )</td>
<td>Advanced workload management ( <a href="/bigquery/docs/slots#idle_slots">idle capacity sharing</a> , <a href="/bigquery/docs/query-queues">target concurrency</a> )</td>
<td><p>On-demand users don't have access to Advanced workload management</p></td>
</tr>
<tr class="even">
<td><strong><a href="/bigquery/docs/reservations-intro">Compute model</a></strong></td>
<td><a href="/bigquery/docs/slots-autoscaling-intro">Autoscaling</a></td>
<td><a href="/bigquery/docs/slots-autoscaling-intro">Autoscaling + Baseline</a></td>
<td><a href="/bigquery/docs/slots-autoscaling-intro">Autoscaling + Baseline</a></td>
<td>On-demand</td>
</tr>
<tr class="odd">
<td><strong><a href="/bigquery/docs/reservations-workload-management">Maximum reservation size</a></strong></td>
<td>1,600 slots</td>
<td><a href="/bigquery/quotas#reservations">Quota</a></td>
<td><a href="/bigquery/quotas#reservations">Quota</a></td>
<td><a href="/bigquery/quotas#reservations">Quota</a></td>
</tr>
<tr class="even">
<td><strong><a href="/bigquery/docs/reservations-workload-management#admin-project">Maximum reservations per administration project</a></strong></td>
<td>10 reservations per administration project, up to 16,000 slots per organization</td>
<td>200</td>
<td>200</td>
<td>No access to reservations</td>
</tr>
<tr class="odd">
<td><strong><a href="/bigquery/docs/reservations-details">Commitment plans</a></strong></td>
<td>No access to capacity commitments</td>
<td><a href="/bigquery/docs/reservations-details#annual_commitments">1-year commitment at 20% discount or 3-year commitment at 40% discount</a></td>
<td><a href="/bigquery/docs/reservations-details#annual_commitments">1-year commitment at 20% discount or 3-year commitment at 40% discount</a></td>
<td>No access to capacity commitments</td>
</tr>
<tr class="even">
<td><strong><a href="/bigquery/docs/reservations-assignments">Assignments</a></strong></td>
<td><a href="/bigquery/docs/reservations-assignments">Project assignments</a></td>
<td><a href="/bigquery/docs/reservations-assignments">Project, folder, or organization assignments</a></td>
<td><a href="/bigquery/docs/reservations-assignments">Project, folder, or organization assignments</a></td>
<td>No assignments</td>
</tr>
<tr class="odd">
<td><strong><a href="/bigquery/docs/reservations-assignments">Supported assignment types</a></strong></td>
<td><code dir="ltr" translate="no">       QUERY      </code> ,<br />
<code dir="ltr" translate="no">       PIPELINE      </code></td>
<td><code dir="ltr" translate="no">       QUERY      </code> , <code dir="ltr" translate="no">       CONTINUOUS      </code> , <code dir="ltr" translate="no">       PIPELINE      </code> , <code dir="ltr" translate="no">       ML_EXTERNAL      </code> , <code dir="ltr" translate="no">       BACKGROUND      </code></td>
<td><code dir="ltr" translate="no">       QUERY      </code> , <code dir="ltr" translate="no">       CONTINUOUS      </code> , <code dir="ltr" translate="no">       PIPELINE      </code> , <code dir="ltr" translate="no">       ML_EXTERNAL      </code> , <code dir="ltr" translate="no">       BACKGROUND      </code></td>
<td>On-demand pricing doesn't support assignments</td>
</tr>
<tr class="even">
<td><strong><a href="/bigquery/docs/managed-disaster-recovery">Managed disaster recovery</a></strong></td>
<td>No access to <a href="/bigquery/docs/managed-disaster-recovery">managed disaster recovery</a></td>
<td>No access to <a href="/bigquery/docs/managed-disaster-recovery">managed disaster recovery</a></td>
<td><a href="/bigquery/docs/managed-disaster-recovery">Managed disaster recovery</a></td>
<td>No access to <a href="/bigquery/docs/managed-disaster-recovery">managed disaster recovery</a></td>
</tr>
<tr class="odd">
<td><strong><a href="/bigquery/docs/export-intro">Data export</a></strong></td>
<td>No access to <a href="/bigquery/docs/export-to-bigtable">exporting data to Bigtable</a></td>
<td><a href="/bigquery/docs/export-to-bigtable">Exporting data to Bigtable</a></td>
<td><a href="/bigquery/docs/export-to-bigtable">Exporting data to Bigtable</a></td>
<td>No access to <a href="/bigquery/docs/export-to-bigtable">exporting data to Bigtable</a></td>
</tr>
</tbody>
</table>

**Note:** BigQuery Enterprise Plus edition supports [Assured Workloads platform controls](/assured-workloads/docs/supported-products) for regulatory compliance regimes, including FedRAMP, CJIS, IL4, and ITAR.

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
<td><strong><a href="/bigquery/docs/analytics-hub-introduction">Data sharing</a></strong></td>
<td><p><a href="/bigquery/docs/entity-resolution-intro">Entity resolution framework</a></p>
<p><a href="/bigquery/docs/analytics-hub-introduction">Publish and subscribe to datasets</a></p>
<p><a href="/bigquery/docs/data-clean-rooms#subscriber_workflows">Data clean room subscriptions</a></p>
<p><a href="/bigquery/docs/analytics-hub-introduction#data_egress">Egress controls</a></p></td>
<td><p><a href="/bigquery/docs/entity-resolution-intro">Entity resolution framework</a></p>
<p><a href="/bigquery/docs/analytics-hub-introduction">Publish and subscribe to datasets</a></p>
<p><a href="/bigquery/docs/data-clean-rooms#subscriber_workflows">Data clean room subscriptions</a></p>
<p><a href="/bigquery/docs/analytics-hub-introduction#data_egress">Egress controls</a></p></td>
<td><p><a href="/bigquery/docs/entity-resolution-intro">Entity resolution framework</a></p>
<p><a href="/bigquery/docs/analytics-hub-introduction">Publish and subscribe to datasets</a></p>
<p><a href="/bigquery/docs/data-clean-rooms#subscriber_workflows">Data clean room subscriptions</a></p>
<p><a href="/bigquery/docs/analytics-hub-introduction#data_egress">Egress controls</a></p></td>
<td><p><a href="/bigquery/docs/entity-resolution-intro">Entity resolution framework</a></p>
<p><a href="/bigquery/docs/analytics-hub-introduction">Publish and subscribe to datasets</a></p>
<p><a href="/bigquery/docs/data-clean-rooms#subscriber_workflows">Data clean room subscriptions</a></p>
<p><a href="/bigquery/docs/analytics-hub-introduction#data_egress">Egress controls</a></p></td>
</tr>
<tr class="even">
<td><strong><a href="/bigquery/docs/materialized-views-intro">Materialized views</a></strong></td>
<td><a href="/bigquery/docs/materialized-views-use#query">Query existing materialized views directly</a></td>
<td><p><a href="/bigquery/docs/materialized-views-create">Create materialized views</a></p>
<p><a href="/bigquery/docs/materialized-views-manage#automatic-refresh">Automatic refresh of materialized views</a></p>
<p><a href="/bigquery/docs/materialized-views-manage#manual-refresh">Manual refresh of materialized views</a></p>
<p><a href="/bigquery/docs/materialized-views-use#query">Direct query of materialized views</a></p>
<p><a href="/bigquery/docs/materialized-views-use#smart_tuning">Smart tuning</a></p></td>
<td><p><a href="/bigquery/docs/materialized-views-create">Create materialized views</a></p>
<p><a href="/bigquery/docs/materialized-views-manage#automatic-refresh">Automatic refresh of materialized views</a></p>
<p><a href="/bigquery/docs/materialized-views-manage#manual-refresh">Manual refresh of materialized views</a></p>
<p><a href="/bigquery/docs/materialized-views-use#query">Direct query of materialized views</a></p>
<p><a href="/bigquery/docs/materialized-views-use#smart_tuning">Smart tuning</a></p></td>
<td><p><a href="/bigquery/docs/materialized-views-create">Create materialized views</a></p>
<p><a href="/bigquery/docs/materialized-views-manage#automatic-refresh">Automatic refresh of materialized views</a></p>
<p><a href="/bigquery/docs/materialized-views-manage#manual-refresh">Manual refresh of materialized views</a></p>
<p><a href="/bigquery/docs/materialized-views-use#query">Direct query of materialized views</a></p>
<p><a href="/bigquery/docs/materialized-views-use#smart_tuning">Smart tuning</a></p></td>
</tr>
<tr class="odd">
<td><strong><a href="/bigquery/docs/cached-results">Cached results</a></strong></td>
<td><a href="/bigquery/docs/cached-results">Single-user caching</a></td>
<td><a href="/bigquery/docs/cached-results#cross-user-caching">Cross-user caching</a></td>
<td><a href="/bigquery/docs/cached-results#cross-user-caching">Cross-user caching</a></td>
<td><a href="/bigquery/docs/cached-results">Single-user caching</a></td>
</tr>
<tr class="even">
<td><strong><a href="/bigquery/docs/continuous-queries-introduction">Continuous queries</a></strong></td>
<td>No access to <a href="/bigquery/docs/continuous-queries-introduction">continuous queries</a></td>
<td><a href="/bigquery/docs/continuous-queries-introduction">Continuous queries</a></td>
<td><a href="/bigquery/docs/continuous-queries-introduction">Continuous queries</a></td>
<td>No access to <a href="/bigquery/docs/continuous-queries-introduction">continuous queries</a></td>
</tr>
<tr class="odd">
<td><strong><a href="/bigquery/docs/search-index">Search</a></strong></td>
<td>Access to the <a href="/bigquery/docs/reference/standard-sql/search_functions#search"><code dir="ltr" translate="no">        SEARCH       </code> function</a> without access to <a href="/bigquery/docs/search-index">search indexes</a></td>
<td><a href="/bigquery/docs/search-index">Query acceleration with search indexes</a></td>
<td><a href="/bigquery/docs/search-index">Query acceleration with search indexes</a></td>
<td><a href="/bigquery/docs/search-index">Query acceleration with search indexes</a></td>
</tr>
<tr class="even">
<td><strong><a href="/bigquery/docs/vector-search-intro">Vector search</a></strong></td>
<td>Access to the <a href="/bigquery/docs/reference/standard-sql/search_functions#vector_search"><code dir="ltr" translate="no">        VECTOR_SEARCH       </code> function</a> without access to <a href="/bigquery/docs/vector-index">vector indexes</a></td>
<td><a href="/bigquery/docs/vector-index">Query acceleration with vector indexes</a></td>
<td><a href="/bigquery/docs/vector-index">Query acceleration with vector indexes</a></td>
<td><a href="/bigquery/docs/vector-index">Query acceleration with vector indexes</a></td>
</tr>
<tr class="odd">
<td><strong><a href="/bigquery/docs/object-table-introduction">Unstructured data</a></strong></td>
<td>Run SQL queries on object tables</td>
<td>Perform ML inference on object tables using remote models:
<ul>
<li><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model">Google models hosted in Vertex AI</a></li>
<li><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-service">Cloud AI services</a></li>
<li><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-https">Custom models deployed to Vertex AI</a></li>
</ul></td>
<td>Perform ML inference on object tables using remote models:
<ul>
<li><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model">Google models hosted in Vertex AI</a></li>
<li><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-service">Cloud AI services</a></li>
<li><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-https">Custom models deployed to Vertex AI</a></li>
</ul></td>
<td>Perform ML inference on object tables using remote models:
<ul>
<li><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model">Google models hosted in Vertex AI</a></li>
<li><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-service">Cloud AI services</a></li>
<li><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-https">Custom models deployed to Vertex AI</a></li>
</ul></td>
</tr>
<tr class="even">
<td><strong><a href="/bigquery/docs/omni-introduction">Multi-cloud analytics</a></strong></td>
<td>Not available</td>
<td><a href="/bigquery/docs/omni-introduction">BigQuery Omni support</a></td>
<td>Not available</td>
<td><a href="/bigquery/docs/omni-introduction">BigQuery Omni support</a></td>
</tr>
<tr class="odd">
<td><strong><a href="/bigquery/docs/bqml-introduction">Integrated machine learning</a></strong></td>
<td>No access to <a href="/bigquery/docs/bqml-introduction">BigQuery ML</a></td>
<td><a href="/bigquery/docs/bqml-introduction">BigQuery ML</a></td>
<td><a href="/bigquery/docs/bqml-introduction">BigQuery ML</a></td>
<td><a href="/bigquery/docs/bqml-introduction">BigQuery ML</a></td>
</tr>
<tr class="even">
<td><strong><a href="/bigquery/docs/reservations-intro">Workload management</a></strong></td>
<td>Users cannot set the <a href="/bigquery/docs/query-queues#set_the_maximum_concurrency_target">maximum concurrency target</a></td>
<td>Advanced workload management ( <a href="/bigquery/docs/slots#idle_slots">idle capacity sharing</a> , <a href="/bigquery/docs/query-queues">target concurrency</a> )</td>
<td>Advanced workload management ( <a href="/bigquery/docs/slots#idle_slots">idle capacity sharing</a> , <a href="/bigquery/docs/query-queues">target concurrency</a> )</td>
<td><p>On-demand users don't have access to Advanced workload management</p></td>
</tr>
<tr class="odd">
<td><strong><a href="/bigquery/docs/reservations-assignments">Supported assignment types</a></strong></td>
<td><code dir="ltr" translate="no">       QUERY      </code> ,<br />
<code dir="ltr" translate="no">       PIPELINE      </code></td>
<td><code dir="ltr" translate="no">       QUERY      </code> , <code dir="ltr" translate="no">       CONTINUOUS      </code> , <code dir="ltr" translate="no">       PIPELINE      </code> , <code dir="ltr" translate="no">       ML_EXTERNAL      </code> , <code dir="ltr" translate="no">       BACKGROUND      </code></td>
<td><code dir="ltr" translate="no">       QUERY      </code> , <code dir="ltr" translate="no">       CONTINUOUS      </code> , <code dir="ltr" translate="no">       PIPELINE      </code> , <code dir="ltr" translate="no">       ML_EXTERNAL      </code> , <code dir="ltr" translate="no">       BACKGROUND      </code></td>
<td>On-demand pricing doesn't support assignments</td>
</tr>
<tr class="even">
<td><strong><a href="/vpc-service-controls">VPC Service Controls</a></strong></td>
<td>No <a href="/vpc-service-controls/docs/supported-products#table_bigquery">VPC Service Controls Support</a></td>
<td><a href="/vpc-service-controls/docs/supported-products#table_bigquery">VPC Service Controls Support</a></td>
<td><a href="/vpc-service-controls/docs/supported-products#table_bigquery">VPC Service Controls Support</a></td>
<td><a href="/vpc-service-controls/docs/supported-products#table_bigquery">VPC Service Controls Support</a></td>
</tr>
<tr class="odd">
<td><strong><a href="/bigquery/docs/export-intro">Data export</a></strong></td>
<td>No access to <a href="/bigquery/docs/export-to-bigtable">exporting data to Bigtable</a> or <a href="/bigquery/docs/export-to-spanner">exporting data to Spanner</a></td>
<td><a href="/bigquery/docs/export-to-bigtable">Exporting data to Bigtable</a> or <a href="/bigquery/docs/export-to-spanner">exporting data to Spanner</a></td>
<td><a href="/bigquery/docs/export-to-bigtable">Exporting data to Bigtable</a> or <a href="/bigquery/docs/export-to-spanner">exporting data to Spanner</a></td>
<td>No access to <a href="/bigquery/docs/export-to-bigtable">exporting data to Bigtable</a> or <a href="/bigquery/docs/export-to-spanner">exporting data to Spanner</a></td>
</tr>
<tr class="even">
<td><strong><a href="/bigquery/docs/encryption-at-rest">Storage encryption</a></strong></td>
<td><p><a href="/bigquery/docs/encryption-at-rest">Google-owned and Google-managed encryption keys</a></p></td>
<td><p><a href="/bigquery/docs/customer-managed-encryption">Customer-managed keys (CMEK)</a></p>
<p><a href="/bigquery/docs/encryption-at-rest">Google-owned and Google-managed encryption keys</a></p></td>
<td><p><a href="/bigquery/docs/customer-managed-encryption">Customer-managed keys (CMEK)</a></p>
<p><a href="/bigquery/docs/encryption-at-rest">Google-owned and Google-managed encryption keys</a></p></td>
<td><p><a href="/bigquery/docs/customer-managed-encryption">Customer-managed keys (CMEK)</a></p>
<p><a href="/bigquery/docs/encryption-at-rest">Google-owned and Google-managed encryption keys</a></p></td>
</tr>
<tr class="odd">
<td><strong><a href="/bigquery/docs/data-governance">Fine-grained security controls</a></strong></td>
<td>No access to fine-grained security controls</td>
<td><p><a href="/bigquery/docs/column-level-security-intro">Column-level access control</a></p>
<p><a href="/bigquery/docs/row-level-security-intro">Row-level security</a></p>
<p><a href="/bigquery/docs/column-data-masking-intro">Dynamic data masking</a></p>
<p><a href="/bigquery/docs/user-defined-functions#custom-mask">Custom data masking</a></p></td>
<td><p><a href="/bigquery/docs/column-level-security-intro">Column-level access control</a></p>
<p><a href="/bigquery/docs/row-level-security-intro">Row-level security</a></p>
<p><a href="/bigquery/docs/column-data-masking-intro">Dynamic data masking</a></p>
<p><a href="/bigquery/docs/user-defined-functions#custom-mask">Custom data masking</a></p></td>
<td><p><a href="/bigquery/docs/column-level-security-intro">Column-level access control</a></p>
<p><a href="/bigquery/docs/row-level-security-intro">Row-level security</a></p>
<p><a href="/bigquery/docs/column-data-masking-intro">Dynamic data masking</a></p>
<p><a href="/bigquery/docs/user-defined-functions#custom-mask">Custom data masking</a></p></td>
</tr>
</tbody>
</table>

**Note:** BigQuery [automatically encrypts all data](/bigquery/docs/encryption-at-rest) at rest. By default, Google manages the encryption keys used to protect your data. You can also use [customer-managed encryption keys (CMEK)](/bigquery/docs/customer-managed-encryption) in the Enterprise edition and Enterprise Plus edition.

## What's next

  - For more information on slots autoscaling, see [Introduction to slots autoscaling](/bigquery/docs/slots-autoscaling-intro) .
  - For more information on reservations, see [Introduction to Reservations](/bigquery/docs/reservations-intro) .
