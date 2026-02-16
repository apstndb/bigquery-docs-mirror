This page shows how to get started with the Cloud Client Libraries for the BigQuery Migration API. Client libraries make it easier to access Google Cloud APIs from a supported language. Although you can use Google Cloud APIs directly by making raw requests to the server, client libraries provide simplifications that significantly reduce the amount of code you need to write.

Read more about the Cloud Client Libraries and the older Google API Client Libraries in [Client libraries explained](/apis/docs/client-libraries-explained) .

## Install the client library

### Go

``` text
go get cloud.google.com/go/bigquery
```

For more information, see [Setting Up a Go Development Environment](/go/docs/setup) .

### Java

For more information, see [Setting Up a Java Development Environment](/java/docs/setup) .

### Python

``` text
pip install --upgrade google-cloud-bigquery-migration
```

For more information, see [Setting Up a Python Development Environment](/python/docs/setup) .

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

The following example demonstrates some basic interactions with the BigQuery Migration API.

### Go

``` go
// Copyright 2021 Google LLC
//
// Licensed under the Apache License, Version 2.0 (the "License");
// you may not use this file except in compliance with the License.
// You may obtain a copy of the License at
//
//     https://www.apache.org/licenses/LICENSE-2.0
//
// Unless required by applicable law or agreed to in writing, software
// distributed under the License is distributed on an "AS IS" BASIS,
// WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
// See the License for the specific language governing permissions and
// limitations under the License.


// The bigquery_migration_quickstart application demonstrates basic usage of the
// BigQuery migration API by executing a workflow that performs a batch SQL
// translation task.
package main

import (
 "context"
 "flag"
 "fmt"
 "log"
 "time"

 migration "cloud.google.com/go/bigquery/migration/apiv2"
 "cloud.google.com/go/bigquery/migration/apiv2/migrationpb"
)

func main() {
 // Define command line flags for controlling the behavior of this quickstart.
 projectID := flag.String("project_id", "", "Cloud Project ID.")
 location := flag.String("location", "us", "BigQuery Migration location used for interactions.")
 outputPath := flag.String("output", "", "Cloud Storage path for translated resources.")
 // Parse flags and do some minimal validation.
 flag.Parse()
 if *projectID == "" {
     log.Fatal("empty --project_id specified, please provide a valid project ID")
 }
 if *location == "" {
     log.Fatal("empty --location specified, please provide a valid location")
 }
 if *outputPath == "" {
     log.Fatalf("empty --output specified, please provide a valid cloud storage path")
 }

 ctx := context.Background()
 migClient, err := migration.NewClient(ctx)
 if err != nil {
     log.Fatalf("migration.NewClient: %v", err)
 }
 defer migClient.Close()

 workflow, err := executeTranslationWorkflow(ctx, migClient, *projectID, *location, *outputPath)
 if err != nil {
     log.Fatalf("workflow execution failed: %v\n", err)
 }

 reportWorkflowStatus(workflow)
}

// executeTranslationWorkflow constructs a migration workflow that performs batch SQL translation.
func executeTranslationWorkflow(ctx context.Context, client *migration.Client, projectID, location, outPath string) (*migrationpb.MigrationWorkflow, error) {

 // Construct the workflow creation request.  In this workflow, we have only a single translation task present.
 req := &migrationpb.CreateMigrationWorkflowRequest{
     Parent: fmt.Sprintf("projects/%s/locations/%s", projectID, location),
     MigrationWorkflow: &migrationpb.MigrationWorkflow{
         DisplayName: "example SQL conversion",
         Tasks: map[string]*migrationpb.MigrationTask{
             "example_conversion": {
                 Type: "Translation_Teradata2BQ",
                 TaskDetails: &migrationpb.MigrationTask_TranslationConfigDetails{
                     TranslationConfigDetails: &migrationpb.TranslationConfigDetails{
                         SourceLocation: &migrationpb.TranslationConfigDetails_GcsSourcePath{
                             GcsSourcePath: "gs://cloud-samples-data/bigquery/migration/translation/input/",
                         },
                         TargetLocation: &migrationpb.TranslationConfigDetails_GcsTargetPath{
                             GcsTargetPath: outPath,
                         },
                         SourceDialect: &migrationpb.Dialect{
                             DialectValue: &migrationpb.Dialect_TeradataDialect{
                                 TeradataDialect: &migrationpb.TeradataDialect{
                                     Mode: migrationpb.TeradataDialect_SQL,
                                 },
                             },
                         },
                         TargetDialect: &migrationpb.Dialect{
                             DialectValue: &migrationpb.Dialect_BigqueryDialect{},
                         },
                     },
                 },
             },
         },
     },
 }

 // Create the workflow using the request.
 workflow, err := client.CreateMigrationWorkflow(ctx, req)
 if err != nil {
     return nil, fmt.Errorf("CreateMigrationWorkflow: %w", err)
 }
 fmt.Printf("workflow created: %s", workflow.GetName())

 // This is an asyncronous process, so we now poll the workflow
 // until completion or a suitable timeout has elapsed.
 timeoutCtx, cancel := context.WithTimeout(ctx, 5*time.Minute)
 defer cancel()
 for {
     select {
     case <-timeoutCtx.Done():
         return nil, fmt.Errorf("task %s didn't complete due to context expiring", workflow.GetName())
     default:
         polledWorkflow, err := client.GetMigrationWorkflow(timeoutCtx, &migrationpb.GetMigrationWorkflowRequest{
             Name: workflow.GetName(),
         })
         if err != nil {
             return nil, fmt.Errorf("polling ended in error: %w", err)
         }
         if polledWorkflow.GetState() == migrationpb.MigrationWorkflow_COMPLETED {
             // polledWorkflow contains the most recent metadata about the workflow, so we return that.
             return polledWorkflow, nil
         }
         // workflow still isn't complete, so sleep briefly before polling again.
         time.Sleep(5 * time.Second)
     }
 }
}

// reportWorkflowStatus prints information about the workflow execution in a more human readable format.
func reportWorkflowStatus(workflow *migrationpb.MigrationWorkflow) {
 fmt.Printf("Migration workflow %s ended in state %s.\n", workflow.GetName(), workflow.GetState().String())
 for k, task := range workflow.GetTasks() {
     fmt.Printf(" - Task %s had id %s", k, task.GetId())
     if task.GetProcessingError() != nil {
         fmt.Printf(" with processing error: %s", task.GetProcessingError().GetReason())
     }
     fmt.Println()
 }
}
```

