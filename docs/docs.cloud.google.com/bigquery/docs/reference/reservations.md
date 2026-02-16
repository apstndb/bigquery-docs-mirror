This page shows how to get started with the Cloud Client Libraries for the BigQuery Reservation API. Client libraries make it easier to access Google Cloud APIs from a supported language. Although you can use Google Cloud APIs directly by making raw requests to the server, client libraries provide simplifications that significantly reduce the amount of code you need to write.

Read more about the Cloud Client Libraries and the older Google API Client Libraries in [Client libraries explained](/apis/docs/client-libraries-explained) .

## Install the client library

### C\#

``` text
Install-Package Google.Cloud.BigQuery.Reservation.V1 -Pre
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
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>com.google.cloud</groupId>
      <artifactId>libraries-bom</artifactId>
      <version>26.75.0</version>
      <type>pom</type>
      <scope>import</scope>
    </dependency>
  </dependencies>
</dependencyManagement>

<dependencies>
  <dependency>
    <groupId>com.google.cloud</groupId>
    <artifactId>google-cloud-bigqueryreservation</artifactId>
  </dependency>
</dependencies>
```

If you are using [Gradle](https://gradle.org/) , add the following to your dependencies:

``` markdown
implementation 'com.google.cloud:google-cloud-bigqueryreservation:2.84.0'
```

If you are using [sbt](https://www.scala-sbt.org/) , add the following to your dependencies:

``` markdown
libraryDependencies += "com.google.cloud" % "google-cloud-bigqueryreservation" % "2.84.0"
```

If you're using Visual Studio Code or IntelliJ, you can add client libraries to your project using the following IDE plugins:

  - [Cloud Code for VS Code](/code/docs/vscode/client-libraries)
  - [Cloud Code for IntelliJ](/code/docs/intellij/client-libraries)

The plugins provide additional functionality, such as key management for service accounts. Refer to each plugin's documentation for details.

**Note:** Cloud Java client libraries do not currently support Android.

For more information, see [Setting Up a Java Development Environment](/java/docs/setup) .

### Node.js

``` text
npm install @google-cloud/bigquery-reservation
```

For more information, see [Setting Up a Node.js Development Environment](/nodejs/docs/setup) .

### PHP

``` text
composer require google/cloud-bigquery-reservation
```

For more information, see [Using PHP on Google Cloud](/php/docs) .

### Python

``` text
pip install --upgrade google-cloud-bigquery-reservation
```

For more information, see [Setting Up a Python Development Environment](/python/docs/setup) .

### Ruby

``` text
gem install google-cloud-bigquery-reservation
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

The following example demonstrates some basic interactions with the BigQuery Reservation API by enumerating resources, namely reservations and capacity commitments.

### Go

``` go
// The bigquery_reservation_quickstart application demonstrates usage of the
// BigQuery reservation API by enumerating some of the resources that can be
// associated with a cloud project.
package main

import (
 "bytes"
 "context"
 "flag"
 "fmt"
 "log"

 reservation "cloud.google.com/go/bigquery/reservation/apiv1"
 "google.golang.org/api/iterator"
 reservationpb "google.golang.org/genproto/googleapis/cloud/bigquery/reservation/v1"
)

func main() {

 // Define two command line flags for controlling the behavior of this quickstart.
 var (
     projectID = flag.String("project_id", "", "Cloud Project ID, used for session creation.")
     location  = flag.String("location", "US", "BigQuery location used for interactions.")
 )
 // Parse flags and do some minimal validation.
 flag.Parse()
 if *projectID == "" {
     log.Fatal("empty --project_id specified, please provide a valid project ID")
 }
 if *location == "" {
     log.Fatal("empty --location specified, please provide a valid location")
 }

 ctx := context.Background()
 bqResClient, err := reservation.NewClient(ctx)
 if err != nil {
     log.Fatalf("NewClient: %v", err)
 }
 defer bqResClient.Close()

 s, err := reportCapacityCommitments(ctx, bqResClient, *projectID, *location)
 if err != nil {
     log.Fatalf("printCapacityCommitments: %v", err)
 }
 fmt.Println(s)

 s, err = reportReservations(ctx, bqResClient, *projectID, *location)
 if err != nil {
     log.Fatalf("printReservations: %v", err)
 }
 fmt.Println(s)
}

// printCapacityCommitments iterates through the capacity commitments and returns a byte buffer with details.
func reportCapacityCommitments(ctx context.Context, client *reservation.Client, projectID, location string) (string, error) {
 var buf bytes.Buffer
 fmt.Fprintf(&buf, "Capacity commitments in project %s in location %s:\n", projectID, location)

 req := &reservationpb.ListCapacityCommitmentsRequest{
     Parent: fmt.Sprintf("projects/%s/locations/%s", projectID, location),
 }
 totalCommitments := 0
 it := client.ListCapacityCommitments(ctx, req)
 for {
     commitment, err := it.Next()
     if err == iterator.Done {
         break
     }
     if err != nil {
         return "", err
     }
     fmt.Fprintf(&buf, "\tCommitment %s in state %s\n", commitment.GetName(), commitment.GetState().String())
     totalCommitments++
 }
 fmt.Fprintf(&buf, "\n%d commitments processed.\n", totalCommitments)
 return buf.String(), nil
}

// printReservations iterates through reservations defined in an admin project.
func reportReservations(ctx context.Context, client *reservation.Client, projectID, location string) (string, error) {
 var buf bytes.Buffer
 fmt.Fprintf(&buf, "Reservations in project %s in location %s:\n", projectID, location)

 req := &reservationpb.ListReservationsRequest{
     Parent: fmt.Sprintf("projects/%s/locations/%s", projectID, location),
 }
 totalReservations := 0
 it := client.ListReservations(ctx, req)
 for {
     reservation, err := it.Next()
     if err == iterator.Done {
         break
     }
     if err != nil {
         return "", err
     }
     fmt.Fprintf(&buf, "\tReservation %s has %d slot capacity.\n", reservation.GetName(), reservation.GetSlotCapacity())
     totalReservations++
 }
 fmt.Fprintf(&buf, "\n%d reservations processed.\n", totalReservations)
 return buf.String(), nil
}
```

### Java

``` java
import com.google.cloud.bigquery.reservation.v1.ReservationServiceClient;
import java.io.IOException;

public class QuickstartSample {

  public static void main(String... args) throws Exception {
    // TODO(developer): Replace these variables before running the sample.
    String projectId = "YOUR_PROJECT_ID";
    String location = "LOCATION";
    quickStartSample(projectId, location);
  }

  public static void quickStartSample(String projectId, String location) throws IOException {
    try (ReservationServiceClient client = ReservationServiceClient.create()) {
      // list reservations in the project
      String parent = String.format("projects/%s/locations/%s", projectId, location);
      client
          .listReservations(parent)
          .iterateAll()
          .forEach(res -> System.out.println("Reservation resource name: " + res.getName()));

      // list capacity commitments in the project
      client
          .listCapacityCommitments(parent)
          .iterateAll()
          .forEach(
              commitment ->
                  System.out.println("Capacity commitment resource name: " + commitment.getName()));
    }
  }
}
```

### Node.js

``` javascript
// Imports the Google Cloud client library
const {
  ReservationServiceClient,
} = require('@google-cloud/bigquery-reservation');

// Creates a client
const client = new ReservationServiceClient();

// project = 'my-project' // Project to list reservations for.
// location = 'US' // BigQuery location.

async function listReservations() {
  const [reservations] = await client.listReservations({
    parent: `projects/${project}/locations/${location}`,
  });

  console.info(`found ${reservations.length} reservations`);
  console.info(reservations);
}

async function listCapacityCommitments() {
  const [commitments] = await client.listCapacityCommitments({
    parent: `projects/${project}/locations/${location}`,
  });

  console.info(`found ${commitments.length} commitments`);
  console.info(commitments);
}

listReservations();
listCapacityCommitments();
```

### Python

``` python
import argparse

from google.cloud import bigquery_reservation_v1


def main(
    project_id: str = "your-project-id", location: str = "US", transport: str = "grpc"
) -> None:
    # Constructs the client for interacting with the service.
    client = bigquery_reservation_v1.ReservationServiceClient(transport=transport)

    report_reservations(client, project_id, location)


def report_reservations(
    client: bigquery_reservation_v1.ReservationServiceClient,
    project_id: str,
    location: str,
) -> None:
    """Prints details and summary information about reservations defined within
    a given admin project and location.
    """
    print("Reservations in project {} in location {}".format(project_id, location))
    req = bigquery_reservation_v1.ListReservationsRequest(
        parent=client.common_location_path(project_id, location)
    )
    total_reservations = 0
    for reservation in client.list_reservations(request=req):
        print(
            f"\tReservation {reservation.name} "
            f"has {reservation.slot_capacity} slot capacity."
        )
        total_reservations = total_reservations + 1
    print(f"\n{total_reservations} reservations processed.")


if __name__ == "__main__":
    parser = argparse.ArgumentParser()
    parser.add_argument("--project_id", type=str)
    parser.add_argument("--location", default="US", type=str)
    args = parser.parse_args()
    main(project_id=args.project_id, location=args.location)
```

## Additional resources

### C\#

The following list contains links to more resources related to the client library for C\#:

  - [API reference](/dotnet/docs/reference/Google.Cloud.BigQuery.Reservation.V1/latest)
  - [Client libraries best practices](/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/google-cloud-dotnet/issues)
  - [`  google-bigquery  ` on Stack Overflow](https://stackoverflow.com/search?q=%5Bgoogle-bigquery%5D+%5Bc%23%5D)
  - [Source code](https://github.com/googleapis/google-cloud-dotnet)

### Go

The following list contains links to more resources related to the client library for Go:

  - [API reference](https://pkg.go.dev/cloud.google.com/go/bigquery/reservation/apiv1?tab=doc)
  - [Client libraries best practices](/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/google-cloud-go/issues)
  - [`  google-bigquery  ` on Stack Overflow](https://stackoverflow.com/search?q=%5Bgoogle-bigquery%5D+%5Bgo%5D)
  - [Source code](https://github.com/googleapis/google-cloud-go)

### Java

The following list contains links to more resources related to the client library for Java:

  - [API reference](/java/docs/reference/google-cloud-bigqueryreservation/latest/overview)
  - [Client libraries best practices](/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/java-bigqueryreservation/issues)
  - [`  google-bigquery  ` on Stack Overflow](https://stackoverflow.com/search?q=%5Bgoogle-bigquery%5D+%5Bjava%5D)
  - [Source code](https://github.com/googleapis/java-bigqueryreservation)

### Node.js

The following list contains links to more resources related to the client library for Node.js:

  - [API reference](https://googleapis.dev/nodejs/bigqueryreservation/latest)
  - [Client libraries best practices](/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/nodejs-bigquery-reservation/issues)
  - [`  google-bigquery  ` on Stack Overflow](https://stackoverflow.com/search?q=%5Bgoogle-bigquery%5D+%5Bnode.js%5D)
  - [Source code](https://github.com/googleapis/nodejs-bigquery-reservation)

### PHP

The following list contains links to more resources related to the client library for PHP:

  - [API reference](/php/docs/reference/cloud-bigquery/latest/BigQueryClient)
  - [Client libraries best practices](/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/google-cloud-php/issues)
  - [`  google-bigquery  ` on Stack Overflow](https://stackoverflow.com/search?q=%5Bgoogle-bigquery%5D+%5Bphp%5D)
  - [Source code](https://github.com/googleapis/google-cloud-php)

### Python

The following list contains links to more resources related to the client library for Python:

  - [API reference](/python/docs/reference/bigqueryreservation/latest)
  - [Client libraries best practices](/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/python-bigquery-reservation/issues)
  - [`  google-bigquery  ` on Stack Overflow](https://stackoverflow.com/search?q=%5Bgoogle-bigquery%5D+%5Bpython%5D)
  - [Source code](https://github.com/googleapis/python-bigquery-reservation)

### Ruby

The following list contains links to more resources related to the client library for Ruby:

  - [API reference](https://googleapis.dev/ruby/google-cloud-bigquery-reservation/latest/index.html)
  - [Client libraries best practices](/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/google-cloud-ruby/issues)
  - [`  google-bigquery  ` on Stack Overflow](https://stackoverflow.com/search?q=%5Bgoogle-bigquery%5D+%5Bruby%5D)
  - [Source code](https://github.com/googleapis/google-cloud-ruby)

### What's next?

For more background and conceptual information about reservations, see [Introduction to Reservations](/bigquery/docs/reservations-intro) .
