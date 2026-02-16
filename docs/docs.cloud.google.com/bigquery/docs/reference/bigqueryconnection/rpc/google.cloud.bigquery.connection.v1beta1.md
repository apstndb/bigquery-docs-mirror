## Index

  - `  ConnectionService  ` (interface)
  - `  CloudSqlCredential  ` (message)
  - `  CloudSqlProperties  ` (message)
  - `  CloudSqlProperties.DatabaseType  ` (enum)
  - `  Connection  ` (message)
  - `  ConnectionCredential  ` (message)
  - `  CreateConnectionRequest  ` (message)
  - `  DeleteConnectionRequest  ` (message)
  - `  GetConnectionRequest  ` (message)
  - `  ListConnectionsRequest  ` (message)
  - `  ListConnectionsResponse  ` (message)
  - `  UpdateConnectionCredentialRequest  ` (message)
  - `  UpdateConnectionRequest  ` (message)

## ConnectionService

Manages external data source connections and credentials.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>CreateConnection</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc CreateConnection(                         CreateConnectionRequest            </code> ) returns ( <code dir="ltr" translate="no">              Connection            </code> )</p>
<p>Creates a new connection.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/bigquery             </code></li>
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
<th>DeleteConnection</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc DeleteConnection(                         DeleteConnectionRequest            </code> ) returns ( <code dir="ltr" translate="no">              Empty            </code> )</p>
<p>Deletes connection and associated credential.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/bigquery             </code></li>
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
<th>GetConnection</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc GetConnection(                         GetConnectionRequest            </code> ) returns ( <code dir="ltr" translate="no">              Connection            </code> )</p>
<p>Returns specified connection.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/bigquery             </code></li>
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
<th>GetIamPolicy</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc GetIamPolicy(                         GetIamPolicyRequest            </code> ) returns ( <code dir="ltr" translate="no">              Policy            </code> )</p>
<p>Gets the access control policy for a resource. Returns an empty policy if the resource exists and does not have a policy set.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/bigquery             </code></li>
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
<th>ListConnections</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc ListConnections(                         ListConnectionsRequest            </code> ) returns ( <code dir="ltr" translate="no">              ListConnectionsResponse            </code> )</p>
<p>Returns a list of connections in the given project.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/bigquery             </code></li>
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
<th>SetIamPolicy</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc SetIamPolicy(                         SetIamPolicyRequest            </code> ) returns ( <code dir="ltr" translate="no">              Policy            </code> )</p>
<p>Sets the access control policy on the specified resource. Replaces any existing policy.</p>
<p>Can return <code dir="ltr" translate="no">           NOT_FOUND          </code> , <code dir="ltr" translate="no">           INVALID_ARGUMENT          </code> , and <code dir="ltr" translate="no">           PERMISSION_DENIED          </code> errors.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/bigquery             </code></li>
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
<th>TestIamPermissions</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc TestIamPermissions(                         TestIamPermissionsRequest            </code> ) returns ( <code dir="ltr" translate="no">              TestIamPermissionsResponse            </code> )</p>
<p>Returns permissions that a caller has on the specified resource. If the resource does not exist, this will return an empty set of permissions, not a <code dir="ltr" translate="no">           NOT_FOUND          </code> error.</p>
<p>Note: This operation is designed to be used for building permission-aware UIs and command-line tools, not for authorization checking. This operation may "fail open" without warning.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/bigquery             </code></li>
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
<th>UpdateConnection</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc UpdateConnection(                         UpdateConnectionRequest            </code> ) returns ( <code dir="ltr" translate="no">              Connection            </code> )</p>
<p>Updates the specified connection. For security reasons, also resets credential if connection properties are in the update field mask.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/bigquery             </code></li>
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
<th>UpdateConnectionCredential</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code dir="ltr" translate="no">           rpc UpdateConnectionCredential(                         UpdateConnectionCredentialRequest            </code> ) returns ( <code dir="ltr" translate="no">              Empty            </code> )</p>
<p>Sets the credential for the specified connection.</p>
<dl>
<dt>Authorization scopes</dt>
<dd><p>Requires one of the following OAuth scopes:</p>
<ul>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/bigquery             </code></li>
<li><code dir="ltr" translate="no">              https://www.googleapis.com/auth/cloud-platform             </code></li>
</ul>
<p>For more information, see the <a href="/docs/authentication#authorization-gcp">Authentication Overview</a> .</p>
</dd>
</dl></td>
</tr>
</tbody>
</table>

