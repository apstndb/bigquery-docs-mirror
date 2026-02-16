# Introduction to notebooks

This document provides an introduction to [Colab Enterprise notebooks](/colab/docs/introduction) in BigQuery. You can use notebooks to complete analysis and machine learning (ML) workflows by using SQL, Python, and other common packages and APIs. Notebooks offer improved collaboration and management with the following options:

  - Share notebooks with specific users and groups by using Identity and Access Management (IAM).
  - Review the notebook version history.
  - Revert to or branch from previous versions of the notebook.

Notebooks are [BigQuery Studio](/bigquery/docs/query-overview#bigquery-studio) code assets powered by [Dataform](/dataform/docs/overview) . [Saved queries](/bigquery/docs/saved-queries-introduction) are also code assets. All code assets are stored in a default [region](#supported_regions) . Updating the default region changes the region for all code assets created after that point.

Notebook capabilities are available only in the Google Cloud console.

## Benefits

Notebooks in BigQuery offer the following benefits:

  - [BigQuery DataFrames](/python/docs/reference/bigframes/latest) is integrated into notebooks, no setup required. BigQuery DataFrames is a Python API that you can use to analyze BigQuery data at scale by using the [pandas DataFrame](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.html) and [scikit-learn](https://scikit-learn.org/stable/modules/classes.html) APIs.
  - Assistive code development powered by [Gemini generative AI](/bigquery/docs/write-sql-gemini) .
  - Auto-completion of SQL statements, the same as in the BigQuery editor.
  - The ability to save, share, and manage versions of notebooks.
  - The ability to use [matplotlib](https://matplotlib.org/) , [seaborn](https://seaborn.pydata.org/) , and other popular libraries to visualize data at any point in your workflow.
  - The ability to write and [execute SQL](/bigquery/docs/create-notebooks#cells) in a cell that can reference Python variables from your notebook.
  - Interactive [DataFrame visualization](/bigquery/docs/create-notebooks#cells) that supports aggregation and customization.

## Notebook gallery

**Preview**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

**Note:** To provide feedback or to request product enhancements, contact <bigquery-notebook-gallery@google.com> .

The notebook gallery is a central hub for discovering and using prebuilt notebook templates. These templates let you perform common tasks like data preparation, data analysis, and visualization. Notebook templates also help you explore BigQuery Studio features, manage workflows, and promote best practices.

You can use notebook gallery templates to streamline your entire intent-to-insights workflow across each stage of the data lifecycle-from ingestion and exploration to advanced analytics and BigQuery ML.

The notebook gallery provides templates for every skill level. The gallery includes fundamental templates for SQL, Python, Apache Spark, and DataFrames. You can also explore topics like generative AI and multimodal data analytics in BigQuery.

To get started with the notebook gallery, follow these steps:

1.  Go to the **BigQuery** page.

2.  From from the BigQuery Studio home page, click **View notebook gallery** .

For more information on using notebook gallery templates, see [Create a notebook using the notebook gallery](/bigquery/docs/create-notebooks#create-notebook-console) .

## Runtime management

BigQuery uses [Colab Enterprise runtimes](/colab/docs/create-runtime) to run notebooks.

A notebook runtime is a Compute Engine virtual machine allocated to a particular user to enable code execution in a notebook. Multiple notebooks can share the same runtime. However, each runtime belongs to only one user and can't be used by others. Notebook runtimes are created based on template, which are typically defined by users with administrative privileges. You can change to a runtime that uses a different template type at any time.

## Notebook security

You control access to notebooks by using Identity and Access Management (IAM) roles. For more information, see [Grant access to notebooks](/bigquery/docs/create-notebooks#grant_access_to_notebooks) .

To detect vulnerabilities in Python packages that you use in your notebooks, install and use [Notebook Security Scanner](/security-command-center/docs/enable-notebook-security-scanner) ( [Preview](https://cloud.google.com/products#product-launch-stages) ).

## Supported regions

BigQuery Studio lets you save, share, and manage versions of notebooks. The following table lists the regions where BigQuery Studio is available:

Region description

Region name

Details

**Africa**

Johannesburg

`  africa-south1  `

**Americas**

Columbus

`  us-east5  `

Dallas

`  us-south1  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Iowa

`  us-central1  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Las Vegas

`  us-west4  `

Los Angeles

`  us-west2  `

Mexico

`  northamerica-south1  `

Montréal

`  northamerica-northeast1  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

North Virginia

`  us-east4  `

Oklahoma

`  us-central2  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Oregon

`  us-west1  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Salt Lake City

`  us-west3  `

Santiago

`  southamerica-west1  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

São Paulo

`  southamerica-east1  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

South Carolina

`  us-east1  `

Toronto

`  northamerica-northeast2  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

**Asia Pacific**

Bangkok

`  asia-southeast3  `

Delhi

`  asia-south2  `

Hong Kong

`  asia-east2  `

Jakarta

`  asia-southeast2  `

Melbourne

`  australia-southeast2  `

Mumbai

`  asia-south1  `

Osaka

`  asia-northeast2  `

Seoul

`  asia-northeast3  `

Singapore

`  asia-southeast1  `

Sydney

`  australia-southeast1  `

Taiwan

`  asia-east1  `

Tokyo

`  asia-northeast1  `

**Europe**

Belgium

`  europe-west1  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Berlin

`  europe-west10  `

Finland

`  europe-north1  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Frankfurt

`  europe-west3  `

London

`  europe-west2  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Madrid

`  europe-southwest1  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Milan

`  europe-west8  `

Netherlands

`  europe-west4  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Paris

`  europe-west9  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Stockholm

`  europe-north2  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Turin

`  europe-west12  `

Warsaw

`  europe-central2  `

Zürich

`  europe-west6  `

[Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

**Middle East**

Dammam

`  me-central2  `

Doha

`  me-central1  `

Tel Aviv

`  me-west1  `

## Pricing

For pricing information about BigQuery Studio notebooks, see [Notebook runtime pricing](https://cloud.google.com/bigquery/pricing#external_services) .

## Monitor slot usage

You can monitor your BigQuery Studio notebook slot usage by viewing your [Cloud Billing report](/billing/docs/reports) in the Google Cloud console. In the Cloud Billing report, apply a filter with the label **goog-bq-feature-type** with the value **BQ\_STUDIO\_NOTEBOOK** to view slot usage and costs from BigQuery Studio notebook.

## Troubleshooting

For more information, see [Troubleshoot Colab Enterprise](/colab/docs/troubleshooting) .

## What's next

  - Learn how to [create notebooks](/bigquery/docs/create-notebooks) .
  - Learn how to [manage notebooks](/bigquery/docs/manage-notebooks) .
