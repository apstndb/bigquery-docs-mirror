This page shows how to get started with the Cloud Client Libraries for the BigQuery Storage API. Client libraries make it easier to access Google Cloud APIs from a supported language. Although you can use Google Cloud APIs directly by making raw requests to the server, client libraries provide simplifications that significantly reduce the amount of code you need to write.

Read more about the Cloud Client Libraries and the older Google API Client Libraries in [Client libraries explained](/apis/docs/client-libraries-explained) .

## Install the client library

### C++

For more information about installing the C++ library, see the [GitHub `  README  `](https://github.com/googleapis/google-cloud-cpp/tree/master/google/cloud/bigquery/quickstart) .

### C\#

``` text
Install-Package Google.Cloud.BigQuery.Storage.V1 -Pre
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
      <version>26.70.0</version>
      <type>pom</type>
      <scope>import</scope>
    </dependency>
    <dependency>
      <groupId>io.opentelemetry</groupId>
      <artifactId>opentelemetry-bom</artifactId>
      <version>1.52.0</version>
      <type>pom</type>
      <scope>import</scope>
    </dependency>
  </dependencies>
</dependencyManagement>

<dependencies>
  <dependency>
    <groupId>com.google.cloud</groupId>
    <artifactId>google-cloud-bigquerystorage</artifactId>
  </dependency>
```

If you are using [Gradle](https://gradle.org/) , add the following to your dependencies:

``` markdown
implementation platform('com.google.cloud:libraries-bom:26.74.0')

implementation 'com.google.cloud:google-cloud-bigquerystorage'
```

If you are using [sbt](https://www.scala-sbt.org/) , add the following to your dependencies:

``` markdown
libraryDependencies += "com.google.cloud" % "google-cloud-bigquerystorage" % "3.21.0"
```

If you're using Visual Studio Code or IntelliJ, you can add client libraries to your project using the following IDE plugins:

  - [Cloud Code for VS Code](/code/docs/vscode/client-libraries)
  - [Cloud Code for IntelliJ](/code/docs/intellij/client-libraries)

The plugins provide additional functionality, such as key management for service accounts. Refer to each plugin's documentation for details.

**Note:** Cloud Java client libraries do not currently support Android.

For more information, see [Setting Up a Java Development Environment](/java/docs/setup) .

### Node.js

``` text
npm install @google-cloud/bigquery-storage
```

For more information, see [Setting Up a Node.js Development Environment](/nodejs/docs/setup) .

### PHP

``` text
composer require google/cloud-bigquery-storage
```

For more information, see [Using PHP on Google Cloud](/php/docs) .

### Python

``` text
pip install --upgrade google-cloud-bigquery-storage
```

For more information, see [Setting Up a Python Development Environment](/python/docs/setup) .

### Ruby

``` text
gem install google-cloud-bigquery-storage
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

The following example shows basic interactions with the [BigQuery Storage Read API](/bigquery/docs/reference/storage) .

For examples of how to use the BigQuery Storage Write API, see [Perform batch and streaming using the Storage Write API](/bigquery/docs/write-api) .

### C++

``` cpp
#include "google/cloud/bigquery/storage/v1/bigquery_read_client.h"
#include <iostream>

namespace {
void ProcessRowsInAvroFormat(
    ::google::cloud::bigquery::storage::v1::AvroSchema const&,
    ::google::cloud::bigquery::storage::v1::AvroRows const&) {
  // Code to deserialize avro rows should be added here.
}
}  // namespace

int main(int argc, char* argv[]) try {
  if (argc != 3) {
    std::cerr << "Usage: " << argv[0] << " <project-id> <table-name>\n";
    return 1;
  }

  // project_name should be in the format "projects/<your-gcp-project>"
  std::string const project_name = "projects/" + std::string(argv[1]);
  // table_name should be in the format:
  // "projects/<project-table-resides-in>/datasets/<dataset-table_resides-in>/tables/<table
  // name>" The project values in project_name and table_name do not have to be
  // identical.
  std::string const table_name = argv[2];

  // Create a namespace alias to make the code easier to read.
  namespace bigquery_storage = ::google::cloud::bigquery_storage_v1;
  constexpr int kMaxReadStreams = 1;
  // Create the ReadSession.
  auto client = bigquery_storage::BigQueryReadClient(
      bigquery_storage::MakeBigQueryReadConnection());
  ::google::cloud::bigquery::storage::v1::ReadSession read_session;
  read_session.set_data_format(
      google::cloud::bigquery::storage::v1::DataFormat::AVRO);
  read_session.set_table(table_name);
  auto session =
      client.CreateReadSession(project_name, read_session, kMaxReadStreams);
  if (!session) throw std::move(session).status();

  // Read rows from the ReadSession.
  constexpr int kRowOffset = 0;
  auto read_rows = client.ReadRows(session->streams(0).name(), kRowOffset);

  std::int64_t num_rows = 0;
  for (auto const& row : read_rows) {
    if (row.ok()) {
      num_rows += row->row_count();
      ProcessRowsInAvroFormat(session->avro_schema(), row->avro_rows());
    }
  }

  std::cout << num_rows << " rows read from table: " << table_name << "\n";
  return 0;
} catch (google::cloud::Status const& status) {
  std::cerr << "google::cloud::Status thrown: " << status << "\n";
  return 1;
}
```

### Go

``` go
// The bigquery_storage_quickstart application demonstrates usage of the
// BigQuery Storage read API.  It demonstrates API features such as column
// projection (limiting the output to a subset of a table's columns),
// column filtering (using simple predicates to filter records on the server
// side), establishing the snapshot time (reading data from the table at a
// specific point in time), decoding Avro row blocks using the third party
// "github.com/linkedin/goavro" library, and decoding Arrow row blocks using
// the third party "github.com/apache/arrow/go" library.
package main

import (
 "bytes"
 "context"
 "encoding/json"
 "flag"
 "fmt"
 "io"
 "log"
 "sort"
 "strings"
 "sync"
 "time"

 bqStorage "cloud.google.com/go/bigquery/storage/apiv1"
 "cloud.google.com/go/bigquery/storage/apiv1/storagepb"
 "github.com/apache/arrow/go/v10/arrow"
 "github.com/apache/arrow/go/v10/arrow/ipc"
 "github.com/apache/arrow/go/v10/arrow/memory"
 gax "github.com/googleapis/gax-go/v2"
 goavro "github.com/linkedin/goavro/v2"
 "google.golang.org/genproto/googleapis/rpc/errdetails"
 "google.golang.org/grpc"
 "google.golang.org/grpc/codes"
 "google.golang.org/grpc/status"
 "google.golang.org/protobuf/types/known/timestamppb"
)

// rpcOpts is used to configure the underlying gRPC client to accept large
// messages.  The BigQuery Storage API may send message blocks up to 128MB
// in size.
var rpcOpts = gax.WithGRPCOptions(
 grpc.MaxCallRecvMsgSize(1024 * 1024 * 129),
)

// Available formats
const (
 AVRO_FORMAT  = "avro"
 ARROW_FORMAT = "arrow"
)

// Command-line flags.
var (
 projectID = flag.String("project_id", "",
     "Cloud Project ID, used for session creation.")
 snapshotMillis = flag.Int64("snapshot_millis", 0,
     "Snapshot time to use for reads, represented in epoch milliseconds format.  Default behavior reads current data.")
 format = flag.String("format", AVRO_FORMAT, "format to read data from storage API. Default is avro.")
)

func main() {
 flag.Parse()
 ctx := context.Background()
 bqReadClient, err := bqStorage.NewBigQueryReadClient(ctx)
 if err != nil {
     log.Fatalf("NewBigQueryStorageClient: %v", err)
 }
 defer bqReadClient.Close()

 // Verify we've been provided a parent project which will contain the read session.  The
 // session may exist in a different project than the table being read.
 if *projectID == "" {
     log.Fatalf("No parent project ID specified, please supply using the --project_id flag.")
 }

 // This example uses baby name data from the public datasets.
 srcProjectID := "bigquery-public-data"
 srcDatasetID := "usa_names"
 srcTableID := "usa_1910_current"
 readTable := fmt.Sprintf("projects/%s/datasets/%s/tables/%s",
     srcProjectID,
     srcDatasetID,
     srcTableID,
 )

 // We limit the output columns to a subset of those allowed in the table,
 // and set a simple filter to only report names from the state of
 // Washington (WA).
 tableReadOptions := &storagepb.ReadSession_TableReadOptions{
     SelectedFields: []string{"name", "number", "state"},
     RowRestriction: `state = "WA"`,
 }

 dataFormat := storagepb.DataFormat_AVRO
 if *format == ARROW_FORMAT {
     dataFormat = storagepb.DataFormat_ARROW
 }
 createReadSessionRequest := &storagepb.CreateReadSessionRequest{
     Parent: fmt.Sprintf("projects/%s", *projectID),
     ReadSession: &storagepb.ReadSession{
         Table:       readTable,
         DataFormat:  dataFormat,
         ReadOptions: tableReadOptions,
     },
     MaxStreamCount: 1,
 }

 // Set a snapshot time if it's been specified.
 if *snapshotMillis > 0 {
     ts := timestamppb.New(time.Unix(0, *snapshotMillis*1000))
     if !ts.IsValid() {
         log.Fatalf("Invalid snapshot millis (%d): %v", *snapshotMillis, err)
     }
     createReadSessionRequest.ReadSession.TableModifiers = &storagepb.ReadSession_TableModifiers{
         SnapshotTime: ts,
     }
 }

 // Create the session from the request.
 session, err := bqReadClient.CreateReadSession(ctx, createReadSessionRequest, rpcOpts)
 if err != nil {
     log.Fatalf("CreateReadSession: %v", err)
 }
 fmt.Printf("Read session: %s\n", session.GetName())

 if len(session.GetStreams()) == 0 {
     log.Fatalf("no streams in session.  if this was a small query result, consider writing to output to a named table.")
 }

 // We'll use only a single stream for reading data from the table.  Because
 // of dynamic sharding, this will yield all the rows in the table. However,
 // if you wanted to fan out multiple readers you could do so by having a
 // increasing the MaxStreamCount.
 readStream := session.GetStreams()[0].Name

 ch := make(chan *storagepb.ReadRowsResponse)

 // Use a waitgroup to coordinate the reading and decoding goroutines.
 var wg sync.WaitGroup

 // Start the reading in one goroutine.
 wg.Add(1)
 go func() {
     defer wg.Done()
     if err := processStream(ctx, bqReadClient, readStream, ch); err != nil {
         log.Fatalf("processStream failure: %v", err)
     }
     close(ch)
 }()

 // Start Avro processing and decoding in another goroutine.
 wg.Add(1)
 go func() {
     defer wg.Done()
     var err error
     switch *format {
     case ARROW_FORMAT:
         err = processArrow(ctx, session.GetArrowSchema().GetSerializedSchema(), ch)
     case AVRO_FORMAT:
         err = processAvro(ctx, session.GetAvroSchema().GetSchema(), ch)
     }
     if err != nil {
         log.Fatalf("error processing %s: %v", *format, err)
     }
 }()

 // Wait until both the reading and decoding goroutines complete.
 wg.Wait()

}

// printDatum prints the decoded row datum.
func printDatum(d interface{}) {
 m, ok := d.(map[string]interface{})
 if !ok {
     log.Printf("failed type assertion: %v", d)
 }
 // Go's map implementation returns keys in a random ordering, so we sort
 // the keys before accessing.
 keys := make([]string, len(m))
 i := 0
 for k := range m {
     keys[i] = k
     i++
 }
 sort.Strings(keys)
 for _, key := range keys {
     fmt.Printf("%s: %-20v ", key, valueFromTypeMap(m[key]))
 }
 fmt.Println()
}

// printRecordBatch prints the arrow record batch
func printRecordBatch(record arrow.Record) error {
 out, err := record.MarshalJSON()
 if err != nil {
     return err
 }
 list := []map[string]interface{}{}
 err = json.Unmarshal(out, &list)
 if err != nil {
     return err
 }
 if len(list) == 0 {
     return nil
 }
 first := list[0]
 keys := make([]string, len(first))
 i := 0
 for k := range first {
     keys[i] = k
     i++
 }
 sort.Strings(keys)
 builder := strings.Builder{}
 for _, m := range list {
     for _, key := range keys {
         builder.WriteString(fmt.Sprintf("%s: %-20v ", key, m[key]))
     }
     builder.WriteString("\n")
 }
 fmt.Print(builder.String())
 return nil
}

// valueFromTypeMap returns the first value/key in the type map.  This function
// is only suitable for simple schemas, as complex typing such as arrays and
// records necessitate a more robust implementation.  See the goavro library
// and the Avro specification for more information.
func valueFromTypeMap(field interface{}) interface{} {
 m, ok := field.(map[string]interface{})
 if !ok {
     return nil
 }
 for _, v := range m {
     // Return the first key encountered.
     return v
 }
 return nil
}

// processStream reads rows from a single storage Stream, and sends the Storage Response
// data blocks to a channel. This function will retry on transient stream
// failures and bookmark progress to avoid re-reading data that's already been
// successfully transmitted.
func processStream(ctx context.Context, client *bqStorage.BigQueryReadClient, st string, ch chan<- *storagepb.ReadRowsResponse) error {
 var offset int64

 // Streams may be long-running.  Rather than using a global retry for the
 // stream, implement a retry that resets once progress is made.
 retryLimit := 3
 retries := 0
 for {
     // Send the initiating request to start streaming row blocks.
     rowStream, err := client.ReadRows(ctx, &storagepb.ReadRowsRequest{
         ReadStream: st,
         Offset:     offset,
     }, rpcOpts)
     if err != nil {
         return fmt.Errorf("couldn't invoke ReadRows: %w", err)
     }

     // Process the streamed responses.
     for {
         r, err := rowStream.Recv()
         if err == io.EOF {
             return nil
         }
         if err != nil {
             // If there is an error, check whether it is a retryable
             // error with a retry delay and sleep instead of increasing
             // retries count.
             var retryDelayDuration time.Duration
             if errorStatus, ok := status.FromError(err); ok && errorStatus.Code() == codes.ResourceExhausted {
                 for _, detail := range errorStatus.Details() {
                     retryInfo, ok := detail.(*errdetails.RetryInfo)
                     if !ok {
                         continue
                     }
                     retryDelay := retryInfo.GetRetryDelay()
                     retryDelayDuration = time.Duration(retryDelay.Seconds)*time.Second + time.Duration(retryDelay.Nanos)*time.Nanosecond
                     break
                 }
             }
             if retryDelayDuration != 0 {
                 log.Printf("processStream failed with a retryable error, retrying in %v", retryDelayDuration)
                 time.Sleep(retryDelayDuration)
             } else {
                 retries++
                 if retries >= retryLimit {
                     return fmt.Errorf("processStream retries exhausted: %w", err)
                 }
             }
             // break the inner loop, and try to recover by starting a new streaming
             // ReadRows call at the last known good offset.
             break
         } else {
             // Reset retries after a successful response.
             retries = 0
         }

         rc := r.GetRowCount()
         if rc > 0 {
             // Bookmark our progress in case of retries and send the rowblock on the channel.
             offset = offset + rc
             // We're making progress, reset retries.
             retries = 0
             ch <- r
         }
     }
 }
}

// processArrow receives row blocks from a channel, and uses the provided Arrow
// schema to decode the blocks into individual row messages for printing.  Will
// continue to run until the channel is closed or the provided context is
// cancelled.
func processArrow(ctx context.Context, schema []byte, ch <-chan *storagepb.ReadRowsResponse) error {
 mem := memory.NewGoAllocator()
 buf := bytes.NewBuffer(schema)
 r, err := ipc.NewReader(buf, ipc.WithAllocator(mem))
 if err != nil {
     return err
 }
 aschema := r.Schema()
 for {
     select {
     case <-ctx.Done():
         // Context was cancelled.  Stop.
         return ctx.Err()
     case rows, ok := <-ch:
         if !ok {
             // Channel closed, no further arrow messages.  Stop.
             return nil
         }
         undecoded := rows.GetArrowRecordBatch().GetSerializedRecordBatch()
         if len(undecoded) > 0 {
             buf = bytes.NewBuffer(schema)
             buf.Write(undecoded)
             r, err = ipc.NewReader(buf, ipc.WithAllocator(mem), ipc.WithSchema(aschema))
             if err != nil {
                 return err
             }
             for r.Next() {
                 rec := r.Record()
                 err = printRecordBatch(rec)
                 if err != nil {
                     return err
                 }
             }
         }
     }
 }
}

// processAvro receives row blocks from a channel, and uses the provided Avro
// schema to decode the blocks into individual row messages for printing.  Will
// continue to run until the channel is closed or the provided context is
// cancelled.
func processAvro(ctx context.Context, schema string, ch <-chan *storagepb.ReadRowsResponse) error {
 // Establish a decoder that can process blocks of messages using the
 // reference schema. All blocks share the same schema, so the decoder
 // can be long-lived.
 codec, err := goavro.NewCodec(schema)
 if err != nil {
     return fmt.Errorf("couldn't create codec: %w", err)
 }

 for {
     select {
     case <-ctx.Done():
         // Context was cancelled.  Stop.
         return ctx.Err()
     case rows, ok := <-ch:
         if !ok {
             // Channel closed, no further avro messages.  Stop.
             return nil
         }
         undecoded := rows.GetAvroRows().GetSerializedBinaryRows()
         for len(undecoded) > 0 {
             datum, remainingBytes, err := codec.NativeFromBinary(undecoded)

             if err != nil {
                 if err == io.EOF {
                     break
                 }
                 return fmt.Errorf("decoding error with %d bytes remaining: %v", len(undecoded), err)
             }
             printDatum(datum)
             undecoded = remainingBytes
         }
     }
 }
}
```

### Java

``` java
import com.google.api.gax.rpc.ServerStream;
import com.google.cloud.bigquery.storage.v1.ArrowRecordBatch;
import com.google.cloud.bigquery.storage.v1.ArrowSchema;
import com.google.cloud.bigquery.storage.v1.BigQueryReadClient;
import com.google.cloud.bigquery.storage.v1.CreateReadSessionRequest;
import com.google.cloud.bigquery.storage.v1.DataFormat;
import com.google.cloud.bigquery.storage.v1.ReadRowsRequest;
import com.google.cloud.bigquery.storage.v1.ReadRowsResponse;
import com.google.cloud.bigquery.storage.v1.ReadSession;
import com.google.cloud.bigquery.storage.v1.ReadSession.TableModifiers;
import com.google.cloud.bigquery.storage.v1.ReadSession.TableReadOptions;
import com.google.common.base.Preconditions;
import com.google.protobuf.Timestamp;
import java.io.IOException;
import java.util.ArrayList;
import java.util.List;
import org.apache.arrow.memory.BufferAllocator;
import org.apache.arrow.memory.RootAllocator;
import org.apache.arrow.vector.FieldVector;
import org.apache.arrow.vector.VectorLoader;
import org.apache.arrow.vector.VectorSchemaRoot;
import org.apache.arrow.vector.ipc.ReadChannel;
import org.apache.arrow.vector.ipc.message.MessageSerializer;
import org.apache.arrow.vector.types.pojo.Field;
import org.apache.arrow.vector.types.pojo.Schema;
import org.apache.arrow.vector.util.ByteArrayReadableSeekableByteChannel;

public class StorageArrowSample {

  /*
   * SimpleRowReader handles deserialization of the Apache Arrow-encoded row batches transmitted
   * from the storage API using a generic datum decoder.
   */
  private static class SimpleRowReader implements AutoCloseable {

    BufferAllocator allocator = new RootAllocator(Long.MAX_VALUE);

    // Decoder object will be reused to avoid re-allocation and too much garbage collection.
    private final VectorSchemaRoot root;
    private final VectorLoader loader;

    public SimpleRowReader(ArrowSchema arrowSchema) throws IOException {
      Schema schema =
          MessageSerializer.deserializeSchema(
              new ReadChannel(
                  new ByteArrayReadableSeekableByteChannel(
                      arrowSchema.getSerializedSchema().toByteArray())));
      Preconditions.checkNotNull(schema);
      List<FieldVector> vectors = new ArrayList<>();
      for (Field field : schema.getFields()) {
        vectors.add(field.createVector(allocator));
      }
      root = new VectorSchemaRoot(vectors);
      loader = new VectorLoader(root);
    }

    /**
     * Sample method for processing Arrow data which only validates decoding.
     *
     * @param batch object returned from the ReadRowsResponse.
     */
    public void processRows(ArrowRecordBatch batch) throws IOException {
      org.apache.arrow.vector.ipc.message.ArrowRecordBatch deserializedBatch =
          MessageSerializer.deserializeRecordBatch(
              new ReadChannel(
                  new ByteArrayReadableSeekableByteChannel(
                      batch.getSerializedRecordBatch().toByteArray())),
              allocator);

      loader.load(deserializedBatch);
      // Release buffers from batch (they are still held in the vectors in root).
      deserializedBatch.close();
      System.out.println(root.contentToTSVString());
      // Release buffers from vectors in root.
      root.clear();
    }

    @Override
    public void close() {
      root.close();
      allocator.close();
    }
  }

  public static void main(String... args) throws Exception {
    // Sets your Google Cloud Platform project ID.
    // String projectId = "YOUR_PROJECT_ID";
    String projectId = args[0];
    Integer snapshotMillis = null;
    if (args.length > 1) {
      snapshotMillis = Integer.parseInt(args[1]);
    }

    try (BigQueryReadClient client = BigQueryReadClient.create()) {
      String parent = String.format("projects/%s", projectId);

      // This example uses baby name data from the public datasets.
      String srcTable =
          String.format(
              "projects/%s/datasets/%s/tables/%s",
              "bigquery-public-data", "usa_names", "usa_1910_current");

      // We specify the columns to be projected by adding them to the selected fields,
      // and set a simple filter to restrict which rows are transmitted.
      TableReadOptions options =
          TableReadOptions.newBuilder()
              .addSelectedFields("name")
              .addSelectedFields("number")
              .addSelectedFields("state")
              .setRowRestriction("state = \"WA\"")
              .build();

      // Start specifying the read session we want created.
      ReadSession.Builder sessionBuilder =
          ReadSession.newBuilder()
              .setTable(srcTable)
              // This API can also deliver data serialized in Apache Avro format.
              // This example leverages Apache Arrow.
              .setDataFormat(DataFormat.ARROW)
              .setReadOptions(options);

      // Optionally specify the snapshot time.  When unspecified, snapshot time is "now".
      if (snapshotMillis != null) {
        Timestamp t =
            Timestamp.newBuilder()
                .setSeconds(snapshotMillis / 1000)
                .setNanos((int) ((snapshotMillis % 1000) * 1000000))
                .build();
        TableModifiers modifiers = TableModifiers.newBuilder().setSnapshotTime(t).build();
        sessionBuilder.setTableModifiers(modifiers);
      }

      // Begin building the session creation request.
      CreateReadSessionRequest.Builder builder =
          CreateReadSessionRequest.newBuilder()
              .setParent(parent)
              .setReadSession(sessionBuilder)
              .setMaxStreamCount(1);

      ReadSession session = client.createReadSession(builder.build());
      // Setup a simple reader and start a read session.
      try (SimpleRowReader reader = new SimpleRowReader(session.getArrowSchema())) {

        // Assert that there are streams available in the session.  An empty table may not have
        // data available.  If no sessions are available for an anonymous (cached) table, consider
        // writing results of a query to a named table rather than consuming cached results
        // directly.
        Preconditions.checkState(session.getStreamsCount() > 0);

        // Use the first stream to perform reading.
        String streamName = session.getStreams(0).getName();

        ReadRowsRequest readRowsRequest =
            ReadRowsRequest.newBuilder().setReadStream(streamName).build();

        // Process each block of rows as they arrive and decode using our simple row reader.
        ServerStream<ReadRowsResponse> stream = client.readRowsCallable().call(readRowsRequest);
        for (ReadRowsResponse response : stream) {
          Preconditions.checkState(response.hasArrowRecordBatch());
          reader.processRows(response.getArrowRecordBatch());
        }
      }
    }
  }
}
```

### Python

``` python
from google.cloud.bigquery_storage import BigQueryReadClient, types

# TODO(developer): Set the project_id variable.
# project_id = 'your-project-id'
#
# The read session is created in this project. This project can be
# different from that which contains the table.

client = BigQueryReadClient()

# This example reads baby name data from the public datasets.
table = "projects/{}/datasets/{}/tables/{}".format(
    "bigquery-public-data", "usa_names", "usa_1910_current"
)

requested_session = types.ReadSession()
requested_session.table = table
# This API can also deliver data serialized in Apache Arrow format.
# This example leverages Apache Avro.
requested_session.data_format = types.DataFormat.AVRO

# We limit the output columns to a subset of those allowed in the table,
# and set a simple filter to only report names from the state of
# Washington (WA).
requested_session.read_options.selected_fields = ["name", "number", "state"]
requested_session.read_options.row_restriction = 'state = "WA"'

# Set a snapshot time if it's been specified.
if snapshot_millis > 0:
    snapshot_time = types.Timestamp()
    snapshot_time.FromMilliseconds(snapshot_millis)
    requested_session.table_modifiers.snapshot_time = snapshot_time

parent = "projects/{}".format(project_id)
session = client.create_read_session(
    parent=parent,
    read_session=requested_session,
    # We'll use only a single stream for reading data from the table. However,
    # if you wanted to fan out multiple readers you could do so by having a
    # reader process each individual stream.
    max_stream_count=1,
)
reader = client.read_rows(session.streams[0].name)

# The read stream contains blocks of Avro-encoded bytes. The rows() method
# uses the fastavro library to parse these blocks as an iterable of Python
# dictionaries. Install fastavro with the following command:
#
# pip install google-cloud-bigquery-storage[fastavro]
rows = reader.rows(session)

# Do any local processing by iterating over the rows. The
# google-cloud-bigquery-storage client reconnects to the API after any
# transient network errors or timeouts.
names = set()
states = set()

# fastavro returns EOFError instead of StopIterationError starting v1.8.4.
# See https://github.com/googleapis/python-bigquery-storage/pull/687
try:
    for row in rows:
        names.add(row["name"])
        states.add(row["state"])
except EOFError:
    pass

print("Got {} unique names in states: {}".format(len(names), ", ".join(states)))
```

## Additional resources

### C++

The following list contains links to more resources related to the client library for C++:

  - [API reference](https://googleapis.dev/cpp/google-cloud-bigquery/latest/)
  - [Client libraries best practices](/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/google-cloud-cpp/issues)
  - [`  google-bigquery  ` on Stack Overflow](https://stackoverflow.com/search?q=%5Bgoogle-bigquery%5D%5Bc%2B%2B%5D)
  - [Source code](https://github.com/googleapis/google-cloud-cpp)

### C\#

The following list contains links to more resources related to the client library for C\#:

  - [API reference](/dotnet/docs/reference/Google.Cloud.BigQuery.Storage.V1/latest)
  - [Client libraries best practices](/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/google-cloud-dotnet/issues)
  - [`  google-bigquery  ` on Stack Overflow](https://stackoverflow.com/search?q=%5Bgoogle-bigquery%5D+%5Bc%23%5D)
  - [Source code](https://github.com/googleapis/google-cloud-dotnet)

### Go

The following list contains links to more resources related to the client library for Go:

  - [API reference](https://pkg.go.dev/cloud.google.com/go/bigquery/storage?tab=doc)
  - [Client libraries best practices](/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/google-cloud-go/issues)
  - [`  google-bigquery  ` on Stack Overflow](https://stackoverflow.com/search?q=%5Bgoogle-bigquery%5D+%5Bgo%5D)
  - [Source code](https://github.com/googleapis/google-cloud-go)

### Java

The following list contains links to more resources related to the client library for Java:

  - [API reference](/java/docs/reference/google-cloud-bigquerystorage/latest/com.google.cloud.bigquery.storage.v1)
  - [Client libraries best practices](/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/java-bigquerystorage/issues)
  - [`  google-bigquery  ` on Stack Overflow](https://stackoverflow.com/search?q=%5Bgoogle-bigquery%5D+%5Bjava%5D)
  - [Source code](https://github.com/googleapis/java-bigquerystorage)

### Node.js

The following list contains links to more resources related to the client library for Node.js:

  - [API reference](https://googleapis.dev/nodejs/bigquery/latest/index.html)
  - [Client libraries best practices](/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/nodejs-bigquery-storage/issues)
  - [`  google-bigquery  ` on Stack Overflow](https://stackoverflow.com/search?q=%5Bgoogle-bigquery%5D+%5Bnode.js%5D)
  - [Source code](https://github.com/googleapis/nodejs-bigquery-storage)

### PHP

The following list contains links to more resources related to the client library for PHP:

  - [API reference](/php/docs/reference/cloud-bigquery/latest/BigQueryClient)
  - [Client libraries best practices](/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/google-cloud-php/issues)
  - [`  google-bigquery  ` on Stack Overflow](https://stackoverflow.com/search?q=%5Bgoogle-bigquery%5D+%5Bphp%5D)
  - [Source code](https://github.com/googleapis/google-cloud-php)

### Python

The following list contains links to more resources related to the client library for Python:

  - [API reference](/python/docs/reference/bigquerystorage/latest)
  - [Client libraries best practices](/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/google-cloud-python/issues)
  - [`  google-bigquery  ` on Stack Overflow](https://stackoverflow.com/search?q=%5Bgoogle-bigquery%5D+%5Bpython%5D)
  - [Source code](https://github.com/googleapis/google-cloud-python)

### Ruby

The following list contains links to more resources related to the client library for Ruby:

  - [API reference](https://googleapis.dev/ruby/google-cloud-bigquery-storage/latest/index.html)
  - [Client libraries best practices](/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/google-cloud-ruby/issues)
  - [`  google-bigquery  ` on Stack Overflow](https://stackoverflow.com/search?q=%5Bgoogle-bigquery%5D+%5Bruby%5D)
  - [Source code](https://github.com/googleapis/google-cloud-ruby)

### What's next?

For users of the pandas and integration to BigQuery, see the tutorial [Visualizing BigQuery data in a Jupyter notebook](/bigquery/docs/visualize-jupyter) .
