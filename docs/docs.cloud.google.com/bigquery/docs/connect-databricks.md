---
name: documents/docs.cloud.google.com/bigquery/docs/connect-databricks
uri: https://docs.cloud.google.com/bigquery/docs/connect-databricks
title: Connect to Databricks
description: Learn how to connect to Databricks from BigQuery.
data_source: docs.cloud.google.com
---

# Connect to Databricks

As a BigQuery administrator, you can create a [connection](https://docs.cloud.google.com/bigquery/docs/connections-api-intro) for reading and writing data from a [Databricks notebook](https://docs.gcp.databricks.com/notebooks/index.html) . The steps are described using the [Google Cloud console](https://console.cloud.google.com/) and [Databricks Workspaces](https://docs.gcp.databricks.com/administration-guide/account-settings-gcp/workspaces.html) . You can also perform these steps using the `gcloud` and `databricks` command-line tools, although that guidance is outside the scope of this tutorial.

Databricks on Google Cloud is a Databricks environment hosted on Google Cloud, running on Google Kubernetes Engine (GKE) and providing built-in integration with BigQuery and other Google Cloud technologies. If you are new to Databricks, watch the [Introduction to Databricks Unified Data Platform](https://www.youtube.com/watch?v=n-yt_3HvkOI) video for an overview of the Databricks lakehouse platform.

## Objectives

  - Configure Google Cloud to connect with Databricks.
  - Deploy Databricks on Google Cloud.
  - Query BigQuery from Databricks.

## Costs

This tutorial uses billable components of Google Cloud console, including BigQuery and GKE. [BigQuery pricing](https://cloud.google.com/bigquery/pricing#data_extraction_pricing) and [GKE pricing](https://cloud.google.com/kubernetes-engine/pricing) apply. For information about costs associated with a Databricks account running on Google Cloud, see the [Set up your account and create a workspace](https://docs.gcp.databricks.com/getting-started/try-databricks-gcp.html#set-up-your-account-and-create-a-workspace) section in the Databricks documentation.

## Before you begin

Before you connect Databricks to BigQuery, complete the following steps:

1.  Enable the [BigQuery Storage API](https://docs.cloud.google.com/bigquery/docs/reference/storage) .
2.  Create a service account for Databricks.
3.  Create a Cloud Storage bucket for temporary storage.

### Enable the BigQuery Storage API

The [BigQuery Storage API](https://docs.cloud.google.com/bigquery/docs/reference/storage) is enabled by default for any new projects where BigQuery is used. For existing projects that don't have the API enabled, follow these instructions:

1.  In the Google Cloud console, go to the **BigQuery Storage API** page.

2.  Confirm that the **BigQuery Storage API** is enabled.
    
    ![BigQuery Storage API enabled](https://docs.cloud.google.com/static/bigquery/images/bigquery-storage-api.png)

### Create a service account for Databricks

Next, create an Identity and Access Management (IAM) service account to allow a Databricks cluster to execute queries against BigQuery. We recommend that you give this service account the least privileges needed to perform its tasks. See [BigQuery Roles and Permissions](https://docs.cloud.google.com/bigquery/docs/access-control) .

1.  In the Google Cloud console, go to the **Service Accounts** page.

2.  Click **Create service account** , name the service account `databricks-bigquery` , enter a brief description such as `Databricks tutorial service account` , and then click **Create and continue** .

3.  Under **Grant this service account access to project** , specify the roles for the service account. To give the service account permission to read data with the Databricks workspace and the BigQuery table in the same project, specifically without referencing a materialized view, grant the following roles:
    
      - **BigQuery Read Session User**
      - **BigQuery Data Viewer**
    
    To give permission to write data, grant the following roles:
    
      - **BigQuery Job User**
      - **BigQuery Data Editor**

4.  Record the email address of your new service account for reference in future steps.

5.  Click **Done** .

### Create a Cloud Storage bucket

To write to BigQuery, the Databricks cluster needs access to a Cloud Storage bucket to buffer the written data.

1.  In the Google Cloud console, go to the **Cloud Storage Browser** .

2.  Click **Create bucket** to open the **Create a bucket** dialog.

3.  Specify a name for the bucket used to write data to BigQuery. The bucket name must be a [globally unique name](https://docs.cloud.google.com/storage/docs/buckets#naming) . If you specify a bucket name that already exists, then Cloud Storage responds with an error message. If this occurs, specify a different name for your bucket.
    
    ![Name your bucket dialog with databricks-bq-123](https://docs.cloud.google.com/static/bigquery/images/storage-bucket-name.png)

4.  For this tutorial, use the default settings for the storage location, storage class, access control, and advanced settings.

5.  Click **Create** to create your Cloud Storage bucket.

6.  Click **Permissions** , click **Add** , and then specify the email address of the service account you created for Databricks access on the [Service Accounts page](https://console.cloud.google.com/iam-admin/serviceaccounts) .
    
    ![image](https://docs.cloud.google.com/static/bigquery/images/add-members-and-roles.png)

7.  Click **Select a role** and add the **Storage admin** role.

8.  Click **Save** .

## Deploy Databricks on Google Cloud

Complete the following steps to prepare to deploy Databricks on Google Cloud.

1.  To set up your Databricks account, follow the instructions in the Databricks documentation, [Set up your Databricks on Google Cloud account](https://docs.gcp.databricks.com/getting-started/try-databricks-gcp.html) .
2.  After you register, learn more about how to [Manage your Databricks account](https://docs.gcp.databricks.com/administration-guide/account-settings-gcp/index.html) .

### Create a Databricks workspace, cluster, and notebook

The following steps describe how to create a Databricks workspace, a cluster, and a Python notebook to write code to access BigQuery.

1.  Confirm the [Databricks prerequisites](https://docs.gcp.databricks.com/getting-started/try-databricks-gcp.html#prerequisites-for-account-and-workspace-creation) .

2.  Create your first workspace. On the [Databricks account console](https://accounts.gcp.databricks.com/workspaces) , click **Create Workspace** .

3.  Specify `gcp-bq` for the **Workspace name** and select your **Region** .
    
    ![Create Workspace screen with Workspace name, region and Google Cloud project ID](https://docs.cloud.google.com/static/bigquery/images/create-workspace-configuration.png)

4.  To determine your Google Cloud project ID, visit the Google Cloud console, and then copy the value to the **Google Cloud project ID** field.

5.  Click **Save** to create your Databricks workspace.

6.  To create a Databricks cluster with Databricks runtime 7.6 or later, in the left menu bar select **Clusters** , and then click **Create Cluster** at the top.

7.  Specify the name of your cluster and its size, then click **Advanced Options** and specify the email address of your Google Cloud service account.
    
    ![New Cluster surface with Google Service Account details](https://docs.cloud.google.com/static/bigquery/images/new-databricks-cluster.png)

8.  Click **Create Cluster** .

9.  To create a Python notebook for Databricks, follow instructions in [Create a notebook](https://docs.gcp.databricks.com/notebooks/notebooks-manage.html#create-a-notebook) .

## Querying BigQuery from Databricks

With the configuration above, you can securely connect Databricks to BigQuery. Databricks uses a fork of the [open source Google Apache Spark Adapter](https://github.com/GoogleCloudDataproc/spark-bigquery-connector) to access BigQuery.

Databricks reduces data transfer and accelerates queries by automatically pushing down certain query predicates, for example filtering on nested columns to BigQuery. In addition, the added capability to first run a SQL query on BigQuery with the `query()` API reduces the transfer size of the resulting dataset.

The following steps describe how to access a dataset in BigQuery and write your own data to BigQuery.

### Access a public dataset on BigQuery

BigQuery provides a list of available [public datasets](https://docs.cloud.google.com/bigquery/public-data) . To query the BigQuery Shakespeare dataset that is part of the public datasets, follow these steps:

1.  To read the BigQuery table, use the following code snippet in your Databricks notebook.
    
        table = "bigquery-public-data.samples.shakespeare"
        df = spark.read.format("bigquery").option("table",table).load()
        df.createOrReplaceTempView("shakespeare")
    
    Execute the code by pressing `Shift+Return` .
    
    You can now query your BigQuery table through the Apache Spark DataFrame ( `df` ). For example, use the following to show the first three rows of the dataframe:
    
        df.show(3)
    
    To query another table, update the `table` variable.

2.  A key feature of Databricks notebooks is that you can mix the cells of different languages such as Scala, Python, and SQL in a single notebook.
    
    The following SQL query allows you to visualize the word count in Shakespeare after running the previous cell that creates the temporary view.
    
        %sql
        SELECT word, SUM(word_count) AS word_count FROM words GROUP BY word ORDER BY word_count DESC LIMIT 12

    ![wordcount in shakespeare bar graph](https://docs.cloud.google.com/static/bigquery/images/word-count-in-shakespeare.png)
    
    > **Note:** The output is in tabular format by default. To change it to a bar graph, click the bar graph icon to select from the available Databricks visualizations.
    
    The cell runs a Apache Spark SQL query against the dataframe in your Databricks cluster, not in BigQuery. The benefit of this approach is that data analysis occurs on a Apache Spark level, no further BigQuery API calls are issued, and you incur no additional BigQuery costs.

3.  As an alternative, you can delegate the execution of a SQL query to BigQuery with the `query()` API and optimize for reducing the transfer size of the resulting data frame. Unlike in the previous example, where the processing was done in Apache Spark, if you use this approach, pricing and query optimizations apply for executing the query on BigQuery.
    
    The following example uses Scala, the `query()` API, and the public Shakespeare dataset in BigQuery to calculate the five most common words in Shakespeare's works. Before you run the code, you must first create an empty dataset in BigQuery called `mdataset` that the code can reference. For more information, see [Writing data to BigQuery](https://docs.cloud.google.com/bigquery/docs/connect-databricks#writing-data-to-bigquery) .
    
        %scala
        // public dataset
        val table = "bigquery-public-data.samples.shakespeare"
        
        // existing dataset where the Google Cloud user has table creation permission
        val tempLocation = "mdataset"
        // query string
        val q = s"""SELECT word, SUM(word_count) AS word_count FROM ${table}
            GROUP BY word ORDER BY word_count DESC LIMIT 10 """
        
        // read the result of a GoogleSQL query into a DataFrame
        val df2 =
          spark.read.format("bigquery")
          .option("query", q)
          .option("materializationDataset", tempLocation)
          .load()
        
        // show the top 5 common words in Shakespeare
        df2.show(5)
    
    For more code examples, see the [Databricks BigQuery sample notebook](https://docs.databricks.com/_extras/notebooks/source/big-query-python.html) .

## Writing data to BigQuery

BigQuery tables exist in [datasets](https://docs.cloud.google.com/bigquery/docs/datasets) . Before you can write data to a BigQuery table, you must create a new dataset in BigQuery. To create a dataset for a Databricks Python notebook, follow these steps:

1.  Go to the BigQuery page in the Google Cloud console.

2.  Expand the more\_vert **Actions** option, click **Create dataset** , and then name it `together` .

3.  In the Databricks Python notebook, create a Apache Spark dataframe from a Python list with three string entries using the following code snippet:
    
        from pyspark.sql.types import StringType
        mylist = ["Google", "Databricks", "better together"]
        
        df = spark.createDataFrame(mylist, StringType())

4.  Add another cell to your notebook that writes the Apache Spark dataframe from the previous step to the BigQuery table `myTable` in the dataset `together` . The table is either created or overwritten. Use the bucket name that you specified earlier.
    
        bucket = YOUR_BUCKET_NAME
        table = "together.myTable"
        
        df.write
          .format("bigquery")
          .option("temporaryGcsBucket", bucket)
          .option("table", table)
          .mode("overwrite").save()

5.  To verify that you have successfully written the data, query and display your BigQuery table through the Apache Spark DataFrame ( `df` ):
    
        display(spark.read.format("bigquery").option("table", table).load)

## Clean up

Before removing Databricks, always back up your data and notebooks. To clean up and completely remove Databricks, cancel your Databricks subscription in the Google Cloud console and remove any related resources you created from the Google Cloud console.

If you delete a Databricks workspace, the two Cloud Storage buckets with the names ` databricks- WORKSPACE_ID  ` and `databricks- WORKSPACE_ID -system` that were [created by Databricks](https://docs.gcp.databricks.com/administration-guide/account-settings-gcp/workspaces.html#secure-the-workspaces-gcs-buckets-in-your-project) might not be deleted if the Cloud Storage buckets are not empty. After workspace deletion, you can delete those objects manually in the Google Cloud console for your project.

## What's next

This section provides a list of additional documents and tutorials:

  - Learn about [Databricks free trial details](https://databricks.com/try-databricks) .
  - Learn about [Databricks on Google Cloud](https://docs.gcp.databricks.com/) .
  - Learn about [Databricks BigQuery](https://docs.databricks.com/data/data-sources/google/bigquery.html) .
  - Read the [BigQuery support for Databricks blog announcement](https://databricks.com/blog/2020/07/31/announcing-support-for-google-bigquery-in-databricks-runtime-7-1.html) .
  - Learn about [BigQuery Sample notebooks](https://docs.databricks.com/_extras/notebooks/source/big-query-python.html) .
  - Learn about [Terraform provider for Databricks on Google Cloud](https://github.com/databrickslabs/terraform-provider-databricks/blob/master/CHANGELOG.md) .
  - Read the [Databricks blog](https://databricks.com/blog/) , including more information about [data science topics](https://databricks.com/blog/2020/01/30/what-is-a-data-lakehouse.html) and [data sets](https://databricks.com/blog/2020/04/14/covid-19-datasets-now-available-on-databricks.html) .
