---
name: documents/docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations.assignments
uri: https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations.assignments
title: 'REST Resource: projects.locations.reservations.assignments'
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

- [Resource: Assignment](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations.assignments#Assignment)
  - [JSON representation](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations.assignments#Assignment.SCHEMA_REPRESENTATION)
- [JobType](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations.assignments#JobType)
- [State](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations.assignments#State)
- [Methods](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations.assignments#METHODS_SUMMARY)

## Resource: Assignment

An assignment allows a project to submit jobs of a certain type using slots from the specified reservation.

**JSON representation**

```
{
  "name": string,
  "assignee": string,
  "jobType": enum (JobType),
  "state": enum (State),
  "schedulingPolicy": {
    object (SchedulingPolicy)
  },
  "principal": string
}
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>name</code></td>
<td><p><code>string</code></p>
<p>Output only. Name of the resource. E.g.: <code>projects/myproject/locations/US/reservations/team1-prod/assignments/123</code> . The assignmentId must only contain lower case alphanumeric characters or dashes and the max length is 64 characters.</p></td>
</tr>
<tr class="even">
<td><code>assignee</code></td>
<td><p><code>string</code></p>
<p>Optional. The resource which will use the reservation. E.g. <code>projects/myproject</code> , <code>folders/123</code> , or <code>organizations/456</code> .</p></td>
</tr>
<tr class="odd">
<td><code>jobType</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations.assignments#JobType"><code>JobType</code></a><code> )</code></p>
<p>Optional. Which type of jobs will use the reservation.</p></td>
</tr>
<tr class="even">
<td><code>state</code></td>
<td><p><code>enum ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations.assignments#State"><code>State</code></a><code> )</code></p>
<p>Output only. State of the assignment.</p></td>
</tr>
<tr class="odd">
<td><code>schedulingPolicy</code></td>
<td><p><code>object ( </code><a href="https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/SchedulingPolicy"><code>SchedulingPolicy</code></a><code> )</code></p>
<p>Optional. The scheduling policy to use for jobs and queries of this assignee when running under the associated reservation. The scheduling policy controls how the reservation's resources are distributed. This overrides the default scheduling policy specified on the reservation.</p>
<p>This feature is not yet generally available.</p></td>
</tr>
<tr class="even">
<td><code>principal</code></td>
<td><p><code>string</code></p>
<p>Optional. Represents the principal for this assignment. If not empty, jobs run by this principal utilize the associated reservation. Otherwise, jobs fall back to using the reservation assigned to the project, folder, or organization, in that order. If no reservation is assigned at any of these levels, on-demand capacity is used.</p>
<p>The supported formats are:</p>
<ul>
<li><code>principal://goog/subject/USER_EMAIL_ADDRESS</code> for users,</li>
<li><code>principal://iam.googleapis.com/projects/-/serviceAccounts/SA_EMAIL_ADDRESS</code> for service accounts,</li>
<li><code>principal://iam.googleapis.com/projects/PROJECT_NUMBER/locations/global/workloadIdentityPools/POOL_ID/subject/SUBJECT_ID</code> for workload identity pool identities.</li>
<li>The special value <code>unknown_or_deleted_user</code> represents principals which cannot be read from the user info service, for example, deleted users.</li>
</ul></td>
</tr>
</tbody>
</table>

## JobType

Types of job, which could be specified when using the reservation.

| Enums                                 |                                                                                                                                                                                                                               |
|---------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `JOB_TYPE_UNSPECIFIED`                | Invalid type. Requests with this value will be rejected with error code `google.rpc.Code.INVALID_ARGUMENT` .                                                                                                                  |
| `PIPELINE`                            | Pipeline (load/export) jobs from the project will use the reservation.                                                                                                                                                        |
| `QUERY`                               | Query jobs from the project will use the reservation.                                                                                                                                                                         |
| `ML_EXTERNAL`                         | BigQuery ML jobs that use services external to BigQuery for model training. These jobs will not utilize idle slots from other reservations.                                                                                   |
| `BACKGROUND`                          | Background jobs that BigQuery runs for the customers in the background.                                                                                                                                                       |
| `CONTINUOUS`                          | Continuous SQL jobs will use this reservation. Reservations with continuous assignments cannot be mixed with non-continuous assignments.                                                                                      |
| `BACKGROUND_CHANGE_DATA_CAPTURE`      | Finer granularity background jobs for capturing changes in a source database and streaming them into BigQuery. Reservations with this job type take priority over a default BACKGROUND reservation assignment (if it exists). |
| `BACKGROUND_COLUMN_METADATA_INDEX`    | Finer granularity background jobs for refreshing cached metadata for BigQuery tables. Reservations with this job type take priority over a default BACKGROUND reservation assignment (if it exists).                          |
| `BACKGROUND_SEARCH_INDEX_REFRESH`     | Finer granularity background jobs for refreshing search indexes upon BigQuery table columns. Reservations with this job type take priority over a default BACKGROUND reservation assignment (if it exists).                   |
| `AUTOMATIC_MATERIALIZED_VIEW_REFRESH` | Automated materialized view refresh jobs will use the reservation. Reservations with this job type will take priority over a default QUERY reservation assignment (if it exists).                                             |

## State

Assignment will remain in PENDING state if no active capacity commitment is present. It will become ACTIVE when some capacity commitment becomes active.

| Enums               |                                                                                        |
|---------------------|----------------------------------------------------------------------------------------|
| `STATE_UNSPECIFIED` | Invalid state value.                                                                   |
| `PENDING`           | Queries from assignee will be executed as on-demand, if related assignment is pending. |
| `ACTIVE`            | Assignment is ready.                                                                   |

| Methods                                                                                                                                                           |                                                                                                                                          |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| [`create`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations.assignments/create)                         | Creates an assignment object which allows the given project to submit jobs of a certain type using slots from the specified reservation. |
| [`delete`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations.assignments/delete)                         | Deletes a assignment.                                                                                                                    |
| [`getIamPolicy`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations.assignments/getIamPolicy)             | Gets the access control policy for a resource.                                                                                           |
| [`list`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations.assignments/list)                             | Lists assignments.                                                                                                                       |
| [`move`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations.assignments/move)                             | Moves an assignment under a new reservation.                                                                                             |
| [`patch`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations.assignments/patch)                           | Updates an existing assignment.                                                                                                          |
| [`setIamPolicy`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations.assignments/setIamPolicy)             | Sets an access control policy for a resource.                                                                                            |
| [`testIamPermissions`](https://docs.cloud.google.com/bigquery/docs/reference/reservations/rest/v1/projects.locations.reservations.assignments/testIamPermissions) | Gets your permissions on a resource.                                                                                                     |
