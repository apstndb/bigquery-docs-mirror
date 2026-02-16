## Index

  - `  DataTransferService  ` (interface)
  - `  CheckValidCredsRequest  ` (message)
  - `  CheckValidCredsResponse  ` (message)
  - `  CreateTransferConfigRequest  ` (message)
  - `  DataSource  ` (message)
  - `  DataSource.AuthorizationType  ` (enum)
  - `  DataSource.DataRefreshType  ` (enum)
  - `  DataSourceParameter  ` (message)
  - `  DataSourceParameter.Type  ` (enum)
  - `  DeleteTransferConfigRequest  ` (message)
  - `  DeleteTransferRunRequest  ` (message)
  - `  EmailPreferences  ` (message)
  - `  EncryptionConfiguration  ` (message)
  - `  EnrollDataSourcesRequest  ` (message)
  - `  EventDrivenSchedule  ` (message)
  - `  GetDataSourceRequest  ` (message)
  - `  GetTransferConfigRequest  ` (message)
  - `  GetTransferRunRequest  ` (message)
  - `  ListDataSourcesRequest  ` (message)
  - `  ListDataSourcesResponse  ` (message)
  - `  ListTransferConfigsRequest  ` (message)
  - `  ListTransferConfigsResponse  ` (message)
  - `  ListTransferLogsRequest  ` (message)
  - `  ListTransferLogsResponse  ` (message)
  - `  ListTransferRunsRequest  ` (message)
  - `  ListTransferRunsRequest.RunAttempt  ` (enum)
  - `  ListTransferRunsResponse  ` (message)
  - `  ManagedTableType  ` (enum)
  - `  ManualSchedule  ` (message)
  - `  ScheduleOptions  ` (message)
  - `  ScheduleOptionsV2  ` (message)
  - `  ScheduleTransferRunsRequest  ` (message)
  - `  ScheduleTransferRunsResponse  ` (message)
  - `  StartManualTransferRunsRequest  ` (message)
  - `  StartManualTransferRunsRequest.TimeRange  ` (message)
  - `  StartManualTransferRunsResponse  ` (message)
  - `  TimeBasedSchedule  ` (message)
  - `  TransferConfig  ` (message)
  - `  TransferMessage  ` (message)
  - `  TransferMessage.MessageSeverity  ` (enum)
  - `  TransferRun  ` (message)
  - `  TransferState  ` (enum)
  - `  TransferType  ` (enum) **(deprecated)**
  - `  UnenrollDataSourcesRequest  ` (message)
  - `  UpdateTransferConfigRequest  ` (message)
  - `  UserInfo  ` (message)

## DataTransferService

This API allows users to manage their data transfers into BigQuery.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>CheckValidCreds</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc CheckValidCreds(                         CheckValidCredsRequest            </code> ) returns ( <code dir="ltr" translate="no">              CheckValidCredsResponse            </code> )</p>
<p>Returns true if valid credentials exist for the given data source and requesting user.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>CreateTransferConfig</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc CreateTransferConfig(                         CreateTransferConfigRequest            </code> ) returns ( <code dir="ltr" translate="no">              TransferConfig            </code> )</p>
<p>Creates a new data transfer configuration.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>DeleteTransferConfig</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc DeleteTransferConfig(                         DeleteTransferConfigRequest            </code> ) returns ( <code dir="ltr" translate="no">              Empty            </code> )</p>
<p>Deletes a data transfer configuration, including any associated transfer runs and logs.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>DeleteTransferRun</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc DeleteTransferRun(                         DeleteTransferRunRequest            </code> ) returns ( <code dir="ltr" translate="no">              Empty            </code> )</p>
<p>Deletes the specified transfer run.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>EnrollDataSources</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc EnrollDataSources(                         EnrollDataSourcesRequest            </code> ) returns ( <code dir="ltr" translate="no">              Empty            </code> )</p>
<p>Enroll data sources in a user project. This allows users to create transfer configurations for these data sources. They will also appear in the ListDataSources RPC and as such, will appear in the <a href="https://console.cloud.google.com/bigquery">BigQuery UI</a> , and the documents can be found in the public guide for <a href="https://cloud.google.com/bigquery/bigquery-web-ui">BigQuery Web UI</a> and <a href="https://cloud.google.com/bigquery/docs/working-with-transfers">Data Transfer Service</a> .</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>GetDataSource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc GetDataSource(                         GetDataSourceRequest            </code> ) returns ( <code dir="ltr" translate="no">              DataSource            </code> )</p>
<p>Retrieves a supported data source and returns its settings.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>GetTransferConfig</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc GetTransferConfig(                         GetTransferConfigRequest            </code> ) returns ( <code dir="ltr" translate="no">              TransferConfig            </code> )</p>
<p>Returns information about a data transfer config.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>GetTransferRun</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc GetTransferRun(                         GetTransferRunRequest            </code> ) returns ( <code dir="ltr" translate="no">              TransferRun            </code> )</p>
<p>Returns information about the particular transfer run.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>ListDataSources</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc ListDataSources(                         ListDataSourcesRequest            </code> ) returns ( <code dir="ltr" translate="no">              ListDataSourcesResponse            </code> )</p>
<p>Lists supported data sources and returns their settings.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>ListTransferConfigs</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc ListTransferConfigs(                         ListTransferConfigsRequest            </code> ) returns ( <code dir="ltr" translate="no">              ListTransferConfigsResponse            </code> )</p>
<p>Returns information about all transfer configs owned by a project in the specified location.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>ListTransferLogs</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc ListTransferLogs(                         ListTransferLogsRequest            </code> ) returns ( <code dir="ltr" translate="no">              ListTransferLogsResponse            </code> )</p>
<p>Returns log messages for the transfer run.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>ListTransferRuns</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc ListTransferRuns(                         ListTransferRunsRequest            </code> ) returns ( <code dir="ltr" translate="no">              ListTransferRunsResponse            </code> )</p>
<p>Returns information about running and completed transfer runs.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>ScheduleTransferRuns</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>This item is deprecated!</p>
<p><code dir="ltr" translate="no">           rpc ScheduleTransferRuns(                         ScheduleTransferRunsRequest            </code> ) returns ( <code dir="ltr" translate="no">              ScheduleTransferRunsResponse            </code> )</p>
<p>Creates transfer runs for a time range [start_time, end_time]. For each date - or whatever granularity the data source supports - in the range, one transfer run is created. Note that runs are created per UTC time in the time range. DEPRECATED: use StartManualTransferRuns instead.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>StartManualTransferRuns</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc StartManualTransferRuns(                         StartManualTransferRunsRequest            </code> ) returns ( <code dir="ltr" translate="no">              StartManualTransferRunsResponse            </code> )</p>
<p>Manually initiates transfer runs. You can schedule these runs in two ways:</p>
<ol>
<li>For a specific point in time using the 'requested_run_time' parameter.</li>
<li>For a period between 'start_time' (inclusive) and 'end_time' (exclusive).</li>
</ol>
<p>If scheduling a single run, it is set to execute immediately (schedule_time equals the current time). When scheduling multiple runs within a time range, the first run starts now, and subsequent runs are delayed by 15 seconds each.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>UnenrollDataSources</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc UnenrollDataSources(                         UnenrollDataSourcesRequest            </code> ) returns ( <code dir="ltr" translate="no">              Empty            </code> )</p>
<p>Unenroll data sources in a user project. This allows users to remove transfer configurations for these data sources. They will no longer appear in the ListDataSources RPC and will also no longer appear in the <a href="https://console.cloud.google.com/bigquery">BigQuery UI</a> . Data transfers configurations of unenrolled data sources will not be scheduled.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>UpdateTransferConfig</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc UpdateTransferConfig(                         UpdateTransferConfigRequest            </code> ) returns ( <code dir="ltr" translate="no">              TransferConfig            </code> )</p>
<p>Updates a data transfer configuration. All fields must be set, even if they are not updated.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires the following OAuth scope:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

