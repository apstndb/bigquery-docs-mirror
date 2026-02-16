  - [JSON representation](#SCHEMA_REPRESENTATION)

Represents request of PolicyCallback.GetResourceInfo method.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th>JSON representation</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><pre class="text" dir="ltr" data-is-upgraded="" style="border: 0;margin: 0;" translate="no"><code>{
  &quot;resourceService&quot;: string,
  &quot;resourceName&quot;: string,
  &quot;fields&quot;: string,
  &quot;rpcRequestMessage&quot;: {
    &quot;@type&quot;: string,
    field1: ...,
    ...
  }
}</code></pre></td>
</tr>
</tbody>
</table>

Fields

`  resourceService  `

`  string  `

REQUIRED: The name of the service that this resource belongs to, such as `  pubsub.googleapis.com  ` . The service may be different from the DNS hostname that actually serves the request.

`  resourceName  `

`  string  `

REQUIRED: The stable identifier (name) of a resource on the `  resourceService  ` . A resource can be logically identified as "//{resourceService}/{resourceName}". The differences between a resource name and a URI are:

  - Resource name is a logical identifier, independent of network protocol and API version. For example, `  //pubsub.googleapis.com/projects/123/topics/news-feed  ` .
  - URI often includes protocol and version information, so it can be used directly by applications. For example, `  https://pubsub.googleapis.com/v1/projects/123/topics/news-feed  ` .

See <https://cloud.google.com/apis/design/resource_names> for details.

`  fields  `

`  string ( FieldMask  ` format)

OPTIONAL: field mask indicating which response parameters to return.

This is a comma-separated list of fully qualified names of fields. Example: `  "user.displayName,photo"  ` .

`  rpcRequestMessage  `

`  object  `

OPTIONAL: The rpc request message in generic format. It contains additional information to be used to create the resource needed by IAM/CAL. Please contact cloud-policy-enforcement@ before use.

An object containing fields of an arbitrary type. An additional field `  "@type"  ` contains a URI identifying the type. Example: `  { "id": 1234, "@type": "types.example.com/standard/id" }  ` .
