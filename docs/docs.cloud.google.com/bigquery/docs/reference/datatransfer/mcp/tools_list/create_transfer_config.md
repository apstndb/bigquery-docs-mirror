## Tool: `       create_transfer_config      `

Create a transfer configuration.

To create a transfer configuration, do the following:

  - Provide the `  required_fields  ` .

  - Specify how often you want your transfer to run by specifying `  schedule_options  `

  - Provide the `  optional_fields  ` .

  - If you want to use a service account to create this transfer, provide a `  service_account_name  ` .

  - Check that you have valid credentials by calling `  check_valid_creds  ` :
    
      - If you do not have valid credentials, do the following:
      - Find your `  client_id  ` and `  data_source_scopes  ` from your data source definition.
      - Authorize your data source by navigating to the following link:
    
    <!-- end list -->
    
    ``` text
    https://bigquery.cloud.google.com/datatransfer/oauthz/auth?redirect_uri=urn:ietf:wg:oauth:2.0:oob&response_type=version_info&client_id=CLIENT_ID&scope=DATA_SOURCE_1%20DATA_SOURCE_2
            
    ```
    
      - Provide the `  version_info  ` .
      - If you have valid credentials, then `  version_info  ` is not required.

The following sample demonstrate how to use `  curl  ` to invoke the `  create_transfer_config  ` MCP tool.

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
curl --location &#39;https://bigquerydatatransfer.googleapis.com/mcp&#39; \
--header &#39;content-type: application/json&#39; \
--header &#39;accept: application/json, text/event-stream&#39; \
--data &#39;{
  &quot;method&quot;: &quot;tools/call&quot;,
  &quot;params&quot;: {
    &quot;name&quot;: &quot;create_transfer_config&quot;,
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

Request for creating a transfer configuration.

The only supported data sources are:

  - Campaign Manager ( `  data_source_id  ` : `  dcm_dt  ` )
  - Cloud Storage ( `  data_source_id  ` : `  google_cloud_storage  ` )
  - Comparison Shopping Service (CSS) Center ( `  data_source_id  ` : `  css_center  ` )
  - Dataset Copies ( `  data_source_id  ` : `  cross_region_copy  ` )
  - Display & Video 360 ( `  data_source_id  ` : `  displayvideo  ` )
  - Google Ad Manager ( `  data_source_id  ` : `  dfp_dt  ` )
  - Google Ads ( `  data_source_id  ` : `  google_ads  ` )
  - Google Analytics 4 ( `  data_source_id  ` : `  ga4  ` )
  - Google Merchant Center ( `  data_source_id  ` : `  merchant_center  ` )
  - Google Play ( `  data_source_id  ` : `  play  ` )
  - Scheduled Queries ( `  data_source_id  ` : `  scheduled_query  ` )
  - Search Ads 360 ( `  data_source_id  ` : `  search_ads  ` )
  - YouTube Channel ( `  data_source_id  ` : `  youtube_channel  ` )
  - YouTube Content Owner ( `  data_source_id  ` : `  youtube_content_owner  ` )

### CreateTransferConfigRequest

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
  &quot;dataSource&quot;: enum (DataSource),
  &quot;projectId&quot;: string,
  &quot;location&quot;: string,
  &quot;displayName&quot;: string,
  &quot;destinationDatasetId&quot;: string,
  &quot;params&quot;: {
    object
  },
  &quot;scheduleOptions&quot;: {
    object (ScheduleOptionsV2)
  },
  &quot;notificationPubsubTopic&quot;: string,
  &quot;emailPreferences&quot;: {
    object (EmailPreferences)
  },

  // Union field authorization can be only one of the following:
  &quot;versionInfo&quot;: string,
  &quot;serviceAccountName&quot;: string
  // End of list of possible types for union field authorization.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  dataSource  `

`  enum ( DataSource  ` )

Required. Data source.

`  projectId  `

`  string  `

Required. Project ID or project number of the transfer config.

`  location  `

`  string  `

Required. Location of the transfer config. If specified location and location of the destination bigquery dataset do not match - the request will fail.

`  displayName  `

`  string  `

Required. Display name of the transfer config.

`  destinationDatasetId  `

`  string  `

Required. Destination dataset ID of the transfer config where data will be loaded.

`  params  `

`  object ( Struct  ` format)

Required. Data source parameters for the transfer config.

`  scheduleOptions  `

`  object ( ScheduleOptionsV2  ` )

