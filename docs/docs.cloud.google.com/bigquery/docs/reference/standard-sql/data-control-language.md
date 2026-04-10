# Data control language (DCL) statements in GoogleSQL

The BigQuery data control language (DCL) statements let you set up and control BigQuery resources using [GoogleSQL](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql) query syntax.

Use these statements to give or remove access to BigQuery resources.

For more information on controlling access to specific BigQuery resources, see:

  - [Controlling access to datasets](https://docs.cloud.google.com/bigquery/docs/dataset-access-controls)
  - [Controlling access to tables](https://docs.cloud.google.com/bigquery/docs/table-access-controls)
  - [Controlling access to views](https://docs.cloud.google.com/bigquery/docs/authorized-views)

## Permissions required

The following permissions are required to run `  GRANT  ` and `  REVOKE  ` statements.

| Resource Type | Permissions                                              |
| ------------- | -------------------------------------------------------- |
| Dataset       | `        bigquery.datasets.update       `                |
| Table         | `        bigquery.tables.setIamPolicy       `            |
| View          | `        bigquery.tables.setIamPolicy       `            |
| Project       | `         resourcemanager.projects.setIamPolicy        ` |

## `     GRANT    ` statement

Grants roles to users on BigQuery resources.

### Syntax

    GRANT role_list
      ON resource_type resource_name
      TO user_list

### Arguments

  - `  role_list  ` : A role or list of comma separated roles that contains the permissions you want to grant. For more information on the types of roles available, see [Roles and permissions](https://docs.cloud.google.com/iam/docs/roles-overview) .

  - `  resource_type  ` : The type of resource the role is applied to. Supported values include: `  SCHEMA  ` (equivalent to dataset), `  TABLE  ` , `  VIEW  ` , `  EXTERNAL TABLE  ` , and `  PROJECT  ` .

  - `  resource_name  ` : The name of the resource you want to grant the permission on.

  - [`  user_list  `](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-control-language#user_list) : A comma separated list of users that the role is granted to.

### `     user_list    `

Specify users using the following formats:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>User Type</th>
<th>Syntax</th>
<th>Example</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Google account</td>
<td><code dir="ltr" translate="no">       user:               $user@$domain       </code></td>
<td><code dir="ltr" translate="no">       user:first.last@example.com      </code></td>
</tr>
<tr class="even">
<td>Google group</td>
<td><code dir="ltr" translate="no">       group:               $group@$domain       </code></td>
<td><code dir="ltr" translate="no">       group:my-group@example.com      </code></td>
</tr>
<tr class="odd">
<td>Service account</td>
<td><code dir="ltr" translate="no">       serviceAccount:               $user@$project.iam.gserviceaccount.com       </code></td>
<td><code dir="ltr" translate="no">       serviceAccount:robot@example.iam.gserviceaccount.com      </code></td>
</tr>
<tr class="even">
<td>Google domain</td>
<td><code dir="ltr" translate="no">       domain:               $domain       </code></td>
<td><code dir="ltr" translate="no">       domain:example.com      </code></td>
</tr>
<tr class="odd">
<td>All Google accounts</td>
<td><code dir="ltr" translate="no">       specialGroup:               allAuthenticatedUsers       </code></td>
<td><code dir="ltr" translate="no">       specialGroup:allAuthenticatedUsers      </code></td>
</tr>
<tr class="even">
<td>All users</td>
<td><code dir="ltr" translate="no">       specialGroup:               allUsers       </code></td>
<td><code dir="ltr" translate="no">       specialGroup:allUsers      </code></td>
</tr>
<tr class="odd">
<td>Connection</td>
<td><p><code dir="ltr" translate="no">        connection:                 [$project_id.]$location.$connection_id        </code></p>
<p>If <code dir="ltr" translate="no">          $project_id        </code> is omitted, the project where you run this DCL statement is used.</p></td>
<td><code dir="ltr" translate="no">       connection:my-bq-project.us.my-connection      </code></td>
</tr>
</tbody>
</table>

For more information about each type of user in the table, see [Concepts related to identity](https://docs.cloud.google.com/iam/docs/overview#concepts_related_identity) .

### Examples

The following example grants the `  bigquery.dataViewer  ` role to the users `  raha@example-pet-store.com  ` and `  sasha@example-pet-store.com  ` on a dataset named `  myDataset  ` :

    GRANT `roles/bigquery.dataViewer` ON SCHEMA `myProject`.myDataset
    TO "user:raha@example-pet-store.com", "user:sasha@example-pet-store.com"

The following example grants the `  aiplatform.user  ` and `  run.invoker  ` roles to the `  my-connection  ` and `  other-connection  ` connections on the `  my-vertex-project  ` project:

    GRANT `roles/aiplatform.user`, `roles/run.invoker`
    ON PROJECT `my-vertex-project`
    TO "connection:my-bq-project.us.my-connection", "connection:another-bq-project.eu.other-connection";

## `     REVOKE    ` statement

Removes roles from a list of users on BigQuery resources.

### Syntax

    REVOKE role_list
      ON resource_type resource_name
      FROM user_list

### Arguments

  - `  role_list  ` : A role or list of comma separated roles that contains the permissions you want to remove. For more information on the types of roles available, see [Roles and permissions](https://docs.cloud.google.com/iam/docs/roles-overview) .

  - `  resource_type  ` : The type of resource that the role will be removed from. Supported values include: `  SCHEMA  ` (equivalent to dataset), `  TABLE  ` , `  VIEW  ` , `  EXTERNAL TABLE  ` , and `  PROJECT  ` .

  - `  resource_name  ` : The name of the resource you want to revoke the role on.

  - [`  user_list  `](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-control-language#user_list) : A comma separated list of users that the role is revoked from.

### Examples

The following example removes the `  bigquery.admin  ` role on the `  myDataset  ` dataset from the `  example-team@example-pet-store.com  ` group and a service account:

    REVOKE `roles/bigquery.admin` ON SCHEMA `myProject`.myDataset
    FROM "group:example-team@example-pet-store.com", "serviceAccount:user@test-project.iam.gserviceaccount.com"

The following example revokes the `  run.invoker  ` role on the `  my-vertex-project  ` project from the `  my-connection  ` connection:

    REVOKE `roles/run.invoker`
    ON PROJECT `my-vertex-project`
    FROM "connection:my-bq-project.us.my-connection";
