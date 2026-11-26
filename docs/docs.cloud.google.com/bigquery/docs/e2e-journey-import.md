---
name: documents/docs.cloud.google.com/bigquery/docs/e2e-journey-import
uri: https://docs.cloud.google.com/bigquery/docs/e2e-journey-import
title: End-to-end user journeys for imported models
description: Understand BigQuery ML end-to-end user journeys for imported models like XGBoost, ONNX, and TensorFlow. The workflow covers model creation, training, evaluation, and inference.
data_source: docs.cloud.google.com
---

# End-to-end user journeys for imported models

You can import machine learning (ML) models from Cloud Storage into BigQuery ML to run SQL-based predictions directly on your BigQuery data using models trained in external frameworks. Understanding these end-to-end user journeys can help you find the exact `CREATE MODEL` statements, `ML.PREDICT` inference workflows, and tutorials supported for [Open Neural Network Exchange (ONNX)](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-onnx) , [TensorFlow](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-tensorflow) , [TensorFlow Lite](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-tflite) , and [XGBoost](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-xgboost) models.

## Imported model user journeys

The following table describes the statements and functions you can use to create and use imported models:

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="header">
<th>Model types</th>
<th>Model creation</th>
<th><a href="https://docs.cloud.google.com/bigquery/docs/inference-overview">Inference</a></th>
<th>Tutorials</th>
</tr>

<tr class="odd">
<td>TensorFlow</td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-tensorflow"><code>CREATE MODEL</code></a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-predict"><code>ML.PREDICT</code></a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/making-predictions-with-imported-tensorflow-models">Make predictions with imported TensorFlow model</a></td>
</tr>
<tr class="even">
<td>TensorFlow Lite</td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-tflite"><code>CREATE MODEL</code></a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-predict"><code>ML.PREDICT</code></a></td>
<td>N/A</td>
</tr>
<tr class="odd">
<td>Open Neural Network Exchange (ONNX)</td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-onnx"><code>CREATE MODEL</code></a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-predict"><code>ML.PREDICT</code></a></td>
<td><ul>
<li><a href="https://docs.cloud.google.com/bigquery/docs/making-predictions-with-sklearn-models-in-onnx-format">Make predictions with scikit-learn models in ONNX format</a></li>
<li><a href="https://docs.cloud.google.com/bigquery/docs/making-predictions-with-pytorch-models-in-onnx-format">Make predictions PyTorch models in ONNX format</a></li>
</ul></td>
</tr>
<tr class="even">
<td>XGBoost</td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-xgboost"><code>CREATE MODEL</code></a></td>
<td><a href="https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-predict"><code>ML.PREDICT</code></a></td>
<td>N/A</td>
</tr>
</tbody>
</table>