Optional. Schedule options for the transfer config. If not specified, the transfer config will be created with its default schedule defined in the data source definition.

`  notificationPubsubTopic  `

`  string  `

Pub/Sub topic where notifications will be sent after transfer runs associated with this transfer config finish.

The format for specifying a pubsub topic is: `  projects/{project_id}/topics/{topic_id}  `

`  emailPreferences  `

`  object ( EmailPreferences  ` )

Email notifications will be sent according to these preferences to the email address of the user who owns this transfer config.

Union field `  authorization  ` . Authorization for the transfer config. `  authorization  ` can be only one of the following:

`  versionInfo  `

`  string  `

This is required only if new credentials are needed, as indicated by `  CheckValidCreds  ` . In order to obtain version info, make a request to the following URL:

``` text
https://bigquery.cloud.google.com/datatransfer/oauthz/auth?redirect_uri=urn:ietf:wg:oauth:2.0:oob&response_type=version_info&client_id=client_id&scope=data_source_scopes
```

  - The client\_id is the OAuth client\_id of the data source as returned by GetDataSource method.
  - data\_source\_scopes are the scopes returned by GetDataSource method.

Note that this should not be set when `  service_account_name  ` is used to create the transfer config.

`  serviceAccountName  `

`  string  `

Optional service account email. If this field is set, the transfer config will be created with this service account's credentials. It requires that the requesting user calling this API has permissions to act as this service account.

### Struct

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
  &quot;fields&quot;: {
    string: value,
    ...
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  fields  `

`  map (key: string, value: value ( Value  ` format))

Unordered map of dynamically typed values.

An object containing a list of `  "key": value  ` pairs. Example: `  { "name": "wrench", "mass": "1.3kg", "count": "3" }  ` .

### FieldsEntry

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
  &quot;value&quot;: value
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  key  `

`  string  `

`  value  `

`  value ( Value  ` format)

### Value

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

  // Union field kind can be only one of the following:
  &quot;nullValue&quot;: null,
  &quot;numberValue&quot;: number,
  &quot;stringValue&quot;: string,
  &quot;boolValue&quot;: boolean,
  &quot;structValue&quot;: {
    object
  },
  &quot;listValue&quot;: array
  // End of list of possible types for union field kind.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `  kind  ` . The kind of value. `  kind  ` can be only one of the following:

`  nullValue  `

`  null  `

Represents a JSON `  null  ` .

`  numberValue  `

`  number  `

Represents a JSON number. Must not be `  NaN  ` , `  Infinity  ` or `  -Infinity  ` , since those are not supported in JSON. This also cannot represent large Int64 values, since JSON format generally does not support them in its number type.

`  stringValue  `

`  string  `

Represents a JSON string.

`  boolValue  `

`  boolean  `

Represents a JSON boolean ( `  true  ` or `  false  ` literal in JSON).

`  structValue  `

`  object ( Struct  ` format)

Represents a JSON object.

`  listValue  `

`  array ( ListValue  ` format)

Represents a JSON array.

