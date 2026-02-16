# Use the Data Engineering Agent to build and modify data pipelines

**Preview**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

**Note:** To provide feedback or to ask questions about this preview feature, contact <bigquery-dea-feedback@google.com>

The Data Engineering Agent lets you use Gemini in BigQuery to build, modify, and manage data pipelines to load and process data in BigQuery. With the Data Engineering Agent, you can use natural language prompts to generate data pipelines from various data sources or adapt existing data pipelines to suit your data engineering needs. The Data Engineering Agent has the following features:

  - Natural language for pipeline creation: The agent uses Gemini to understand your data and interpret your plain-language instructions. You can use plain-language instructions to have the Data Engineering Agent build or edit data pipelines.

  - Dataform integration: The agent generates and organizes the necessary pipeline code into SQLX files within a Dataform repository. The agent operates in the Dataform workspace, so Dataform pipelines are automatically available to the agent.

  - Custom agent instructions: Create agent instructions in plain-language to define custom rules for the Data Engineering Agent. Agent instructions are persistent across your organization, and can be useful to enforce organization-wide rules, such as naming conventions or style guides.

  - Pipeline validation: The agent validates any generated code to ensure that the data pipelines are functional.

You can use natural language prompts with the Data Engineering Agent to create tables, views, assertions, declarations and operations SQLX files. For example, you can use the Data Engineering Agent to do the following:

  - Load data from external data sources such as Cloud Storage in various formats, like CSV, AVRO, or PARQUET.
  - Create or use existing BigQuery routines (UDFs) to perform custom analysis and transformations on your data.
  - Define reusable guidelines for the agent in natural language.

