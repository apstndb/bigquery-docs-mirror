  - [JSON representation](#SCHEMA_REPRESENTATION)

A job reference is a fully qualified identifier for referring to a job.

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
  &quot;projectId&quot;: string,
  &quot;jobId&quot;: string,
  &quot;location&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  projectId  `

`  string  `

Required. The ID of the project containing this job.

`  jobId  `

`  string  `

Required. The ID of the job. The ID must contain only letters (a-z, A-Z), numbers (0-9), underscores (\_), or dashes (-). The maximum length is 1,024 characters.

`  location  `

`  string  `

Optional. The geographic location of the job. The default value is US.

For more information about BigQuery locations, see: <https://cloud.google.com/bigquery/docs/locations>
