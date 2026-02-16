# Supported input feature types

BigQuery ML supports different input feature types for different model types. Supported input feature types are listed in the following table:

Model Category

[Model Types](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create#model_option_list)

[Numeric types](/bigquery/docs/reference/standard-sql/data-types#numeric_types) ( [INT64](/bigquery/docs/reference/standard-sql/data-types#integer_types) , [NUMERIC](/bigquery/docs/reference/standard-sql/data-types#decimal_types) , [BIGNUMERIC](/bigquery/docs/reference/standard-sql/data-types#decimal_types) , [FLOAT64](/bigquery/docs/reference/standard-sql/data-types#floating_point_types) )

Categorical types ( [BOOL](/bigquery/docs/reference/standard-sql/data-types#boolean_type) , [STRING](/bigquery/docs/reference/standard-sql/data-types#string_type) , [BYTES](/bigquery/docs/reference/standard-sql/data-types#bytes_type) , [DATE](/bigquery/docs/reference/standard-sql/data-types#date_type) , [DATETIME](/bigquery/docs/reference/standard-sql/data-types#datetime_type) )

[TIMESTAMP](/bigquery/docs/reference/standard-sql/data-types#timestamp_type)

[STRUCT](/bigquery/docs/reference/standard-sql/data-types#struct_type)

[GEOGRAPHY](/bigquery/docs/reference/standard-sql/data-types#geography_type)

[ARRAY](/bigquery/docs/reference/standard-sql/data-types#array_type) \< [Numeric types](/bigquery/docs/reference/standard-sql/data-types#numeric_types) \>

[ARRAY](/bigquery/docs/reference/standard-sql/data-types#array_type) \<Categorical types\>

[ARRAY](/bigquery/docs/reference/standard-sql/data-types#array_type) \< [STRUCT](/bigquery/docs/reference/standard-sql/data-types#struct_type) \< [INT64](/bigquery/docs/reference/standard-sql/data-types#integer_types) , [Numeric types](/bigquery/docs/reference/standard-sql/data-types#numeric_types) \>\>

Supervised Learning

Linear & Logistic Regression

✔

✔

✔

✔

✔

✔

✔

Deep Neural Networks

✔

✔

✔

✔

✔

✔

Wide-and-Deep

✔

✔

✔

✔

✔

✔

Boosted trees

✔

✔

✔

✔

✔

✔

AutoML Tables

✔

✔

✔

✔

✔

✔

Unsupervised Learning

K-means

✔

✔

✔

✔

✔

✔

✔

PCA

✔

✔

✔

✔

✔

✔

Autoencoder

✔

✔

✔

✔

✔

✔

✔

Time Series Models

ARIMA\_PLUS\_XREG

✔

✔

✔

✔

✔

✔

**Note:** [Matrix Factorization](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-matrix-factorization#inputs) and [ARIMA\_PLUS](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-time-series#time_series_data_col) models have special input feature types. The input types listed for [ARIMA\_PLUS\_XREG](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-multivariate-time-series#time_series_data_col) are only for external regressors.

## Dense vector input

BigQuery ML supports `  ARRAY<numerical>  ` as dense vector input during model training. The embedding feature is a special type of dense vector. see the [`  AI.GENERATE_EMBEDDING  ` function](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate-embedding) for more information.

## Sparse input

BigQuery ML supports `  ARRAY<STRUCT>  ` as sparse input during model training. Each struct contains an `  INT64  ` value that represents its zero-based index, and a [numeric type](/bigquery/docs/reference/standard-sql/data-types#numeric_types) that represents the corresponding value.

Below is an example of a sparse tensor input for the integer array `  [0,1,0,0,0,0,1]  ` :

``` text
ARRAY<STRUCT<k INT64, v INT64>>[(1, 1), (6, 1)] AS f1
```
