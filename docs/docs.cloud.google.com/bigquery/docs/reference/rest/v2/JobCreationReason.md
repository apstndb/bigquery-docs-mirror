  - [JSON representation](#SCHEMA_REPRESENTATION)
  - [Code](#Code)

Reason about why a Job was created from a [`  jobs.query  `](https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query) method when used with `  JOB_CREATION_OPTIONAL  ` Job creation mode.

For [`  jobs.insert  `](https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/insert) method calls it will always be `  REQUESTED  ` .

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
  &quot;code&quot;: enum (Code)
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  code  `

`  enum ( Code  ` )

Output only. Specifies the high level reason why a Job was created.

## Code

Indicates the high level reason why a job was created.

Enums

`  CODE_UNSPECIFIED  `

Reason is not specified.

`  REQUESTED  `

Job creation was requested.

`  LONG_RUNNING  `

The query request ran beyond a system defined timeout specified by the [timeoutMs field in the QueryRequest](https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query#queryrequest) . As a result it was considered a long running operation for which a job was created.

`  LARGE_RESULTS  `

The results from the query cannot fit in the response.

`  OTHER  `

BigQuery has determined that the query needs to be executed as a Job.
