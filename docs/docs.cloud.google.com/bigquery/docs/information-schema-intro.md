# Introduction to INFORMATION\_SCHEMA

The BigQuery `  INFORMATION_SCHEMA  ` views are read-only, system-defined views that provide metadata information about your BigQuery objects. The following table lists all `  INFORMATION_SCHEMA  ` views that you can query to retrieve metadata information:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Resource type</th>
<th>INFORMATION_SCHEMA View</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Access control</td>
<td><code dir="ltr" translate="no">         OBJECT_PRIVILEGES                science       </code></td>
</tr>
<tr class="even">
<td>BI Engine</td>
<td><code dir="ltr" translate="no">         BI_CAPACITIES       </code><br />
<code dir="ltr" translate="no">         BI_CAPACITY_CHANGES       </code></td>
</tr>
<tr class="odd">
<td>Configurations</td>
<td><code dir="ltr" translate="no">         EFFECTIVE_PROJECT_OPTIONS       </code><br />
<code dir="ltr" translate="no">         ORGANIZATION_OPTIONS       </code><br />
<code dir="ltr" translate="no">         ORGANIZATION_OPTIONS_CHANGES       </code><br />
<code dir="ltr" translate="no">         PROJECT_OPTIONS       </code><br />
<code dir="ltr" translate="no">         PROJECT_OPTIONS_CHANGES       </code><br />
</td>
</tr>
<tr class="even">
<td>Datasets</td>
<td><code dir="ltr" translate="no">         SCHEMATA                 SCHEMATA_LINKS                 SCHEMATA_OPTIONS                 SHARED_DATASET_USAGE                 SCHEMATA_REPLICAS                 SCHEMATA_REPLICAS_BY_FAILOVER_RESERVATION       </code></td>
</tr>
<tr class="odd">
<td>Jobs</td>
<td><code dir="ltr" translate="no">         JOBS_BY_PROJECT                 †         </code><br />
<code dir="ltr" translate="no">         JOBS_BY_USER       </code><br />
<code dir="ltr" translate="no">         JOBS_BY_FOLDER       </code><br />
<code dir="ltr" translate="no">         JOBS_BY_ORGANIZATION       </code></td>
</tr>
<tr class="even">
<td>Jobs by timeslice</td>
<td><code dir="ltr" translate="no">         JOBS_TIMELINE_BY_PROJECT                 †         </code><br />
<code dir="ltr" translate="no">         JOBS_TIMELINE_BY_USER       </code><br />
<code dir="ltr" translate="no">         JOBS_TIMELINE_BY_FOLDER       </code><br />
<code dir="ltr" translate="no">         JOBS_TIMELINE_BY_ORGANIZATION       </code></td>
</tr>
<tr class="odd">
<td>Recommendations and insights</td>
<td><code dir="ltr" translate="no">         INSIGHTS                science       </code><br />
<code dir="ltr" translate="no">         RECOMMENDATIONS                science       </code><br />
<code dir="ltr" translate="no">         RECOMMENDATIONS_BY_ORGANIZATION                science       </code></td>
</tr>
<tr class="even">
<td>Reservations</td>
<td><code dir="ltr" translate="no">         ASSIGNMENTS_BY_PROJECT                 †         </code><br />
<code dir="ltr" translate="no">         ASSIGNMENT_CHANGES_BY_PROJECT                 †         </code><br />
<code dir="ltr" translate="no">         CAPACITY_COMMITMENTS_BY_PROJECT                 †         </code><br />
<code dir="ltr" translate="no">         CAPACITY_COMMITMENT_CHANGES_BY_PROJECT                 †         </code><br />
<code dir="ltr" translate="no">         RESERVATIONS_BY_PROJECT                 †         </code><br />
<code dir="ltr" translate="no">         RESERVATION_CHANGES_BY_PROJECT                 †         </code><br />
<code dir="ltr" translate="no">         RESERVATIONS_TIMELINE_BY_PROJECT                 †         </code></td>
</tr>
<tr class="odd">
<td>Routines</td>
<td><code dir="ltr" translate="no">         PARAMETERS       </code><br />
<code dir="ltr" translate="no">         ROUTINES       </code><br />
<code dir="ltr" translate="no">         ROUTINE_OPTIONS       </code></td>
</tr>
<tr class="even">
<td>Search indexes</td>
<td><code dir="ltr" translate="no">         SEARCH_INDEXES       </code><br />
<code dir="ltr" translate="no">         SEARCH_INDEX_COLUMNS       </code><br />
<code dir="ltr" translate="no">         SEARCH_INDEX_COLUMN_OPTIONS                science       </code><br />
<code dir="ltr" translate="no">         SEARCH_INDEX_OPTIONS       </code><br />
<code dir="ltr" translate="no">         SEARCH_INDEXES_BY_ORGANIZATION       </code></td>
</tr>
<tr class="odd">
<td>Sessions</td>
<td><code dir="ltr" translate="no">         SESSIONS_BY_PROJECT                 †         </code><br />
<code dir="ltr" translate="no">         SESSIONS_BY_USER       </code></td>
</tr>
<tr class="even">
<td>Streaming</td>
<td><code dir="ltr" translate="no">         STREAMING_TIMELINE_BY_PROJECT                 †         </code><br />
<code dir="ltr" translate="no">         STREAMING_TIMELINE_BY_FOLDER       </code><br />
<code dir="ltr" translate="no">         STREAMING_TIMELINE_BY_ORGANIZATION       </code></td>
</tr>
<tr class="odd">
<td>Tables</td>
<td><code dir="ltr" translate="no">         COLUMNS       </code><br />
<code dir="ltr" translate="no">         COLUMN_FIELD_PATHS       </code><br />
<code dir="ltr" translate="no">         CONSTRAINT_COLUMN_USAGE       </code><br />
<code dir="ltr" translate="no">         KEY_COLUMN_USAGE       </code><br />
<code dir="ltr" translate="no">         PARTITIONS                science       </code><br />
<code dir="ltr" translate="no">         TABLES       </code><br />
<code dir="ltr" translate="no">         TABLE_OPTIONS       </code><br />
<code dir="ltr" translate="no">         TABLE_CONSTRAINTS       </code><br />
<code dir="ltr" translate="no">         TABLE_SNAPSHOTS       </code><br />
<code dir="ltr" translate="no">         TABLE_STORAGE_BY_PROJECT                 †         </code><br />
<code dir="ltr" translate="no">         TABLE_STORAGE_BY_FOLDER       </code><br />
<code dir="ltr" translate="no">         TABLE_STORAGE_BY_ORGANIZATION       </code><br />
<code dir="ltr" translate="no">         TABLE_STORAGE_USAGE_TIMELINE                science       </code><br />
<code dir="ltr" translate="no">         TABLE_STORAGE_USAGE_TIMELINE_BY_FOLDER                science       </code><br />
<code dir="ltr" translate="no">         TABLE_STORAGE_USAGE_TIMELINE_BY_ORGANIZATION                science       </code></td>
</tr>
<tr class="even">
<td>Vector indexes</td>
<td><code dir="ltr" translate="no">         VECTOR_INDEXES       </code><br />
<code dir="ltr" translate="no">         VECTOR_INDEX_COLUMNS       </code><br />
<code dir="ltr" translate="no">         VECTOR_INDEX_OPTIONS       </code></td>
</tr>
<tr class="odd">
<td>Views</td>
<td><code dir="ltr" translate="no">         VIEWS       </code><br />
<code dir="ltr" translate="no">         MATERIALIZED_VIEWS       </code></td>
</tr>
<tr class="even">
<td>Write API</td>
<td><code dir="ltr" translate="no">         WRITE_API_TIMELINE_BY_PROJECT                 †         </code><br />
<code dir="ltr" translate="no">         WRITE_API_TIMELINE_BY_FOLDER       </code><br />
<code dir="ltr" translate="no">         WRITE_API_TIMELINE_BY_ORGANIZATION       </code></td>
</tr>
</tbody>
</table>

