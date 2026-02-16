This page shows how to get started with the Cloud Client Libraries for the BigQuery Connection API. Client libraries make it easier to access Google Cloud APIs from a supported language. Although you can use Google Cloud APIs directly by making raw requests to the server, client libraries provide simplifications that significantly reduce the amount of code you need to write.

Read more about the Cloud Client Libraries and the older Google API Client Libraries in [Client libraries explained](/apis/docs/client-libraries-explained) .

**Beta**

This library is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA libraries are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

## Install the client library

### C\#

``` text
Install-Package Google.Cloud.BigQuery.Connection.V1 -Pre
```

For more information, see [Setting Up a C\# Development Environment](/dotnet/docs/setup) .

### Go

``` text
go get cloud.google.com/go/bigquery
```

For more information, see [Setting Up a Go Development Environment](/go/docs/setup) .

### Java

If you are using [Maven](https://maven.apache.org/) , add the following to your `  pom.xml  ` file. For more information about BOMs, see [The Google Cloud Platform Libraries BOM](https://cloud.google.com/java/docs/bom) .

``` markdown
<dependency>
  <groupId>com.google.cloud</groupId>
  <artifactId>google-cloud-bigqueryconnection</artifactId>
  <version>2.5.6</version>
</dependency>
```

If you are using [Gradle](https://gradle.org/) , add the following to your dependencies:

``` markdown
implementation 'com.google.cloud:google-cloud-bigqueryconnection:2.20.0'
```

If you are using [sbt](https://www.scala-sbt.org/) , add the following to your dependencies:

``` markdown
libraryDependencies += "com.google.cloud" % "google-cloud-bigqueryconnection" % "2.20.0"
```

If you're using Visual Studio Code or IntelliJ, you can add client libraries to your project using the following IDE plugins:

  - [Cloud Code for VS Code](/code/docs/vscode/client-libraries)
  - [Cloud Code for IntelliJ](/code/docs/intellij/client-libraries)

The plugins provide additional functionality, such as key management for service accounts. Refer to each plugin's documentation for details.

**Note:** Cloud Java client libraries do not currently support Android.

For more information, see [Setting Up a Java Development Environment](/java/docs/setup) .

### Node.js

``` text
npm install @google-cloud/bigquery-connection
```

For more information, see [Setting Up a Node.js Development Environment](/nodejs/docs/setup) .

### PHP

``` text
composer require google/cloud-bigquery-connection
```

For more information, see [Using PHP on Google Cloud](/php/docs) .

### Python

``` text
pip install --upgrade google-cloud-bigquery-connection
```

For more information, see [Setting Up a Python Development Environment](/python/docs/setup) .

### Ruby

``` text
gem install google-cloud-bigquery-connection
```

For more information, see [Setting Up a Ruby Development Environment](/ruby/docs/setup) .

## Set up authentication

To authenticate calls to Google Cloud APIs, client libraries support [Application Default Credentials (ADC)](/docs/authentication/application-default-credentials) ; the libraries look for credentials in a set of defined locations and use those credentials to authenticate requests to the API. With ADC, you can make credentials available to your application in a variety of environments, such as local development or production, without needing to modify your application code.

For production environments, the way you set up ADC depends on the service and context. For more information, see [Set up Application Default Credentials](/docs/authentication/provide-credentials-adc) .

For a local development environment, you can set up ADC with the credentials that are associated with your Google Account:

1.  [Install](/sdk/docs/install) the Google Cloud CLI. After installation, [initialize](/sdk/docs/initializing) the Google Cloud CLI by running the following command:
    
    ``` text
    gcloud init
    ```
    
    If you're using an external identity provider (IdP), you must first [sign in to the gcloud CLI with your federated identity](/iam/docs/workforce-log-in-gcloud) .

2.  If you're using a local shell, then create local authentication credentials for your user account:
    
    ``` text
    gcloud auth application-default login
    ```
    
    You don't need to do this if you're using Cloud Shell.
    
    If an authentication error is returned, and you are using an external identity provider (IdP), confirm that you have [signed in to the gcloud CLI with your federated identity](/iam/docs/workforce-log-in-gcloud) .
    
    A sign-in screen appears. After you sign in, your credentials are stored in the [local credential file used by ADC](/docs/authentication/application-default-credentials#personal) .

## Use the client library

The following example demonstrates some basic interactions with the BigQuery Connection API.

### Go

``` go
// The bigquery_connection_quickstart application demonstrates basic usage of the
// BigQuery connection API.
package main

import (
 "bytes"
 "context"
 "flag"
 "fmt"
 "log"
 "time"

 connection "cloud.google.com/go/bigquery/connection/apiv1"
 "cloud.google.com/go/bigquery/connection/apiv1/connectionpb"
 "google.golang.org/api/iterator"
)

func main() {

 // Define two command line flags for controlling the behavior of this quickstart.
 projectID := flag.String("project_id", "", "Cloud Project ID, used for session creation.")
 location := flag.String("location", "US", "BigQuery location used for interactions.")

 // Parse flags and do some minimal validation.
 flag.Parse()
 if *projectID == "" {
     log.Fatal("empty --project_id specified, please provide a valid project ID")
 }
 if *location == "" {
     log.Fatal("empty --location specified, please provide a valid location")
 }

 ctx := context.Background()
 connClient, err := connection.NewClient(ctx)
 if err != nil {
     log.Fatalf("NewClient: %v", err)
 }
 defer connClient.Close()

 s, err := reportConnections(ctx, connClient, *projectID, *location)
 if err != nil {
     log.Fatalf("printCapacityCommitments: %v", err)
 }
 fmt.Println(s)
}

// reportConnections gathers basic information about existing connections in a given project and location.
func reportConnections(ctx context.Context, client *connection.Client, projectID, location string) (string, error) {
 var buf bytes.Buffer
 fmt.Fprintf(&buf, "Current connections defined in project %s in location %s:\n", projectID, location)

 req := &connectionpb.ListConnectionsRequest{
     Parent: fmt.Sprintf("projects/%s/locations/%s", projectID, location),
 }
 totalConnections := 0
 it := client.ListConnections(ctx, req)
 for {
     conn, err := it.Next()
     if err == iterator.Done {
         break
     }
     if err != nil {
         return "", err
     }
     fmt.Fprintf(&buf, "\tConnection %s was created %s\n", conn.GetName(), unixMillisToTime(conn.GetCreationTime()).Format(time.RFC822Z))
     totalConnections++
 }
 fmt.Fprintf(&buf, "\n%d connections processed.\n", totalConnections)
 return buf.String(), nil
}

// unixMillisToTime converts epoch-millisecond representations used by the API into a time.Time representation.
func unixMillisToTime(m int64) time.Time {
 if m == 0 {
     return time.Time{}
 }
 return time.Unix(0, m*1e6)
}
```

### Java

``` java
import com.google.cloud.bigquery.connection.v1.ListConnectionsRequest;
import com.google.cloud.bigquery.connection.v1.LocationName;
import com.google.cloud.bigqueryconnection.v1.ConnectionServiceClient;
import java.io.IOException;

// Sample to demonstrates basic usage of the BigQuery connection API.
public class QuickstartSample {

  public static void main(String[] args) throws IOException {
    // TODO(developer): Replace these variables before running the sample.
    String projectId = "MY_PROJECT_ID";
    String location = "MY_LOCATION";
    listConnections(projectId, location);
  }

  static void listConnections(String projectId, String location) throws IOException {
    try (ConnectionServiceClient connectionServiceClient = ConnectionServiceClient.create()) {
      LocationName parent = LocationName.of(projectId, location);
      int pageSize = 10;
      ListConnectionsRequest request =
          ListConnectionsRequest.newBuilder()
              .setParent(parent.toString())
              .setPageSize(pageSize)
              .build();
      ConnectionServiceClient.ListConnectionsPagedResponse response =
          connectionServiceClient.listConnections(request);

      // Print the results.
      System.out.println("List of connections:");
      response
          .iterateAll()
          .forEach(connection -> System.out.println("Connection Name: " + connection.getName()));
    }
  }
}
```

### Python

``` python
from google.cloud import bigquery_connection_v1 as bq_connection


def main(
    project_id: str = "your-project-id", location: str = "US", transport: str = "grpc"
) -> None:
    """Prints details and summary information about connections for a given admin project and location"""
    client = bq_connection.ConnectionServiceClient(transport=transport)
    print(f"List of connections in project {project_id} in location {location}")
    req = bq_connection.ListConnectionsRequest(
        parent=client.common_location_path(project_id, location)
    )
    for connection in client.list_connections(request=req):
        print(f"\tConnection {connection.friendly_name} ({connection.name})")
```

## Additional resources

### C\#

The following list contains links to more resources related to the client library for C\#:

  - [API reference](/dotnet/docs/reference/Google.Cloud.BigQuery.Connection.V1/latest)
  - [Client libraries best practices](/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/google-cloud-dotnet/issues)
  - [`  google-bigquery  ` on Stack Overflow](https://stackoverflow.com/search?q=%5Bgoogle-bigquery%5D+%5Bc%23%5D)
  - [Source code](https://github.com/googleapis/google-cloud-dotnet)

### Go

The following list contains links to more resources related to the client library for Go:

  - [API reference](https://pkg.go.dev/cloud.google.com/go/bigquery/connection/apiv1?tab=doc)
  - [Client libraries best practices](/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/google-cloud-go/issues)
  - [`  google-bigquery  ` on Stack Overflow](https://stackoverflow.com/search?q=%5Bgoogle-bigquery%5D+%5Bgo%5D)
  - [Source code](https://github.com/googleapis/google-cloud-go)

### Java

The following list contains links to more resources related to the client library for Java:

  - [API reference](/java/docs/reference/google-cloud-bigqueryconnection/latest/overview)
  - [Client libraries best practices](/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/java-bigqueryconnection/issues)
  - [`  google-bigquery  ` on Stack Overflow](https://stackoverflow.com/search?q=%5Bgoogle-bigquery%5D+%5Bjava%5D)
  - [Source code](https://github.com/googleapis/java-bigqueryconnection)

### Node.js

The following list contains links to more resources related to the client library for Node.js:

  - [API reference](https://googleapis.dev/nodejs/bigqueryconnection/latest)
  - [Client libraries best practices](/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/nodejs-bigquery-connection/issues)
  - [`  google-bigquery  ` on Stack Overflow](https://stackoverflow.com/search?q=%5Bgoogle-bigquery%5D+%5Bnode.js%5D)
  - [Source code](https://github.com/googleapis/nodejs-bigquery-connection)

### PHP

The following list contains links to more resources related to the client library for PHP:

  - [API reference](/php/docs/reference/cloud-bigquery/latest/BigQueryClient)
  - [Client libraries best practices](/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/google-cloud-php/issues)
  - [`  google-bigquery  ` on Stack Overflow](https://stackoverflow.com/search?q=%5Bgoogle-bigquery%5D+%5Bphp%5D)
  - [Source code](https://github.com/googleapis/google-cloud-php)

### Python

The following list contains links to more resources related to the client library for Python:

  - [API reference](/python/docs/reference/bigqueryconnection/latest)
  - [Client libraries best practices](/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/python-bigquery-connection/issues)
  - [`  google-bigquery  ` on Stack Overflow](https://stackoverflow.com/search?q=%5Bgoogle-bigquery%5D+%5Bpython%5D)
  - [Source code](https://github.com/googleapis/python-bigquery-connection)

### Ruby

The following list contains links to more resources related to the client library for Ruby:

  - [API reference](https://googleapis.dev/ruby/google-cloud-bigquery-connection/latest/index.html)
  - [Client libraries best practices](/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/google-cloud-ruby/issues)
  - [`  google-bigquery  ` on Stack Overflow](https://stackoverflow.com/search?q=%5Bgoogle-bigquery%5D+%5Bruby%5D)
  - [Source code](https://github.com/googleapis/google-cloud-ruby)

### What's next?

For more background, see [Working with connections](/bigquery/docs/working-with-connections) .
