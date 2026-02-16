**Preview**

This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://cloud.google.com/terms/service-terms) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products#product-launch-stages) .

**Note:** To provide feedback or request support for this feature, send an email to <bq-objectref-feedback@google.com> .

GoogleSQL for BigQuery supports the following ObjectRef functions.

This topic includes functions that let you create and interact with [`  ObjectRef  `](/bigquery/docs/reference/standard-sql/objectref_functions#objectref) and [`  ObjectRefRuntime  `](/bigquery/docs/reference/standard-sql/objectref_functions#objectrefruntime) values.

## Function list

<table>
<thead>
<tr class="header">
<th>Name</th>
<th>Summary</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/objectref_functions#objfetch_metadata"><code dir="ltr" translate="no">        OBJ.FETCH_METADATA       </code></a></td>
<td>Fetches Cloud Storage metadata for a partially populated <code dir="ltr" translate="no">       ObjectRef      </code> value.</td>
</tr>
<tr class="even">
<td><a href="/bigquery/docs/reference/standard-sql/objectref_functions#objget_access_url"><code dir="ltr" translate="no">        OBJ.GET_ACCESS_URL       </code></a></td>
<td>Returns access URLs for a Cloud Storage object.</td>
</tr>
<tr class="odd">
<td><a href="/bigquery/docs/reference/standard-sql/objectref_functions#objmake_ref"><code dir="ltr" translate="no">        OBJ.MAKE_REF       </code></a></td>
<td>Creates an <code dir="ltr" translate="no">       ObjectRef      </code> value that contains reference information for a Cloud Storage object.</td>
</tr>
</tbody>
</table>

## `     OBJ.FETCH_METADATA    `

**Preview**

This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://cloud.google.com/terms/service-terms) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products#product-launch-stages) .

**Note:** To provide feedback or request support for this feature, send an email to <bq-objectref-feedback@google.com> .

``` text
OBJ.FETCH_METADATA(
  objectref
)
```

**Description**

The `  OBJ.FETCH_METADATA  ` function returns Cloud Storage metadata for a partially populated [`  ObjectRef  `](/bigquery/docs/reference/standard-sql/objectref_functions#objectref) value.

To fetch object metadata, you must have the `  bigquery.objectRefs.read  ` permission on the Cloud resource connection specified in the `  authorizer  ` field of the input `  ObjectRef  ` value. You can get this permission from the [BigQuery ObjectRef Reader ( `  roles/bigquery.objectRefReader  ` )](/bigquery/docs/access-control#bigquery.objectRefReader) or [BigQuery ObjectRef Admin ( `  roles/bigquery.objectRefAdmin  ` )](/bigquery/docs/access-control#bigquery.objectRefAdmin) role.

This function still succeeds if there is a problem fetching metadata. In this case, the `  details  ` field contains an `  error  ` field with the error message, as shown in the following example:

``` text
{
  "details": {
    "errors":{
      "OBJ.FETCH_METADATA":"Connection credential for projects/myproject/locations/us/connections/connection1 cannot be used. Either the connection does not exist, or the user does not have sufficient permissions to use it."
    }
  }
}
```

**Definitions**

  - `  objectref  ` : A partially populated `  ObjectRef  ` value, in which the `  uri  ` and `  authorizer  ` fields are populated and the `  details  ` field isn't.

**Output**

A fully populated `  ObjectRef  ` value. The metadata is provided in the `  details  ` field of the returned `  ObjectRef  ` value.

**Example**

This example returns the metadata for a JPG object.

``` text
SELECT OBJ.FETCH_METADATA(OBJ.MAKE_REF("gs://mybucket/path/to/file.jpg", "us.connection1"));
```

## `     OBJ.GET_ACCESS_URL    `

**Preview**

This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://cloud.google.com/terms/service-terms) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products#product-launch-stages) .

**Note:** To provide feedback or request support for this feature, send an email to <bq-objectref-feedback@google.com> .

``` text
OBJ.GET_ACCESS_URL(
  objectref,
  mode
  [, duration]
)
```

**Description**

The `  OBJ.GET_ACCESS_URL  ` function returns JSON that contains reference information for the input [`  ObjectRef  `](/bigquery/docs/reference/standard-sql/objectref_functions#objectref) value, and also access URLs that you can use to read or modify the Cloud Storage object.

To create a URL to read the object, you must have the `  bigquery.objectRefs.read  ` permission on the Cloud resource connection specified in the `  authorizer  ` field of the input `  ObjectRef  ` value. You can get this permission from the [BigQuery ObjectRef Reader ( `  roles/bigquery.objectRefReader  ` )](/bigquery/docs/access-control#bigquery.objectRefReader) or [BigQuery ObjectRef Admin ( `  roles/bigquery.objectRefAdmin  ` )](/bigquery/docs/access-control#bigquery.objectRefAdmin) role.

To create a URL to modify the object, you must have the `  bigquery.objectRefs.write  ` permission on the Cloud resource connection specified in the `  authorizer  ` field of the input `  ObjectRef  ` value. You can get this permission from the [BigQuery ObjectRef Admin ( `  roles/bigquery.objectRefAdmin  ` ) role](/bigquery/docs/access-control#bigquery.objectRefAdmin) .

If the function encounters an error, the returned JSON contains a `  runtime_errors  ` field with the error message instead of the `  access_urls  ` field with the access URLs. This is shown in the following example:

``` text
{
  "objectref": {
    "authorizer": "myproject.us.connection1",
    "uri": "gs://mybucket/path/to/file.jpg"
  },
  "runtime_errors": {
    "OBJ.GET_ACCESS_URL": "Connection credential for projects/myproject/locations/us/connections/connection1 cannot be used. Either the connection does not exist, or the user does not have sufficient permissions to use it."
  }
}
```

**Definitions**

  - `  objectref  ` : An `  ObjectRef  ` value that represents a Cloud Storage object.

  - `  mode  ` : A `  STRING  ` value that identifies the type of URL that you want to be returned. The following values are supported:
    
      - `  r  ` : Returns a URL that lets you read the object.
      - `  rw  ` : Returns two URLs, one that lets you read the object, and one that lets you modify the object.

  - `  duration  ` : An optional [`  INTERVAL  `](/bigquery/docs/reference/standard-sql/data-types#interval_type) value that specifies how long the generated access URLs remain valid. You can specify a value between 30 minutes and 6 hours. For example, you could specify `  INTERVAL 2 HOUR  ` to generate URLs that expire after 2 hours. The default value is 6 hours.

**Output**

A JSON value that contains the Cloud Storage object reference information from the input `  ObjectRef  ` value, and also one or more URLs that you can use to access the Cloud Storage object.

The JSON output is returned in the `  ObjectRefRuntime  ` schema:

``` text
obj_ref_runtime json {
  obj_ref json {
    uri string, // Cloud Storage object URI
    version string, // Cloud Storage object version
    authorizer string, // Cloud resource connection to use for object access
    details json { // Cloud Storage managed object metadata
      gcs_metadata json {
      }
    }
  }
  access_urls json {
    read_url string, // read-only signed url
    write_url string, // writeable signed url
    expiry_time string // the URL expiration time in YYYY-MM-DD'T'HH:MM:SS'Z' format
  }
}
```

**Example**

This example returns read URLs for all of the image objects associated with the films in the `  mydataset.films  ` table, where the `  poster  ` column is a struct in the `  ObjectRef  ` schema. The URLs expire in 45 minutes.

``` text
SELECT
  OBJ.GET_ACCESS_URL(poster, 'r', INTERVAL 45 MINUTE) AS read_url
FROM mydataset.films;
```

## `     OBJ.MAKE_REF    `

**Preview**

This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://cloud.google.com/terms/service-terms) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products#product-launch-stages) .

**Note:** To provide feedback or request support for this feature, send an email to <bq-objectref-feedback@google.com> .

``` text
OBJ.MAKE_REF(
  uri,
  authorizer
)
```

``` text
OBJ.MAKE_REF(
  objectref_json
)
```

**Description**

Use the `  OBJ.MAKE_REF  ` function to create an [`  ObjectRef  `](/bigquery/docs/reference/standard-sql/objectref_functions#objectref) value that contains reference information for a Cloud Storage object. You can use this function in workflows similar to the following:

1.  Transform an object.
2.  Save it to Cloud Storage using a writable signed URL that you created by using the [`  OBJ.GET_ACCESS_URL  ` function](/bigquery/docs/reference/standard-sql/objectref_functions#objget_access_url) .
3.  Create an `  ObjectRef  ` value for the transformation output by using the `  OBJ.MAKE_REF  ` function
4.  Save the `  ObjectRef  ` value by writing it to a table column.

**Definitions**

  - `  uri  ` : A `  STRING  ` value that contains the URI for the Cloud Storage object, for example, `  gs://mybucket/flowers/12345.jpg  ` . You can also specify a column name in place of a string literal. For example, if you have URI data in a `  uri  ` field, you can specify `  OBJ.MAKE_REF(uri, "myproject.us.conn")  ` .

  - `  authorizer  ` : A `  STRING  ` value that contains the [Cloud Resource connection](/bigquery/docs/create-cloud-resource-connection) used to access the Cloud Storage object. To read or write using ObjectRef returned from this function, the connection's service account must have the following roles on the Cloud Storage bucket that stores the object:
    
      - Storage Object User ( `  roles/storage.objectUser  ` ) for reads and writes
      - Storage Object Viewer ( `  roles/storage.objectViewer  ` ) for reads
    
    The `  authorizer  ` value must be in the format `  location.connection_id  ` . For example, `  use-west1.myconnection  ` . You can get the connection ID or service account by [viewing the connection details](/bigquery/docs/working-with-connections#view-connections) in the Cloud console. You can copy the value in the last section of the fully qualified connection ID that is shown in **Connection ID** . For example, `  projects/myproject/locations/connection_location/connections/ myconnection  ` .
    
    The connection must be in the same project and region as the query where you are calling the function.

  - `  objectref_json  ` : A `  JSON  ` value that represents a Cloud Storage object, using the following schema:
    
    ``` text
    obj_ref json {
      uri string,
      authorizer string
    }
    ```

No validations are performed on the input values.

**Output**

An `  ObjectRef  ` value.

An `  ObjectRef  ` value represents a Cloud Storage object, including the object URI, size, type, and similar metadata. It also contains an authorizer, which identifies the [Cloud resource connection](/bigquery/docs/create-cloud-resource-connection) to use to access the Cloud Storage object from BigQuery. An `  ObjectRef  ` value is a struct in the following format:

``` text
struct {
  uri string,  // Cloud Storage object URI
  version string,  // Cloud Storage object version
  authorizer string,  // Cloud resource connection to use for object access
  details json {  // Cloud Storage managed object metadata
    gcs_metadata json {
      "content_type": string,  // for example, "image/png"
      "md5_hash": string,  // for example, "d9c38814e44028bf7a012131941d5631"
      "size": number,  // for example, 23000
      "updated": number  // for example, 1741374857000000
    }
  }
}
```

When you use the `  uri  ` and `  authorizer  ` arguments as input, the output `  ObjectRef  ` value contains a reference to a Cloud Storage object. When you use the `  objectref_json  ` argument as input, the output `  ObjectRef  ` value contains a struct that is equivalent to the input JSON value.

**Examples**

This example creates an `  ObjectRef  ` value using a URI and a Cloud resource connection as input:

``` text
CREATE OR REPLACE TABLE `mydataset.movies` AS (
  SELECT
    f.title,
    f.director
    OBJ.MAKE_REF(p.uri, 'asia-south2.storage_connection') AS movie_poster
  FROM mydataset.movie_posters p
  join mydataset.films f
  using(title)
  where region = 'US'
  and release_year = 2024
);
```

This example creates an `  ObjectRef  ` value using JSON input:

``` text
OBJ.MAKE_REF(JSON '{"uri": "gs://mybucket/flowers/12345.jpg", "authorizer": "asia-south2.storage_connection"}');
```

**Limitations**

You can't have more than 20 connections in the project where you are running queries that reference `  ObjectRef  ` or `  ObjectRefRuntime  ` values.
