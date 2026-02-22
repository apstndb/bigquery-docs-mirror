# Scan for data quality issues

This document explains how to use BigQuery and Dataplex Universal Catalog together to ensure that data meets your quality expectations. Dataplex Universal Catalog automatic data quality lets you define and measure the quality of the data in your BigQuery tables. You can automate the scanning of data, validate data against defined rules, and log alerts if your data doesn't meet quality requirements.

For more information about automatic data quality, see the [Auto data quality overview](/dataplex/docs/auto-data-quality-overview) .

**Tip:** The steps in this document show how to manage data quality scans across your project. You can also create and manage data quality scans when working with a specific table. For more information, see the [Manage data quality scans for a specific table](#start-from-table) section of this document.

## Before you begin

1.  Enable the Dataplex API.
    
    **Roles required to enable APIs**
    
    To enable APIs, you need the Service Usage Admin IAM role ( `  roles/serviceusage.serviceUsageAdmin  ` ), which contains the `  serviceusage.services.enable  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .

2.  Optional: If you want Dataplex Universal Catalog to generate recommendations for data quality rules based on the results of a data profile scan, [create and run the data profile scan](/bigquery/docs/data-profile-scan) .

## Required roles

  - To run a data quality scan on a BigQuery table, you need permission to read the BigQuery table and permission to create a BigQuery job in the project used to scan the table.
    
    **Note:** Dataplex Universal Catalog doesn't create a BigQuery job in your project. However, you need this permission to create a `  DryRun  ` job to check for permissions for the table.

  - If the BigQuery table and the data quality scan are in different projects, then you need to give the Dataplex Universal Catalog service account of the project containing the data quality scan read permission for the corresponding BigQuery table.
    
    **Note:** If you haven't created any data quality or data profile scans or you don't have a Dataplex Universal Catalog lake in this project, create a service identifier by running: `  gcloud beta services identity create --service=dataplex.googleapis.com  ` . This command returns a Dataplex Universal Catalog service identifier if it exists.

  - If the data quality rules refer to additional tables, then the scan project's service account must have read permissions on the same tables.

  - To export the scan results to a BigQuery table, ensure that the following permissions are granted:
    
      - The **Dataplex Universal Catalog service account** must be granted the BigQuery Data Editor ( `  roles/bigquery.dataEditor  ` ) IAM role on the results dataset and table. This grants the following permissions:
        
          - `  bigquery.datasets.get  `
          - `  bigquery.tables.create  `
          - `  bigquery.tables.get  `
          - `  bigquery.tables.getData  `
          - `  bigquery.tables.update  `
          - `  bigquery.tables.updateData  `

  - If the BigQuery data is organized in a Dataplex Universal Catalog lake, grant the Dataplex Universal Catalog service account the Dataplex Metadata Reader ( `  roles/dataplex.metadataReader  ` ) and Dataplex Viewer ( `  roles/dataplex.viewer  ` ) IAM roles. Alternatively, you need all of the following permissions:
    
      - `  dataplex.lakes.list  `
      - `  dataplex.lakes.get  `
      - `  dataplex.zones.list  `
      - `  dataplex.zones.get  `
      - `  dataplex.entities.list  `
      - `  dataplex.entities.get  `
      - `  dataplex.operations.get  `

  - If you're scanning a BigQuery external table from Cloud Storage, grant the Dataplex Universal Catalog service account the Storage Object Viewer ( `  roles/storage.objectViewer  ` ) role for the bucket. Alternatively, assign the Dataplex Universal Catalog service account the following permissions:
    
      - `  storage.buckets.get  `
      - `  storage.objects.get  `

  - If you want to publish the data quality scan results as Dataplex Universal Catalog metadata, you must be granted the BigQuery Data Editor ( `  roles/bigquery.dataEditor  ` ) IAM role for the table, and the `  dataplex.entryGroups.useDataQualityScorecardAspect  ` permission on the `  @bigquery  ` entry group in the same location as the table. Alternatively, you must be granted the Dataplex Catalog Editor ( `  roles/dataplex.catalogEditor  ` ) role for the `  @bigquery  ` entry group in the same location as the table.
    
    Alternatively, you need all of the following permissions:
    
      - `  bigquery.tables.update  ` - on the table
      - `  dataplex.entryGroups.useDataQualityScorecardAspect  ` - on the `  @bigquery  ` entry group
    
    Or, you need all of the following permissions:
    
      - `  dataplex.entries.update  ` - on the `  @bigquery  ` entry group
      - `  dataplex.entryGroups.useDataQualityScorecardAspect  ` - on the `  @bigquery  ` entry group

  - If you need to access columns protected by BigQuery column-level access policies, then assign the Dataplex Universal Catalog service account permissions for those columns. The user creating or updating a data scan also needs permissions for the columns.

  - If a table has BigQuery row-level access policies enabled, then you can only scan rows visible to the Dataplex Universal Catalog service account. Note that the individual user's access privileges are not evaluated for row-level policies.

### Required data scan roles

To use auto data quality, ask your administrator to grant you one of the following IAM roles:

  - Full access to `  DataScan  ` resources: Dataplex DataScan Administrator ( `  roles/dataplex.dataScanAdmin  ` )
  - To create `  DataScan  ` resources: Dataplex DataScan Creator ( `  roles/dataplex.dataScanCreator  ` ) on the project
  - Write access to `  DataScan  ` resources: Dataplex DataScan Editor ( `  roles/dataplex.dataScanEditor  ` )
  - Read access to `  DataScan  ` resources excluding rules and results: Dataplex DataScan Viewer ( `  roles/dataplex.dataScanViewer  ` )
  - Read access to `  DataScan  ` resources, including rules and results: Dataplex DataScan DataViewer ( `  roles/dataplex.dataScanDataViewer  ` )

The following table lists the `  DataScan  ` permissions:

<table>
<thead>
<tr class="header">
<th style="text-align: center;">Permission name</th>
<th style="text-align: center;">Grants permission to do the following:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: center;"><code dir="ltr" translate="no">       dataplex.datascans.create      </code></td>
<td style="text-align: center;">Create a <code dir="ltr" translate="no">       DataScan      </code></td>
</tr>
<tr class="even">
<td style="text-align: center;"><code dir="ltr" translate="no">       dataplex.datascans.delete      </code></td>
<td style="text-align: center;">Delete a <code dir="ltr" translate="no">       DataScan      </code></td>
</tr>
<tr class="odd">
<td style="text-align: center;"><code dir="ltr" translate="no">       dataplex.datascans.get      </code></td>
<td style="text-align: center;">View operational metadata such as ID or schedule, but not results and rules</td>
</tr>
<tr class="even">
<td style="text-align: center;"><code dir="ltr" translate="no">       dataplex.datascans.getData      </code></td>
<td style="text-align: center;">View <code dir="ltr" translate="no">       DataScan      </code> details including rules and results</td>
</tr>
<tr class="odd">
<td style="text-align: center;"><code dir="ltr" translate="no">       dataplex.datascans.list      </code></td>
<td style="text-align: center;">List <code dir="ltr" translate="no">       DataScan      </code> s</td>
</tr>
<tr class="even">
<td style="text-align: center;"><code dir="ltr" translate="no">       dataplex.datascans.run      </code></td>
<td style="text-align: center;">Run a <code dir="ltr" translate="no">       DataScan      </code></td>
</tr>
<tr class="odd">
<td style="text-align: center;"><code dir="ltr" translate="no">       dataplex.datascans.update      </code></td>
<td style="text-align: center;">Update the description of a <code dir="ltr" translate="no">       DataScan      </code></td>
</tr>
<tr class="even">
<td style="text-align: center;"><code dir="ltr" translate="no">       dataplex.datascans.getIamPolicy      </code></td>
<td style="text-align: center;">View the current IAM permissions on the scan</td>
</tr>
<tr class="odd">
<td style="text-align: center;"><code dir="ltr" translate="no">       dataplex.datascans.setIamPolicy      </code></td>
<td style="text-align: center;">Set IAM permissions on the scan</td>
</tr>
</tbody>
</table>

## Create a data quality scan

### Console

1.  In the Google Cloud console, on the BigQuery **Metadata curation** page, go to the **Data profiling & quality** tab.

2.  Click **Create data quality scan** .

3.  In the **Define scan** window, fill in the following fields:
    
    1.  Optional: Enter a **Display name** .
    
    2.  Enter an **ID** . See the [resource naming conventions](/compute/docs/naming-resources#resource-name-format) .
    
    3.  Optional: Enter a **Description** .
    
    4.  In the **Table** field, click **Browse** . Choose the table to scan, and then click **Select** . Only standard BigQuery tables are supported.
        
        For tables in multi-region datasets, choose a region where to create the data scan.
        
        To browse the tables organized within Dataplex Universal Catalog lakes, click **Browse within Dataplex Lakes** .
    
    5.  In the **Scope** field, choose **Incremental** or **Entire data** .
        
          - If you choose **Incremental** : In the **Timestamp column** field, select a column of type `  DATE  ` or `  TIMESTAMP  ` from your BigQuery table that increases as new records are added, and that can be used to identify new records. It can be a column that partitions the table.
    
    6.  To filter your data, select the **Filter rows** checkbox. Provide a row filter consisting of a valid SQL expression that can be used as a part of a [`  WHERE  ` clause in GoogleSQL syntax](/bigquery/docs/reference/standard-sql/query-syntax#where_clause) . For example, `  col1 >= 0  ` . The filter can be a combination of multiple column conditions. For example, `  col1 >= 0 AND col2 < 10  ` .
    
    7.  To sample your data, in the **Sampling size** list, select a sampling percentage. Choose a percentage value that ranges between 0.0% and 100.0% with up to 3 decimal digits. For larger datasets, choose a lower sampling percentage. For example, for a 1 PB table, if you enter a value between 0.1% and 1.0%, the data quality scan samples between 1-10 TB of data. For incremental data scans, the data quality scan applies sampling to the latest increment.
    
    8.  To publish the data quality scan results as Dataplex Universal Catalog metadata, select the **Publish results to Dataplex Catalog** checkbox.
        
        You can view the latest scan results on the **Data quality** tab in the BigQuery and Dataplex Universal Catalog pages for the source table. To enable users to access the published scan results, see the [Grant access to data quality scan results](#share-results) section of this document.
    
    9.  In the **Schedule** section, choose one of the following options:
        
          - **Repeat** : Run the data quality scan on a schedule: hourly, daily, weekly, monthly, or custom. Specify how often the scan runs and at what time. If you choose custom, use [cron](https://en.wikipedia.org/wiki/Cron) format to specify the schedule.
        
          - **On-demand** : Run the data quality scan on demand.
        
          - **One-time** : Run the data quality scan once now, and remove the scan after the time-to-live period.
        
          - **Time to live** : The time-to-live value is the time span between when the scan is executed and when the scan is deleted. A data quality scan without a specified time-to-live is automatically deleted 24 hours after its execution. The time-to-live can range from 0 seconds (immediate deletion) to 365 days.
    
    10. Click **Continue** .

4.  In the **Data quality rules** window, define the rules to configure for this data quality scan.
    
    1.  Click **Add rules** , and then choose from the following options.
        
          - **Profile based recommendations** : Build rules from the recommendations based on an existing data profiling scan.
            
            1.  **Choose columns** : Select the columns to get recommended rules for.
            
            2.  **Choose scan project** : If the data profiling scan is in a different project than the project where you are creating the data quality scan, then select the project to pull profile scans from.
            
            3.  **Choose profile results** : Select one or more profile results and then click **OK** . This populates a list of suggested rules that you can use as a starting point.
            
            4.  Select the checkbox for the rules that you want to add, and then click **Select** . Once selected, the rules are added to your current rule list. Then, you can edit the rules.
        
          - **Built-in rule types** : Build rules from predefined rules. See the list of [predefined rules](/dataplex/docs/auto-data-quality-overview#predefined-rules) .
            
            1.  **Choose columns** : Select the columns to select rules for.
            
            2.  **Choose rule types** : Select the rule types that you want to choose from, and then click **OK** . The rule types that appear depend on the columns that you selected.
            
            3.  Select the checkbox for the rules that you want to add, and then click **Select** . Once selected, the rules are added to your current rules list. Then, you can edit the rules.
        
          - **SQL row check rule** : Create a custom SQL rule to apply to each row.
            
            1.  In **Dimension** , choose one dimension.
            
            2.  In **Passing threshold** , choose a percentage of records that must pass the check.
            
            3.  In **Column name** , choose a column.
            
            4.  In the **Provide a SQL expression** field, enter a SQL expression that evaluates to a boolean `  true  ` (pass) or `  false  ` (fail). For more information, see [Supported custom SQL rule types](/dataplex/docs/auto-data-quality-overview#supported-custom-sql-rule-types) and the examples in [Define data quality rules](/dataplex/docs/use-auto-data-quality#sample-rules) .
            
            5.  Click **Add** .
        
          - **SQL aggregate check rule** : Create a custom SQL table condition rule.
            
            1.  In **Dimension** , choose one dimension.
            
            2.  In **Column name** , choose a column.
            
            3.  In the **Provide a SQL expression** field, enter a SQL expression that evaluates to a boolean `  true  ` (pass) or `  false  ` (fail). For more information, see [Supported custom SQL rule types](/dataplex/docs/auto-data-quality-overview#supported-custom-sql-rule-types) and the examples in [Define data quality rules](/dataplex/docs/use-auto-data-quality#sample-rules) .
            
            4.  Click **Add** .
        
          - **SQL assertion rule** : Create a custom SQL assertion rule to check for an invalid state of the data.
            
            1.  In **Dimension** , choose one dimension.
            
            2.  Optional: In **Column name** , choose a column.
            
            3.  In the **Provide a SQL statement** field, enter a SQL statement that returns rows that match the invalid state. If any rows are returned, this rule fails. Omit the trailing semicolon from the SQL statement. For more information, see [Supported custom SQL rule types](/dataplex/docs/auto-data-quality-overview#supported-custom-sql-rule-types) and the examples in [Define data quality rules](/dataplex/docs/use-auto-data-quality#sample-rules) .
            
            4.  Click **Add** .
    
    2.  Optional: For any data quality rule, you can assign a custom rule name to use for monitoring and alerting, and a description. To do this, edit a rule and specify the following details:
        
          - **Rule name** : Enter a custom rule name with up to 63 characters. The rule name can include letters (a-z, A-Z), digits (0-9), and hyphens (-) and must start with a letter and end with a number or a letter.
          - **Description** : Enter a rule description with a maximum length of 1,024 characters.
    
    3.  Repeat the previous steps to add additional rules to the data quality scan. When finished, click **Continue** .

5.  Optional: Export the scan results to a BigQuery standard table. In the **Export scan results to BigQuery table** section, do the following:
    
    1.  In the **Select BigQuery dataset** field, click **Browse** . Select a BigQuery dataset to store the data quality scan results.
    
    2.  In the **BigQuery table** field, specify the table to store the data quality scan results. If you're using an existing table, make sure that it is compatible with the [export table schema](/dataplex/docs/use-auto-data-quality#table-schema) . If the specified table doesn't exist, Dataplex Universal Catalog creates it for you.
        
        **Note:** You can use the same results table for multiple data quality scans.

6.  Optional: Add labels. Labels are key-value pairs that let you group related objects together or with other Google Cloud resources.

7.  Optional: Set up email notification reports to alert people about the status and results of a data quality scan job. In the **Notification report** section, click add **Add email ID** and enter up to five email addresses. Then, select the scenarios that you want to send reports for:
    
      - **Quality score (\<=)** : sends a report when a job succeeds with a data quality score that is lower than the specified target score. Enter a target quality score between 0 and 100.
      - **Job failures** : sends a report when the job itself fails, regardless of the data quality results.
      - **Job completion (success or failure)** : sends a report when the job ends, regardless of the data quality results.

8.  Click **Create** .
    
    After the scan is created, you can run it at any time by clicking **Run now** .

### gcloud

To create a data quality scan, use the [`  gcloud dataplex datascans create data-quality  ` command](/sdk/gcloud/reference/dataplex/datascans/create/data-quality) .

If the source data is organized in a Dataplex Universal Catalog lake, include the `  --data-source-entity  ` flag:

``` text
gcloud dataplex datascans create data-quality DATASCAN \
    --location=LOCATION \
    --data-quality-spec-file=DATA_QUALITY_SPEC_FILE \
    --data-source-entity=DATA_SOURCE_ENTITY
```

If the source data isn't organized in a Dataplex Universal Catalog lake, include the `  --data-source-resource  ` flag:

``` text
gcloud dataplex datascans create data-quality DATASCAN \
    --location=LOCATION \
    --data-quality-spec-file=DATA_QUALITY_SPEC_FILE \
    --data-source-resource=DATA_SOURCE_RESOURCE
```

Replace the following variables:

  - `  DATASCAN  ` : The name of the data quality scan.
  - `  LOCATION  ` : The Google Cloud region in which to create the data quality scan.
  - `  DATA_QUALITY_SPEC_FILE  ` : The path to the JSON or YAML file containing the specifications for the data quality scan. The file can be a local file or a Cloud Storage path with the prefix `  gs://  ` . Use this file to specify the data quality rules for the scan. You can also specify additional details in this file, such as filters, sampling percent, and post-scan actions like exporting to BigQuery or sending email notification reports. See the [documentation for JSON representation](/dataplex/docs/reference/rest/v1/DataQualitySpec) and the [example YAML representation](/dataplex/docs/use-auto-data-quality#create-scan-using-gcloud) .
  - `  DATA_SOURCE_ENTITY  ` : The Dataplex Universal Catalog entity that contains the data for the data quality scan. For example, `  projects/test-project/locations/test-location/lakes/test-lake/zones/test-zone/entities/test-entity  ` .
  - `  DATA_SOURCE_RESOURCE  ` : The name of the resource that contains the data for the data quality scan. For example, `  //bigquery.googleapis.com/projects/test-project/datasets/test-dataset/tables/test-table  ` .

### C\#

### C\#

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
using Google.Api.Gax.ResourceNames;
using Google.Cloud.Dataplex.V1;
using Google.LongRunning;

public sealed partial class GeneratedDataScanServiceClientSnippets
{
    /// <summary>Snippet for CreateDataScan</summary>
    /// <remarks>
    /// This snippet has been automatically generated and should be regarded as a code template only.
    /// It will require modifications to work:
    /// - It may require correct/in-range values for request initialization.
    /// - It may require specifying regional endpoints when creating the service client as shown in
    ///   https://cloud.google.com/dotnet/docs/reference/help/client-configuration#endpoint.
    /// </remarks>
    public void CreateDataScanRequestObject()
    {
        // Create client
        DataScanServiceClient dataScanServiceClient = DataScanServiceClient.Create();
        // Initialize request argument(s)
        CreateDataScanRequest request = new CreateDataScanRequest
        {
            ParentAsLocationName = LocationName.FromProjectLocation("[PROJECT]", "[LOCATION]"),
            DataScan = new DataScan(),
            DataScanId = "",
            ValidateOnly = false,
        };
        // Make the request
        Operation<DataScan, OperationMetadata> response = dataScanServiceClient.CreateDataScan(request);

        // Poll until the returned long-running operation is complete
        Operation<DataScan, OperationMetadata> completedResponse = response.PollUntilCompleted();
        // Retrieve the operation result
        DataScan result = completedResponse.Result;

        // Or get the name of the operation
        string operationName = response.Name;
        // This name can be stored, then the long-running operation retrieved later by name
        Operation<DataScan, OperationMetadata> retrievedResponse = dataScanServiceClient.PollOnceCreateDataScan(operationName);
        // Check if the retrieved long-running operation has completed
        if (retrievedResponse.IsCompleted)
        {
            // If it has completed, then access the result
            DataScan retrievedResult = retrievedResponse.Result;
        }
    }
}
```

### Go

### Go

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
package main

import (
 "context"

 dataplex "cloud.google.com/go/dataplex/apiv1"
 dataplexpb "cloud.google.com/go/dataplex/apiv1/dataplexpb"
)

func main() {
 ctx := context.Background()
 // This snippet has been automatically generated and should be regarded as a code template only.
 // It will require modifications to work:
 // - It may require correct/in-range values for request initialization.
 // - It may require specifying regional endpoints when creating the service client as shown in:
 //   https://pkg.go.dev/cloud.google.com/go#hdr-Client_Options
 c, err := dataplex.NewDataScanClient(ctx)
 if err != nil {
     // TODO: Handle error.
 }
 defer c.Close()

 req := &dataplexpb.CreateDataScanRequest{
     // TODO: Fill request struct fields.
     // See https://pkg.go.dev/cloud.google.com/go/dataplex/apiv1/dataplexpb#CreateDataScanRequest.
 }
 op, err := c.CreateDataScan(ctx, req)
 if err != nil {
     // TODO: Handle error.
 }

 resp, err := op.Wait(ctx)
 if err != nil {
     // TODO: Handle error.
 }
 // TODO: Use resp.
 _ = resp
}
```

### Java

### Java

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
import com.google.cloud.dataplex.v1.CreateDataScanRequest;
import com.google.cloud.dataplex.v1.DataScan;
import com.google.cloud.dataplex.v1.DataScanServiceClient;
import com.google.cloud.dataplex.v1.LocationName;

public class SyncCreateDataScan {

  public static void main(String[] args) throws Exception {
    syncCreateDataScan();
  }

  public static void syncCreateDataScan() throws Exception {
    // This snippet has been automatically generated and should be regarded as a code template only.
    // It will require modifications to work:
    // - It may require correct/in-range values for request initialization.
    // - It may require specifying regional endpoints when creating the service client as shown in
    // https://cloud.google.com/java/docs/setup#configure_endpoints_for_the_client_library
    try (DataScanServiceClient dataScanServiceClient = DataScanServiceClient.create()) {
      CreateDataScanRequest request =
          CreateDataScanRequest.newBuilder()
              .setParent(LocationName.of("[PROJECT]", "[LOCATION]").toString())
              .setDataScan(DataScan.newBuilder().build())
              .setDataScanId("dataScanId1260787906")
              .setValidateOnly(true)
              .build();
      DataScan response = dataScanServiceClient.createDataScanAsync(request).get();
    }
  }
}
```

### Node.js

### Node.js

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` javascript
// Copyright 2026 Google LLC
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
//
// ** This file is automatically generated by gapic-generator-typescript. **
// ** https://github.com/googleapis/gapic-generator-typescript **
// ** All changes to this file may be overwritten. **



'use strict';

function main(parent, dataScan, dataScanId) {
  /**
   * This snippet has been automatically generated and should be regarded as a code template only.
   * It will require modifications to work.
   * It may require correct/in-range values for request initialization.
   * TODO(developer): Uncomment these variables before running the sample.
   */
  /**
   *  Required. The resource name of the parent location:
   *  `projects/{project}/locations/{location_id}`
   *  where `project` refers to a *project_id* or *project_number* and
   *  `location_id` refers to a Google Cloud region.
   */
  // const parent = 'abc123'
  /**
   *  Required. DataScan resource.
   */
  // const dataScan = {}
  /**
   *  Required. DataScan identifier.
   *  * Must contain only lowercase letters, numbers and hyphens.
   *  * Must start with a letter.
   *  * Must end with a number or a letter.
   *  * Must be between 1-63 characters.
   *  * Must be unique within the customer project / location.
   */
  // const dataScanId = 'abc123'
  /**
   *  Optional. Only validate the request, but do not perform mutations.
   *  The default is `false`.
   */
  // const validateOnly = true

  // Imports the Dataplex library
  const {DataScanServiceClient} = require('@google-cloud/dataplex').v1;

  // Instantiates a client
  const dataplexClient = new DataScanServiceClient();

  async function callCreateDataScan() {
    // Construct request
    const request = {
      parent,
      dataScan,
      dataScanId,
    };

    // Run request
    const [operation] = await dataplexClient.createDataScan(request);
    const [response] = await operation.promise();
    console.log(response);
  }

  callCreateDataScan();
}

process.on('unhandledRejection', err => {
  console.error(err.message);
  process.exitCode = 1;
});
main(...process.argv.slice(2));
```

### Python

### Python

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
#   client as shown in:
#   https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import dataplex_v1


def sample_create_data_scan():
    # Create a client
    client = dataplex_v1.DataScanServiceClient()

    # Initialize request argument(s)
    data_scan = dataplex_v1.DataScan()
    data_scan.data_quality_spec.rules.dimension = "dimension_value"
    data_scan.data.entity = "entity_value"

    request = dataplex_v1.CreateDataScanRequest(
        parent="parent_value",
        data_scan=data_scan,
        data_scan_id="data_scan_id_value",
    )

    # Make the request
    operation = client.create_data_scan(request=request)

    print("Waiting for operation to complete...")

    response = operation.result()

    # Handle the response
    print(response)
```

### Ruby

### Ruby

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
require "google/cloud/dataplex/v1"

##
# Snippet for the create_data_scan call in the DataScanService service
#
# This snippet has been automatically generated and should be regarded as a code
# template only. It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in https://cloud.google.com/ruby/docs/reference.
#
# This is an auto-generated example demonstrating basic usage of
# Google::Cloud::Dataplex::V1::DataScanService::Client#create_data_scan.
#
def create_data_scan
  # Create a client object. The client can be reused for multiple calls.
  client = Google::Cloud::Dataplex::V1::DataScanService::Client.new

  # Create a request. To set request fields, pass in keyword arguments.
  request = Google::Cloud::Dataplex::V1::CreateDataScanRequest.new

  # Call the create_data_scan method.
  result = client.create_data_scan request

  # The returned object is of type Gapic::Operation. You can use it to
  # check the status of an operation, cancel it, or wait for results.
  # Here is how to wait for a response.
  result.wait_until_done! timeout: 60
  if result.response?
    p result.response
  else
    puts "No response received."
  end
end
```

### REST

To create a data quality scan, use the [`  dataScans.create  ` method](/dataplex/docs/reference/rest/v1/projects.locations.dataScans/create) .

The following request creates a one-time data quality scan:

``` text
POST https://dataplex.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/dataScans?data_scan_id=DATASCAN_ID

{
"data": {
  "resource": "//bigquery.googleapis.com/projects/PROJECT_ID/datasets/DATASET_ID/tables/TABLE_ID"
},
"type": "DATA_QUALITY",
"executionSpec": {
  "trigger": {
    "oneTime": {
      "ttl_after_scan_completion": "120s"
    }
  }
},
"dataQualitySpec": {
  "rules": [
    {
      "nonNullExpectation": {},
      "column": "COLUMN_NAME",
      "dimension": "DIMENSION",
      "threshold": 1
    }
  ]
}
}
```

Replace the following:

  - `  PROJECT_ID  ` : Your project ID.
  - `  LOCATION  ` : The region where to create the data quality scan.
  - `  DATASCAN_ID  ` : The ID of the data quality scan.
  - `  DATASET_ID  ` : The ID of BigQuery dataset.
  - `  TABLE_ID  ` : The ID of BigQuery table.
  - `  COLUMN_NAME  ` : The column name for the rule.
  - `  DIMENSION  ` : The dimension for the rule, for example `  VALIDITY  ` .

If you want to build rules for the data quality scan by using rule recommendations that are based on the results of a data profiling scan, get the recommendations by calling the [`  dataScans.jobs.generateDataQualityRules  ` method](/dataplex/docs/reference/rest/v1/projects.locations.dataScans.jobs/generateDataQualityRules) on the data profiling scan.

**Note:** If your BigQuery table is configured with the **Require partition filter** set to `  true  ` , use the BigQuery partition column as the data quality scan row filter or timestamp column.

## Run a data quality scan

### Console

1.  In the Google Cloud console, on the BigQuery **Metadata curation** page, go to the **Data profiling & quality** tab.

2.  Click the data quality scan to run.

3.  Click **Run now** .

### gcloud

To run a data quality scan, use the [`  gcloud dataplex datascans run  ` command](/sdk/gcloud/reference/dataplex/datascans/run) :

``` text
gcloud dataplex datascans run DATASCAN \
--location=LOCATION \
```

Replace the following variables:

  - `  LOCATION  ` : The Google Cloud region in which the data quality scan was created.
  - `  DATASCAN  ` : The name of the data quality scan.

### C\#

### C\#

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
using Google.Cloud.Dataplex.V1;

public sealed partial class GeneratedDataScanServiceClientSnippets
{
    /// <summary>Snippet for RunDataScan</summary>
    /// <remarks>
    /// This snippet has been automatically generated and should be regarded as a code template only.
    /// It will require modifications to work:
    /// - It may require correct/in-range values for request initialization.
    /// - It may require specifying regional endpoints when creating the service client as shown in
    ///   https://cloud.google.com/dotnet/docs/reference/help/client-configuration#endpoint.
    /// </remarks>
    public void RunDataScanRequestObject()
    {
        // Create client
        DataScanServiceClient dataScanServiceClient = DataScanServiceClient.Create();
        // Initialize request argument(s)
        RunDataScanRequest request = new RunDataScanRequest
        {
            DataScanName = DataScanName.FromProjectLocationDataScan("[PROJECT]", "[LOCATION]", "[DATASCAN]"),
        };
        // Make the request
        RunDataScanResponse response = dataScanServiceClient.RunDataScan(request);
    }
}
```

### Go

### Go

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
package main

import (
 "context"

 dataplex "cloud.google.com/go/dataplex/apiv1"
 dataplexpb "cloud.google.com/go/dataplex/apiv1/dataplexpb"
)

func main() {
 ctx := context.Background()
 // This snippet has been automatically generated and should be regarded as a code template only.
 // It will require modifications to work:
 // - It may require correct/in-range values for request initialization.
 // - It may require specifying regional endpoints when creating the service client as shown in:
 //   https://pkg.go.dev/cloud.google.com/go#hdr-Client_Options
 c, err := dataplex.NewDataScanClient(ctx)
 if err != nil {
     // TODO: Handle error.
 }
 defer c.Close()

 req := &dataplexpb.RunDataScanRequest{
     // TODO: Fill request struct fields.
     // See https://pkg.go.dev/cloud.google.com/go/dataplex/apiv1/dataplexpb#RunDataScanRequest.
 }
 resp, err := c.RunDataScan(ctx, req)
 if err != nil {
     // TODO: Handle error.
 }
 // TODO: Use resp.
 _ = resp
}
```

### Java

### Java

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
import com.google.cloud.dataplex.v1.DataScanName;
import com.google.cloud.dataplex.v1.DataScanServiceClient;
import com.google.cloud.dataplex.v1.RunDataScanRequest;
import com.google.cloud.dataplex.v1.RunDataScanResponse;

public class SyncRunDataScan {

  public static void main(String[] args) throws Exception {
    syncRunDataScan();
  }

  public static void syncRunDataScan() throws Exception {
    // This snippet has been automatically generated and should be regarded as a code template only.
    // It will require modifications to work:
    // - It may require correct/in-range values for request initialization.
    // - It may require specifying regional endpoints when creating the service client as shown in
    // https://cloud.google.com/java/docs/setup#configure_endpoints_for_the_client_library
    try (DataScanServiceClient dataScanServiceClient = DataScanServiceClient.create()) {
      RunDataScanRequest request =
          RunDataScanRequest.newBuilder()
              .setName(DataScanName.of("[PROJECT]", "[LOCATION]", "[DATASCAN]").toString())
              .build();
      RunDataScanResponse response = dataScanServiceClient.runDataScan(request);
    }
  }
}
```

### Python

### Python

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
#   client as shown in:
#   https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import dataplex_v1


def sample_run_data_scan():
    # Create a client
    client = dataplex_v1.DataScanServiceClient()

    # Initialize request argument(s)
    request = dataplex_v1.RunDataScanRequest(
        name="name_value",
    )

    # Make the request
    response = client.run_data_scan(request=request)

    # Handle the response
    print(response)
```

### Ruby

### Ruby

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
require "google/cloud/dataplex/v1"

##
# Snippet for the run_data_scan call in the DataScanService service
#
# This snippet has been automatically generated and should be regarded as a code
# template only. It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in https://cloud.google.com/ruby/docs/reference.
#
# This is an auto-generated example demonstrating basic usage of
# Google::Cloud::Dataplex::V1::DataScanService::Client#run_data_scan.
#
def run_data_scan
  # Create a client object. The client can be reused for multiple calls.
  client = Google::Cloud::Dataplex::V1::DataScanService::Client.new

  # Create a request. To set request fields, pass in keyword arguments.
  request = Google::Cloud::Dataplex::V1::RunDataScanRequest.new

  # Call the run_data_scan method.
  result = client.run_data_scan request

  # The returned object is of type Google::Cloud::Dataplex::V1::RunDataScanResponse.
  p result
end
```

### REST

To run a data quality scan, use the [`  dataScans.run  ` method](/dataplex/docs/reference/rest/v1/projects.locations.dataScans/run) .

**Note:** Run isn't supported for data quality scans that are on a one-time schedule.

## View data quality scan results

### Console

1.  In the Google Cloud console, on the BigQuery **Metadata curation** page, go to the **Data profiling & quality** tab.

2.  Click the name of a data quality scan.
    
      - The **Overview** section displays information about the most recent jobs, including when the scan was run, the number of records scanned in each job, whether all the data quality checks passed, and if there were failures, the number of data quality checks that failed.
    
      - The **Data quality scan configuration** section displays details about the scan.

3.  To see detailed information about a job, such as data quality scores that indicate the percentage of rules that passed, which rules failed, and the job logs, click the **Jobs history** tab. Then, click a job ID.

**Note:** If you exported the scan results to a BigQuery table, then you can also access the scan results from the table. The data quality scores are available if you published the scan results as Dataplex Universal Catalog metadata.

### gcloud

To view the results of a data quality scan job, use the [`  gcloud dataplex datascans jobs describe  ` command](/sdk/gcloud/reference/dataplex/datascans/jobs/describe) :

``` text
gcloud dataplex datascans jobs describe JOB \
--location=LOCATION \
--datascan=DATASCAN \
--view=FULL
```

Replace the following variables:

  - `  JOB  ` : The job ID of the data quality scan job.
  - `  LOCATION  ` : The Google Cloud region in which the data quality scan was created.
  - `  DATASCAN  ` : The name of the data quality scan the job belongs to.
  - `  --view=FULL  ` : To see the scan job result, specify `  FULL  ` .

### C\#

### C\#

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
using Google.Cloud.Dataplex.V1;

public sealed partial class GeneratedDataScanServiceClientSnippets
{
    /// <summary>Snippet for GetDataScan</summary>
    /// <remarks>
    /// This snippet has been automatically generated and should be regarded as a code template only.
    /// It will require modifications to work:
    /// - It may require correct/in-range values for request initialization.
    /// - It may require specifying regional endpoints when creating the service client as shown in
    ///   https://cloud.google.com/dotnet/docs/reference/help/client-configuration#endpoint.
    /// </remarks>
    public void GetDataScanRequestObject()
    {
        // Create client
        DataScanServiceClient dataScanServiceClient = DataScanServiceClient.Create();
        // Initialize request argument(s)
        GetDataScanRequest request = new GetDataScanRequest
        {
            DataScanName = DataScanName.FromProjectLocationDataScan("[PROJECT]", "[LOCATION]", "[DATASCAN]"),
            View = GetDataScanRequest.Types.DataScanView.Unspecified,
        };
        // Make the request
        DataScan response = dataScanServiceClient.GetDataScan(request);
    }
}
```

### Go

### Go

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
package main

import (
 "context"

 dataplex "cloud.google.com/go/dataplex/apiv1"
 dataplexpb "cloud.google.com/go/dataplex/apiv1/dataplexpb"
)

func main() {
 ctx := context.Background()
 // This snippet has been automatically generated and should be regarded as a code template only.
 // It will require modifications to work:
 // - It may require correct/in-range values for request initialization.
 // - It may require specifying regional endpoints when creating the service client as shown in:
 //   https://pkg.go.dev/cloud.google.com/go#hdr-Client_Options
 c, err := dataplex.NewDataScanClient(ctx)
 if err != nil {
     // TODO: Handle error.
 }
 defer c.Close()

 req := &dataplexpb.GetDataScanRequest{
     // TODO: Fill request struct fields.
     // See https://pkg.go.dev/cloud.google.com/go/dataplex/apiv1/dataplexpb#GetDataScanRequest.
 }
 resp, err := c.GetDataScan(ctx, req)
 if err != nil {
     // TODO: Handle error.
 }
 // TODO: Use resp.
 _ = resp
}
```

### Java

### Java

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
import com.google.cloud.dataplex.v1.DataScan;
import com.google.cloud.dataplex.v1.DataScanName;
import com.google.cloud.dataplex.v1.DataScanServiceClient;
import com.google.cloud.dataplex.v1.GetDataScanRequest;

public class SyncGetDataScan {

  public static void main(String[] args) throws Exception {
    syncGetDataScan();
  }

  public static void syncGetDataScan() throws Exception {
    // This snippet has been automatically generated and should be regarded as a code template only.
    // It will require modifications to work:
    // - It may require correct/in-range values for request initialization.
    // - It may require specifying regional endpoints when creating the service client as shown in
    // https://cloud.google.com/java/docs/setup#configure_endpoints_for_the_client_library
    try (DataScanServiceClient dataScanServiceClient = DataScanServiceClient.create()) {
      GetDataScanRequest request =
          GetDataScanRequest.newBuilder()
              .setName(DataScanName.of("[PROJECT]", "[LOCATION]", "[DATASCAN]").toString())
              .build();
      DataScan response = dataScanServiceClient.getDataScan(request);
    }
  }
}
```

### Python

### Python

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
#   client as shown in:
#   https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import dataplex_v1


def sample_get_data_scan():
    # Create a client
    client = dataplex_v1.DataScanServiceClient()

    # Initialize request argument(s)
    request = dataplex_v1.GetDataScanRequest(
        name="name_value",
    )

    # Make the request
    response = client.get_data_scan(request=request)

    # Handle the response
    print(response)
```

### Ruby

### Ruby

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
require "google/cloud/dataplex/v1"

##
# Snippet for the get_data_scan call in the DataScanService service
#
# This snippet has been automatically generated and should be regarded as a code
# template only. It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in https://cloud.google.com/ruby/docs/reference.
#
# This is an auto-generated example demonstrating basic usage of
# Google::Cloud::Dataplex::V1::DataScanService::Client#get_data_scan.
#
def get_data_scan
  # Create a client object. The client can be reused for multiple calls.
  client = Google::Cloud::Dataplex::V1::DataScanService::Client.new

  # Create a request. To set request fields, pass in keyword arguments.
  request = Google::Cloud::Dataplex::V1::GetDataScanRequest.new

  # Call the get_data_scan method.
  result = client.get_data_scan request

  # The returned object is of type Google::Cloud::Dataplex::V1::DataScan.
  p result
end
```

### REST

To view the results of a data quality scan, use the [`  dataScans.get  ` method](/dataplex/docs/reference/rest/v1/projects.locations.dataScans/get) .

### View published results

If the data quality scan results are published as Dataplex Universal Catalog metadata, then you can see the latest scan results on the BigQuery and Dataplex Universal Catalog pages in the Google Cloud console, on the source table's **Data quality** tab.

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :
    
    If you don't see the left pane, click last\_page **Expand left pane** to open the pane.

3.  In the **Explorer** pane, click **Datasets** , and then click your dataset.

4.  Click **Overview \> Tables** , and then select the table whose data quality scan results you want to see.

5.  Click the **Data quality** tab.
    
    The latest published results are displayed.
    
    **Note:** Published results might not be available if a scan is running for the first time.

### View historical scan results

Dataplex Universal Catalog saves the data quality scan history of the last 300 jobs or for the past year, whichever occurs first.

### Console

1.  In the Google Cloud console, on the BigQuery **Metadata curation** page, go to the **Data profiling & quality** tab.

2.  Click the name of a data quality scan.

3.  Click the **Jobs history** tab.
    
    The **Jobs history** tab provides information about past jobs, such as the number of records scanned in each job, the job status, the time the job was run, and whether each rule passed or failed.

4.  To view detailed information about a job, click any of the jobs in the **Job ID** column.

### gcloud

To view historical data quality scan jobs, use the [`  gcloud dataplex datascans jobs list  ` command](/sdk/gcloud/reference/dataplex/datascans/jobs/list) :

``` text
gcloud dataplex datascans jobs list \
--location=LOCATION \
--datascan=DATASCAN \
```

Replace the following variables:

  - `  LOCATION  ` : The Google Cloud region in which the data quality scan was created.
  - `  DATASCAN  ` : The name of the data quality scan to view historical jobs for.

### C\#

### C\#

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
using Google.Api.Gax;
using Google.Cloud.Dataplex.V1;
using System;

public sealed partial class GeneratedDataScanServiceClientSnippets
{
    /// <summary>Snippet for ListDataScanJobs</summary>
    /// <remarks>
    /// This snippet has been automatically generated and should be regarded as a code template only.
    /// It will require modifications to work:
    /// - It may require correct/in-range values for request initialization.
    /// - It may require specifying regional endpoints when creating the service client as shown in
    ///   https://cloud.google.com/dotnet/docs/reference/help/client-configuration#endpoint.
    /// </remarks>
    public void ListDataScanJobsRequestObject()
    {
        // Create client
        DataScanServiceClient dataScanServiceClient = DataScanServiceClient.Create();
        // Initialize request argument(s)
        ListDataScanJobsRequest request = new ListDataScanJobsRequest
        {
            ParentAsDataScanName = DataScanName.FromProjectLocationDataScan("[PROJECT]", "[LOCATION]", "[DATASCAN]"),
            Filter = "",
        };
        // Make the request
        PagedEnumerable<ListDataScanJobsResponse, DataScanJob> response = dataScanServiceClient.ListDataScanJobs(request);

        // Iterate over all response items, lazily performing RPCs as required
        foreach (DataScanJob item in response)
        {
            // Do something with each item
            Console.WriteLine(item);
        }

        // Or iterate over pages (of server-defined size), performing one RPC per page
        foreach (ListDataScanJobsResponse page in response.AsRawResponses())
        {
            // Do something with each page of items
            Console.WriteLine("A page of results:");
            foreach (DataScanJob item in page)
            {
                // Do something with each item
                Console.WriteLine(item);
            }
        }

        // Or retrieve a single page of known size (unless it's the final page), performing as many RPCs as required
        int pageSize = 10;
        Page<DataScanJob> singlePage = response.ReadPage(pageSize);
        // Do something with the page of items
        Console.WriteLine($"A page of {pageSize} results (unless it's the final page):");
        foreach (DataScanJob item in singlePage)
        {
            // Do something with each item
            Console.WriteLine(item);
        }
        // Store the pageToken, for when the next page is required.
        string nextPageToken = singlePage.NextPageToken;
    }
}
```

### Go

### Go

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
package main

import (
 "context"

 dataplex "cloud.google.com/go/dataplex/apiv1"
 dataplexpb "cloud.google.com/go/dataplex/apiv1/dataplexpb"
 "google.golang.org/api/iterator"
)

func main() {
 ctx := context.Background()
 // This snippet has been automatically generated and should be regarded as a code template only.
 // It will require modifications to work:
 // - It may require correct/in-range values for request initialization.
 // - It may require specifying regional endpoints when creating the service client as shown in:
 //   https://pkg.go.dev/cloud.google.com/go#hdr-Client_Options
 c, err := dataplex.NewDataScanClient(ctx)
 if err != nil {
     // TODO: Handle error.
 }
 defer c.Close()

 req := &dataplexpb.ListDataScanJobsRequest{
     // TODO: Fill request struct fields.
     // See https://pkg.go.dev/cloud.google.com/go/dataplex/apiv1/dataplexpb#ListDataScanJobsRequest.
 }
 it := c.ListDataScanJobs(ctx, req)
 for {
     resp, err := it.Next()
     if err == iterator.Done {
         break
     }
     if err != nil {
         // TODO: Handle error.
     }
     // TODO: Use resp.
     _ = resp

     // If you need to access the underlying RPC response,
     // you can do so by casting the `Response` as below.
     // Otherwise, remove this line. Only populated after
     // first call to Next(). Not safe for concurrent access.
     _ = it.Response.(*dataplexpb.ListDataScanJobsResponse)
 }
}
```

### Java

### Java

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
import com.google.cloud.dataplex.v1.DataScanJob;
import com.google.cloud.dataplex.v1.DataScanName;
import com.google.cloud.dataplex.v1.DataScanServiceClient;
import com.google.cloud.dataplex.v1.ListDataScanJobsRequest;

public class SyncListDataScanJobs {

  public static void main(String[] args) throws Exception {
    syncListDataScanJobs();
  }

  public static void syncListDataScanJobs() throws Exception {
    // This snippet has been automatically generated and should be regarded as a code template only.
    // It will require modifications to work:
    // - It may require correct/in-range values for request initialization.
    // - It may require specifying regional endpoints when creating the service client as shown in
    // https://cloud.google.com/java/docs/setup#configure_endpoints_for_the_client_library
    try (DataScanServiceClient dataScanServiceClient = DataScanServiceClient.create()) {
      ListDataScanJobsRequest request =
          ListDataScanJobsRequest.newBuilder()
              .setParent(DataScanName.of("[PROJECT]", "[LOCATION]", "[DATASCAN]").toString())
              .setPageSize(883849137)
              .setPageToken("pageToken873572522")
              .setFilter("filter-1274492040")
              .build();
      for (DataScanJob element : dataScanServiceClient.listDataScanJobs(request).iterateAll()) {
        // doThingsWith(element);
      }
    }
  }
}
```

### Python

### Python

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
#   client as shown in:
#   https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import dataplex_v1


def sample_list_data_scan_jobs():
    # Create a client
    client = dataplex_v1.DataScanServiceClient()

    # Initialize request argument(s)
    request = dataplex_v1.ListDataScanJobsRequest(
        parent="parent_value",
    )

    # Make the request
    page_result = client.list_data_scan_jobs(request=request)

    # Handle the response
    for response in page_result:
        print(response)
```

### Ruby

### Ruby

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
require "google/cloud/dataplex/v1"

##
# Snippet for the list_data_scan_jobs call in the DataScanService service
#
# This snippet has been automatically generated and should be regarded as a code
# template only. It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in https://cloud.google.com/ruby/docs/reference.
#
# This is an auto-generated example demonstrating basic usage of
# Google::Cloud::Dataplex::V1::DataScanService::Client#list_data_scan_jobs.
#
def list_data_scan_jobs
  # Create a client object. The client can be reused for multiple calls.
  client = Google::Cloud::Dataplex::V1::DataScanService::Client.new

  # Create a request. To set request fields, pass in keyword arguments.
  request = Google::Cloud::Dataplex::V1::ListDataScanJobsRequest.new

  # Call the list_data_scan_jobs method.
  result = client.list_data_scan_jobs request

  # The returned object is of type Gapic::PagedEnumerable. You can iterate
  # over elements, and API calls will be issued to fetch pages as needed.
  result.each do |item|
    # Each element is of type ::Google::Cloud::Dataplex::V1::DataScanJob.
    p item
  end
end
```

### REST

To view historical data quality scan jobs, use the [`  dataScans.jobs.list  ` method](/dataplex/docs/reference/rest/v1/projects.locations.dataScans.jobs/list) .

## Grant access to data quality scan results

To enable the users in your organization to view the scan results, do the following:

1.  In the Google Cloud console, on the BigQuery **Metadata curation** page, go to the **Data profiling & quality** tab.

2.  Click the data quality scan you want to share the results of.

3.  Click the **Permissions** tab.

4.  Do the following:
    
      - To grant access to a principal, click person\_add **Grant access** . Grant the **Dataplex DataScan DataViewer** role to the associated principal.
      - To remove access from a principal, select the principal that you want to remove the **Dataplex DataScan DataViewer** role from. Click person\_remove **Remove access** , and then confirm when prompted.

## Troubleshoot a data quality failure

You can set alerts for data quality failures using the logs in Cloud Logging. For more information, including sample queries, see [Set alerts in Cloud Logging](/dataplex/docs/use-auto-data-quality#set-alerts) .

For each job with row-level rules that fail, Dataplex Universal Catalog provides a query to get the failed records. Run this query to see the records that did not match your rule.

**Note:** The query returns all of the columns of the table, not just the failed column.

### Console

1.  In the Google Cloud console, on the BigQuery **Metadata curation** page, go to the **Data profiling & quality** tab.

2.  Click the name of the data quality scan whose records you want to troubleshoot.

3.  Click the **Jobs history** tab.

4.  Click the job ID of the job that identified data quality failures.

5.  In the job results window that opens, in the **Rules** section, find the column **Query to get failed records** . Click **Copy query to clipboard** for the failed rule.

6.  [Run the query in BigQuery](/bigquery/docs/running-queries) to see the records that caused the job to fail.

### gcloud

Not supported.

### REST

1.  To get the job that identified the data quality failures, use the [`  dataScans.get  ` method](/dataplex/docs/reference/rest/v1/DataQualityResult) .
    
    In the response object, the `  failingRowsQuery  ` field shows the query.

2.  [Run the query in BigQuery](/bigquery/docs/running-queries) to see the records that caused the job to fail.

Dataplex Universal Catalog also runs the debug query, provided it was included during the rule creation. The debug query results are included in each rule's output. This feature is in [Preview](/products#product-launch-stages) .

### Console

Not supported.

### gcloud

Not supported.

### REST

To get the job that identified the data quality failures, use the [`  dataScans.get  ` method](/dataplex/docs/reference/rest/v1/DataQualityResult) . In the response object, the `  debugQueriesResultSets  ` field shows the results of the debug queries.

## Manage data quality scans for a specific table

The steps in this document show how to manage data quality scans across your project by using the BigQuery **Metadata curation \> Data profiling & quality** page in the Google Cloud console.

You can also create and manage data quality scans when working with a specific table. In the Google Cloud console, on the BigQuery page for the table, use the **Data quality** tab. Do the following:

1.  In the Google Cloud console, go to the **BigQuery** page.
    
    In the **Explorer** pane (in the left pane), click **Datasets** , and then click your dataset. Click **Overview \> Tables** , and then select the table whose data quality scan results you want to see.

2.  Click the **Data quality** tab.

3.  Depending on whether the table has a data quality scan whose results are published as Dataplex Universal Catalog metadata, you can work with the table's data quality scans in the following ways:
    
      - **Data quality scan results are published** : the latest scan results are displayed on the page.
        
        To manage the data quality scans for this table, click **Data quality scan** , and then select from the following options:
        
          - **Create new scan** : create a new data quality scan. For more information, see the [Create a data quality scan](#create-scan) section of this document. When you create a scan from a table's details page, the table is preselected.
        
          - **Run now** : run the scan.
        
          - **Edit scan configuration** : edit settings including the display name, filters, and schedule.
            
            To edit the data quality rules, on the **Data quality** tab, click the **Rules** tab. Click **Modify rules** . Update the rules and then click **Save** .
        
          - **Manage scan permissions** : control who can access the scan results. For more information, see the [Grant access to data quality scan results](#share-results) section of this document.
        
          - **View historical results** : view detailed information about previous data quality scan jobs. For more information, see the [View data quality scan results](#results) and [View historical scan results](#older-scans) sections of this document.
        
          - **View all scans** : view a list of data quality scans that apply to this table.
    
      - **Data quality scan results aren't published** : select from the following options:
        
          - **Create data quality scan** : create a new data quality scan. For more information, see the [Create a data quality scan](#create-scan) section of this document. When you create a scan from a table's details page, the table is preselected.
        
          - **View existing scans** : view a list of data quality scans that apply to this table.

## View the data quality scans for a table

To view the data quality scans that apply to a specific table, do the following:

1.  In the Google Cloud console, on the BigQuery **Metadata curation** page, go to the **Data profiling & quality** tab.

2.  Filter the list by table name and scan type.

## Update a data quality scan

You can edit various settings for an existing data quality scan, such as the display name, filters, schedule, and data quality rules.

**Note:** If an existing data quality scan publishes the results to the BigQuery and Dataplex Universal Catalog pages in the Google Cloud console, and you instead want to publish future scan results as Dataplex Universal Catalog metadata, you must edit the scan and re-enable publishing. You might need additional permissions to enable catalog publishing.

### Console

1.  In the Google Cloud console, on the BigQuery **Metadata curation** page, go to the **Data profiling & quality** tab.

2.  Click the name of a data quality scan.

3.  To edit settings including the display name, filters, and schedule, click **Edit** . Edit the values and then click **Save** .

4.  To edit the data quality rules, on the scan details page, click the **Current rules** tab. Click **Modify rules** . Update the rules and then click **Save** .

### gcloud

To update the description of a data quality scan, use the [`  gcloud dataplex datascans update data-quality  ` command](/sdk/gcloud/reference/dataplex/datascans/update/data-quality) :

``` text
gcloud dataplex datascans update data-quality DATASCAN \
--location=LOCATION \
--description=DESCRIPTION
```

Replace the following:

  - `  DATASCAN  ` : The name of the data quality scan to update.
  - `  LOCATION  ` : The Google Cloud region in which the data quality scan was created.
  - `  DESCRIPTION  ` : The new description for the data quality scan.

**Note:** You can update specification fields, such as `  rules  ` , `  rowFilter  ` , or `  samplingPercent  ` , in the data quality specification file. Refer to [JSON](/dataplex/docs/reference/rest/v1/DataQualitySpec) and [YAML](/dataplex/docs/use-auto-data-quality#create-scan-using-gcloud) representations.

### C\#

### C\#

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
using Google.Cloud.Dataplex.V1;
using Google.LongRunning;
using Google.Protobuf.WellKnownTypes;

public sealed partial class GeneratedDataScanServiceClientSnippets
{
    /// <summary>Snippet for UpdateDataScan</summary>
    /// <remarks>
    /// This snippet has been automatically generated and should be regarded as a code template only.
    /// It will require modifications to work:
    /// - It may require correct/in-range values for request initialization.
    /// - It may require specifying regional endpoints when creating the service client as shown in
    ///   https://cloud.google.com/dotnet/docs/reference/help/client-configuration#endpoint.
    /// </remarks>
    public void UpdateDataScanRequestObject()
    {
        // Create client
        DataScanServiceClient dataScanServiceClient = DataScanServiceClient.Create();
        // Initialize request argument(s)
        UpdateDataScanRequest request = new UpdateDataScanRequest
        {
            DataScan = new DataScan(),
            UpdateMask = new FieldMask(),
            ValidateOnly = false,
        };
        // Make the request
        Operation<DataScan, OperationMetadata> response = dataScanServiceClient.UpdateDataScan(request);

        // Poll until the returned long-running operation is complete
        Operation<DataScan, OperationMetadata> completedResponse = response.PollUntilCompleted();
        // Retrieve the operation result
        DataScan result = completedResponse.Result;

        // Or get the name of the operation
        string operationName = response.Name;
        // This name can be stored, then the long-running operation retrieved later by name
        Operation<DataScan, OperationMetadata> retrievedResponse = dataScanServiceClient.PollOnceUpdateDataScan(operationName);
        // Check if the retrieved long-running operation has completed
        if (retrievedResponse.IsCompleted)
        {
            // If it has completed, then access the result
            DataScan retrievedResult = retrievedResponse.Result;
        }
    }
}
```

### Go

### Go

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
package main

import (
 "context"

 dataplex "cloud.google.com/go/dataplex/apiv1"
 dataplexpb "cloud.google.com/go/dataplex/apiv1/dataplexpb"
)

func main() {
 ctx := context.Background()
 // This snippet has been automatically generated and should be regarded as a code template only.
 // It will require modifications to work:
 // - It may require correct/in-range values for request initialization.
 // - It may require specifying regional endpoints when creating the service client as shown in:
 //   https://pkg.go.dev/cloud.google.com/go#hdr-Client_Options
 c, err := dataplex.NewDataScanClient(ctx)
 if err != nil {
     // TODO: Handle error.
 }
 defer c.Close()

 req := &dataplexpb.UpdateDataScanRequest{
     // TODO: Fill request struct fields.
     // See https://pkg.go.dev/cloud.google.com/go/dataplex/apiv1/dataplexpb#UpdateDataScanRequest.
 }
 op, err := c.UpdateDataScan(ctx, req)
 if err != nil {
     // TODO: Handle error.
 }

 resp, err := op.Wait(ctx)
 if err != nil {
     // TODO: Handle error.
 }
 // TODO: Use resp.
 _ = resp
}
```

### Java

### Java

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
import com.google.cloud.dataplex.v1.DataScan;
import com.google.cloud.dataplex.v1.DataScanServiceClient;
import com.google.cloud.dataplex.v1.UpdateDataScanRequest;
import com.google.protobuf.FieldMask;

public class SyncUpdateDataScan {

  public static void main(String[] args) throws Exception {
    syncUpdateDataScan();
  }

  public static void syncUpdateDataScan() throws Exception {
    // This snippet has been automatically generated and should be regarded as a code template only.
    // It will require modifications to work:
    // - It may require correct/in-range values for request initialization.
    // - It may require specifying regional endpoints when creating the service client as shown in
    // https://cloud.google.com/java/docs/setup#configure_endpoints_for_the_client_library
    try (DataScanServiceClient dataScanServiceClient = DataScanServiceClient.create()) {
      UpdateDataScanRequest request =
          UpdateDataScanRequest.newBuilder()
              .setDataScan(DataScan.newBuilder().build())
              .setUpdateMask(FieldMask.newBuilder().build())
              .setValidateOnly(true)
              .build();
      DataScan response = dataScanServiceClient.updateDataScanAsync(request).get();
    }
  }
}
```

### Python

### Python

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
#   client as shown in:
#   https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import dataplex_v1


def sample_update_data_scan():
    # Create a client
    client = dataplex_v1.DataScanServiceClient()

    # Initialize request argument(s)
    data_scan = dataplex_v1.DataScan()
    data_scan.data_quality_spec.rules.dimension = "dimension_value"
    data_scan.data.entity = "entity_value"

    request = dataplex_v1.UpdateDataScanRequest(
        data_scan=data_scan,
    )

    # Make the request
    operation = client.update_data_scan(request=request)

    print("Waiting for operation to complete...")

    response = operation.result()

    # Handle the response
    print(response)
```

### Ruby

### Ruby

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
require "google/cloud/dataplex/v1"

##
# Snippet for the update_data_scan call in the DataScanService service
#
# This snippet has been automatically generated and should be regarded as a code
# template only. It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in https://cloud.google.com/ruby/docs/reference.
#
# This is an auto-generated example demonstrating basic usage of
# Google::Cloud::Dataplex::V1::DataScanService::Client#update_data_scan.
#
def update_data_scan
  # Create a client object. The client can be reused for multiple calls.
  client = Google::Cloud::Dataplex::V1::DataScanService::Client.new

  # Create a request. To set request fields, pass in keyword arguments.
  request = Google::Cloud::Dataplex::V1::UpdateDataScanRequest.new

  # Call the update_data_scan method.
  result = client.update_data_scan request

  # The returned object is of type Gapic::Operation. You can use it to
  # check the status of an operation, cancel it, or wait for results.
  # Here is how to wait for a response.
  result.wait_until_done! timeout: 60
  if result.response?
    p result.response
  else
    puts "No response received."
  end
end
```

### REST

To edit a data quality scan, use the [`  dataScans.patch  ` method](/dataplex/docs/reference/rest/v1/projects.locations.dataScans/patch) .

**Note:** Update isn't supported for data quality scans that are on a one-time schedule.

## Delete a data quality scan

### Console

### Console

1.  In the Google Cloud console, on the BigQuery **Metadata curation** page, go to the **Data profiling & quality** tab.

2.  Click the scan you want to delete.

3.  Click **Delete** , and then confirm when prompted.

### gcloud

### gcloud

To delete a data quality scan, use the [`  gcloud dataplex datascans delete  ` command](/sdk/gcloud/reference/dataplex/datascans/delete) :

``` text
gcloud dataplex datascans delete DATASCAN \
--location=LOCATION \
--async
```

Replace the following variables:

  - `  DATASCAN  ` : The name of the data quality scan to delete.
  - `  LOCATION  ` : The Google Cloud region in which the data quality scan was created.

### C\#

### C\#

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` csharp
using Google.Cloud.Dataplex.V1;
using Google.LongRunning;
using Google.Protobuf.WellKnownTypes;

public sealed partial class GeneratedDataScanServiceClientSnippets
{
    /// <summary>Snippet for DeleteDataScan</summary>
    /// <remarks>
    /// This snippet has been automatically generated and should be regarded as a code template only.
    /// It will require modifications to work:
    /// - It may require correct/in-range values for request initialization.
    /// - It may require specifying regional endpoints when creating the service client as shown in
    ///   https://cloud.google.com/dotnet/docs/reference/help/client-configuration#endpoint.
    /// </remarks>
    public void DeleteDataScanRequestObject()
    {
        // Create client
        DataScanServiceClient dataScanServiceClient = DataScanServiceClient.Create();
        // Initialize request argument(s)
        DeleteDataScanRequest request = new DeleteDataScanRequest
        {
            DataScanName = DataScanName.FromProjectLocationDataScan("[PROJECT]", "[LOCATION]", "[DATASCAN]"),
            Force = false,
        };
        // Make the request
        Operation<Empty, OperationMetadata> response = dataScanServiceClient.DeleteDataScan(request);

        // Poll until the returned long-running operation is complete
        Operation<Empty, OperationMetadata> completedResponse = response.PollUntilCompleted();
        // Retrieve the operation result
        Empty result = completedResponse.Result;

        // Or get the name of the operation
        string operationName = response.Name;
        // This name can be stored, then the long-running operation retrieved later by name
        Operation<Empty, OperationMetadata> retrievedResponse = dataScanServiceClient.PollOnceDeleteDataScan(operationName);
        // Check if the retrieved long-running operation has completed
        if (retrievedResponse.IsCompleted)
        {
            // If it has completed, then access the result
            Empty retrievedResult = retrievedResponse.Result;
        }
    }
}
```

### Go

### Go

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` go
package main

import (
 "context"

 dataplex "cloud.google.com/go/dataplex/apiv1"
 dataplexpb "cloud.google.com/go/dataplex/apiv1/dataplexpb"
)

func main() {
 ctx := context.Background()
 // This snippet has been automatically generated and should be regarded as a code template only.
 // It will require modifications to work:
 // - It may require correct/in-range values for request initialization.
 // - It may require specifying regional endpoints when creating the service client as shown in:
 //   https://pkg.go.dev/cloud.google.com/go#hdr-Client_Options
 c, err := dataplex.NewDataScanClient(ctx)
 if err != nil {
     // TODO: Handle error.
 }
 defer c.Close()

 req := &dataplexpb.DeleteDataScanRequest{
     // TODO: Fill request struct fields.
     // See https://pkg.go.dev/cloud.google.com/go/dataplex/apiv1/dataplexpb#DeleteDataScanRequest.
 }
 op, err := c.DeleteDataScan(ctx, req)
 if err != nil {
     // TODO: Handle error.
 }

 err = op.Wait(ctx)
 if err != nil {
     // TODO: Handle error.
 }
}
```

### Java

### Java

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` java
import com.google.cloud.dataplex.v1.DataScanName;
import com.google.cloud.dataplex.v1.DataScanServiceClient;
import com.google.cloud.dataplex.v1.DeleteDataScanRequest;
import com.google.protobuf.Empty;

public class SyncDeleteDataScan {

  public static void main(String[] args) throws Exception {
    syncDeleteDataScan();
  }

  public static void syncDeleteDataScan() throws Exception {
    // This snippet has been automatically generated and should be regarded as a code template only.
    // It will require modifications to work:
    // - It may require correct/in-range values for request initialization.
    // - It may require specifying regional endpoints when creating the service client as shown in
    // https://cloud.google.com/java/docs/setup#configure_endpoints_for_the_client_library
    try (DataScanServiceClient dataScanServiceClient = DataScanServiceClient.create()) {
      DeleteDataScanRequest request =
          DeleteDataScanRequest.newBuilder()
              .setName(DataScanName.of("[PROJECT]", "[LOCATION]", "[DATASCAN]").toString())
              .setForce(true)
              .build();
      dataScanServiceClient.deleteDataScanAsync(request).get();
    }
  }
}
```

### Python

### Python

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` python
# This snippet has been automatically generated and should be regarded as a
# code template only.
# It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
#   client as shown in:
#   https://googleapis.dev/python/google-api-core/latest/client_options.html
from google.cloud import dataplex_v1


def sample_delete_data_scan():
    # Create a client
    client = dataplex_v1.DataScanServiceClient()

    # Initialize request argument(s)
    request = dataplex_v1.DeleteDataScanRequest(
        name="name_value",
    )

    # Make the request
    operation = client.delete_data_scan(request=request)

    print("Waiting for operation to complete...")

    response = operation.result()

    # Handle the response
    print(response)
```

### Ruby

### Ruby

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](/docs/authentication/set-up-adc-local-dev-environment) .

``` ruby
require "google/cloud/dataplex/v1"

##
# Snippet for the delete_data_scan call in the DataScanService service
#
# This snippet has been automatically generated and should be regarded as a code
# template only. It will require modifications to work:
# - It may require correct/in-range values for request initialization.
# - It may require specifying regional endpoints when creating the service
# client as shown in https://cloud.google.com/ruby/docs/reference.
#
# This is an auto-generated example demonstrating basic usage of
# Google::Cloud::Dataplex::V1::DataScanService::Client#delete_data_scan.
#
def delete_data_scan
  # Create a client object. The client can be reused for multiple calls.
  client = Google::Cloud::Dataplex::V1::DataScanService::Client.new

  # Create a request. To set request fields, pass in keyword arguments.
  request = Google::Cloud::Dataplex::V1::DeleteDataScanRequest.new

  # Call the delete_data_scan method.
  result = client.delete_data_scan request

  # The returned object is of type Gapic::Operation. You can use it to
  # check the status of an operation, cancel it, or wait for results.
  # Here is how to wait for a response.
  result.wait_until_done! timeout: 60
  if result.response?
    p result.response
  else
    puts "No response received."
  end
end
```

### REST

### REST

To delete a data quality scan, use the [`  dataScans.delete  ` method](/dataplex/docs/reference/rest/v1/projects.locations.dataScans/delete) .

**Note:** Delete isn't supported for data quality scans that are on a one-time schedule.

## What's next

  - Learn more about [data governance in BigQuery](/bigquery/docs/data-governance) .
