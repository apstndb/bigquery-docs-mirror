---
name: documents/docs.cloud.google.com/bigquery/docs/security-center-overview
uri: https://docs.cloud.google.com/bigquery/docs/security-center-overview
title: Security center overview
description: Overview of key data security and governance tasks in the BigQuery Security center, including security profile analysis, row-level and column-level security policy management, and tag configuration.
data_source: docs.cloud.google.com
---

# Security center overview

This document describes the BigQuery Security center in the Google Cloud console. You can use the Security center to analyze your organization's data security profiles, configure and manage row-level and column-level security policies, and manage data governance tags and policy tags.

## Before you begin

To view information in the Security center, you need the following:

Enable the Dataplex API, if it is not already enabled.

**Roles required to enable APIs**

To enable APIs, you need the `serviceusage.services.enable` permission. If you created the project, then you likely already have this permission through the Owner role ( `roles/owner` ). Otherwise, you can get this permission through the Service Usage Admin role ( `roles/serviceusage.serviceUsageAdmin` ). [Learn how to grant roles](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

### Required roles

To get the permissions that you need to manage and monitor security settings from the BigQuery **Security center** page, ask your administrator to grant you the following IAM roles:

- Browse and search resources on the **Resources** tab, and view data masking routines: [BigQuery Metadata Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.metadataViewer) ( `roles/bigquery.metadataViewer` ) on the project
- Manage row-level access policies, data policies (column-level security), and table and dataset security: [BigQuery Security Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin) ( `roles/bigquery.securityAdmin` ) on the project
- Attach policy tags to columns:
  - [BigQuery Data Owner](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner) ( `roles/bigquery.dataOwner` ) on the table
  - [BigQuery Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin) ( `roles/bigquery.admin` ) on the project
- Create and manage data policies without dataset ownership: [BigQuery Data Policy Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.admin) ( `roles/bigquerydatapolicy.admin` ) on the project
- Run query jobs and view security insights (including `INFORMATION_SCHEMA` views): [BigQuery Job User](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.jobUser) ( `roles/bigquery.jobUser` ) on the project
- Manage data governance tags: [Tag Administrator](https://docs.cloud.google.com/iam/docs/roles-permissions/resourcemanager#resourcemanager.tagAdmin) ( `roles/resourcemanager.tagAdmin` ) on the organization
- Create and manage policy tag taxonomies: [Policy Tag Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/datacatalog#datacatalog.categoryAdmin) ( `roles/datacatalog.categoryAdmin` ) on the taxonomy or organization
- Query columns protected by policy tags: [Fine-Grained Reader](https://docs.cloud.google.com/iam/docs/roles-permissions/datacatalog#datacatalog.categoryFineGrainedReader) ( `roles/datacatalog.categoryFineGrainedReader` ) on the taxonomy or policy tag
- Use Gemini Cloud Assist in the Security center: [Gemini for Google Cloud User](https://docs.cloud.google.com/iam/docs/roles-permissions/cloudaicompanion#cloudaicompanion.user) ( `roles/cloudaicompanion.user` ) on the project

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Resource selection and security profile analysis

The **Resources** tab in the Security center lets you search for datasets and tables within a BigQuery project, view attached security policies, and analyze the security profile of each resource.

### Analyze a security profile with Gemini Cloud Assist

Gemini Cloud Assist in the Security center lets you review security settings, ask questions about your resources, and analyze the security profile of a dataset or table:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the navigation menu, click **Governance** , and then click **Security center** .

3.  Click the **Resources** tab.

4.  Hold the pointer over a dataset or table, and then click astrophotography_mode **Show security profile** .

Gemini Cloud Assist generates a summary of the resource's security profile, including attached row-level access policies, column-level data policies, and classification tags.

To ask questions about security findings, policies, and access controls, you can also use the Gemini Cloud Assist chat panel.

For more information, see [Use Gemini Cloud Assist](https://docs.cloud.google.com/bigquery/docs/use-cloud-assist) .

### Search and filter resources

The **Resources** tab provides the following capabilities for locating resources and inspecting access controls:

- **Project scope:** the **Resources** tab displays datasets and tables in the selected Google Cloud project.
- **Search and filter:** click **Filter** to search for resources by dataset name, table name, or location.
- **Inspect attached policies:** the **Policies** and **Policy tags** columns show whether access policies or tags are attached to each table. To view policy details, click the resource name. To create or modify policies for a selected resource, go to the **Policy management** tab.

## Policy management

The **Policy management** tab in the Security center lets you configure and manage row-level access policies and column-level security policies for your tables.

You can configure column-level security policies in three ways:

- Directly assigned data policies on columns
- Data governance tag-based policies ( [Preview](https://cloud.google.com/products#product-launch-stages) )
- Policy tag-based policies

### Row access policies

The **Row access** view displays all row-level access policies created for your resources. For each policy, you can view the policy name, table name, dataset name, and last modified date. You can edit, delete, or create policies directly from this view.

When creating a row-level access policy, you specify the following:

- **Policy name:** a unique name for the policy.
- **Table search:** enter the table name in the search field to locate and select the target table.
- **Schema view:** review the table schema to verify available column names.
- **Filter predicate:** enter a SQL filter condition that defines which rows are visible (for example, `region = 'us-east1'` ).
- **Principals:** specify the users, groups, or domains to which the policy applies.

For more information, see [Introduction to BigQuery row-level security](https://docs.cloud.google.com/bigquery/docs/row-level-security-intro) .

### Column security policies

The **Column security** view lets you manage column-level access control and data masking across your resources.

To view column security policies, you must first select a region from the **Region** list.

After you select a region, policies appear in three sections based on how they were created:

- **Policy tags:** policies tied to Data Catalog taxonomy tags.
- **Data governance tags:** policies tied to Resource Manager tags with `purpose=DATA_GOVERNANCE` ( [Preview](https://cloud.google.com/products#product-launch-stages) ).
- **Directly assigned data policies:** data policies attached directly to table columns without tag intermediaries.

#### Policy impact metrics

For each policy, the table displays impact metrics showing the number of tables and columns affected by that policy. These metrics indicate how widely a policy is applied across your datasets, helping administrators evaluate the reach and sensitivity of a policy before updating or reassigning it.

#### Attach policies to multiple columns

To attach an existing policy to multiple columns across different tables and datasets, in the policy table, click **Attach** . This lets you apply consistent column-level access controls or data masking rules across your organization in a single action.

When you assign principals to a data policy, BigQuery grants them the Masked Reader role ( `roles/bigquerydatapolicy.maskedReader` ) on that policy. This role is the only predefined role that grants `bigquery.dataPolicies.maskedGet` , the permission required to read masked values in the protected columns. For more information, see [Roles for querying masked data](https://docs.cloud.google.com/bigquery/docs/column-data-masking-intro#roles_for_querying_masked_data) .

Depending on your access control requirements, see one of the following guides for detailed instructions about configuring policies:

- **Filter rows by user identity:** to restrict which rows users can query based on attributes such as department or region, see [Introduction to BigQuery row-level security](https://docs.cloud.google.com/bigquery/docs/row-level-security-intro) .
- **Block access to specific columns:** to prevent unauthorized users from querying sensitive columns entirely, see [Restrict access with column-level access control](https://docs.cloud.google.com/bigquery/docs/column-level-security) .
- **Obscure column values during queries:** to let users query tables while masking sensitive data (such as email addresses), see [Mask column data](https://docs.cloud.google.com/bigquery/docs/column-data-masking) .

## Data governance tags and policy tags

Data governance tags and policy tags let you classify columns and apply access controls across BigQuery resources.

To manage tags in the Security center:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the navigation menu, click **Governance** , and then click **Security center** .

3.  Depending on the type of tag you want to manage, select one of the following tabs:

    - **Data governance tags:** click the **Data governance tags** tab to create Resource Manager tag keys (with `purpose=DATA_GOVERNANCE` ) and define hierarchical tag values ( [Preview](https://cloud.google.com/products#product-launch-stages) ). To configure access permissions, click **Manage access** .
    - **Policy tags:** click the **Policy tags** tab, and then click **Create taxonomy** to create Data Catalog taxonomies and hierarchical policy tags. To configure access permissions, use the permissions panel.

After you create tag keys or taxonomies, you attach the tags to table columns to enforce column-level access control and data masking:

- **Data governance tags:** to attach data governance tags to columns and apply data policies using Resource Manager, see [Control access to columns with data governance tags](https://docs.cloud.google.com/bigquery/docs/tags#data-governance-tags) .
- **Data Catalog policy tags:** to associate taxonomy policy tags with table schemas and manage access control, see [Set up column-level access control](https://docs.cloud.google.com/bigquery/docs/column-level-security#set_up_column-level_access_control) .

## What's next

- Learn more about [data governance in BigQuery](https://docs.cloud.google.com/bigquery/docs/data-governance) .
- Learn how to [restrict access with row-level security](https://docs.cloud.google.com/bigquery/docs/row-level-security-intro) .
- Learn how to [restrict access with column-level access control](https://docs.cloud.google.com/bigquery/docs/column-level-security) .
- Learn how to [mask column data with policy tags](https://docs.cloud.google.com/bigquery/docs/column-data-masking) .
- Learn how to [control column access with data governance tags](https://docs.cloud.google.com/bigquery/docs/tags#data-governance-tags) .
