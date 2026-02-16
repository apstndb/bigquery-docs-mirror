  - [Resource: MigrationSubtask](#MigrationSubtask)
      - [JSON representation](#MigrationSubtask.SCHEMA_REPRESENTATION)
  - [State](#State)
  - [Methods](#METHODS_SUMMARY)

## Resource: MigrationSubtask

A subtask for a migration which carries details about the configuration of the subtask. The content of the details should not matter to the end user, but is a contract between the subtask creator and subtask worker.

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
  &quot;taskId&quot;: string,
  &quot;type&quot;: string,
  &quot;state&quot;: enum (State),
  &quot;processingError&quot;: {
    object (ErrorInfo)
  },
  &quot;resourceErrorDetails&quot;: [
    {
      object (ResourceErrorDetail)
    }
  ],
  &quot;resourceErrorCount&quot;: integer,
  &quot;createTime&quot;: string,
  &quot;lastUpdateTime&quot;: string,
  &quot;metrics&quot;: [
    {
      object (TimeSeries)
    }
  ]
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  name  `

`  string  `

Output only. Immutable. The resource name for the migration subtask. The ID is server-generated.

Example: `  projects/123/locations/us/workflows/345/subtasks/678  `

`  taskId  `

`  string  `

The unique ID of the task to which this subtask belongs.

`  type  `

`  string  `

The type of the Subtask. The migration service does not check whether this is a known type. It is up to the task creator (i.e. orchestrator or worker) to ensure it only creates subtasks for which there are compatible workers polling for Subtasks.

`  state  `

`  enum ( State  ` )

Output only. The current state of the subtask.

`  processingError  `

`  object ( ErrorInfo  ` )

Output only. An explanation that may be populated when the task is in FAILED state.

`  resourceErrorDetails[]  `

`  object ( ResourceErrorDetail  ` )

Output only. Provides details to errors and issues encountered while processing the subtask. Presence of error details does not mean that the subtask failed.

`  resourceErrorCount  `

`  integer  `

Output only. The number or resources with errors. Note: This is not the total number of errors as each resource can have more than one error. This is used to indicate truncation by having a `  resourceErrorCount  ` that is higher than the size of `  resourceErrorDetails  ` .

`  createTime  `

`  string ( Timestamp  ` format)

Output only. Time when the subtask was created.

`  lastUpdateTime  `

`  string ( Timestamp  ` format)

Output only. Time when the subtask was last updated.

`  metrics[]  `

`  object ( TimeSeries  ` )

Output only. The metrics for the subtask.

## State

Possible states of a migration subtask.

Enums

`  STATE_UNSPECIFIED  `

The state is unspecified.

`  ACTIVE  `

The subtask is ready, i.e. it is ready for execution.

`  RUNNING  `

The subtask is running, i.e. it is assigned to a worker for execution.

`  SUCCEEDED  `

The subtask finished successfully.

`  FAILED  `

The subtask finished unsuccessfully.

`  PAUSED  `

The subtask is paused, i.e., it will not be scheduled. If it was already assigned,it might still finish but no new lease renewals will be granted.

`  PENDING_DEPENDENCY  `

The subtask is pending a dependency. It will be scheduled once its dependencies are done.

## Methods

### `             get           `

Gets a previously created migration subtask.

### `             list           `

Lists previously created migration subtasks.
