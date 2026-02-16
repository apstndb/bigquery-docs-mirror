# Use open source a Python libraries

You can choose from among three Python libraries in BigQuery, based on your use case.

<table>
<thead>
<tr class="header">
<th></th>
<th>Use case</th>
<th>Maintained by</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>BigQuery DataFrames</td>
<td>Python based data processing and ML operations with server-side processing (for example, using slots)</td>
<td>Google</td>
<td>Pandas and Scikit learn APIs implemented with server-side pushdown. For more information, see <a href="/bigquery/docs/bigquery-dataframes-introduction">Introduction to BigQuery DataFrames</a> .</td>
</tr>
<tr class="even">
<td>pandas-gbq</td>
<td>Python based data processing using client side data copy</td>
<td>Open source library maintained by PyData and volunteer contributors</td>
<td>Lets you move data to and from Python DataFrames on the client side. For more information, see the <a href="https://googleapis.dev/python/pandas-gbq/latest/index.html">documentation</a> and <a href="https://github.com/googleapis/python-bigquery-pandas">source code</a> .</td>
</tr>
<tr class="odd">
<td>google-cloud-bigquery</td>
<td>BigQuery deployment, administration, and SQL-based querying</td>
<td>Open source library maintained by Google</td>
<td>Python package that wraps all the BigQuery APIs. For more information, see the <a href="/python/docs/reference/bigquery/latest">documentation</a> and <a href="https://github.com/googleapis/python-bigquery">source code</a> .</td>
</tr>
</tbody>
</table>

## Using pandas-gbq and google-cloud-bigquery

The `  pandas-gbq  ` library provides a simple interface for running queries and uploading pandas dataframes to BigQuery. It is a thin wrapper around the [BigQuery client library](/bigquery/docs/reference/libraries) , `  google-cloud-bigquery  ` . Both of these libraries focus on helping you perform data analysis using SQL.

### Install the libraries

To use the code samples in this guide, install the `  pandas-gbq  ` package and the BigQuery Python client libraries.

