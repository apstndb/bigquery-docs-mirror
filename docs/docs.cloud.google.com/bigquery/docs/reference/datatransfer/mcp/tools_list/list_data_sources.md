## Tool: `list_data_sources`

List all the data sources that the project has access to.

The following example shows a MCP call to list all data sources in the project `myproject` in the location `myregion` .

If the location isn't explicitly specified, and it can't be determined from the resources in the request, then the [default location](https://docs.cloud.google.com/bigquery/docs/locations#default_location) is used. If the default location isn't set, then the job runs in the `US` multi-region.

`list_data_sources(project_id="myproject", location="myregion")`

The following sample demonstrate how to use `curl` to invoke the `list_data_sources` MCP tool.

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
    &quot;name&quot;: &quot;list_data_sources&quot;,
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

Request for listing data sources.

### ListDataSourcesRequest

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
  &quot;projectId&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`projectId`

`string`

Required. Project ID or project number.

## Output Schema

Response for listing data sources.

### ListDataSourcesResponse

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;dataSources&quot;: [{object (DataSource)}]}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`dataSources[]`

` object ( DataSource  ` )

Data sources.

### DataSource

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;name&quot;: string,&quot;dataSourceId&quot;: string,&quot;displayName&quot;: string,&quot;description&quot;: string,&quot;clientId&quot;: string,&quot;scopes&quot;: [string],&quot;transferType&quot;: enum (TransferType),&quot;supportsMultipleTransfers&quot;: boolean,&quot;updateDeadlineSeconds&quot;: integer,&quot;defaultSchedule&quot;: string,&quot;supportsCustomSchedule&quot;: boolean,&quot;parameters&quot;: [{object (DataSourceParameter)}],&quot;helpUrl&quot;: string,&quot;authorizationType&quot;: enum (AuthorizationType),&quot;dataRefreshType&quot;: enum (DataRefreshType),&quot;defaultDataRefreshWindowDays&quot;: integer,&quot;manualRunsDisabled&quot;: boolean,&quot;minimumScheduleInterval&quot;: string}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`name`

`string`

Output only. Data source resource name.

`dataSourceId`

`string`

Data source id.

`displayName`

`string`

User friendly data source name.

`description`

`string`

User friendly data source description string.

`clientId`

`string`

Data source client id which should be used to receive refresh token.

`scopes[]`

`string`

Api auth scopes for which refresh token needs to be obtained. These are scopes needed by a data source to prepare data and ingest them into BigQuery, e.g., <https://www.googleapis.com/auth/bigquery>

` transferType (deprecated)  `

`enum ( TransferType` )

This item is deprecated\!

Deprecated. This field has no effect.

` supportsMultipleTransfers (deprecated)  `

`boolean`

This item is deprecated\!

Deprecated. This field has no effect.

`updateDeadlineSeconds`

`integer`

The number of seconds to wait for an update from the data source before the Data Transfer Service marks the transfer as FAILED.

`defaultSchedule`

`string`

Default data transfer schedule. Examples of valid schedules include: `1st,3rd monday of month 15:30` , `every wed,fri of jan,jun 13:15` , and `first sunday of quarter 00:00` .

`supportsCustomSchedule`

`boolean`

Specifies whether the data source supports a user defined schedule, or operates on the default schedule. When set to `true` , user can override default schedule.

`parameters[]`

` object ( DataSourceParameter  ` )

Data source parameters.

`helpUrl`

`string`

Url for the help document for this data source.

`authorizationType`

`enum ( AuthorizationType` )

Indicates the type of authorization.

`dataRefreshType`

`enum ( DataRefreshType` )

Specifies whether the data source supports automatic data refresh for the past few days, and how it's supported. For some data sources, data might not be complete until a few days later, so it's useful to refresh data automatically.

`defaultDataRefreshWindowDays`

`integer`

Default data refresh window on days. Only meaningful when `data_refresh_type` = `SLIDING_WINDOW` .

`manualRunsDisabled`

`boolean`

Disables backfilling and manual run scheduling for the data source.

`minimumScheduleInterval`

` string ( Duration  ` format)

The minimum interval for scheduler to schedule runs.

A duration in seconds with up to nine fractional digits, ending with ' `s` '. Example: `"3.5s"` .

### DataSourceParameter

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
<td><pre dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{&quot;paramId&quot;: string,&quot;displayName&quot;: string,&quot;description&quot;: string,&quot;type&quot;: enum (Type),&quot;required&quot;: boolean,&quot;repeated&quot;: boolean,&quot;validationRegex&quot;: string,&quot;allowedValues&quot;: [string],&quot;minValue&quot;: number,&quot;maxValue&quot;: number,&quot;fields&quot;: [{object (DataSourceParameter)}],&quot;validationDescription&quot;: string,&quot;validationHelpUrl&quot;: string,&quot;immutable&quot;: boolean,&quot;recurse&quot;: boolean,&quot;deprecated&quot;: boolean,// Union field _max_list_size can be only one of the following:&quot;maxListSize&quot;: string// End of list of possible types for union field _max_list_size.}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`paramId`

`string`

Parameter identifier.

`displayName`

`string`

Parameter display name in the user interface.

`description`

`string`

Parameter description.

`type`

`enum ( Type` )

Parameter type.

`required`

`boolean`

Is parameter required.

`repeated`

`boolean`

Deprecated. This field has no effect.

`validationRegex`

`string`

Regular expression which can be used for parameter validation.

`allowedValues[]`

`string`

All possible values for the parameter.

`minValue`

`number`

For integer and double values specifies minimum allowed value.

`maxValue`

`number`

For integer and double values specifies maximum allowed value.

`fields[]`

` object ( DataSourceParameter  ` )

Deprecated. This field has no effect.

`validationDescription`

`string`

Description of the requirements for this field, in case the user input does not fulfill the regex pattern or min/max values.

`validationHelpUrl`

`string`

URL to a help document to further explain the naming requirements.

`immutable`

`boolean`

Cannot be changed after initial creation.

`recurse`

`boolean`

Deprecated. This field has no effect.

`deprecated`

`boolean`

If true, it should not be used in new transfers, and it should not be visible to users.

Union field `_max_list_size` .

`_max_list_size` can be only one of the following:

`maxListSize`

`string ( int64 format)`

For list parameters, the max size of the list.

### DoubleValue

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
  &quot;value&quot;: number
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`value`

`number`

The double value.

### Duration

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
  &quot;seconds&quot;: string,
  &quot;nanos&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`seconds`

`string ( int64 format)`

Signed seconds of the span of time. Must be from -315,576,000,000 to +315,576,000,000 inclusive. Note: these bounds are computed from: 60 sec/min \* 60 min/hr \* 24 hr/day \* 365.25 days/year \* 10000 years

`nanos`

`integer`

Signed fractions of a second at nanosecond resolution of the span of time. Durations less than one second are represented with a 0 `seconds` field and a positive or negative `nanos` field. For durations of one second or more, a non-zero value for the `nanos` field must be of the same sign as the `seconds` field. Must be from -999,999,999 to +999,999,999 inclusive.

### Tool Annotations

Destructive Hint: ❌ | Idempotent Hint: ✅ | Read Only Hint: ✅ | Open World Hint: ❌
