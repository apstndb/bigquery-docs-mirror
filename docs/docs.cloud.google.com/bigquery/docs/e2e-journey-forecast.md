---
name: documents/docs.cloud.google.com/bigquery/docs/e2e-journey-forecast
uri: https://docs.cloud.google.com/bigquery/docs/e2e-journey-forecast
title: End-to-end user journeys for time series forecasting models
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# End-to-end user journeys for time series forecasting models

This document describes the user journeys for BigQuery ML time series forecasting models, including the statements and functions that you can use to work with time series forecasting models. BigQuery ML offers the following types of time series forecasting models:

- [`ARIMA_PLUS` univariate models](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series)
- [`ARIMA_PLUS_XREG` multivariate models](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-multivariate-time-series)
- [TimesFM univariate model](https://docs.cloud.google.com/bigquery/docs/timesfm-model)

## Model creation user journeys

The following table describes the statements and functions you can use to create time series forecasting models:

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Model type</th>
<th>Model creation</th>
<th><a href="https://docs.cloud.google.com/bigquery/docs/preprocess-overview">Feature preprocessing</a></th>
<th><a href="https://docs.cloud.google.com/bigquery/docs/hp-tuning-overview">Hyperparameter tuning</a></th>
<th><a href="https://docs.cloud.google.com/bigquery/docs/weights-overview">Model weights</a></th>
<th>Tutorials</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>ARIMA_PLUS</code></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series"><code>CREATE MODEL</code></a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/auto-preprocessing">Automatic preprocessing</a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series#auto_arima">auto.ARIMA <sup>1</sup></a> automatic tuning</td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-arima-coefficients"><code>ML.ARIMA_COEFFICIENTS</code></a></td>
<td><ul>
<li><a href="https://docs.cloud.google.com/bigquery/docs/arima-single-time-series-forecasting-tutorial">Forecast a single time series</a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/arima-multiple-time-series-forecasting-tutorial">Forecast multiple time series</a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/arima-speed-up-tutorial">Forecast millions of time series</a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/time-series-forecasting-holidays-tutorial">Use custom holidays</a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/arima-time-series-forecasting-with-limits-tutorial">Limit forecasted values</a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/arima-time-series-forecasting-with-hierarchical-time-series">Perform hierarchical time series forecasting</a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/time-series-anomaly-detection-tutorial">Perform anomaly detection with a multivariate time-series forecasting model</a></li>
</ul></td>
</tr>
<tr class="even">
<td><code>ARIMA_PLUS_XREG</code></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-multivariate-time-series"><code>CREATE MODEL</code></a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/auto-preprocessing">Automatic preprocessing</a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-multivariate-time-series#auto_arima">auto.ARIMA <sup>1</sup></a> automatic tuning</td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-arima-coefficients"><code>ML.ARIMA_COEFFICIENTS</code></a></td>
<td><ul>
<li><a href="https://docs.cloud.google.com/bigquery/docs/arima-plus-xreg-single-time-series-forecasting-tutorial">Forecast a single time series</a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/arima-plus-xreg-multiple-time-series-forecasting-tutorial">Forecast multiple time series</a></li>
</ul></td>
</tr>
<tr class="odd">
<td>TimesFM</td>
<td>N/A</td>
<td>N/A</td>
<td>N/A</td>
<td>N/A</td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/timesfm-time-series-forecasting-tutorial">Forecast multiple time series</a></td>
</tr>
</tbody>
</table>

<sup>1</sup> The auto.ARIMA algorithm performs hyperparameter tuning for the trend module. The entire modeling pipeline doesn't support hyperparameter tuning. See the [modeling pipeline](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series#modeling-pipeline) for more details.

## Model use user journeys

The following table describes the statements and functions you can use to evaluate, explain, and get forecasts from time series forecasting models:

| Model type        | [Evaluation](https://docs.cloud.google.com/bigquery/docs/evaluate-overview)                                                                                                                                                                                                                                                                                                   | [Inference](https://docs.cloud.google.com/bigquery/docs/inference-overview)                                                                                                                                                                   | [AI explanation](https://docs.cloud.google.com/bigquery/docs/xai-overview)                                                                  |
|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------|
| `ARIMA_PLUS`      | [`ML.EVALUATE`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-evaluate) <sup>1</sup> [`ML.ARIMA_EVALUATE`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-arima-evaluate) [`ML.HOLIDAY_INFO`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-holiday-info) | [`ML.FORECAST`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-forecast) [`ML.DETECT_ANOMALIES`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-detect-anomalies) | [`ML.EXPLAIN_FORECAST` <sup>2</sup>](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-explain-forecast) |
| `ARIMA_PLUS_XREG` | [`ML.EVALUATE`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-evaluate) <sup>1</sup> [`ML.ARIMA_EVALUATE`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-arima-evaluate) [`ML.HOLIDAY_INFO`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-holiday-info) | [`ML.FORECAST`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-forecast) [`ML.DETECT_ANOMALIES`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-detect-anomalies) | [`ML.EXPLAIN_FORECAST` <sup>2</sup>](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-explain-forecast) |
| TimesFM           | [`AI.EVALUATE`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-evaluate)                                                                                                                                                                                                                                                             | [`AI.FORECAST`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-forecast)                                                                                                                             | N/A                                                                                                                                         |

<sup>1</sup> You can input evaluation data to the `ML.EVALUATE` function to compute forecasting metrics such as mean absolute percentage error (MAPE). If you don't have evaluation data, you can use the `ML.ARIMA_EVALUATE` function to output information about the model like drift and variance.

<sup>2</sup> The `ML.EXPLAIN_FORECAST` function encompasses the `ML.FORECAST` function because its output is a superset of the results of `ML.FORECAST` .
