# Introduction to sessions

This guide describes how to enable, create, and track changes in a BigQuery session. It is intended for users who are familiar with [BigQuery](/bigquery/docs) and [GoogleSQL](/bigquery/docs/reference/standard-sql/query-syntax) .

You can capture your SQL activities in a BigQuery session. Temporary tables, temporary functions, and variables can be used throughout the session to interactively build one or more queries. Multiple sessions can be active at the same time and the history for each session is saved. You can view the history of a session for up to 20 days after the session is terminated.

Typical uses for a session include the following:

  - **Maintain transient session data.** Define variables and temporary tables once and use them throughout the session.

  - **Look up query history by session.** If you want to keep track of a behavior that happened at a particular time during the session, you can view the history of changes that were made during the session.

  - **Create multi-statement transactions over multiple queries.** Within a session, you can begin a transaction, make changes, and view the temporary result before deciding to commit or rollback. You can do this over several queries in the session. If you don't use a session, a multi-statement transaction needs to be completed in a single query.

## Pricing

  - There are no additional costs for using sessions.

  - For projects that use on-demand pricing, queries against `  INFORMATION_SCHEMA  ` incur charges. For more information, see [`  INFORMATION_SCHEMA  ` pricing](/bigquery/docs/information-schema-intro#pricing) .

  - You are charged for temporary tables that you create in sessions. Storage charges are based on how much data is stored in the tables. For information about storage pricing, see [Storage pricing](https://cloud.google.com/bigquery/pricing#storage) .

## Limitations

  - Every query in a session is run in the location where the session was created.

  - A session is automatically terminated after 24 hours of inactivity.

  - A session is automatically terminated 7 days after its creation.

  - The maximum size of a session variable is 1 MB, and the maximum size of all variables used in a session is 10 MB.

  - Concurrent queries aren't allowed within a session.

## Roles and permissions

This section describes the [Identity and Access Management (IAM) permissions](/bigquery/docs/access-control#bq-permissions) and the [IAM roles](/bigquery/docs/access-control#bigquery) that you need to perform actions with sessions.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Actions</th>
<th>Required permissions</th>
<th>Default roles</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Create a new session. Work with an existing session that you created.</td>
<td><code dir="ltr" translate="no">       bigquery.jobs.create      </code></td>
<td><code dir="ltr" translate="no">       bigquery.user      </code><br />
<code dir="ltr" translate="no">       bigquery.Jobuser      </code><br />
<code dir="ltr" translate="no">       bigquery.admin      </code><br />
</td>
</tr>
<tr class="even">
<td>Terminate a session that you created.</td>
<td><code dir="ltr" translate="no">       bigquery.jobs.create      </code></td>
<td><code dir="ltr" translate="no">       bigquery.user      </code><br />
<code dir="ltr" translate="no">       bigquery.Jobuser      </code><br />
<code dir="ltr" translate="no">       bigquery.admin      </code><br />
</td>
</tr>
<tr class="odd">
<td>Terminate a session another user created.</td>
<td><code dir="ltr" translate="no">       bigquery.jobs.create      </code><br />
<code dir="ltr" translate="no">       bigquery.jobs.update      </code><br />
</td>
<td><code dir="ltr" translate="no">       bigquery.admin      </code><br />
</td>
</tr>
<tr class="even">
<td>View a list of your sessions in a project. This list includes the IDs for sessions you've created in a project with <code dir="ltr" translate="no">         INFORMATION_SCHEMA.JOBS_BY_USER       </code> .</td>
<td><code dir="ltr" translate="no">       bigquery.jobs.list      </code></td>
<td><code dir="ltr" translate="no">       bigquery.user      </code><br />
<code dir="ltr" translate="no">       bigquery.Jobuser      </code><br />
<code dir="ltr" translate="no">       bigquery.admin      </code><br />
</td>
</tr>
<tr class="odd">
<td>View all sessions for all users in a project. This list includes the IDs for all sessions created in the project with <code dir="ltr" translate="no">         INFORMATION_SCHEMA.JOBS       </code> .</td>
<td><code dir="ltr" translate="no">       bigquery.jobs.listAll      </code></td>
<td><code dir="ltr" translate="no">       bigquery.admin      </code></td>
</tr>
<tr class="even">
<td>View metadata for sessions created by the current user in the current project with <code dir="ltr" translate="no">         INFORMATION_SCHEMA.SESSIONS_BY_USER       </code> .</td>
<td><code dir="ltr" translate="no">       bigquery.jobs.list      </code></td>
<td><code dir="ltr" translate="no">       bigquery.user      </code><br />
<code dir="ltr" translate="no">       bigquery.Jobuser      </code><br />
<code dir="ltr" translate="no">       bigquery.admin      </code><br />
</td>
</tr>
<tr class="odd">
<td>View metadata for all sessions in the current project with <code dir="ltr" translate="no">         INFORMATION_SCHEMA.SESSIONS_BY_PROJECT       </code> .</td>
<td><code dir="ltr" translate="no">       bigquery.jobs.listAll      </code></td>
<td><code dir="ltr" translate="no">       bigquery.admin      </code></td>
</tr>
</tbody>
</table>

## What's next

  - Learn more about how to [write queries in sessions](/bigquery/docs/sessions-write-queries) .
  - Learn more about how to [work with sessions](/bigquery/docs/sessions) , including how to create, use, terminate, and list your sessions.