For more examples of prompts you can use with the Data Engineering Agent, see [Sample prompts](#sample_prompts) .

## Limitations

The Data Engineering Agent has the following limitations:

  - The Data Engineering Agent is a pre-GA offering and isn't intended for production use.
  - The Data Engineering Agent doesn't support natural-language commands for the following file types:
      - Notebooks
      - Data preparation
      - Javascript within any SQLx
  - The Data Engineering Agent cannot execute pipelines. Users need to review and run or schedule pipelines.
  - The Data Engineering Agent cannot validate SQL that's dependent on non-existent intermediary resources without full pipeline invocation (user-triggered).
  - The Data Engineering Agent cannot search any web-links or URLs provided through instructions or direct prompts.
  - When importing files in an [agent instruction file](#create_agent_instructions_for_the_data_engineering_agent) , the `  @  ` import syntax only supports paths that begin with `  ./  ` , `  /  ` , or a letter.
  - The [data preview](#review_a_data_pipeline) feature is only supported for tables, declarations, or queries with the `  hasOutput  ` flag set to `  true  ` .

## Supported regions

Gemini in BigQuery is served from the following regions:

### Americas

  - Iowa ( `  us-central1  ` )

### Europe

  - Finland ( `  europe-north1  ` )
  - Frankfurt ( `  europe-west3  ` )

### Change processing region

You can change the processing region for the Data Engineering Agent using one of the following options:

### BigQuery pipelines

If you are using BigQuery pipelines, you can update your processing region by setting the default region for your code assets. For more information, see [Set the default region for code assets](/bigquery/docs/create-pipelines#set_the_default_region_for_code_assets) .

If the default region is not set, then the Data Engineering Agent processes your data globally.

### Dataform

If you are using Dataform, you can update your processing region by changing the `  defaultLocation  ` value in your Dataform workflow settings file, or `  workflow_settings.yaml  ` . For more information, see [Configure Dataform workflow settings](/dataform/docs/manage-repository#configure-workflow-settings) .

If the `  defaultLocation  ` value is not set, then the Data Engineering Agent processes your data globally.

## How the Data Engineering Agent uses your data

To produce higher quality agent responses, the Data Engineering Agent can retrieve additional data and metadata from BigQuery and Dataplex Universal Catalog, including sample rows from BigQuery tables and data scan profiles generated in Dataplex Universal Catalog. This data is not used to train the data engineering agent, and is only used during agent conversations as additional context to inform the agent's responses.

## Before you begin

Ensure that Gemini in BigQuery is enabled for your Google Cloud project. For more information, see [Set up Gemini in BigQuery](/bigquery/docs/gemini-set-up) .

You must also enable the Gemini Data Analytics API.

**Roles required to enable APIs**

To enable APIs, you need the Service Usage Admin IAM role ( `  roles/serviceusage.serviceUsageAdmin  ` ), which contains the `  serviceusage.services.enable  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .

### Required roles

To get the permissions that you need to use the Data Engineering Agent, ask your administrator to grant you the following IAM roles on the project:

  - [Dataform Code Editor](/iam/docs/roles-permissions/dataform#dataform.codeEditor) ( `  roles/dataform.codeEditor  ` )
  - [BigQuery Job User](/iam/docs/roles-permissions/bigquery#bigquery.jobuser) ( `  roles/bigquery.jobuser  ` )

For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

## Generate a data pipeline with the Data Engineering Agent

To use the Data Engineering Agent in BigQuery, select one of the following options:

### BigQuery pipelines

You can use the Data Engineering Agent in the BigQuery pipelines interface by doing the following:

1.  Go to the **BigQuery** page.

2.  In the query editor, click arrow\_drop\_down **Create new** \> **Pipeline** .

3.  Select an option for execution credentials and click **Get started** . These credentials aren't used by the agent, but are required for you to execute the generated data pipeline.

4.  Click **Try out the agent experience for data pipeline** .

5.  In the **Ask agent** field, enter a natural language prompt to generate a data pipeline. For example:
    
    ``` text
      Create dimension tables for a taxi trips star schema from
      new_york_taxi_trips.tlc_green_trips_2022. Generate surrogate keys and all
      the descriptive attributes.
    ```
    
    Once you have entered a prompt, click **Send** .

6.  The Data Engineering Agent generates a data pipeline based on your prompt.

The data pipeline generated by the Data Engineering Agent is a proposed draft of a data pipeline. You can click a pipeline node to review the generated SQLX query. To apply the agent-suggested data pipeline, click **Apply** .

### Dataform

You can use the Data Engineering Agent in Dataform by doing the following:

1.  Go to the **Dataform** page.

2.  Select a repository.

3.  Select or create a development workspace.

4.  In the workspace, click **Ask Agent** .

5.  In the **Ask agent** prompt that appears, enter a natural language prompt to generate a data pipeline. For example:
    
    ``` text
      Create dimension tables for a taxi trips star schema from
      new_york_taxi_trips.tlc_green_trips_2022. Generate surrogate keys and all
      the descriptive attributes.
    ```
    
    Once you have entered a prompt, click **Send** .

Once your prompt is sent, the Data Engineering Agent generates a data pipeline and modifies Dataform SQLX files based on your prompt. The agent applies these changes directly to your workspace files.

## Review a data pipeline

In a data pipeline generated by the Data Engineering Agent, you can click a pipeline node to review it.

  - The **Configuration** tab shows the generated SQLX query associated with the node.
  - The **Data preview** tab shows you the input and output table of the file. You can see a preview of your data transformation through this node by clicking **Run task** to run the task with or without dependencies.

## Edit a data pipeline

You can edit your data pipeline using the Data Engineering Agent by clicking **Ask agent** and entering a prompt that suggests a change to the data pipeline.

Review the changes proposed by the Data Engineering Agent, then click **Apply** to apply the changes.

You can also edit a SQLX query manually by selecting a pipeline node and then clicking **Open** .

## Create agent instructions for the Data Engineering Agent

Agent instructions are natural-language instructions for the data engineering agent that let you store persistent instructions so that the agent follows a set of custom, predefined rules. Use agent instructions if you want the results of your agent to be consistent across your organization, for example with naming conventions or to enforce a style guide.

You can create a [`  GEMINI.MD  ` context file](/gemini/docs/codeassist/use-agentic-chat-pair-programmer#create-context-file) as an agent instruction file for the Data Engineering Agent. You can create agent instruction files to use in your local workspace, or you can use the same instruction files across multiple data pipelines using an external repository.

Create agent instructions by doing the following:

1.  Under **Ask agent** , click **Pipeline instructions** .

2.  In the **Instructions for pipeline pane** , click **Create instructions file** .

3.  In the `  GEMINI.MD  ` file that appears, enter your instructions in natural language.
    
    The following example shows an agent instruction file with several rules:
    
    ``` text
      1. All event-specific tables MUST be prefixed with `cs_event_`.
      2. The primary key for any player activity table is a composite key of `player_id` and `event_timestamp_micros`.
      3. Filter out any player actions where `mana_spent` is greater than `max_mana_pool`. This is considered a data anomaly.
    ```

4.  Click **Save** .

For information on how best to structure your agent instruction files, see [Best practices with agent instruction files](#best_practices_with_agent_instruction_files) .

### Load agent instructions from an external repository

You can specify a set of agent instructions to be reused across multiple data pipelines by linking an external repository:

1.  Under **Ask agent** , click **Pipeline instructions** .
2.  Under **External repository** , select **Use instructions from external repository**
3.  In the fields provided, specify a repository that contains agent instructions that you want to use with your data pipeline.
4.  Click **Save** .

### Import additional local files as agent instructions

You can also import other instruction files for the Data Engineering Agent into the `  GEMINI.md  ` file using `  @file.md  ` syntax. For more information, see [Memory Import Processor](https://github.com/google-gemini/gemini-cli/blob/main/docs/core/memport.md) .

## Troubleshoot data pipeline errors

If you encounter any errors during data pipeline generation, verify that you have done all the prerequisites required to run the Data Engineering Agent. For more information, see [Before you begin](#before_you_begin) .

If the generated data pipeline encounters any errors, you can prompt the data engineering agent to diagnose any data pipeline failures and propose troubleshooting recommendations with the following steps:

1.  In your pipeline or your development workspace, click the **Executions** tab.

2.  From the executions list, find the failed data pipeline run. You can identify failed runs in the **Status** column of the execution run.

3.  Hover over the icon, then click **Investigate** . The Data Engineering Agent runs an analysis on your data pipeline execution for any errors.

4.  Once the analysis is complete, the Data Engineering Agent generates a report in the **Observations and Hypothesis** section. This report includes:
    
      - Observations and data points extracted from the data pipeline execution logs
      - Probably causes for the failure
      - A set of actionable steps or recommendations to resolve the identified issue

With the troubleshooting report by the Data Engineering Agent, you can implement the recommendations manually. You can also instruct the Data Engineering Agent to apply the fix for you with the following steps:

1.  Copy the suggestions in the troubleshooting report.
2.  Return to the Data Engineering Agent:
    1.  If you are using BigQuery pipelines, go to your pipelines page and then click **Ask agent** .
    2.  If you are using Dataform, click **Ask agent** .
3.  Paste the suggestions into the prompt, and instruct the data engineering agent to make the fixes directly to your data pipeline.
4.  Click **Send** .

## Sample prompts

The following sections show you some sample prompts that you can use with the Data Engineering Agent to develop your data pipeline.

### Aggregate existing data into a new table

With this prompt, the Data Engineering Agent uses the schema and samples to infer data grouping by key. The agent typically sets up a new table configuration with table and column descriptions.

``` text
  Create a daily sales report from the
  bigquery-public-data.thelook_ecommerce.order_items table into a
  reporting.daily_sales_aggregation table.
```

### Add data quality checks to an existing table

With this prompt, the agent infers reasonable quality checks for the table based on the schema and samples. You could also add some opinionated assertions as part of the prompt.

``` text
  Add data quality checks for bigquery-public-data.thelook_ecommerce.users.
```

### Create a new derived column and add data quality checks to the new table

This following prompt shows how you can add a table and a column, and specify quality checks to the table at the same time.

``` text
  Create a new table named staging.products from
  bigquery-public-data.thelook_ecommerce.products and add a calculated column
  named gross_profit, which is the retail_price minus the cost.


  Also, add the following assertions: ID must not be null and must be unique.
  The retail_price must be greater than or equal to the cost. The department
  column can only contain 'Men' or 'Women'.
```

### Create UDFs as part of the model definition

The Data Engineering Agent can also set up the DDL to create user-defined functions (UDFs). While the agent won't actually create the UDF, you can create the UDF by running the data pipeline. These UDFs can be used in model definitions in your data pipeline.

``` text
  Create a user-defined function (UDF) named get_age_group that takes an integer
  age as input and returns a string representing the age group ('Gen Z',
  'Millennial', 'Gen X', 'Baby Boomer').


  Use this UDF on the age column from the
  bigquery-public-data.thelook_ecommerce.users table to create a new view called
  reporting.user_age_demographics that includes user_id, age, and the calculated
  age_group.
```

## Best practices

The following sections suggest best practices for working with the Data Engineering Agent and Dataform.

### Best practices with the Data Engineering Agent

**Utilize agent instructions for common requests.** If there are techniques you find yourself commonly applying, or if you frequently make the same corrections to the agent, use the agent instructions as a centralized location to store common instructions and requests.

**Give the agent more context.** You can give the agent additional context from Dataplex Universal Catalog by attaching glossary terms to BigQuery tables and columns and generating data profile scans. Glossary terms can be used to tag columns that require additional context, such as columns containing personally-identifiable information (PII) that require special-handling instructions, or to identify matching columns with different naming across tables. Data profile scans provide the agent a better understanding of data distribution within columns of a table and can help the agent create more specified data quality assertions. For more information, see [About data profiling](/dataplex/docs/data-profiling-overview) .

**Write with clarity.** State your request clearly and avoid being vague. Where possible, provide source and destination data sources when prompting, as seen in the following example:

``` text
  Extract data from the sales.customers table in the us_west_1 region, and load
  it into the reporting.dim_customers table in BigQuery. Match the schema of the
  destination table.
```

**Provide direct and scoped requests.** Ask one question at a time, and keep prompts concise. For prompts with more than one question, you can itemize each distinct part of the question to improve clarity, as seen in the following example:

``` text
  1. Create a new table named staging.events_cleaned. Use raw.events as the
     source. This new table should filter out any records where the user_agent
     matches the pattern '%bot%'. All original columns should be included.

  2. Next, create a table named analytics.user_sessions. Use
     staging.events_cleaned as the source. This table should calculate the
     duration for each session by grouping by session_id and finding the
     difference between the MAX(event_timestamp) and MIN(event_timestamp).
```

**Give explicit instructions and emphasize key terms.** You can add emphasis to key terms or concepts in your prompts and label certain requirements as important, as seen in the following example:

``` text
  When creating the staging.customers table, it is *VERY IMPORTANT* that you
  transform the email column from the source table bronze.raw_customers.
  Coalesce any NULL values in the email column to an empty string ''.
```

**Specify the order of operations.** For ordered tasks, you can structure your prompt in lists, where listed items are divided into small, focused steps, as seen in the following example:

``` text
  Create a pipeline with the following steps:
  1. Extract data from the ecomm.orders table.
  2. Join the extracted data with the marts.customers table on customer_id
  3. Load the final result into the reporting.customer_orders table.
```

**Refine and iterate.** Keep trying different phrases and approaches to see what yields the best results. If the agent generates invalid SQL or other mistakes, guide the agent using examples or public documentation.

``` text
  The previous query was incorrect because it removed the timestamp. Please
  correct the SQL. Use the TIMESTAMP_TRUNC function to truncate the
  event_timestamp to the nearest hour, instead of casting it as a DATE. For
  example: TIMESTAMP_TRUNC(event_timestamp, HOUR).
```

### Best practices with agent instruction files

[Create agent instruction files](#create_agent_instructions_for_the_data_engineering_agent) to customize the Data Engineering Agent to suit your needs. When using agent instructions, we recommend that you do the following:

  - All file paths in Dataform are relative to the root of the repository. Use relative paths for any `  @file.md  ` syntax to properly import instructions to `  GEMINI.md  ` .
  - Files imported in `  GEMINI.md  ` can themselves contain imports, which can create a nested structure. To prevent infinite recursion, `  GEMINI.md  ` has a maximum import depth of five levels.
  - To share instructions across data pipelines, store instructions in a central Dataform repository and link them to the working Dataform repository. You can use local instructions to override central rules for pipeline-specific behavior.
  - Use headings and lists in the agent instruction file can help organize and clarify instructions for the Data Engineering Agent.
  - Give meaningful filenames and group similar instructions together in a file. Organize rules logically by category, feature, or functionality using Markdown headings.
  - To avoid conflicting instructions, clearly define the specific conditions under which each instruction applies.
  - Iterate and refine your prompts and workflow. Agent behavior changes over time with agent rollouts and model upgrades, so we recommend iterating on your rules with different prompts to identify areas that might need improvement. Keep your rules file in sync with any changes to your data pipeline.

The following example shows an agent instruction file named `  GEMINI.md  ` that utilizes our best practices for effective use of the Data Engineering Agent:

``` text
  ### Naming Conventions

  * Datasets: [business_domain]_[use_case] (e.g., ecommerce_sales)

  * Tables:
      - Raw/External: raw_[source_name]
      - Staging: stg_[business_entity]
      - Dimension: dim_[dimension_name]
      - Fact: fct_[fact_name]

  * Dataform Folders:
      - sources
      - staging
      - marts
      - dataProducts

  * Views: vw_[view_name]

  * Columns: snake_case (e.g., order_id, customer_name)

  ## Cloud Storage data load
  * When ingesting data from Cloud Storage, create external tables.

  ## Null handling
  * Filter out null id values

  ## String normalization
  * Standardize string columns by converting to lower case

  ## Data Cleaning Guidelines
  @./generic_cleaning.md
```
