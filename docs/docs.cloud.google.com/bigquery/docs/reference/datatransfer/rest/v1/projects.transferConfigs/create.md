  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Query parameters](#body.QUERY_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
  - [Authorization scopes](#body.aspect)
  - [Try it\!](#try-it)

**Full name** : projects.transferConfigs.create

Creates a new data transfer configuration.

### HTTP request

`  POST https://bigquerydatatransfer.googleapis.com/v1/{parent=projects/*}/transferConfigs  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  parent  `

`  string  `

Required. The BigQuery project id where the transfer configuration should be created. Must be in the format projects/{projectId}/locations/{locationId} or projects/{projectId}. If specified location and location of the destination bigquery dataset do not match - the request will fail.

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  parent  ` :

  - `  bigquery.transfers.update  `

### Query parameters

Parameters

`  authorizationCode (deprecated)  `

`  string  `

Deprecated: Authorization code was required when `  transferConfig.dataSourceId  ` is 'youtube\_channel' but it is no longer used in any data sources. Use `  versionInfo  ` instead.

Optional OAuth2 authorization code to use with this transfer configuration. This is required only if `  transferConfig.dataSourceId  ` is 'youtube\_channel' and new credentials are needed, as indicated by `  dataSources.checkValidCreds  ` . In order to obtain authorizationCode, make a request to the following URL:

``` text
https://bigquery.cloud.google.com/datatransfer/oauthz/auth?redirect_uri=urn:ietf:wg:oauth:2.0:oob&response_type=authorization_code&client_id=clientId&scope=data_source_scopes
```

  - The clientId is the OAuth clientId of the data source as returned by dataSources.list method.
  - data\_source\_scopes are the scopes returned by dataSources.list method.

Note that this should not be set when `  serviceAccountName  ` is used to create the transfer config.

`  versionInfo  `

`  string  `

Optional version info. This parameter replaces `  authorizationCode  ` which is no longer used in any data sources. This is required only if `  transferConfig.dataSourceId  ` is 'youtube\_channel' *or* new credentials are needed, as indicated by `  dataSources.checkValidCreds  ` . In order to obtain version info, make a request to the following URL:

``` text
https://bigquery.cloud.google.com/datatransfer/oauthz/auth?redirect_uri=urn:ietf:wg:oauth:2.0:oob&response_type=version_info&client_id=clientId&scope=data_source_scopes
```

  - The clientId is the OAuth clientId of the data source as returned by dataSources.list method.
  - data\_source\_scopes are the scopes returned by dataSources.list method.

Note that this should not be set when `  serviceAccountName  ` is used to create the transfer config.

`  serviceAccountName  `

`  string  `

Optional service account email. If this field is set, the transfer config will be created with this service account's credentials. It requires that the requesting user calling this API has permissions to act as this service account.

Note that not all data sources support service account credentials when creating a transfer config. For the latest list of data sources, read about [using service accounts](https://cloud.google.com/bigquery-transfer/docs/use-service-accounts) .

### Request body

The request body contains an instance of `  TransferConfig  ` .

### Response body

If successful, the response body contains a newly created instance of `  TransferConfig  ` .

### Authorization scopes

Requires the following OAuth scope:

  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
