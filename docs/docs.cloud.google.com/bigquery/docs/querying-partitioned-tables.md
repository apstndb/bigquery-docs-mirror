---
name: documents/docs.cloud.google.com/bigquery/docs/querying-partitioned-tables
uri: https://docs.cloud.google.com/bigquery/docs/querying-partitioned-tables
title: Query partitioned tables
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# Query partitioned tables

This document describes some specific considerations for querying [partitioned tables](https://docs.cloud.google.com/bigquery/docs/partitioned-tables) in BigQuery.

For general information on running queries in BigQuery, see [Running interactive and batch queries](https://docs.cloud.google.com/bigquery/docs/running-queries) .

## Overview

If a query uses a qualifying filter on the value of the partitioning column, BigQuery can scan the partitions that match the filter and skip the remaining partitions. This process is called *partition pruning* .

Partition pruning is the mechanism BigQuery uses to eliminate unnecessary partitions from the input scan. The pruned partitions are not included when calculating the bytes scanned by the query. In general, partition pruning helps reduce query cost.

Pruning behaviors vary for the different types of partitioning, so you could see a difference in bytes processed when querying tables that are partitioned differently but are otherwise identical. To estimate how many bytes a query will process, perform a [dry run](https://docs.cloud.google.com/bigquery/docs/running-queries#dry-run) .

## Query a time-unit column-partitioned table

To prune partitions when you query a [time-unit column-partitioned table](https://docs.cloud.google.com/bigquery/docs/partitioned-tables#date_timestamp_partitioned_tables) , include a filter on the partitioning column.

In the following example, assume that `dataset.table` is partitioned on the `transaction_date` column. The example query prunes dates before `2016-01-01` .

    SELECT * FROM dataset.table
    WHERE transaction_date >= '2016-01-01'

## Query an ingestion-time partitioned table

[Ingestion-time partitioned tables](https://docs.cloud.google.com/bigquery/docs/partitioned-tables#ingestion_time) contain a pseudocolumn named `_PARTITIONTIME` , which is the partitioning column. The value of the column is the UTC ingestion time for each row, truncated to the partition boundary (such as hourly or daily), as a `TIMESTAMP` value.

For example, if you append data on April 15, 2021, 08:15:00 UTC, the `_PARTITIONTIME` column for those rows contains the following values:

  - Hourly partitioned table: `TIMESTAMP("2021-04-15 08:00:00")`
  - Daily partitioned table: `TIMESTAMP("2021-04-15")`
  - Monthly partitioned table: `TIMESTAMP("2021-04-01")`
  - Yearly partitioned table: `TIMESTAMP("2021-01-01")`

If the partition granularity is daily, the table also contains a pseudocolumn named `_PARTITIONDATE` . The value is equal to `_PARTITIONTIME` truncated to a `DATE` value.

Both of these pseudocolumn names are reserved. You can't create a column with either name in any of your tables.

To prune partitions, filter on either of these columns. For example, the following query scans only the partitions between the dates January 1, 2016 and January 2, 2016:

    SELECT
      column
    FROM
      dataset.table
    WHERE
      _PARTITIONTIME BETWEEN TIMESTAMP('2016-01-01') AND TIMESTAMP('2016-01-02')

To select the `_PARTITIONTIME` pseudocolumn, you must use an alias. For example, the following query selects `_PARTITIONTIME` by assigning the alias `pt` to the pseudocolumn:

    SELECT
      _PARTITIONTIME AS pt, column
    FROM
      dataset.table

For daily partitioned tables, you can select the `_PARTITIONDATE` pseudocolumn in the same way:

    SELECT
      _PARTITIONDATE AS pd, column
    FROM
      dataset.table

The `_PARTITIONTIME` and `_PARTITIONDATE` pseudocolumns are not returned by a `SELECT *` statement. You must select them explicitly:

    SELECT
      _PARTITIONTIME AS pt, *
    FROM
      dataset.table

### Handle time zones in ingestion-time partitioned tables

The value of `_PARTITIONTIME` is based on the UTC date when the field is populated. If you want to query data based on a time zone other than UTC, choose one of the following options:

  - Adjust for time zone differences in your SQL queries.
  - Use [partition decorators](https://docs.cloud.google.com/bigquery/docs/managing-partitioned-table-data#write-to-partition) to load data into specific ingestion-time partitions, based on a different time zone than UTC.

### Better performance with pseudocolumns

To improve query performance, use the `_PARTITIONTIME` pseudocolumn by itself on the left side of a comparison.

For example, the following two queries are equivalent. Depending on the table size, the second query might perform better, because it places `_PARTITIONTIME` by itself on the left side of the `>` operator. Both queries process the same amount of data.

    -- Might be slower.
    SELECT
      field1
    FROM
      dataset.table1
    WHERE
      TIMESTAMP_ADD(_PARTITIONTIME, INTERVAL 5 DAY) > TIMESTAMP("2016-04-15");
    
    -- Often performs better.
    SELECT
      field1
    FROM
      dataset.table1
    WHERE
      _PARTITIONTIME > TIMESTAMP_SUB(TIMESTAMP('2016-04-15'), INTERVAL 5 DAY);

To limit the partitions that are scanned in a query, use a constant expression in your filter. The following query limits which partitions are pruned based on the first filter condition in the `WHERE` clause. However, the second filter condition doesn't limit the scanned partitions, because it uses table values, which are dynamic.

    SELECT
      column
    FROM
      dataset.table2
    WHERE
      -- This filter condition limits the scanned partitions:
      _PARTITIONTIME BETWEEN TIMESTAMP('2017-01-01') AND TIMESTAMP('2017-03-01')
      -- This one doesn't, because it uses dynamic table values:
      AND _PARTITIONTIME = (SELECT MAX(timestamp) from dataset.table1)

To limit the partitions scanned, don't include any other columns in a `_PARTITIONTIME` filter. For example, the following query does not limit the scanned partitions, because `field1` is a column in the table.

    -- Scans all partitions of table2. No pruning.
    SELECT
      field1
    FROM
      dataset.table2
    WHERE
      _PARTITIONTIME + field1 = TIMESTAMP('2016-03-28');

If you often query a particular range of times, consider creating a view that filters on the `_PARTITIONTIME` pseudocolumn. For example, the following statement creates a view that includes only the most recent seven days of data from a table named `dataset.partitioned_table` :

    -- This view provides pruning.
    CREATE VIEW dataset.past_week AS
      SELECT *
      FROM
        dataset.partitioned_table
      WHERE _PARTITIONTIME BETWEEN
        TIMESTAMP_TRUNC(TIMESTAMP_SUB(CURRENT_TIMESTAMP, INTERVAL 7 * 24 HOUR), DAY)
        AND TIMESTAMP_TRUNC(CURRENT_TIMESTAMP, DAY);

For information about creating views, see [Creating views](https://docs.cloud.google.com/bigquery/docs/views) .

## Query an integer-range partitioned table

To prune partitions when you query an [integer-range partitioned table](https://docs.cloud.google.com/bigquery/docs/partitioned-tables#integer_range) , include a filter on the integer partitioning column.

In the following example, assume that `dataset.table` is an integer-range partitioned table with a partitioning specification of `customer_id:0:100:10` The example query scans the three partitions that start with 30, 40, and 50.

    SELECT * FROM dataset.table
    WHERE customer_id BETWEEN 30 AND 50
    
    +-------------+-------+
    | customer_id | value |
    +-------------+-------+
    |          40 |    41 |
    |          45 |    46 |
    |          30 |    31 |
    |          35 |    36 |
    |          50 |    51 |
    +-------------+-------+

Partition pruning is not supported for functions over an integer range partitioned column. For example, the following query scans the entire table.

    SELECT * FROM dataset.table
    WHERE customer_id + 1 BETWEEN 30 AND 50

## Query data in the write-optimized storage

The `__UNPARTITIONED__` partition temporarily holds data that is streamed to a partitioned table while it is in the [write-optimized storage](https://docs.cloud.google.com/bigquery/docs/streaming-data-into-bigquery#dataavailability) . Data that is streamed directly to a specific partition of a partitioned table does not use the `__UNPARTITIONED__` partition. Instead, the data is streamed directly to the partition.

Data in the write-optimized storage has `NULL` values in the `_PARTITIONTIME` and `_PARTITIONDATE` columns.

To query data in the `__UNPARTITIONED__` partition, use the `_PARTITIONTIME` pseudocolumn with the `NULL` value. For example:

    SELECT
      column
    FROM dataset.table
    WHERE
      _PARTITIONTIME IS NULL

For more information, see [Streaming into partitioned tables](https://docs.cloud.google.com/bigquery/docs/streaming-data-into-bigquery#streaming_into_partitioned_tables) .

## Best practices for partition pruning

This section describes best practices for writing queries that utilize partition pruning to optimize query performance and reduce cost.

### Use a constant filter expression

To limit the partitions that are scanned in a query, filter the partitioning column using a constant expression, rather than a dynamic expression.

The following query prunes partitions:

    SELECT
      t1.name, t1.quantity
    FROM
      table1 AS t1
    WHERE
      t1.ts = CURRENT_TIMESTAMP()

In comparison, the following query doesn't prune partitions, because the predicate, `WHERE t1.ts = (SELECT timestamp FROM table3 WHERE key = 2)` , is not a constant expression. This query compares the partitioning column to a dynamic value, what prevents partition pruning.

    SELECT
      t1.name, t1.quantity
    FROM
      table1 AS t1
    WHERE
      t1.ts = (SELECT timestamp FROM table3 WHERE key = 2)

Additionally, a query with the following predicates don't prune partitions because they require a computation based on a second, non-constant table column `ts2` or `duration` :

    WHERE ts >= ts2
    
    WHERE ts < CURRENT_TIMESTAMP() - duration

### Isolate the partitioning column or use supported functions

To prune partitions, filter conditions must be structured so that BigQuery can determine which partitions to scan without reading table data. To achieve this, isolate the partitioning column on one side of a comparison operator, or wrap the column only in a supported built-in function. You can use [dry run](https://docs.cloud.google.com/bigquery/docs/running-queries#dry-run) to verify if partition pruning is supported on your particular query.

The following built-in functions on the partitioning column support partition pruning, if their additional arguments are constant:

  - [`DATE_ADD`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/date_functions#date_add) , [`DATE_DIFF`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/date_functions#date_diff) , [`DATE_SUB`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/date_functions#date_sub) , [`DATE_TRUNC`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/date_functions#date_trunc) , [`EXTRACT`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/date_functions#extract) with `YEAR` part,
  - [`DATETIME_DIFF`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/datetime_functions#datetime_diff) ,
  - [`TIMESTAMP_ADD`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp_add) , [`TIMESTAMP_DIFF`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp_diff) , [`TIMESTAMP_SUB`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp_sub) , [`TIMESTAMP_TRUNC`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/timestamp_functions#timestamp_trunc) , [`EXTRACT`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/timestamp_functions#extract) with `DATE` or `YEAR` parts,
  - [`FORMAT_TIMESTAMP`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/timestamp_functions#format_timestamp) with the following format specifiers: `%F` , `%Y-%m-%d` and `%Y%m%d` .

Other functions and complex mathematical operations will require a full table scan.

#### Examples

The following queries show example predicates that support partition pruning.

    SELECT COUNT(*) FROM `bigquery-public-data.wikipedia.pageviews_2025`
    WHERE datehour = '2025-03-30 12:00:00';

    SELECT COUNT(*) FROM `bigquery-public-data.wikipedia.pageviews_2025`
    WHERE datehour >= '2025-03-30'
      AND datehour < TIMESTAMP_ADD('2025-03-30', INTERVAL 1 DAY);

    SELECT COUNT(*) FROM `bigquery-public-data.wikipedia.pageviews_2025`
    WHERE DATE(datehour) = '2025-03-30';

    SELECT COUNT(*) FROM `bigquery-public-data.wikipedia.pageviews_2025`
    WHERE EXTRACT(DATE FROM datehour) = '2025-03-30';

    SELECT COUNT(*) FROM `bigquery-public-data.wikipedia.pageviews_2025`
    WHERE CAST(datehour AS DATE) = '2025-03-30';

    SELECT COUNT(*) FROM `bigquery-public-data.wikipedia.pageviews_2025`
    WHERE datehour >= '2025-01-01' AND datehour < '2025-02-01';

    SELECT COUNT(*) FROM `bigquery-public-data.wikipedia.pageviews_2025`
    WHERE TIMESTAMP_TRUNC(datehour, MONTH) >= '2025-04-01'
      AND TIMESTAMP_TRUNC(datehour, MONTH) < '2025-07-01';

    SELECT COUNT(*) FROM `bigquery-public-data.wikipedia.pageviews_2025`
    WHERE TIMESTAMP_DIFF(datehour, '2025-01-01', DAY) < 1;

    SELECT COUNT(*) FROM `bigquery-public-data.wikipedia.pageviews_2025`
    WHERE TIMESTAMP_ADD(datehour, INTERVAL 1 DAY) < '2025-01-03';

    SELECT COUNT(*) FROM `bigquery-public-data.wikipedia.pageviews_2025`
    WHERE TIMESTAMP_SUB(datehour, INTERVAL 1 DAY) < '2025-01-01';

The following query skips all partitions because the predicate doesn't match any row.

    SELECT COUNT(*) FROM `bigquery-public-data.wikipedia.pageviews_2025`
    WHERE EXTRACT(YEAR FROM datehour) = 1900;

The following query select the first day of each month in the table, and it supports partition pruning.

    SELECT COUNT(*) FROM bigquery-public-data.wikipedia.pageviews_2025WHERE DATE(datehour) IN UNNEST(GENERATE_DATE_ARRAY(  DATE_TRUNC(CURRENT_DATE(), YEAR),  DATE(DATE_TRUNC(CURRENT_DATE(), YEAR) + INTERVAL 1 YEAR - INTERVAL 1 DAY),  INTERVAL 1 MONTH))

Queries with the following predicates doesn't prune partitions because it manipulates the partitioning column with unsupported functions:

    WHERE FORMAT_DATE('%Y-%m-%d %H', ts) = '2025-03-28 20';
    
    WHERE EXTRACT(MONTH FROM ts) = 3 AND EXTRACT(HOUR FROM ts) = 20

Similarly, a query with the following predicate doesn't prune partitions because it manipulates the partitioning column with an arithmetic operation:

    WHERE ts + INTERVAL 1 DAY > CURRENT_TIMESTAMP()

To enable partition pruning, you must rewrite the expression by isolating the partitioning column `ts` from the unsupported functions or arithmetic operations. For time ranges, use `>=` and `<` to capture the exact range. For arithmetic, move the operation to the other side of the comparison.

The following query allows for partition pruning by isolating the partitioning column `ts` for a time range:

    WHERE ts >= '2025-03-28 20:00:00' AND ts < '2025-03-28 21:00:00'

The following query allows for partition pruning by isolating the partitioning column from the arithmetic operation:

    WHERE ts > CURRENT_TIMESTAMP() - INTERVAL 1 DAY

### Filter on multiple columns

A predicate on the partitioning column in a query doesn't restrict what else you can filter on. You can include predicates on other columns in the same `WHERE` clause, and partition pruning will still occur as long as the condition evaluating the partitioning column follows the best practices. Note that `AND` is important in the following example. If `AND` is changed to `OR` , partition pruning won't work, as even if a partition doesn't match the predicate on the partitioning column, it still cannot be pruned. Data in these partitions with `meter_id = 1234` still qualifies for the query.

Note that the predicates don't need to be written in a specific order. In the following sample query, assuming partitioning on the `ts` column, partition pruning still occurs regardless of predicate placement.

    WHERE meter_id = 1234
      AND ts >= '2025-03-28 20:00:00' AND ts < '2025-03-28 21:00:00'

### Require a partition filter in queries

When you create a partitioned table, you can require the use of predicate filters by enabling the **Require partition filter** option. When this option is applied, attempts to query the partitioned table without specifying a `WHERE` clause produce the following error:

`Cannot query over table 'project_id.dataset.table' without a filter that can be used for partition elimination` .

This requirement also applies to queries on views and materialized views that reference the partitioned table.

There must be at least one predicate that only references a partitioning column for the filter to be considered eligible for partition elimination. For a table partitioned on column `partition_id` with an additional column `f` in its schema, both of the following `WHERE` clauses satisfy the requirement:

    WHERE partition_id = "20221231"
    
    WHERE partition_id = "20221231" AND f = "20221130"

However, the following is not sufficient, and will result in an error:

    WHERE partition_id = "20221231" OR f = "20221130"

For ingestion-time partitioned tables, use either the `_PARTITIONTIME` or `_PARTITIONDATE` pseudocolumn.

For more information about adding the **Require partition filter** option when you create a partitioned table, see [Creating partitioned tables](https://docs.cloud.google.com/bigquery/docs/creating-partitioned-tables) . You can also [update](https://docs.cloud.google.com/bigquery/docs/managing-partitioned-tables#require-filter) this setting on an existing table.

## What's next

  - For an overview of partitioned tables, see [Introduction to partitioned tables](https://docs.cloud.google.com/bigquery/docs/partitioned-tables) .
  - To learn more about creating partitioned tables, see [Creating partitioned tables](https://docs.cloud.google.com/bigquery/docs/creating-partitioned-tables) .
