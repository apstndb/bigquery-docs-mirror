## Tool: `check_valid_creds`

Check for valid credentials for a data source.

The following example shows a MCP call to check for valid credentials for a data source with the ID `data_source_id` in the project `myproject` in the location `myregion` .

If the location isn't explicitly specified, and it can't be determined from the resources in the request, then the [default location](https://docs.cloud.google.com/bigquery/docs/locations#default_location) is used. If the default location isn't set, then the job runs in the `US` multi-region.

If `has_valid_creds` is true, then the credentials are valid. Otherwise, the credentials are not valid.

`check_valid_creds(project_id="myproject", location="myregion", data_source_id="mydatasource")`

The following sample demonstrate how to use `curl` to invoke the `check_valid_creds` MCP tool.

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
<td><pre dir="ltr" data-is-upgraded="" data-syntax="Bash" translate="no"><code>                  
curl --location &#39;https://bigquerydatatransfer.googleapis.com/mcp&#39; \
--header &#39;content-type: application/json&#39; \
--header &#39;accept: application/json, text/event-stream&#39; \
--data &#39;{
  &quot;method&quot;: &quot;tools/call&quot;,
  &quot;params&quot;: {
    &quot;name&quot;: &quot;check_valid_creds&quot;,
    &quot;arguments&quot;: {
      // provide these details according to the tool&#39;s MCP specification
    }
  },
  &quot;jsonrpc&quot;: &quot;2.0&quot;,
  &quot;id&quot;: 1
}&#39;
                </code></pre></td>
</tr>
</tbody>
</table>

## Input Schema

A request to determine whether the user has valid credentials. This method is used to limit the number of OAuth popups in the user interface. The user id is inferred from the API call context. If the data source has the Google+ authorization type, this method returns false, as it cannot be determined whether the credentials are already valid merely based on the user id.

### CheckValidCredsRequest

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;name&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Required. The name of the data source. If you are using the regionless method, the location must be `US` and the name should be in the following form:

  - `projects/{project_id}/dataSources/{data_source_id}`

If you are using the regionalized method, the name should be in the following form:

  - `projects/{project_id}/locations/{location_id}/dataSources/{data_source_id}`

## Output Schema

A response indicating whether the credentials exist and are valid.

### CheckValidCredsResponse

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;hasValidCreds&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`hasValidCreds`

`boolean`

If set to `true` , the credentials exist and are valid.

### Tool Annotations

Destructive Hint: ❌ | Idempotent Hint: ✅ | Read Only Hint: ✅ | Open World Hint: ❌
