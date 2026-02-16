# End-to-end user journeys for imported models

This document describes the user journeys for ML models that are imported to BigQuery ML from Cloud Storage, including the statements and functions that you can use to work with imported models. BigQuery ML offers the following types of imported models:

  - [Open Neural Network Exchange (ONNX)](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-onnx)
  - [TensorFlow](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-tensorflow)
  - [TensorFlow Lite](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-tflite)
  - [XGBoost](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-xgboost)

## Imported model user journeys

The following table describes the statements and functions you can use to create and use imported models:

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Model types</th>
<th>Model creation</th>
<th><a href="/bigquery/docs/inference-overview">Inference</a></th>
<th>Tutorials</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>TensorFlow</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-tensorflow"><code dir="ltr" translate="no">        CREATE MODEL       </code></a></td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-predict"><code dir="ltr" translate="no">        ML.PREDICT       </code></a></td>
<td><a href="/bigquery/docs/making-predictions-with-imported-tensorflow-models">Make predictions with imported TensorFlow model</a></td>
</tr>
<tr class="even">
<td>TensorFlow Lite</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-tflite"><code dir="ltr" translate="no">        CREATE MODEL       </code></a></td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-predict"><code dir="ltr" translate="no">        ML.PREDICT       </code></a></td>
<td>N/A</td>
</tr>
<tr class="odd">
<td>Open Neural Network Exchange (ONNX)</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-onnx"><code dir="ltr" translate="no">        CREATE MODEL       </code></a></td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-predict"><code dir="ltr" translate="no">        ML.PREDICT       </code></a></td>
<td><ul>
<li><a href="/bigquery/docs/making-predictions-with-sklearn-models-in-onnx-format">Make predictions with scikit-learn models in ONNX format</a></li>
<li><a href="/bigquery/docs/making-predictions-with-pytorch-models-in-onnx-format">Make predictions PyTorch models in ONNX format</a></li>
</ul></td>
</tr>
<tr class="even">
<td>XGBoost</td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-xgboost"><code dir="ltr" translate="no">        CREATE MODEL       </code></a></td>
<td><a href="/bigquery/docs/reference/standard-sql/bigqueryml-syntax-predict"><code dir="ltr" translate="no">        ML.PREDICT       </code></a></td>
<td>N/A</td>
</tr>
</tbody>
</table>
