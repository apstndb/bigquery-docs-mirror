# Generate dataset insights

**Preview**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

This document describes how to generate dataset insights for BigQuery datasets. Dataset insights help you understand relationships between tables in a dataset by generating relationship graphs and cross-table queries.

Dataset insights help you accelerate the exploration of datasets with multiple tables by automatically discovering and visualizing relationships between tables in a graph, identifying primary-key and foreign-key relationships, and generating sample cross-table queries. This is useful for understanding data structure without documentation, discovering schema-defined, usage-based, or AI-inferred relationships between tables, and generating complex queries that join multiple tables.

For an overview of table and dataset insights, see [Data insights overview](/bigquery/docs/data-insights) .

## Before you begin

Data insights are generated using [Gemini in BigQuery](/gemini/docs/bigquery/overview) . To start generating insights, you must first [set up Gemini in BigQuery](/gemini/docs/bigquery/set-up-gemini) .

**Note** : Gemini in BigQuery is part of Gemini for Google Cloud and doesn't support the same compliance and security offerings as BigQuery. You should only set up Gemini in BigQuery for BigQuery projects that don't require [compliance offerings that aren't supported by Gemini for Google Cloud](/gemini/docs/discover/certifications) . For information about how to turn off or prevent access to Gemini in BigQuery, see [Turn off Gemini in BigQuery](/bigquery/docs/gemini-set-up#turn-off) .

### Enable APIs

**Important:** To enable any API in your project, ask your administrator to grant you the `  serviceusage.services.enable  ` permission on your project.

To use data insights, enable the following APIs in your project: Dataplex API, BigQuery API, and Gemini for Google Cloud API.

**Roles required to enable APIs**

To enable APIs, you need the Service Usage Admin IAM role ( `  roles/serviceusage.serviceUsageAdmin  ` ), which contains the `  serviceusage.services.enable  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .

For more information about enabling the Gemini for Google Cloud API, see [Enable the Gemini for Google Cloud API in a Google Cloud project](/gemini/docs/discover/set-up-gemini#enable-api) .

### Complete a data profile scan

To improve the quality of insights, generate [data profiling results](/bigquery/docs/data-profile-scan) for tables in your dataset.

### Required roles

To get the permissions that you need to generate, manage, and retrieve dataset insights, ask your administrator to grant you the following IAM roles:

  - To generate, manage, and retrieve insights:
      - Dataplex DataScan Editor ( `  roles/dataplex.dataScanEditor  ` ) or Dataplex DataScan Administrator ( `  roles/dataplex.dataScanAdmin  ` ) on project
      - [BigQuery Data Editor](/iam/docs/roles-permissions/bigquery#bigquery.dataEditor) ( `  roles/bigquery.dataEditor  ` ) on tables
      - BigQuery User ( `  roles/bigquery.user  ` ) or BigQuery Studio User ( `  roles/bigquery.studioUser  ` ) on project.
  - To view insights:
      - [Dataplex DataScan DataViewer](/iam/docs/roles-permissions/dataplex#dataplex.dataScanDataViewer) ( `  roles/dataplex.dataScanDataViewer  ` ) on project
      - [BigQuery Data Viewer](/iam/docs/roles-permissions/bigquery#bigquery.dataViewer) ( `  roles/bigquery.dataViewer  ` ) on dataset

For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

To see the exact permissions that are required to generate insights, expand the **Required permissions** section:

#### Required permissions

  - `  bigquery.datasets.get  ` : read dataset metadata
  - `  bigquery.jobs.create  ` : create jobs
  - `  bigquery.tables.get  ` : get table metadata
  - `  bigquery.tables.getData  ` : get table data and metadata
  - `  dataplex.datascans.create  ` : create DataScan resource
  - `  dataplex.datascans.get  ` : read DataScan resource metadata
  - `  dataplex.datascans.getData  ` : read DataScan execution results
  - `  dataplex.datascans.run  ` : run on-demand DataScan

## Generate dataset insights

1.  In the Google Cloud console, go to **BigQuery Studio** .

2.  In the **Explorer** pane, select the project and then the dataset for which you want to generate insights.

3.  Click the **Insights** tab.

4.  Click **Generate** .
    
    If your dataset is in a multi-region, you might be prompted to select a region to generate insights. Select a region corresponding to the multi-region where the insights scan is going to be created.
    
    It takes a few minutes for the insights to be populated. The quality of insights improves if the tables in the dataset have [data profiling results](/bigquery/docs/data-profile-scan) .

After insights are generated, BigQuery displays a dataset description, a relationship graph, a relationship table, and sample cross-table queries.

### View and save the dataset description

Gemini generates a natural language description of the dataset, summarizing the types of tables it contains and the business domain it represents. To save this description to the metadata of the dataset, click **Save to details** .

You can edit the description before saving the details.

### Explore the relationship graph

The **Relationships** graph provides a visual representation of how tables in the dataset relate to each other. It displays the top 10 most connected tables as nodes, with lines representing relationships between them.

  - To see relationship details, such as the columns that join two tables, hover over the edge connecting the table nodes.
  - To rearrange the graph for better visibility, drag the table nodes.

### Use the relationship table

The **Relationship table** lists the discovered relationships in a tabular format. Each row represents a relationship between two tables, showing the source table and column, and the destination table and column. The **Source** column indicates how the relationship was determined:

  - **LLM inferred.** Relationships inferred by Gemini, based on table and column names and descriptions across the dataset.
  - **Usage based.** Relationships extracted from query logs, based on frequent joins.
  - **Schema-defined.** Relationships derived from existing primary key and foreign key mappings in the table schema.

You can filter the relationships for a specific table or provide feedback on the quality of detected relationships. To export the generated dataset description and relationships to a JSON file, click **Export to JSON** .

### Use query recommendations

Based on the discovered relationships, Gemini generates sample queries. These are natural language questions with corresponding SQL queries that join multiple tables in the dataset.

1.  To view a SQL query, click a question.

2.  To open the query in the BigQuery query editor, click **Copy to query** . You can then run the query or modify it.

3.  To ask a follow up question, click **Ask a follow-up** , which opens an untitled data canvas where you can chat with Gemini to explore your data.

## What's next

  - Learn about [data insights overview](/bigquery/docs/data-insights) .
  - Learn how to [generate table insights](/bigquery/docs/generate-table-insights) .
  - Learn more about [Dataplex Universal Catalog data profiling](/dataplex/docs/data-profiling-overview) .
