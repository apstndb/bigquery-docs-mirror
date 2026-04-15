# Visualize graphs

> ****
> 
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

To request support or provide feedback for this feature, send an email to <bq-graph-preview-support@google.com> .

BigQuery Graph visualizations show the graph elements returned by a query or the elements of a graph schema. You can visualize graphs in a notebook environment, such as BigQuery Studio, [Google Colab](https://developers.google.com/colab) , or [Jupyter Notebook](https://jupyter.org/) .

A visualization helps you understand how data points (nodes) are connected (edges). While a table of hundreds of data points can be difficult to interpret, its graph visualization can reveal patterns, dependencies, and anomalies.

## Visualize query results and schemas in a notebook environment

You can visualize graph query results and graph schemas in notebook environments such as BigQuery Studio, Google Colab, and Jupyter Notebook. The visualization is implemented as an IPython Magics.

### Visualize graph query results

To visualize query results in a notebook, follow these steps:

1.  In a notebook cell, run the following command to install the latest BigQuery magics library:
    
        !pip install bigquery_magics==0.12.1

2.  In your notebook environment, ensure you have the BigQuery Graph client library installed.

3.  In a notebook cell, use the `%%bigquery --graph` magic command followed by your GQL query. The query must return graph elements in JSON format using the [`TO_JSON`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/json_functions#to_json) function. We recommend returning graph paths instead of individual nodes and edges. Returning paths provides the following benefits:
    
      - Paths contain complete data of nodes and edges. If you return individual nodes and edges, some intermediate nodes and edges in a complex query's visualization might not be available.
    
      - If you return paths, your `RETURN` statement is less complex than if you return individual nodes and edges.

4.  Run the cell. The visualization is displayed in the output area of the cell.

The following sample query finds a person, their accounts, and repaid loans, and then returns the results in a notebook:

    %%bigquery --graph
    GRAPH graph_db.FinGraph
    MATCH
      p = ((person:Person {name: "Dana"})-[own:Owns]->
      (account:Account)-[transfer:Transfers]->(acount2:Account)<-[own2:Owns]-(person2:Person))
    RETURN
      TO_JSON(p) AS path;

After you run a query, the output area displays the visualization. The detail panel shows a summary of node and edge labels with counts for each. Click a node or an edge to navigate the graph and view properties, neighbors, and connections. The following image shows properties, neighbors, and connections.

![Visualization of query results.](https://docs.cloud.google.com/static/bigquery/images/graph-transfer-visualization.png)

### Visualize a BigQuery Graph schema

A graph's structure, including its nodes, edges, labels, and properties, is defined by its schema, which maps data in BigQuery tables to graph elements. The graph definition is stored in a schema that you create using input tables.

You can visualize graphs that you create with a schema. Visualizing the schema helps you understand your graph's structure, including the types of nodes and edges it contains and their connections. This can be useful for complex graphs because it provides a clear view of relationships that might be hard to infer from the DDL statements that you used to create the graph. The following image shows an example of a graph schema visualization.

![Visualization of a graph schema.](https://docs.cloud.google.com/static/bigquery/images/graph-schema-visualization.png)

To see a visualization of a BigQuery Graph schema in a notebook, follow these steps:

1.  In a notebook cell, run the following command to install the BigQuery magics library:
    
        !pip install bigquery_magics==0.12.1

2.  In your notebook environment, ensure that you have the BigQuery Graph client library installed.

3.  In a notebook cell, use the `%%bigquery --graph` magic command followed by your GQL query. The query must return graph elements in JSON format using the [`TO_JSON`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/json_functions#to_json) function.

4.  Run the cell. The visualization is displayed in the output area of the cell.

5.  In the visualization output, click schema **Schema view** .

## Troubleshoot BigQuery Graph visualizations

The following information can help you troubleshoot and understand BigQuery Graph visualization issues and behavior.

### A visualization doesn't appear for a BigQuery Graph query

**Issue** : You run a BigQuery Graph query, but it appears only in table format.

**Possible cause** : The query doesn't return graph elements in JSON format.

For example, the following query can't be visualized because it returns property values instead of graph elements in JSON format:

    GRAPH graph_db.FinGraph
    MATCH (person:Person {name: "Dana"})-[owns:Owns]->(account:Account)
    RETURN owns.create_time, account.nick_name;

**Solution** :

Return graph elements in JSON format using [`TO_JSON`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/json_functions#to_json) . For more information, see [Visualize BigQuery Graph query results](https://docs.cloud.google.com/bigquery/docs/graph-visualization#visualization-results) .

### BigQuery Graph query results are partially visualized

**Issue** : A query result visualization shows only part of the query results.

**Possible cause** : The query returns more than 2 MB of data. A query visualization can display a maximum of 2 MB of data.

**Solution** : Simplify the query to return less than 2 MB of data.

### Some graph elements aren't displayed in a BigQuery Graph visualization

**Issue** : A visualization includes all returned nodes and edges, but some graph elements aren't displayed.

**Possible cause** : The query used to create the BigQuery Graph visualization returns individual nodes and edges instead of a graph path.

**Solution** : Update the query to return a graph path.

## What's next

  - Learn more about [BigQuery Graph](https://docs.cloud.google.com/bigquery/docs/graph-overview) .
  - Learn how to [create and query a graph](https://docs.cloud.google.com/bigquery/docs/graph-create) .
  - Learn about [graph visualization tools and integrations](https://docs.cloud.google.com/bigquery/docs/graph-visualization-integrations) .
