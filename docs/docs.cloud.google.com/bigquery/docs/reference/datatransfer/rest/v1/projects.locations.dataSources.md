  - [Resource: DataSource](#DataSource)
      - [JSON representation](#DataSource.SCHEMA_REPRESENTATION)
  - [Methods](#METHODS_SUMMARY)

## Resource: DataSource

Defines the properties and custom parameters for a data source.

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
  &quot;name&quot;: string,
  &quot;dataSourceId&quot;: string,
  &quot;displayName&quot;: string,
  &quot;description&quot;: string,
  &quot;clientId&quot;: string,
  &quot;scopes&quot;: [
    string
  ],
  &quot;transferType&quot;: enum (TransferType),
  &quot;supportsMultipleTransfers&quot;: boolean,
  &quot;updateDeadlineSeconds&quot;: integer,
  &quot;defaultSchedule&quot;: string,
  &quot;supportsCustomSchedule&quot;: boolean,
  &quot;parameters&quot;: [
    {
      object (DataSourceParameter)
    }
  ],
  &quot;helpUrl&quot;: string,
  &quot;authorizationType&quot;: enum (AuthorizationType),
  &quot;dataRefreshType&quot;: enum (DataRefreshType),
  &quot;defaultDataRefreshWindowDays&quot;: integer,
  &quot;manualRunsDisabled&quot;: boolean,
  &quot;minimumScheduleInterval&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  name  `

`  string  `

Output only. Data source resource name.

`  dataSourceId  `

`  string  `

Data source id.

`  displayName  `

`  string  `

User friendly data source name.

`  description  `

`  string  `

User friendly data source description string.

`  clientId  `

`  string  `

Data source client id which should be used to receive refresh token.

`  scopes[]  `

`  string  `

Api auth scopes for which refresh token needs to be obtained. These are scopes needed by a data source to prepare data and ingest them into BigQuery, e.g., <https://www.googleapis.com/auth/bigquery>

`  transferType (deprecated)  `

`  enum ( TransferType  ` )

This item is deprecated\!

Deprecated. This field has no effect.

`  supportsMultipleTransfers (deprecated)  `

`  boolean  `

This item is deprecated\!

Deprecated. This field has no effect.

`  updateDeadlineSeconds  `

`  integer  `

The number of seconds to wait for an update from the data source before the Data Transfer Service marks the transfer as FAILED.

`  defaultSchedule  `

`  string  `

Default data transfer schedule. Examples of valid schedules include: `  1st,3rd monday of month 15:30  ` , `  every wed,fri of jan,jun 13:15  ` , and `  first sunday of quarter 00:00  ` .

`  supportsCustomSchedule  `

`  boolean  `

Specifies whether the data source supports a user defined schedule, or operates on the default schedule. When set to `  true  ` , user can override default schedule.

`  parameters[]  `

`  object ( DataSourceParameter  ` )

Data source parameters.

`  helpUrl  `

`  string  `

Url for the help document for this data source.

`  authorizationType  `

`  enum ( AuthorizationType  ` )

Indicates the type of authorization.

`  dataRefreshType  `

`  enum ( DataRefreshType  ` )

Specifies whether the data source supports automatic data refresh for the past few days, and how it's supported. For some data sources, data might not be complete until a few days later, so it's useful to refresh data automatically.

`  defaultDataRefreshWindowDays  `

`  integer  `

Default data refresh window on days. Only meaningful when `  dataRefreshType  ` = `  SLIDING_WINDOW  ` .

`  manualRunsDisabled  `

`  boolean  `

Disables backfilling and manual run scheduling for the data source.

`  minimumScheduleInterval  `

`  string ( Duration  ` format)

The minimum interval for scheduler to schedule runs.

A duration in seconds with up to nine fractional digits, ending with ' `  s  ` '. Example: `  "3.5s"  ` .

## Methods

### `             checkValidCreds           `

Returns true if valid credentials exist for the given data source and requesting user.

### `             get           `

Retrieves a supported data source and returns its settings.

### `             list           `

Lists supported data sources and returns their settings.