## CloudSqlCredential

Credential info for the Cloud SQL.

Fields

`  username  `

`  string  `

The username for the credential.

`  password  `

`  string  `

The password for the credential.

## CloudSqlProperties

Connection properties specific to the Cloud SQL.

Fields

`  instance_id  `

`  string  `

Cloud SQL instance ID in the form `  project:location:instance  ` .

`  database  `

`  string  `

Database name.

`  type  `

`  DatabaseType  `

Type of the Cloud SQL database.

`  credential  `

`  CloudSqlCredential  `

Input only. Cloud SQL credential.

`  service_account_id  `

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

## Connection

Configuration parameters to establish connection with an external data source, except the credential attributes.

Fields

`  name  `

`  string  `

The resource name of the connection in the form of: `  projects/{project_id}/locations/{location_id}/connections/{connection_id}  `

`  friendly_name  `

`  string  `

User provided display name for the connection.

`  description  `

`  string  `

User provided description.

`  creation_time  `

`  int64  `

Output only. The creation timestamp of the connection.

`  last_modified_time  `

`  int64  `

Output only. The last update timestamp of the connection.

`  has_credential  `

`  bool  `

Output only. True, if credential is configured for this connection.

Union field `  properties  ` . Properties specific to the underlying data source. `  properties  ` can be only one of the following:

`  cloud_sql  `

`  CloudSqlProperties  `

Cloud SQL properties.

## ConnectionCredential

Credential to use with a connection.

Fields

Union field `  credential  ` . Credential specific to the underlying data source. `  credential  ` can be only one of the following:

`  cloud_sql  `

`  CloudSqlCredential  `

Credential for Cloud SQL database.

## CreateConnectionRequest

The request for `  ConnectionService.CreateConnection  ` .

Fields

`  parent  `

`  string  `

Required. Parent resource name. Must be in the format `  projects/{project_id}/locations/{location_id}  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  parent  ` :

  - `  bigquery.connections.create  `

`  connection_id  `

`  string  `

Optional. Connection id that should be assigned to the created connection.

`  connection  `

`  Connection  `

Required. Connection to create.

## DeleteConnectionRequest

The request for \[ConnectionService.DeleteConnectionRequest\]\[\].

Fields

`  name  `

`  string  `

Required. Name of the deleted connection, for example: `  projects/{project_id}/locations/{location_id}/connections/{connection_id}  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  name  ` :

  - `  bigquery.connections.delete  `

## GetConnectionRequest

The request for `  ConnectionService.GetConnection  ` .

Fields

`  name  `

`  string  `

Required. Name of the requested connection, for example: `  projects/{project_id}/locations/{location_id}/connections/{connection_id}  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  name  ` :

  - `  bigquery.connections.get  `

## ListConnectionsRequest

The request for `  ConnectionService.ListConnections  ` .

Fields

`  parent  `

`  string  `

Required. Parent resource name. Must be in the form: `  projects/{project_id}/locations/{location_id}  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  parent  ` :

  - `  bigquery.connections.list  `

`  max_results  `

`  UInt32Value  `

Required. Maximum number of results per page.

`  page_token  `

`  string  `

Page token.

## ListConnectionsResponse

The response for `  ConnectionService.ListConnections  ` .

Fields

`  next_page_token  `

`  string  `

Next page token.

`  connections[]  `

`  Connection  `

List of connections.

## UpdateConnectionCredentialRequest

The request for `  ConnectionService.UpdateConnectionCredential  ` .

Fields

`  name  `

`  string  `

Required. Name of the connection, for example: `  projects/{project_id}/locations/{location_id}/connections/{connection_id}/credential  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  name  ` :

  - `  bigquery.connections.update  `

`  credential  `

`  ConnectionCredential  `

Required. Credential to use with the connection.

## UpdateConnectionRequest

The request for `  ConnectionService.UpdateConnection  ` .

Fields

`  name  `

`  string  `

Required. Name of the connection to update, for example: `  projects/{project_id}/locations/{location_id}/connections/{connection_id}  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  name  ` :

  - `  bigquery.connections.update  `

`  connection  `

`  Connection  `

Required. Connection containing the updated fields.

`  update_mask  `

`  FieldMask  `

Required. Update mask for the connection fields to be updated.
