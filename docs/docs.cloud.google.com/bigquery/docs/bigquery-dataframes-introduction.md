---
name: documents/docs.cloud.google.com/bigquery/docs/bigquery-dataframes-introduction
uri: https://docs.cloud.google.com/bigquery/docs/bigquery-dataframes-introduction
title: Introduction to BigQuery DataFrames
description: BigQuery DataFrames lets you use BigQuery to process terabytes of data and train machine learning models with Python, pandas, and scikit-learn APIs.
data_source: docs.cloud.google.com
---

# Introduction to BigQuery DataFrames

BigQuery DataFrames is an open source Python library that lets you take advantage of BigQuery data processing by using familiar Python APIs. BigQuery DataFrames provides a Pythonic DataFrame powered by the BigQuery engine, and it implements the pandas and scikit-learn APIs by pushing data processing down to BigQuery through SQL conversion. This lets you use BigQuery to explore and process terabytes of data, build data pipelines, and train machine learning (ML) models, all with Python APIs, and without moving data to your client machine.

If you are familiar with pandas, you can use BigQuery DataFrames to work with BigQuery data with minimal changes to your code. For example, you can use familiar pandas methods to analyze data from a BigQuery table:

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

> **Note:** There are breaking changes to some default parameters in BigQuery DataFrames version 2.0. To learn about these changes and how to migrate to version 2.0, see [Migrate to BigQuery DataFrames 2.0](https://docs.cloud.google.com/bigquery/docs/migrate-dataframes) .

## BigQuery DataFrames benefits

BigQuery DataFrames does the following:

  - Offers more than 750 pandas and scikit-learn APIs implemented through SQL conversion to BigQuery and BigQuery ML APIs.
  - Defers the execution of queries for enhanced performance.
  - Extends data transformations with user-defined Python functions to let you process data in Google Cloud. These functions are automatically deployed as BigQuery [remote functions](https://docs.cloud.google.com/bigquery/docs/remote-functions) .
  - Integrates with Gemini Enterprise Agent Platform to let you use Gemini models for text generation.

## Licensing

BigQuery DataFrames is distributed with the [Apache-2.0 license](https://github.com/googleapis/python-bigquery-dataframes/blob/main/LICENSE) .

BigQuery DataFrames also contains code derived from the following third-party packages:

  - [Ibis](https://ibis-project.org/)
  - [pandas](https://pandas.pydata.org/)
  - [Python](https://www.python.org/)
  - [scikit-learn](https://scikit-learn.org/)
  - [XGBoost](https://xgboost.readthedocs.io/en/stable/)

For details, see the [`third_party/bigframes_vendored`](https://github.com/googleapis/python-bigquery-dataframes/tree/main/third_party/bigframes_vendored) directory in the BigQuery DataFrames GitHub repository.

## Quotas and limits

  - [BigQuery quotas](https://docs.cloud.google.com/bigquery/quotas) apply to BigQuery DataFrames, including hardware, software, and network components.
  - A subset of pandas and scikit-learn APIs are supported. For more information, see [Supported pandas APIs](https://dataframes.bigquery.dev/supported_pandas_apis.html) .
  - You must explicitly clean up any automatically created Cloud Run functions functions as part of session cleanup. For more information, see [Supported pandas APIs](https://dataframes.bigquery.dev/supported_pandas_apis.html) .

## Pricing

  - BigQuery DataFrames is a set of open source Python libraries available for download at no extra cost.
  - BigQuery DataFrames uses BigQuery, Cloud Run functions, Agent Platform, and other Google Cloud services, which incur their own costs.
  - During regular usage, BigQuery DataFrames stores temporary data, such as intermediate results, in BigQuery tables. These tables persist for seven days by default, and you are charged for the data stored in them. The tables are created in the `_anonymous_` dataset in the Google Cloud project you specify in the [`bf.options.bigquery.project` option](https://dataframes.bigquery.dev/reference/api/bigframes._config.BigQueryOptions.html) .

## Use cases

You can use BigQuery DataFrames for the following analytics and machine learning use cases:

  - [Machine learning and AI](https://docs.cloud.google.com/bigquery/docs/dataframes-ml-ai)
  - [Customize Python functions](https://docs.cloud.google.com/bigquery/docs/dataframes-custom-python-functions)
  - [Visualize graphs using BigQuery DataFrames](https://docs.cloud.google.com/bigquery/docs/dataframes-visualizations)
  - [Use BigQuery DataFrames in dbt](https://docs.cloud.google.com/bigquery/docs/dataframes-dbt)
  - [Use the BigQuery JupyterLab plugin](https://docs.cloud.google.com/bigquery/docs/jupyterlab-plugin)

## Code samples and reference documentation

Explore code samples, notebooks, and reference documentation for BigQuery DataFrames:

  - [BigQuery DataFrames sample notebooks on GitHub](https://github.com/google/bigframes/tree/main/notebooks)
  - [BigQuery DataFrames API reference](https://dataframes.bigquery.dev/reference/index.html) (including [`bigframes.pandas`](https://dataframes.bigquery.dev/reference/api/bigframes.pandas.html) and [`bigframes.bigquery.ai`](https://dataframes.bigquery.dev/reference/api/bigframes.bigquery.ai.html) )
  - [BigQuery DataFrames Cloud client library reference](https://docs.cloud.google.com/python/docs/reference/bigframes/latest)
  - [BigQuery Python libraries overview](https://docs.cloud.google.com/bigquery/docs/python-libraries)
  - [BigQuery DataFrames source code repository on GitHub](https://github.com/google/bigframes) and [package on PyPI](https://pypi.org/project/bigframes/)

## What's next

  - Try the [BigQuery DataFrames quickstart](https://docs.cloud.google.com/bigquery/docs/dataframes-quickstart) .
  - [Install and configure BigQuery DataFrames](https://docs.cloud.google.com/bigquery/docs/install-dataframes) .
  - Learn how to [manipulate data](https://docs.cloud.google.com/bigquery/docs/dataframes-data-manipulation) and [work with the data type system](https://docs.cloud.google.com/bigquery/docs/dataframes-data-types) .
  - Learn how to [manage sessions and I/O](https://docs.cloud.google.com/bigquery/docs/dataframes-sessions-io) .
  - Learn how to [optimize performance](https://docs.cloud.google.com/bigquery/docs/dataframes-performance) .