### ListValue

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
  &quot;values&quot;: [
    value
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  values[]  `

`  value ( Value  ` format)

Repeated field of dynamically typed values.

### ScheduleOptionsV2

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

  // Union field schedule can be only one of the following:
  &quot;timeBasedSchedule&quot;: {
    object (TimeBasedSchedule)
  },
  &quot;manualSchedule&quot;: {
    object (ManualSchedule)
  },
  &quot;eventDrivenSchedule&quot;: {
    object (EventDrivenSchedule)
  }
  // End of list of possible types for union field schedule.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `  schedule  ` . Data transfer schedules. `  schedule  ` can be only one of the following:

`  timeBasedSchedule  `

`  object ( TimeBasedSchedule  ` )

Time based transfer schedule options. This is the default schedule option.

`  manualSchedule  `

`  object ( ManualSchedule  ` )

Manual transfer schedule. If set, the transfer run will not be auto-scheduled by the system, unless the client invokes StartManualTransferRuns. This is equivalent to disable\_auto\_scheduling = true.

`  eventDrivenSchedule  `

`  object ( EventDrivenSchedule  ` )

Event driven transfer schedule options. If set, the transfer will be scheduled upon events arrial.

### TimeBasedSchedule

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
  &quot;schedule&quot;: string,
  &quot;startTime&quot;: string,
  &quot;endTime&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  schedule  `

`  string  `

Data transfer schedule. If the data source does not support a custom schedule, this should be empty. If it is empty, the default value for the data source will be used. The specified times are in UTC. Examples of valid format: `  1st,3rd monday of month 15:30  ` , `  every wed,fri of jan,jun 13:15  ` , and `  first sunday of quarter 00:00  ` . See more explanation about the format here: <https://cloud.google.com/appengine/docs/flexible/python/scheduling-jobs-with-cron-yaml#the_schedule_format>

NOTE: The minimum interval time between recurring transfers depends on the data source; refer to the documentation for your data source.

`  startTime  `

`  string ( Timestamp  ` format)

Specifies time to start scheduling transfer runs. The first run will be scheduled at or after the start time according to a recurrence pattern defined in the schedule string. The start time can be changed at any moment.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  endTime  `

`  string ( Timestamp  ` format)

Defines time to stop scheduling transfer runs. A transfer run cannot be scheduled at or after the end time. The end time can be changed at any moment.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

### Timestamp

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
  &quot;seconds&quot;: string,
  &quot;nanos&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  seconds  `

`  string ( int64 format)  `

Represents seconds of UTC time since Unix epoch 1970-01-01T00:00:00Z. Must be between -62135596800 and 253402300799 inclusive (which corresponds to 0001-01-01T00:00:00Z to 9999-12-31T23:59:59Z).

`  nanos  `

`  integer  `

Non-negative fractions of a second at nanosecond resolution. This field is the nanosecond portion of the duration, not an alternative to seconds. Negative second values with fractions must still have non-negative nanos values that count forward in time. Must be between 0 and 999,999,999 inclusive.

### EventDrivenSchedule

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

  // Union field eventStream can be only one of the following:
  &quot;pubsubSubscription&quot;: string
  // End of list of possible types for union field eventStream.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `  eventStream  ` . The event stream which specifies the Event-driven transfer options. Event-driven transfers listen to an event stream to transfer data. `  eventStream  ` can be only one of the following:

`  pubsubSubscription  `

`  string  `

Pub/Sub subscription name used to receive events. Only Google Cloud Storage data source support this option. Format: projects/{project}/subscriptions/{subscription}

### EmailPreferences

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
  &quot;enableFailureEmail&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  enableFailureEmail  `

`  boolean  `

If true, email notifications will be sent on transfer run failures.

## Output Schema

Represents a data transfer configuration. A transfer configuration contains all metadata needed to perform a data transfer. For example, `  destination_dataset_id  ` specifies where data should be stored. When a new transfer configuration is created, the specified `  destination_dataset_id  ` is created when needed and shared with the appropriate data source service account.

### TransferConfig

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
  &quot;displayName&quot;: string,
  &quot;dataSourceId&quot;: string,
  &quot;params&quot;: {
    object
  },
  &quot;schedule&quot;: string,
  &quot;scheduleOptions&quot;: {
    object (ScheduleOptions)
  },
  &quot;scheduleOptionsV2&quot;: {
    object (ScheduleOptionsV2)
  },
  &quot;dataRefreshWindowDays&quot;: integer,
  &quot;disabled&quot;: boolean,
  &quot;updateTime&quot;: string,
  &quot;nextRunTime&quot;: string,
  &quot;state&quot;: enum (TransferState),
  &quot;userId&quot;: string,
  &quot;datasetRegion&quot;: string,
  &quot;notificationPubsubTopic&quot;: string,
  &quot;emailPreferences&quot;: {
    object (EmailPreferences)
  },
  &quot;encryptionConfiguration&quot;: {
    object (EncryptionConfiguration)
  },
  &quot;error&quot;: {
    object (Status)
  },
  &quot;managedTableType&quot;: enum (ManagedTableType),

  // Union field destination can be only one of the following:
  &quot;destinationDatasetId&quot;: string
  // End of list of possible types for union field destination.

  // Union field _owner_info can be only one of the following:
  &quot;ownerInfo&quot;: {
    object (UserInfo)
  }
  // End of list of possible types for union field _owner_info.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  name  `

`  string  `

Identifier. The resource name of the transfer config. Transfer config names have the form either `  projects/{project_id}/locations/{region}/transferConfigs/{config_id}  ` or `  projects/{project_id}/transferConfigs/{config_id}  ` , where `  config_id  ` is usually a UUID, even though it is not guaranteed or required. The name is ignored when creating a transfer config.

`  displayName  `

`  string  `

User specified display name for the data transfer.

`  dataSourceId  `

`  string  `

Data source ID. This cannot be changed once data transfer is created. The full list of available data source IDs can be returned through an API call: <https://cloud.google.com/bigquery-transfer/docs/reference/datatransfer/rest/v1/projects.locations.dataSources/list>

`  params  `

`  object ( Struct  ` format)

Parameters specific to each data source. For more information see the bq tab in the 'Setting up a data transfer' section for each data source. For example the parameters for Cloud Storage transfers are listed here: <https://cloud.google.com/bigquery-transfer/docs/cloud-storage-transfer#bq>

`  schedule  `

`  string  `

Data transfer schedule. If the data source does not support a custom schedule, this should be empty. If it is empty, the default value for the data source will be used. The specified times are in UTC. Examples of valid format: `  1st,3rd monday of month 15:30  ` , `  every wed,fri of jan,jun 13:15  ` , and `  first sunday of quarter 00:00  ` . See more explanation about the format here: <https://cloud.google.com/appengine/docs/flexible/python/scheduling-jobs-with-cron-yaml#the_schedule_format>

NOTE: The minimum interval time between recurring transfers depends on the data source; refer to the documentation for your data source.

`  scheduleOptions  `

`  object ( ScheduleOptions  ` )

Options customizing the data transfer schedule.

`  scheduleOptionsV2  `

`  object ( ScheduleOptionsV2  ` )

Options customizing different types of data transfer schedule. This field replaces "schedule" and "schedule\_options" fields. ScheduleOptionsV2 cannot be used together with ScheduleOptions/Schedule.

`  dataRefreshWindowDays  `

`  integer  `

The number of days to look back to automatically refresh the data. For example, if `  data_refresh_window_days = 10  ` , then every day BigQuery reingests data for \[today-10, today-1\], rather than ingesting data for just \[today-1\]. Only valid if the data source supports the feature. Set the value to 0 to use the default value.

`  disabled  `

`  boolean  `

Is this config disabled. When set to true, no runs will be scheduled for this transfer config.

`  updateTime  `

`  string ( Timestamp  ` format)

Output only. Data transfer modification time. Ignored by server on input.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  nextRunTime  `

`  string ( Timestamp  ` format)

Output only. Next time when data transfer will run.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  state  `

`  enum ( TransferState  ` )

Output only. State of the most recently updated transfer run.

`  userId  `

`  string ( int64 format)  `

Deprecated. Unique ID of the user on whose behalf transfer is done.

`  datasetRegion  `

`  string  `

Output only. Region in which BigQuery dataset is located.

`  notificationPubsubTopic  `

`  string  `

Pub/Sub topic where notifications will be sent after transfer runs associated with this transfer config finish.

The format for specifying a pubsub topic is: `  projects/{project_id}/topics/{topic_id}  `

`  emailPreferences  `

`  object ( EmailPreferences  ` )

