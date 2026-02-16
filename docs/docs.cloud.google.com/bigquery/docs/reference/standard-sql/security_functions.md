GoogleSQL for BigQuery supports the following security functions.

## Function list

<table>
<thead>
<tr class="header">
<th>Name</th>
<th>Summary</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/security_functions#session_user"><code dir="ltr" translate="no">        SESSION_USER       </code></a></td>
<td>Get the email address or principal identifier of the user that's running the query.</td>
</tr>
</tbody>
</table>

## `     SESSION_USER    `

``` text
SESSION_USER()
```

**Description**

For first-party users, returns the email address of the user that's running the query. For third-party users, returns the [principal identifier](https://cloud.google.com/iam/docs/principal-identifiers) of the user that's running the query. For more information about identities, see [Principals](https://cloud.google.com/docs/authentication#principal) .

**Return Data Type**

`  STRING  `

**Example**

``` text
SELECT SESSION_USER() as user;

/*----------------------+
 | user                 |
 +----------------------+
 | jdoe@example.com     |
 +----------------------*/
```
