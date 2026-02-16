  - [JSON representation](#SCHEMA_REPRESENTATION)

A connection-level property to customize query behavior. Under JDBC, these correspond directly to connection properties passed to the DriverManager. Under ODBC, these correspond to properties in the connection string.

Currently supported connection properties:

  - **dataset\_project\_id** : represents the default project for datasets that are used in the query. Setting the system variable `  @@dataset_project_id  ` achieves the same behavior. For more information about system variables, see: <https://cloud.google.com/bigquery/docs/reference/system-variables>

  - **time\_zone** : represents the default timezone used to run the query.

  - **session\_id** : associates the query with a given session.

  - **query\_label** : associates the query with a given job label. If set, all subsequent queries in a script or session will have this label. For the format in which a you can specify a query label, see labels in the JobConfiguration resource type: <https://cloud.google.com/bigquery/docs/reference/rest/v2/Job#jobconfiguration>

  - **service\_account** : indicates the service account to use to run a continuous query. If set, the query job uses the service account to access Google Cloud resources. Service account access is bounded by the IAM permissions that you have granted to the service account.

Additional properties are allowed, but ignored. Specifying multiple connection properties with the same key returns an error.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;key&quot;: string,
  &quot;value&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  key  `

`  string  `

The key of the property to set.

`  value  `

`  string  `

The value of the property to set.
