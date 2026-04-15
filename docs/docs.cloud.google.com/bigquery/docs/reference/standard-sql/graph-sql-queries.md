> **Preview**
> 
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://cloud.google.com/terms/service-terms) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products#product-launch-stages) .

> **Note:** To provide feedback or request support for this feature, send an email to <bq-graph-preview-support@google.com> .

GoogleSQL for BigQuery supports the following syntax to use GQL within SQL queries.

## Language list

| Name                                                                                                                                | Summary                                                                                                          |
| ----------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| [`GRAPH_TABLE` operator](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/graph-sql-queries#graph_table_operator) | Performs an operation on a graph in the `FROM` clause of a SQL query and then produces a table with the results. |

## `GRAPH_TABLE` operator

    FROM GRAPH_TABLE (
      property_graph_name
      multi_linear_query_statement
    ) [ [ AS ] alias ]

#### Description

Performs an operation on a graph in the `FROM` clause of a SQL query and then produces a table with the results.

With the `GRAPH_TABLE` operator, you can use the [GQL syntax](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/graph-query-statements) to query a property graph. The result of this operation is produced as a table that you can use in the rest of the query.

#### Definitions

  - `property_graph_name` : The name of the property graph to query for patterns.
  - `multi_linear_query_statement` : You can use GQL to query a property graph for patterns. For more information, see [Graph query language](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/graph-query-statements) .
  - `alias` : An optional alias, which you can use to refer to the table produced by the `GRAPH_TABLE` operator elsewhere in the query.

#### Examples

> **Note:** The examples in this section reference a property graph called [`FinGraph`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/graph-schema-statements#fin_graph) .

You can use the `RETURN` statement to return specific node and edge properties. For example:

    SELECT name, id
    FROM GRAPH_TABLE(
      graph_db.FinGraph
      MATCH (n:Person)
      RETURN n.name AS name, n.id AS id
    );
    
    /*-----------+
     | name | id |
     +-----------+
     | Alex | 1  |
     | Dana | 2  |
     | Lee  | 3  |
     +-----------*/

The following query produces an error because `id` isn't included in the `RETURN` statement, even though this property exists for element `n` :

    SELECT name, id
    FROM GRAPH_TABLE(
      graph_db.FinGraph
      MATCH (n:Person)
      RETURN n.name
    );

The following query produces an error because directly outputting the graph element `n` is not supported. Convert `n` to its JSON representation using the `TO_JSON` function for successful output.

    -- Error
    SELECT n
    FROM GRAPH_TABLE(
      graph_db.FinGraph
      MATCH (n:Person)
      RETURN n
    );

    SELECT TO_JSON(n) as json_node
    FROM GRAPH_TABLE(
      graph_db.FinGraph
      MATCH (n:Person)
      RETURN n
    );
    
    /*---------------------------+
     | json_node                 |
     +---------------------------+
     | {"identifier":"mUZpbk...} |
     | {"identifier":"mUZpbk...} |
     | {"identifier":"mUZpbk...} |
     +--------------------------*/
