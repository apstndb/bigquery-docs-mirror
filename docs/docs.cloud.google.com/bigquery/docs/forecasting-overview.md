# Forecasting overview

Forecasting is a technique where you analyze historical data in order to make an informed prediction about future trends. For example, you might analyze historical sales data from several store locations in order to predict future sales at those locations. In BigQuery ML, you perform forecasting on [time series](https://en.wikipedia.org/wiki/Time_series) data.

You can perform forecasting in the following ways:

  - By using the [`  AI.FORECAST  ` function](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-forecast) with the built-in [TimesFM model](/bigquery/docs/timesfm-model) . Use this approach when you need to forecast future values for a single variable. This approach doesn't require you to create and manage a model.
  - By using the [`  ML.FORECAST  ` function](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-forecast) with the [`  ARIMA_PLUS  ` model](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series) . Use this approach when you need to run an ARIMA-based modeling pipeline and decompose the time series into multiple components in order to explain the results. This approach requires you to create and manage a model.
  - By using the [`  ML.FORECAST  ` function](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-forecast) with the [`  ARIMA_PLUS_XREG  ` model](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-multivariate-time-series) . Use this approach when you need to forecast future values for multiple variables. This approach requires you to create and manage a model.

In addition to forecasting, you can use `  ARIMA_PLUS  ` and `  ARIMA_PLUS_XREG  ` models for anomaly detection. For more information, see the following documents:

  - [Anomaly detection overview](/bigquery/docs/anomaly-detection-overview)
  - [Perform anomaly detection with a multivariate time-series forecasting model](/bigquery/docs/time-series-anomaly-detection-tutorial)

## Compare `     ARIMA_PLUS    ` models and the TimesFM model

Use the following table to determine whether to use TimesFM, `  ARIMA_PLUS  ` , or `  ARIMA_PLUS_XREG  ` model for your use case:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Model type</th>
<th><code dir="ltr" translate="no">       ARIMA_PLUS      </code> and <code dir="ltr" translate="no">       ARIMA_PLUS_XREG      </code></th>
<th><code dir="ltr" translate="no">       TimesFM      </code></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Model details</td>
<td>Statistical model that uses the <code dir="ltr" translate="no">       ARIMA      </code> algorithm for the trend component, and a variety of other algorithms for non-trend components. For more information, see <a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series#modeling-pipeline">Time series modeling pipeline</a> and publication below.</td>
<td>Transformer-based foundation model. For more information, see the publications in the next row.</td>
</tr>
<tr class="even">
<td>Publication</td>
<td><a href="https://arxiv.org/abs/2510.24452">ARIMA_PLUS: Large-scale, Accurate, Automatic and Interpretable In-Database Time Series Forecasting and Anomaly Detection in Google BigQuery</a></td>
<td><a href="https://arxiv.org/pdf/2310.10688">A Decoder-only Foundation Model for Time-series Forecasting</a></td>
</tr>
<tr class="odd">
<td>Training required</td>
<td>Yes, one <code dir="ltr" translate="no">       ARIMA_PLUS      </code> or <code dir="ltr" translate="no">       ARIMA_PLUS_XREG      </code> model is trained for each time series.</td>
<td>No, the TimesFM model is pre-trained.</td>
</tr>
<tr class="even">
<td>SQL ease of use</td>
<td>High. Requires a <code dir="ltr" translate="no">       CREATE MODEL      </code> statement and a function call.</td>
<td>Very high. Requires a single function call.</td>
</tr>
<tr class="odd">
<td>Data history used</td>
<td>Uses all time points in the training data, but can be customized to use fewer time points.</td>
<td>Uses 512 time points.</td>
</tr>
<tr class="even">
<td>Accuracy</td>
<td>Very high. For more information, see publications listed in a previous row.</td>
<td>Very high. For more information, see publications listed in a previous row.</td>
</tr>
<tr class="odd">
<td>Customization</td>
<td>High. The <a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series"><code dir="ltr" translate="no">        CREATE MODEL       </code> statement</a> offers arguments that let you tune many model settings, such as the following:
<ul>
<li>Seasonality</li>
<li>Holiday effects</li>
<li>Step changes</li>
<li>Trend</li>
<li>Spikes and dips removal</li>
<li>Forecasting upper and lower bounds</li>
</ul></td>
<td>Low.</td>
</tr>
<tr class="even">
<td>Supports covariates</td>
<td>Yes, when using the <a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-multivariate-time-series"><code dir="ltr" translate="no">        ARIMA_PLUS_XREG       </code> model</a> .</td>
<td>No.</td>
</tr>
<tr class="odd">
<td>Explainability</td>
<td>High. You can use the <a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-explain-forecast"><code dir="ltr" translate="no">        ML.EXPLAIN_FORECAST       </code> function</a> to inspect model components.</td>
<td>Low.</td>
</tr>
<tr class="even">
<td>Best use cases</td>
<td><ul>
<li>You want full control of the model including customization.</li>
<li>You need explainability for model output.</li>
</ul></td>
<td><ul>
<li>You want minimal setup -- doing forecast without creating a model first.</li>
</ul></td>
</tr>
</tbody>
</table>

## Recommended knowledge

By using the default settings of BigQuery ML's statements and functions, you can create and use a forecasting model even without much ML knowledge. However, having basic knowledge about ML development, and forecasting models in particular, helps you optimize both your data and your model to deliver better results. We recommend using the following resources to develop familiarity with ML techniques and processes:

  - [Machine Learning Crash Course](https://developers.google.com/machine-learning/crash-course)
  - [Intro to Machine Learning](https://www.kaggle.com/learn/intro-to-machine-learning)
  - [Intermediate Machine Learning](https://www.kaggle.com/learn/intermediate-machine-learning)
  - [Time Series](https://www.kaggle.com/learn/time-series)
