## Get MCP tool specifications

To get the MCP tool specifications for all tools in an MCP server, use the `  tools/list  ` method. The following example demonstrates how to use `  curl  ` to list all tools and their specifications currently available within the MCP server.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>Curl Request</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" data-syntax="Bash" translate="no"><code>                    
curl --location &#39;https://bigquery.googleapis.com/mcp&#39; \
--header &#39;content-type: application/json&#39; \
--header &#39;accept: application/json, text/event-stream&#39; \
--data &#39;{
    &quot;method&quot;: &quot;tools/list&quot;,
    &quot;jsonrpc&quot;: &quot;2.0&quot;,
    &quot;id&quot;: 1
}&#39;
                  </code></pre></td>
</tr>
</tbody>
</table>

MCP Tools

[list\_dataset\_ids](/bigquery/docs/reference/mcp/list_dataset_ids)

List BigQuery dataset IDs in a Google Cloud project.

[get\_dataset\_info](/bigquery/docs/reference/mcp/get_dataset_info)

Get metadata information about a BigQuery dataset.

[list\_table\_ids](/bigquery/docs/reference/mcp/list_table_ids)

List table ids in a BigQuery dataset.

[get\_table\_info](/bigquery/docs/reference/mcp/get_table_info)

Get metadata information about a BigQuery table.

[execute\_sql](/bigquery/docs/reference/mcp/execute_sql)

Run a SQL query in the project and return the result.

This tool is restricted to only `  SELECT  ` statements. `  INSERT  ` , `  UPDATE  ` , and `  DELETE  ` statements and stored procedures aren't allowed. If the query doesn't include a `  SELECT  ` statement, an error is returned. For information on creating queries, see the [GoogleSQL documentation](https://cloud.google.com/bigquery/docs/reference/standard-sql/query-syntax) .

The `  execute_sql  ` tool can also have side effects if the the query invokes [remote functions](https://cloud.google.com/bigquery/docs/remote-functions) or [Python UDFs](https://cloud.google.com/bigquery/docs/user-defined-functions-python) .

All queries that are run using the `  execute_sql  ` tool have a label that identifies the tool as the source. You can use this label to filter the queries using the label and value pair `  goog-mcp-server: true  ` .

Queries are charged to the project specified in the `  project_id  ` field.
