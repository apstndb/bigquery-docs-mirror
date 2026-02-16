You can explore BigQuery query results by using [Colab Enterprise notebooks](/colab/docs/introduction) in BigQuery.

In this tutorial, you query data from a [BigQuery public dataset](/bigquery/public-data) and explore the query results in a notebook.

## Objectives

  - Create and run a query in BigQuery.
  - Explore query results in a notebook.

## Costs

This tutorial uses a dataset available through the [Google Cloud Public Datasets Program](https://cloud.google.com/blog/products/data-analytics/big-data-analytics-in-the-cloud-with-free-public-datasets) . Google pays for the storage of these datasets and provides public access to the data. You incur charges for the queries that you perform on the data. For more information, see [BigQuery pricing](https://cloud.google.com/bigquery/pricing) .

## Before you begin

1.  In the Google Cloud console, on the project selector page, select or create a Google Cloud project.
    
    **Roles required to select or create a project**
    
      - **Select a project** : Selecting a project doesn't require a specific IAM role—you can select any project that you've been granted a role on.
      - **Create a project** : To create a project, you need the Project Creator role ( `  roles/resourcemanager.projectCreator  ` ), which contains the `  resourcemanager.projects.create  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .
    
    **Note** : If you don't plan to keep the resources that you create in this procedure, create a project instead of selecting an existing project. After you finish these steps, you can delete the project, removing all resources associated with the project.

2.  [Verify that billing is enabled for your Google Cloud project](/billing/docs/how-to/verify-billing-enabled#confirm_billing_is_enabled_on_a_project) .

3.  Enable the BigQuery API.
    
    **Roles required to enable APIs**
    
    To enable APIs, you need the Service Usage Admin IAM role ( `  roles/serviceusage.serviceUsageAdmin  ` ), which contains the `  serviceusage.services.enable  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .
    
    For new projects, BigQuery is automatically enabled.

## Set the default region for code assets

If this is the first time you are creating a code asset, you should set the default region for code assets. You can't change the region for a code asset after it is created.

**Note:** If you create a code asset and choose a different default region than the one you have been using for code assets—for example, choosing `  us-west1  ` when you have been using `  us-central1  ` —then that code asset and all code assets you create afterwards use that new region by default. Existing code assets continue to use the region they were assigned when they were created.

All code assets in BigQuery Studio use the same default region. To set the default region for code assets, follow these steps:

1.  Go to the **BigQuery** page.

2.  In the **Explorer** pane, find the project in which you have enabled code assets.

3.  Click more\_vert **View actions** next to the project, and then click **Change my default code region** .

4.  For **Region** , select the region that you want to use for code assets.

5.  Click **Select** .

For a list of supported regions, see [BigQuery Studio locations](/bigquery/docs/locations#bqstudio-loc) .

### Required permissions

To create and run notebooks, you need the following Identity and Access Management (IAM) roles:

  - [BigQuery User ( `  roles/bigquery.user  ` )](/bigquery/docs/access-control#bigquery.user)
  - [Notebook Runtime User ( `  roles/aiplatform.notebookRuntimeUser  ` )](/vertex-ai/docs/general/access-control#aiplatform.notebookRuntimeUser)
  - [Code Creator ( `  roles/dataform.codeCreator  ` )](/dataform/docs/access-control#dataform.codeCreator)

## Open query results in a notebook

You can run a SQL query and then use a notebook to explore the data. This approach is useful if you want to modify the data in BigQuery before working with it, or if you need only a subset of the fields in the table.

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the **Type to search** field, enter `  bigquery-public-data  ` .
    
    If the project is not shown, enter `  bigquery  ` in the search field, and then click **Search to all projects** to match the search string with the existing projects.

3.  Select **bigquery-public-data \> ml\_datasets \> penguins** .

4.  For the **penguins** table, click more\_vert **View actions** , and then click **Query** .

5.  Add an asterisk ( `  *  ` ) for field selection to the generated query, so that it reads like the following example:
    
    ``` text
    SELECT * FROM `bigquery-public-data.ml_datasets.penguins` LIMIT 1000;
    ```

6.  Click play\_circle **Run** .

7.  In the **Query results** section, click **Open in** , and then click **Notebook** .

## Prepare the notebook for use

Prepare the notebook for use by connecting to a runtime and setting application default values.

1.  In the notebook header, click **Connect** to [connect to the default runtime](/bigquery/docs/create-notebooks#connect_to_the_default_runtime) .
2.  In the **Setup** code block, click play\_circle **Run cell** .

## Explore the data

1.  To load the **penguins** data into a [BigQuery DataFrame](/bigquery/docs/reference/bigquery-dataframes) and show the results, click play\_circle **Run cell** in the code block in the **Result set loaded from BigQuery job as a DataFrame** section.
2.  To get descriptive metrics for the data, click play\_circle **Run cell** in the code block in the **Show descriptive statistics using describe()** section.
3.  Optional: Use other Python functions or packages to explore and analyze the data.

The following code sample shows using [`  bigframes.pandas  `](/bigquery/docs/bigquery-dataframes-introduction) to analyze data, and [`  bigframes.ml  `](/bigquery/docs/dataframes-ml-ai) to create a linear regression model from **penguins** data in a BigQuery DataFrame:

``` python
import bigframes.pandas as bpd

# Load data from BigQuery
query_or_table = "bigquery-public-data.ml_datasets.penguins"
bq_df = bpd.read_gbq(query_or_table)

# Inspect one of the columns (or series) of the DataFrame:
bq_df["body_mass_g"]

# Compute the mean of this series:
average_body_mass = bq_df["body_mass_g"].mean()
print(f"average_body_mass: {average_body_mass}")

# Find the heaviest species using the groupby operation to calculate the
# mean body_mass_g:
(
    bq_df["body_mass_g"]
    .groupby(by=bq_df["species"])
    .mean()
    .sort_values(ascending=False)
    .head(10)
)

# Create the Linear Regression model
from bigframes.ml.linear_model import LinearRegression

# Filter down to the data we want to analyze
adelie_data = bq_df[bq_df.species == "Adelie Penguin (Pygoscelis adeliae)"]

# Drop the columns we don't care about
adelie_data = adelie_data.drop(columns=["species"])

# Drop rows with nulls to get our training data
training_data = adelie_data.dropna()

# Pick feature columns and label column
X = training_data[
    [
        "island",
        "culmen_length_mm",
        "culmen_depth_mm",
        "flipper_length_mm",
        "sex",
    ]
]
y = training_data[["body_mass_g"]]

model = LinearRegression(fit_intercept=False)
model.fit(X, y)
model.score(X, y)
```

## Clean up

To avoid incurring charges to your Google Cloud account for the resources used in this tutorial, either delete the project that contains the resources, or keep the project and delete the individual resources.

The easiest way to eliminate billing is to delete the Google Cloud project that you created for this tutorial.

**Caution** : Deleting a project has the following effects:

  - **Everything in the project is deleted.** If you used an existing project for the tasks in this document, when you delete it, you also delete any other work you've done in the project.
  - **Custom project IDs are lost.** When you created this project, you might have created a custom project ID that you want to use in the future. To preserve the URLs that use the project ID, such as an `  appspot.com  ` URL, delete selected resources inside the project instead of deleting the whole project.

If you plan to explore multiple architectures, tutorials, or quickstarts, reusing projects can help you avoid exceeding project quota limits.

In the Google Cloud console, go to the **Manage resources** page.

In the project list, select the project that you want to delete, and then click **Delete** .

In the dialog, type the project ID, and then click **Shut down** to delete the project.

## What's next

  - Learn more about [creating notebooks in BigQuery](/bigquery/docs/create-notebooks) .
  - Learn more about [exploring data with BigQuery DataFrames](/bigquery/docs/bigquery-dataframes-introduction) .
