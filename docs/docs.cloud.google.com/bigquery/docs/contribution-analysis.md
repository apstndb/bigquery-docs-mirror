# Contribution analysis overview

Use this document to understand the contribution analysis use case, and the options for performing contribution analysis in BigQuery ML.

## What is contribution analysis?

Contribution analysis, also called key driver analysis, is a method used to generate insights about changes to key metrics in your multi-dimensional data. For example, you can use contribution analysis to see what data contributed to a change in revenue numbers across two quarters, or to compare two sets of training data to understand changes in an ML model's performance.

Contribution analysis is a form of [augmented analytics](https://en.wikipedia.org/wiki/Augmented_Analytics) , which is the use of artificial intelligence (AI) to enhance and automate the analysis and understanding of data. Contribution analysis accomplishes one of the key goals of augmented analytics, which is to help users find patterns in their data.

## Contribution analysis with BigQuery ML

To use contribution analysis in BigQuery ML, create a contribution analysis model with the [`  CREATE MODEL  ` statement](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-contribution-analysis) .

A contribution analysis model detects segments of data that show changes in a given metric by comparing a test set of data to a control set of data. For example, you might use a [table snapshot](/bigquery/docs/table-snapshots-intro) of sales data taken at the end of 2023 as your test data and a table snapshot taken at the end of 2022 as your control data, and compare them to see how your sales changed over time. A contribution analysis model could show you which segment of data, such as online customers in a particular region, drove the biggest change in sales from one year to the next.

A *metric* is the numerical value that contribution analysis models use to measure and compare the changes between the test and control data. You can specify the following types of metrics with a contribution analysis model:

  - [*Summable*](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-contribution-analysis#use_a_summable_metric) : sums the values of a metric column that you specify, and then determines a total for each segment of the data.
  - [*Summable ratio*](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-contribution-analysis#use_a_summable_ratio_metric) : sums the values of two numeric columns that you specify, and determines the ratio between them for each segment of the data.
  - [*Summable by category*](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-contribution-analysis#use_a_summable_by_category_metric) : sums the value of a numeric column and divides it by the number of distinct values from a categorical column.

A *segment* is a slice of the data identified by a given combination of dimension values. For example, for a contribution analysis model based on the `  store_number  ` , `  customer_id  ` , and `  day  ` dimensions, every unique combination of those dimension values represents a segment. In the following table, each row represents a different segment:

<table>
<thead>
<tr class="header">
<th><strong><code dir="ltr" translate="no">        store_number       </code></strong></th>
<th><strong><code dir="ltr" translate="no">        customer_id       </code></strong></th>
<th><strong><code dir="ltr" translate="no">        day       </code></strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>store 1</td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>store 1</td>
<td>customer 1</td>
<td></td>
</tr>
<tr class="odd">
<td>store 1</td>
<td>customer 1</td>
<td>Monday</td>
</tr>
<tr class="even">
<td>store 1</td>
<td>customer 1</td>
<td>Tuesday</td>
</tr>
<tr class="odd">
<td>store 1</td>
<td>customer 2</td>
<td></td>
</tr>
<tr class="even">
<td>store 2</td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

To reduce model creation time, specify an [apriori support threshold](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-contribution-analysis#use_an_apriori_support_threshold) . An apriori support threshold lets you prune small and less relevant segments so that the model uses only the largest and most relevant segments.

After you have created a contribution analysis model, you can use the [`  ML.GET_INSIGHTS  ` function](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-get-insights) to retrieve the metric information calculated by the model. The model output consists of rows of insights, where each insight corresponds to a segment and provides the segment's corresponding metrics.

## Contribution analysis user journey

The following table describes the statements and functions you can use with contribution analysis models:

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Model creation</th>
<th><a href="/bigquery/docs/preprocess-overview">Feature preprocessing</a></th>
<th>Insights generation</th>
<th>Tutorials</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-contribution-analysis"><code dir="ltr" translate="no">        CREATE MODEL       </code></a></td>
<td><a href="/bigquery/docs/manual-preprocessing">Manual preprocessing</a></td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-get-insights"><code dir="ltr" translate="no">        ML.GET_INSIGHTS       </code></a></td>
<td><ul>
<li><a href="/bigquery/docs/get-contribution-analysis-insights">Get data insights from a contribution analysis model using a summable metric</a></li>
<li><a href="/bigquery/docs/get-contribution-analysis-insights-sum-ratio">Get data insights from a contribution analysis model using a summable ratio metric</a></li>
</ul></td>
</tr>
</tbody>
</table>

## What's next

  - [Create a contribution analysis model](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-contribution-analysis)
  - [Get data insights from a contribution analysis model](/bigquery/docs/get-contribution-analysis-insights)
