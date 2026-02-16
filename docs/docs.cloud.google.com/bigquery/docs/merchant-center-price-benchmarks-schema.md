# Google Merchant Center price benchmarks table

## Overview

**Caution:** BigQuery will no longer support the Price Benchmarks report on September 1, 2025. We recommend that you migrate to use the [Price Competitiveness report](/bigquery/docs/merchant-center-price-competitiveness-schema) instead. For more information about migrating to the new report, see [Migrate the price competitiveness report](/bigquery/docs/merchant-center-price-competitiveness-migration) .

Price Benchmarks data in BigQuery helps merchants understand how other merchants are pricing the same product. When your Google Merchant Center reporting data is transferred to BigQuery, the format of the `  Products_PriceBenchmarks_  ` table provides a daily price benchmark per country and per product.

The data is written to a table named `  Products_PriceBenchmarks_ MERCHANT_ID  ` if you are using an individual Merchant ID, or `  Products_PriceBenchmarks_ AGGREGATOR_ID  ` if you're using an MCA account.

## Schema

The `  Products_PriceBenchmarks  ` table has the following schema:

<table>
<thead>
<tr class="header">
<th>Column</th>
<th>BigQuery data type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">         product_id       </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Content API's REST ID of the product in the form: <code dir="ltr" translate="no">       channel:content_language:feed_label:offer_id      </code> , similar to the way it's defined in the <a href="/bigquery/docs/merchant-center-products-schema">products table schema</a> . This field is a primary key.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       merchant_id      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>Merchant account ID.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       aggregator_id      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
<td>Aggregator account ID for multi-client accounts.</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       country_of_sale      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Country where the user performed the query on Google.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       price_benchmark_value      </code></td>
<td><code dir="ltr" translate="no">       FLOAT      </code></td>
<td>The average click-weighted price for a given product across all merchants who advertise that same product on Shopping ads. Products are matched based on their GTIN. For more details, see the <a href="https://support.google.com/merchants/answer/9626903">Help Center article</a> .</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       price_benchmark_currency      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td>Currency of the benchmark value.</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       price_benchmark_timestamp      </code></td>
<td><code dir="ltr" translate="no">       DATETIME      </code></td>
<td>Timestamp of the benchmark.</td>
</tr>
</tbody>
</table>

## Example: compare product prices to benchmarks

The following SQL query joins `  Products  ` and `  Price Benchmarks  ` data to return the list of products and associated benchmarks.

``` text
WITH products AS
(
  SELECT
    _PARTITIONDATE AS date,
    *
  FROM
    dataset.Products_merchant_id
  WHERE
   _PARTITIONDATE >= 'YYYY-MM-DD'
),
benchmarks AS
(
  SELECT
    _PARTITIONDATE AS date,
    *
  FROM
    dataset.Products_PriceBenchmarks_merchant_id
  WHERE
    _PARTITIONDATE >= 'YYYY-MM-DD'
)
SELECT
  products.date,
  products.product_id,
  products.merchant_id,
  products.aggregator_id,
  products.price,
  products.sale_price,
  benchmarks.price_benchmark_value,
  benchmarks.price_benchmark_currency,
  benchmarks.country_of_sale
FROM
  products
INNER JOIN
  benchmarks
ON products.product_id = benchmarks.product_id AND
   products.merchant_id = benchmarks.merchant_id AND
   products.date = benchmarks.date
```

Notes on joining the data:  
1\. Not all products have benchmarks, so use INNER JOIN or LEFT JOIN accordingly.  
2\. Each product may have multiple benchmarks (one per country).
