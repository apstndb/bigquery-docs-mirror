---
name: documents/docs.cloud.google.com/bigquery/docs/graph-overview
uri: https://docs.cloud.google.com/bigquery/docs/graph-overview
title: Introduction to BigQuery Graph
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# Introduction to BigQuery Graph

> **Note:** This feature may not be available when using reservations that are created with certain BigQuery editions. For more information about which features are enabled in each edition, see [Introduction to BigQuery editions](https://docs.cloud.google.com/bigquery/docs/editions-intro) .

[Video](https://www.youtube.com/watch?v=_9YTyst9xWg)

BigQuery Graph lets you use the analytical power of BigQuery to perform graph analysis on a large scale. When you model your data as a graph with nodes and edges, you can use [Graph Query Language (GQL)](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/graph-intro) to find complex, hidden relationships between data points that would be challenging to find using SQL.

You can create node and edge tables directly from tables or views that store entities and relationships between entities. You don't need to modify your existing workflows or replicate your data to use it in graph queries. A graph is a logical layer on top of your existing data and it respects the [column-level access control](https://docs.cloud.google.com/bigquery/docs/column-level-security-intro) , [data masking](https://docs.cloud.google.com/bigquery/docs/column-data-masking-intro) , and [row-level security](https://docs.cloud.google.com/bigquery/docs/row-level-security-intro) of the underlying tables.

BigQuery Graph supports a graph query interface compatible with the [ISO GQL standard](https://www.iso.org/standard/76120.html) and the [ISO Property Graph Queries (SQL/PGQ) standard](https://www.iso.org/standard/79473.html) . This provides you with interoperability between relational and graph models by combining well-established SQL capabilities with the expressiveness of graph pattern matching.

## Benefits of BigQuery Graph

Graphs are a natural way to represent relationships in data. Graph databases are used for fraud detection, recommendations, community detection, knowledge graphs, customer profiles, data cataloging, and lineage tracking.

When your graph data is represented as tables, you must perform self joins or recursive joins to traverse your data. Expressing graph traversal logic in SQL leads to complex queries that are difficult to write, maintain, and debug. BigQuery Graph lets you navigate relationships and identify patterns in your graph data in a more intuitive way.

## Key capabilities

- **Built-in graph experience** . The ISO GQL interface offers a familiar, purpose-built graph experience that's based on open standards.

- **Unified relational and graph** . Full interoperability between graph queries and SQL breaks down data silos and lets you choose the optimal tool for each use case, without any operational overhead to extract, transform, and load (ETL).

- **Built-in search capabilities** . Rich vector and full-text search capabilities integrate with graph, letting you use semantic meaning and keywords in graph analysis.

- **Graph visualization** . Graph query results are displayed in a visually appealing graph format that makes data exploration, investigation, and explanation much easier.

- **Performance and scalability** . Graph workloads are powered by BigQuery's scalable, cost-effective and distributed analytics engine.

- **Integration with Spanner Graph** . BigQuery Graph and [Spanner Graph](https://docs.cloud.google.com/spanner/docs/graph/overview) share the same graph schema and query language. You can execute operational graph workloads in Spanner and run complex graph analytics in BigQuery without needing to remodel your data or translate your queries.

- **Integration with the BigQuery MCP server** . You can connect Gemini Enterprise Agent Platform to BigQuery Graph using the [MCP server](https://docs.cloud.google.com/bigquery/docs/use-bigquery-mcp) or [publish](https://docs.cloud.google.com/bigquery/docs/create-data-agents#publish-agent-gemini-enterprise) your data agent to Agent Platform directly.

- **Integration with the Google Cloud Data Agent Kit extension** . Build and query your graphs using the [Google Cloud Data Agent Kit](https://docs.cloud.google.com/data-agent-kit/overview) .

- **Trace agent decisions** . Use BigQuery agent analytics to build a [context graph](https://adk.dev/integrations/bigquery-agent-analytics/#context-graph) , which is a queryable graph of your agent's decisions including requests handled, options weighed, and outcomes chosen.

- **Query using natural language** . Ask questions about your graph using [conversational analytics](https://docs.cloud.google.com/bigquery/docs/conversational-analytics#graphs) . Agents can write SQL and GQL queries and provide visualizations of your output. Agents can also use descriptions, synonyms, and [measures](https://docs.cloud.google.com/bigquery/docs/graph-measures) defined on your graph to improve the quality of the results. To try chatting with an agent about a graph, use the `Look Graph` sample agent on the BigQuery on the [Agents page](https://console.cloud.google.com/bigquery/agents_hub) to ask questions about the [`bigquery-public-data.thelook_ecommerce.graph`](https://console.cloud.google.com/bigquery?ws=!1m5!1m4!18m3!1sbigquery-public-data!2sthelook_ecommerce!3sgraph) graph.

### Use cases

You can use BigQuery Graph to build many types of analytic graph workloads, including the following:

- **Financial fraud detection** . Analyze complex relationships among users, accounts, and transactions to identify suspicious patterns and anomalies, such as money laundering and irregular connections between entities, which can be difficult to detect using relational databases.

- **Customer profiles** . Track customer relationships, preferences, and purchase histories. Gain a holistic understanding of each customer to enable personalized recommendations, targeted marketing campaigns, and improved customer service experiences.

- **Social networks** . Capture user activities and interactions and use graph pattern matching for friend recommendations and content discovery.

- **Manufacturing and supply chain management** . Use graph patterns for efficient impact analysis, cost rollups, and compliance checks by modeling parts, suppliers, orders, availability, and defects in the graph.

- **Healthcare** . Capture patient relationships, conditions, diagnosis, and treatments to facilitate patient similarity analysis and treatment planning.

- **Transportation** . Model places, connections, distances, and costs in the graph, and then use graph queries to find the optimal route.

## How BigQuery Graph and Spanner Graph work together

BigQuery Graph is designed for analytical graph workloads, focusing on deep analysis at scale. It's optimized for uncovering global patterns, identifying historical trends, and scanning petabytes of data using parallel processing. If your application requires real-time operations, predictable millisecond latency, or k-hop queries starting from a single node (such as live fraud detection or serving live recommendations), use [Spanner Graph](https://docs.cloud.google.com/spanner/docs/graph/overview) instead.

BigQuery Graph and Spanner Graph work together to provide a comprehensive solution. The following customer 360 use case describes how they complement each other:

1.  **Gather real-time insights** . A customer service agent uses Spanner Graph to handle user complaints about shipping the wrong product based on real-time purchase and delivery statistics.
2.  **Replicate or query data** . You can replicate data from Spanner to BigQuery by using [Spanner Change Streams](https://docs.cloud.google.com/spanner/docs/change-streams) without complex extract, transform, and load (ETL) operations, or query Spanner data directly from BigQuery by using [BigQuery federated queries](https://docs.cloud.google.com/bigquery/docs/federated-queries-intro) .
3.  **Analyze patterns** . A data scientist uses BigQuery Graph to identify a "churn hotspot" on that same data to label the customer as "at risk".
4.  **Improve feedback loop** . The "at-risk" labels are pushed to Spanner Graph with reverse ETL support to generate a coupon code for this customer to prevent churn.

### Move data between BigQuery Graph and Spanner Graph

You can move data between Spanner Graph and BigQuery Graph to suit your workload requirements:

- **Forward ETL** . To move data from Spanner to BigQuery for analytical queries, use a [Dataflow template](https://docs.cloud.google.com/dataflow/docs/guides/templates/provided/cloud-spanner-to-bigquery) .

- **Reverse ETL** . While you can query Spanner data directly from BigQuery Graph, there might be scenarios where you need to bring BigQuery data into Spanner Graph. Use the [`EXPORT DATA`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/export-statements#export_data_statement) SQL statement. For more details, see [Understand the reverse ETL pipeline](https://docs.cloud.google.com/spanner/docs/graph/reverse-etl#reverse-etl-pipeline) .

## Tutorials

The following tutorials show how to use BigQuery Graph in different scenarios:

- [Fraud detection with BigQuery Graph](https://codelabs.developers.google.com/codelabs/fraud-bigquery-graph)
- [Build customer 360 recommendations with BigQuery Graph](https://codelabs.developers.google.com/codelabs/c360-bigquery-graph)
- [Supply chain traceability with BigQuery Graph](https://codelabs.developers.google.com/codelabs/supplychaingraph)
- [Spanner & BigQuery: Real-Time Fraud Defense Shield](https://codelabs.developers.google.com/next26/spanner-bigquery-graph)
- [Perform semantic search on a graph](https://docs.cloud.google.com/bigquery/docs/graph-search)
- [Analyze drug interactions with BigQuery Graph](https://codelabs.developers.google.com/codelabs/drug-interaction-bigquery-graph)
- [Anti-money laundering & fraud prevention with BigQuery GraphRAG](https://codelabs.developers.google.com/codelabs/graphrag-with-bigquery)
- [Customer identity resolution with BigQuery Graph](https://codelabs.developers.google.com/codelabs/identity-resolution-bigquery-graph)
- [Trace AI agent decisions with BigQuery Graph](https://codelabs.developers.google.com/bqaa-context-graph)

## Pricing

To run GQL queries, you must use on-demand pricing or have a [reservation](https://docs.cloud.google.com/bigquery/docs/reservations-workload-management) that uses the [Enterprise or Enterprise Plus edition](https://docs.cloud.google.com/bigquery/docs/editions-intro) .

### Storage

You are charged only once for the storage of the underlying tables used to define your graphs. Storage costs follow the standard [BigQuery storage pricing](https://cloud.google.com/bigquery/pricing#storage-pricing) (active or long-term storage), regardless of how many graph models are built on top of those tables.

## What's next

- Learn how to [create and query a graph](https://docs.cloud.google.com/bigquery/docs/graph-create) .
- Learn about [graph schemas](https://docs.cloud.google.com/bigquery/docs/graph-schema-overview) .
- Learn how to [write graph queries](https://docs.cloud.google.com/bigquery/docs/graph-query-overview) .
- Learn how to [visualize graphs](https://docs.cloud.google.com/bigquery/docs/graph-visualization) .
- Learn about the [differences between BigQuery Graph and Spanner Graph](https://docs.cloud.google.com/bigquery/docs/graph-compare) .
- Learn about the [Graph Query Language (GQL)](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/graph-intro) .