## CheckValidCredsRequest

A request to determine whether the user has valid credentials. This method is used to limit the number of OAuth popups in the user interface. The user id is inferred from the API call context. If the data source has the Google+ authorization type, this method returns false, as it cannot be determined whether the credentials are already valid merely based on the user id.

Fields

`  name  `

`  string  `

Required. The name of the data source. If you are using the regionless method, the location must be `  US  ` and the name should be in the following form:

  - `  projects/{project_id}/dataSources/{data_source_id}  `

If you are using the regionalized method, the name should be in the following form:

  - `  projects/{project_id}/locations/{location_id}/dataSources/{data_source_id}  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  name  ` :

  - `  bigquery.transfers.get  `

## CheckValidCredsResponse

A response indicating whether the credentials exist and are valid.

Fields

`  has_valid_creds  `

`  bool  `

If set to `  true  ` , the credentials exist and are valid.

## CreateTransferConfigRequest

A request to create a data transfer configuration. If new credentials are needed for this transfer configuration, authorization info must be provided. If authorization info is provided, the transfer configuration will be associated with the user id corresponding to the authorization info. Otherwise, the transfer configuration will be associated with the calling user.

When using a cross project service account for creating a transfer config, you must enable cross project service account usage. For more information, see [Disable attachment of service accounts to resources in other projects](https://cloud.google.com/resource-manager/docs/organization-policy/restricting-service-accounts#disable_cross_project_service_accounts) .

Fields

`  parent  `

`  string  `

Required. The BigQuery project id where the transfer configuration should be created. Must be in the format projects/{project\_id}/locations/{location\_id} or projects/{project\_id}. If specified location and location of the destination bigquery dataset do not match - the request will fail.

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  parent  ` :

  - `  bigquery.transfers.update  `

`  transfer_config  `

`  TransferConfig  `

Required. Data transfer configuration to create.

`  authorization_code (deprecated)  `

`  string  `

This item is deprecated\!

Deprecated: Authorization code was required when `  transferConfig.dataSourceId  ` is 'youtube\_channel' but it is no longer used in any data sources. Use `  version_info  ` instead.

Optional OAuth2 authorization code to use with this transfer configuration. This is required only if `  transferConfig.dataSourceId  ` is 'youtube\_channel' and new credentials are needed, as indicated by `  CheckValidCreds  ` . In order to obtain authorization\_code, make a request to the following URL:

``` text
https://bigquery.cloud.google.com/datatransfer/oauthz/auth?redirect_uri=urn:ietf:wg:oauth:2.0:oob&response_type=authorization_code&client_id=client_id&scope=data_source_scopes
```

  - The client\_id is the OAuth client\_id of the data source as returned by ListDataSources method.
  - data\_source\_scopes are the scopes returned by ListDataSources method.

Note that this should not be set when `  service_account_name  ` is used to create the transfer config.

`  version_info  `

`  string  `

Optional version info. This parameter replaces `  authorization_code  ` which is no longer used in any data sources. This is required only if `  transferConfig.dataSourceId  ` is 'youtube\_channel' *or* new credentials are needed, as indicated by `  CheckValidCreds  ` . In order to obtain version info, make a request to the following URL:

``` text
https://bigquery.cloud.google.com/datatransfer/oauthz/auth?redirect_uri=urn:ietf:wg:oauth:2.0:oob&response_type=version_info&client_id=client_id&scope=data_source_scopes
```

  - The client\_id is the OAuth client\_id of the data source as returned by ListDataSources method.
  - data\_source\_scopes are the scopes returned by ListDataSources method.

Note that this should not be set when `  service_account_name  ` is used to create the transfer config.

`  service_account_name  `

`  string  `

Optional service account email. If this field is set, the transfer config will be created with this service account's credentials. It requires that the requesting user calling this API has permissions to act as this service account.

Note that not all data sources support service account credentials when creating a transfer config. For the latest list of data sources, read about [using service accounts](https://cloud.google.com/bigquery-transfer/docs/use-service-accounts) .

## DataSource

Defines the properties and custom parameters for a data source.

Fields

`  name  `

`  string  `

Output only. Data source resource name.

`  data_source_id  `

`  string  `

Data source id.

`  display_name  `

`  string  `

User friendly data source name.

`  description  `

`  string  `

User friendly data source description string.

`  client_id  `

`  string  `

Data source client id which should be used to receive refresh token.

`  scopes[]  `

`  string  `

Api auth scopes for which refresh token needs to be obtained. These are scopes needed by a data source to prepare data and ingest them into BigQuery, e.g., <https://www.googleapis.com/auth/bigquery>

`  transfer_type (deprecated)  `

`  TransferType  `

This item is deprecated\!

Deprecated. This field has no effect.

`  supports_multiple_transfers (deprecated)  `

`  bool  `

This item is deprecated\!

Deprecated. This field has no effect.

`  update_deadline_seconds  `

`  int32  `

The number of seconds to wait for an update from the data source before the Data Transfer Service marks the transfer as FAILED.

`  default_schedule  `

`  string  `

Default data transfer schedule. Examples of valid schedules include: `  1st,3rd monday of month 15:30  ` , `  every wed,fri of jan,jun 13:15  ` , and `  first sunday of quarter 00:00  ` .

`  supports_custom_schedule  `

`  bool  `

Specifies whether the data source supports a user defined schedule, or operates on the default schedule. When set to `  true  ` , user can override default schedule.

`  parameters[]  `

`  DataSourceParameter  `

Data source parameters.

`  help_url  `

`  string  `

Url for the help document for this data source.

`  authorization_type  `

`  AuthorizationType  `

Indicates the type of authorization.

`  data_refresh_type  `

`  DataRefreshType  `

Specifies whether the data source supports automatic data refresh for the past few days, and how it's supported. For some data sources, data might not be complete until a few days later, so it's useful to refresh data automatically.

`  default_data_refresh_window_days  `

`  int32  `

Default data refresh window on days. Only meaningful when `  data_refresh_type  ` = `  SLIDING_WINDOW  ` .

`  manual_runs_disabled  `

`  bool  `

Disables backfilling and manual run scheduling for the data source.

`  minimum_schedule_interval  `

`  Duration  `

The minimum interval for scheduler to schedule runs.

## AuthorizationType

The type of authorization needed for this data source.

Enums

`  AUTHORIZATION_TYPE_UNSPECIFIED  `

Type unspecified.

`  AUTHORIZATION_CODE  `

Use OAuth 2 authorization codes that can be exchanged for a refresh token on the backend.

`  GOOGLE_PLUS_AUTHORIZATION_CODE  `

Return an authorization code for a given Google+ page that can then be exchanged for a refresh token on the backend.

`  FIRST_PARTY_OAUTH  `

Use First Party OAuth.

## DataRefreshType

Represents how the data source supports data auto refresh.

Enums

`  DATA_REFRESH_TYPE_UNSPECIFIED  `

The data source won't support data auto refresh, which is default value.

`  SLIDING_WINDOW  `

The data source supports data auto refresh, and runs will be scheduled for the past few days. Does not allow custom values to be set for each transfer config.

`  CUSTOM_SLIDING_WINDOW  `

The data source supports data auto refresh, and runs will be scheduled for the past few days. Allows custom values to be set for each transfer config.

## DataSourceParameter

A parameter used to define custom fields in a data source definition.

Fields

`  param_id  `

`  string  `

Parameter identifier.

`  display_name  `

`  string  `

Parameter display name in the user interface.

`  description  `

`  string  `

Parameter description.

`  type  `

`  Type  `

Parameter type.

`  required  `

`  bool  `

Is parameter required.

`  repeated  `

`  bool  `

Deprecated. This field has no effect.

`  validation_regex  `

`  string  `

Regular expression which can be used for parameter validation.

`  allowed_values[]  `

`  string  `

All possible values for the parameter.

`  min_value  `

`  DoubleValue  `

For integer and double values specifies minimum allowed value.

`  max_value  `

`  DoubleValue  `

For integer and double values specifies maximum allowed value.

`  fields[]  `

`  DataSourceParameter  `

Deprecated. This field has no effect.

`  validation_description  `

`  string  `

Description of the requirements for this field, in case the user input does not fulfill the regex pattern or min/max values.

`  validation_help_url  `

`  string  `

URL to a help document to further explain the naming requirements.

`  immutable  `

`  bool  `

Cannot be changed after initial creation.

`  recurse  `

`  bool  `

Deprecated. This field has no effect.

`  deprecated  `

`  bool  `

If true, it should not be used in new transfers, and it should not be visible to users.

`  max_list_size  `

`  int64  `

For list parameters, the max size of the list.

## Type

Parameter type.

Enums

`  TYPE_UNSPECIFIED  `

Type unspecified.

`  STRING  `

String parameter.

`  INTEGER  `

Integer parameter (64-bits). Will be serialized to json as string.

`  DOUBLE  `

Double precision floating point parameter.

`  BOOLEAN  `

Boolean parameter.

`  RECORD  `

Deprecated. This field has no effect.

`  PLUS_PAGE  `

Page ID for a Google+ Page.

`  LIST  `

List of strings parameter.

## DeleteTransferConfigRequest

A request to delete data transfer information. All associated transfer runs and log messages will be deleted as well.

Fields

`  name  `

`  string  `

Required. The name of the resource to delete. If you are using the regionless method, the location must be `  US  ` and the name should be in the following form:

  - `  projects/{project_id}/transferConfigs/{config_id}  `

If you are using the regionalized method, the name should be in the following form:

  - `  projects/{project_id}/locations/{location_id}/transferConfigs/{config_id}  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  name  ` :

  - `  bigquery.transfers.update  `

## DeleteTransferRunRequest

A request to delete data transfer run information.

Fields

`  name  `

`  string  `

Required. The name of the resource requested. If you are using the regionless method, the location must be `  US  ` and the name should be in the following form:

  - `  projects/{project_id}/transferConfigs/{config_id}/runs/{run_id}  `

If you are using the regionalized method, the name should be in the following form:

  - `  projects/{project_id}/locations/{location_id}/transferConfigs/{config_id}/runs/{run_id}  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  name  ` :

  - `  bigquery.transfers.update  `

## EmailPreferences

Represents preferences for sending email notifications for transfer run events.

Fields

`  enable_failure_email  `

`  bool  `

If true, email notifications will be sent on transfer run failures.

## EncryptionConfiguration

Represents the encryption configuration for a transfer.

Fields

`  kms_key_name  `

`  StringValue  `

The name of the KMS key used for encrypting BigQuery data.

## EnrollDataSourcesRequest

A request to enroll a set of data sources so they are visible in the BigQuery UI's `  Transfer  ` tab.

Fields

`  name  `

`  string  `

Required. The name of the project resource in the form: `  projects/{project_id}  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  name  ` :

  - `  resourcemanager.projects.update  `

`  data_source_ids[]  `

`  string  `

Data sources that are enrolled. It is required to provide at least one data source id.

## EventDrivenSchedule

Options customizing EventDriven transfers schedule.

Fields

Union field `  eventStream  ` . The event stream which specifies the Event-driven transfer options. Event-driven transfers listen to an event stream to transfer data. `  eventStream  ` can be only one of the following:

`  pubsub_subscription  `

`  string  `

Pub/Sub subscription name used to receive events. Only Google Cloud Storage data source support this option. Format: projects/{project}/subscriptions/{subscription}

## GetDataSourceRequest

A request to get data source info.

Fields

`  name  `

`  string  `

Required. The name of the resource requested. If you are using the regionless method, the location must be `  US  ` and the name should be in the following form:

  - `  projects/{project_id}/dataSources/{data_source_id}  `

If you are using the regionalized method, the name should be in the following form:

  - `  projects/{project_id}/locations/{location_id}/dataSources/{data_source_id}  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  name  ` :

  - `  bigquery.transfers.get  `

## GetTransferConfigRequest

A request to get data transfer information.

Fields

`  name  `

`  string  `

Required. The name of the resource requested. If you are using the regionless method, the location must be `  US  ` and the name should be in the following form:

  - `  projects/{project_id}/transferConfigs/{config_id}  `

If you are using the regionalized method, the name should be in the following form:

  - `  projects/{project_id}/locations/{location_id}/transferConfigs/{config_id}  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  name  ` :

  - `  bigquery.transfers.get  `

## GetTransferRunRequest

A request to get data transfer run information.

Fields

`  name  `

`  string  `

Required. The name of the resource requested. If you are using the regionless method, the location must be `  US  ` and the name should be in the following form:

  - `  projects/{project_id}/transferConfigs/{config_id}/runs/{run_id}  `

If you are using the regionalized method, the name should be in the following form:

  - `  projects/{project_id}/locations/{location_id}/transferConfigs/{config_id}/runs/{run_id}  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  name  ` :

  - `  bigquery.transfers.get  `

## ListDataSourcesRequest

Request to list supported data sources and their data transfer settings.

Fields

`  parent  `

`  string  `

Required. The BigQuery project id for which data sources should be returned. Must be in the form: `  projects/{project_id}  ` or `  projects/{project_id}/locations/{location_id}  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  parent  ` :

  - `  bigquery.transfers.get  `

`  page_token  `

`  string  `

Pagination token, which can be used to request a specific page of `  ListDataSourcesRequest  ` list results. For multiple-page results, `  ListDataSourcesResponse  ` outputs a `  next_page  ` token, which can be used as the `  page_token  ` value to request the next page of list results.

`  page_size  `

`  int32  `

Page size. The default page size is the maximum value of 1000 results.

## ListDataSourcesResponse

Returns list of supported data sources and their metadata.

Fields

`  data_sources[]  `

`  DataSource  `

List of supported data sources and their transfer settings.

`  next_page_token  `

`  string  `

Output only. The next-pagination token. For multiple-page list results, this token can be used as the `  ListDataSourcesRequest.page_token  ` to request the next page of list results.

## ListTransferConfigsRequest

A request to list data transfers configured for a BigQuery project.

Fields

`  parent  `

`  string  `

Required. The BigQuery project id for which transfer configs should be returned. If you are using the regionless method, the location must be `  US  ` and `  parent  ` should be in the following form:

  - \`projects/{project\_id}

If you are using the regionalized method, `  parent  ` should be in the following form:

  - `  projects/{project_id}/locations/{location_id}  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  parent  ` :

  - `  bigquery.transfers.get  `

`  data_source_ids[]  `

`  string  `

When specified, only configurations of requested data sources are returned.

`  page_token  `

`  string  `

Pagination token, which can be used to request a specific page of `  ListTransfersRequest  ` list results. For multiple-page results, `  ListTransfersResponse  ` outputs a `  next_page  ` token, which can be used as the `  page_token  ` value to request the next page of list results.

`  page_size  `

`  int32  `

Page size. The default page size is the maximum value of 1000 results.

## ListTransferConfigsResponse

The returned list of pipelines in the project.

Fields

`  transfer_configs[]  `

`  TransferConfig  `

Output only. The stored pipeline transfer configurations.

`  next_page_token  `

`  string  `

Output only. The next-pagination token. For multiple-page list results, this token can be used as the `  ListTransferConfigsRequest.page_token  ` to request the next page of list results.

## ListTransferLogsRequest

A request to get user facing log messages associated with data transfer run.

Fields

`  parent  `

`  string  `

Required. Transfer run name. If you are using the regionless method, the location must be `  US  ` and the name should be in the following form:

  - `  projects/{project_id}/transferConfigs/{config_id}/runs/{run_id}  `

If you are using the regionalized method, the name should be in the following form:

  - `  projects/{project_id}/locations/{location_id}/transferConfigs/{config_id}/runs/{run_id}  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  parent  ` :

  - `  bigquery.transfers.get  `

`  page_token  `

`  string  `

Pagination token, which can be used to request a specific page of `  ListTransferLogsRequest  ` list results. For multiple-page results, `  ListTransferLogsResponse  ` outputs a `  next_page  ` token, which can be used as the `  page_token  ` value to request the next page of list results.

`  page_size  `

`  int32  `

Page size. The default page size is the maximum value of 1000 results.

`  message_types[]  `

`  MessageSeverity  `

Message types to return. If not populated - INFO, WARNING and ERROR messages are returned.

## ListTransferLogsResponse

The returned list transfer run messages.

Fields

`  transfer_messages[]  `

`  TransferMessage  `

Output only. The stored pipeline transfer messages.

`  next_page_token  `

`  string  `

Output only. The next-pagination token. For multiple-page list results, this token can be used as the `  GetTransferRunLogRequest.page_token  ` to request the next page of list results.

## ListTransferRunsRequest

A request to list data transfer runs.

Fields

`  parent  `

`  string  `

Required. Name of transfer configuration for which transfer runs should be retrieved. If you are using the regionless method, the location must be `  US  ` and the name should be in the following form:

  - `  projects/{project_id}/transferConfigs/{config_id}  `

If you are using the regionalized method, the name should be in the following form:

  - `  projects/{project_id}/locations/{location_id}/transferConfigs/{config_id}  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  parent  ` :

  - `  bigquery.transfers.get  `

`  states[]  `

`  TransferState  `

When specified, only transfer runs with requested states are returned.

`  page_token  `

`  string  `

Pagination token, which can be used to request a specific page of `  ListTransferRunsRequest  ` list results. For multiple-page results, `  ListTransferRunsResponse  ` outputs a `  next_page  ` token, which can be used as the `  page_token  ` value to request the next page of list results.

`  page_size  `

`  int32  `

Page size. The default page size is the maximum value of 1000 results.

`  run_attempt  `

`  RunAttempt  `

Indicates how run attempts are to be pulled.

## RunAttempt

Represents which runs should be pulled.

Enums

`  RUN_ATTEMPT_UNSPECIFIED  `

All runs should be returned.

`  LATEST  `

Only latest run per day should be returned.

## ListTransferRunsResponse

The returned list of pipelines in the project.

Fields

`  transfer_runs[]  `

`  TransferRun  `

Output only. The stored pipeline transfer runs.

`  next_page_token  `

`  string  `

Output only. The next-pagination token. For multiple-page list results, this token can be used as the `  ListTransferRunsRequest.page_token  ` to request the next page of list results.

## ManagedTableType

The classifications of managed tables that can be created, native or BigLake.

Enums

`  MANAGED_TABLE_TYPE_UNSPECIFIED  `

Type unspecified. This defaults to `  NATIVE  ` table.

`  NATIVE  `

The managed table is a native BigQuery table. This is the default value.

`  BIGLAKE  `

The managed table is a BigQuery table for Apache Iceberg (formerly BigLake managed tables), with a BigLake configuration.

## ManualSchedule

This type has no fields.

Options customizing manual transfers schedule.

## ScheduleOptions

Options customizing the data transfer schedule.

Fields

`  disable_auto_scheduling  `

`  bool  `

If true, automatic scheduling of data transfer runs for this configuration will be disabled. The runs can be started on ad-hoc basis using StartManualTransferRuns API. When automatic scheduling is disabled, the TransferConfig.schedule field will be ignored.

`  start_time  `

`  Timestamp  `

Specifies time to start scheduling transfer runs. The first run will be scheduled at or after the start time according to a recurrence pattern defined in the schedule string. The start time can be changed at any moment. The time when a data transfer can be triggered manually is not limited by this option.

`  end_time  `

`  Timestamp  `

Defines time to stop scheduling transfer runs. A transfer run cannot be scheduled at or after the end time. The end time can be changed at any moment. The time when a data transfer can be triggered manually is not limited by this option.

## ScheduleOptionsV2

V2 options customizing different types of data transfer schedule. This field supports existing time-based and manual transfer schedule. Also supports Event-Driven transfer schedule. ScheduleOptionsV2 cannot be used together with ScheduleOptions/Schedule.

Fields

Union field `  schedule  ` . Data transfer schedules. `  schedule  ` can be only one of the following:

`  time_based_schedule  `

`  TimeBasedSchedule  `

Time based transfer schedule options. This is the default schedule option.

`  manual_schedule  `

`  ManualSchedule  `

Manual transfer schedule. If set, the transfer run will not be auto-scheduled by the system, unless the client invokes StartManualTransferRuns. This is equivalent to disable\_auto\_scheduling = true.

`  event_driven_schedule  `

`  EventDrivenSchedule  `

Event driven transfer schedule options. If set, the transfer will be scheduled upon events arrial.

## ScheduleTransferRunsRequest

A request to schedule transfer runs for a time range.

Fields

`  parent  `

`  string  `

Required. Transfer configuration name. If you are using the regionless method, the location must be `  US  ` and the name should be in the following form:

  - `  projects/{project_id}/transferConfigs/{config_id}  `

If you are using the regionalized method, the name should be in the following form:

  - `  projects/{project_id}/locations/{location_id}/transferConfigs/{config_id}  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  parent  ` :

  - `  bigquery.transfers.update  `

`  start_time  `

`  Timestamp  `

Required. Start time of the range of transfer runs. For example, `  "2017-05-25T00:00:00+00:00"  ` .

`  end_time  `

`  Timestamp  `

Required. End time of the range of transfer runs. For example, `  "2017-05-30T00:00:00+00:00"  ` .

## ScheduleTransferRunsResponse

A response to schedule transfer runs for a time range.

Fields

`  runs[]  `

`  TransferRun  `

The transfer runs that were scheduled.

## StartManualTransferRunsRequest

A request to start manual transfer runs.

Fields

`  parent  `

`  string  `

Required. Transfer configuration name. If you are using the regionless method, the location must be `  US  ` and the name should be in the following form:

  - `  projects/{project_id}/transferConfigs/{config_id}  `

If you are using the regionalized method, the name should be in the following form:

  - `  projects/{project_id}/locations/{location_id}/transferConfigs/{config_id}  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  parent  ` :

  - `  bigquery.transfers.update  `

Union field `  time  ` . The requested time specification - this can be a time range or a specific run\_time. `  time  ` can be only one of the following:

`  requested_time_range  `

`  TimeRange  `

A time\_range start and end timestamp for historical data files or reports that are scheduled to be transferred by the scheduled transfer run. requested\_time\_range must be a past time and cannot include future time values.

`  requested_run_time  `

`  Timestamp  `

A run\_time timestamp for historical data files or reports that are scheduled to be transferred by the scheduled transfer run. requested\_run\_time must be a past time and cannot include future time values.

## TimeRange

A specification for a time range, this will request transfer runs with run\_time between start\_time (inclusive) and end\_time (exclusive).

Fields

`  start_time  `

`  Timestamp  `

Start time of the range of transfer runs. For example, `  "2017-05-25T00:00:00+00:00"  ` . The start\_time must be strictly less than the end\_time. Creates transfer runs where run\_time is in the range between start\_time (inclusive) and end\_time (exclusive).

`  end_time  `

`  Timestamp  `

End time of the range of transfer runs. For example, `  "2017-05-30T00:00:00+00:00"  ` . The end\_time must not be in the future. Creates transfer runs where run\_time is in the range between start\_time (inclusive) and end\_time (exclusive).

## StartManualTransferRunsResponse

A response to start manual transfer runs.

Fields

`  runs[]  `

`  TransferRun  `

The transfer runs that were created.

## TimeBasedSchedule

Options customizing the time based transfer schedule. Options are migrated from the original ScheduleOptions message.

Fields

`  schedule  `

`  string  `

Data transfer schedule. If the data source does not support a custom schedule, this should be empty. If it is empty, the default value for the data source will be used. The specified times are in UTC. Examples of valid format: `  1st,3rd monday of month 15:30  ` , `  every wed,fri of jan,jun 13:15  ` , and `  first sunday of quarter 00:00  ` . See more explanation about the format here: <https://cloud.google.com/appengine/docs/flexible/python/scheduling-jobs-with-cron-yaml#the_schedule_format>

NOTE: The minimum interval time between recurring transfers depends on the data source; refer to the documentation for your data source.

`  start_time  `

`  Timestamp  `

Specifies time to start scheduling transfer runs. The first run will be scheduled at or after the start time according to a recurrence pattern defined in the schedule string. The start time can be changed at any moment.

`  end_time  `

`  Timestamp  `

Defines time to stop scheduling transfer runs. A transfer run cannot be scheduled at or after the end time. The end time can be changed at any moment.

## TransferConfig

Represents a data transfer configuration. A transfer configuration contains all metadata needed to perform a data transfer. For example, `  destination_dataset_id  ` specifies where data should be stored. When a new transfer configuration is created, the specified `  destination_dataset_id  ` is created when needed and shared with the appropriate data source service account.

Fields

`  name  `

`  string  `

Identifier. The resource name of the transfer config. Transfer config names have the form either `  projects/{project_id}/locations/{region}/transferConfigs/{config_id}  ` or `  projects/{project_id}/transferConfigs/{config_id}  ` , where `  config_id  ` is usually a UUID, even though it is not guaranteed or required. The name is ignored when creating a transfer config.

`  display_name  `

`  string  `

User specified display name for the data transfer.

`  data_source_id  `

`  string  `

Data source ID. This cannot be changed once data transfer is created. The full list of available data source IDs can be returned through an API call: <https://cloud.google.com/bigquery-transfer/docs/reference/datatransfer/rest/v1/projects.locations.dataSources/list>

`  params  `

`  Struct  `

Parameters specific to each data source. For more information see the bq tab in the 'Setting up a data transfer' section for each data source. For example the parameters for Cloud Storage transfers are listed here: <https://cloud.google.com/bigquery-transfer/docs/cloud-storage-transfer#bq>

`  schedule  `

`  string  `

Data transfer schedule. If the data source does not support a custom schedule, this should be empty. If it is empty, the default value for the data source will be used. The specified times are in UTC. Examples of valid format: `  1st,3rd monday of month 15:30  ` , `  every wed,fri of jan,jun 13:15  ` , and `  first sunday of quarter 00:00  ` . See more explanation about the format here: <https://cloud.google.com/appengine/docs/flexible/python/scheduling-jobs-with-cron-yaml#the_schedule_format>

NOTE: The minimum interval time between recurring transfers depends on the data source; refer to the documentation for your data source.

`  schedule_options  `

`  ScheduleOptions  `

Options customizing the data transfer schedule.

`  schedule_options_v2  `

`  ScheduleOptionsV2  `

Options customizing different types of data transfer schedule. This field replaces "schedule" and "schedule\_options" fields. ScheduleOptionsV2 cannot be used together with ScheduleOptions/Schedule.

`  data_refresh_window_days  `

`  int32  `

The number of days to look back to automatically refresh the data. For example, if `  data_refresh_window_days = 10  ` , then every day BigQuery reingests data for \[today-10, today-1\], rather than ingesting data for just \[today-1\]. Only valid if the data source supports the feature. Set the value to 0 to use the default value.

`  disabled  `

`  bool  `

Is this config disabled. When set to true, no runs will be scheduled for this transfer config.

`  update_time  `

`  Timestamp  `

Output only. Data transfer modification time. Ignored by server on input.

`  next_run_time  `

`  Timestamp  `

Output only. Next time when data transfer will run.

`  state  `

`  TransferState  `

Output only. State of the most recently updated transfer run.

`  user_id  `

`  int64  `

Deprecated. Unique ID of the user on whose behalf transfer is done.

`  dataset_region  `

`  string  `

Output only. Region in which BigQuery dataset is located.

`  notification_pubsub_topic  `

`  string  `

Pub/Sub topic where notifications will be sent after transfer runs associated with this transfer config finish.

The format for specifying a pubsub topic is: `  projects/{project_id}/topics/{topic_id}  `

`  email_preferences  `

`  EmailPreferences  `

Email notifications will be sent according to these preferences to the email address of the user who owns this transfer config.

`  encryption_configuration  `

`  EncryptionConfiguration  `

The encryption configuration part. Currently, it is only used for the optional KMS key name. The BigQuery service account of your project must be granted permissions to use the key. Read methods will return the key name applied in effect. Write methods will apply the key if it is present, or otherwise try to apply project default keys if it is absent.

`  error  `

`  Status  `

Output only. Error code with detailed information about reason of the latest config failure.

`  managed_table_type  `

`  ManagedTableType  `

The classification of the destination table.

Union field `  destination  ` . The destination of the transfer config. `  destination  ` can be only one of the following:

`  destination_dataset_id  `

`  string  `

The BigQuery target dataset id.

`  owner_info  `

`  UserInfo  `

Output only. Information about the user whose credentials are used to transfer data. Populated only for `  transferConfigs.get  ` requests. In case the user information is not available, this field will not be populated.

## TransferMessage

Represents a user facing message for a particular data transfer run.

Fields

`  message_time  `

`  Timestamp  `

Time when message was logged.

`  severity  `

`  MessageSeverity  `

Message severity.

`  message_text  `

`  string  `

Message text.

## MessageSeverity

Represents data transfer user facing message severity.

Enums

`  MESSAGE_SEVERITY_UNSPECIFIED  `

No severity specified.

`  INFO  `

Informational message.

`  WARNING  `

Warning message.

`  ERROR  `

Error message.

## TransferRun

Represents a data transfer run.

Fields

`  name  `

`  string  `

Identifier. The resource name of the transfer run. Transfer run names have the form `  projects/{project_id}/locations/{location}/transferConfigs/{config_id}/runs/{run_id}  ` . The name is ignored when creating a transfer run.

`  schedule_time  `

`  Timestamp  `

Minimum time after which a transfer run can be started.

`  run_time  `

`  Timestamp  `

For batch transfer runs, specifies the date and time of the data should be ingested.

`  error_status  `

`  Status  `

Status of the transfer run.

`  start_time  `

`  Timestamp  `

Output only. Time when transfer run was started. Parameter ignored by server for input requests.

`  end_time  `

`  Timestamp  `

Output only. Time when transfer run ended. Parameter ignored by server for input requests.

`  update_time  `

`  Timestamp  `

Output only. Last time the data transfer run state was updated.

`  params  `

`  Struct  `

Output only. Parameters specific to each data source. For more information see the bq tab in the 'Setting up a data transfer' section for each data source. For example the parameters for Cloud Storage transfers are listed here: <https://cloud.google.com/bigquery-transfer/docs/cloud-storage-transfer#bq>

`  data_source_id  `

`  string  `

Output only. Data source id.

`  state  `

`  TransferState  `

Data transfer run state. Ignored for input requests.

`  user_id  `

`  int64  `

Deprecated. Unique ID of the user on whose behalf transfer is done.

`  schedule  `

`  string  `

Output only. Describes the schedule of this transfer run if it was created as part of a regular schedule. For batch transfer runs that are scheduled manually, this is empty. NOTE: the system might choose to delay the schedule depending on the current load, so `  schedule_time  ` doesn't always match this.

`  notification_pubsub_topic  `

`  string  `

Output only. Pub/Sub topic where a notification will be sent after this transfer run finishes.

The format for specifying a pubsub topic is: `  projects/{project_id}/topics/{topic_id}  `

`  email_preferences  `

`  EmailPreferences  `

Output only. Email notifications will be sent according to these preferences to the email address of the user who owns the transfer config this run was derived from.

Union field `  destination  ` . Data transfer destination. `  destination  ` can be only one of the following:

`  destination_dataset_id  `

`  string  `

Output only. The BigQuery target dataset id.

## TransferState

Represents data transfer run state.

Enums

`  TRANSFER_STATE_UNSPECIFIED  `

State placeholder (0).

`  PENDING  `

Data transfer is scheduled and is waiting to be picked up by data transfer backend (2).

`  RUNNING  `

Data transfer is in progress (3).

`  SUCCEEDED  `

Data transfer completed successfully (4).

`  FAILED  `

Data transfer failed (5).

`  CANCELLED  `

Data transfer is cancelled (6).

## TransferType

This item is deprecated\!

DEPRECATED. Represents data transfer type.

Enums

`  TRANSFER_TYPE_UNSPECIFIED  `

Invalid or Unknown transfer type placeholder.

`  BATCH  `

Batch data transfer.

`  STREAMING  `

Streaming data transfer. Streaming data source currently doesn't support multiple transfer configs per project.

## UnenrollDataSourcesRequest

A request to unenroll a set of data sources so they are no longer visible in the BigQuery UI's `  Transfer  ` tab.

Fields

`  name  `

`  string  `

Required. The name of the project resource in the form: `  projects/{project_id}  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  name  ` :

  - `  resourcemanager.projects.update  `

`  data_source_ids[]  `

`  string  `

Data sources that are unenrolled. It is required to provide at least one data source id.

## UpdateTransferConfigRequest

A request to update a transfer configuration. To update the user id of the transfer configuration, authorization info needs to be provided.

When using a cross project service account for updating a transfer config, you must enable cross project service account usage. For more information, see [Disable attachment of service accounts to resources in other projects](https://cloud.google.com/resource-manager/docs/organization-policy/restricting-service-accounts#disable_cross_project_service_accounts) .

Fields

`  transfer_config  `

`  TransferConfig  `

Required. Data transfer configuration to create.

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  transferConfig  ` :

  - `  bigquery.transfers.update  `

`  authorization_code (deprecated)  `

`  string  `

This item is deprecated\!

Deprecated: Authorization code was required when `  transferConfig.dataSourceId  ` is 'youtube\_channel' but it is no longer used in any data sources. Use `  version_info  ` instead.

Optional OAuth2 authorization code to use with this transfer configuration. This is required only if `  transferConfig.dataSourceId  ` is 'youtube\_channel' and new credentials are needed, as indicated by `  CheckValidCreds  ` . In order to obtain authorization\_code, make a request to the following URL:

``` text
https://bigquery.cloud.google.com/datatransfer/oauthz/auth?redirect_uri=urn:ietf:wg:oauth:2.0:oob&response_type=authorization_code&client_id=client_id&scope=data_source_scopes
```

  - The client\_id is the OAuth client\_id of the data source as returned by ListDataSources method.
  - data\_source\_scopes are the scopes returned by ListDataSources method.

Note that this should not be set when `  service_account_name  ` is used to update the transfer config.

`  update_mask  `

`  FieldMask  `

Required. Required list of fields to be updated in this request.

`  version_info  `

`  string  `

Optional version info. This parameter replaces `  authorization_code  ` which is no longer used in any data sources. This is required only if `  transferConfig.dataSourceId  ` is 'youtube\_channel' *or* new credentials are needed, as indicated by `  CheckValidCreds  ` . In order to obtain version info, make a request to the following URL:

``` text
https://bigquery.cloud.google.com/datatransfer/oauthz/auth?redirect_uri=urn:ietf:wg:oauth:2.0:oob&response_type=version_info&client_id=client_id&scope=data_source_scopes
```

  - The client\_id is the OAuth client\_id of the data source as returned by ListDataSources method.
  - data\_source\_scopes are the scopes returned by ListDataSources method.

Note that this should not be set when `  service_account_name  ` is used to update the transfer config.

`  service_account_name  `

`  string  `

Optional service account email. If this field is set, the transfer config will be created with this service account's credentials. It requires that the requesting user calling this API has permissions to act as this service account.

Note that not all data sources support service account credentials when creating a transfer config. For the latest list of data sources, read about [using service accounts](https://cloud.google.com/bigquery-transfer/docs/use-service-accounts) .

## UserInfo

Information about a user.

Fields

`  email  `

`  string  `

E-mail address of the user.
