# Basic roles and permissions

BigQuery supports IAM [basic roles](/iam/docs/roles-overview#basic) for project-level access.

**Caution:** Avoid using basic roles. They predate IAM and grant excessive and uneven access. Use [predefined IAM](/bigquery/docs/access-control) roles instead.

## Basic roles for projects

By default, granting access to a project also grants access to datasets within it. Default access can be overridden on a per-dataset basis. The following table describes what access is granted to members of the basic IAM roles.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Basic role</th>
<th>Capabilities</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       Viewer      </code></td>
<td><ul>
<li>Can start a job in the project. Additional dataset roles are required depending on the job type.</li>
<li>Can list and get all jobs, and update jobs that they started for the project</li>
<li>If you create a dataset in a project that contains any viewers, BigQuery grants those users the <a href="/bigquery/docs/access-control#bigquery.dataViewer">bigquery.dataViewer</a> predefined role for the new dataset.</li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       Editor      </code></td>
<td><ul>
<li>Same as <code dir="ltr" translate="no">         Viewer        </code> , plus:
<ul>
<li>Can create a new dataset in the project</li>
<li>If you create a dataset in a project that contains any editors, BigQuery grants those users the <a href="/bigquery/docs/access-control#bigquery.dataEditor">bigquery.dataEditor</a> predefined role for the new dataset.</li>
</ul></li>
</ul></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       Owner      </code></td>
<td><ul>
<li>Same as <code dir="ltr" translate="no">         Editor        </code> , plus:
<ul>
<li>Can revoke or change any project role</li>
<li>Can list all datasets in the project</li>
<li>Can delete any dataset in the project</li>
<li>Can list and get all jobs run on the project, including jobs run by other project users</li>
<li><p>If you create a dataset, BigQuery grants all project owners the <a href="/bigquery/docs/access-control#bigquery.dataOwner">bigquery.dataOwner</a> predefined role for the new dataset.</p>
<p><strong>Exception:</strong> When a user runs a query, an <a href="/bigquery/docs/cached-results#how_cached_results_are_stored">anonymous dataset</a> is created to store the cached results table. Only the user that runs the query is given <code dir="ltr" translate="no">            OWNER           </code> access to the anonymous dataset.</p></li>
</ul></li>
</ul>
Don't confuse the <code dir="ltr" translate="no">        OWNER       </code> basic role with the <a href="/bigquery/docs/access-control#bigquery.admin">BigQuery Admin</a> ( <code dir="ltr" translate="no">        roles/bigquery.admin       </code> ) IAM role. BigQuery Admin provides a number of permissions that aren't granted by the <code dir="ltr" translate="no">        OWNER       </code> basic role. If you're granting project-level access to BigQuery, use IAM roles instead of basic roles.</td>
</tr>
</tbody>
</table>

Basic roles for projects are granted or revoked through the [Google Cloud console](https://console.cloud.google.com/) . When a project is created, the `  Owner  ` role is granted to the user who created the project.

For more information about how to grant or revoke access for project roles, see [Granting, changing, and revoking access to resources](/iam/docs/granting-changing-revoking-access) in the IAM documentation.

## Basic roles for datasets

The following basic roles apply at the dataset level.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Dataset role</th>
<th>Capabilities</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       READER      </code></td>
<td><ul>
<li>Can read, query, copy or export tables in the dataset. Can read routines in the dataset
<ul>
<li>Can call <a href="/bigquery/docs/reference/v2/datasets/get">get</a> on the dataset</li>
<li>Can call <a href="/bigquery/docs/reference/v2/tables/get">get</a> and <a href="/bigquery/docs/reference/v2/tables/list">list</a> on tables in the dataset</li>
<li>Can call <a href="/bigquery/docs/reference/v2/routines/get">get</a> and <a href="/bigquery/docs/reference/v2/routines/list">list</a> on routines in the dataset</li>
<li>Can call <a href="/bigquery/docs/reference/v2/tabledata/list">list</a> on table data for tables in the dataset</li>
</ul></li>
</ul>
The <a href="/bigquery/docs/access-control#bigquery.dataViewer">BigQuery Data Viewer</a> ( <code dir="ltr" translate="no">        roles/bigquery.dataViewer       </code> ) predefined IAM role is mapped to the <code dir="ltr" translate="no">        READER       </code> BigQuery basic role. When you grant BigQuery Data Viewer to a principal at the dataset level, the principal is granted <code dir="ltr" translate="no">        READER       </code> access to the dataset.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       WRITER      </code></td>
<td><ul>
<li>Same as <code dir="ltr" translate="no">         READER        </code> , plus:
<ul>
<li>Can edit or append data in the dataset
<ul>
<li>Can call <a href="/bigquery/docs/reference/v2/tables/insert">insert</a> , <a href="/bigquery/docs/reference/v2/tabledata/insertAll">insertAll</a> , <a href="/bigquery/docs/reference/v2/tables/update">update</a> or <a href="/bigquery/docs/reference/v2/tables/delete">delete</a> on tables</li>
<li>Can use tables in the dataset as destinations for load, copy or query jobs</li>
<li>Can call <a href="/bigquery/docs/reference/v2/routines/insert">insert</a> , <a href="/bigquery/docs/reference/v2/routines/update">update</a> , or <a href="/bigquery/docs/reference/v2/routines/delete">delete</a> on routines</li>
</ul></li>
</ul></li>
</ul>
The <a href="/bigquery/docs/access-control#bigquery.dataEditor">BigQuery Data Editor</a> ( <code dir="ltr" translate="no">        roles/bigquery.dataEditor       </code> ) predefined IAM role is mapped to the <code dir="ltr" translate="no">        WRITER       </code> BigQuery basic role. When you grant BigQuery Data Editor to a principal at the dataset level, the principal is granted <code dir="ltr" translate="no">        WRITER       </code> access to the dataset.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       OWNER      </code></td>
<td><ul>
<li>Same as <code dir="ltr" translate="no">         WRITER        </code> , plus:
<ul>
<li>Can call <a href="/bigquery/docs/reference/v2/datasets/update">update</a> on the dataset</li>
<li>Can call <a href="/bigquery/docs/reference/v2/datasets/delete">delete</a> on the dataset</li>
</ul></li>
</ul>
<p>A dataset must have at least one entity with the <code dir="ltr" translate="no">        OWNER       </code> role. A user with the <code dir="ltr" translate="no">        OWNER       </code> role can't remove their own <code dir="ltr" translate="no">        OWNER       </code> role.</p>
The <a href="/bigquery/docs/access-control#bigquery.dataOwner">BigQuery Data Owner</a> ( <code dir="ltr" translate="no">        roles/bigquery.dataOwner       </code> ) predefined IAM role is mapped to the <code dir="ltr" translate="no">        OWNER       </code> BigQuery basic role. When you grant BigQuery Data Owner to a principal at the dataset level, the principal is granted <code dir="ltr" translate="no">        OWNER       </code> access to the dataset.</td>
</tr>
</tbody>
</table>

For more information on assigning roles at the dataset level, see [Controlling access to datasets](/bigquery/docs/dataset-access-controls) .

When you create a new dataset, BigQuery adds default dataset access for the following entities. Roles that you specify on dataset creation overwrite the default values.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Entity</th>
<th>Dataset role</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>All users with <code dir="ltr" translate="no">       Viewer      </code> access to the project</td>
<td><code dir="ltr" translate="no">       READER      </code></td>
</tr>
<tr class="even">
<td>All users with <code dir="ltr" translate="no">       Editor      </code> access to the project</td>
<td><code dir="ltr" translate="no">       WRITER      </code></td>
</tr>
<tr class="odd">
<td>All users with <code dir="ltr" translate="no">       Owner      </code> access to the project,<br />
and the dataset creator</td>
<td><p><code dir="ltr" translate="no">        OWNER       </code></p>
<p><strong>Exception:</strong> When a user runs a query, an <a href="/bigquery/docs/cached-results#how_cached_results_are_stored">anonymous dataset</a> is created to store the cached results table. Only the user that runs the query is given <code dir="ltr" translate="no">        OWNER       </code> access to the anonymous dataset.</p></td>
</tr>
</tbody>
</table>
