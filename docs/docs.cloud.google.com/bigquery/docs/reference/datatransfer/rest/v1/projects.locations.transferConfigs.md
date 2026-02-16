  - [Resource: TransferConfig](#TransferConfig)
      - [JSON representation](#TransferConfig.SCHEMA_REPRESENTATION)
      - [ScheduleOptions](#TransferConfig.ScheduleOptions)
          - [JSON representation](#TransferConfig.ScheduleOptions.SCHEMA_REPRESENTATION)
      - [ScheduleOptionsV2](#TransferConfig.ScheduleOptionsV2)
          - [JSON representation](#TransferConfig.ScheduleOptionsV2.SCHEMA_REPRESENTATION)
      - [TimeBasedSchedule](#TransferConfig.TimeBasedSchedule)
          - [JSON representation](#TransferConfig.TimeBasedSchedule.SCHEMA_REPRESENTATION)
      - [ManualSchedule](#TransferConfig.ManualSchedule)
      - [EventDrivenSchedule](#TransferConfig.EventDrivenSchedule)
          - [JSON representation](#TransferConfig.EventDrivenSchedule.SCHEMA_REPRESENTATION)
      - [UserInfo](#TransferConfig.UserInfo)
          - [JSON representation](#TransferConfig.UserInfo.SCHEMA_REPRESENTATION)
      - [EncryptionConfiguration](#TransferConfig.EncryptionConfiguration)
          - [JSON representation](#TransferConfig.EncryptionConfiguration.SCHEMA_REPRESENTATION)
      - [ManagedTableType](#TransferConfig.ManagedTableType)
  - [Methods](#METHODS_SUMMARY)

## Resource: TransferConfig

Represents a data transfer configuration. A transfer configuration contains all metadata needed to perform a data transfer. For example, `  destinationDatasetId  ` specifies where data should be stored. When a new transfer configuration is created, the specified `  destinationDatasetId  ` is created when needed and shared with the appropriate data source service account.

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
  &quot;ownerInfo&quot;: {
    object (UserInfo)
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  name  `

`  string  `

Identifier. The resource name of the transfer config. Transfer config names have the form either `  projects/{projectId}/locations/{region}/transferConfigs/{configId}  ` or `  projects/{projectId}/transferConfigs/{configId}  ` , where `  configId  ` is usually a UUID, even though it is not guaranteed or required. The name is ignored when creating a transfer config.

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

Options customizing different types of data transfer schedule. This field replaces "schedule" and "scheduleOptions" fields. ScheduleOptionsV2 cannot be used together with ScheduleOptions/Schedule.

`  dataRefreshWindowDays  `

`  integer  `

The number of days to look back to automatically refresh the data. For example, if `  dataRefreshWindowDays = 10  ` , then every day BigQuery reingests data for \[today-10, today-1\], rather than ingesting data for just \[today-1\]. Only valid if the data source supports the feature. Set the value to 0 to use the default value.

`  disabled  `

`  boolean  `

Is this config disabled. When set to true, no runs will be scheduled for this transfer config.

`  updateTime  `

`  string ( Timestamp  ` format)

Output only. Data transfer modification time. Ignored by server on input.

`  nextRunTime  `

`  string ( Timestamp  ` format)

Output only. Next time when data transfer will run.

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

The format for specifying a pubsub topic is: `  projects/{projectId}/topics/{topic_id}  `

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

`  ownerInfo  `

`  object ( UserInfo  ` )

Output only. Information about the user whose credentials are used to transfer data. Populated only for `  transferConfigs.get  ` requests. In case the user information is not available, this field will not be populated.

### ScheduleOptions

Options customizing the data transfer schedule.

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

If true, automatic scheduling of data transfer runs for this configuration will be disabled. The runs can be started on ad-hoc basis using transferConfigs.startManualRuns API. When automatic scheduling is disabled, the TransferConfig.schedule field will be ignored.

`  startTime  `

`  string ( Timestamp  ` format)

Specifies time to start scheduling transfer runs. The first run will be scheduled at or after the start time according to a recurrence pattern defined in the schedule string. The start time can be changed at any moment. The time when a data transfer can be triggered manually is not limited by this option.

`  endTime  `

`  string ( Timestamp  ` format)

Defines time to stop scheduling transfer runs. A transfer run cannot be scheduled at or after the end time. The end time can be changed at any moment. The time when a data transfer can be triggered manually is not limited by this option.

### ScheduleOptionsV2

V2 options customizing different types of data transfer schedule. This field supports existing time-based and manual transfer schedule. Also supports Event-Driven transfer schedule. ScheduleOptionsV2 cannot be used together with ScheduleOptions/Schedule.

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

Manual transfer schedule. If set, the transfer run will not be auto-scheduled by the system, unless the client invokes transferConfigs.startManualRuns. This is equivalent to disableAutoScheduling = true.

`  eventDrivenSchedule  `

`  object ( EventDrivenSchedule  ` )

Event driven transfer schedule options. If set, the transfer will be scheduled upon events arrial.

### TimeBasedSchedule

Options customizing the time based transfer schedule. Options are migrated from the original ScheduleOptions message.

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

`  endTime  `

`  string ( Timestamp  ` format)

Defines time to stop scheduling transfer runs. A transfer run cannot be scheduled at or after the end time. The end time can be changed at any moment.

### ManualSchedule

This type has no fields.

Options customizing manual transfers schedule.

### EventDrivenSchedule

Options customizing EventDriven transfers schedule.

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

### UserInfo

Information about a user.

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
  &quot;email&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  email  `

`  string  `

E-mail address of the user.

### EncryptionConfiguration

Represents the encryption configuration for a transfer.

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

### ManagedTableType

The classifications of managed tables that can be created, native or BigLake.

Enums

`  MANAGED_TABLE_TYPE_UNSPECIFIED  `

Type unspecified. This defaults to `  NATIVE  ` table.

`  NATIVE  `

The managed table is a native BigQuery table. This is the default value.

`  BIGLAKE  `

The managed table is a BigQuery table for Apache Iceberg (formerly BigLake managed tables), with a BigLake configuration.

## Methods

### `             create           `

Creates a new data transfer configuration.

### `             delete           `

Deletes a data transfer configuration, including any associated transfer runs and logs.

### `             get           `

Returns information about a data transfer config.

### `             list           `

Returns information about all transfer configs owned by a project in the specified location.

### `             patch           `

Updates a data transfer configuration.

### `             scheduleRuns                       (deprecated)           `

Creates transfer runs for a time range \[start\_time, end\_time\].

### `             startManualRuns           `

Manually initiates transfer runs.