Email notifications will be sent according to these preferences to the email address of the user who owns this transfer config.

`  encryptionConfiguration  `

`  object ( EncryptionConfiguration  ` )

The encryption configuration part. Currently, it is only used for the optional KMS key name. The BigQuery service account of your project must be granted permissions to use the key. Read methods will return the key name applied in effect. Write methods will apply the key if it is present, or otherwise try to apply project default keys if it is absent.

`  error  `

`  object ( Status  ` )

Output only. Error code with detailed information about reason of the latest config failure.

`  managedTableType  `

`  enum ( ManagedTableType  ` )

The classification of the destination table.

Union field `  destination  ` . The destination of the transfer config. `  destination  ` can be only one of the following:

`  destinationDatasetId  `

`  string  `

The BigQuery target dataset id.

Union field `  _owner_info  ` .

`  _owner_info  ` can be only one of the following:

`  ownerInfo  `

`  object ( UserInfo  ` )

Output only. Information about the user whose credentials are used to transfer data. Populated only for `  transferConfigs.get  ` requests. In case the user information is not available, this field will not be populated.

### Struct

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
  &quot;fields&quot;: {
    string: value,
    ...
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  fields  `

`  map (key: string, value: value ( Value  ` format))

Unordered map of dynamically typed values.

An object containing a list of `  "key": value  ` pairs. Example: `  { "name": "wrench", "mass": "1.3kg", "count": "3" }  ` .

### FieldsEntry

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
  &quot;value&quot;: value
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  key  `

`  string  `

`  value  `

`  value ( Value  ` format)

### Value

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

  // Union field kind can be only one of the following:
  &quot;nullValue&quot;: null,
  &quot;numberValue&quot;: number,
  &quot;stringValue&quot;: string,
  &quot;boolValue&quot;: boolean,
  &quot;structValue&quot;: {
    object
  },
  &quot;listValue&quot;: array
  // End of list of possible types for union field kind.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `  kind  ` . The kind of value. `  kind  ` can be only one of the following:

`  nullValue  `

`  null  `

Represents a JSON `  null  ` .

`  numberValue  `

`  number  `

Represents a JSON number. Must not be `  NaN  ` , `  Infinity  ` or `  -Infinity  ` , since those are not supported in JSON. This also cannot represent large Int64 values, since JSON format generally does not support them in its number type.

`  stringValue  `

`  string  `

Represents a JSON string.

`  boolValue  `

`  boolean  `

Represents a JSON boolean ( `  true  ` or `  false  ` literal in JSON).

`  structValue  `

`  object ( Struct  ` format)

Represents a JSON object.

`  listValue  `

`  array ( ListValue  ` format)