<sup>†</sup> For `  *BY_PROJECT  ` views, the `  BY_PROJECT  ` suffix is optional. For example, querying `  INFORMATION_SCHEMA.JOBS_BY_PROJECT  ` and `  INFORMATION_SCHEMA.JOBS  ` return the same results.

**Note:** Not all `  INFORMATION_SCHEMA  ` views are supported for [BigQuery Omni system tables](/bigquery/docs/omni-introduction#limitations) . You can view resource metadata with `  INFORMATION_SCHEMA  ` for [Amazon S3](/bigquery/docs/omni-aws-create-external-table#view_resource_metadata) and [Azure Storage](/bigquery/docs/omni-azure-create-external-table#view_resource_metadata_with_information_schema) .

## Pricing

For projects that use on-demand pricing, queries against `  INFORMATION_SCHEMA  ` views incur a minimum of 10 MB of data processing charges, even if the bytes processed by the query are less than 10 MB. 10 MB is the minimum billing amount for on-demand queries. For more information, see [On-demand pricing](https://cloud.google.com/bigquery/pricing#on_demand_pricing) .

For projects that use capacity-based pricing, queries against `  INFORMATION_SCHEMA  ` views and tables consume your purchased BigQuery slots. For more information, see [capacity-based pricing](https://cloud.google.com/bigquery/pricing#capacity_compute_analysis_pricing) .

Because `  INFORMATION_SCHEMA  ` queries are not cached, you are charged each time that you run an `  INFORMATION_SCHEMA  ` query, even if the query text is the same each time you run it.

You are not charged storage fees for the `  INFORMATION_SCHEMA  ` views.

## Syntax

An `  INFORMATION_SCHEMA  ` view needs to be qualified with a dataset or region.

**Note:** You must [specify a location](/bigquery/docs/locations#specify_locations) to query an `  INFORMATION_SCHEMA  ` view. Querying an `  INFORMATION_SCHEMA  ` view fails with the following error if the location of the query execution doesn't match the location of the dataset or regional qualifier used:  

``` text
Table myproject: region-us.INFORMATION_SCHEMA.[VIEW] not found in location US
```

### Dataset qualifier

When present, a dataset qualifier restricts results to the specified dataset. For example:

``` text
-- Returns metadata for tables in a single dataset.
SELECT * FROM myDataset.INFORMATION_SCHEMA.TABLES;
```

The following `  INFORMATION_SCHEMA  ` views support dataset qualifiers:

  - `  COLUMNS  `
  - `  COLUMN_FIELD_PATHS  `
  - `  MATERIALIZED_VIEWS  `
  - `  PARAMETERS  `
  - `  PARTITIONS  `
  - `  ROUTINES  `
  - `  ROUTINE_OPTIONS  `
  - `  TABLES  `
  - `  TABLE_OPTIONS  `
  - `  VIEWS  `

### Region qualifier

Region qualifiers are represented using a `  region- REGION  ` syntax. Any [dataset location name](/bigquery/docs/locations) can be used for `  REGION  ` . For example, the following region qualifiers are valid:

  - `  region-us  `
  - `  region-asia-east2  `
  - `  region-europe-north1  `

When present, a region qualifier restricts results to the specified location. [Region qualifiers](/bigquery/docs/locations#locations_and_regions) aren't hierarchical, which means the EU multi-region does not include `  europe-*  ` regions nor does the US multi-region include the `  us-*  ` regions. For example, the following query returns metadata for all datasets in the `  US  ` multi-region for the project in which the query is executing, but doesn't include datasets in the `  us-west1  ` region:

``` text
-- Returns metadata for all datasets in the US multi-region.
SELECT * FROM region-us.INFORMATION_SCHEMA.SCHEMATA;
```

The following `  INFORMATION_SCHEMA  ` views don't support region qualifiers:

  - [`  INFORMATION_SCHEMA.PARTITIONS  `](/bigquery/docs/information-schema-partitions#scope_and_syntax)
  - [`  INFORMATION_SCHEMA.SEARCH_INDEXES  `](/bigquery/docs/information-schema-indexes#scope_and_syntax)
  - [`  INFORMATION_SCHEMA.SEARCH_INDEX_COLUMNS  `](/bigquery/docs/information-schema-index-columns)
  - [`  INFORMATION_SCHEMA.SEARCH_INDEX_OPTIONS  `](/bigquery/docs/information-schema-index-options)

If neither a region qualifier nor a dataset qualifier is specified, you will receive an error.

Queries against a region-qualified `  INFORMATION_SCHEMA  ` view run in the region that you specify, which means that you can't write a single query to join data from views in different regions. To combine `  INFORMATION_SCHEMA  ` views from multiple regions, read and combine the query results locally, or [copy](/bigquery/docs/managing-tables#copy_tables_across_regions) the resulting tables to a common region.

### Project qualifier

When present, a project qualifier restricts results to the specified project. For example:

``` text
-- Returns metadata for the specified project and region.
SELECT * FROM myProject.`region-us`.INFORMATION_SCHEMA.TABLES;

-- Returns metadata for the specified project and dataset.
SELECT * FROM myProject.myDataset.INFORMATION_SCHEMA.TABLES;
```

All `  INFORMATION_SCHEMA  ` views support project qualifiers. If a project qualifier is not specified, the view will default to the project in which the query is executing.

Specifying a project qualifier for organization-level views (e.g. `  STREAMING_TIMELINE_BY_ORGANIZATION  ` ) has no impact on the results.

## Limitations

  - BigQuery `  INFORMATION_SCHEMA  ` queries must be in GoogleSQL syntax. `  INFORMATION_SCHEMA  ` does not support legacy SQL.
  - `  INFORMATION_SCHEMA  ` query results are not cached.
  - `  INFORMATION_SCHEMA  ` views cannot be used in DDL statements.
  - `  INFORMATION_SCHEMA  ` views don't contain information about [hidden datasets](/bigquery/docs/datasets#hidden_datasets) .
  - `  INFORMATION_SCHEMA  ` queries with region qualifiers might include metadata from resources in that region from [deleted datasets that are within your time travel window](/bigquery/docs/restore-deleted-datasets) .
  - When you list resources from an `  INFORMATION_SCHEMA  ` view, the permissions are checked only at the parent level, not at an individual row level. Therefore, any [deny policy](/bigquery/docs/control-access-to-resources-iam#deny_access_to_a_resource) ( [preview](https://cloud.google.com/products#product-launch-stages) ) that conditionally targets an individual row using tags is ignored.
