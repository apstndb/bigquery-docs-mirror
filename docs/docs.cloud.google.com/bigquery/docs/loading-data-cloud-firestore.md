# Loading data from Firestore exports

BigQuery supports loading data from [Firestore](/firestore) exports created using the Firestore [managed import and export service](/firestore/docs/manage-data/export-import) . The managed import and export service exports Firestore documents into a Cloud Storage bucket. You can then load the exported data into a BigQuery table.

**Note:** Not all Firestore exports can be loaded. Reference the BigQuery [limitations](#limitations) to create a Firestore export which can be loaded into a BigQuery table.

## Limitations

When you load data into BigQuery from a Firestore export, note the following restrictions:

  - Your dataset must be in the same location as the Cloud Storage bucket containing your export files.
  - You can specify only one Cloud Storage URI, and you cannot use a URI wildcard.
  - For a Firestore export to load correctly, documents in the export data must share a consistent schema with fewer than 10,000 unique field names.
  - You can create a new table to store the data, or you can overwrite an existing table. You cannot append Firestore export data to an existing table.
  - Your [export command](/firestore/docs/manage-data/export-import#export_data) must specify a `  collection-ids  ` filter. Data exported without specifying a collection ID filter cannot be loaded into BigQuery.

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

## Loading Firestore export service data

You can load data from a Firestore export metadata file by using the Google Cloud console, [bq command-line tool](/bigquery/docs/bq-command-line-tool) , or [API](/bigquery/docs/reference/rest/v2) .

Sometimes Datastore terminology is used in the Google Cloud console and the bq command-line tool, but the following procedures are compatible with Firestore export files. Firestore and Datastore share an export format.

**Note:** You can load specific fields by using the [--projection\_fields flag](#cloud_firestore_options) in the bq command-line tool or by setting the `  projectionFields  ` property in the `  load  ` job configuration.

### Console

In the Google Cloud console, go to the **BigQuery** page.

In the left pane, click explore **Explorer** .

In the **Explorer** pane, expand your project, click **Datasets** , and then select a dataset.

In the **Dataset info** section, click add\_box **Create table** .

In the **Create table** pane, specify the following details:

1.  In the **Source** section, select **Google Cloud Storage** in the **Create table from** list. Then, do the following:
    1.  Select a file from the Cloud Storage bucket, or enter the [Cloud Storage URI](/bigquery/docs/batch-loading-data#gcs-uri) . You cannot include multiple URIs in the Google Cloud console, but [wildcards](/bigquery/docs/batch-loading-data#load-wildcards) are supported. The Cloud Storage bucket must be in the same location as the dataset that contains the table you want to create, append, or overwrite.  
        The URI for your Firestore export file must end with `  KIND_COLLECTION_ID .export_metadata  ` . For example, in `  default_namespace_kind_Book.export_metadata  ` , `  Book  ` is the collection ID, and `  default_namespace_kind_Book  ` is the file name generated by Firestore. If the URI doesn't end with `  KIND_COLLECTION_ID .export_metadata  ` , you receive the following error message: **does not contain valid backup metadata. (error code: invalid).**
        **Note:** Do not use the file ending in `  overall_export_metadata  ` . This file is not usable by BigQuery.
    2.  For **File format** , select **Cloud Datastore Backup** . Firestore and Datastore share the export format.
2.  In the **Destination** section, specify the following details:
    1.  For **Dataset** , select the dataset in which you want to create the table.
    2.  In the **Table** field, enter the name of the table that you want to create.
    3.  Verify that the **Table type** field is set to **Native table** .
3.  In the **Schema** section, no action is necessary. The schema is inferred for a Firestore export.
4.  Optional: Specify **Partition and cluster settings** . For more information, see [Creating partitioned tables](/bigquery/docs/creating-partitioned-tables) and [Creating and using clustered tables](/bigquery/docs/creating-clustered-tables) .
5.  Click **Advanced options** and do the following:
      - For **Write preference** , leave **Write if empty** selected. This option creates a new table and loads your data into it.
      - If you want to ignore values in a row that are not present in the table's schema, then select **Unknown values** .
      - For **Encryption** , click **Customer-managed key** to use a [Cloud Key Management Service key](/bigquery/docs/customer-managed-encryption) . If you leave the **Google-managed key** setting, BigQuery [encrypts the data at rest](/docs/security/encryption/default-encryption) .
6.  Click **Create table** .

### bq

Use the [`  bq load  `](/bigquery/docs/reference/bq-cli-reference#bq_load) command with `  source_format  ` set to `  DATASTORE_BACKUP  ` . Supply the `  --location  ` flag and set the value to your [location](/bigquery/docs/locations) . If you are overwiting an existing table, add the `  --replace  ` flag.

To load only specific fields, use the [--projection\_fields flag](#cloud_firestore_options) .

``` text
bq --location=LOCATION load \
--source_format=FORMAT \
DATASET.TABLE \
PATH_TO_SOURCE
```

Replace the following:

  - `  LOCATION  ` : your location. The `  --location  ` flag is optional.
  - `  FORMAT  ` : `  DATASTORE_BACKUP  ` . Datastore Backup is the correct option for Firestore. Firestore and Datastore share an export format.
  - `  DATASET  ` : the dataset that contains the table into which you're loading data.
  - `  TABLE  ` : the table into which you're loading data. If the table doesn't exist, it is created.
  - `  PATH_TO_SOURCE  ` : the [Cloud Storage URI](/bigquery/docs/batch-loading-data#gcs-uri) .

For example, the following command loads the `  gs://mybucket/20180228T1256/default_namespace/kind_Book/default_namespace_kind_Book.export_metadata  ` Firestore export file into a table named `  book_data  ` . `  mybucket  ` and `  mydataset  ` were created in the `  US  ` multi-region location.

``` text
bq --location=US load \
--source_format=DATASTORE_BACKUP \
mydataset.book_data \
gs://mybucket/20180228T1256/default_namespace/kind_Book/default_namespace_kind_Book.export_metadata
```

### API

Set the following properties to load Firestore export data using the [API](/bigquery/docs/reference/v2) .

1.  Create a `  load  ` job configuration that points to the source data in Cloud Storage.

2.  Specify your [location](/bigquery/docs/locations) in the `  location  ` property in the `  jobReference  ` section of the [job resource](/bigquery/docs/reference/rest/v2/jobs) .

3.  The `  sourceUris  ` must be fully qualified, in the format `  gs:// BUCKET / OBJECT  ` in the load job configuration. The file (object) name must end in `  KIND_NAME .export_metadata  ` . Only one URI is allowed for Firestore exports, and you cannot use a wildcard.

4.  Specify the data format by setting the `  sourceFormat  ` property to `  DATASTORE_BACKUP  ` in the load job configuration. Datastore Backup is the correct option for Firestore. Firestore and Datastore share an export format.

5.  To load only specific fields, set the `  projectionFields  ` property.

6.  If you are overwriting an existing table, specify the write disposition by setting the `  writeDisposition  ` property to `  WRITE_TRUNCATE  ` .

### Python

Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/bigquery/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` python
# TODO(developer): Set table_id to the ID of the table to create.
table_id = "your-project.your_dataset.your_table_name"

# TODO(developer): Set uri to the path of the kind export metadata
uri = (
    "gs://cloud-samples-data/bigquery/us-states"
    "/2021-07-02T16:04:48_70344/all_namespaces/kind_us-states"
    "/all_namespaces_kind_us-states.export_metadata"
)

# TODO(developer): Set projection_fields to a list of document properties
#                  to import. Leave unset or set to `None` for all fields.
projection_fields = ["name", "post_abbr"]

from google.cloud import bigquery

# Construct a BigQuery client object.
client = bigquery.Client()

job_config = bigquery.LoadJobConfig(
    source_format=bigquery.SourceFormat.DATASTORE_BACKUP,
    projection_fields=projection_fields,
)

load_job = client.load_table_from_uri(
    uri, table_id, job_config=job_config
)  # Make an API request.

load_job.result()  # Waits for the job to complete.

destination_table = client.get_table(table_id)
print("Loaded {} rows.".format(destination_table.num_rows))
```

**Note:** If you prefer to skip the loading process, you can query the export directly by setting it up as an external data source. For more information, see [External data sources](/bigquery/external-data-sources) .

## Firestore options

To change how BigQuery parses Firestore export data, specify the following option:

<table>
<thead>
<tr class="header">
<th>Google Cloud console option</th>
<th>`bq` flag</th>
<th>BigQuery API property</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Not available</td>
<td><code dir="ltr" translate="no">       --projection_fields      </code></td>
<td><code dir="ltr" translate="no">       projectionFields      </code> ( <a href="/java/docs/reference/google-cloud-bigquery/latest/com.google.cloud.bigquery.DatastoreBackupOptions.Builder#com_google_cloud_bigquery_DatastoreBackupOptions_Builder_setProjectionFields_java_util_List_java_lang_String__">Java</a> , <a href="/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig#google_cloud_bigquery_job_LoadJobConfig_projection_fields">Python</a> )</td>
<td>(Optional) A comma-separated list that indicates which document fields to load from a Firestore export. By default, BigQuery loads all fields. Field names are case-sensitive and must be present in the export. You cannot specify field paths within a map field such as <code dir="ltr" translate="no">       map.foo      </code> .</td>
</tr>
</tbody>
</table>

## Data type conversion

BigQuery converts data from each document in Firestore export files to BigQuery [data types](/bigquery/docs/schemas#standard_sql_data_types) . The following table describes the conversion between supported data types.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Firestore data type</th>
<th>BigQuery data type</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Array</td>
<td>RECORD</td>
</tr>
<tr class="even">
<td>Boolean</td>
<td>BOOLEAN</td>
</tr>
<tr class="odd">
<td>Reference</td>
<td>RECORD</td>
</tr>
<tr class="even">
<td>Date and time</td>
<td>TIMESTAMP</td>
</tr>
<tr class="odd">
<td>Map</td>
<td>RECORD</td>
</tr>
<tr class="even">
<td>Floating-point number</td>
<td>FLOAT</td>
</tr>
<tr class="odd">
<td>Geographical point</td>
<td><p>RECORD</p>
<pre class="text" dir="ltr" data-is-upgraded="" translate="no"><code>[{&quot;lat&quot;,&quot;FLOAT&quot;},
 {&quot;long&quot;,&quot;FLOAT&quot;}]
        </code></pre></td>
</tr>
<tr class="even">
<td>Integer</td>
<td>INTEGER</td>
</tr>
<tr class="odd">
<td>String</td>
<td>STRING (truncated to 64 KB)</td>
</tr>
</tbody>
</table>

## Firestore key properties

Each document in Firestore has a unique key that contains information such as the document ID and the document path. BigQuery creates a `  RECORD  ` data type (also known as a [`  STRUCT  `](/bigquery/docs/reference/standard-sql/data-types#struct_type) ) for the key, with nested fields for each piece of information, as described in the following table.

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
<td>The Firestore app name.</td>
<td>STRING</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       __key__.id      </code></td>
<td>The document's ID, or <code dir="ltr" translate="no">       null      </code> if <code dir="ltr" translate="no">       __key__.name      </code> is set.</td>
<td>INTEGER</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       __key__.kind      </code></td>
<td>The document's collection ID.</td>
<td>STRING</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       __key__.name      </code></td>
<td>The document's name, or <code dir="ltr" translate="no">       null      </code> if <code dir="ltr" translate="no">       __key__.id      </code> is set.</td>
<td>STRING</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       __key__.namespace      </code></td>
<td>Firestore does not support custom namespaces. The default namespace is represented by an empty string.</td>
<td>STRING</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       __key__.path      </code></td>
<td>The path of the document: the sequence of the document and the collection pairs from the root collection. For example: <code dir="ltr" translate="no">       "Country",         "USA", "PostalCode", 10011, "Route", 1234      </code> .</td>
<td>STRING</td>
</tr>
</tbody>
</table>
