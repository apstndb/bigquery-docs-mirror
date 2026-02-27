# Changes to dataset-level access controls

Starting Mar 17 2026, the `  bigquery.datasets.getIamPolicy  ` Identity and Access Management (IAM) permission is required to view a dataset's access controls and to query the [`  INFORMATION_SCHEMA.OBJECT_PRIVILEGES  `](/bigquery/docs/information-schema-object-privileges) view. The `  bigquery.datasets.setIamPolicy  ` permission is required to update a dataset's access controls or to [create a dataset with access controls using the API](#changes_to_api_methods) .

## Opt into early enforcement

Before Mar 17, 2026, you can opt into early enforcement of the permission changes. When you opt in, the `  bigquery.datasets.getIamPolicy  ` permission is necessary to get a dataset's access controls, and the `  bigquery.datasets.setIamPolicy  ` permission is necessary to update a dataset's access controls or to create a dataset with access controls using the API.

To opt into early enforcement, set the `  enable_fine_grained_dataset_acls_option  ` configuration setting to `  TRUE  ` at the organization or project level. For instructions on enabling configuration settings, see [Manage configuration settings](/bigquery/docs/default-configuration) .

### Configuration setting examples

The following examples show you how to set and remove the `  enable_fine_grained_dataset_acls_option  ` configuration setting.

#### Configure organization settings

To configure organization settings, use the [`  ALTER ORGANIZATION SET OPTIONS  ` DDL statement](/bigquery/docs/reference/standard-sql/data-definition-language#alter_organization_set_options_statement) . The following example sets `  enable_fine_grained_dataset_acls_option  ` to `  TRUE  ` at the organization level:

``` text
ALTER ORGANIZATION
SET OPTIONS (
  `region-REGION.enable_fine_grained_dataset_acls_option` = TRUE);
```

Replace REGION with the [region](/bigquery/docs/locations#regions) associated with your organization—for example, `  us  ` or `  europe-west6  ` .

The following example clears the organization-level `  enable_fine_grained_dataset_acls_option  ` setting:

``` text
ALTER ORGANIZATION
SET OPTIONS (
  `region-REGION.enable_fine_grained_dataset_acls_option` = FALSE);
```

#### Configure project settings

To configure project settings, use the [`  ALTER PROJECT SET OPTIONS  ` DDL statement](/bigquery/docs/reference/standard-sql/data-definition-language#alter_project_set_options_statement) . The `  ALTER PROJECT SET OPTIONS  ` DDL statement optionally accepts the `  project_id  ` variable. If the `  project_id  ` is not specified, it defaults to the current project where the query runs.

The following example sets `  enable_fine_grained_dataset_acls_option  ` to `  TRUE  ` .

``` text
ALTER PROJECT PROJECT_ID
SET OPTIONS (
  `region-REGION.enable_fine_grained_dataset_acls_option` = TRUE);
```

Replace PROJECT\_ID with your project ID.

The following example clears the project-level `  enable_fine_grained_dataset_acls_option  ` setting:

``` text
ALTER PROJECT PROJECT_ID
SET OPTIONS (
  `region-REGION.enable_fine_grained_dataset_acls_option` = FALSE);
```

## Changes to custom roles

This change to the required permissions impacts existing custom roles that grant `  bigquery.datasets.get  ` , `  bigquery.datasets.create  ` , or `  bigquery.datasets.update  ` permission and don't also grant the `  bigquery.datasets.getIamPolicy  ` or `  bigquery.datasets.setIamPolicy  ` permission.

Any custom roles that only include the `  bigquery.datasets.get  ` , `  bigquery.datasets.update  ` , or `  bigquery.datasets.create  ` permission must be updated to include the `  bigquery.datasets.getIamPolicy  ` or `  bigquery.datasets.setIamPolicy  ` permission by Mar 17, 2026, if you want to maintain the existing functionality of the custom roles. If your custom roles need to view or update only a dataset's metadata, use the new `  dataset_view  ` and `  update_mode  ` parameters.

BigQuery predefined roles are *not* affected by this change. All predefined roles that grant the `  bigquery.datasets.get  ` permission also grant the `  bigquery.datasets.getIamPolicy  ` permission. All predefined roles that grant the `  bigquery.datasets.update  ` permission also grant the `  bigquery.datasets.setIamPolicy  ` permission.

## Changes to bq command-line tool commands

When you opt into early enforcement, the following bq tool commands are affected.

### bq show

You can use the [`  bq show  `](/bigquery/docs/reference/bq-cli-reference#bq_show) command with the following flag:

  - **`  --dataset_view={METADATA|ACL|FULL}  `**  
    Specifies how to apply permissions when you're viewing a dataset's access controls or metadata. Use one of the following values:
      - `  METADATA  ` : view only the dataset's metadata. This value requires the `  bigquery.datasets.get  ` permission.
      - `  ACL  ` : view only the dataset's access controls. This value requires the `  bigquery.datasets.getIamPolicy  ` permission.
      - `  FULL  ` : view both the dataset's metadata and access controls. This value requires the `  bigquery.datasets.get  ` permission and `  bigquery.datasets.getIamPolicy  ` permissions.

### bq update

You can use the [`  bq update  `](/bigquery/docs/reference/bq-cli-reference#bq_update) command with the following flag:

  - **`  --update_mode={UPDATE_METADATA|UPDATE_ACL|UPDATE_FULL}  `**  
    Specifies how to apply permissions when you're updating a dataset's access controls or metadata. Use one of the following values:
      - `  UPDATE_METADATA  ` : update only the dataset's metadata. This value requires the `  bigquery.datasets.update  ` permission.
      - `  UPDATE_ACL  ` : update only the dataset's access controls. This value requires the `  bigquery.datasets.setIamPolicy  ` permission.
      - `  UPDATE_FULL  ` : update both the dataset's metadata and access controls. This value requires the `  bigquery.datasets.update  ` permission and `  bigquery.datasets.setIamPolicy  ` permissions.

## Changes to data control language (DCL) statements

When you opt into early enforcement, the following permissions are required to run `  GRANT  ` and `  REVOKE  ` statements on datasets using the [data control language (DCL)](/bigquery/docs/reference/standard-sql/data-control-language) :

  - `  bigquery.datasets.setIamPolicy  `

## Changes to `     INFORMATION_SCHEMA    ` view queries

When you opt into early enforcement, the `  bigquery.datasets.getIamPolicy  ` permission is required to query the [`  INFORMATION_SCHEMA.OBJECT_PRIVILEGES  `](/bigquery/docs/information-schema-object-privileges) view.

## Changes to API methods

After you opt into early enforcement, the following REST v2 API dataset methods are affected.

### datasets.get method

The [`  datasets.get  ` method](/bigquery/docs/reference/rest/v2/datasets/get) has an additional [path parameter](/bigquery/docs/reference/rest/v2/datasets/get#path-parameters) named `  dataset_view  ` .

This parameter gives you more control over the information returned by the `  datasets.get  ` method. Rather than always returning both access controls and metadata, the `  dataset_view  ` parameter lets you specify whether to return just metadata, just access controls, or both.

The `  access  ` field in the [dataset resource](/bigquery/docs/reference/rest/v2/datasets) contains the dataset's access controls. The other fields such as `  friendlyName  ` , `  description  ` , and `  labels  ` represent the dataset's metadata.

The following table shows the required permission and API response for the different values supported by the `  dataset_view  ` parameter:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameter value</th>
<th>Permissions required</th>
<th>API response</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       DATASET_VIEW_UNSPECIFIED      </code> (or empty)</td>
<td><ul>
<li><code dir="ltr" translate="no">         bigquery.datasets.get        </code></li>
<li><code dir="ltr" translate="no">         bigquery.datasets.getIamPolicy        </code></li>
</ul></td>
<td>The default value. Returns the dataset's metadata and access controls.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       METADATA      </code></td>
<td><ul>
<li><code dir="ltr" translate="no">         bigquery.datasets.get        </code></li>
</ul></td>
<td>Returns the dataset's metadata.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       ACL      </code></td>
<td><ul>
<li><code dir="ltr" translate="no">         bigquery.datasets.getIamPolicy        </code></li>
</ul></td>
<td>Returns the dataset's access controls, required fields, and fields in the dataset resource that are output only.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       FULL      </code></td>
<td><ul>
<li><code dir="ltr" translate="no">         bigquery.datasets.get        </code></li>
<li><code dir="ltr" translate="no">         bigquery.datasets.getIamPolicy        </code></li>
</ul></td>
<td>Returns the dataset's metadata and access controls.</td>
</tr>
</tbody>
</table>

If you don't opt into early enforcement, or if you opt out after opting in, you can use the `  dataset_view  ` parameter with the `  METADATA  ` or `  ACL  ` values. The `  FULL  ` and `  DATASET_VIEW_UNSPECIFIED  ` (or empty) values default to the previous behavior; the `  bigquery.datasets.get  ` permission lets you get both metadata and access controls.

#### Example

The following example sends a `  GET  ` request with the `  dataset_view  ` parameter set to `  METADATA  ` :

``` text
GET https://bigquery.googleapis.com/bigquery/v2/projects/YOUR_PROJECT/datasets/YOUR_DATASET?datasetView=METADATA&key=YOUR_API_KEY HTTP/1.1
```

Replace the following:

  - YOUR\_PROJECT : the name of your project
  - YOUR\_DATASET : the name of the dataset
  - YOUR\_API\_KEY : your API key

### datasets.update method

The [`  datasets.update  ` method](/bigquery/docs/reference/rest/v2/datasets/update) has an additional [path parameter](/bigquery/docs/reference/rest/v2/datasets/update#path-parameters) named `  update_mode  ` .

This parameter gives you more control over the fields updated by the `  datasets.update  ` method. Rather than always allowing updates to both access controls and metadata, the `  update_mode  ` parameter lets you specify whether to update just metadata, just access controls, or both.

The `  access  ` field in the [dataset resource](/bigquery/docs/reference/rest/v2/datasets) contains the dataset's access controls. The other fields such as `  friendlyName  ` , `  description  ` , and `  labels  ` represent the dataset's metadata.

The following table shows the required permission and API response for the different values supported by the `  update_mode  ` parameter:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameter value</th>
<th>Permissions required</th>
<th>API response</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       UPDATE_MODE_UNSPECIFIED      </code> (or empty)</td>
<td><ul>
<li><code dir="ltr" translate="no">         bigquery.datasets.update        </code></li>
<li><code dir="ltr" translate="no">         bigquery.datasets.setIamPolicy        </code></li>
</ul></td>
<td>The default value. Returns the dataset's updated metadata and access controls.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       UPDATE_METADATA      </code></td>
<td><ul>
<li><code dir="ltr" translate="no">         bigquery.datasets.update        </code></li>
</ul></td>
<td>Returns the dataset's updated metadata.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       UPDATE_ACL      </code></td>
<td><ul>
<li><code dir="ltr" translate="no">         bigquery.datasets.update        </code></li>
<li><code dir="ltr" translate="no">         bigquery.datasets.setIamPolicy        </code></li>
</ul></td>
<td>Returns the dataset's updated access controls, required fields, and fields in the dataset resource that are output only.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       UPDATE_FULL      </code></td>
<td><ul>
<li><code dir="ltr" translate="no">         bigquery.datasets.update        </code></li>
<li><code dir="ltr" translate="no">         bigquery.datasets.setIamPolicy        </code></li>
</ul></td>
<td>Returns the dataset's updated metadata and access controls.</td>
</tr>
</tbody>
</table>

If you don't opt into early enforcement, or if you opt out after opting in, BigQuery defaults to the previous behavior; the `  bigquery.datasets.update  ` permission lets you update both metadata and access controls.

#### Example

The following example sends a `  PUT  ` request with the `  update_mode  ` parameter set to `  METADATA  ` :

``` text
PUT https://bigquery.googleapis.com/bigquery/v2/projects/YOUR_PROJECT/datasets/YOUR_DATASET?updateMode=METADATA&key=YOUR_API_KEY HTTP/1.1
```

Replace the following:

  - YOUR\_PROJECT : the name of your project
  - YOUR\_DATASET : the name of the dataset
  - YOUR\_API\_KEY : your API key name

### datasets.patch method

The [`  datasets.patch  ` method](/bigquery/docs/reference/rest/v2/datasets/patch) has an additional [path parameter](/bigquery/docs/reference/rest/v2/datasets/patch#path-parameters) named `  update_mode  ` .

This parameter gives you more control over the fields updated by the `  datasets.patch  ` method. Rather than always allowing updates to both access controls and metadata, the `  update_mode  ` parameter lets you specify whether to update just metadata, just access controls, or both.

The `  access  ` field in the [dataset resource](/bigquery/docs/reference/rest/v2/datasets) contains the dataset's access controls. The other fields such as `  friendlyName  ` , `  description  ` , and `  labels  ` represent the dataset's metadata.

The following table shows the required permission and API response for the different values supported by the `  update_mode  ` parameter:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameter value</th>
<th>Permissions required</th>
<th>API response</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       UPDATE_MODE_UNSPECIFIED      </code> (or empty)</td>
<td><ul>
<li><code dir="ltr" translate="no">         bigquery.datasets.update        </code></li>
<li><code dir="ltr" translate="no">         bigquery.datasets.setIamPolicy        </code></li>
</ul></td>
<td>The default value. Returns the dataset's updated metadata and access controls.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       UPDATE_METADATA      </code></td>
<td><ul>
<li><code dir="ltr" translate="no">         bigquery.datasets.update        </code></li>
</ul></td>
<td>Returns the dataset's updated metadata.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       UPDATE_ACL      </code></td>
<td><ul>
<li><code dir="ltr" translate="no">         bigquery.datasets.setIamPolicy        </code></li>
</ul></td>
<td>Returns the dataset's updated access controls, required fields, and fields in the dataset resource that are output only.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       UPDATE_FULL      </code></td>
<td><ul>
<li><code dir="ltr" translate="no">         bigquery.datasets.update        </code></li>
<li><code dir="ltr" translate="no">         bigquery.datasets.setIamPolicy        </code></li>
</ul></td>
<td>Returns the dataset's updated metadata and access controls.</td>
</tr>
</tbody>
</table>

If you don't opt into early enforcement, or if you opt out after opting in, BigQuery defaults to the previous behavior; the `  bigquery.datasets.update  ` permission lets you update both metadata and access controls.

#### Example

The following example sends a `  PUT  ` request with the `  update_mode  ` parameter set to `  METADATA  ` :

``` text
PUT https://bigquery.googleapis.com/bigquery/v2/projects/YOUR_PROJECT/datasets/YOUR_DATASET?updateMode=METADATA&key=YOUR_API_KEY HTTP/1.1
```

Replace the following:

  - YOUR\_PROJECT : the name of your project
  - YOUR\_DATASET : the name of the dataset
  - YOUR\_API\_KEY : your API key name

### datasets.insert method

If you opt into early enforcement and use the [`  datasets.insert  ` method](/bigquery/docs/reference/rest/v2/datasets/patch) , to create a dataset with access controls, BigQuery verifies that the `  bigquery.datasets.create  ` and `  bigquery.datasets.setIamPolicy  ` permissions are granted to the user.

If you use the API to create a dataset without access controls, only the `  bigquery.datasets.create  ` permission is required.
