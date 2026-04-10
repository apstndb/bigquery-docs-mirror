# Work with Data Catalog

**Caution:** Data Catalog is [deprecated](https://docs.cloud.google.com/data-catalog/docs/deprecations) in favor of [Dataplex Universal Catalog](https://docs.cloud.google.com/dataplex/docs/catalog-overview) , which offers intelligent governance for data and AI assets across Google Cloud. Key Dataplex Universal Catalog capabilities are integrated with BigQuery and are also available in the BigQuery experience. See [Manage aspects and enrich metadata](https://docs.cloud.google.com/dataplex/docs/enrich-entries-metadata) for details on enriching your data with aspects, which are the equivalent of Data Catalog tags.

Data Catalog integrates with BigQuery by automatically cataloging metadata about BigQuery resources like tables, datasets, views, and models. This document describes how to search these resources, view data lineage, and add tags by using Data Catalog.

## Search for BigQuery resources

To use Data Catalog to search for BigQuery datasets, tables, and starred projects, follow these steps:

1.  In the Google Cloud console, go to the Data Catalog **Search** page.
    
    [Go to Search](https://console.cloud.google.com/dataplex)

2.  In the **Search** field, enter a query, and then click **Search** .
    
    ![Data Catalog search lets you find data across your projects and organizations.](https://docs.cloud.google.com/static/bigquery/images/data-catalog-search.png)
    
    To refine your search parameters, use the **Filters** panel. For example, in the **Systems** section, select the **BigQuery** checkbox. The results are filtered to BigQuery systems.

You can perform basic searches in Data Catalog through the Google Cloud console. For more information about searching in the Google Cloud console, see [Open a public dataset](https://docs.cloud.google.com/bigquery/docs/quickstarts/query-public-dataset-console#open_a_public_dataset) .

## Data lineage

[Data lineage](https://docs.cloud.google.com/dataplex/docs/about-data-lineage) is a Dataplex Universal Catalog feature that lets you track how data moves through your systems: where it comes from, where it is passed to, and what transformations are applied to it. You can access the data lineage feature directly from BigQuery.

Enabling data lineage in your BigQuery project causes Dataplex Universal Catalog to automatically record lineage information for tables created by the following operations:

  - [Copy jobs](https://docs.cloud.google.com/bigquery/docs/managing-tables#copy-table) .

  - [Query jobs](https://docs.cloud.google.com/bigquery/docs/running-queries) that use the following data definition language (DDL) or data manipulation language (DML) statements in GoogleSQL:
    
      - [`  CREATE TABLE  `](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_table_statement) (including the `  CREATE TABLE AS SELECT  ` statement)
      - [`  INSERT  `](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/dml-syntax#insert_statement)
      - [`  UPDATE  `](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/dml-syntax#update_statement)
      - [`  DELETE  `](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/dml-syntax#delete_statement)
      - [`  MERGE  `](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/dml-syntax#merge_statement)

### Before you begin

In this section, you enable the Data Lineage API and grant [Identity and Access Management (IAM)](https://docs.cloud.google.com/iam/docs) roles that give users the necessary permissions to perform each task in this document.

#### Enable data lineage

1.  In the Google Cloud console, on the project selector page, select the project that contains the resources for which you want to track lineage.
    
    [Go to project selector](https://console.cloud.google.com/projectselector2/home/dashboard)

2.  Enable the Data Lineage API and Dataplex API.
    
    [Enable the APIs](https://console.cloud.google.com/apis/enableflow?apiid=datalineage.googleapis.com,dataplex.googleapis.com)

**Note:** Enabling the Data Lineage API may incur additional costs. For more information, see [Data lineage considerations](https://docs.cloud.google.com/dataplex/docs/lineage-considerations) .

#### Required IAM roles

Lineage information is tracked automatically when you enable the Data Lineage API.

To get the permissions that you need to view lineage graphs, ask your administrator to grant you the following IAM roles:

  - [Data Catalog Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/datacatalog#datacatalog.viewer) ( `  roles/datacatalog.viewer  ` ) on a Data Catalog resource project.
  - [Data lineage viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/datalineage#datalineage.viewer) ( `  roles/datalineage.viewer  ` ) on the project where you use systems supported by data lineage.
  - [BigQuery Metadata](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.metadataViewer) ( `  roles/bigquery.metadataViewer  ` )

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

For more information, see [Data lineage roles](https://docs.cloud.google.com/dataplex/docs/iam-roles#lineage-roles) .

### View lineage graphs in BigQuery

To view the data lineage graph from BigQuery follow these steps:

1.  In the Google Cloud console, go to the **BigQuery** page.
    
    [Go to BigQuery](https://console.cloud.google.com/bigquery)

2.  In the left pane, click explore **Explorer** :
    
    ![Highlighted button for the Explorer pane.](https://docs.cloud.google.com/static/bigquery/images/explorer-tab.png)
    
    If you don't see the left pane, click last\_page **Expand left pane** to open the pane.

3.  In the **Explorer** pane, expand your project and then click **Datasets** .

4.  Click **Overview \> Tables** , and then select a table.

5.  Click the **Lineage** tab.
    
    ![Data lineage tab.](https://docs.cloud.google.com/static/bigquery/images/data-lineage-tab.png)
    
    Your data lineage graph is displayed.
    
    ![Data lineage graph.](https://docs.cloud.google.com/static/bigquery/images/sample-lineage-graph.png)

6.  Optional: Select a node to view additional details about the entities or processes involved in constructing lineage information.

For more information about data lineage, see [About data lineage](https://docs.cloud.google.com/dataplex/docs/about-data-lineage) .

## Tags and tag templates

Tags let organizations create, search, and manage metadata for all their data entries in a unified service.

This section explains two key Data Catalog concepts:

  - *Tags* let you provide context for a data entry by attaching custom metadata fields.

  - *Tag templates* are reusable structures that you can use to rapidly create new tags.

### Tags

Data Catalog provides two types of tags: private tags and public tags.

#### Private tags

Private tags provide strict access controls. You can search or view the tags and the data entries associated with the tags only if you are granted the [required view permissions](https://docs.cloud.google.com/data-catalog/docs/concepts/iam#roles_to_view_public_and_private_tags) on both the private tag template and the data entries.

Searching for private tags in the Data Catalog page requires that you use the `  tag:  ` search syntax or the search filters.

Private tags are suitable for scenarios where you need to store some sensitive information in the tag and you want to apply additional access restrictions beyond checking whether the user has the permissions to view the tagged entry.

#### Public tags

Public tags provide less strict access control for searching and viewing the tag as compared to private tags. Any user who has the required view permissions for a data entry can view all the public tags associated with it. View permissions for public tags are only required when you perform a search in Data Catalog using the `  tag:  ` syntax or when you view an unattached tag template.

Public tags support both simple search and search with predicates in the Data Catalog search page. When you create a tag template, the option to create a public tag template is the default and recommended option in the Google Cloud console.

For example, let's assume you have a public tag template called `  employee data  ` that you used to create tags for three data entries called `  Name  ` , `  Location  ` , and `  Salary  ` . Among the three data entries, only members of a specific group called `  HR  ` can view the `  Salary  ` data entry. The other two data entries have view permissions for all employees of the company.

If any employee who is not a member of the `  HR  ` group uses the Data Catalog search page and searches with the word `  employee  ` , the search result displays only `  Name  ` and `  Location  ` data entries with the associated public tags.

Public tags are useful for a broad set of scenarios. Public tags support simple search and search with predicates, while private tags support only search with predicates.

### Tag templates

To start tagging metadata, you first need to create one or more tag templates. A tag template can be a public or private tag template. When you create a tag template, the option to create a public tag template is the default and recommended option in the Google Cloud console. A tag template is a group of metadata key-value pairs called *fields* . Having a set of templates is similar to having a database schema for your metadata.

You can structure your tags by topic. For example:

  - A `  data governance  ` tag with fields for data governor, retention date, deletion date, PII (yes or no), data classification (public, confidential, sensitive, regulatory)
  - A `  data quality  ` tag with fields for quality issues, update frequency, SLO information
  - A `  data usage  ` tag with fields for top users, top queries, average daily users

You can then mix and match tags, using only the tags relevant for each data asset and your business needs.

#### View the tag template gallery

To help you get started, Data Catalog includes a gallery of sample tag templates to illustrate common tagging use cases. Use these examples to learn about the power of tagging, for inspiration, or as a starting point for creating your own tagging infrastructure.

To use a tag template gallery, perform the following steps:

1.  In the Google Cloud console, go to the Dataplex Universal Catalog **Tag templates** page.
    
    [Go to Tag templates](https://console.cloud.google.com/dataplex/templates)

2.  Click **Create tag template** .
    
    The template gallery is displayed as part of the **Create template** page.

After you select a template from the gallery, you can use it just like any other tag template. You can add or delete attributes and change anything in the template to suit your business needs. You can then search for the template fields and values using Data Catalog.

For more information about tags and tag templates, see [Tags and tag templates](https://docs.cloud.google.com/data-catalog/docs/tags-and-tag-templates) .

### Regional resources

Every tag template and tag is stored in a particular [Google Cloud region](https://docs.cloud.google.com/bigquery/docs/locations) . You can use a tag template to create a tag in any region, so you don't need to create copies of your template if you have metadata entries spread across multiple regions.
