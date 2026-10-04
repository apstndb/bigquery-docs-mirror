---
name: documents/docs.cloud.google.com/bigquery/docs/programmatic-analysis
uri: https://docs.cloud.google.com/bigquery/docs/programmatic-analysis
title: Notebooks and programmatic analysis tools
description: Describes multiple ways for writing and running code to analyze data managed in BigQuery.
data_source: docs.cloud.google.com
---

# Notebooks and programmatic analysis tools

While SQL is a powerful query language, programming languages like Python, Java, or R provide syntaxes and statistical functions that can be more expressive for data analysis tasks. Notebook environments offer a highly flexible alternative to spreadsheets for complex data exploration and machine learning (ML) workflows.

BigQuery provides built-in notebook integration as well as support for several other programmatic analysis solutions.

## Colab Enterprise notebooks

You can use Colab Enterprise notebooks in BigQuery to perform end-to-end data science and ML workflows in a single, integrated interface. Unlike standard SQL editors, notebooks let you combine SQL queries with Python code, rich text, and visualizations to tell a comprehensive story with your data. Colab Enterprise notebooks are ideal for the following use cases:

- **End-to-end ML workflows:** build, evaluate, and deploy BigQuery ML models within a single interface.
- **Data exploration:** clean and analyze large datasets using [BigQuery DataFrames](https://docs.cloud.google.com/bigquery/docs/bigquery-dataframes-introduction) .
- **Collaborative research:** track version history and share notebooks with colleagues using Identity and Access Management (IAM).

Colab Enterprise notebooks offer the following benefits:

- **AI-powered development:** leverage Gemini Enterprise Agent Platform for assistive code development.
- **Seamless Python integration:** use the BigQuery DataFrames API without any additional setup.
- **Familiar editor features:** benefit from SQL auto-completion similar to the BigQuery SQL editor.
- **Integrated visualizations:** use interactive DataFrame visualizations or libraries like `matplotlib` and `seaborn` directly in your workflow.
- **SQL-Python interoperability:** execute SQL in cells that reference Python variables.

### Notebook gallery

The notebook gallery is a central hub for discovering and using prebuilt notebook templates. It includes fundamental templates for SQL, Python, Apache Spark, and DataFrames to help you perform common tasks like data preparation, analysis, and visualization.

### Runtime management and security

Notebooks use Colab Enterprise runtimes, which are Compute Engine virtual machines allocated to a specific user to enable code execution. Access to notebooks is controlled using IAM roles. To detect vulnerabilities in the Python packages used in your notebooks, you can install and use the [Notebook Security Scanner](https://docs.cloud.google.com/security-command-center/docs/enable-notebook-security-scanner) .

### Monitoring and regions

All code assets in BigQuery Studio are stored in a default region, and updating this setting changes the region for any newly created code assets. Colab Enterprise notebooks are available in all regions where BigQuery Studio is available.

To monitor notebook slot usage, you can view your Cloud Billing report and apply a filter for the `goog-bq-feature-type` label with the value `BQ_STUDIO_NOTEBOOK` .

Notebook capabilities are available only in the Google Cloud console.

### Pricing

For pricing information about Colab Enterprise notebooks, see [Notebook runtime pricing](https://docs.cloud.google.com/bigquery/pricing#external_services) .

## BigQuery DataFrames

[BigQuery DataFrames](https://docs.cloud.google.com/bigquery/docs/bigquery-dataframes-introduction) is a set of open source Python libraries that let you take advantage of BigQuery data processing by using familiar Python APIs. BigQuery DataFrames implements the pandas and scikit-learn APIs by pushing the processing down to BigQuery through SQL conversion. This design lets you use BigQuery to explore and process terabytes of data and train ML models, all with Python APIs.

BigQuery DataFrames offers the following benefits:

- More than 750 pandas and scikit-learn APIs implemented through transparent SQL conversion to BigQuery and BigQuery ML APIs.
- Deferred execution of queries for enhanced performance.
- Extending data transformations with user-defined Python functions to let you process data in the cloud. These functions are automatically deployed as BigQuery [remote functions](https://docs.cloud.google.com/bigquery/docs/remote-functions) .
- Integration with Gemini Enterprise Agent Platform to let you use Gemini models for text generation.

## Other programmatic analysis solutions

In addition to Colab Enterprise and BigQuery DataFrames, BigQuery integrates with several other programmatic solutions:

- **Jupyter Notebooks and JupyterLab:** you can interact with BigQuery directly from Jupyter Notebooks using [IPython Magics for BigQuery](https://docs.cloud.google.com/python/docs/reference/bigquery/latest/magics) or [BigQuery client libraries](https://docs.cloud.google.com/bigquery/docs/reference/libraries) . You can deploy your environments on Google Cloud using [Vertex AI Workbench instances](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/introduction) or [Managed Service for Apache Spark](https://cloud.google.com/products/managed-service-for-apache-spark) .
- **Apache Zeppelin:** you can deploy web-based Apache Zeppelin notebooks for data analytics by installing the [Zeppelin optional component](https://docs.cloud.google.com/dataproc/docs/concepts/components/zeppelin) on Managed Service for Apache Spark.
- **Apache Hadoop, Spark, and Hive:** [Managed Service for Apache Spark](https://cloud.google.com/products/managed-service-for-apache-spark) integrates with open source BigQuery connectors. These connectors use the [BigQuery Storage API](https://docs.cloud.google.com/bigquery/docs/reference/storage) to stream data in parallel directly from BigQuery through gRPC.
- **Apache Beam & Dataflow:** Apache Beam is an open source framework that provides a rich set of windowing and session analysis primitives, as well as an ecosystem of connectors, including one for BigQuery. [Dataflow](https://docs.cloud.google.com/dataflow/docs/overview) is a fully managed service that lets you run these Apache Beam jobs at scale.

### Other resources

BigQuery offers several [client libraries](https://docs.cloud.google.com/bigquery/docs/reference/libraries) in languages such as Java, Go, Python, JavaScript, PHP, and Ruby. Certain data analysis frameworks like [pandas](https://pandas.pydata.org/) provide [plugins](https://pandas-gbq.readthedocs.io/en/latest/) to interact directly with BigQuery, and for those who prefer shell environments, the [bq command-line tool](https://docs.cloud.google.com/bigquery/docs/bq-command-line-tool) is available.
