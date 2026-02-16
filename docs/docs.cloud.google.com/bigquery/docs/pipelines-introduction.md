# Introduction to BigQuery pipelines

You can use BigQuery pipelines to automate and streamline your BigQuery data processes. With pipelines, you can schedule and execute code assets in sequence to improve efficiency and reduce manual effort.

## Overview

Pipelines are powered by [Dataform](/dataform/docs/overview) .

A pipeline consists of one or more of the following code assets:

  - [Notebooks](/bigquery/docs/notebooks-introduction)
  - [SQL queries](/bigquery/docs/reference/standard-sql/query-syntax)
  - [Data preparations](/bigquery/docs/data-prep-introduction)

You can use pipelines to schedule the execution of code assets. For example, you can schedule a SQL query to run daily and update a table with the most recent source data, which can then power a dashboard.

In a pipeline with multiple code assets, you define the execution sequence. For example, to train a machine learning model, you can create a workflow in which a SQL query prepares data, and then a subsequent notebook trains the model using that data.

## Capabilities

You can do the following in a pipeline:

  - [Create new or import existing](/bigquery/docs/create-pipelines#add_a_pipeline_task) SQL queries or notebooks into a pipeline.
  - [Schedule a pipeline](/bigquery/docs/schedule-pipelines) to automatically run at a specified time and frequency.
  - [Share a pipeline](/bigquery/docs/create-pipelines#share_a_pipeline) with users or groups you specify.
  - [Share a link to a pipeline](/bigquery/docs/create-pipelines#share_a_link_to_a_pipeline) .

## Limitations

Pipelines are subject to the following limitations:

  - Pipelines are available only in the Google Cloud console.
  - You can't change the region for storing a pipeline after it is created.
  - You can grant users or groups access to a selected pipeline, but you can't grant them access to individual tasks within the pipeline.
  - If a scheduled pipeline run doesn't finish before the start of the next scheduled run, the next scheduled run is skipped and marked with an error.

### Set the default region for code assets

If this is the first time you are creating a code asset, you should set the default region for code assets. You can't change the region for a code asset after it is created.

**Note:** If you create a pipeline and choose a different default region than the one you have been using for code assets—for example, choosing `  us-west1  ` when you have been using `  us-central1  ` —then that pipeline and all code assets you create afterwards use that new region by default. Existing code assets continue to use the region they were assigned when they were created.

All code assets in BigQuery Studio use the same default region. To set the default region for code assets, follow these steps:

1.  Go to the **BigQuery** page.

2.  In the **Explorer** pane, find the project in which you have enabled code assets.

3.  Click more\_vert **View actions** next to the project, and then click **Change my default code region** .

4.  For **Region** , select the region that you want to use for code assets.

5.  Click **Select** .

For a list of supported regions, see [BigQuery Studio locations](/bigquery/docs/locations#bqstudio-loc) .

## Supported regions

All code assets are stored in your [default region for code assets](/bigquery/docs/enable-assets#set_the_default_region_for_code_assets) . Updating the default region changes the region for all code assets created after that point.

The following table lists the regions where pipelines are available:

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

## Quotas and limits

BigQuery pipelines are subject to [Dataform quotas and limits](/dataform/docs/quotas) .

## Pricing

The execution of BigQuery pipeline tasks incurs compute and storage charges in BigQuery. For more information, see [BigQuery pricing](https://cloud.google.com/bigquery/pricing) .

Pipelines containing notebooks incur Colab Enterprise runtime charges based on the [default machine type](/colab/docs/runtimes#default_runtime_specifications) . For pricing details, see [Colab Enterprise pricing](https://cloud.google.com/colab/pricing) .

Each BigQuery pipeline run is logged using [Cloud Logging](/logging/docs) . Logging is automatically enabled for BigQuery pipeline runs, which can incur Cloud Logging billing charges. For more information, see [Cloud Logging pricing](https://cloud.google.com/logging/pricing) .

## What's next

  - Learn how to [create pipelines](/bigquery/docs/create-pipelines) .
  - Learn how to [manage pipelines](/bigquery/docs/manage-pipelines) .
  - Learn how to [schedule pipelines](/bigquery/docs/schedule-pipelines) .