Install the [`  pandas-gbq  `](https://pypi.org/project/pandas-gbq/) and [`  google-cloud-bigquery  `](https://pypi.org/project/google-cloud-bigquery/) packages.

``` text
pip install --upgrade pandas-gbq 'google-cloud-bigquery[bqstorage,pandas]'
```

### Running Queries

Both libraries support querying data stored in BigQuery. Key differences between the libraries include:

<table>
<thead>
<tr class="header">
<th></th>
<th>pandas-gbq</th>
<th>google-cloud-bigquery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Default SQL syntax</td>
<td>GoogleSQL (configurable with <code dir="ltr" translate="no">       pandas_gbq.context.dialect      </code> )</td>
<td>GoogleSQL</td>
</tr>
<tr class="even">
<td>Query configurations</td>
<td>Sent as dictionary in the format of a <a href="/bigquery/docs/reference/rest/v2/jobs/query#QueryRequest">query request</a> .</td>
<td>Use the <a href="/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig"><code dir="ltr" translate="no">        QueryJobConfig       </code></a> class, which contains properties for the various API configuration options.</td>
</tr>
</tbody>
</table>

#### Querying data with the GoogleSQL syntax

The following sample shows how to run a GoogleSQL query with and without explicitly specifying a project. For both libraries, if a project is not specified, the project will be determined from the [default credentials](https://googleapis.dev/python/google-auth/latest/reference/google.auth.html#google.auth.default) .

**Note:** The `  pandas.read_gbq  ` method defaults to legacy SQL. To use standard SQL, you must explicitly set the `  dialect  ` parameter to `  'standard'  ` , as shown.

**`  pandas-gbq  ` :**

``` python
import pandas

sql = """
    SELECT name
    FROM `bigquery-public-data.usa_names.usa_1910_current`
    WHERE state = 'TX'
    LIMIT 100
"""

# Run a Standard SQL query using the environment's default project
df = pandas.read_gbq(sql, dialect="standard")

# Run a Standard SQL query with the project set explicitly
project_id = "your-project-id"
df = pandas.read_gbq(sql, project_id=project_id, dialect="standard")
```

**`  google-cloud-bigquery  ` :**

``` python
from google.cloud import bigquery

client = bigquery.Client()
sql = """
    SELECT name
    FROM `bigquery-public-data.usa_names.usa_1910_current`
    WHERE state = 'TX'
    LIMIT 100
"""

# Run a Standard SQL query using the environment's default project
df = client.query(sql).to_dataframe()

# Run a Standard SQL query with the project set explicitly
project_id = "your-project-id"
df = client.query(sql, project=project_id).to_dataframe()
```

#### Querying data with the legacy SQL syntax

The following sample shows how to run a query using legacy SQL syntax. See the [GoogleSQL migration guide](/bigquery/docs/reference/standard-sql/migrating-from-legacy-sql) for guidance on updating your queries to GoogleSQL.

**`  pandas-gbq  ` :**

``` python
import pandas

sql = """
    SELECT name
    FROM [bigquery-public-data:usa_names.usa_1910_current]
    WHERE state = 'TX'
    LIMIT 100
"""

df = pandas.read_gbq(sql, dialect="legacy")
```

**`  google-cloud-bigquery  ` :**

``` python
from google.cloud import bigquery

client = bigquery.Client()
sql = """
    SELECT name
    FROM [bigquery-public-data:usa_names.usa_1910_current]
    WHERE state = 'TX'
    LIMIT 100
"""
query_config = bigquery.QueryJobConfig(use_legacy_sql=True)

df = client.query(sql, job_config=query_config).to_dataframe()
```

#### Using the BigQuery Storage API to download large results

Use the [BigQuery Storage API](/bigquery/docs/reference/storage) to [speed-up downloads of large results by 15 to 31 times](https://friendliness.dev/2019/07/29/bigquery-arrow/) .

**`  pandas-gbq  ` :**

``` python
import pandas

sql = "SELECT * FROM `bigquery-public-data.irs_990.irs_990_2012`"

# Use the BigQuery Storage API to download results more quickly.
df = pandas.read_gbq(sql, dialect="standard", use_bqstorage_api=True)
```

**`  google-cloud-bigquery  ` :**

``` python
from google.cloud import bigquery

client = bigquery.Client()
sql = "SELECT * FROM `bigquery-public-data.irs_990.irs_990_2012`"

# The client library uses the BigQuery Storage API to download results to a
# pandas dataframe if the API is enabled on the project, the
# `google-cloud-bigquery-storage` package is installed, and the `pyarrow`
# package is installed.
df = client.query(sql).to_dataframe()
```

#### Running a query with a configuration

Sending a configuration with a BigQuery API request is required to perform certain complex operations, such as running a parameterized query or specifying a destination table to store the query results. In `  pandas-gbq  ` , the configuration must be sent as a dictionary in the format of a [query request](/bigquery/docs/reference/rest/v2/jobs/query#QueryRequest) . In `  google-cloud-bigquery  ` , job configuration classes are provided, such as [`  QueryJobConfig  `](/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.QueryJobConfig) , which contain the necessary properties to configure complex jobs.

The following sample shows how to run a query with named parameters.

**`  pandas-gbq  ` :**

``` python
import pandas

sql = """
    SELECT name
    FROM `bigquery-public-data.usa_names.usa_1910_current`
    WHERE state = @state
    LIMIT @limit
"""
query_config = {
    "query": {
        "parameterMode": "NAMED",
        "queryParameters": [
            {
                "name": "state",
                "parameterType": {"type": "STRING"},
                "parameterValue": {"value": "TX"},
            },
            {
                "name": "limit",
                "parameterType": {"type": "INTEGER"},
                "parameterValue": {"value": 100},
            },
        ],
    }
}

df = pandas.read_gbq(sql, configuration=query_config)
```

**`  google-cloud-bigquery  ` :**

``` python
from google.cloud import bigquery

client = bigquery.Client()
sql = """
    SELECT name
    FROM `bigquery-public-data.usa_names.usa_1910_current`
    WHERE state = @state
    LIMIT @limit
"""
query_config = bigquery.QueryJobConfig(
    query_parameters=[
        bigquery.ScalarQueryParameter("state", "STRING", "TX"),
        bigquery.ScalarQueryParameter("limit", "INTEGER", 100),
    ]
)

df = client.query(sql, job_config=query_config).to_dataframe()
```

### Loading a pandas DataFrame to a BigQuery table

Both libraries support uploading data from a pandas DataFrame to a new table in BigQuery. Key differences include:

<table>
<thead>
<tr class="header">
<th></th>
<th>pandas-gbq</th>
<th>google-cloud-bigquery</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Type support</td>
<td>Converts the DataFrame to CSV format before sending to the API, which does not support nested or array values.</td>
<td>Converts the DataFrame to Parquet or CSV format before sending to the API, which supports nested and array values. Choose Parquet for struct and array values and CSV for date and time serialization flexibility. Parquet is the default choice. Note that <code dir="ltr" translate="no">       pyarrow      </code> , which is the parquet engine used to send the DataFrame data to the BigQuery API, must be installed to load the DataFrame to a table.</td>
</tr>
<tr class="even">
<td>Load configurations</td>
<td>You can optionally specify a <a href="/bigquery/docs/reference/rest/v2/tables#TableSchema">table schema</a> ).</td>
<td>Use the <a href="/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.LoadJobConfig"><code dir="ltr" translate="no">        LoadJobConfig       </code></a> class, which contains properties for the various API configuration options.</td>
</tr>
</tbody>
</table>

**`  pandas-gbq  ` :**

``` python
import pandas

df = pandas.DataFrame(
    {
        "my_string": ["a", "b", "c"],
        "my_int64": [1, 2, 3],
        "my_float64": [4.0, 5.0, 6.0],
        "my_timestamp": [
            pandas.Timestamp("1998-09-04T16:03:14"),
            pandas.Timestamp("2010-09-13T12:03:45"),
            pandas.Timestamp("2015-10-02T16:00:00"),
        ],
    }
)
table_id = "my_dataset.new_table"

df.to_gbq(table_id)
```

**`  google-cloud-bigquery  ` :**

The `  google-cloud-bigquery  ` package requires the `  pyarrow  ` library to serialize a pandas DataFrame to a Parquet file.

Install the `  pyarrow  ` package:

``` text
 pip install pyarrow
```

``` python
from google.cloud import bigquery
import pandas

df = pandas.DataFrame(
    {
        "my_string": ["a", "b", "c"],
        "my_int64": [1, 2, 3],
        "my_float64": [4.0, 5.0, 6.0],
        "my_timestamp": [
            pandas.Timestamp("1998-09-04T16:03:14"),
            pandas.Timestamp("2010-09-13T12:03:45"),
            pandas.Timestamp("2015-10-02T16:00:00"),
        ],
    }
)
client = bigquery.Client()
table_id = "my_dataset.new_table"
# Since string columns use the "object" dtype, pass in a (partial) schema
# to ensure the correct BigQuery data type.
job_config = bigquery.LoadJobConfig(
    schema=[
        bigquery.SchemaField("my_string", "STRING"),
    ]
)

job = client.load_table_from_dataframe(df, table_id, job_config=job_config)

# Wait for the load job to complete.
job.result()
```

### Features not supported by pandas-gbq

While the `  pandas-gbq  ` library provides a useful interface for querying data and writing data to tables, it does not cover many of the BigQuery API features, including but not limited to:

  - [Managing datasets](/bigquery/docs/datasets) , including [creating new datasets](/bigquery/docs/datasets) , [updating dataset properties](/bigquery/docs/updating-datasets) , and [deleting datasets](/bigquery/docs/managing-datasets#delete-datasets)
  - [Loading data into BigQuery](/bigquery/docs/loading-data) from formats other than pandas DataFrames or from pandas DataFrames with JSON columns
  - [Managing tables](/bigquery/docs/managing-tables) , including [listing tables in a dataset](/bigquery/docs/tables#list_tables_in_a_dataset) , [copying table data](/bigquery/docs/managing-tables#copying_a_single_source_table) , and [deleting tables](/bigquery/docs/managing-tables#deleting_a_table)
  - [Exporting BigQuery data](/bigquery/docs/exporting-data) directly to Cloud Storage

## Troubleshooting connection pool errors

Error string: `  Connection pool is full, discarding connection: bigquery.googleapis.com. Connection pool size: 10  `

If you use the default BigQuery client object in Python, you are limited to a maximum of 10 threads because the default pool size for the [Python HTTPAdapter](https://docs.python-requests.org/en/latest/api/#requests.adapters.HTTPAdapter) is 10. To use more than 10 connections, create a custom `  requests.adapters.HTTPAdapter  ` object. For example:

``` text
client = bigquery.Client()
adapter = requests.adapters.HTTPAdapter(pool_connections=128,
pool_maxsize=128,max_retries=3)
client._http.mount("https://",adapter)
client._http._auth_request.session.mount("https://",adapter)
query_job = client.query(QUERY)
```
