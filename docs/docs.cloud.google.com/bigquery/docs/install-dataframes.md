---
name: documents/docs.cloud.google.com/bigquery/docs/install-dataframes
uri: https://docs.cloud.google.com/bigquery/docs/install-dataframes
title: Install BigQuery DataFrames
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# Install BigQuery DataFrames

BigQuery DataFrames is an open-source package that lets you perform data analysis and machine learning (ML) tasks using familiar Python APIs. Installing this package lets you use the BigQuery engine to scale your pandas and scikit-learn workflows to process massive datasets.

## Install BigQuery DataFrames

To install the latest version of BigQuery DataFrames, run `pip install --upgrade bigframes` .

## Available libraries

BigQuery DataFrames provides three libraries:

- `bigframes.pandas` provides a [pandas API](https://dataframes.bigquery.dev/reference/api/bigframes.pandas.html) that you can use to analyze and manipulate data in BigQuery. Many workloads can be migrated from pandas to bigframes by just changing a few imports. The `bigframes.pandas` API is scalable to support processing terabytes of BigQuery data, and the API uses the BigQuery query engine to perform calculations.
- `bigframes.bigquery` provides many BigQuery SQL functions that might not have a pandas equivalent.
- `bigframes.ml` provides an API similar to the scikit-learn API for ML. The ML capabilities in BigQuery DataFrames let you preprocess data, and then train models on that data. You can also chain these actions together to create data pipelines.

## Required roles

To get the permissions that you need to complete the tasks in this document, ask your administrator to grant you the following IAM roles on your project:

- [BigQuery Job User](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.jobUser) ( `roles/bigquery.jobUser` )
- [BigQuery Read Session User](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.readSessionUser) ( `roles/bigquery.readSessionUser` )
- Use BigQuery DataFrames in a BigQuery notebook:
  - [BigQuery User](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.user) ( `roles/bigquery.user` )
  - [Notebook Runtime User](https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.notebookRuntimeUser) ( `roles/aiplatform.notebookRuntimeUser` )
  - [Code Creator](https://docs.cloud.google.com/iam/docs/roles-permissions/dataform#dataform.codeCreator) ( `roles/dataform.codeCreator` )

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

When you're performing end user authentication in an interactive environment like a notebook, Python REPL, or the command line, BigQuery DataFrames prompts for authentication, if needed. Otherwise, see [how to set up application default credentials](https://docs.cloud.google.com/docs/authentication/provide-credentials-adc) for various environments.

## Configure installation options

After you install BigQuery DataFrames, you can specify the following options.

### Location and project

You need to specify the [location](https://dataframes.bigquery.dev/reference/api/bigframes._config.BigQueryOptions.location.html#bigframes._config.BigQueryOptions.location) and [project](https://dataframes.bigquery.dev/reference/api/bigframes._config.BigQueryOptions.project.html) in which you want to use BigQuery DataFrames.

You can define the location and project in your notebook in the following way:

```
import bigframes.pandas as bpd

PROJECT_ID = "bigframes-dev"  # @param {type:"string"}
REGION = "US"  # @param {type:"string"}

# Set BigQuery DataFrames options
# Note: The project option is not required in all environments.
# On BigQuery Studio, the project ID is automatically detected.
bpd.options.bigquery.project = PROJECT_ID

# Note: The location option is not required.
# It defaults to the location of the first table or query
# passed to read_gbq(). For APIs where a location can't be
# auto-detected, the location defaults to the "US" location.
bpd.options.bigquery.location = REGION
```

### Data processing location

BigQuery DataFrames is designed for scale, which it achieves by keeping data and processing on the BigQuery service. However, you can bring data into the memory of your client machine by calling `.to_pandas()` on a DataFrame or `Series` object. If you choose to do this, the memory limitation of your client machine applies.

## Migrate to BigQuery DataFrames version 2.0

Version 2.0 of BigQuery DataFrames makes security and performance improvements to the BigQuery DataFrames API, adds new features, and introduces breaking changes. The following sections describe the changes and provide migration guidance. You can apply these recommendations before installing the 2.0 version by using the latest version 1.x of BigQuery DataFrames.

### Install BigQuery DataFrames version 2.0

To avoid breaking changes, pin to a specific version of BigQuery DataFrames in your `requirements.txt` file (for example, `bigframes==1.42.0` ) or your `pyproject.toml` file (for example, `dependencies = ["bigframes = 1.42.0"]` ). When you're ready to try the latest version, you can run `pip install --upgrade bigframes` to install the latest version of BigQuery DataFrames.

### Use the `allow_large_results` option

BigQuery has a [maximum response size limit](https://docs.cloud.google.com/bigquery/quotas#query_jobs) for query jobs. Starting in BigQuery DataFrames version 2.0, BigQuery DataFrames enforces this limit by default in methods that return results to the client, such as `peek()` , `to_pandas()` , and `to_pandas_batches()` . If your job returns large results, you can set `allow_large_results` to `True` in your `BigQueryOptions` object to avoid breaking changes. This option is set to `False` by default in BigQuery DataFrames version 2.0.

```
import bigframes.pandas as bpd

bpd.options.bigquery.allow_large_results = True
```

You can override this option by using the `allow_large_results` parameter in `to_pandas()` and other methods:

```
bf_df = bpd.read_gbq(query)
# ... other operations on bf_df ...
pandas_df = bf_df.to_pandas(allow_large_results=True)
```

### Use the `@remote_function` decorator

BigQuery DataFrames version 2.0 makes some changes to the default behavior of the `@remote_function` decorator.

#### Keyword arguments are enforced for ambiguous parameters

To prevent passing values to an unintended parameter, BigQuery DataFrames version 2.0 and beyond enforces the use of keyword arguments for the following parameters:

- `bigquery_connection`
- `reuse`
- `name`
- `packages`
- `cloud_function_service_account`
- `cloud_function_kms_key_name`
- `cloud_function_docker_repository`
- `max_batching_rows`
- `cloud_function_timeout`
- `cloud_function_max_instances`
- `cloud_function_vpc_connector`
- `cloud_function_memory_mib`
- `cloud_function_ingress_settings`

When you use these parameters, supply the parameter name:

```
@remote_function(
  name="my_remote_function",
  ...
)
def my_remote_function(parameter: int) -> str:
  return str(parameter)
```

#### Set a service account

Starting in version 2.0, BigQuery DataFrames doesn't use the Compute Engine service account by default for the Cloud Run functions it deploys. To limit the permissions of the function that you deploy, do the following:

1.  [Create a service account](https://docs.cloud.google.com/iam/docs/service-accounts-create) with minimal permissions.
2.  Supply the service account email to the `cloud_function_service_account` parameter of the `@remote_function` decorator.

For example:

```
@remote_function(
  cloud_function_service_account="my-service-account@my-project.iam.gserviceaccount.com",
  ...
)
def my_remote_function(parameter: int) -> str:
  return str(parameter)
```

To use the Compute Engine service account, you can set the `cloud_function_service_account` parameter of the `@remote_function` decorator to `"default"` . Only use this option if you have a specific reason to use the Compute Engine service account. For example:

```
@remote_function(cloud_function_service_account="default", ...)
def my_remote_function(parameter: int) -> str:
  return str(parameter)
```

#### Set ingress settings

Starting in version 2.0, BigQuery DataFrames sets the [ingress settings of the Cloud Run functions](https://docs.cloud.google.com/functions/docs/networking/network-settings#ingress_settings) it deploys to `"internal-only"` . Previously, the ingress settings were set to `"all"` by default. You can change the ingress settings by setting the `cloud_function_ingress_settings` parameter of the `@remote_function` decorator:

```
@remote_function(cloud_function_ingress_settings="internal-and-gclb", ...)
def my_remote_function(parameter: int) -> str:
  return str(parameter)
```

### Use custom endpoints

In BigQuery DataFrames versions earlier than 2.0, if a region didn't support [regional service endpoints](https://docs.cloud.google.com/vpc/docs/regional-service-endpoints#bigquery) and `bigframes.pandas.options.bigquery.use_regional_endpoints = True` , then BigQuery DataFrames would fall back to [locational endpoints](https://docs.cloud.google.com/storage/docs/locational-endpoints) . Version 2.0 of BigQuery DataFrames removes this fallback behavior. To connect to locational endpoints in version 2.0, set the `bigframes.pandas.options.bigquery.client_endpoints_override` option:

```
import bigframes.pandas as bpd

bpd.options.bigquery.client_endpoints_override = {
  "bqclient": "https://LOCATION-bigquery.googleapis.com",
  "bqconnectionclient": "LOCATION-bigqueryconnection.googleapis.com",
  "bqstoragereadclient": "LOCATION-bigquerystorage.googleapis.com",
}
```

Replace ` LOCATION ` with the name of the BigQuery location that you want to connect to.

### Use the `bigframes.ml.llm` module

To avoid breakages if the default model changes in the future, supply a supported `model_name` directly, such as `"gemini-3.5-flash"` :

```
import bigframes.ml.llm

model = bigframes.ml.llm.GeminiTextGenerator(model_name="gemini-3.5-flash")
```

## What's next

- Learn about [manipulating data](https://docs.cloud.google.com/bigquery/docs/dataframes-data-manipulation) with BigQuery DataFrames.
- Learn how to [generate BigQuery DataFrames code with Gemini](https://docs.cloud.google.com/bigquery/docs/write-sql-gemini#dataframe) .
- Learn how to [analyze package downloads from PyPI with BigQuery DataFrames](https://github.com/googleapis/python-bigquery-dataframes/blob/main/notebooks/dataframes/pypi.ipynb) .
- View BigQuery DataFrames [source code](https://github.com/googleapis/python-bigquery-dataframes) , [sample notebooks](https://github.com/googleapis/python-bigquery-dataframes/tree/main/notebooks) , and [samples](https://github.com/googleapis/python-bigquery-dataframes/tree/main/samples/snippets) on GitHub.
- Explore the [BigQuery DataFrames API reference](https://dataframes.bigquery.dev/reference/index.html) .
