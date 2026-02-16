# Loading data from Datastore exports

BigQuery supports loading data from [Datastore](/datastore) exports created using the Datastore managed import and export service. You can use the managed import and export service to export Datastore entities into a Cloud Storage bucket. You can then load the export into BigQuery as a table.

To learn how to create a Datastore export file, see [Exporting and importing entities](/datastore/docs/export-import-entities) in the Datastore documentation. For information on scheduling exports, see [Scheduling an export](/datastore/docs/schedule-export) .

**Note:** If you intend to load a Datastore export into BigQuery, you must specify an entity filter in your [export command](/datastore/docs/export-import-entities#exporting_entities) . Data exported without specifying an entity filter cannot be loaded into BigQuery.

You can control which properties BigQuery should load by setting the [`  projectionFields  ` property](/bigquery/docs/reference/rest/v2/Job#JobConfigurationLoad.FIELDS.projection_fields) in the API or by using the `  --projection_fields  ` flag in the bq command-line tool.

If you prefer to skip the loading process, you can query the export directly by setting it up as an external data source. For more information, see [External data sources](/bigquery/external-data-sources) .

When you load data from Cloud Storage into a BigQuery table, the dataset that contains the table must be in the same region or multi-region as the Cloud Storage bucket.

## Limitations

When you load data into BigQuery from a Datastore export, note the following restrictions:

  - You cannot use a wildcard in the Cloud Storage URI when you specify a Datastore export file.
  - You can specify only one Cloud Storage URI when loading data from Datastore exports.
  - You cannot append Datastore export data to an existing table with a defined schema.
  - For a Datastore export to load correctly, entities in the export data must share a consistent schema with fewer than 10,000 unique property names.
  - Data exported without specifying an entity filter cannot be loaded into BigQuery. The export request must include one or more kind names in the entity filter.
  - The maximum field size for Datastore exports is 64 KB. When you load a Datastore export, any field larger than 64 KB is truncated.

## Before you begin

Grant Identity and Access Management (IAM) roles that give users the necessary permissions to perform each task in this document.

### Required permissions

To load data into BigQuery, you need IAM permissions to run a load job and load data into BigQuery tables and partitions. If you are loading data from Cloud Storage, you also need IAM permissions to access the bucket that contains your data.

#### Permissions to load data into BigQuery

To load data into a new BigQuery table or partition or to append or overwrite an existing table or partition, you need the following IAM permissions:

  - `  bigquery.tables.create  `
  - `  bigquery.tables.updateData  `
  - `  bigquery.tables.update  `
  - `  bigquery.jobs.create  `

Each of the following predefined IAM roles includes the permissions that you need in order to load data into a BigQuery table or partition:

  - `  roles/bigquery.dataEditor  `
  - `  roles/bigquery.dataOwner  `
  - `  roles/bigquery.admin  ` (includes the `  bigquery.jobs.create  ` permission)
  - `  bigquery.user  ` (includes the `  bigquery.jobs.create  ` permission)
  - `  bigquery.jobUser  ` (includes the `  bigquery.jobs.create  ` permission)

Additionally, if you have the `  bigquery.datasets.create  ` permission, you can create and update tables using a load job in the datasets that you create.

For more information on IAM roles and permissions in BigQuery, see [Predefined roles and permissions](/bigquery/access-control) .

### Permissions to load data from Cloud Storage

To get the permissions that you need to load data from a Cloud Storage bucket, ask your administrator to grant you the [Storage Admin](/iam/docs/roles-permissions/storage#storage.admin) ( `  roles/storage.admin  ` ) IAM role on the bucket. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

This predefined role contains the permissions required to load data from a Cloud Storage bucket. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to load data from a Cloud Storage bucket:

  - `  storage.buckets.get  `
  - `  storage.objects.get  `
  - `  storage.objects.list (required if you are using a URI wildcard )  `

You might also be able to get these permissions with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

## Loading Datastore export service data

To load data from a Datastore export metadata file:

### Console

In the Google Cloud console, go to the **BigQuery** page.

In the left pane, click explore **Explorer** .

In the **Explorer** pane, expand your project, click **Datasets** , and then select a dataset.

In the **Dataset info** section, click add\_box **Create table** .

In the **Create table** pane, specify the following details:

1.  In the **Source** section, select **Google Cloud Storage** in the **Create table from** list. Then, do the following:
    1.  Select a file from the Cloud Storage bucket, or enter the [Cloud Storage URI](/bigquery/docs/batch-loading-data#gcs-uri) . You cannot include multiple URIs in the Google Cloud console, but [wildcards](/bigquery/docs/batch-loading-data#load-wildcards) are supported. The Cloud Storage bucket must be in the same location as the dataset that contains the table you want to create, append, or overwrite.  
        The URI for your Datastore export file must end with `  KIND_NAME .export_metadata  ` or `  export[NUM].export_metadata  ` . For example, in `  default_namespace_kind_Book.export_metadata  ` , `  Book  ` is the kind name, and `  default_namespace_kind_Book  ` is the filename generated by Datastore.
    2.  For **File format** , select **Cloud Datastore Backup** .
2.  In the **Destination** section, specify the following details:
    1.  For **Dataset** , select the dataset in which you want to create the table.
    2.  In the **Table** field, enter the name of the table that you want to create.
    3.  Verify that the **Table type** field is set to **Native table** .
3.  In the **Schema** section, no action is necessary. The schema is inferred for a Datastore export.
4.  Optional: Specify **Partition and cluster settings** . For more information, see [Creating partitioned tables](/bigquery/docs/creating-partitioned-tables) and [Creating and using clustered tables](/bigquery/docs/creating-clustered-tables) .
5.  Click **Advanced options** and do the following:
      - For **Write preference** , leave **Write if empty** selected. This option creates a new table and loads your data into it.
      - If you want to ignore values in a row that are not present in the table's schema, then select **Unknown values** .
      - For **Encryption** , click **Customer-managed key** to use a [Cloud Key Management Service key](/bigquery/docs/customer-managed-encryption) . If you leave the **Google-managed key** setting, BigQuery [encrypts the data at rest](/docs/security/encryption/default-encryption) .
6.  Click **Create table** .

### bq

Use the `  bq load  ` command with `  source_format  ` set to `  DATASTORE_BACKUP  ` . Supply the `  --location  ` flag and set the value to your [location](/bigquery/docs/locations) .

``` text
bq --location=LOCATION load \
--source_format=FORMAT \
DATASET.TABLE \
PATH_TO_SOURCE
```

Replace the following:

  - `  LOCATION  ` : your location. The `  --location  ` flag is optional. For example, if you are using BigQuery in the Tokyo region, you can set the flag's value to `  asia-northeast1  ` . You can set a default value for the location by using the [.bigqueryrc file](/bigquery/docs/bq-command-line-tool#setting_default_values_for_command-line_flags) .
  - `  FORMAT  ` : `  DATASTORE_BACKUP  ` .
  - `  DATASET  ` : the dataset that contains the table into which you're loading data.
  - `  TABLE  ` : the table into which you're loading data. If the table does not exist, it is created.
  - `  PATH_TO_SOURCE  ` : the [Cloud Storage URI](/bigquery/docs/batch-loading-data#gcs-uri) .

For example, the following command loads the `  gs://mybucket/20180228T1256/default_namespace/kind_Book/default_namespace_kind_Book.export_metadata  ` Datastore export file into a table named `  book_data  ` . `  mybucket  ` and `  mydataset  ` were created in the `  US  ` multi-region location.

``` text
bq --location=US load \
--source_format=DATASTORE_BACKUP \
mydataset.book_data \
gs://mybucket/20180228T1256/default_namespace/kind_Book/default_namespace_kind_Book.export_metadata
```

### API

Set the following properties to load Datastore export data using the [API](/bigquery/docs/reference/v2) .

1.  Create a [load job](/bigquery/docs/reference/rest/v2/Job#jobconfigurationload) that points to the source data in Cloud Storage.

2.  Specify your [location](/bigquery/docs/locations) in the `  location  ` property in the `  jobReference  ` section of the [job resource](/bigquery/docs/reference/rest/v2/jobs) .

3.  The [source URIs](/bigquery/docs/reference/rest/v2/Job#JobConfigurationLoad.FIELDS.source_uris) must be fully qualified, in the format gs://\[BUCKET\]/\[OBJECT\]. The file (object) name must end in `  [KIND_NAME].export_metadata  ` . Only one URI is allowed for Datastore exports, and you cannot use a wildcard.

4.  Specify the data format by setting the [`  JobConfigurationLoad.sourceFormat  ` property](/bigquery/docs/reference/rest/v2/Job#JobConfigurationLoad.FIELDS.source_format) to `  DATASTORE_BACKUP  ` .

## Appending to or overwriting a table with Datastore data

When you load Datastore export data into BigQuery, you can create a new table to store the data, or you can overwrite an existing table. You cannot append Datastore export data to an existing table.

If you attempt to append Datastore export data to an existing table, the following error results: `  Cannot append a datastore backup to a table that already has a schema. Try using the WRITE_TRUNCATE write disposition to replace the existing table  ` .

To overwrite an existing table with Datastore export data:

### Console

In the Google Cloud console, go to the **BigQuery** page.

In the left pane, click explore **Explorer** .

In the **Explorer** pane, expand your project, click **Datasets** , and then select a dataset.

In the **Dataset info** section, click add\_box **Create table** .

In the **Create table** pane, specify the following details:

1.  In the **Source** section, select **Google Cloud Storage** in the **Create table from** list. Then, do the following:
    1.  Select a file from the Cloud Storage bucket, or enter the [Cloud Storage URI](/bigquery/docs/batch-loading-data#gcs-uri) . You cannot include multiple URIs in the Google Cloud console, but [wildcards](/bigquery/docs/batch-loading-data#load-wildcards) are supported. The Cloud Storage bucket must be in the same location as the dataset that contains the table you want to create, append, or overwrite.  
        The URI for your Datastore export file must end with `  KIND_NAME .export_metadata  ` or `  export[NUM].export_metadata  ` . For example, in `  default_namespace_kind_Book.export_metadata  ` , `  Book  ` is the kind name, and `  default_namespace_kind_Book  ` is the filename generated by Datastore.
    2.  For **File format** , select **Cloud Datastore Backup** .
2.  In the **Destination** section, specify the following details:
    1.  For **Dataset** , select the dataset in which you want to create the table.
    2.  In the **Table** field, enter the name of the table that you want to create.
    3.  Verify that the **Table type** field is set to **Native table** .
3.  In the **Schema** section, no action is necessary. The schema is inferred for a Datastore export.
4.  Optional: Specify **Partition and cluster settings** . For more information, see [Creating partitioned tables](/bigquery/docs/creating-partitioned-tables) and [Creating and using clustered tables](/bigquery/docs/creating-clustered-tables) . You cannot convert a table to a partitioned or clustered table by appending or overwriting it. The Google Cloud console does not support appending to or overwriting partitioned or clustered tables in a load job.
5.  Click **Advanced options** and do the following:
      - For **Write preference** , choose **Append to table** or **Overwrite table** .
      - If you want to ignore values in a row that are not present in the table's schema, then select **Unknown values** .
      - For **Encryption** , click **Customer-managed key** to use a [Cloud Key Management Service key](/bigquery/docs/customer-managed-encryption) . If you leave the **Google-managed key** setting, BigQuery [encrypts the data at rest](/docs/security/encryption/default-encryption) .
6.  Click **Create table** .

### bq

Use the `  bq load  ` command with the `  --replace  ` flag and with `  source_format  ` set to `  DATASTORE_BACKUP  ` . Supply the `  --location  ` flag and set the value to your [location](/bigquery/docs/locations) .

``` text
bq --location=LOCATION load \
--source_format=FORMAT \
--replace \
DATASET.TABLE \
PATH_TO_SOURCE
```

Replace the following:

  - `  LOCATION  ` : your location. The `  --location  ` flag is optional. For example, if you are using BigQuery in the Tokyo region, you can set the flag's value to `  asia-northeast1  ` . You can set a default value for the location by using the [.bigqueryrc file](/bigquery/docs/bq-command-line-tool#setting_default_values_for_command-line_flags) .
  - `  FORMAT  ` : `  DATASTORE_BACKUP  ` .
  - `  DATASET  ` : the dataset containing the table into which you're loading data.
  - `  TABLE  ` : the table you're overwriting.
  - `  PATH_TO_SOURCE  ` : the [Cloud Storage URI](/bigquery/docs/batch-loading-data#gcs-uri) .

For example, the following command loads the `  gs://mybucket/20180228T1256/default_namespace/kind_Book/default_namespace_kind_Book.export_metadata  ` Datastore export file and overwrites a table named `  book_data  ` :

``` text
bq load --source_format=DATASTORE_BACKUP \
--replace \
mydataset.book_data \
gs://mybucket/20180228T1256/default_namespace/kind_Book/default_namespace_kind_Book.export_metadata
```

### API

Set the following properties to load data from the [API](/bigquery/docs/reference/v2) .

1.  Create a [load job](/bigquery/docs/reference/rest/v2/Job#jobconfigurationload) that points to the source data in Cloud Storage.

2.  Specify your [location](/bigquery/docs/locations) in the `  location  ` property in the `  jobReference  ` section of the [job resource](/bigquery/docs/reference/rest/v2/jobs) .

3.  The [source URIs](/bigquery/docs/reference/rest/v2/Job#JobConfigurationLoad.FIELDS.source_uris) must be fully qualified, in the format gs://\[BUCKET\]/\[OBJECT\]. The file (object) name must end in `  [KIND_NAME].export_metadata  ` . Only one URI is allowed for Datastore exports, and you cannot use a wildcard.

4.  Specify the data format by setting the [`  JobConfigurationLoad.sourceFormat  ` property](/bigquery/docs/reference/rest/v2/Job#JobConfigurationLoad.FIELDS.source_format) to `  DATASTORE_BACKUP  ` .

5.  Specify the write disposition by setting the [`  JobConfigurationLoad.writeDisposition  ` property](/bigquery/docs/reference/rest/v2/Job#JobConfigurationLoad.FIELDS.write_disposition) to `  WRITE_TRUNCATE  ` .

## Datastore options

To change how BigQuery parses Datastore export data, specify the following option:

<table>
<thead>
<tr class="header">
<th>Console option</th>
<th>bq tool flag</th>
<th>BigQuery API property</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Not available</td>
<td><code dir="ltr" translate="no">       --projection_fields      </code></td>
<td><a href="/bigquery/docs/reference/rest/v2/Job#JobConfigurationLoad.FIELDS.projection_fields">projectionFields</a></td>
<td>A comma-separated list that indicates which entity properties to load into BigQuery from a Datastore export. Property names are case-sensitive and must be top-level properties. If no properties are specified, BigQuery loads all properties. If any named property isn't found in the Datastore export, an invalid error is returned in the job result. The default value is ''.</td>
</tr>
</tbody>
</table>

## Data type conversion

BigQuery converts data from each entity in Datastore export files to BigQuery [data types](/bigquery/docs/reference/standard-sql/data-types) . The following table describes the conversion between data types.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Datastore data type</th>
<th>BigQuery data type</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Array</td>
<td><code dir="ltr" translate="no">       ARRAY      </code></td>
</tr>
<tr class="even">
<td>Blob</td>
<td><code dir="ltr" translate="no">       BYTES      </code></td>
</tr>
<tr class="odd">
<td>Boolean</td>
<td><code dir="ltr" translate="no">       BOOLEAN      </code></td>
</tr>
<tr class="even">
<td>Date and time</td>
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
</tr>
<tr class="odd">
<td>Embedded entity</td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
</tr>
<tr class="even">
<td>Floating-point number</td>
<td><code dir="ltr" translate="no">       FLOAT      </code></td>
</tr>
<tr class="odd">
<td>Geographical point</td>
<td><p><code dir="ltr" translate="no">        RECORD       </code></p>
<pre class="text" dir="ltr" data-is-upgraded="" translate="no"><code>[{&quot;lat&quot;,&quot;DOUBLE&quot;},
 {&quot;long&quot;,&quot;DOUBLE&quot;}]
        </code></pre></td>
</tr>
<tr class="even">
<td>Integer</td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
</tr>
<tr class="odd">
<td>Key</td>
<td><code dir="ltr" translate="no">       RECORD      </code></td>
</tr>
<tr class="even">
<td>Null</td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="odd">
<td>Text string</td>
<td><code dir="ltr" translate="no">       STRING      </code> (truncated to 64 KB)</td>
</tr>
</tbody>
</table>

## Datastore key properties

Each entity in Datastore has a unique key that contains information such as the namespace and the path. BigQuery creates a `  RECORD  ` data type for the key, with nested fields for each piece of information, as described in the following table.

<table>
<thead>
<tr class="header">
<th>Key property</th>
<th>Description</th>
<th>BigQuery data type</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       __key__.app      </code></td>
<td>The Datastore app name.</td>
<td>STRING</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       __key__.id      </code></td>
<td>The entity's ID, or <code dir="ltr" translate="no">       null      </code> if <code dir="ltr" translate="no">       __key__.name      </code> is set.</td>
<td>INTEGER</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       __key__.kind      </code></td>
<td>The entity's kind.</td>
<td>STRING</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       __key__.name      </code></td>
<td>The entity's name, or <code dir="ltr" translate="no">       null      </code> if <code dir="ltr" translate="no">       __key__.id      </code> is set.</td>
<td>STRING</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       __key__.namespace      </code></td>
<td>If the Datastore app uses a custom namespace, the entity's namespace. Else, the default namespace is represented by an empty string.</td>
<td>STRING</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       __key__.path      </code></td>
<td>The flattened <a href="/appengine/docs/java/datastore/entities#Java_Ancestor_paths">ancestral path of the entity</a> , consisting of the sequence of kind-identifier pairs from the root entity to the entity itself. For example: <code dir="ltr" translate="no">       "Country", "USA", "PostalCode",         10011, "Route", 1234      </code> .</td>
<td>STRING</td>
</tr>
</tbody>
</table>
