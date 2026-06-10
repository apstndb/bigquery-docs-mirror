---
name: documents/docs.cloud.google.com/bigquery/docs/notebooks-introduction
uri: https://docs.cloud.google.com/bigquery/docs/notebooks-introduction
title: Introduction to notebooks
description: This page provides an overview of Colab Enterprise notebooks in BigQuery, including benefits, setup steps, and management tips.
data_source: docs.cloud.google.com
---

# Introduction to notebooks

[Colab Enterprise notebooks](https://docs.cloud.google.com/colab/docs/introduction) in BigQuery let you perform end-to-end data science and machine learning workflows within a single, integrated interface. Unlike standard SQL editors, notebooks let you combine SQL queries with Python code, rich text, and visualizations to tell a comprehensive story with your data. Notebooks are ideal for the following use cases:

  - **End-to-end ML workflows** : build, evaluate, and deploy a BigQuery ML model within a single notebook interface.
  - **Data exploration** : clean and analyze large datasets using BigQuery DataFrames.
  - **Collaborative research** : share notebooks with colleagues using IAM and track version history.

Notebooks are code assets in BigQuery Studio, alongside saved queries, and are powered by Dataform. These capabilities are available only in the Google Cloud console.

## Benefits

Notebooks in BigQuery offer the following benefits:

  - **Seamless Python integration** : use the BigQuery DataFrames API without any additional setup.
  - **AI-powered development** : use [Gemini generative AI](https://docs.cloud.google.com/bigquery/docs/\(/bigquery/docs/write-sql-gemini\)) for assistive code development.
  - **Familiar editor features** : use SQL auto-completion, similar to the BigQuery SQL editor.
  - **Integrated visualizations** : use interactive [DataFrame visualizations](https://docs.cloud.google.com/bigquery/docs/create-notebooks#cells) , or libraries like [matplotlib](https://matplotlib.org/) and [seaborn](https://seaborn.pydata.org/) , to visualize data directly in your workflow.
  - **SQL-Python interoperability** : [execute SQL](https://docs.cloud.google.com/bigquery/docs/\(/bigquery/docs/create-notebooks#cells\)) in cells that reference Python variables.

## Notebook gallery

The notebook gallery is a central hub for discovering and using prebuilt notebook templates. These templates let you perform common tasks like data preparation, data analysis, and visualization. Notebook templates also help you explore BigQuery Studio features, manage workflows, and promote best practices.

You can use notebook gallery templates to streamline your entire intent-to-insights workflow across each stage of the data lifecycle—from ingestion and exploration to advanced analytics and BigQuery ML.

The notebook gallery provides templates for every skill level. The gallery includes fundamental templates for SQL, Python, Apache Spark, and DataFrames. You can also explore topics like generative AI and multimodal data analytics in BigQuery.

To get started with the notebook gallery, follow these steps:

1.  Go to the **BigQuery** page.

2.  Click **Notebooks** in the **Explorer** menu.

3.  Click the **New notebook** drop-down and select **All templates** .

For more information on using notebook gallery templates, see [Create a notebook using the notebook gallery](https://docs.cloud.google.com/bigquery/docs/create-notebooks#create-notebook-console) .

## Runtime management

BigQuery uses [Colab Enterprise runtimes](https://docs.cloud.google.com/colab/docs/create-runtime) to run notebooks.

A notebook runtime is a Compute Engine virtual machine allocated to a particular user to enable code execution in a notebook. Multiple notebooks can share the same runtime. However, each runtime belongs to only one user and can't be used by others. Notebook runtimes are created based on templates, which are typically defined by users with administrative privileges. You can change to a runtime that uses a different template type at any time.

## Notebook security

You control access to notebooks by using Identity and Access Management (IAM) roles. For more information, see [Grant access to notebooks](https://docs.cloud.google.com/bigquery/docs/create-notebooks#grant_access_to_notebooks) .

To detect vulnerabilities in Python packages that you use in your notebooks, install and use [Notebook Security Scanner](https://docs.cloud.google.com/security-command-center/docs/enable-notebook-security-scanner) ( [Preview](https://cloud.google.com/products#product-launch-stages) ).

## Supported regions

BigQuery Studio lets you save, share, and manage versions of notebooks. The following table lists the regions where BigQuery Studio is available:

Region description

Region name

Details

**Africa**

Johannesburg

`africa-south1`

**Americas**

Columbus

`us-east5`

Dallas

`us-south1`

![leaf icon](https://cloud.google.com/sustainability/region-carbon/gleaf.svg) [Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Iowa

`us-central1`

![leaf icon](https://cloud.google.com/sustainability/region-carbon/gleaf.svg) [Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Los Angeles

`us-west2`

Las Vegas

`us-west4`

Montréal

`northamerica-northeast1`

![leaf icon](https://cloud.google.com/sustainability/region-carbon/gleaf.svg) [Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

N. Virginia

`us-east4`

Oregon

`us-west1`

![leaf icon](https://cloud.google.com/sustainability/region-carbon/gleaf.svg) [Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

São Paulo

`southamerica-east1`

![leaf icon](https://cloud.google.com/sustainability/region-carbon/gleaf.svg) [Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

South Carolina

`us-east1`

**Asia Pacific**

Hong Kong

`asia-east2`

Jakarta

`asia-southeast2`

Mumbai

`asia-south1`

Seoul

`asia-northeast3`

Singapore

`asia-southeast1`

Sydney

`australia-southeast1`

Taiwan

`asia-east1`

Tokyo

`asia-northeast1`

**Europe**

Belgium

`europe-west1`

![leaf icon](https://cloud.google.com/sustainability/region-carbon/gleaf.svg) [Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Frankfurt

`europe-west3`

London

`europe-west2`

![leaf icon](https://cloud.google.com/sustainability/region-carbon/gleaf.svg) [Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Madrid

`europe-southwest1`

![leaf icon](https://cloud.google.com/sustainability/region-carbon/gleaf.svg) [Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Netherlands

`europe-west4`

![leaf icon](https://cloud.google.com/sustainability/region-carbon/gleaf.svg) [Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

Turin

`europe-west12`

Zürich

`europe-west6`

![leaf icon](https://cloud.google.com/sustainability/region-carbon/gleaf.svg) [Low CO <sub>2</sub>](https://cloud.google.com/sustainability/region-carbon#region-picker)

**Middle East**

Doha

`me-central1`

Dammam

`me-central2`

> **Note:** All code assets are stored in a default region. Updating the default region changes the region for all code assets created after that point.

## Pricing

For pricing information about BigQuery Studio notebooks, see [Notebook runtime pricing](https://cloud.google.com/bigquery/pricing#external_services) .

## Monitor slot usage

You can monitor your BigQuery Studio notebook slot usage by viewing your [Cloud Billing report](https://docs.cloud.google.com/billing/docs/reports) in the Google Cloud console. In the Cloud Billing report, apply a filter with the label **goog-bq-feature-type** with the value **BQ\_STUDIO\_NOTEBOOK** to view slot usage and costs from BigQuery Studio notebooks.

![BigQuery Studio notebook slot usage report.](https://docs.cloud.google.com/static/bigquery/images/studio-notebook-slot-usage.png)

## Troubleshooting

For more information, see [Troubleshoot Colab Enterprise](https://docs.cloud.google.com/colab/docs/troubleshooting) .

## What's next

  - Learn how to [create notebooks](https://docs.cloud.google.com/bigquery/docs/create-notebooks) .
  - Learn how to [manage notebooks](https://docs.cloud.google.com/bigquery/docs/manage-notebooks) .
