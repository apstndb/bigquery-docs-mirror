# Sharing VPC Service Controls rules

This document describes the ingress and egress rules that you need to let publishers and subscribers in BigQuery sharing (formerly Analytics Hub) access data from projects that have VPC Service Controls perimeters. This document assumes you're familiar with [VPC Service Controls perimeters](/vpc-service-controls/docs/service-perimeters) , [shared datasets](/bigquery/docs/analytics-hub-introduction#shared_datasets) , [data exchanges](/bigquery/docs/analytics-hub-introduction#data_exchanges) , [listings](/bigquery/docs/analytics-hub-introduction#listings) , and [linked datasets](/bigquery/docs/analytics-hub-introduction#linked_datasets) .

A *caller project* is the network or client Google Cloud project that initiates the request, such as a SQL query or a Google Cloud CLI command.

## Create a data exchange

In the following diagram, the projects that contain the data exchange and the shared dataset are in different service perimeters:

**Figure 1.** VPC Service Controls rules for creating a data exchange.

In figure 1, the following components are labeled:

  - **Caller** : a BigQuery sharing administrator.
  - **Project R** : the caller project.
  - **Project E** : hosts the data exchange and listings.

As a BigQuery sharing administrator, when you [create a data exchange](/bigquery/docs/analytics-hub-manage-exchanges#create-exchange) in a different project than the caller project, you must add the following ingress and egress rules:

<table>
<thead>
<tr class="header">
<th><strong>Project</strong></th>
<th><strong>Rule</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Project R</td>
<td>Egress rule for project E</td>
</tr>
<tr class="even">
<td>Project E (data exchange)</td>
<td>Ingress rule for project R</td>
</tr>
</tbody>
</table>

## Create a listing

In the following diagram, the projects that contain the data exchange and the shared dataset are in different service perimeters:

**Figure 2.** VPC Service Controls rules for creating a listing.

In figure 2, the following components are labeled:

  - **Caller** : a BigQuery sharing administrator or publisher.
  - **Project R** : the caller project.
  - **Project E** : hosts the data exchange and listings.
  - **Project S** : hosts the shared dataset.

When you create a listing in a data exchange that is in a different project than the shared dataset, you must add the following ingress and egress rules to let BigQuery sharing publishers create a listing:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Project</strong></th>
<th><strong>Rule</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Project R</td>
<td><p>Egress rule for project E</p>
<p>Egress rule for project S</p></td>
</tr>
<tr class="even">
<td>Project E (data exchange)</td>
<td><p>Egress rule for project S</p>
<p>Ingress rule for project R</p></td>
</tr>
<tr class="odd">
<td>Project S (shared dataset)</td>
<td><p>Egress rule for project E</p>
<p>Ingress rule for project R</p></td>
</tr>
</tbody>
</table>

## Subscribe to a listing

In the following diagram, the projects that contain the listing and the linked dataset for that listing are in different service perimeters:

**Figure 3.** VPC Service Controls rules for subscribing to a listing.

In figure 3, the following components are labeled:

  - **Caller** : a BigQuery sharing subscriber.
  - **Project R** : the caller project.
  - **Project E** : hosts the data exchange and listings.
  - **Project L** : hosts the linked dataset.

As a BigQuery sharing subscriber, when you subscribe to a listing in a data exchange that is in a different project than your project, you must add the following ingress and egress rules:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Project</strong></th>
<th><strong>Rule</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Project R</td>
<td><p>Egress rule for project E</p>
<p>Egress rule for project L</p></td>
</tr>
<tr class="even">
<td>Project E (listing)</td>
<td><p>Egress rule for project L</p>
<p>Ingress rule for project R</p></td>
</tr>
<tr class="odd">
<td>Project L (linked dataset)</td>
<td><p>Egress rule for project E</p>
<p>Ingress rule for project R</p></td>
</tr>
</tbody>
</table>

## Query tables in a linked dataset

In the following diagram, the caller project and the project that contain the linked dataset are in different service perimeters:

**Figure 4.** VPC Service Controls rules for querying a linked dataset.

In figure 4, the following components are labeled:

  - **Caller** : a BigQuery sharing subscriber or any BigQuery job user of the linked dataset.
  - **Project R** : the caller project.
  - **Project L** : hosts the linked dataset.
  - **Project V** : hosts the shared dataset that contains the table.

When you, as a BigQuery sharing subscriber, query a table in the linked dataset, you must add the following ingress and egress rules:

<table>
<thead>
<tr class="header">
<th><strong>Project</strong></th>
<th><strong>Rule</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Project R</td>
<td>Egress rule for project L</td>
</tr>
<tr class="even">
<td>Project L (linked dataset)</td>
<td>Ingress rule for project R</td>
</tr>
</tbody>
</table>

## Query views in a linked dataset

This section describes the required VPC Service Controls rules for querying a view in a linked dataset. The rules vary depending on whether the view and its underlying base tables are in the same project or in separate projects.

### Scenario 1

In the following diagram, the projects that contain the linked dataset and the base tables associated with the view are in different service perimeters. The view (Project S) and the base table associated with the view (Project V) are in different projects:

**Figure 5.** VPC Service Controls rules for querying a view in a linked dataset.

In figure 5, the following components are labeled:

  - **Caller** : a BigQuery sharing subscriber or any BigQuery job user of the linked dataset.
  - **Project R** : the caller project.
  - **Project L** : hosts the linked dataset.
  - **Project S** : hosts the shared dataset.
  - **Project V** : hosts the dataset that contains the base tables associated with the view.

When you, as a BigQuery sharing subscriber, query a view in a linked dataset, you must add the following ingress and egress rules:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Project</strong></th>
<th><strong>Rule</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Project R</td>
<td><p>Egress rule for project L</p>
<p>Egress rule for project V</p></td>
</tr>
<tr class="even">
<td>Project L (linked dataset)</td>
<td><p>Ingress rule for project R</p>
<p>Egress rule for project V</p></td>
</tr>
<tr class="odd">
<td>Project V</td>
<td><p>Egress rule for project L</p>
<p>Ingress rule for project R</p></td>
</tr>
</tbody>
</table>

### Scenario 2

In the following diagram, the view (Project V) and the base table associated with the view (Project V) are in the same project:

**Figure 6.** VPC Service Controls rules for querying a view in a linked dataset.

In figure 6, the following components are labeled:

  - **Caller** : a BigQuery sharing subscriber or any BigQuery job user of the linked dataset.
  - **Project R** : the caller project.
  - **Project L** : hosts the linked dataset.
  - **Project V** : hosts both the view and the base tables associated with the view.

When you, as a BigQuery sharing subscriber, query a view in a linked dataset, you must add the following ingress and egress rules:

<table>
<thead>
<tr class="header">
<th><strong>Project</strong></th>
<th><strong>Rule</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Project R</td>
<td><p>Egress rule for project L</p></td>
</tr>
<tr class="even">
<td>Project L (linked dataset)</td>
<td><p>Ingress rule for project R</p></td>
</tr>
</tbody>
</table>

## Query authorized views in a linked dataset

In the following diagram, the authorized view and the base table associated with the authorized view (Project V) are in the same project:

**Figure 7.** VPC Service Controls rules for querying a view in a linked dataset.

In figure 7, the following components are labeled:

  - **Caller** : a BigQuery sharing subscriber or any BigQuery job user of the linked dataset.
  - **Project R** : the caller project.
  - **Project L** : hosts the linked dataset.
  - **Project V** : hosts both the authorized view and the base tables associated with the view.

**Caution:** If the shared dataset and the base table associated with the authorized view are not in the same project and VPC Service Controls perimeter, the service perimeter rejects the subscriber's query. To resolve this issue, verify that the shared dataset and the base table associated with the authorized view are in the same project.

When you, as a BigQuery sharing subscriber, query a view in a linked dataset, you must add the following ingress and egress rules:

<table>
<thead>
<tr class="header">
<th><strong>Project</strong></th>
<th><strong>Rule</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Project R</td>
<td><p>Egress rule for project L</p></td>
</tr>
<tr class="even">
<td>Project L (linked dataset)</td>
<td><p>Ingress rule for project R</p></td>
</tr>
</tbody>
</table>

## Limitations

BigQuery sharing doesn't support [method-based rules](/vpc-service-controls/docs/ingress-egress-rules) . You must allow all methods to enable method-based rules. For example:

``` text
          ingressTo:
            operations:
            - methodSelectors:
              - method: '*'
              serviceName: analyticshub.googleapis.com
            resources:
            - projects/PROJECT_ID
```

If BigQuery resources are also protected by service perimeters, you must allow ingress and egress rules for the BigQuery service. Allowing ingress and egress rules is not required when you create a data exchange. The ingress and egress rules for BigQuery are similar to those for BigQuery sharing. For example:

``` text
          ingressTo:
            operations:
            - methodSelectors:
              - method: '*'
              serviceName: bigquery.googleapis.com
            resources:
            - projects/PROJECT_ID
```

## What's next

  - Learn about [troubleshooting VPC Service Controls problems](/vpc-service-controls/docs/troubleshooting) .
  - Learn about [ingress and egress rules](/vpc-service-controls/docs/ingress-egress-rules) .
  - Learn about [configuring ingress and egress policies](/vpc-service-controls/docs/configuring-ingress-egress-policies) .
  - Learn about [creating a listing](/bigquery/docs/analytics-hub-manage-listings#create_a_listing) .
  - Learn about [subscribing to a listing](/bigquery/docs/analytics-hub-view-subscribe-listings#subscribe-listings) .
  - Learn about [Sharing audit logging](/bigquery/docs/analytics-hub-audit-logging) .
