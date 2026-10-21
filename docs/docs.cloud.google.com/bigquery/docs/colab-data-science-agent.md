---
name: documents/docs.cloud.google.com/bigquery/docs/colab-data-science-agent
uri: https://docs.cloud.google.com/bigquery/docs/colab-data-science-agent
title: Use the Colab Enterprise Data Science Agent with BigQuery
description: Overview of Colab Enterprise Data Science Agent in BigQuery.
data_source: docs.cloud.google.com
---

# Use the Colab Enterprise Data Science Agent with BigQuery

The Data Science Agent (DSA) for Colab Enterprise and BigQuery lets you automate exploratory data analysis, perform machine learning tasks, and deliver insights all within a Colab Enterprise notebook.

## Before you begin

1.  Enable the BigQuery, Gemini for Google Cloud, Dataform, and Compute Engine APIs, if any are not already enabled.

    **Roles required to enable APIs**

    To enable APIs, you need the `serviceusage.services.enable` permission. If you created the project, then you likely already have this permission through the Owner role ( `roles/owner` ). Otherwise, you can get this permission through the Service Usage Admin role ( `roles/serviceusage.serviceUsageAdmin` ). [Learn how to grant roles](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

    For new projects, the BigQuery API is automatically enabled.

If you're new to Colab Enterprise in BigQuery, see the setup steps on the [Create notebooks](https://docs.cloud.google.com/bigquery/docs/create-notebooks#required_permissions) page.

## Limitations

- The DSA is only available within the Colab Enterprise environment.
- The DSA supports the following data sources:
  - CSV files
  - BigQuery tables
- The code produced by the DSA only runs in your notebook's runtime.
- Searching for BigQuery tables using the `@mention` function is limited to your current project. Use the table selector to search across projects.
- The `@mention` function only searches for BigQuery tables. To search for data files that you can upload, use the `+` symbol.
- PySpark in the DSA only generates Managed Service for Apache Spark 4.0 code. The DSA can help you upgrade to Managed Service for Apache Spark 4.0. If you require earlier versions, [write and run PySpark code directly in your notebook](https://docs.cloud.google.com/bigquery/docs/use-spark) instead.
- [Customer-managed encryption keys (CMEK)](https://docs.cloud.google.com/kms/docs/cmek) aren't supported.

## Use the Data Science Agent in BigQuery

The following steps show you how to use the DSA in BigQuery.

1.  Create or open a Colab Enterprise notebook.

2.  Optional: Reference your data in one of the following ways:

    - Upload a CSV file or use the `+` symbol in your prompt to search for available files.
    - Choose one or more BigQuery tables in the table selector from your current project or from other projects you have access to.
    - Reference a BigQuery table name in your prompt in this format: `project_id `` : `` dataset `` . `` table` .
    - Type the `@` symbol to search for a BigQuery table name using the `@mention` function.

3.  Enter a [prompt](https://docs.cloud.google.com/bigquery/docs/colab-data-science-agent#sample-prompts) that describes the data analysis you want to perform or the prototype you want to build. The default behavior is to generate Python code using open source libraries such as sklearn to accomplish complex machine learning tasks. To use a specific tool, include the following keywords in your prompt:

    - If you want to use BigQuery ML, include the "SQL" keyword.
    - If you want to use "BigQuery DataFrames", specify the "BigFrames" or "BigQuery DataFrames" keywords.
    - If you want to use PySpark, include the "Apache Spark" or "PySpark" keywords.

4.  Choose your model. The default model is Gemini 3.0 Flash.

5.  Send your prompt, and examine the results.

### Analyze a CSV file

To analyze a CSV using the DSA in BigQuery, follow these steps.

1.  Go to the **BigQuery** page.

2.  In the left pane, expand your project, and then click **Notebooks** .

3.  Click **New notebook \> Empty notebook** .

    Alternatively, in the tab bar, click the arrow_drop_down drop-down arrow next to the add_box **Add** icon, and then click **Notebook \> Empty notebook** .

4.  Click the spark **Toggle Gemini in Colab** button to open the chat dialog.

    > **Note:** You can toggle between displaying the chat dialog in a separate panel and displaying the chat dialog inside your notebook by clicking the collapse_content **Move** icon.

5.  Upload your CSV file.

    1.  In the chat dialog, click add_circle_outline **Add to Gemini \> Upload** .

    2.  If necessary, authorize your Google Account.

    3.  Browse to the location of the CSV file, and then click **Open** .

6.  Alternatively, type the `+` symbol in your prompt to search for available files to upload.

7.  Enter your prompt in the chat window. For example: `Identify trends and anomalies in this file.`

8.  Choose your model. The default model is Gemini 3.0 Flash.

9.  Click send **Send** . The results appear in the chat window.

10. You can ask the agent to change the plan, or you can run it by clicking **Accept & run** . As the plan runs, generated code and text appear in the notebook. Click **Cancel** to stop.

### Analyze BigQuery tables

To analyze a BigQuery table, choose one or more tables in the table selector, provide a reference to the table in your prompt, or search for a table by using the `@` symbol.

1.  Go to the **BigQuery** page.

2.  In the left pane, expand your project, and then click **Notebooks** .

3.  Click **New notebook \> Empty notebook** .

    Alternatively, in the tab bar, click the arrow_drop_down drop-down arrow next to the add_box **Add** icon, and then click **Notebook \> Empty notebook** .

4.  Click the spark **Toggle Gemini in Colab** button to open the chat dialog.

    > **Note:** You can toggle between displaying the chat dialog in a separate panel and displaying the chat dialog inside your notebook by clicking the collapse_content **Move** icon.

5.  Enter your prompt in the chat window.

6.  Reference your data in one of the following ways:

    1.  Choose one or more tables using the table selector:

        1.  Click add_circle_outline **Add to Gemini \> BigQuery tables** .

        2.  In the **BigQuery tables** window, select one or more tables in your project. You can search for tables across projects and filter tables by using the search bar.

    2.  Include a BigQuery table name directly in your prompt. For example: "Help me perform exploratory data analysis and get insights about the data in this table: `project_id `` : `` dataset `` . `` table` ."

        Replace the following:

        - `project_id` : your project ID
        - `dataset` : the name of the dataset that contains the table you're analyzing
        - `table` : the name of the table you're analyzing

    3.  Type `@` to search for a BigQuery table in your current project.

7.  Choose your model. The default model is Gemini 3.0 Flash.

8.  Click send **Send** .

    The results appear in the chat window.

9.  You can ask the agent to change the plan, or you can run it by clicking **Accept & run** . As the plan runs, generated code and text appear in the notebook. For additional steps in the plan, you may be required to click **Accept & run** again. Click **Cancel** to stop.

## Sample prompts

Regardless of the complexity of the prompt that you use, the DSA generates a plan that you can refine to meet your needs.

The following examples show the types of prompts that you can use with the DSA.

### Python prompts

Python code is generated by default unless you use a specific keyword in the prompt such as "BigQuery ML" or "SQL".

- "Investigate and fill missing values by using the k-Nearest Neighbors (KNN) machine learning algorithm."
- "Create a plot of salary by experience level. Use the `experience_level` column to group the salaries, and create a box plot for each group showing the values from the `salary_in_usd` column."
- "Use the XGBoost algorithm to make a model for determining the `class` variable of a particular fruit. Split the data into training and testing datasets to generate a model and to determine the model's accuracy. Create a confusion matrix to show the predictions amongst each class, including all predictions that are correct and incorrect."
- "Forecast `target_variable` from `filename.csv` for the next six months."

### SQL and BigQuery ML prompts

- "Create and evaluate a classification model on `bigquery-public-data.ml_datasets.census_adult_income` using BigQuery SQL."
- "Using SQL, forecast the future traffic of my website for the next month based on `bigquery-public-data.google_analytics_sample.ga_sessions_*` . Then, plot the historical and forecasted values."
- "Group similar customers together to create targeting market campaigns using a KMeans model and BigQuery ML SQL functions. Use three features for clustering. Then visualize the results by creating a series of 2D scatter plots. Use the table `bigquery-public-data.ml_datasets.census_adult_income` ."
- "Generate text embeddings in BigQuery ML using the review content in `bigquery-public-data.imdb.reviews` ."

For a list of supported models and machine learning tasks, see the [BigQuery ML documentation](https://docs.cloud.google.com/bigquery/docs/bqml-introduction) .

### DataFrame prompts

- "Create a pandas DataFrame for the data in `project_id `` : `` dataset `` . `` table` . Analyze the data for null values, and then graph the distribution of each column using the graph type. Use violin plots for measured values and bar plots for categories."
- "Read `filename.csv` and construct a DataFrame. Run analysis on the DataFrame to determine what needs to be done with values. For example, are there missing values that need to be replaced or removed, or are there duplicate rows that need to be addressed. Use the data file to determine the distribution of the money invested in USD per city location. Graph the top 20 results using a bar graph that shows the results in descending order as Location versus Avg Amount Invested (USD)."
- "Create and evaluate a classification model on `project_id `` : `` dataset `` . `` table` using BigQuery DataFrames."
- "Create a time series forecasting model on `project_id `` : `` dataset `` . `` table` using BigQuery DataFrames, and visualize the model evaluations."
- "Visualize the sales figures in the past year in BigQuery table `project_id `` : `` dataset `` . `` table` using BigQuery DataFrames."
- "Find the features that can best predict the penguin species from the table `bigquery-public_data.ml_datasets.penguins` using BigQuery DataFrames."

### PySpark prompts

- "Create and evaluate a classification model on `project_id `` : `` dataset `` . `` table` using Managed Service for Apache Spark."
- "Group similar customers together to create targeting market campaigns, but first do dimensionality reduction using a PCA model. Use PySpark to do this on table `project_id `` : `` dataset `` . `` table` ."

## Turn off Gemini in BigQuery

To turn off Gemini in BigQuery for a Google Cloud project, an administrator must turn off the Gemini for Google Cloud API. See [Disabling services](https://docs.cloud.google.com/service-usage/docs/enable-disable#disabling) .

To turn off Gemini in BigQuery for a specific user, an administrator needs to revoke the [Gemini for Google Cloud User](https://docs.cloud.google.com/iam/docs/roles-permissions/cloudaicompanion#cloudaicompanion.user) ( `roles/cloudaicompanion.user` ) role for that user. See [Revoke a single IAM role](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access#revoke-single-role) .

> **Note:** To opt out of using the Data Science Agent without turning off other Gemini features, contact <vertex-notebooks-previews-external@google.com> , or complete the [Data Science Agent opt-out form](https://forms.gle/KuTAunuLT2YmFAcs8) . To learn more about how to turn off Data Science Agent, see [Turn off Gemini in Colab Enterprise](https://docs.cloud.google.com/colab/docs/use-data-science-agent#turn-off) .

## Pricing

Data Science Agent pricing is based on your input and output data. For more information, see Agents pricing at [How BigQuery pricing works](https://cloud.google.com/bigquery#pricing) .

## Supported regions

To view the supported regions for Colab Enterprise's Data Science Agent, see [Locations](https://docs.cloud.google.com/colab/docs/locations) .