Represents a JSON array.

### ListValue

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
  &quot;values&quot;: [
    value
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  values[]  `

`  value ( Value  ` format)

Repeated field of dynamically typed values.

### ScheduleOptions

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
  &quot;disableAutoScheduling&quot;: boolean,
  &quot;startTime&quot;: string,
  &quot;endTime&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  disableAutoScheduling  `

`  boolean  `

If true, automatic scheduling of data transfer runs for this configuration will be disabled. The runs can be started on ad-hoc basis using StartManualTransferRuns API. When automatic scheduling is disabled, the TransferConfig.schedule field will be ignored.

`  startTime  `

`  string ( Timestamp  ` format)

Specifies time to start scheduling transfer runs. The first run will be scheduled at or after the start time according to a recurrence pattern defined in the schedule string. The start time can be changed at any moment. The time when a data transfer can be triggered manually is not limited by this option.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  endTime  `

`  string ( Timestamp  ` format)

Defines time to stop scheduling transfer runs. A transfer run cannot be scheduled at or after the end time. The end time can be changed at any moment. The time when a data transfer can be triggered manually is not limited by this option.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

### Timestamp

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
  &quot;seconds&quot;: string,
  &quot;nanos&quot;: integer
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  seconds  `

`  string ( int64 format)  `

Represents seconds of UTC time since Unix epoch 1970-01-01T00:00:00Z. Must be between -62135596800 and 253402300799 inclusive (which corresponds to 0001-01-01T00:00:00Z to 9999-12-31T23:59:59Z).

`  nanos  `

`  integer  `

Non-negative fractions of a second at nanosecond resolution. This field is the nanosecond portion of the duration, not an alternative to seconds. Negative second values with fractions must still have non-negative nanos values that count forward in time. Must be between 0 and 999,999,999 inclusive.

### ScheduleOptionsV2

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

  // Union field schedule can be only one of the following:
  &quot;timeBasedSchedule&quot;: {
    object (TimeBasedSchedule)
  },
  &quot;manualSchedule&quot;: {
    object (ManualSchedule)
  },
  &quot;eventDrivenSchedule&quot;: {
    object (EventDrivenSchedule)
  }
  // End of list of possible types for union field schedule.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `  schedule  ` . Data transfer schedules. `  schedule  ` can be only one of the following:

`  timeBasedSchedule  `

`  object ( TimeBasedSchedule  ` )

Time based transfer schedule options. This is the default schedule option.

`  manualSchedule  `

`  object ( ManualSchedule  ` )

Manual transfer schedule. If set, the transfer run will not be auto-scheduled by the system, unless the client invokes StartManualTransferRuns. This is equivalent to disable\_auto\_scheduling = true.

`  eventDrivenSchedule  `

`  object ( EventDrivenSchedule  ` )

Event driven transfer schedule options. If set, the transfer will be scheduled upon events arrial.

