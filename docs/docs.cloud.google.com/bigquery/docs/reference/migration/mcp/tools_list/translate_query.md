## Tool: `translate_query`

Translates a single query into BigQuery SQL syntax.

The following sample demonstrate how to use `curl` to invoke the `translate_query` MCP tool.

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
curl --location &#39;https://bigquerymigration.googleapis.com/mcp&#39; \
--header &#39;content-type: application/json&#39; \
--header &#39;accept: application/json, text/event-stream&#39; \
--data &#39;{
  &quot;method&quot;: &quot;tools/call&quot;,
  &quot;params&quot;: {
    &quot;name&quot;: &quot;translate_query&quot;,
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

Request message for `TranslateQuery` .

### TranslateQueryRequest

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
  &quot;parent&quot;: string,
  &quot;inputQuery&quot;: string,
  &quot;sourceDialect&quot;: string,
  &quot;metadataFilePath&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`parent`

`string`

Required. The parent resource name where the translation is performed. Format: `projects/PROJECT_ID/locations/LOCATION` . For more information, see [Locations](https://cloud.google.com/bigquery/docs/interactive-sql-translator#locations) . Note: If you're using an AI client, users should provide the project number and location if they aren't configured.

`inputQuery`

`string`

Required. The query string to be translated.

`sourceDialect`

`string`

Required. The dialect of the source query. Supported dialects are Teradata, Bteq, Redshift, Oracle, HiveQL, Impala, SparkSQL, Snowflake, Netezza, AzureSynapse, Vertica, SQLServer, Presto, MySQL, Postgresql, BigQuery, Db2, Greenplum, and SQLite.

`metadataFilePath`

`string`

Optional. The path to the metadata file in Cloud Storage. Format: `gs://BUCKET_NAME/PATH_TO_FILE.zip` . The metadata file contains information about the source database and its schema. For more information on generating a metadata file, see [Generate metadata](https://cloud.google.com/bigquery/docs/generate-metadata) . Translation may fail if the metadata file isn't generated correctly.

## Output Schema

Response message for `TranslateQuery` .

### TranslateQueryResponse

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;translatedQuery&quot;: string,&quot;translationId&quot;: string,&quot;translationState&quot;: string,&quot;translationLogs&quot;: [{object (Log)}],&quot;errorInfo&quot;: {object (ErrorInfo)}}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`translatedQuery`

`string`

The translated query.

`translationId`

`string`

The ID of the migration workflow created for this translation. Use this ID as the name for `get_translation` , `explain_translation` , and `generate_ddl` tools.

`translationState`

`string`

The current state of the translation, for example, `SUCCEEDED` or `FAILED` .

`translationLogs[]`

` object ( Log  ` )

A list of logs generated during the translation process. Tip: If you're using an AI client, these logs can be used to troubleshoot issues and to improve translation quality. You should persist these logs so users can see them in the UI and use them for troubleshooting or improving translation quality.

`errorInfo`

` object ( ErrorInfo  ` )

The error information.

### Log

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
  &quot;severity&quot;: string,
  &quot;category&quot;: string,
  &quot;message&quot;: string,
  &quot;action&quot;: string,
  &quot;effect&quot;: string,
  &quot;impactedObject&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`severity`

`string`

Severity of the translation record, for example, `INFO` , `WARNING` , or `ERROR` .

`category`

`string`

Category of the error or warning, for example, `SyntaxError` .

`message`

`string`

Detailed message of the record.

`action`

`string`

Recommended action to address the log.

`effect`

`string`

The effect or impact of the issue noted in the log. Effect can be one of the following values: `CORRECTNESS` : Errors with this effect indicate that the translation service couldn't meaningfully process the translation. This is caused by issues in the user's input such as incorrect language or formatting, or using an unsupported file type. `COMPLETENESS` : Errors with this effect indicate that the translation service doesn't have sufficient information to complete the translation. This can be caused by missing information in the user's input such as missing metadata for name resolution. `COMPATIBILITY` : Errors with this effect indicate that the translation service encountered compatibility issues when it processed the translation. This can happen when the target platform doesn't support a feature used in the input script, and the translation service tries to make a semantic approximation for the target platform. `NONE` : Errors with this effect are purely informational messages that have no effect on the output. Effects are ordered by their stage in the translation process. For example, `CORRECTNESS` issues are identified before `COMPLETENESS` issues.

`impactedObject`

`string`

Name of the object that is impacted by the log message.

### ErrorInfo

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
  &quot;reason&quot;: string,
  &quot;domain&quot;: string,
  &quot;metadata&quot;: {
    string: string,
    ...
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`reason`

`string`

The reason of the error. This is a constant value that identifies the proximate cause of the error. Error reasons are unique within a particular domain of errors. This should be at most 63 characters and match a regular expression of `[A-Z][A-Z0-9_]+[A-Z0-9]` , which represents UPPER\_SNAKE\_CASE.

`domain`

`string`

The logical grouping to which the "reason" belongs. The error domain is typically the registered service name of the tool or product that generates the error. Example: "pubsub.googleapis.com". If the error is generated by some common infrastructure, the error domain must be a globally unique value that identifies the infrastructure. For Google API infrastructure, the error domain is "googleapis.com".

`metadata`

`map (key: string, value: string)`

Additional structured details about this error.

Keys must match a regular expression of `[a-z][a-zA-Z0-9-_]+` but should ideally be lowerCamelCase. Also, they must be limited to 64 characters in length. When identifying the current value of an exceeded limit, the units should be contained in the key, not the value. For example, rather than `{"instanceLimit": "100/request"}` , should be returned as, `{"instanceLimitPerRequest": "100"}` , if the client exceeds the number of instances that can be created in a single (batch) request.

An object containing a list of `"key": value` pairs. Example: `{ "name": "wrench", "mass": "1.3kg", "count": "3" }` .

### MetadataEntry

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
  &quot;key&quot;: string,
  &quot;value&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`key`

`string`

`value`

`string`

### Tool Annotations

Destructive Hint: ❌ | Idempotent Hint: ❌ | Read Only Hint: ❌ | Open World Hint: ❌
