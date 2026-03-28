  - [HTTP request](#body.HTTP_TEMPLATE)
  - [Path parameters](#body.PATH_PARAMETERS)
  - [Request body](#body.request_body)
  - [Response body](#body.response_body)
  - [Authorization scopes](#body.aspect)
  - [Try it\!](#try-it)

**Full name** : projects.locations.transferConfigs.transferResources.get

Returns a transfer resource.

### HTTP request

`  GET https://bigquerydatatransfer.googleapis.com/v1/{name=projects/*/locations/*/transferConfigs/*/transferResources/*}  `

The URL uses [gRPC Transcoding](https://google.aip.dev/127) syntax.

### Path parameters

Parameters

`  name  `

`  string  `

Required. The name of the transfer resource in the form of:

  - `  projects/{project}/transferConfigs/{transferConfig}/transferResources/{transferResource}  `
  - `  projects/{project}/locations/{location}/transferConfigs/{transferConfig}/transferResources/{transferResource}  `

Authorization requires the following [IAM](https://cloud.google.com/iam/docs/) permission on the specified resource `  name  ` :

  - `  bigquery.transfers.get  `

### Request body

The request body must be empty.

### Response body

If successful, the response body contains an instance of `  TransferResource  ` .

### Authorization scopes

Requires the following OAuth scope:

  - `  https://www.googleapis.com/auth/cloud-platform  `

For more information, see the [Authentication Overview](/docs/authentication#authorization-gcp) .
