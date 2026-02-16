# Get data insights from a contribution analysis model using a summable ratio metric

In this tutorial, you use a [contribution analysis](/bigquery/docs/contribution-analysis) model to analyze the contribution of the cost of sales ratio in the Iowa liquor sales dataset. This tutorial guides you through performing the following tasks:

  - Create an input table based on publicly available Iowa liquor data.
  - Create a [contribution analysis model](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-contribution-analysis) that uses a [summable ratio metric](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-contribution-analysis#use_a_summable_ratio_metric) . This type of model summarizes the values of two numeric columns and determines the ratio differences across the control and test dataset for each segment of the data.
  - Get the metric insights from the model by using the [`  ML.GET_INSIGHTS  ` function](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-get-insights) .

Before starting this tutorial, you should be familiar with the [contribution analysis](/bigquery/docs/contribution-analysis) use case.

## Required permissions

  - To create the dataset, you need the `  bigquery.datasets.create  ` Identity and Access Management (IAM) permission.

  - To create the model, you need the following permissions:
    
      - `  bigquery.jobs.create  `
      - `  bigquery.models.create  `
      - `  bigquery.models.getData  `
      - `  bigquery.models.updateData  `

  - To run inference, you need the following permissions:
    
      - `  bigquery.models.getData  `
      - `  bigquery.jobs.create  `

## Costs

In this document, you use the following billable components of Google Cloud:

  - **BigQuery ML** : You incur costs for the data that you process in BigQuery.

To generate a cost estimate based on your projected usage, use the [pricing calculator](/products/calculator) .

New Google Cloud users might be eligible for a [free trial](/free) .

For more information about BigQuery pricing, see [BigQuery pricing](https://cloud.google.com/bigquery/pricing) in the BigQuery documentation.

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

## Create a dataset

Create a BigQuery dataset to store your ML model.

### Console

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the **Explorer** pane, click your project name.

3.  Click more\_vert **View actions \> Create dataset**

4.  On the **Create dataset** page, do the following:
    
      - For **Dataset ID** , enter `  bqml_tutorial  ` .
    
      - For **Location type** , select **Multi-region** , and then select **US (multiple regions in United States)** .
    
      - Leave the remaining default settings as they are, and click **Create dataset** .

### bq

To create a new dataset, use the [`  bq mk  `](/bigquery/docs/reference/bq-cli-reference#mk-dataset) command with the `  --location  ` flag. For a full list of possible parameters, see the [`  bq mk --dataset  ` command](/bigquery/docs/reference/bq-cli-reference#mk-dataset) reference.

1.  Create a dataset named `  bqml_tutorial  ` with the data location set to `  US  ` and a description of `  BigQuery ML tutorial dataset  ` :
    
    ``` text
    bq --location=US mk -d \
     --description "BigQuery ML tutorial dataset." \
     bqml_tutorial
    ```
    
    Instead of using the `  --dataset  ` flag, the command uses the `  -d  ` shortcut. If you omit `  -d  ` and `  --dataset  ` , the command defaults to creating a dataset.

2.  Confirm that the dataset was created:
    
    ``` text
    bq ls
    ```

### API

Call the [`  datasets.insert  `](/bigquery/docs/reference/rest/v2/datasets/insert) method with a defined [dataset resource](/bigquery/docs/reference/rest/v2/datasets) .

``` text
{
  "datasetReference": {
     "datasetId": "bqml_tutorial"
  }
}
```

### BigQuery DataFrames

Before trying this sample, follow the BigQuery DataFrames setup instructions in the [BigQuery quickstart using BigQuery DataFrames](/bigquery/docs/dataframes-quickstart) . For more information, see the [BigQuery DataFrames reference documentation](/python/docs/reference/bigframes/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up ADC for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
import google.cloud.bigquery

bqclient = google.cloud.bigquery.Client()
bqclient.create_dataset("bqml_tutorial", exists_ok=True)
```

## Create a table of input data

Create a table that contains test and control data to analyze. The following query creates two intermediate tables, a test table for liquor data from 2021 and a control table with liquor data from 2020, and then performs a union of the intermediate tables to create a table with both test and control rows and the same set of columns.

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, run the following statement:
    
    ``` text
    CREATE OR REPLACE TABLE bqml_tutorial.iowa_liquor_sales_data AS
    (SELECT
      store_name,
      city,
      vendor_name,
      category_name,
      item_description,
      SUM(sale_dollars) AS total_sales,
      SUM(state_bottle_cost) AS total_bottle_cost,
      FALSE AS is_test
    FROM `bigquery-public-data.iowa_liquor_sales.sales`
    WHERE EXTRACT(YEAR FROM date) = 2020
    GROUP BY store_name, city, vendor_name, category_name, item_description, is_test)
    UNION ALL
    (SELECT
      store_name,
      city,
      vendor_name,
      category_name,
      item_description,
      SUM(sale_dollars) AS total_sales,
      SUM(state_bottle_cost) AS total_bottle_cost,
      TRUE AS is_test
    FROM `bigquery-public-data.iowa_liquor_sales.sales`
    WHERE EXTRACT(YEAR FROM date) = 2021
    GROUP BY store_name, city, vendor_name, category_name, item_description, is_test);
    ```

## Create the model

Create a contribution analysis model:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, run the following statement:
    
    ``` text
    CREATE OR REPLACE MODEL bqml_tutorial.liquor_sales_model
    OPTIONS(
      model_type = 'CONTRIBUTION_ANALYSIS',
      contribution_metric = 'sum(total_bottle_cost)/sum(total_sales)',
      dimension_id_cols = ['store_name', 'city', 'vendor_name', 'category_name', 'item_description'],
      is_test_col = 'is_test',
      min_apriori_support = 0.05
    ) AS
    SELECT * FROM bqml_tutorial.iowa_liquor_sales_data;
    ```

The query takes approximately 35 seconds to complete, after which the model `  liquor_sales_model  ` appears in the `  bqml_tutorial  ` dataset. Because the query uses a `  CREATE MODEL  ` statement to create a model, there are no query results.

## Get insights from the model

Get insights generated by the contribution analysis model by using the `  ML.GET_INSIGHTS  ` function.

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, run the following statement to select columns from the [output for a summable ratio metric contribution analysis model](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-get-insights#output_for_summable_ratio_metric_contribution_analysis_models) :
    
    ``` text
    SELECT
    contributors,
    metric_test,
    metric_control,
    metric_test_over_metric_control,
    metric_test_over_complement,
    metric_control_over_complement,
    aumann_shapley_attribution,
    apriori_support
    contribution
    FROM
      ML.GET_INSIGHTS(
        MODEL `bqml_tutorial.liquor_sales_model`)
    ORDER BY aumann_shapley_attribution DESC;
    ```

The first several rows of the output should look similar to the following. The values are truncated to improve readability.

<table>
<thead>
<tr class="header">
<th>contributors</th>
<th>metric_test</th>
<th>metric_control</th>
<th>metric_test_over_metric_control</th>
<th>metric_test_over_complement</th>
<th>metric_control_over_complement</th>
<th>aumann_shapley_attribution</th>
<th>apriori_support</th>
<th>contribution</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>all</td>
<td>0.069</td>
<td>0.071</td>
<td>0.969</td>
<td>null</td>
<td>null</td>
<td>-0.00219</td>
<td>1.0</td>
<td>0.00219</td>
</tr>
<tr class="even">
<td>city=DES MOINES</td>
<td>0.048</td>
<td>0.054</td>
<td>0.88</td>
<td>0.67</td>
<td>0.747</td>
<td>-0.00108</td>
<td>0.08</td>
<td>0.00108</td>
</tr>
<tr class="odd">
<td>vendor_name=DIAGEO AMERICAS</td>
<td>0.064</td>
<td>0.068</td>
<td>0.937</td>
<td>0.917</td>
<td>0.956</td>
<td>-0.0009</td>
<td>0.184</td>
<td>0.0009</td>
</tr>
<tr class="even">
<td>vendor_name=BACARDI USA INC</td>
<td>0.071</td>
<td>0.082</td>
<td>0.857</td>
<td>1.025</td>
<td>1.167</td>
<td>-0.00054</td>
<td>0.057</td>
<td>0.00054</td>
</tr>
<tr class="odd">
<td>vendor_name=PERNOD RICARD USA</td>
<td>0.068</td>
<td>0.077</td>
<td>0.89</td>
<td>0.988</td>
<td>1.082</td>
<td>-0.0005</td>
<td>0.061</td>
<td>0.0005</td>
</tr>
</tbody>
</table>

In the output, you can see that the data segment `  city=DES MOINES  ` has the highest contribution of change in the sales ratio. You can also see this difference in the `  metric_test  ` and `  metric_control  ` columns, which show that the ratio decreased in the test data compared to the control data. Other metrics, such as `  metric_test_over_metric_control  ` , `  metric_test_over_complement  ` , and `  metric_control_over_complement  ` , compute additional statistics that describe the relationship between the control and test ratios and how they relate to the overall population. For more information, see [Output for summable ratio metric contribution analysis models](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-get-insights#output_for_summable_ratio_metric_contribution_analysis_models) .

## Clean up

**Caution** : Deleting a project has the following effects:

  - **Everything in the project is deleted.** If you used an existing project for the tasks in this document, when you delete it, you also delete any other work you've done in the project.
  - **Custom project IDs are lost.** When you created this project, you might have created a custom project ID that you want to use in the future. To preserve the URLs that use the project ID, such as an `  appspot.com  ` URL, delete selected resources inside the project instead of deleting the whole project.

If you plan to explore multiple architectures, tutorials, or quickstarts, reusing projects can help you avoid exceeding project quota limits.

In the Google Cloud console, go to the **Manage resources** page.

In the project list, select the project that you want to delete, and then click **Delete** .

In the dialog, type the project ID, and then click **Shut down** to delete the project.
