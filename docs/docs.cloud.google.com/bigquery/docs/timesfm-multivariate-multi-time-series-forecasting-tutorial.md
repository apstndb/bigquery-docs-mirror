---
name: documents/docs.cloud.google.com/bigquery/docs/timesfm-multivariate-multi-time-series-forecasting-tutorial
uri: https://docs.cloud.google.com/bigquery/docs/timesfm-multivariate-multi-time-series-forecasting-tutorial
title: Forecast multiple time series with a TimesFM multivariate model
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This product is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

This tutorial teaches you how to perform multivariate forecasting across multiple time series by using the [`AI.FORECAST` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-forecast) with the [`TimesFM 3.0` model](https://docs.cloud.google.com/bigquery/docs/timesfm-model) that's built into BigQuery ML. Multivariate forecasting helps you improve forecast accuracy by incorporating other variables (covariates) that influence the target.

By specifying identifier columns, you can generate forecasts for multiple distinct entities simultaneously. This tutorial demonstrates how to forecast New York taxi trips and fares for different pickup zones by incorporating historical trip distance data, which is a past covariate.

## Objectives

  - Prepare a unified dataset for multiple time series.
  - Generate predictions for New York taxi data by using the `AI.FORECAST` function with the `TimesFM 3.0` model.

## Costs

This tutorial uses billable components of Google Cloud, including the following:

  - BigQuery
  - BigQuery ML

For more information, see [BigQuery pricing](https://cloud.google.com/bigquery/pricing) and [BigQuery ML pricing](https://cloud.google.com/bigquery/pricing#bqml) .

## Before you begin

1.  Enable the BigQuery API, if it is not already enabled.
    
    **Roles required to enable APIs**
    
    To enable APIs, you need the `serviceusage.services.enable` permission. If you created the project, then you likely already have this permission through the Owner role ( `roles/owner` ). Otherwise, you can get this permission through the Service Usage Admin role ( `roles/serviceusage.serviceUsageAdmin` ). [Learn how to grant roles](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .
    
    For new projects, the BigQuery API is automatically enabled.

### Required roles

To get the permissions that you need to complete the tasks in this tutorial, ask your administrator to grant you the following IAM roles:

  - Create the dataset: [BigQuery Data Editor](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor) ( `roles/bigquery.dataEditor` )
  - Create the model:
      - [BigQuery Data Editor](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor) ( `roles/bigquery.dataEditor` )
      - [BigQuery Job User](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.jobUser) ( `roles/bigquery.jobUser` )
  - Run inference:
      - [BigQuery Data Editor](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor) ( `roles/bigquery.dataEditor` )
      - [BigQuery Job User](https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.jobUser) ( `roles/bigquery.jobUser` )

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

These predefined roles contain the permissions required to complete the tasks in this tutorial. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to complete the tasks in this tutorial:

  - Create the dataset: `bigquery.datasets.create`
  - Create the model:
      - `bigquery.jobs.create`
      - `bigquery.models.create`
      - `bigquery.models.getData`
      - `bigquery.models.updateData`
  - Run inference:
      - `bigquery.models.getData`
      - `bigquery.jobs.create`

You might also be able to get these permissions with [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

For more information about IAM roles and permissions in BigQuery, see [Introduction to IAM](https://docs.cloud.google.com/bigquery/docs/access-control) .

## Prepare the input data

Unlike other multivariate models that might require separate tables for historical and future covariates, the `AI.FORECAST` function with `TimesFM 3.0` expects a single input table or query.

For a multiple time series forecast, your data must include one or more identifier columns to separate the data into distinct time series. In this example, one time series contains data for pickup location 132 (JFK Airport) and the other time series contains data for pickup location 138 (LaGuardia Airport). Make sure your data meets the following requirements for every individual time series:

  - Historical rows: contain non-null values for timestamps, targets, and past covariates.

Because this example doesn't use future covariates, the input query only needs to provide historical data. Your input table must contain columns with the following data:

  - The date of the taxi trip.
  - The pickup location: either 132 or 138.
  - The number of trips on that date. This is a target column.
  - The average fare amount on that date. This is a target column.
  - The average distance of trips on that date. This is a past covariate column used in the forecast.

## Forecast the multiple multivariate time series

The following query forecasts the number of trips and average fare per day for the next 14 days for the JFK and LaGuardia pickup zones. It defines `past_cov_avg_distance` as a feature that's only known historically. You must provide the `id_cols` argument so the model knows how to separate the different time series.

Follow these steps to forecast data with the `TimesFM 3.0` model:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, paste in the following query and click **Run** :
    
        SELECT
          pickup_location_id,
          FORMAT_DATE("%Y-%m-%d", pickup_date) AS pickup_date,
          # Extract the forecast value and prediction intervals for the number of trips target
          target_num_trips.value AS forecasted_num_trips,
          target_num_trips.prediction_interval_lower_bound AS num_trips_lower,
          target_num_trips.prediction_interval_upper_bound AS num_trips_upper,
          # Extract the forecast value and prediction intervals for the average fare target
          target_avg_fare.value AS forecasted_avg_fare,
          target_avg_fare.prediction_interval_lower_bound AS avg_fare_lower,
          target_avg_fare.prediction_interval_upper_bound AS avg_fare_upper
        FROM AI.FORECAST(
          (
            SELECT
              DATE(pickup_datetime) AS pickup_date,
              pickup_location_id,
              COUNT(*) AS target_num_trips,
              AVG(fare_amount) AS target_avg_fare,
              AVG(trip_distance) AS past_cov_avg_distance
            FROM `bigquery-public-data.new_york_taxi_trips.tlc_yellow_trips_2022`
            WHERE pickup_datetime >= "2022-01-01" AND pickup_datetime < "2022-04-01"
              AND pickup_location_id IN ("132", "138") -- JFK and LaGuardia Airports
            GROUP BY 1, 2
          ),
          model => "TimesFM 3.0",
          target_cols => ["target_num_trips", "target_avg_fare"],
          past_covariate_cols => ["past_cov_avg_distance"],
          timestamp_col => "pickup_date",
          id_cols => ["pickup_location_id"],
          horizon => 14
        )
        ORDER BY pickup_date;

The result is similar to the following, with values rounded for clarity:

    +--------------------+-------------+----------------------+-----------------+-----------------+---------------------+----------------+----------------+
    | pickup_location_id | pickup_date | forecasted_num_trips | num_trips_lower | num_trips_upper | forecasted_avg_fare | avg_fare_lower | avg_fare_upper |
    +--------------------+-------------+----------------------+-----------------+-----------------+---------------------+----------------+----------------+
    | 132                | 2022-04-01  | 5240                 | 4633            | 5842            | 47                  | 46             | 48             |
    | 138                | 2022-04-01  | 3451                 | 2848            | 4008            | 32                  | 31             | 34             |
    | ...                | ...         | ...                  | ...             | ...             | ...                 | ...            | ...            |
    +--------------------+-------------+----------------------+-----------------+-----------------+---------------------+----------------+----------------+

The results show the forecasted number of trips and average fare amount for the next 14 days at the JFK and LaGuardia pickup zones. The results also include the lower and upper bounds for a 95% prediction interval for each forecasted value.

## Clean up

To avoid incurring charges to your Google Cloud account for the resources used in this tutorial, either delete the project that contains the resources, or keep the project and delete the individual resources.

### Delete your project

> **Caution** : Deleting a project has the following effects:
> 
>   - **Everything in the project is deleted.** If you used an existing project for the tasks in this document, when you delete it, you also delete any other work you've done in the project.
>   - **Custom project IDs are lost.** When you created this project, you might have created a custom project ID that you want to use in the future. To preserve the URLs that use the project ID, such as an `appspot.com` URL, delete selected resources inside the project instead of deleting the whole project.
> 
> If you plan to explore multiple architectures, tutorials, or quickstarts, reusing projects can help you avoid exceeding project quota limits.

In the Google Cloud console, go to the **Manage resources** page.

In the project list, select the project that you want to delete, and then click **Delete** .

In the dialog, type the project ID, and then click **Shut down** to delete the project.

## What's next

  - For an overview of BigQuery ML, see [Introduction to AI and ML in BigQuery](https://docs.cloud.google.com/bigquery/docs/bqml-introduction) .
  - Learn how to [forecast single or multiple time series with a TimesFM univariate model](https://docs.cloud.google.com/bigquery/docs/timesfm-time-series-forecasting-tutorial) .
  - Learn how to [forecast single time series with a TimesFM multivariate model](https://docs.cloud.google.com/bigquery/docs/timesfm-multivariate-single-time-series-forecasting-tutorial) .
