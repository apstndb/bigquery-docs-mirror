# Visualize query results

**Preview**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

Use this quickstart to run SQL and visualize your results in a [BigQuery notebook](/bigquery/docs/notebooks-introduction) :

  - Run a query using the `  bigquery-public-data.ml_datasets.penguins  ` public dataset.
  - Use a SQL cell to iterate on your query results.
  - Use a visualization cell to display the average culmen length and depth of female penguins for each species.

## Before you begin

1.  Sign in to your Google Cloud account. If you're new to Google Cloud, [create an account](https://console.cloud.google.com/freetrial) to evaluate how our products perform in real-world scenarios. New customers also get $300 in free credits to run, test, and deploy workloads.

2.  In the Google Cloud console, on the project selector page, select or create a Google Cloud project.
    
    **Roles required to select or create a project**
    
      - **Select a project** : Selecting a project doesn't require a specific IAM role—you can select any project that you've been granted a role on.
      - **Create a project** : To create a project, you need the Project Creator role ( `  roles/resourcemanager.projectCreator  ` ), which contains the `  resourcemanager.projects.create  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .
    
    **Note** : If you don't plan to keep the resources that you create in this procedure, create a project instead of selecting an existing project. After you finish these steps, you can delete the project, removing all resources associated with the project.

3.  In the Google Cloud console, on the project selector page, select or create a Google Cloud project.
    
    **Roles required to select or create a project**
    
      - **Select a project** : Selecting a project doesn't require a specific IAM role—you can select any project that you've been granted a role on.
      - **Create a project** : To create a project, you need the Project Creator role ( `  roles/resourcemanager.projectCreator  ` ), which contains the `  resourcemanager.projects.create  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .
    
    **Note** : If you don't plan to keep the resources that you create in this procedure, create a project instead of selecting an existing project. After you finish these steps, you can delete the project, removing all resources associated with the project.

4.  [Verify that billing is enabled for your Google Cloud project](/billing/docs/how-to/verify-billing-enabled#confirm_billing_is_enabled_on_a_project) .

5.  Verify that the BigQuery API is enabled.
    
    If you created a new project, the BigQuery API is automatically enabled.

### Required permissions

To create and run notebooks, you need the following Identity and Access Management (IAM) roles:

  - [BigQuery User ( `  roles/bigquery.user  ` )](/bigquery/docs/access-control#bigquery.user)
  - [Colab Enterprise User ( `  roles/aiplatform.colabEnterpriseUser  ` )](/vertex-ai/docs/general/access-control#aiplatform.colabEnterpriseUser)

## Create a notebook

Follow the instructions in [Create a notebook from the BigQuery editor](/bigquery/docs/create-notebooks#create-notebook-console) to create a new notebook.

## Run a query

To run a SQL query in a notebook, follow these steps:

1.  To create a new SQL cell in your notebook, click add **SQL** .

2.  Enter the following query:
    
    ``` text
    SELECT * FROM `bigquery-public-data.ml_datasets.penguins`;
    ```

3.  Click play\_circle **Run cell** .
    
    The results of the query are automatically saved in a DataFrame called `  df  ` .

4.  Create another SQL cell and change the title to `  female_penguins  ` .

5.  Enter the following query, which references the DataFrame you just created and filters the results to only include female penguins:
    
    ``` text
    SELECT * FROM {df} WHERE sex = 'FEMALE';
    ```

6.  Click play\_circle **Run cell** .
    
    The results of the query are automatically saved in a DataFrame called `  female_penguins  ` .

## Visualize results

1.  To create a new visualization cell in your notebook, click add **Visualization** .

2.  Click **Choose a dataframe** and then select `  female_penguins  ` .
    
    A chart interface appears.

3.  Click **Scatter chart** to open a chart menu, then select the bar\_chart **Vertical bar chart** .

4.  In the **Metric** section, check that `  culmen_length_mm  ` and `  culmen_depth_mm  ` appear. If a metric is missing, click add\_circle\_outline **Add metric** and select it. To remove a metric, hold the pointer over the metric name and then click close **Close** .

5.  For each metric, click edit **Edit** . For **Aggregation** select **Average** .

## Clean up

The easiest way to eliminate billing is to delete the project that you created for the tutorial.

To delete the project:

**Caution** : Deleting a project has the following effects:

  - **Everything in the project is deleted.** If you used an existing project for the tasks in this document, when you delete it, you also delete any other work you've done in the project.
  - **Custom project IDs are lost.** When you created this project, you might have created a custom project ID that you want to use in the future. To preserve the URLs that use the project ID, such as an `  appspot.com  ` URL, delete selected resources inside the project instead of deleting the whole project.

If you plan to explore multiple architectures, tutorials, or quickstarts, reusing projects can help you avoid exceeding project quota limits.

In the Google Cloud console, go to the **Manage resources** page.

In the project list, select the project that you want to delete, and then click **Delete** .

In the dialog, type the project ID, and then click **Shut down** to delete the project.

## What's next

  - Learn more about [BigQuery DataFrames](/bigquery/docs/bigquery-dataframes-introduction) .
  - Learn more about [SQL cells in Colab Enterprise](/colab/docs/sql-cells) .
  - Learn more about [visualization cells in Colab Enterprise](/colab/docs/visualization-cells) .
  - Learn how to [visualize graphs using BigQuery DataFrames](/bigquery/docs/dataframes-visualizations) .
  - Learn how to [use a BigQuery DataFrames notebook](https://github.com/googleapis/python-bigquery-dataframes/tree/main/notebooks/getting_started/getting_started_bq_dataframes.ipynb) .
