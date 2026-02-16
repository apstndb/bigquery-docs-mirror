# End-to-end user journeys for time series forecasting models

This document describes the user journeys for BigQuery ML time series forecasting models, including the statements and functions that you can use to work with time series forecasting models. BigQuery ML offers the following types of time series forecasting models:

  - [`  ARIMA_PLUS  ` univariate models](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series)
  - [`  ARIMA_PLUS_XREG  ` multivariate models](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-multivariate-time-series)
  - [TimesFM univariate model](/bigquery/docs/timesfm-model)

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
<th><a href="/bigquery/docs/preprocess-overview">Feature preprocessing</a></th>
<th><a href="/bigquery/docs/hp-tuning-overview">Hyperparameter tuning</a></th>
<th><a href="/bigquery/docs/weights-overview">Model weights</a></th>
<th>Tutorials</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       ARIMA_PLUS      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series"><code dir="ltr" translate="no">        CREATE MODEL       </code></a></td>
<td><a href="/bigquery/docs/auto-preprocessing">Automatic preprocessing</a></td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series#auto_arima">auto.ARIMA <sup>1</sup></a> automatic tuning</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-arima-coefficients"><code dir="ltr" translate="no">        ML.ARIMA_COEFFICIENTS       </code></a></td>
<td><ul>
<li><a href="/bigquery/docs/arima-single-time-series-forecasting-tutorial">Forecast a single time series</a></li>
<li><a href="/bigquery/docs/arima-multiple-time-series-forecasting-tutorial">Forecast multiple time series</a></li>
<li><a href="/bigquery/docs/arima-speed-up-tutorial">Forecast millions of time series</a></li>
<li><a href="/bigquery/docs/time-series-forecasting-holidays-tutorial">Use custom holidays</a></li>
<li><a href="/bigquery/docs/arima-time-series-forecasting-with-limits-tutorial">Limit forecasted values</a></li>
<li><a href="/bigquery/docs/arima-time-series-forecasting-with-hierarchical-time-series">Perform hierarchical time series forecasting</a></li>
<li><a href="/bigquery/docs/time-series-anomaly-detection-tutorial">Perform anomaly detection with a multivariate time-series forecasting model</a></li>
</ul></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ARIMA_PLUS_XREG      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-multivariate-time-series"><code dir="ltr" translate="no">        CREATE MODEL       </code></a></td>
<td><a href="/bigquery/docs/auto-preprocessing">Automatic preprocessing</a></td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-multivariate-time-series#auto_arima">auto.ARIMA <sup>1</sup></a> automatic tuning</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-arima-coefficients"><code dir="ltr" translate="no">        ML.ARIMA_COEFFICIENTS       </code></a></td>
<td><ul>
<li><a href="/bigquery/docs/arima-plus-xreg-single-time-series-forecasting-tutorial">Forecast a single time series</a></li>
<li><a href="/bigquery/docs/arima-plus-xreg-multiple-time-series-forecasting-tutorial">Forecast multiple time series</a></li>
</ul></td>
</tr>
<tr class="odd">
<td>TimesFM</td>
<td>N/A</td>
<td>N/A</td>
<td>N/A</td>
<td>N/A</td>
<td><a href="/bigquery/docs/timesfm-time-series-forecasting-tutorial">Forecast multiple time series</a></td>
</tr>
</tbody>
</table>

<sup>1</sup> The auto.ARIMA algorithm performs hyperparameter tuning for the trend module. Hyperparameter tuning isn't supported for the entire modeling pipeline. See the [modeling pipeline](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series#modeling-pipeline) for more details.

## Model use user journeys

The following table describes the statements and functions you can use to evaluate, explain, and get forecasts from time series forecasting models:

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Model type</th>
<th><a href="/bigquery/docs/evaluate-overview">Evaluation</a></th>
<th><a href="/bigquery/docs/inference-overview">Inference</a></th>
<th><a href="/bigquery/docs/xai-overview">AI explanation</a></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       ARIMA_PLUS      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-evaluate"><code dir="ltr" translate="no">        ML.EVALUATE       </code></a> <sup>1</sup><br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-arima-evaluate"><code dir="ltr" translate="no">        ML.ARIMA_EVALUATE       </code></a><br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-holiday-info"><code dir="ltr" translate="no">        ML.HOLIDAY_INFO       </code></a></td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-forecast"><code dir="ltr" translate="no">        ML.FORECAST       </code></a><br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-detect-anomalies"><code dir="ltr" translate="no">        ML.DETECT_ANOMALIES       </code></a></td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-explain-forecast"><code dir="ltr" translate="no">        ML.EXPLAIN_FORECAST       </code> <sup>2</sup></a></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ARIMA_PLUS_XREG      </code></td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-evaluate"><code dir="ltr" translate="no">        ML.EVALUATE       </code></a> <sup>1</sup><br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-arima-evaluate"><code dir="ltr" translate="no">        ML.ARIMA_EVALUATE       </code></a><br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-holiday-info"><code dir="ltr" translate="no">        ML.HOLIDAY_INFO       </code></a></td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-forecast"><code dir="ltr" translate="no">        ML.FORECAST       </code></a><br />
<a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-detect-anomalies"><code dir="ltr" translate="no">        ML.DETECT_ANOMALIES       </code></a></td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-explain-forecast"><code dir="ltr" translate="no">        ML.EXPLAIN_FORECAST       </code> <sup>2</sup></a></td>
</tr>
<tr class="odd">
<td>TimesFM</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-evaluate"><code dir="ltr" translate="no">        AI.EVALUATE       </code></a></td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-forecast"><code dir="ltr" translate="no">        AI.FORECAST       </code></a></td>
<td>N/A</td>
</tr>
</tbody>
</table>

<sup>1</sup> You can input evaluation data to the `  ML.EVALUATE  ` function to compute forecasting metrics such as mean absolute percentage error (MAPE). If you don't have evaluation data, you can use the `  ML.ARIMA_EVALUATE  ` function to output information about the model like drift and variance.

<sup>2</sup> The `  ML.EXPLAIN_FORECAST  ` function encompasses the `  ML.FORECAST  ` function because its output is a superset of the results of `  ML.FORECAST  ` .
