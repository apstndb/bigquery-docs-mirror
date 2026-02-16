  - [Resource: Connection](#Connection)
      - [JSON representation](#Connection.SCHEMA_REPRESENTATION)
  - [CloudSqlProperties](#CloudSqlProperties)
      - [JSON representation](#CloudSqlProperties.SCHEMA_REPRESENTATION)
  - [DatabaseType](#DatabaseType)
  - [CloudSqlCredential](#CloudSqlCredential)
      - [JSON representation](#CloudSqlCredential.SCHEMA_REPRESENTATION)
  - [Methods](#METHODS_SUMMARY)

## Resource: Connection

Configuration parameters to establish connection with an external data source, except the credential attributes.

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
  &quot;friendlyName&quot;: string,
  &quot;description&quot;: string,
  &quot;creationTime&quot;: string,
  &quot;lastModifiedTime&quot;: string,
  &quot;hasCredential&quot;: boolean,

  // Union field properties can be only one of the following:
  &quot;cloudSql&quot;: {
    object (CloudSqlProperties)
  }
  // End of list of possible types for union field properties.
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  name  `

`  string  `

The resource name of the connection in the form of: `  projects/{projectId}/locations/{locationId}/connections/{connectionId}  `

`  friendlyName  `

`  string  `

User provided display name for the connection.

`  description  `

`  string  `

User provided description.

`  creationTime  `

`  string ( int64 format)  `

Output only. The creation timestamp of the connection.

`  lastModifiedTime  `

`  string ( int64 format)  `

Output only. The last update timestamp of the connection.

`  hasCredential  `

`  boolean  `

Output only. True, if credential is configured for this connection.

Union field `  properties  ` . Properties specific to the underlying data source. `  properties  ` can be only one of the following:

`  cloudSql  `

`  object ( CloudSqlProperties  ` )

Cloud SQL properties.

## CloudSqlProperties

Connection properties specific to the Cloud SQL.

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
  &quot;instanceId&quot;: string,
  &quot;database&quot;: string,
  &quot;type&quot;: enum (DatabaseType),
  &quot;credential&quot;: {
    object (CloudSqlCredential)
  },
  &quot;serviceAccountId&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  instanceId  `

`  string  `

Cloud SQL instance ID in the form `  project:location:instance  ` .

`  database  `

`  string  `

Database name.

`  type  `

`  enum ( DatabaseType  ` )

Type of the Cloud SQL database.

`  credential  `

`  object ( CloudSqlCredential  ` )

Input only. Cloud SQL credential.

`  serviceAccountId  `

`  string  `

Output only. The account ID of the service used for the purpose of this connection.

When the connection is used in the context of an operation in BigQuery, this service account will serve as the identity being used for connecting to the CloudSQL instance specified in this connection.

## DatabaseType

Supported Cloud SQL database types.

Enums

`  DATABASE_TYPE_UNSPECIFIED  `

Unspecified database type.

`  POSTGRES  `

Cloud SQL for PostgreSQL.

`  MYSQL  `

Cloud SQL for MySQL.

## CloudSqlCredential

Credential info for the Cloud SQL.

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
  &quot;username&quot;: string,
  &quot;password&quot;: string
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  username  `

`  string  `

The username for the credential.

`  password  `

`  string  `

The password for the credential.

## Methods

### `             create           `

Creates a new connection.

### `             delete           `

Deletes connection and associated credential.

### `             get           `

Returns specified connection.

### `             getIamPolicy           `

Gets the access control policy for a resource.

### `             list           `

Returns a list of connections in the given project.

### `             patch           `

Updates the specified connection.

### `             setIamPolicy           `

Sets the access control policy on the specified resource.

### `             testIamPermissions           `

Returns permissions that a caller has on the specified resource.

### `             updateCredential           `

Sets the credential for the specified connection.
