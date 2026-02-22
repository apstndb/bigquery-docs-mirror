# Use the bq tool

In this tutorial, you learn how to use `  bq  ` , the Python-based command-line interface (CLI) tool for BigQuery to create a dataset, load sample data, and query tables. After completing this tutorial, you'll be familiar with `  bq  ` and how to work with BigQuery by using a CLI.

For a complete reference of all `  bq  ` commands and flags, see the [bq command-line tool reference](/bigquery/docs/reference/bq-cli-reference) .

To follow step-by-step guidance for this task directly in the Google Cloud console, click **Guide me** :

## Before you begin

1.  Enable the BigQuery API:
    
    **Roles required to enable APIs**
    
    To enable APIs, you need the Service Usage Admin IAM role ( `  roles/serviceusage.serviceUsageAdmin  ` ), which contains the `  serviceusage.services.enable  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .
    
    ``` text
    gcloud services enable bigquery
    ```
    
    For new projects, the BigQuery API is automatically enabled.

2.  Optional: [Enable billing](/billing/docs/how-to/modify-project) for the project. If you don't want to enable billing or provide a credit card, the steps in this document still work. BigQuery provides you a sandbox to perform the steps. For more information, see [Enable the BigQuery sandbox](/bigquery/docs/sandbox#setup) .
    
    **Note:** If your project has a billing account and you want to use the BigQuery sandbox, then [disable billing for your project](/billing/docs/how-to/modify-project#disable_billing_for_a_project) .

### Required roles

To get the permissions that you need to create a dataset, create a table, load data, and query data, ask your administrator to grant you the following IAM roles on the project:

  - Run load jobs and query jobs: [BigQuery Job User](/iam/docs/roles-permissions/bigquery#bigquery.jobUser) ( `  roles/bigquery.jobUser  ` )
  - Create a dataset, create a table, load data into a table, and query a table: [BigQuery Data Editor](/iam/docs/roles-permissions/bigquery#bigquery.dataEditor) ( `  roles/bigquery.dataEditor  ` )

For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

## Download the file that contains the source data

The file that you're downloading contains approximately 7 MB of data about popular baby names. It's provided by the US Social Security Administration.

For more information about the data, see the Social Security Administration's [Background information for popular names](http://www.ssa.gov/OACT/babynames/background.html) .

1.  Download the US Social Security Administration's data by opening the following URL in a new browser tab:
    
    ``` text
    https://www.ssa.gov/OACT/babynames/names.zip
    ```

2.  Extract the file.
    
    For more information about the dataset schema, see the `  NationalReadMe.pdf  ` file you extracted.

3.  To see what the data looks like, open the `  yob2024.txt  ` file. This file contains comma-separated values for name, assigned sex at birth, and number of children with that name. The file has no header row.

4.  Move the file to your working directory.
    
      - If you're working in Cloud Shell, click more\_vert **More** **Upload** , click **Choose Files** , choose the `  yob2024.txt  ` file, and then click **Upload** .
    
      - If you're working in a local shell, copy or move the file `  yob2024.txt  ` into the directory where you're running the bq tool.

## Create a dataset

1.  If you launched Cloud Shell from the documentation, enter the following command to set your project ID. This prevents you from having to specify the project ID in each CLI command.
    
    ``` text
    gcloud config set project PROJECT_ID
    ```
    
    Replace PROJECT\_ID with your project ID.

<!-- end list -->

1.  Enter the following command to create a dataset named `  babynames  ` :
    
    ``` text
    bq mk --dataset babynames
    ```
    
    The output is similar to the following:
    
    ``` text
    Dataset 'babynames' successfully created.
    ```

2.  Confirm that the dataset `  babynames  ` now appears in your project:
    
    ``` text
    bq ls --datasets=true
    ```
    
    The output is similar to the following:
    
    ``` text
      datasetId
    -------------
      babynames
    ```

## Load data into a table

1.  In the `  babynames  ` dataset, load the source file `  yob2024.txt  ` into a new table named `  names2024  ` :
    
    ``` text
    bq load babynames.names2024 yob2024.txt name:string,assigned_sex_at_birth:string,count:integer
    ```
    
    The output is similar to the following:
    
    ``` text
    Upload complete.
    Waiting on bqjob_r3c045d7cbe5ca6d2_0000018292f0815f_1 ... (1s) Current status: DONE
    ```

2.  Confirm that the table `  names2024  ` now appears in the `  babynames  ` dataset:
    
    ``` text
    bq ls --format=pretty babynames
    ```
    
    The output is similar to the following. Some columns are omitted to simplify the output.
    
    ``` text
    +-----------+-------+
    |  tableId  | Type  |
    +-----------+-------+
    | names2024 | TABLE |
    +-----------+-------+
    ```

3.  Confirm that the table schema of your new `  names2024  ` table is `  name: string  ` , `  assigned_sex_at_birth: string  ` , and `  count: integer  ` :
    
    ``` text
    bq show babynames.names2024
    ```
    
    The output is similar to the following. Some columns are omitted to simplify the output.
    
    ``` text
      Last modified        Schema                      Total Rows   Total Bytes
    ----------------- ------------------------------- ------------ ------------
    14 Mar 17:16:45   |- name: string                    31904       607494
                      |- assigned_sex_at_birth: string
                      |- count: integer
    ```

## Query table data

1.  Determine the most popular girls' names in the data:
    
    ``` text
    bq query \
        'SELECT
          name,
          count
        FROM
          babynames.names2024
        WHERE
          assigned_sex_at_birth = "F"
        ORDER BY
          count DESC
        LIMIT 5'
    ```
    
    The output is similar to the following:
    
    ``` text
    +-----------+-------+
    |   name    | count |
    +-----------+-------+
    | Olivia    | 14718 |
    | Emma      | 13485 |
    | Amelia    | 12740 |
    | Charlotte | 12552 |
    | Mia       | 12113 |
    +-----------+-------+
    ```

2.  Determine the least popular boys' names in the data:
    
    ``` text
    bq query \
        'SELECT
          name,
          count
        FROM
          babynames.names2024
        WHERE
          assigned_sex_at_birth = "M"
        ORDER BY
          count ASC
        LIMIT 5'
    ```
    
    The output is similar to the following:
    
    ``` text
    +---------+-------+
    |  name   | count |
    +---------+-------+
    | Aaran   |     5 |
    | Aadiv   |     5 |
    | Aadarsh |     5 |
    | Aarash  |     5 |
    | Aadrik  |     5 |
    +---------+-------+
    ```
    
    The minimum count is 5 because the source data omits names with fewer than 5 occurrences.

## Clean up

To avoid incurring charges to your Google Cloud account for the resources used on this page, delete the Google Cloud project with the resources.

### Delete the project

If you used the [BigQuery sandbox](/bigquery/docs/sandbox) to query the public dataset, then billing is not enabled for your project, and you don't need to delete the project.

The easiest way to eliminate billing is to delete the project that you created for the tutorial.

To delete the project:

**Caution** : Deleting a project has the following effects:

  - **Everything in the project is deleted.** If you used an existing project for the tasks in this document, when you delete it, you also delete any other work you've done in the project.
  - **Custom project IDs are lost.** When you created this project, you might have created a custom project ID that you want to use in the future. To preserve the URLs that use the project ID, such as an `  appspot.com  ` URL, delete selected resources inside the project instead of deleting the whole project.

If you plan to explore multiple architectures, tutorials, or quickstarts, reusing projects can help you avoid exceeding project quota limits.

In the Google Cloud console, go to the **Manage resources** page.

In the project list, select the project that you want to delete, and then click **Delete** .

In the dialog, type the project ID, and then click **Shut down** to delete the project.

### Delete the resources

If you used an existing project, delete the resources that you created:

1.  Delete the `  babynames  ` dataset:
    
    ``` text
    bq rm --recursive=true babynames
    ```
    
    The `  --recursive  ` flag deletes all tables in the dataset, including the `  names2024  ` table.
    
    The output is similar to the following:
    
    ``` text
    rm: remove dataset 'myproject:babynames'? (y/N)
    ```

2.  To confirm the delete command, enter `  y  ` .

## What's next

  - Learn more about [using the bq tool](/bigquery/bq-command-line-tool) .
  - Learn about the [BigQuery sandbox](/bigquery/docs/sandbox) .
  - Learn more about [loading data into BigQuery](/bigquery/docs/loading-data) .
  - Learn more about [querying data in BigQuery](/bigquery/docs/query-overview) .
