# Introduction to continuous queries

This document describes BigQuery continuous queries.

BigQuery continuous queries are SQL statements that run continuously. Continuous queries let you analyze incoming data in BigQuery in real time. You can insert the output rows produced by a continuous query into a BigQuery table or export them to Pub/Sub, Bigtable, or Spanner. Continuous queries can process data that has been written to [standard BigQuery tables](/bigquery/docs/tables-intro#standard-tables) by using one of the following methods:

  - The [BigQuery Storage Write API](/bigquery/docs/write-api)
  - The [`  tabledata.insertAll  ` method](/bigquery/docs/reference/rest/v2/tabledata/insertAll)
  - [Batch load](/bigquery/docs/batch-loading-data)
  - The [`  INSERT  ` DML statement](/bigquery/docs/reference/standard-sql/dml-syntax#insert_statement)
  - Writes from the [results of a batch query to a permanent table](/bigquery/docs/writing-results#permanent-table)
  - Writes from the [results of a BigQuery continuous query to a permanent table](/bigquery/docs/continuous-queries#write-bigquery)
  - A [Pub/Sub BigQuery subscription](/pubsub/docs/bigquery)
  - Writes from [Dataflow to BigQuery](/dataflow/docs/guides/write-to-bigquery)
  - Writes from Datastream to BigQuery using [append-only write mode](/datastream/docs/destination-bigquery#append-only_write_mode)

You can use continuous queries to perform time sensitive tasks, such as creating and immediately acting on insights, applying real time machine learning (ML) inference, and replicating data into other platforms. This lets you use BigQuery as an event-driven data processing engine for your application's decision logic.

The following diagram shows common continuous query workflows:

## Use cases

Common use cases where you might want to use continuous queries are as follows:

  - **Personalized customer interaction services** : use generative AI to create tailored messages customized for each customer interaction.
  - **Anomaly detection** : build solutions that let you perform anomaly and threat detection on complex data in real time, so that you can react to issues more quickly.
  - **Customizable event-driven pipelines** : use continuous query integration with Pub/Sub to trigger downstream applications based on incoming data.
  - **Data enrichment and entity extraction** : use continuous queries to perform real time data enrichment and transformation by using SQL functions and ML models.
  - **Reverse extract-transform-load (ETL)** : perform real time reverse ETL into other storage systems more suited for low latency application serving. For example, analyzing or enhancing event data that is written to BigQuery, and then streaming it to Bigtable or Spanner for application serving.

## Supported operations

The following operations are supported in continuous queries:

  - Running [`  INSERT  ` statements](/bigquery/docs/reference/standard-sql/dml-syntax#insert_statement) to write data from a continuous query into a BigQuery table.

  - Running [`  EXPORT DATA  ` statements](/bigquery/docs/reference/standard-sql/export-statements) to [publish](/pubsub/docs/publish-message-overview) continuous query output to Pub/Sub topics. For more information, see [Export data to Pub/Sub](/bigquery/docs/export-to-pubsub) .
    
    From a Pub/Sub topic, you can use the data with other services, such as performing streaming analytics by using Dataflow, or using the data in an application integration workflow.

  - Running `  EXPORT DATA  ` statements to export data from BigQuery to [Bigtable tables](/bigtable/docs/managing-tables) . For more information, see [Export data to Bigtable](/bigquery/docs/export-to-bigtable) .

  - Running `  EXPORT DATA  ` statements to export data from BigQuery to Spanner tables. For more information, see [Export data to Spanner (reverse ETL)](/bigquery/docs/export-to-spanner) .

  - Calling the following generative AI functions:
    
      - [`  AI.GENERATE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate)
    
      - [`  AI.GENERATE_TEXT  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-text)
        
          - This function requires you to have a [BigQuery ML remote model](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model) over a [Vertex AI model](/vertex-ai/generative-ai/docs/learn/models) .

  - Calling the following AI functions:
    
      - [`  ML.UNDERSTAND_TEXT  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-understand-text)
      - [`  ML.TRANSLATE  `](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-translate)
    
    These functions require you to have a [BigQuery ML remote model](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model-service) over a Cloud AI API.

  - Normalizing numerical data by using the [`  ML.NORMALIZER  ` function](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-normalizer) .

  - Using stateless GoogleSQL functions—for example, [conversion functions](/bigquery/docs/reference/standard-sql/conversion_functions) . In stateless functions, each row is processed independently from other rows in the table.

  - Using the [`  APPENDS  `](/bigquery/docs/reference/standard-sql/time-series-functions#appends) change history function to start continuous query processing from a specific point in time.

## Authorization

The [Google Cloud access tokens](/docs/authentication/token-types#access-tokens) that are used when running continuous query jobs have a time to live (TTL) of two days when they are generated by a user account. Therefore, such jobs stop running after two days. The access tokens that are generated by service accounts can run longer, but must still adhere to the maximum query runtime. For more information, see [Run a continuous query by using a service account](/bigquery/docs/continuous-queries#run_a_continuous_query_by_using_a_service_account) .

## Locations

For a list of supported regions, see [BigQuery continuous query locations](/bigquery/docs/locations#continuous-query-loc) .

## Limitations

Continuous queries are subject to the following limitations:

  - BigQuery continuous queries don't maintain the state of ingested data. Common operations that rely on state, such as a `  JOIN  ` , aggregation function, or window function, aren't supported.

  - You can't use the following SQL capabilities in a continuous query:
    
      - [`  JOIN  ` operations](/bigquery/docs/reference/standard-sql/query-syntax#join_types)
    
      - [Aggregate functions](/bigquery/docs/reference/standard-sql/aggregate_functions)
    
      - [Approximate aggregate functions](/bigquery/docs/reference/standard-sql/approximate_aggregate_functions)
    
      - The following [query](/bigquery/docs/reference/standard-sql/query-syntax) clauses:
        
          - [`  GROUP BY  `](/bigquery/docs/reference/standard-sql/query-syntax#group_by_clause)
          - [`  HAVING  `](/bigquery/docs/reference/standard-sql/query-syntax#having_clause)
          - [`  ORDER BY  `](/bigquery/docs/reference/standard-sql/query-syntax#order_by_clause)
          - [`  LIMIT  `](/bigquery/docs/reference/standard-sql/query-syntax#limit_and_offset_clause)
    
      - The following [query](/bigquery/docs/reference/standard-sql/query-syntax) operators:
        
          - [`  PIVOT  `](/bigquery/docs/reference/standard-sql/query-syntax#pivot_operator)
          - [`  UNPIVOT  `](/bigquery/docs/reference/standard-sql/query-syntax#unpivot_operator)
          - [`  TABLESAMPLE  `](/bigquery/docs/reference/standard-sql/query-syntax#tablesample_operator)
    
      - Query [set operators](/bigquery/docs/reference/standard-sql/query-syntax#set_operators)
    
      - The [`  SELECT DISTINCT  ` statement](/bigquery/docs/reference/standard-sql/query-syntax#select_distinct)
    
      - [`  EXISTS  ` or `  NOT EXISTS  ` subqueries](/bigquery/docs/reference/standard-sql/subqueries#exists_subquery_concepts)
    
      - [Recursive CTEs](/bigquery/docs/recursive-ctes)
    
      - [User-defined functions](/bigquery/docs/user-defined-functions)
    
      - [Windowing functions](/bigquery/docs/reference/standard-sql/window-function-calls)
    
      - BigQuery ML functions other than those listed in [Supported operations](#supported_operations)
    
      - [Data definition language (DDL) statements](/bigquery/docs/reference/standard-sql/data-definition-language)
    
      - [Data manipulation language (DML) statements](/bigquery/docs/reference/standard-sql/dml-syntax) except for `  INSERT  ` .
    
      - [Data control language (DCL) statements](/bigquery/docs/reference/standard-sql/data-control-language)
    
      - `  EXPORT DATA  ` statements that don't target Bigtable, Pub/Sub, or Spanner.
    
      - [Procedural language](/bigquery/docs/reference/standard-sql/procedural-language)
    
      - [Debugging statements](/bigquery/docs/reference/standard-sql/debugging-statements)

  - Continuous queries don't support the following data sources:
    
      - [External tables](/bigquery/docs/external-data-sources) .
      - [Information schema views](/bigquery/docs/information-schema-intro) .
      - [BigLake tables for Apache Iceberg in BigQuery](/bigquery/docs/iceberg-tables) .
      - [Wildcard tables](/bigquery/docs/querying-wildcard-tables) .
      - [Change Data Capture (CDC) upsert](/bigquery/docs/change-data-capture) data.
      - [Materialized views](/bigquery/docs/materialized-views-intro) .
      - [Views](/bigquery/docs/views) that are defined by other continuous query limitations, such as `  JOIN  ` operations, aggregate functions, change data capture enabled tables.

  - Continuous queries don't support the [column-](/bigquery/docs/column-level-security-intro) and [row-level](/bigquery/docs/row-level-security-intro) security features.

  - The output of a continuous query is subject to the inherent quotas and limits of the destination service the output is being exported to.

  - When exporting data to Bigtable, Spanner, or [Pub/Sub locational endpoints](/pubsub/docs/reference/service_apis_overview#pubsub_endpoints) you can only target Bigtable, Spanner, or Pub/Sub resources that fall within the same Google Cloud regional boundary as the BigQuery dataset that contains the table you are querying. This restriction doesn't apply when exporting data to Pub/Sub global endpoints. For more information about exporting to a [Bigtable app profile](/bigtable/docs/app-profiles) routing policy, see [Location considerations](/bigquery/docs/export-to-bigtable#data-locations) .

  - You can't run a continuous query from a [data canvas](/bigquery/docs/data-canvas) .

  - You can't modify the SQL used in a continuous query while the continuous query job is running. For more information, see [Modify the SQL of a continuous query](/bigquery/docs/continuous-queries#modify_the_sql_of_a_continuous_query) .

  - If a continuous query job falls behind in processing incoming data and has an [output watermark lag](/bigquery/docs/monitoring-dashboard#metrics) of more than 48 hours, then it fails. You can run the query again and use the [`  APPENDS  `](/bigquery/docs/reference/standard-sql/time-series-functions#appends) change history function to resume processing from the point in time at which you stopped the previous continuous query job. For more information, see [Start a continuous query from a particular point in time](/bigquery/docs/continuous-queries#start_a_continuous_query_from_a_particular_point_in_time) .

  - A continuous query configured with a user account can run for up to two days. A continuous query configured with a service account can run for up to 150 days. When the maximum query runtime is reached, the query fails and stops processing incoming data.

  - Although continuous queries are built using [BigQuery reliability features](/bigquery/docs/reliability-intro) , occasional temporary issues can occur. Issues might lead to some amount of automatic reprocessing of your continuous query, which could result in duplicate data in the continuous query output. Design your downstream systems to handle such scenarios.

### Reservation limitations

  - You must create Enterprise edition or Enterprise Plus edition [reservations](/bigquery/docs/reservations-intro) in order to run continuous queries. Continuous queries don't support the on-demand compute billing model.
  - When you create a `  CONTINUOUS  ` [reservation assignment](/bigquery/docs/reservations-assignments) , the associated reservation is limited to at most 500 slots. You can request an increase to this limit by contacting <bq-continuous-queries-feedback@google.com> .
  - You can't create a reservation assignment that uses a different [job type](/bigquery/docs/reservations-workload-management#assignments) in the same reservation as a continuous query reservation assignment.
  - You can't configure continuous query concurrency. BigQuery automatically determines the number of continuous queries that can run concurrently, based on available reservation assignments that use the `  CONTINUOUS  ` job type.
  - When running multiple continuous queries using the same reservation, individual jobs might not split available resources fairly, as defined by [BigQuery fairness](/bigquery/docs/slots#fair_scheduling_in_bigquery) .

## Slots autoscaling

Continuous queries can use [slot autoscaling](/bigquery/docs/slots-autoscaling-intro) to dynamically scale allocated capacity to accommodate your workload. As your continuous queries workload increases or decreases, BigQuery dynamically adjusts your slots.

After a continuous query starts running, it actively *listens* for incoming data, which consumes slot resources. While a reservation with a running continuous query does not scale down to zero slots, an idle continuous query that is primarily listening for incoming data is expected to consume a minimal amount of slots, typically around 1 slot.

## Idle slot sharing

Continuous queries can use [idle slot sharing](/bigquery/docs/slots#idle_slots) to share unused slot resources with other reservations and [job types](/bigquery/docs/reservations-workload-management#assignments) .

  - A `  CONTINUOUS  ` [reservation assignment](/bigquery/docs/reservations-assignments) is still required to run a continuous query and can't solely rely on idle slots from other reservations. Thus a `  CONTINUOUS  ` reservation assignment requires either a non-zero slot baseline or a non-zero slot autoscaling configuration.
  - Only idle baseline slots or committed slots from a `  CONTINUOUS  ` reservation assignment are sharable. [Autoscaled slots](/bigquery/docs/slots-autoscaling-intro) aren't shareable as idle slots for other reservations.

## Pricing

Continuous queries use [BigQuery capacity compute pricing](https://cloud.google.com/bigquery/pricing#capacity_compute_analysis_pricing) , which is measured in [slots](/bigquery/docs/slots) . To run continuous queries, you must have a [reservation](/bigquery/docs/reservations-workload-management) that uses the [Enterprise or Enterprise Plus edition](/bigquery/docs/editions-intro) , and a [reservation assignment](/bigquery/docs/reservations-workload-management#assignments) that uses the `  CONTINUOUS  ` job type.

Usage of other BigQuery resources, such as data ingestion and storage, are charged at the rates shown in [BigQuery pricing](https://cloud.google.com/bigquery/pricing) .

Usage of other services that receive continuous query results or that are called during continuous query processing are charged at the rates published for those services. For the pricing of other Google Cloud services used by continuous queries, see the following topics:

  - [Bigtable pricing](https://cloud.google.com/bigtable/pricing)
  - [Pub/Sub pricing](https://cloud.google.com/pubsub/pricing)
  - [Spanner pricing](https://cloud.google.com/spanner/pricing)
  - [Vertex AI pricing](https://cloud.google.com/vertex-ai/pricing)

## What's next

Try [creating a continuous query](/bigquery/docs/continuous-queries) .
