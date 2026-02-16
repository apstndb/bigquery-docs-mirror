# Introduction to BigQuery row-level security

**Note:** This feature may not be available when using reservations that are created with certain BigQuery editions. For more information about which features are enabled in each edition, see [Introduction to BigQuery editions](/bigquery/docs/editions-intro) .

This document explains the concept of row-level security, how it works in BigQuery, when to use row-level security to secure your data, and other details.

## What is row-level security?

Row-level security lets you filter data and enables access to specific rows in a table based on qualifying user conditions.

BigQuery supports access controls at the project, dataset, and table levels, as well as [column-level security](/bigquery/docs/column-level-security-intro) through policy tags. Row-level security extends the principle of least privilege by enabling fine-grained access control to a subset of data in a BigQuery table, by means of row-level access policies.

One table can have multiple row-level access policies. Row-level access policies can [coexist on a table](/bigquery/docs/using-row-level-security-with-features#example_of_row-level_security_and_column-level_security_interacting) with [column-level security](/bigquery/docs/column-level-security-intro) as well as [dataset-level](/bigquery/docs/control-access-to-resources-iam#grant_access_to_a_dataset) , [table-level](/bigquery/docs/control-access-to-resources-iam#grant_access_to_a_table_or_view) , and [project-level](/bigquery/docs/access-control) access controls.

## How row-level security works

At a high level, row-level security involves the creation of row-level access policies on a target BigQuery table. These policies act as filters to hide or display certain rows of data, depending on whether a user or group is in an allowed list. Any users or groups not specifically included in the allowed list are denied access.

**Note:** If you create a new row-level security policy to limit row access, users that previously had full access must be added to a [`  TRUE  ` filter](/bigquery/docs/using-row-level-security-with-features#the_true_filter) to maintain their access.

An authorized user, with the Identity and Access Management (IAM) roles [BigQuery Admin or BigQuery DataOwner](/bigquery/docs/access-control#bigquery) , can create row-level access policies on a BigQuery table.

When you create a row-level access policy, you specify the table by name, and which users or groups (called the `  grantee-list  ` ) can access certain row data. The policy also includes the data on which you want to filter, called the `  filter_expression  ` . The `  filter_expression  ` functions like a `  WHERE  ` clause in a typical query.

**Remember:** Like a `  WHERE  ` clause, the `  filter_expression  ` matches the data that you want to be visible to the principals in the `  grantee_list  ` . The users that are not in the `  grantee_list  ` cannot see any rows.

For instructions on how to create and use a row-level access policy, see [Managing row-level security](/bigquery/docs/managing-row-level-security) .

See the [DDL reference](/bigquery/docs/reference/standard-sql/data-definition-language#create_row_access_policy_statement) for the complete syntax, usage, and options when creating row-level access policies.

### Example use cases

The following examples demonstrate potential use cases for row-level security.

**Note:** When managing access for users in [external identity providers](/iam/docs/workforce-identity-federation) , replace instances of Google Account principal identifiers—like `  user:kiran@example.com  ` , `  group:support@example.com  ` , and `  domain:example.com  ` —with appropriate [Workforce Identity Federation principal identifiers](/iam/docs/principal-identifiers) .

#### Filter row data based on region

Consider the case where the table `  dataset1.table1  ` contains rows belonging to different regions (denoted by the `  region  ` column).

You can create and populate the example table by using the following query:

``` text
CREATE TABLE IF NOT EXISTS
  dataset1.table1 (partner STRING,
    contact STRING,
    country STRING,
    region STRING);
INSERT INTO
  dataset1.table1 (partner,
    contact,
    country,
    region)
VALUES
  ('Example Customers Corp', 'alice@examplecustomers.com', 'Japan', 'APAC'),
  ('Example Enterprise Group', 'bob@exampleenterprisegroup.com', 'Singapore', 'APAC'),
  ('Example HighTouch Co.', 'carrie@examplehightouch.com', 'USA', 'US'),
  ('Example Buyers Inc.', 'david@examplebuyersinc.com', 'USA', 'US');
```

Row-level security lets a data owner or administrator implement policies. The following statement implements a policy that restricts users in the APAC mailing group to see only partners from the APAC region:

``` text
CREATE ROW ACCESS POLICY
  apac_filter
ON
  dataset1.table1 GRANT TO ("group:sales-apac@example.com")
FILTER USING
  (region="APAC" );
```

The resulting behavior is that users in the `  sales-apac@example.com  ` group can view only rows where the value for `  region  ` is `  APAC  ` .

The following statement implements a policy that restricts both individuals and groups to see only partners from the US region:

``` text
CREATE ROW ACCESS POLICY
  us_filter
ON
  dataset1.table1 GRANT TO ("group:sales-us@example.com",
"user:jon@example.com")
FILTER USING
  (region="US");
```

The resulting behavior is that users in the group `  sales-us@example.com  ` and the user `  jon@example.com  ` can view only rows where the value for `  region  ` is `  US  ` .

The following image shows how the previous two access policies restrict which users and groups can view which rows in the table:

Users that aren't in the `  APAC  ` or `  US  ` groups don't see any rows.

#### Filter row data based on sensitive data

Now, consider a different use case, where you have a table that contains salary information.

You can create and populate the example table by using the following query:

``` text
CREATE OR REPLACE TABLE
  dataset1.table1 (name STRING,
    department STRING,
    salary INT64,
    email STRING);
INSERT INTO
  dataset1.table1 ( name,
    department,
    salary,
    email)
VALUES
  ('Jim D', 'HR', 100000, 'jim@example.com'),
  ('Anna K', 'Finance', 100000, 'anna@example.com'),
  ('Bruce L', 'Engineering', 100000, 'bruce@example.com'),
  ('Carrie F', 'Business', 100000, 'carrie@example.com');
```

The row access policy in the following statement restricts querying to members of the company domain. In addition, the use of the `  SESSION_USER()  ` function restricts access only to rows that belong to the user running the query, based on their user email address.

``` text
CREATE ROW ACCESS POLICY
  salary_personal
ON
  dataset1.table1 GRANT TO ("domain:example.com")
  FILTER USING
  (Email=SESSION_USER());
```

The following image demonstrates how the row access policy restricts the table containing salary information. In this example, the user is named Jim, with the email address `  jim@example.com  ` .

For additional row-level security examples, see [Use row-level security](/bigquery/docs/managing-row-level-security) .

#### Filter row data based on lookup table

With subquery support, row access policies can reference other tables and use them as lookup tables. Data used in filtering rules can be stored in a table and a single subquery row access policy can replace multiple configured row access policies. To update the row access policies, you only need to update the lookup table, which replaces multiple row access policies. You don't need to update each individual row access policy.

For examples of filtering row data, see [Use row-level security](/bigquery/docs/managing-row-level-security) .

## When to use row-level security versus other methods

[Authorized views](/bigquery/docs/authorized-views) , row-level access policies, and storing data in separate tables all provide different levels of security, performance, and convenience. Choosing the right mechanism for your use case is important to ensure the proper level of security for your data.

### Comparison with authorized views: vulnerabilities

Both row-level security and [enforcing row-level access with an authorized view](/bigquery/docs/authorized-views#combine_row-level_security_with_authorized_views) can have vulnerabilities, if used improperly.

*When you use either authorized views or row-level access policies for row-level security, we recommend that you monitor for any suspicious activity using [audit logging](#audit_logging_and_monitoring) .*

Side channels, such as the query duration, can leak information about rows that are at the edge of a storage shard. Such attacks would likely require either some knowledge of how the table is sharded, or a large number of queries.

For more information about preventing such side-channel attacks, see [Best practices for row-level security](/bigquery/docs/best-practices-row-level-security#limit-side-channel-attacks) .

### Comparison of authorized views, row-level security, and separate tables

The following table compares the flexibility, performance, and security of authorized views, row-level access policies, and separate tables.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Method</strong></th>
<th><strong>Security considerations</strong></th>
<th><strong>Recommendation</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Authorized</strong><br />
<strong>views</strong></td>
<td>Recommended for flexibility. Can be vulnerable to carefully crafted queries, query durations, and other types of side-channel attacks.</td>
<td>Authorized views are a good choice when you need to share data with others and flexibility and performance are important. For example, you can use authorized views to share data within your work group.</td>
</tr>
<tr class="even">
<td><strong>Row-level access policies</strong></td>
<td>Recommended for a balance of flexibility and security. Can be vulnerable to <a href="/bigquery/docs/best-practices-row-level-security#limit-side-channel-attacks">query duration side-channel attacks</a> .</td>
<td>Row-level access policies are a good choice when you need to share data with others and you want to provide additional security over views or table slices. For example, you can use row-level access policies to share data with people who all use the same dashboard, even if some people have access to more data than others.</td>
</tr>
<tr class="odd">
<td><strong>Separate tables</strong></td>
<td>Recommended for security. Users cannot infer data without access to the table.</td>
<td>Separate tables are a good choice when you need to share data with others and you need to keep data isolated. For example, you can use separate tables to share data with third-party partners and vendors, when the total number of rows must be secret.</td>
</tr>
</tbody>
</table>

## Create and manage row-level access policies

For information about how to create, update (re-create), list, view, and delete row-level access policies on a table, and how to query tables with row-level access policies, see [Working with row-level access security](/bigquery/docs/managing-row-level-security) .

## Implicit deletion of row-level access policies

Row access policies can be implicitly (automatically) removed from a table under several conditions.

The general principle for automatically deleting row access policies are:

  - Operations using a [`  WRITE_TRUNCATE  ` write disposition](/bigquery/docs/reference/rest/v2/Job#JobConfigurationLoad.FIELDS.write_disposition) always overwrite any existing row access policies on the destination table.
  - For operations with a `  WRITE_APPEND  ` write disposition, the destination table's current row access policies are preserved, and the source table's policies are added to the destination table.

Specifically, row access policies are implicitly removed in the following situations:

  - Replacing a table: when a table is replaced using the [`  CREATE OR REPLACE TABLE  `](/bigquery/docs/reference/standard-sql/data-definition-language#create_table_statement) DDL statement, all existing row access policies on the original table are dropped. This occurs even if the replacement query is based on the original table's data.

  - Loading or querying with `  WRITE_TRUNCATE  ` : operations that use the `  WRITE_TRUNCATE  ` write disposition remove all existing row access policies. This includes loading data using the [`  bq load --replace  `](/bigquery/docs/reference/bq-cli-reference#bq_load) command and running a query with the status of `  writeDisposition  ` set to `  WRITE_TRUNCATE  ` . Such operations completely overwrite the table, and row access policies aren't carried over.

  - Table deletion or expiration: if a table is explicitly deleted or if it reaches its expiration time and is automatically removed, all associated row access policies are also deleted.

  - Table copy operations: when copying a table without row access policies to a destination table that has row access policies, the policies on the destination table are removed, unless the [`  --append_table  `](/bigquery/docs/reference/bq-cli-reference#bq_cp) flag or `  "writeDisposition": "WRITE_APPEND"  ` is used. See [Using row-level security with other BigQuery features](/bigquery/docs/using-row-level-security-with-features#features_that_work_with_the_true_filter) for more information on table copy jobs.

Using the [`  TRUNCATE TABLE  `](/bigquery/docs/reference/standard-sql/dml-syntax#truncate_table_statement) DML statement, which removes all rows from a table while maintaining its schema, doesn't remove row access policies.

## Quotas

For more information about quotas and limits for row-level security, see BigQuery [Quotas and limits](/bigquery/quotas#row-level_security) .

## Pricing

Row-level security is included with BigQuery at no additional cost. However, a row-level access policy can affect the cost of running a query in the following ways:

  - Additional billing can be caused by row-level access policies, specifically policies that include subqueries that reference other tables.

  - Row-level access policy filters don't participate in query pruning on [partitioned and clustered tables](/bigquery/docs/using-row-level-security-with-features#partitioned_and_clustered_tables) . This does not mean it reads more data during the main query execution. It doesn't take advantage of row access policy predicates to prune any further.

  - With row-level access policy filters, not all user filters are applied early. This might increase the data read from tables and might read and bill for more rows.

For more information about BigQuery query pricing, see [BigQuery pricing](https://cloud.google.com/bigquery/pricing) .

## Limitations

For information about limits for row-level security, see BigQuery [Row-level security limits](/bigquery/quotas#row-level_security) . The following sections document additional row-level security limitations.

### Performance limitations

  - Some BigQuery features aren't accelerated when working with tables containing row-level access policies, such as [BigQuery BI Engine](/bigquery/docs/using-row-level-security-with-features#bi-engine) and [materialized views](/bigquery/docs/using-row-level-security-with-features#logical_materialized_and_authorized_views) .

  - Row-level security does not participate in query [pruning](/bigquery/docs/querying-partitioned-tables#overview) , which is a feature of [partitioned tables](/bigquery/docs/partitioned-tables) . For more information, see [Partitioned and clustered tables](/bigquery/docs/using-row-level-security-with-features#partitioned_and_clustered_tables) . This limitation doesn't slow down the main query execution.

  - You might experience a small performance degradation when you query tables with row-level security.

For more information about how row-level security interacts with some BigQuery features and services, see [Using row-level security with other BigQuery features](/bigquery/docs/using-row-level-security-with-features) .

### Other limitations

  - This feature may not be available when using reservations that are created with certain BigQuery editions. For more information about which features are enabled in each edition, see [Introduction to BigQuery editions](/bigquery/docs/editions-intro) .

  - Row access policies are not compatible with Legacy SQL. Queries of tables with row-level access policies must use GoogleSQL. Legacy SQL queries are rejected with an error.

  - You cannot apply row-level access policies on [JSON columns](/bigquery/docs/json-data) .

  - Wildcard table queries are not supported over tables with row access policies.

  - Row access policies cannot be applied to temporary tables.

  - You cannot apply row-level access policies to tables that reference other tables that have row-level security.

  - Some features of BigQuery are not compatible with row-level security. For more information, see [Using row-level security](/bigquery/docs/using-row-level-security-with-features) .
    
      - Row access policies that incorporate [subqueries](#filter_row_data_based_on_lookup_table) aren't compatible with the [BigQuery Storage Read API](/bigquery/docs/reference/storage) . The BigQuery Storage Read API only supports simple filter predicates.

  - Non-query operations, including service account jobs, that need full access to table data can use row-level security with the [`  TRUE  ` filter](/bigquery/docs/using-row-level-security-with-features#the_true_filter) . Examples include [table copying](/bigquery/docs/using-row-level-security-with-features#features_that_work_with_the_true_filter) , [dataproc workflows](/bigquery/docs/using-row-level-security-with-features#tabledata-list) , and more. For more information, see [Using row-level security](/bigquery/docs/using-row-level-security-with-features) .

  - You can create, replace, or delete row-level access policies with DDL statements or [row access policy APIs](/bigquery/docs/reference/rest#rest-resource:-v2.rowaccesspolicies) . You can also perform all available actions in the row access policy APIs in the [bq command-line tool](/bigquery/docs/bq-command-line-tool) . You can list and view row-level access policies in the Google Cloud console.

  - [Previewing or browsing tables](/bigquery/docs/managing-table-data#browse-table) is incompatible with row-level security.

  - [Table sampling](/bigquery/docs/table-sampling) is not compatible with row-level security.

  - Top-level subquery policy results are limited to 100 MB. This limit applies per row-level access policy.

  - Top-level [`  IN  ` subqueries](/bigquery/docs/reference/standard-sql/subqueries#in_subquery_concepts) where the type of `  search_value  ` is `  FLOAT  ` , `  STRUCT  ` , `  ARRAY  ` , `  JSON  ` or `  GEOGRAPHY  ` aren't available in row access policies.

  - If the row-level access policy predicate cannot be evaluated due to the deletion of any referenced table, the query fails.

  - Subquery row-level access policies only support BigQuery tables, BigLake external tables, and BigLake managed tables.

  - Column [renaming](/bigquery/docs/managing-table-schemas#change_a_columns_name) and [dropping](/bigquery/docs/managing-table-schemas#delete_a_column) statements that modify table schema and could impact row access policies aren't permitted.

  - [Data masking](/bigquery/docs/column-data-masking) is only compatible with queries that have non-subquery row access policies. Data masking is applied on top of row-level security. For example, if there is a row access policy applied on `  location = "US"  ` and `  location  ` is masked, then users are able to see rows where `  location = "US"  ` but the location field is masked in the results. Queries involving a subquery row access policy will require Fine-Grained Reader access on columns referenced by row access policies.

## Audit logging and monitoring

When data in a table with one or more row-level access policies is read, the row-level access policies authorized for the read access and any corresponding tables referenced in subqueries appear in the IAM authorization information for that read request.

Creation and deletion of row-level access policies are audit logged, and can be accessed through [Cloud Logging](/logging/docs/overview) . Audit logs include the name of the row-level access policy. However, the `  filter_expression  ` and `  grantee_list  ` definitions of a row-level access policy are omitted from logs, as they may contain user or other sensitive information. Listing and viewing of row-level access policies are not audit logged.

For more information about logging in BigQuery, see [Introduction to BigQuery monitoring](/bigquery/docs/monitoring) .

For more information about logging in Google Cloud, see [Cloud Logging](/logging/docs) .

## What's next

  - For information about managing row-level security, see [Use row-level security](/bigquery/docs/managing-row-level-security) .

  - For information about how row-level security works with other BigQuery features and services, see [Using row-level security with other BigQuery features](/bigquery/docs/using-row-level-security-with-features) .

  - For information about best practices for row-level security, see [Best Practices for row-level security in BigQuery](/bigquery/docs/best-practices-row-level-security) .
