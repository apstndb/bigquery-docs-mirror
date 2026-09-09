---
name: documents/docs.cloud.google.com/bigquery/docs/migration/migration-lineage
uri: https://docs.cloud.google.com/bigquery/docs/migration/migration-lineage
title: Plan a migration with migration lineage
description: Generate a lineage graph to visualize how data flows and how data is connected in your source database as you plan a BigQuery data warehouse migration.
data_source: docs.cloud.google.com
---

# Plan a migration with migration lineage

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> **Note:** To get support or provide feedback for this feature, contact <bq-edw-migration-support@google.com> .

You can use the migration lineage service to visualize data flow and connections in your source database when you plan a BigQuery data warehouse migration.

When you create a migration lineage, the lineage service provides a graph that visualizes how data moves through your source system, and how each table or view in your source system is connected, as the following diagram shows:

![A migration lineage showing a graph of the data flow.](https://docs.cloud.google.com/static/bigquery/images/lineage-view-graph.png)

The migration lineage service supports the following SQL dialects:

  - Amazon Redshift SQL
  - Snowflake SQL
  - Teradata SQL
  - GoogleSQL (BigQuery)

## Limitations

The lineage service processes the first 5 GB of the oldest logs from your source database.

## Supported locations

The migration lineage service is available in select locations. For more information, see [BigQuery SQL translator and lineage service locations](https://docs.cloud.google.com/bigquery/docs/locations#sql-translator-loc) .

## Required permissions

To get the permissions that you need to use the migration lineage service, ask your administrator to grant you the [MigrationWorkflow Editor](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.editor) ( `roles/bigquerymigration.editor` ) IAM role on the project. For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

This predefined role contains the permissions required to use the migration lineage service. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to use the migration lineage service:

  - `bigquerymigration.workflows.create`
  - `bigquerymigration.workflows.get`
  - `bigquerymigration.lineageDbs.query`

You might also be able to get these permissions with [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

For more information on IAM roles and permissions in BigQuery, see [BigQuery IAM roles and permissions](https://docs.cloud.google.com/bigquery/docs/access-control) .

## Create a migration lineage

To create a migration lineage, you first run the `dwh-migration-dumper` tool to generate source input SQL log files that you upload to Cloud Storage. After you upload the input files to Cloud Storage, you can generate the migration lineage with the Google Cloud console or the BigQuery Migration API.

### Run the `dwh-migration-dumper` tool

Select one of the following options:

### Amazon Redshift

To build and view a migration lineage on an Amazon Redshift database, do the following:

1.  [Run the `dwh-migration-dumper` tool](https://docs.cloud.google.com/bigquery/docs/migration-assessment#redshift) to generate a dump of your source system files.
2.  [Upload the query logs to Cloud Storage](https://docs.cloud.google.com/bigquery/docs/migration-assessment#redshift_1) .

### Snowflake

To build and view a migration lineage on an Snowflake database, do the following:

1.  [Run the `dwh-migration-dumper` tool](https://docs.cloud.google.com/bigquery/docs/migration-assessment#snowflake) to generate a dump of your source system files.
2.  [Upload the query logs to Cloud Storage](https://docs.cloud.google.com/bigquery/docs/migration-assessment#snowflake_1) .

### Teradata

To build and view a migration lineage on an Teradata database, do the following:

1.  [Run the `dwh-migration-dumper` tool](https://docs.cloud.google.com/bigquery/docs/migration-assessment#teradata) to generate a dump of your source system files.
2.  [Upload the query logs to Cloud Storage](https://docs.cloud.google.com/bigquery/docs/migration-assessment#teradata_1) .

### BigQuery

To build and view a migration lineage on a BigQuery database, do the following:

1.  Grant the account or service account the following roles:
    
      - [BigQuery Metadata Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.metadataViewer) ( `roles/bigquery.metadataViewer` )
      - [Data Catalog Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/datacatalog#datacatalog.viewer) ( `roles/datacatalog.viewer` )

2.  Install the [`dwh-migration-dumper` tool](https://docs.cloud.google.com/bigquery/docs/generate-metadata#install-dumper) .

3.  To generate metadata and query logs, run the `dwh-migration-dumper` tool. These metadata and query logs are contained in one or more ZIP files.
    
        dwh-migration-dumper --connector bigquery
        
        dwh-migration-dumper --connector bigquery-logs

4.  Upload the ZIP files to a Cloud Storage bucket. For more information about creating buckets and uploading files to Cloud Storage, see [Create a bucket](https://docs.cloud.google.com/storage/docs/creating-buckets) and [Upload objects from a file system](https://docs.cloud.google.com/storage/docs/uploading-objects) .

### Generate the migration lineage

After you upload the ZIP files that contain the metadata and query logs to Cloud Storage, you can generate the migration lineage. Select one of the following options:

### Console

1.  Go to the **Your migration services** page.

2.  Under **Translate SQL** , click **Translate** \> **Batch translation** .

3.  Under **Translation configuration** , enter the following:
    
    1.  For **Display name** , specify a name for the lineage job. The name can contain letters, numbers or underscores.
    2.  For **Processing Location** , select the location where you want the lineage job to run.
    3.  For **Source dialect** , select your source SQL dialect.
    4.  For **Target dialect** , select **GoogleSQL** .

4.  Click **Next** .

5.  Under **File location details** , do the following:
    
    1.  For **Output directory location** , specify the path to a Cloud Storage bucket to save your translation output files. You can type the path in the format `  bucket_name / folder_name / ` or click **Browse** .
    2.  For **Input directory location** , specify the path to the Cloud Storage folder containing the log ZIP files that you uploaded earlier. You can type the path in the format `  bucket_name / folder_name / ` or click **Browse** . You can also name the subdirectory of your output files in the **Output subdirectory name** field.
    3.  You can add additional input files by clicking **Add an input directory location** .

6.  Click **Next** .

7.  Select the **Lineage from query logs** checkbox.

8.  Click **Create** .

The lineage job is now running. The job can take several hours to complete depending on your input size. After the job is complete, the tool provides a link to the generated migration lineage.

### API

To create a lineage job, run the following `curl` command:

``` 
  curl -d "{
    \"tasks\": {
      \"TASK_NAME\": {
        \"type\": \"Experimental_Lineage\",
        \"translation_details\": {
          \"target_base_uri\": \"BUCKET_PATH\",
          \"source_target_mapping\": {
            \"source_spec\": {
              \"base_uri\": \"BUCKET_PATH\"
            }
          },
          \"target_types\": \"LINEAGE\"
        }
      }
    }
  }
  " \
    -H "Content-Type:application/json" \
    -H "Authorization: Bearer TOKEN" -X POST https://bigquerymigration.googleapis.com/v2/projects/PROJECT_ID/locations/LOCATION/workflows
```

Replace the following:

  - `  TASK_NAME  ` : a name to identify this lineage job.
  - `  BUCKET_PATH  ` : the path to the Cloud Storage bucket that contains your input ZIP files.
  - `  PROJECT_ID  ` : the project ID to your Google Cloud project.
  - `  LOCATION  ` : a processing location. This value must either be `eu` or `us` .

This call returns a message similar to the following:

``` 
  {
    "name": "projects/PROJECT_ID/locations/LOCATION/workflows/WORKFLOW_ID",
    "tasks": {
      "task_name": { /*...*/ }
    },
    "state": "RUNNING"
  }
```

The lineage job is now running. The job can take several hours to complete depending on your input size. To check the status of the lineage job, run the following `curl` command with the workflow ID:

``` 
  curl \
  -H "Content-Type:application/json" \
  -H "Authorization:Bearer " -X GET https://bigquerymigration.googleapis.com/v2/projects/PROJECT_ID/locations/LOCATION/workflows/WORKFLOW_ID
```

After the job is complete, the tool provides a link to the generated lineage view.

## Open the migration lineage

After you have generated a migration lineage, you can open the migration lineage by using one of the following options:

### Console

1.  Go to the **Your migration services** page.

2.  Under **Translate SQL** , click **View recent** .

3.  On the **SQL translations** page, click the job name to select the complete lineage job. Lineage jobs have the output value `Lineage` .

4.  On the **Translation details** page, click **Data lineage** .

### API

To open a completed migration lineage, run the following `curl` command with the [BigQuery Migration API](https://docs.cloud.google.com/bigquery/docs/reference/migration/rest) :

``` 
  curl \
  -H "Content-Type:application/json" \
  -H "Authorization:Bearer " -X GET https://bigquerymigration.googleapis.com/v2/projects/PROJECT_ID/locations/LOCATION/workflows/WORKFLOW_ID
```

Replace the following:

  - `  PROJECT_ID  ` : the project ID to your Google Cloud project.
  - `  LOCATION  ` : a processing location. This value must either be `eu` or `us` .
  - `  WORKFLOW_ID  ` : the workflow ID of the generated lineage.

Navigate to the link included in the `taskResult.translationTaskResult.consoleUri` field of the output message.

## Work with migration lineage

The following sections describe ways you can use migration lineage to work with your source data and database.

### Understand migration lineage terms

The following terms are used in a migration lineage:

| Terms               | Description                                                                                                                                                                                                                                                                                                                                                                                         |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Scripts             | SQL scripts and other programs that are visible in the database logs ingested during lineage building. Scripts are composed of statements, which are most commonly single SQL statements.                                                                                                                                                                                                           |
| Nodes               | The vertices of the lineage graph. These consist of *tables* and *columns* .                                                                                                                                                                                                                                                                                                                        |
| Tables              | Also referred to as *relations* , including ordinary tables, views, structured files, and other table-like resources.                                                                                                                                                                                                                                                                               |
| Columns             | Also referred to as *attributes* , including table columns, view projections, pseudocolumns, column-like fields in files and other resources, and sub-columns such as struct fields.                                                                                                                                                                                                                |
| Edges               | Connections between lineage nodes that indicate interactions due to a pipeline executing a script that read or wrote those nodes. Edges are annotated with timestamps, predicates, and other metadata from when the edge was derived. A node that is adjacent to another node with an edge is called a *direct connection* ; a path of edges between two nodes is called an *indirect connection* . |
| Lineage edges       | Directional edges that indicate that the source node was included in a clause such as a `FROM` , `WHERE` , or `GROUP BY` clause that influenced the data of the target node.                                                                                                                                                                                                                        |
| Users and pipelines | Metadata labels provided by the source database about who and what executed scripts. They have no inherent meaning to the lineage engine, but are used to group scripts together by origin.                                                                                                                                                                                                         |

The following sections describe the different pages in a migration lineage.

### Review the landing page

The landing page of the migration lineage shows the ID of the lineage job, a search field for locating lineage objects by name, and a suggestions list highlighting some lineage objects that might be of interest. The page also includes the total counts of tables, pipelines, and users across the migration lineage.

To navigate to a particular table, view, or column, search for the object in the search field, or click one of the suggested objects on the landing page.

> **Note:** As you review the landing page, verify that the total object counts matches with the number of objects in your source database. If the number of tables is lower than expected, it might indicate that there was an error in the lineage view generation. If this result is the case, confirm that you used the correct log file, and that your logs are below the 5 GB limit, and then generate the migration lineage again.

### Review the node page

To review the nodes in your migration lineage, click one of the following tabs.

#### Data Flow tab

The **Data Flow** tab shows a visual representation of a portion of the lineage graph. It is the default page when you view a table or column for the first time in the lineage service. The graph visualizes how data moves through your source system. Nodes in this graph represent tables or views, while edges between the nodes represent data flowing from the nodes on the left, towards the nodes on the right.

Each table in the **Data Flow** graph shows its unqualified name. To see a table's fully qualified name with the database and schema prefix, hold the pointer over the node to show its tooltip. Each table indicates its schema as indicated by the vertical bar on the node. All schemas in the lineage are sorted alphabetically and are assigned a color, so tables in the same schema have the same colored bars, and tables in schemas with similar names have similarly colored bars.

Each node displays an icon, which indicates the node's properties:

  - monitor : a view, not a table.
  - cached : a table that is always fully refreshed (truncated, and then rewritten). Click the icon to view scripts adjacent to this table.
  - cached : a table that is not always fully refreshed (truncated, and then rewritten). Click the icon to view scripts adjacent to this table.
  - timer : a table that was short lived. Hold the pointer over the icon to view the duration for which the table existed.
  - snowflake : a table that was last written more more than seven days ago, which suggests a table with static or infrequently-written data.

To review the objects in the **Data Flow** graph, do the following:

  - To view a list of table columns, click a table. This view includes the name of each column as well as its data type, as determined from a provided metadata dump or deduced from the SQL seen in the query logs.

  - To view the column-level lineage graph for a column, click a column. In the column-level lineage graph, the edges represent data flows that affect the target column.

  - To view details about an edge, click an edge in the graph. This view includes links to the SQL scripts that induced the edge.
    
    An edge is generated from a source node to a target node when a SQL statement references the source node while the statement is computing data that is inserted into the target node. Typically, this involves transfer of data from the source to the target, but the **Data Flow** tab also shows an edge when the source node is used in a `WHERE` or `GROUP BY` clause that affects the target. To filter for data transfers only, toggle the **Show non-data edges** button in the toolbar.

> **Note:** To help with navigating large migration lineages, you can refocus the graph on a node by clicking the fully qualified name of the node in the sidebar or in the node's tooltip.

#### Connections tab

The **Connections** tab of a lineage node displays a list of nearby nodes in the lineage graph. By default, connected nodes are sorted by the distance of the shortest path from the current node—nodes that require fewer edges to reach from the current node are listed first. You can change the sorting with the **Sort** option.

The connections list includes both upstream (producer) and downstream (consumer) nodes of the current node by default. You can change this filter with the **Type** control. In the **Distance** column, nodes that are upstream of the current node are shown with an upward-pointing arrow with the distance of the shortest backward path to that node from the current node; likewise, nodes that are downstream of the current node are shown with a downward-pointing arrow with the distance of the shortest forward path to that node from the current node. A node can be both upstream and downstream of the current node if it is part of a cycle.

To download a file containing all of the displayed nodes, click **download CSV**

#### Users tab

The **Users** tab of a node shows users who ran scripts that read or wrote the node or nodes that are upstream or downstream of it. By default, the user who performed the most separate actions is listed first. You can change the sorting with the **Sort** option.

To download a file containing all of the displayed user, click **download CSV** .

#### Pipelines tab

The **Pipelines** tab of a node shows the pipelines that ran scripts that read or wrote the node or nodes that are upstream or downstream of it. By default, the pipeline that performed the most separate actions is listed first. You can change the sorting with the **Sort** option.

To download a file containing all of the displayed pipelines, click **download CSV** .

#### Code tab

The **Code** tab for a node shows all the SQL scripts seen in the input files that read data from or wrote data to that node. Mentions of the node are highlighted in the SQL text. Click a script to expand the full text. You can change the filter settings to filter the list of displayed scripts.

To download a file containing all of the displayed scripts, click **download CSV** .

### Review the edge page

To review the node edges in your lineage graph, click one of the following tabs.

#### Details tab

The **Details** tab for an edge displays predicates and categories, which describe the operations performed by scripts that induced the edge.

Predicates are notated as three-part codes that are separated by hyphens. The first part is either `r` , indicating that the source of the edge is a relation, or `a` , indicating that the source of the edge is an attribute. The second part is one of the following abbreviations that indicates the way the source node influenced the data in the target node:

  - `has` : the source relation contains the target attribute.
  - `dat` : the source copies or transfers data to the target.
  - `res` : the source filters or restricts the cardinality of the target in a clause such as `WHERE` , `HAVING` , or `JOIN ON` .
  - `grp` : the source is used in a `GROUP BY` clause that affects the target.

The third part is also either `r` or `a` , indicating whether the target of the edge is a relation or an attribute.

Edge categories can include the following:

  - `dat` predicates:
      - `AGGREGATE` : the source was used in an aggregate computation that wrote the target.
      - `EXACT_COPY` : data from the source was copied in its entirety to the target.
      - `FUNCTION` : the source was used to compute the target.
      - `IDENTITY_COPY` : the target was not computed. The target was a literal copy of the source without any casts or conversions.
      - `PARTITION_PROMOTION` : the target contains data from the source as a result of promoting a partition of the source to the target.
      - `WEAK_COPY` : data from the source was copied at least partially to the target.
  - `res` predicates:
      - `FILTER` : the source was used in a comparison that wrote the target.
      - `KEY` : data from the source was used as a key in a join comparison which wrote the target.
  - `grp` predicates:
      - `GROUP` : data from the source was used as a key in a `GROUP BY` clause which affects the target.

#### Code tab

The **Code** tab for an edge shows the SQL scripts that induced that edge. The source and target nodes of the edge are highlighted where they are mentioned in the SQL text.

## What's next

  - Run a [migration assessment](https://docs.cloud.google.com/bigquery/docs/migration-assessment) to assess the feasibility and potential benefits of migrating your data warehouse to BigQuery.
  - Use the SQL translation service, such as the [interactive SQL translator](https://docs.cloud.google.com/bigquery/docs/interactive-sql-translator) , the [translation API](https://docs.cloud.google.com/bigquery/docs/api-sql-translator) , and the [batch SQL translator](https://docs.cloud.google.com/bigquery/docs/batch-sql-translator) to automate the conversion of your SQL queries into GoogleSQL, including Gemini-enhanced SQL customization.