### Python

``` python
# Copyright 2022 Google LLC
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     https://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.


def create_migration_workflow(
    gcs_input_path: str, gcs_output_path: str, project_id: str
) -> None:
    """Creates a migration workflow of a Batch SQL Translation and prints the response."""

    from google.cloud import bigquery_migration_v2

    parent = f"projects/{project_id}/locations/us"

    # Construct a BigQuery Migration client object.
    client = bigquery_migration_v2.MigrationServiceClient()

    # Set the source dialect to Teradata SQL.
    source_dialect = bigquery_migration_v2.Dialect()
    source_dialect.teradata_dialect = bigquery_migration_v2.TeradataDialect(
        mode=bigquery_migration_v2.TeradataDialect.Mode.SQL
    )

    # Set the target dialect to BigQuery dialect.
    target_dialect = bigquery_migration_v2.Dialect()
    target_dialect.bigquery_dialect = bigquery_migration_v2.BigQueryDialect()

    # Prepare the config proto.
    translation_config = bigquery_migration_v2.TranslationConfigDetails(
        gcs_source_path=gcs_input_path,
        gcs_target_path=gcs_output_path,
        source_dialect=source_dialect,
        target_dialect=target_dialect,
    )

    # Prepare the task.
    migration_task = bigquery_migration_v2.MigrationTask(
        type_="Translation_Teradata2BQ", translation_config_details=translation_config
    )

    # Prepare the workflow.
    workflow = bigquery_migration_v2.MigrationWorkflow(
        display_name="demo-workflow-python-example-Teradata2BQ"
    )

    workflow.tasks["translation-task"] = migration_task  # type: ignore

    # Prepare the API request to create a migration workflow.
    request = bigquery_migration_v2.CreateMigrationWorkflowRequest(
        parent=parent,
        migration_workflow=workflow,
    )

    response = client.create_migration_workflow(request=request)

    print("Created workflow:")
    print(response.display_name)
    print("Current state:")
    print(response.State(response.state))

```

## Additional resources

### Go

The following list contains links to more resources related to the client library for Go:

  - [API reference](https://pkg.go.dev/cloud.google.com/go/bigquery/migration/apiv2alpha?tab=doc)
  - [Client libraries best practices](/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/google-cloud-go/issues)
  - [`  google-bigquery  ` on Stack Overflow](https://stackoverflow.com/search?q=%5Bgoogle-bigquery%5D+%5Bgo%5D)
  - [Source code](https://github.com/googleapis/google-cloud-go)

### Java

The following list contains links to more resources related to the client library for Java:

  - [API reference](/java/docs/reference/google-cloud-bigquerymigration/latest/overview)
  - [Client libraries best practices](/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/java-bigquerymigration/issues)
  - [`  google-bigquery  ` on Stack Overflow](https://stackoverflow.com/search?q=%5Bgoogle-bigquery%5D+%5Bjava%5D)
  - [Source code](https://github.com/googleapis/java-bigquerymigration)

### Python

The following list contains links to more resources related to the client library for Python:

  - [API reference](/python/docs/reference/bigquerymigration/latest)
  - [Client libraries best practices](/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/python-bigquery-migration/issues)
  - [`  google-bigquery  ` on Stack Overflow](https://stackoverflow.com/search?q=%5Bgoogle-bigquery%5D+%5Bpython%5D)
  - [Source code](https://github.com/googleapis/python-bigquery-migration)

### What's next?

For more background, see the [introduction to BigQuery Migration Service](https://cloud.google.com/bigquery/docs/migration-intro) page.
