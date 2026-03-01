# User-defined functions in Python

**Preview**

This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

**Note:** For support during the preview, email <bq-python-udf-feedback@google.com> .

A Python user-defined function (UDF) lets you implement a scalar function in Python and use it in a SQL query. Python UDFs are similar to [SQL and Javascript UDFs](/bigquery/docs/reference/standard-sql/user-defined-functions) , but with additional capabilities. Python UDFs let you install third-party libraries from [the Python Package Index (PyPI)](https://pypi.org/) and let you access external services using a [Cloud resource connection](/bigquery/docs/create-cloud-resource-connection) .

Python UDFs are built and run on BigQuery managed resources.

## Limitations

  - `  python-3.11  ` is the only supported runtime.
  - You cannot create a temporary Python UDF.
  - You cannot use a Python UDF with a materialized view.
  - The results of a query that calls a Python UDF are not cached because the return value of a Python UDF is always assumed to be non-deterministic.
  - Python UDFs are not fully supported in [`  INFORMATION_SCHEMA  `](/bigquery/docs/information-schema-intro) views.
  - You cannot create or update a Python UDF using the [Routine API](/bigquery/docs/reference/rest/v2/routines) .
  - [VPC service controls](/vpc-service-controls/docs/overview) are not supported.
  - [Customer-managed encryption keys (CMEK)](/kms/docs/cmek) are not supported.
  - These data types are not supported: `  JSON  ` , `  RANGE  ` , `  INTERVAL  ` , and `  GEOGRAPHY  ` .
  - Containers that run Python UDFs can be configured up to [2 vCpu and 8 Gi](#configure-container-limits) only.

## Required IAM roles

The required IAM roles are based on whether you are a Python UDF owner or a Python UDF user. A Python UDF owner typically creates or updates a UDF. A Python UDF user invokes a UDF created by someone else.

Additional roles are also required if you create or run a Python UDF that references a Cloud resource connection.

### UDF owners

If you're creating or updating a Python UDF, the following predefined IAM roles should be granted on the appropriate resource:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Role</th>
<th>Required permissions</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="/bigquery/docs/access-control#bigquery.dataEditor">BigQuery Data Editor</a> ( <code dir="ltr" translate="no">       roles/bigquery.dataEditor      </code> )</td>
<td><ul>
<li><code dir="ltr" translate="no">         bigquery.routines.create        </code> to create a Python UDF using the <code dir="ltr" translate="no">         CREATE FUNCTION        </code> statement.</li>
<li><code dir="ltr" translate="no">         bigquery.routines.update        </code> to update a Python UDF using the <code dir="ltr" translate="no">         CREATE FUNCTION        </code> statement.</li>
</ul></td>
<td>The dataset where the Python UDF is created or updated.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/access-control#bigquery.jobUser">BigQuery Job User</a> ( <code dir="ltr" translate="no">       roles/bigquery.jobUser      </code> )</td>
<td><ul>
<li><code dir="ltr" translate="no">         bigquery.jobs.create        </code> to run a <code dir="ltr" translate="no">         CREATE FUNCTION        </code> statement query job.</li>
</ul></td>
<td>The project where you're running the <code dir="ltr" translate="no">       CREATE FUNCTION      </code> statement.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/access-control#bigquery.connectionAdmin">BigQuery Connection Admin</a> ( <code dir="ltr" translate="no">       roles/bigquery.connectionAdmin      </code> )</td>
<td><ul>
<li><code dir="ltr" translate="no">         bigquery.connections.create        </code> is needed only to <a href="/bigquery/docs/create-cloud-resource-connection#create-cloud-resource-connection">create a new Cloud resource connection</a> .</li>
<li><code dir="ltr" translate="no">         bigquery.connections.delegate        </code> to use a connection in the <code dir="ltr" translate="no">         CREATE FUNCTION        </code> statement.</li>
</ul></td>
<td>The connection you're giving access to an external resource. This connection is required only if your UDF uses the <a href="#use-online-service"><code dir="ltr" translate="no">        WITH CONNECTION       </code></a> clause to access an external service.</td>
</tr>
</tbody>
</table>

### UDF users

If you're invoking a Python UDF, the following predefined IAM roles should be granted on the appropriate resource:

<table>
<thead>
<tr class="header">
<th>Role</th>
<th>Required permissions</th>
<th>Resource</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="/bigquery/docs/access-control#bigquery.user">BigQuery User</a> ( <code dir="ltr" translate="no">       roles/bigquery.user      </code> )</td>
<td><code dir="ltr" translate="no">       bigquery.jobs.create      </code> to run a query job that references the UDF.</td>
<td>The project where you're running a query job that invokes the Python UDF.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/access-control#bigquery.dataViewer">BigQuery Data Viewer</a> ( <code dir="ltr" translate="no">       roles/bigquery.dataViewer      </code> )</td>
<td><code dir="ltr" translate="no">       bigquery.routines.get      </code> to run a UDF created by someone else.</td>
<td>The dataset where the Python UDF is stored.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/access-control#bigquery.connectionUser">BigQuery Connection User</a> ( <code dir="ltr" translate="no">       roles/bigquery.connectionUser      </code> )</td>
<td><code dir="ltr" translate="no">       bigquery.connections.use      </code> to run a Python UDF that references a Cloud resource connection.</td>
<td>The Cloud resource connection referenced by the Python UDF. This connection is required only if your UDF references a connection.</td>
</tr>
</tbody>
</table>

For more information about roles in BigQuery, see [Predefined IAM roles](/bigquery/docs/access-control#bigquery) .

## Create a persistent Python UDF

Follow these rules when you create a Python UDF:

  - The body of the Python UDF must be a quoted string literal that represents the Python code. To learn more about quoted string literals, see [Formats for quoted literals](/bigquery/docs/reference/standard-sql/lexical#quoted_literals) .

  - The body of the Python UDF must include a Python function that is used in the `  entry_point  ` argument in the Python UDF options list.

  - A Python runtime version needs to be specified in the `  runtime_version  ` option. The only supported Python runtime version is `  python-3.11  ` . For a full list of available options, see the [Function option list](/bigquery/docs/reference/standard-sql/data-definition-language#function_option_list) for the `  CREATE FUNCTION  ` statement.

To create a persistent Python UDF, use the [`  CREATE FUNCTION  ` statement](/bigquery/docs/reference/standard-sql/data-definition-language#create_function_statement) without the `  TEMP  ` or `  TEMPORARY  ` keyword. To delete a persistent Python UDF, use the [`  DROP FUNCTION  `](/bigquery/docs/reference/standard-sql/data-definition-language#drop_function_statement) statement.

When you create a Python UDF using the `  CREATE FUNCTION  ` statement, BigQuery creates or updates a container image that is based on a base image. The container is built on the base image using your code and any specified package dependencies. Creating the container is a long-running process. The first query after you run the `  CREATE FUNCTION  ` statement might automatically wait for the image to complete. Without any external dependencies, the container image should typically be created in less than a minute.

### Example

To see an example of creating a persistent Python UDF, choose on of the following options:

### Console

The following example creates a persistent Python UDF named `  multiplyInputs  ` and calls the UDF from within a `  SELECT  ` statement:

1.  Go to the **BigQuery** page.

2.  In the query editor, enter the following `  CREATE FUNCTION  ` statement:
    
    ``` text
    CREATE FUNCTION `PROJECT_ID.DATASET_ID`.multiplyInputs(x FLOAT64, y FLOAT64)
    RETURNS FLOAT64
    LANGUAGE python
    OPTIONS(runtime_version="python-3.11", entry_point="multiply")
    AS r'''
    
    def multiply(x, y):
      return x * y
    
    ''';
    
    -- Call the Python UDF.
    WITH numbers AS
      (SELECT 1 AS x, 5 as y
      UNION ALL
      SELECT 2 AS x, 10 as y
      UNION ALL
      SELECT 3 as x, 15 as y)
    SELECT x, y,
    `PROJECT_ID.DATASET_ID`.multiplyInputs(x, y) AS product
    FROM numbers;
    ```
    
    Replace PROJECT\_ID . DATASET\_ID with your project ID and dataset ID.

3.  Click play\_circle\_filled **Run** .
    
    This example produces the following output:
    
    ``` text
    +-----+-----+--------------+
    | x   | y   | product      |
    +-----+-----+--------------+
    | 1   | 5   |  5.0         |
    | 2   | 10  | 20.0         |
    | 3   | 15  | 45.0         |
    +-----+-----+--------------+
    ```

### BigQuery DataFrames

The following example uses BigQuery DataFrames to turn a custom function into a Python UDF:

``` python
import bigframes.pandas as bpd

# Set BigQuery DataFrames options
bpd.options.bigquery.project = your_gcp_project_id
bpd.options.bigquery.location = "US"

# BigQuery DataFrames gives you the ability to turn your custom functions
# into a BigQuery Python UDF. One can find more details about the usage and
# the requirements via `help` command.
help(bpd.udf)

# Read a table and inspect the column of interest.
df = bpd.read_gbq("bigquery-public-data.ml_datasets.penguins")
df["body_mass_g"].peek(10)

# Define a custom function, and specify the intent to turn it into a
# BigQuery Python UDF. Let's try a `pandas`-like use case in which we want
# to apply a user defined function to every value in a `Series`, more
# specifically bucketize the `body_mass_g` value of the penguins, which is a
# real number, into a category, which is a string.
@bpd.udf(
    dataset=your_bq_dataset_id,
    name=your_bq_routine_id,
)
def get_bucket(num: float) -> str:
    if not num:
        return "NA"
    boundary = 4000
    return "at_or_above_4000" if num >= boundary else "below_4000"

# Then we can apply the udf on the `Series` of interest via
# `apply` API and store the result in a new column in the DataFrame.
df = df.assign(body_mass_bucket=df["body_mass_g"].apply(get_bucket))

# This will add a new column `body_mass_bucket` in the DataFrame. You can
# preview the original value and the bucketized value side by side.
df[["body_mass_g", "body_mass_bucket"]].peek(10)

# The above operation was possible by doing all the computation on the
# cloud through an underlying BigQuery Python UDF that was created to
# support the user's operations in the Python code.

# The BigQuery Python UDF created to support the BigQuery DataFrames
# udf can be located via a property `bigframes_bigquery_function`
# set in the udf object.
print(f"Created BQ Python UDF: {get_bucket.bigframes_bigquery_function}")

# If you have already defined a custom function in BigQuery, either via the
# BigQuery Google Cloud Console or with the `udf` decorator,
# or otherwise, you may use it with BigQuery DataFrames with the
# `read_gbq_function` method. More details are available via the `help`
# command.
help(bpd.read_gbq_function)

existing_get_bucket_bq_udf = get_bucket.bigframes_bigquery_function

# Here is an example of using `read_gbq_function` to load an existing
# BigQuery Python UDF.
df = bpd.read_gbq("bigquery-public-data.ml_datasets.penguins")
get_bucket_function = bpd.read_gbq_function(existing_get_bucket_bq_udf)

df = df.assign(body_mass_bucket=df["body_mass_g"].apply(get_bucket_function))
df.peek(10)

# Let's continue trying other potential use cases of udf. Let's say we
# consider the `species`, `island` and `sex` of the penguins sensitive
# information and want to redact that by replacing with their hash code
# instead. Let's define another scalar custom function and decorate it
# as a udf. The custom function in this example has external package
# dependency, which can be specified via `packages` parameter.
@bpd.udf(
    dataset=your_bq_dataset_id,
    name=your_bq_routine_id,
    packages=["cryptography"],
)
def get_hash(input: str) -> str:
    from cryptography.fernet import Fernet

    # handle missing value
    if input is None:
        input = ""

    key = Fernet.generate_key()
    f = Fernet(key)
    return f.encrypt(input.encode()).decode()

# We can use this udf in another `pandas`-like API `map` that
# can be applied on a DataFrame
df_redacted = df[["species", "island", "sex"]].map(get_hash)
df_redacted.peek(10)

# If the BigQuery routine is no longer needed, we can clean it up
# to free up any cloud quota
session = bpd.get_global_session()
session.bqclient.delete_routine(f"{your_bq_dataset_id}.{your_bq_routine_id}")
```

## Create a vectorized Python UDF

You can implement your Python UDF to process a batch of rows instead of a single row by using vectorization. Vectorization can improve query performance.

To control batching behavior, specify the maximum number of rows in each batch by using the `  max_batching_rows  ` option in the [`  CREATE OR REPLACE FUNCTION  ` option list](/bigquery/docs/reference/standard-sql/data-definition-language#function_option_list) . If you specify `  max_batching_rows  ` , BigQuery determines the number of rows in a batch, up to the `  max_batching_rows  ` limit. If `  max_batching_rows  ` is not specified, the number of rows to batch is determined automatically.

A vectorized Python UDF has a single [`  pandas.DataFrame  `](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.html) argument that must be annotated. The `  pandas.DataFrame  ` argument has the same number of columns as the Python UDF parameters defined in the `  CREATE FUNCTION  ` statement. The column names in the `  pandas.DataFrame  ` argument have the same names as the UDF's parameters.

Your function needs to return either a [`  pandas.Series  `](https://pandas.pydata.org/docs/reference/api/pandas.Series.html#pandas.Series) or a single-column `  pandas.DataFrame  ` with the same number of rows as the input.

The following example creates a vectorized Python UDF named `  multiplyInputs  ` with two parameters— `  x  ` and `  y  ` :

1.  Go to the **BigQuery** page.

2.  In the query editor, enter the following `  CREATE FUNCTION  ` statement:
    
    ``` text
    CREATE FUNCTION `PROJECT_ID.DATASET_ID`.multiplyVectorized(x FLOAT64, y FLOAT64)
    RETURNS FLOAT64
    LANGUAGE python
    OPTIONS(runtime_version="python-3.11", entry_point="vectorized_multiply")
    AS r'''
    import pandas as pd
    
    def vectorized_multiply(df: pd.DataFrame):
      return df['x'] * df['y']
    
    ''';
    ```
    
    Replace PROJECT\_ID . DATASET\_ID with your project ID and dataset ID.
    
    Calling the UDF is the same as in the previous example.

3.  Click play\_circle\_filled **Run** .

## Supported Python UDF data types

The following table defines the mapping between BigQuery data types, Python data types, and Pandas data types:

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>BigQuery data type</th>
<th>Python built-in data type used by standard UDF</th>
<th>Pandas data type used by vectorized UDF</th>
<th>PyArrow data type used for ARRAY and STRUCT in vectorized UDF</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       BOOL      </code></td>
<td><code dir="ltr" translate="no">       bool      </code></td>
<td><code dir="ltr" translate="no">       BooleanDtype      </code></td>
<td><code dir="ltr" translate="no">       DataType(bool)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       INT64      </code></td>
<td><code dir="ltr" translate="no">       int      </code></td>
<td><code dir="ltr" translate="no">       Int64Dtype      </code></td>
<td><code dir="ltr" translate="no">       DataType(int64)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
<td><code dir="ltr" translate="no">       float      </code></td>
<td><code dir="ltr" translate="no">       FloatDtype      </code></td>
<td><code dir="ltr" translate="no">       DataType(double)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       STRING      </code></td>
<td><code dir="ltr" translate="no">       str      </code></td>
<td><code dir="ltr" translate="no">       StringDtype      </code></td>
<td><code dir="ltr" translate="no">       DataType(string)      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       BYTES      </code></td>
<td><code dir="ltr" translate="no">       bytes      </code></td>
<td><code dir="ltr" translate="no">       binary[pyarrow]      </code></td>
<td><code dir="ltr" translate="no">       DataType(binary)      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       TIMESTAMP      </code></td>
<td><p>Function parameter: <code dir="ltr" translate="no">        datetime.datetime       </code> (with UTC timezone set)</p>
<p>Function return value: <code dir="ltr" translate="no">        datetime.datetime       </code> (with any timezone set)</p></td>
<td><p>Function parameter: <code dir="ltr" translate="no">        timestamp[us, tz=UTC][pyarrow]       </code></p>
<p>Function return value: <code dir="ltr" translate="no">        timestamp[us, tz=*][pyarrow]\(any timezone\)       </code></p></td>
<td><code dir="ltr" translate="no">       TimestampType(timestamp[us])      </code> , with timezone</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       DATE      </code></td>
<td><code dir="ltr" translate="no">       datetime.date      </code></td>
<td><code dir="ltr" translate="no">       date32[pyarrow]      </code></td>
<td><code dir="ltr" translate="no">       DataType(date32[day])      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       TIME      </code></td>
<td><code dir="ltr" translate="no">       datetime.time      </code></td>
<td><code dir="ltr" translate="no">       time64[pyarrow]      </code></td>
<td><code dir="ltr" translate="no">       Time64Type(time64[us])      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       DATETIME      </code></td>
<td><code dir="ltr" translate="no">       datetime.datetime      </code> (without timezone)</td>
<td><code dir="ltr" translate="no">       timestamp[us][pyarrow]      </code></td>
<td><code dir="ltr" translate="no">       TimestampType(timestamp[us])      </code> , without timezone</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       ARRAY      </code></td>
<td><code dir="ltr" translate="no">       list      </code></td>
<td><code dir="ltr" translate="no">       list&lt;...&gt;[pyarrow]      </code> , where the element data type is a <a href="https://pandas.pydata.org/docs/reference/api/pandas.ArrowDtype.html"><code dir="ltr" translate="no">        pandas.ArrowDtype       </code></a></td>
<td><code dir="ltr" translate="no">       ListType      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       STRUCT      </code></td>
<td><code dir="ltr" translate="no">       dict      </code></td>
<td><code dir="ltr" translate="no">       struct&lt;...&gt;[pyarrow]      </code> , where the field data type is a <a href="https://pandas.pydata.org/docs/reference/api/pandas.ArrowDtype.html"><code dir="ltr" translate="no">        pandas.ArrowDtype       </code></a></td>
<td><code dir="ltr" translate="no">       StructType      </code></td>
</tr>
</tbody>
</table>

## Supported runtime versions

BigQuery Python UDFs support the `  python-3.11  ` runtime. This Python version includes some additional pre-installed packages. For system libraries, check the runtime base image.

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Runtime version</th>
<th>Python version</th>
<th>Includes</th>
<th>Runtime base image</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>python-3.11</td>
<td>Python 3.11</td>
<td>numpy 1.26.3<br />
pyarrow 14.0.2<br />
pandas 2.1.4<br />
python-dateutil 2.8.2<br />
</td>
<td><a href="http://us-central1-docker.pkg.dev/serverless-runtimes/google-22-full/runtimes/python311">google-22-full/python311</a></td>
</tr>
</tbody>
</table>

## Use third-party packages

You can use the [`  CREATE FUNCTION  ` option list](/bigquery/docs/reference/standard-sql/data-definition-language#function_option_list) to use modules other than those provided by the [Python standard library](https://docs.python.org/3/library/index.html) and pre-installed packages. You can install packages from the [Python Package Index (PyPI)](https://pypi.org/) , or you can import Python files from Cloud Storage.

### Install a package from the Python package index

When you install a package, you must provide the package name, and you can optionally provide the package version using [Python package version specifiers](https://packaging.python.org/en/latest/specifications/version-specifiers) . If the package is in the runtime, that package is used unless a particular version is specified in the `  CREATE FUNCTION  ` option list. If a package version is not specified, and the package isn't in the runtime, the latest available version is used. Only packages with [the wheels binary format](https://peps.python.org/pep-0427) are supported.

The following example shows you how to create a Python UDF that installs the `  scipy  ` package using the `  CREATE OR REPLACE FUNCTION  ` option list:

1.  Go to the **BigQuery** page.

2.  In the query editor, enter the following `  CREATE FUNCTION  ` statement:
    
    ``` text
    CREATE FUNCTION `PROJECT_ID.DATASET_ID`.area(radius FLOAT64)
    RETURNS FLOAT64 LANGUAGE python
    OPTIONS (entry_point='area_handler', runtime_version='python-3.11', packages=['scipy==1.15.3'])
    AS r"""
    import scipy
    
    def area_handler(radius):
      return scipy.constants.pi*radius*radius
    """;
    
    SELECT `PROJECT_ID.DATASET_ID`.area(4.5);
    ```
    
    Replace PROJECT\_ID . DATASET\_ID with your project ID and dataset ID.

3.  Click play\_circle\_filled **Run** .

### Import additional Python files as libraries

You can extend your Python UDFs using the [Function option list](/bigquery/docs/reference/standard-sql/data-definition-language#function_option_list) by importing Python files from Cloud Storage.

**Note:** The user that creates the UDF needs the [`  storage.objects.get  `](/storage/docs/access-control/iam-permissions#objects) permission on the Cloud Storage bucket.

In your UDF's Python code, you can import the Python files from Cloud Storage as modules by using the import statement followed by the path to the Cloud Storage object. For example, if you are importing `  gs://BUCKET_NAME/path/to/lib1.py  ` , then your import statement would be `  import path.to.lib1  ` .

The Python filename needs to be a Python identifier. Each `  folder  ` name in the object name (after the `  /  ` ) should be a valid Python identifier. Within the ASCII range (U+0001..U+007F), the following characters can be used in identifiers:

  - Uppercase and lowercase letters A through Z.
  - Underscores.
  - The digits zero through nine, but a number cannot appear as the first character in the identifier.

The following example shows you how to create a Python UDF that imports the `  lib1.py  ` client library package from a Cloud Storage bucket named `  my_bucket  ` :

1.  Go to the **BigQuery** page.

2.  In the query editor, enter the following `  CREATE FUNCTION  ` statement:
    
    ``` text
    CREATE FUNCTION `PROJECT_ID.DATASET_ID`.myFunc(a FLOAT64, b STRING)
    RETURNS STRING LANGUAGE python
    OPTIONS (
    entry_point='compute', runtime_version='python-3.11',
    library=['gs://my_bucket/path/to/lib1.py'])
    AS r"""
    import path.to.lib1 as lib1
    
    def compute(a, b):
      # doInterestingStuff is a function defined in
      # gs://my_bucket/path/to/lib1.py
      return lib1.doInterestingStuff(a, b);
    
    """;
    ```
    
    Replace PROJECT\_ID . DATASET\_ID with your project ID and dataset ID.

3.  Click play\_circle\_filled **Run** .

## Configure container limits for Python UDFs

You can use the [`  CREATE FUNCTION  ` option list](/bigquery/docs/reference/standard-sql/data-definition-language#function_option_list) to specify CPU and memory limits for containers that run Python UDFs.

By default, the memory allocated to each container instance is 512 MiB, and the CPU allocated is 1.0 vCPU.

The following example creates a Python UDF using the `  CREATE FUNCTION  ` option list to specify container limits:

1.  Go to the **BigQuery** page.

2.  In the query editor, enter the following `  CREATE FUNCTION  ` statement:
    
    ``` text
    CREATE FUNCTION `PROJECT_ID.DATASET_ID`.resizeImage(image BYTES)
    RETURNS BYTES LANGUAGE python
    OPTIONS (entry_point='resize_image', runtime_version='python-3.11',
    packages=['Pillow==11.2.1'], container_memory='2Gi', container_cpu=1)
    AS r"""
    import io
    from PIL import Image
    
    def resize_image(image_bytes):
      img = Image.open(io.BytesIO(image_bytes))
    
      resized_img = img.resize((256, 256), Image.Resampling.LANCZOS)
      output_stream = io.BytesIO()
      resized_img.convert('RGB').save(output_stream, format='JPEG')
      return output_stream.getvalue()
    """;
    ```
    
    Replace PROJECT\_ID . DATASET\_ID with your project ID and dataset ID.

3.  Click play\_circle\_filled **Run** .

### Supported CPU values

Python UDFs support fractional CPU values between `  0.33  ` and `  1.0  ` and non-fractional CPU values of `  1  ` , `  2  ` . Fractional input values are rounded to two decimal places before they are applied to the container.

### Supported Memory Values

Python UDF containers support memory values in the following format: `  <integer_number><unit>  ` . The unit must be one of these values: `  Mi  ` , `  M  ` , `  Gi  ` , `  G  ` . The minimum amount of memory you can configure is 256 Mebibyte (256 Mi). The maximum amount of memory you can configure is 8 Gibibyte (8 Gi).

Based on the memory value you choose, you must also specify the minimum amount of CPU. The following table shows the minimum CPU values for each memory value:

<table>
<thead>
<tr class="header">
<th>Memory</th>
<th>Minimum CPU</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       512 MiB or less      </code></td>
<td><code dir="ltr" translate="no">       0.33      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       More than 512 MiB      </code></td>
<td><code dir="ltr" translate="no">       0.5      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       More than 1 GiB      </code></td>
<td><code dir="ltr" translate="no">       1      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       More than 4 GiB      </code></td>
<td><code dir="ltr" translate="no">       2      </code></td>
</tr>
</tbody>
</table>

## Call Google Cloud or online services in Python code

A Python UDF accesses a Google Cloud service or an external service by using the [Cloud resource connection](/bigquery/docs/create-cloud-resource-connection) service account. The connection's service account must be granted permissions to access the service. The permissions required vary depending on the service that is accessed and the APIs that are called from your Python code.

If you create a Python UDF without using a Cloud resource connection, the function is executed in an environment that blocks network access. If your UDF accesses online services, you must create the UDF with a Cloud resource connection. If you don't, the UDF is blocked from accessing the network until an internal connection timeout is reached.

The following example shows you how to access the Cloud Translation service from a Python UDF. This example has two projects—a project named `  my_query_project  ` where you create the UDF and the Cloud resource connection, and a project where you are running the Cloud Translation named `  my_translate_project  ` .

### Create a Cloud resource connection

First, you create a Cloud resource connection in `  my_query_project  ` . To create the cloud resource connection, follow the steps on the [Create a Cloud resource connection](/bigquery/docs/create-cloud-resource-connection#create-cloud-resource-connection) page.

After you create the connection, open it, and in the **Connection info** pane, copy the service account ID. You need this ID when you configure permissions for the connection. When you create a connection resource, BigQuery creates a unique system service account and associates it with the connection.

### Grant access to the connection's service account

To grant the Cloud resource connection service account access to your projects, grant the service account the [Service usage consumer role](/service-usage/docs/access-control#serviceusage.serviceUsageConsumer) ( `  roles/serviceusage.serviceUsageConsumer  ` ) in `  my_query_project  ` and the [Cloud Translation API user role](/translate/docs/access-control#cloudtranslate.user) ( `  roles/cloudtranslate.user  ` ) in `  my_translate_project  ` .

1.  Go to the **IAM** page.

2.  Verify that `  my_query_project  ` is selected.

3.  Click person\_add **Grant Access** .

4.  In the **New principals** field, enter the Cloud resource connection's service account ID that you copied previously.

5.  In the **Select a role** field, choose **Service usage** , and then select **Service usage consumer** .

6.  Click **Save** .

7.  In the project selector, choose **`  my_translate_project  `** .

8.  Go to the **IAM** page.

9.  Click person\_add **Grant Access** .

10. In the **New principals** field, enter the Cloud resource connection's service account ID that you copied previously.

11. In the **Select a role** field, choose **Cloud translation** , and then select **Cloud Translation API user** .

12. Click **Save** .

### Create a Python UDF that calls the Cloud Translation service

In `  my_query_project  ` , create a Python UDF that calls the Cloud Translation service using your Cloud resource connection.

1.  Go to the **BigQuery** page.

2.  Enter the following `  CREATE FUNCTION  ` statement in the query editor:
    
    ``` text
    CREATE FUNCTION `PROJECT_ID.DATASET_ID`.translate_to_es(x STRING)
    RETURNS STRING LANGUAGE python
    WITH CONNECTION `PROJECT_ID.REGION.CONNECTION_ID`
    OPTIONS (entry_point='do_translate', runtime_version='python-3.11', packages=['google-cloud-translate>=3.11', 'google-api-core'])
    AS r"""
    
    from google.api_core.retry import Retry
    from google.cloud import translate
    
    project = "my_translate_project"
    translate_client = translate.TranslationServiceClient()
    
    def do_translate(x : str) -> str:
    
        response = translate_client.translate_text(
            request={
                "parent": f"projects/{project}/locations/us-central1",
                "contents": [x],
                "target_language_code": "es",
                "mime_type": "text/plain",
            },
            retry=Retry(),
        )
        return response.translations[0].translated_text
    
    """;
    
    -- Call the UDF.
    WITH text_table AS
      (SELECT "Hello" AS text
      UNION ALL
      SELECT "Good morning" AS text
      UNION ALL
      SELECT "Goodbye" AS text)
    SELECT text,
    `PROJECT_ID.DATASET_ID`.translate_to_es(text) AS translated_text
    FROM text_table;
    ```
    
    Replace the following:
    
      - `  PROJECT_ID . DATASET_ID  ` : your project ID and dataset ID
      - `  REGION . CONNECTION_ID  ` : your connection's region and connection ID

3.  Click play\_circle\_filled **Run** .
    
    The output should look like the following:
    
    ``` text
    +--------------------------+-------------------------------+
    | text                     | translated_text               |
    +--------------------------+-------------------------------+
    | Hello                    | Hola                          |
    | Good morning             | Buen dia                      |
    | Goodbye                  | Adios                         |
    +--------------------------+-------------------------------+
    ```

## Supported locations

Python UDFs are supported in all BigQuery [multi-region and regional locations](/bigquery/docs/locations) .

## Pricing

Python UDFs are offered without any additional charges.

When billing is enabled, the following apply:

  - Python UDF charges are billed using the [BigQuery Services SKU](https://cloud.google.com/skus?&filter=bigquery&currency=USD) .
  - The charges are proportional to the amount of compute and memory consumed when the Python UDF is invoked.
  - Python UDF customers are also charged for the cost of building or rebuilding the UDF container image. This charge is proportional to the resources used to build the image with customer code and dependencies.
  - If Python UDFs result in external or internet network egress, you also see a [Premium Tier](https://cloud.google.com/network-tiers/pricing) internet egress charge from Cloud Networking.
