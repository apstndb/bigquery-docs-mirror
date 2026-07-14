---
name: documents/docs.cloud.google.com/bigquery/docs/postgresql-transfer-intro
uri: https://docs.cloud.google.com/bigquery/docs/postgresql-transfer-intro
title: Introduction to PostgreSQL data transfers
description: Provides an overview of configuration options, data type mappings, and pricing for PostgreSQL data transfers.
data_source: docs.cloud.google.com
---

# Introduction to PostgreSQL data transfers

You can load data from PostgreSQL to BigQuery by using the [BigQuery Data Transfer Service](https://docs.cloud.google.com/bigquery/docs/dts-introduction) for PostgreSQL connector. The connector supports PostgreSQL instances hosted in your on-premises environment, Cloud SQL, and other public cloud providers such as Amazon Web Services (AWS) and Microsoft Azure. This document provides an overview of the data ingestion options for your PostgreSQL transfer and information about data type mapping and pricing.

To learn how to schedule a PostgreSQL transfer, see [Load PostgreSQL data into BigQuery](https://docs.cloud.google.com/bigquery/docs/postgresql-transfer) .

## Data ingestion options

The following sections provide information about the data ingestion options when you set up a PostgreSQL data transfer.

### TLS configuration

The PostgreSQL connector supports the configuration for transport level security (TLS) to encrypt your data transfers into BigQuery. The PostgreSQL connector supports the following TLS configurations:

  - The *Encrypt data, and verify CA and hostname* mode. This mode performs a full validation of the server using TLS over the TCPS protocol. It encrypts all data in transit and verifies that the database server's certificate is signed by a trusted certificate authority (CA). This mode also checks that the hostname you're connecting to exactly matches the Common Name (CN) or a Subject Alternative Name (SAN) on the server's certificate. This mode prevents attackers from using a valid certificate for a different domain to impersonate your database server.
    
    If your hostname does not match the certificate CN or SAN, the connection fails. You must configure a DNS resolution to match the certificate or use a different security mode. Use this mode for the most secure option to prevent person-in-the-middle (PITM) attacks.

  - The *Encrypt data, and verify CA only* mode. This mode encrypts all data using TLS over the TCPS protocol and verifies that the server's certificate is signed by a CA that the client trusts. However, this mode does not verify the server's hostname. This mode successfully connects as long as the certificate is valid and issued by a trusted CA, regardless of whether the hostname in the certificate matches the hostname you are connecting to.
    
    Use this mode if you want to ensure that you are connecting to a server whose certificate is signed by a trusted CA, but the hostname is not verifiable or you don't have control over the hostname configuration.

  - The *Encryption only* mode. This mode encrypts all data transferred between the client and the server. It does not perform any certificate or hostname validation.
    
    This mode provides some level of security by protecting data in transit, but it can be vulnerable to PITM attacks.
    
    Use this mode if you need to ensure all data is encrypted but can't or don't want to verify the server's identity. We recommend using this mode when working with private VPCs.

  - The *No encryption or verification* mode. This mode does not encrypt any data and does not perform any certificate or hostname verification. All data is sent as plain text.
    
    We don't recommend using this mode in an environment where sensitive data is handled. We only recommend using this mode for testing purposes on an isolated network where security is not a concern.

#### Trusted Server Certificate (PEM)

If you are using either the *Encrypt data, and verify CA and hostname* mode or the *Encrypt data, and verify CA* mode, then you can also provide one or more PEM-encoded certificates. These certificates are required in some scenarios where the BigQuery Data Transfer Service needs to verify the identity of your database server during the TLS connection:

  - If you are using a certificate signed by a private CA within your organization or a self-signed certificate, you must provide the full certificate chain or the single self-signed certificate. This is required for certificates issued by internal CAs of managed cloud provider services, such as the Amazon Relational Database Service (RDS).
  - If your database server certificate is signed by a public CA (for example, Let's Encrypt, DigiCert, or GlobalSign), you don't need to provide a certificate. The root certificates for these public CAs are pre-installed and trusted by the BigQuery Data Transfer Service.

You can specify PEM-encoded certificates in the **Trusted PEM Certificate** field in the transfer configuration, with the following requirements:

  - The certificate must be a valid PEM-encoded certificate chain.
  - The certificate must be entirely correct. Any missing certificates in the chain or incorrect content causes the TLS connection to fail.
  - For a single certificate, you can provide a single, self-signed certificate from the database server.
  - For a full certificate chain issued by a private CA, you must provide the full chain of trust. This includes the certificate from the database server and any intermediate and root CA certificates.

### Full or incremental transfers

You can specify how data is loaded into BigQuery by selecting either the *Full* or *Incremental* write preference in the transfer configuration when you [set up a PostgreSQL transfer](https://docs.cloud.google.com/bigquery/docs/postgresql-transfer#set-up) . Incremental transfers are supported in [Preview](https://cloud.google.com/products#product-launch-stages) .

> **Note:** To request feedback or support for incremental transfers, send an email to <dts-preview-support@google.com> .

You can configure a *full* data transfer to transfer all data from your PostgreSQL datasets with each data transfer.

Alternatively, you can configure an *incremental* data transfer (\[Preview\](https://cloud.google.com/products\#product-launch-stages)) to only transfer data that was changed since the last data transfer, instead of loading the entire dataset with each data transfer. If you select **Incremental** for your data transfer, you must specify either the **Append** or **Upsert** write modes to define how data is written to BigQuery during an incremental data transfer. The following sections describe the available write modes.

#### Append write mode

The append write mode only inserts new rows to your destination table. This option strictly appends transferred data without checking for existing records, so this mode can potentially cause data duplication in the destination table.

When you select the append mode, you must select a watermark column. A watermark column is required for the PostgreSQL connector to track changes in the source table.

For PostgreSQL transfers, we recommend selecting a column that is only updated when the record was created, and won't change with subsequent updates. For example, the `CREATED_AT` column.

#### Upsert write mode

The upsert write mode either updates a row or inserts a new row in your destination table by checking for a primary key. You can specify a primary key to let the PostgreSQL connector determine what changes are needed to keep your destination table up to date with your source table. If the specified primary key is present in the destination BigQuery table during a data transfer, then the PostgreSQL connector updates that row with new data from the source table. If a primary key is not present during a data transfer, then the PostgreSQL connector inserts a new row.

When you select the upsert mode, you must select a watermark column and a primary key:

  - A watermark column is required for the PostgreSQL connector to track changes in the source table.
      - Select a watermark column that updates every time a row is modified. We recommend columns similar to the `UPDATED_AT` or `LAST_MODIFIED` column.

<!-- end list -->

  - The primary key can be one or more columns on your table that are required for the PostgreSQL connector to determine if it needs to insert or update a row.
    
    Select columns that contain non-null values that are unique across all rows of the table. We recommend columns that include system-generated identifiers, unique reference codes (for example, auto-incrementing IDs), or immutable time-based sequence IDs.
    
    To prevent potential data loss or data corruption, the primary key columns that you select must have unique values. If you have doubts about the uniqueness of your chosen primary key column, then we recommend that you use the append write mode instead.

### Incremental ingestion behavior

When you make changes to the table schema in your data source, incremental data transfers from those tables are reflected in BigQuery in the following ways:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Changes to data source</th>
<th>Incremental ingestion behavior</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Adding a new column</td>
<td>A new column is added to the destination BigQuery table. Any previous records for this column will have null values.</td>
</tr>
<tr class="even">
<td>Deleting a column</td>
<td>The deleted column remains in the destination BigQuery table. New entries to this deleted column are populated with null values.</td>
</tr>
<tr class="odd">
<td>Changing the data type in a column</td>
<td>The connector only supports <a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#alter_column_set_data_type_statement">data type conversions that are supported by the <code dir="ltr" translate="no">ALTER COLUMN</code> DDL statement</a> . Any other data type conversion causes the data transfer to fail.
<p>If you encounter any issues, we recommend creating a new transfer configuration.</p></td>
</tr>
<tr class="even">
<td>Renaming a column</td>
<td>The original column remains in the destination BigQuery table as is, while a new column is added to the destination table with the updated name.</td>
</tr>
</tbody>
</table>

## Data type mapping

> **Note:** On March 16, 2027, the PostgreSQL connector will update some of its data type mapping. For more information, see [March 16, 2027](https://docs.cloud.google.com/bigquery/docs/transfer-changes#Mar16-postgresql) .

The following table maps PostgreSQL data types to the corresponding BigQuery data types:

| PostgreSQL data type                                  | BigQuery data type | [Updated BigQuery data type](https://docs.cloud.google.com/bigquery/docs/transfer-changes#Mar16-postgresql) |
| ----------------------------------------------------- | ------------------ | ----------------------------------------------------------------------------------------------------------- |
| `array`                                               | `STRING`           |                                                                                                             |
| `bigint`                                              | `INTEGER`          |                                                                                                             |
| `bigserial`                                           | `INTEGER`          |                                                                                                             |
| `bit(n)`                                              | `STRING`           |                                                                                                             |
| `bit varying(n)`                                      | `STRING`           |                                                                                                             |
| `boolean`                                             | `BOOLEAN`          |                                                                                                             |
| `box`                                                 | `STRING`           |                                                                                                             |
| `bytea`                                               | `BYTES`            |                                                                                                             |
| `character`                                           | `STRING`           |                                                                                                             |
| `character varying`                                   | `STRING`           |                                                                                                             |
| `cidr`                                                | `STRING`           |                                                                                                             |
| `circle`                                              | `STRING`           |                                                                                                             |
| `circularstring`                                      | `STRING`           |                                                                                                             |
| `compoundcurve`                                       | `STRING`           |                                                                                                             |
| `curvepolygon`                                        | `STRING`           |                                                                                                             |
| `date`                                                | `DATE`             |                                                                                                             |
| `double precision`                                    | `FLOAT`            |                                                                                                             |
| `enum`                                                | `STRING`           |                                                                                                             |
| `geometrycollection`                                  | `STRING`           |                                                                                                             |
| `inet`                                                | `STRING`           |                                                                                                             |
| `integer`                                             | `INTEGER`          |                                                                                                             |
| `interval`                                            | `STRING`           |                                                                                                             |
| `json`                                                | `STRING`           | `JSON`                                                                                                      |
| `jsonb`                                               | `STRING`           | `JSON`                                                                                                      |
| `line`                                                | `STRING`           |                                                                                                             |
| `linestring`                                          | `STRING`           |                                                                                                             |
| `lseg`                                                | `STRING`           |                                                                                                             |
| `macaddr`                                             | `STRING`           |                                                                                                             |
| `macaddr8`                                            | `STRING`           |                                                                                                             |
| `money`                                               | `STRING`           |                                                                                                             |
| `multicurve`                                          | `STRING`           |                                                                                                             |
| `multilinestring`                                     | `STRING`           |                                                                                                             |
| `multipoint`                                          | `STRING`           |                                                                                                             |
| `multipolygon`                                        | `STRING`           |                                                                                                             |
| `multisurface`                                        | `STRING`           |                                                                                                             |
| `numeric(precision, scale)/decimal(precision, scale)` | `NUMERIC`          |                                                                                                             |
| `path`                                                | `STRING`           |                                                                                                             |
| `point`                                               | `STRING`           |                                                                                                             |
| `polygon`                                             | `STRING`           |                                                                                                             |
| `polyhedralsurface`                                   | `STRING`           |                                                                                                             |
| `range`                                               | `STRING`           |                                                                                                             |
| `real`                                                | `FLOAT`            |                                                                                                             |
| `serial`                                              | `INTEGER`          |                                                                                                             |
| `smallint`                                            | `INTEGER`          |                                                                                                             |
| `smallserial`                                         | `INTEGER`          |                                                                                                             |
| `text`                                                | `STRING`           |                                                                                                             |
| `time [ (p) ] [ without timezone ]`                   | `TIMESTAMP`        |                                                                                                             |
| `time [ (p) ] with time zone`                         | `TIMESTAMP`        |                                                                                                             |
| `tin`                                                 | `STRING`           |                                                                                                             |
| `timestamp [ (p) ] [ without timezone ]`              | `TIMESTAMP`        | `DATETIME`                                                                                                  |
| `timestamp [ (p) ] with time zone`                    | `TIMESTAMP`        |                                                                                                             |
| `triangle`                                            | `STRING`           |                                                                                                             |
| `tsquery`                                             | `STRING`           |                                                                                                             |
| `tsvector`                                            | `STRING`           |                                                                                                             |
| `uuid`                                                | `STRING`           |                                                                                                             |
| `xml`                                                 | `STRING`           |                                                                                                             |

## Pricing

For pricing information about PostgreSQL transfers, see [Data Transfer Service pricing](https://docs.cloud.google.com/bigquery/pricing#data-transfer-service-pricing) .

## What's next

  - Learn about [setting up a PostgreSQL transfer](https://docs.cloud.google.com/bigquery/docs/postgresql-transfer) .
  - Learn more about the [BigQuery Data Transfer Service](https://docs.cloud.google.com/bigquery/docs/dts-introduction) .
