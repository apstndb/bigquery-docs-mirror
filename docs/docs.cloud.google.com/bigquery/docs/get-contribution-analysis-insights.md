# Get data insights from a contribution analysis model using a summable metric

In this tutorial, you use a [contribution analysis](/bigquery/docs/contribution-analysis) model to analyze sales changes between 2020 and 2021 in the Iowa liquor sales dataset. This tutorial guides you through performing the following tasks:

  - Create an input table based on publicly available Iowa liquor data.
  - Create a [contribution analysis model](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-contribution-analysis) that uses a [summable metric](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-contribution-analysis#use_a_summable_metric) . This type of model summarizes a given metric for a combination of one or more dimensions in the data, to determine how those dimensions contribute to the metric value.
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

Create a table that contains test and control data to analyze. The test table contains liquor data from 2021 and the control table contains liquor data from 2020. The following query combines the test and control data into a single input table:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, run the following statement:
    
    ``` text
    CREATE OR REPLACE TABLE bqml_tutorial.iowa_liquor_sales_sum_data AS (
      (SELECT
        store_name,
        city,
        vendor_name,
        category_name,
        item_description,
        SUM(sale_dollars) AS total_sales,
        FALSE AS is_test
      FROM `bigquery-public-data.iowa_liquor_sales.sales`
      WHERE EXTRACT(YEAR from date) = 2020
      GROUP BY store_name, city, vendor_name, category_name, item_description, is_test)
      UNION ALL
      (SELECT
        store_name,
        city,
        vendor_name,
        category_name,
        item_description,
        SUM(sale_dollars) AS total_sales,
        TRUE AS is_test
      FROM `bigquery-public-data.iowa_liquor_sales.sales`
      WHERE EXTRACT (YEAR FROM date) = 2021
      GROUP BY store_name, city, vendor_name, category_name, item_description, is_test)
    );
    ```

## Create the model

Create a contribution analysis model:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, run the following statement:
    
    ``` text
    CREATE OR REPLACE MODEL bqml_tutorial.iowa_liquor_sales_sum_model
      OPTIONS(
        model_type='CONTRIBUTION_ANALYSIS',
        contribution_metric = 'sum(total_sales)',
        dimension_id_cols = ['store_name', 'city', 'vendor_name', 'category_name',
          'item_description'],
        is_test_col = 'is_test',
        min_apriori_support=0.05
      ) AS
    SELECT * FROM bqml_tutorial.iowa_liquor_sales_sum_data;
    ```

The query takes approximately 60 seconds to complete, after which the model `  iowa_liquor_sales_sum_model  ` appears in the `  bqml_tutorial  ` dataset. Because the query uses a `  CREATE MODEL  ` statement to create a model, there are no query results.

## Get insights from the model

Get insights generated by the contribution analysis model by using the `  ML.GET_INSIGHTS  ` function.

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, run the following statement to select columns from the [output for a summable metric contribution analysis model](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-get-insights#output_for_summable_metric_contribution_analysis_models) :
    
    ``` text
    SELECT
      contributors,
      metric_test,
      metric_control,
      difference,
      relative_difference,
      unexpected_difference,
      relative_unexpected_difference,
      apriori_support,
      contribution
    FROM
      ML.GET_INSIGHTS(
        MODEL `bqml_tutorial.iowa_liquor_sales_sum_model`);
    ```

The first several rows of the output should look similar to the following. The values are truncated to improve readability.

<table>
<thead>
<tr class="header">
<th>contributors</th>
<th>metric_test</th>
<th>metric_control</th>
<th>difference</th>
<th>relative_difference</th>
<th>unexpected_difference</th>
<th>relative_unexpected_difference</th>
<th>apriori_support</th>
<th>contribution</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>all</td>
<td>428068179</td>
<td>396472956</td>
<td>31595222</td>
<td>0.079</td>
<td>31595222</td>
<td>0.079</td>
<td>1.0</td>
<td>31595222</td>
</tr>
<tr class="even">
<td>vendor_name=SAZERAC COMPANY INC</td>
<td>52327307</td>
<td>38864734</td>
<td>13462573</td>
<td>0.346</td>
<td>11491923</td>
<td>0.281</td>
<td>0.122</td>
<td>13462573</td>
</tr>
<tr class="odd">
<td>city=DES MOINES</td>
<td>49521322</td>
<td>41746773</td>
<td>7774549</td>
<td>0.186</td>
<td>4971158</td>
<td>0.111</td>
<td>0.115</td>
<td>7774549</td>
</tr>
<tr class="even">
<td>vendor_name=DIAGEO AMERICAS</td>
<td>84681073</td>
<td>77259259</td>
<td>7421814</td>
<td>0.096</td>
<td>1571126</td>
<td>0.018</td>
<td>0.197</td>
<td>7421814</td>
</tr>
<tr class="odd">
<td>category_name=100% AGAVE TEQUILA</td>
<td>23915100</td>
<td>17252174</td>
<td>6662926</td>
<td>0.386</td>
<td>5528662</td>
<td>0.3</td>
<td>0.055</td>
<td>6662926</td>
</tr>
</tbody>
</table>

The output is automatically sorted by contribution, or `  ABS(difference)  ` , in descending order. In the `  all  ` row, the `  difference  ` column shows there was a $31,595,222 increase in total sales from 2020 to 2021, a 7.9% increase as indicated by the `  relative_difference  ` column. In the second row, with `  vendor_name=SAZERAC COMPANY INC  ` , there was an `  unexpected_difference  ` of $11,491,923, meaning this segment of data grew 28% more than the growth rate of the data as a whole, as seen from the `  relative_unexpected_difference  ` column. For more information, see the [summable metric output columns](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-get-insights#output_for_summable_metric_contribution_analysis_models) .

## Clean up

**Caution** : Deleting a project has the following effects:

  - **Everything in the project is deleted.** If you used an existing project for the tasks in this document, when you delete it, you also delete any other work you've done in the project.
  - **Custom project IDs are lost.** When you created this project, you might have created a custom project ID that you want to use in the future. To preserve the URLs that use the project ID, such as an `  appspot.com  ` URL, delete selected resources inside the project instead of deleting the whole project.

If you plan to explore multiple architectures, tutorials, or quickstarts, reusing projects can help you avoid exceeding project quota limits.

In the Google Cloud console, go to the **Manage resources** page.

In the project list, select the project that you want to delete, and then click **Delete** .

In the dialog, type the project ID, and then click **Shut down** to delete the project.
