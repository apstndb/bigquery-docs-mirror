# Create table snapshots with a scheduled query

This document describes how to create monthly snapshots of a table using a [service account](/bigquery/docs/scheduling-queries#using_a_service_account) that runs a scheduled [DDL query](/bigquery/docs/reference/standard-sql/data-definition-language) . The document steps you through the following example:

1.  In the `  PROJECT  ` project, create a service account named `  snapshot-bot  ` .
2.  Grant the `  snapshot-bot  ` service account the permissions that it needs to take [table snapshots](/bigquery/docs/table-snapshots-intro) of the `  TABLE  ` table, which is located in the `  DATASET  ` dataset, and store the table snapshots in the `  BACKUP  ` dataset.
3.  Write a query that creates monthly snapshots of the `  TABLE  ` table and places them in the `  BACKUP  ` dataset. Because you can't overwrite an existing table snapshot, the table snapshots must have unique names. To achieve this, the query appends the current date to the table snapshot names; for example, `  TABLE _20220521  ` . The table snapshots expire after 40 days.
4.  Schedule the `  snapshot-bot  ` service account to run the query on the first day of every month.

**Note:** To customize this document to use your own project, dataset, and/or table names in the text and examples, edit these variables: `  PROJECT  ` , `  DATASET  ` , `  BACKUP  ` , `  TABLE  ` .

This document is intended for users who are familiar with [BigQuery](/bigquery/docs) and [BigQuery table snapshots](/bigquery/docs/table-snapshots-intro) .

## Permissions and roles

This section describes the [Identity and Access Management (IAM) permissions](/bigquery/docs/access-control#bq-permissions) you need to create a service account and to schedule a query, and the [predefined IAM roles](/bigquery/docs/access-control#bigquery) that grant those permissions.

### Permissions

To work with a service account, you need the following permissions:

<table>
<thead>
<tr class="header">
<th><strong>Permission</strong></th>
<th><strong>Resource</strong></th>
<th><strong>Resource type</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       iam.serviceAccounts.*      </code></td>
<td><code dir="ltr" translate="no">         PROJECT       </code></td>
<td>Project</td>
</tr>
</tbody>
</table>

To schedule a query, you need the following permission:

<table>
<thead>
<tr class="header">
<th><strong>Permission</strong></th>
<th><strong>Resource</strong></th>
<th><strong>Resource type</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.jobs.create      </code></td>
<td><code dir="ltr" translate="no">         PROJECT       </code></td>
<td>Project</td>
</tr>
</tbody>
</table>

### Roles

The predefined roles that provide the permissions that are required to work with a service account are as follows:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Role</strong></th>
<th><strong>Resource</strong></th>
<th><strong>Resource type</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Any of the following:<br />
<br />
<code dir="ltr" translate="no">       roles/iam.serviceAccountAdmin      </code><br />
<code dir="ltr" translate="no">       roles/editor      </code><br />
<code dir="ltr" translate="no">       roles/owner      </code></td>
<td><code dir="ltr" translate="no">         PROJECT       </code></td>
<td>Project</td>
</tr>
</tbody>
</table>

The predefined BigQuery roles that provide the permissions that are required to schedule a query are as follows:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Role</strong></th>
<th><strong>Resource</strong></th>
<th><strong>Resource type</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Any of the following:<br />
<br />
<code dir="ltr" translate="no">       roles/bigquery.user      </code><br />
<code dir="ltr" translate="no">       roles/bigquery.jobuser      </code><br />
<code dir="ltr" translate="no">       roles/bigquery.admin      </code> `</td>
<td><code dir="ltr" translate="no">         PROJECT       </code></td>
<td>Project</td>
</tr>
</tbody>
</table>

## Create the `     snapshot-bot    ` service account

Follow these steps to create the `  snapshot-bot  ` [service account](/iam/docs/service-accounts) and grant it the [permissions](/bigquery/docs/access-control#bq-permissions) that it needs to run queries in the `  PROJECT  ` project:

### Console

1.  In Google Cloud console, go to the **Service accounts** page:

2.  Select the `  PROJECT  ` project.

3.  Create the `  snapshot-bot  ` service account:
    
    1.  Click **Create service account** .
    
    2.  In the **Service account name** field, enter **snapshot-bot** .
    
    3.  Click **Create and Continue** .

4.  Give the service account the permissions that it needs to run BigQuery jobs:
    
    1.  In the **Grant this service account access to project** section, select the [**BigQuery User**](/bigquery/docs/access-control#bigquery) role.
    
    2.  Click **Done** .

BigQuery creates the service account with the email address `  snapshot-bot@ PROJECT .iam.gserviceaccount.com  ` .

To verify that BigQuery created the service account with the permissions that you specified, follow these steps:

### Console

Verify that BigQuery has created the service account:

1.  In Google Cloud console, go to the **Service accounts** page:

2.  Select the `  PROJECT  ` project.

3.  Click **snapshot-bot@ PROJECT .iam.gserviceaccount.com** .

4.  Verify that the **Service account status** message indicates that your service account is active.

Verify that BigQuery has granted your service account the permission that it needs to run queries:

1.  In Google Cloud console, go to to the **Manage resources** page:

2.  Click `  PROJECT  ` .

3.  Click **Show Info Panel** .

4.  In the **Permissions** tab, expand the **BigQuery User** node.

5.  Verify that your **snapshot-bot** service account is listed.

## Grant permissions to the service account

This section describes how to grant the `  snapshot-bot  ` service account the permissions it needs to create table snapshots of the `  DATASET . TABLE  ` table in the `  BACKUP  ` dataset.

### Permission to take snapshots of the base table

To give the `  snapshot-bot  ` service account the permissions that it needs to take snapshots of the `  DATASET . TABLE  ` table, follow these steps:

### Console

1.  In Google Cloud console, open the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :
    
    If you don't see the left pane, click last\_page **Expand left pane** to open the pane.

3.  In the **Explorer** pane, expand the `  PROJECT  ` project node.

4.  Click **Datasets** , and then click the **DATASET** dataset.

5.  Click **Overview \> Tables** , and then click the **TABLE** table.

6.  Click **Share** . The **Share** pane opens.

7.  Click **Add Principal** . The **Grant access** pane opens.

8.  In **New principals** , enter the email address of the service account: **snapshot-bot@ PROJECT .iam.gserviceaccount.com** .

9.  From the **Select a role** dropdown, select the [**BigQuery Data Editor**](/bigquery/docs/access-control#bigquery) role.

10. Click **Save** .

11. In the **Share** pane, expand the **BigQuery Data Editor** node and verify that the **snapshot-bot@ PROJECT .iam.gserviceaccount.com** service account is listed.

12. Click **Close** .

### bq

1.  In Google Cloud console, activate Cloud Shell:

2.  Enter the following [`  bq add-iam-policy-binding  `](/bigquery/docs/reference/bq-cli-reference#bq_add-iam-policy-binding) command:
    
    ``` text
    bq add-iam-policy-binding \
    --member=serviceAccount:snapshot-bot@PROJECT.iam.gserviceaccount.com \
    --role=roles/bigquery.dataEditor DATASET.TABLE
    ```

BigQuery confirms that the new policy binding has been added.

### Permission to create tables in the destination dataset

Give the `  snapshot-bot  ` service account the permissions that it needs to create table snapshots in the `  BACKUP  ` dataset as follows:

### Console

1.  In Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :

3.  In the **Explorer** pane, expand the `  PROJECT  ` project node.

4.  Click **Datasets** , and then click the **BACKUP** dataset.

5.  Click **Share \> Manage permissions** . The dataset permissions pane opens.

6.  Click **Add principal** . In the **New principals** field, enter the service account's email address: **snapshot-bot@ PROJECT .iam.gserviceaccount.com** .

7.  From the **Select a role** dropdown, select the [**BigQuery Data Owner**](/bigquery/docs/access-control#bigquery) role.

8.  Click **Save** .

9.  On the dataset permissions pane, verify that the **snapshot-bot@ PROJECT .iam.gserviceaccount.com** service account is listed under the **BigQuery Data Owner** node.

10. Click **Close** .

Your `  snapshot-bot  ` service account now has the following IAM roles for the following resources:

<table>
<thead>
<tr class="header">
<th>Role</th>
<th>Resource</th>
<th>Resource type</th>
<th>Purpose</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>BigQuery Data Editor</td>
<td><code dir="ltr" translate="no">         PROJECT              :               DATASET              .               TABLE       </code></td>
<td>Table</td>
<td>Take snapshots of the <code dir="ltr" translate="no">         TABLE       </code> table.</td>
</tr>
<tr class="even">
<td>BigQuery Data Owner</td>
<td><code dir="ltr" translate="no">         PROJECT              :               BACKUP       </code></td>
<td>Dataset</td>
<td>Create and delete table snapshots in the <code dir="ltr" translate="no">         BACKUP       </code> dataset.</td>
</tr>
<tr class="odd">
<td>BigQuery User</td>
<td><code dir="ltr" translate="no">         PROJECT       </code></td>
<td>Project</td>
<td>Run the scheduled query that creates the table snapshots.</td>
</tr>
</tbody>
</table>

These roles provide the permissions that the `  snapshot-bot  ` service account needs to run queries that create table snapshots of the `  DATASET . TABLE  ` table and place the table snapshots in the `  BACKUP  ` dataset.

## Write a multi-statement query

This section describes how to write a [multi-statement query](/bigquery/docs/multi-statement-queries) that creates a [table snapshot](/bigquery/docs/table-snapshots-intro) of the `  DATASET . TABLE  ` table by using the [`  CREATE SNAPSHOT TABLE  ` DDL statement](/bigquery/docs/reference/standard-sql/data-definition-language#create_snapshot_table_statement) . The snapshot is saved in the `  BACKUP  ` dataset and it expires after one day.

``` text
-- Declare variables
DECLARE snapshot_name STRING;
DECLARE expiration TIMESTAMP;
DECLARE query STRING;

-- Set variables
SET expiration = DATE_ADD(current_timestamp(), INTERVAL 1 DAY);
SET snapshot_name = CONCAT(
                      "BACKUP.TABLE_",
                      FORMAT_DATETIME('%Y%m%d', current_date()));

-- Construct the query to create the snapshot
SET query = CONCAT(
              "CREATE SNAPSHOT TABLE ",
              snapshot_name,
              " CLONE mydataset.mytable OPTIONS(expiration_timestamp = TIMESTAMP '",
              expiration,
              "');");

-- Run the query
EXECUTE IMMEDIATE query;
```

## Schedule the monthly query

[Schedule](/bigquery/docs/scheduling-queries) your query to run at 5:00 AM on the first day of every month as follows:

### bq

1.  In Google Cloud console, activate Cloud Shell:

2.  Enter the following [`  bq query  `](/bigquery/docs/reference/bq-cli-reference#bq_query) command:
    
    ``` text
    bq query --use_legacy_sql=false --display_name="Monthly snapshots of the TABLE table" \
    --location="us" --schedule="1 of month 05:00" \
    --project_id=PROJECT \
    'DECLARE snapshot_name STRING;
    DECLARE expiration TIMESTAMP;
    DECLARE query STRING;
    SET expiration = DATE_ADD(@run_time, INTERVAL 40 DAY);
    SET snapshot_name = CONCAT("BACKUP.TABLE_",
      FORMAT_DATETIME("%Y%m%d", @run_date));
    SET query = CONCAT("CREATE SNAPSHOT TABLE ", snapshot_name,
      " CLONE PROJECT.DATASET.TABLE OPTIONS(expiration_timestamp=TIMESTAMP \"",
      expiration, "\");");
    EXECUTE IMMEDIATE query;'
    ```

3.  BigQuery schedules the query.

The multi-statement query in the bq command-line tool command differs from the query you ran in Google Cloud console as follows:

  - The bq command-line tool query uses `  @run_date  ` instead of `  current_date()  ` . In a scheduled query, the `  @run_date  ` parameter contains the current date. But in an interactive query, the `  @run_date  ` parameter is not supported. You can use `  current_date()  ` instead of `  @run_date  ` for testing an interactive query before you schedule it.
  - The bq command-line tool query uses `  @run_time  ` instead of `  current_timestamp()  ` for a similar reason—the `  @run_time  ` parameter is not supported in interactive queries, but `  current_timestamp()  ` can be used instead of `  @run_time  ` for testing the interactive query.
  - The bq command-line tool query uses a slash and a double quote `  \"  ` instead of a single quote `  '  ` because single quotes are used to enclose the query.

## Configure the service account to run the scheduled query

The query is currently scheduled to run using your credentials. Update your scheduled query to run with the `  snapshot-bot  ` service account credentials as follows:

1.  Run the [`  bq ls  `](/bigquery/docs/reference/bq-cli-reference#bq_ls) command to get the identity of the scheduled query job:
    
    ``` text
    bq ls --transfer_config=true --transfer_location=us
    ```
    
    The output looks similar to the following:
    
    <table>
    <thead>
    <tr class="header">
    <th><code dir="ltr" translate="no">         name        </code></th>
    <th><code dir="ltr" translate="no">         displayName        </code></th>
    <th><code dir="ltr" translate="no">         dataSourceId        </code></th>
    <th><code dir="ltr" translate="no">         state        </code></th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><code dir="ltr" translate="no">         projects/12345/locations/us/transferConfigs/12345        </code></td>
    <td><code dir="ltr" translate="no">         Monthly snapshots of the                   TABLE                  table        </code></td>
    <td><code dir="ltr" translate="no">         scheduled_query        </code></td>
    <td><code dir="ltr" translate="no">         RUNNING        </code></td>
    </tr>
    </tbody>
    </table>

2.  Using the identifier in the **`  name  `** field, run the following [`  bq update  `](/bigquery/docs/reference/bq-cli-reference#bq_update) command:
    
    ``` text
    bq update --transfer_config --update_credentials \
    --service_account_name=snapshot-bot@PROJECT.iam.gserviceaccount.com \
    projects/12345/locations/us/transferConfigs/12345
    ```

Cloud Shell confirms that the scheduled query has been successfully updated.

## Check your work

This section describes how to verify that your query is scheduled correctly, how to see if there were any errors when your query ran, and how to verify that the monthly snapshots are being created.

### View the scheduled query

To verify that BigQuery has scheduled your monthly table snapshots query, follow these steps:

### Console

1.  In Google Cloud console, go to the **Scheduled queries** page:

2.  Click **Monthly snapshots of the TABLE table** .

3.  Click **Configuration** .

4.  Verify that the **Query string** contains your query, and that your query is scheduled to run on the first day of every month.

### View the scheduled query's run history

After the scheduled query has run, you can see whether it ran successfully as follows:

### Console

1.  In Google Cloud console, go to the **Scheduled queries** page:

2.  Click the query description, **Monthly snapshots of the TABLE table** .

3.  Click **Run history** .

You can see the date and time that the query ran, whether the run was successful, and if not, what errors occurred. To see more details about a particular run, click its row in the **Run history** table. The **Run details** pane displays additional details.

### View the table snapshots

To verify that the table snapshots are being created, follow these steps:

### Console

1.  In Google Cloud console, go to the **BigQuery** page:

2.  In the left pane, click explore **Explorer** :

3.  In the **Explorer** pane, open the `  BACKUP  ` dataset and verify that the `  TABLE _YYYYMMDD  ` snapshots have been created, where `  YYYYMMDD  ` is the first day of each month.
    
    For example:
    
      - `  TABLE _20220601  `
      - `  TABLE _20220701  `
      - `  TABLE _20220801  `

## What's next

  - For more information about table snapshots, see [Working with table snapshots](/bigquery/docs/table-snapshots-intro) .
  - For more information about scheduling queries, see [Scheduling queries](/bigquery/docs/scheduling-queries) .
  - For more information about Google Cloud service accounts, see [Service accounts](/iam/docs/service-accounts) .