### TimeBasedSchedule

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
  &quot;schedule&quot;: string,
  &quot;startTime&quot;: string,
  &quot;endTime&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  schedule  `

`  string  `

Data transfer schedule. If the data source does not support a custom schedule, this should be empty. If it is empty, the default value for the data source will be used. The specified times are in UTC. Examples of valid format: `  1st,3rd monday of month 15:30  ` , `  every wed,fri of jan,jun 13:15  ` , and `  first sunday of quarter 00:00  ` . See more explanation about the format here: <https://cloud.google.com/appengine/docs/flexible/python/scheduling-jobs-with-cron-yaml#the_schedule_format>

NOTE: The minimum interval time between recurring transfers depends on the data source; refer to the documentation for your data source.

`  startTime  `

`  string ( Timestamp  ` format)

Specifies time to start scheduling transfer runs. The first run will be scheduled at or after the start time according to a recurrence pattern defined in the schedule string. The start time can be changed at any moment.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

`  endTime  `

`  string ( Timestamp  ` format)

Defines time to stop scheduling transfer runs. A transfer run cannot be scheduled at or after the end time. The end time can be changed at any moment.

Uses RFC 3339, where generated output will always be Z-normalized and use 0, 3, 6 or 9 fractional digits. Offsets other than "Z" are also accepted. Examples: `  "2014-10-02T15:01:23Z"  ` , `  "2014-10-02T15:01:23.045123456Z"  ` or `  "2014-10-02T15:01:23+05:30"  ` .

### EventDrivenSchedule

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

  // Union field eventStream can be only one of the following:
  &quot;pubsubSubscription&quot;: string
  // End of list of possible types for union field eventStream.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `  eventStream  ` . The event stream which specifies the Event-driven transfer options. Event-driven transfers listen to an event stream to transfer data. `  eventStream  ` can be only one of the following:

`  pubsubSubscription  `

`  string  `

Pub/Sub subscription name used to receive events. Only Google Cloud Storage data source support this option. Format: projects/{project}/subscriptions/{subscription}

### EmailPreferences

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
  &quot;enableFailureEmail&quot;: boolean
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  enableFailureEmail  `

`  boolean  `

If true, email notifications will be sent on transfer run failures.

### UserInfo

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

  // Union field _email can be only one of the following:
  &quot;email&quot;: string
  // End of list of possible types for union field _email.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

Union field `  _email  ` .

`  _email  ` can be only one of the following:

`  email  `

`  string  `

E-mail address of the user.

### EncryptionConfiguration

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
  &quot;kmsKeyName&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  kmsKeyName  `

`  string  `

The name of the KMS key used for encrypting BigQuery data.

### StringValue

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
  &quot;value&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  value  `

`  string  `

The string value.

### Status

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
  &quot;code&quot;: integer,
  &quot;message&quot;: string,
  &quot;details&quot;: [
    {
      &quot;@type&quot;: string,
      field1: ...,
      ...
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  code  `

`  integer  `

The status code, which should be an enum value of `  google.rpc.Code  ` .

`  message  `

`  string  `

A developer-facing error message, which should be in English. Any user-facing error message should be localized and sent in the `  google.rpc.Status.details  ` field, or localized by the client.

`  details[]  `

`  object  `

A list of messages that carry the error details. There is a common set of message types for APIs to use.

An object containing fields of an arbitrary type. An additional field `  "@type"  ` contains a URI identifying the type. Example: `  { "id": 1234, "@type": "types.example.com/standard/id" }  ` .

### Any

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
  &quot;typeUrl&quot;: string,
  &quot;value&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  typeUrl  `

`  string  `

Identifies the type of the serialized Protobuf message with a URI reference consisting of a prefix ending in a slash and the fully-qualified type name.

Example: type.googleapis.com/google.protobuf.StringValue

This string must contain at least one `  /  ` character, and the content after the last `  /  ` must be the fully-qualified name of the type in canonical form, without a leading dot. Do not write a scheme on these URI references so that clients do not attempt to contact them.

The prefix is arbitrary and Protobuf implementations are expected to simply strip off everything up to and including the last `  /  ` to identify the type. `  type.googleapis.com/  ` is a common default prefix that some legacy implementations require. This prefix does not indicate the origin of the type, and URIs containing it are not expected to respond to any requests.

All type URL strings must be legal URI references with the additional restriction (for the text format) that the content of the reference must consist only of alphanumeric characters, percent-encoded escapes, and characters in the following set (not including the outer backticks): `  /-.~_!$&()*+,;=  ` . Despite our allowing percent encodings, implementations should not unescape them to prevent confusion with existing parsers. For example, `  type.googleapis.com%2FFoo  ` should be rejected.

In the original design of `  Any  ` , the possibility of launching a type resolution service at these type URLs was considered but Protobuf never implemented one and considers contacting these URLs to be problematic and a potential security issue. Do not attempt to contact type URLs.

`  value  `

`  string ( bytes format)  `

Holds a Protobuf serialization of the type described by type\_url.

A base64-encoded string.

### Tool Annotations

Destructive Hint: ❌ | Idempotent Hint: ❌ | Read Only Hint: ❌ | Open World Hint: ❌
