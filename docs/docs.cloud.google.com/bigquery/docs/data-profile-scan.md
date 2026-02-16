# Profile your data

This document explains how to use data profile scans to better understand your data. BigQuery uses Dataplex Universal Catalog to analyze the statistical characteristics of your data, such as average values, unique values, and maximum values. Dataplex Universal Catalog also uses this information to [recommend rules for data quality checks](/dataplex/docs/auto-data-quality-overview) .

For more information about data profiling, see [About data profiling](/dataplex/docs/data-profiling-overview) .

**Tip:** The steps in this document show how to manage data profile scans across your project. You can also create and manage data profile scans when working with a specific table. For more information, see the [Manage data profile scans for a specific table](#start-from-table) section of this document.

## Before you begin

Enable the Dataplex API.

**Roles required to enable APIs**

To enable APIs, you need the Service Usage Admin IAM role ( `  roles/serviceusage.serviceUsageAdmin  ` ), which contains the `  serviceusage.services.enable  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .

## Required roles

To get the permissions that you need to create and manage data profile scans, ask your administrator to grant you the following IAM roles on your resource such as the project or table:

  - To create, run, update, and delete data profile scans: **Dataplex DataScan Editor** ( `  roles/dataplex.dataScanEditor  ` ) role on the project containing the data scan.
  - To allow Dataplex Universal Catalog to run data profile scans against BigQuery data, grant the following roles to the [Dataplex Universal Catalog service account](/dataplex/docs/iam-and-access-control#service-agent) : **BigQuery Job User** ( `  roles/bigquery.jobUser  ` ) role on the project running the scan; **BigQuery Data Viewer** ( `  roles/bigquery.dataViewer  ` ) role on the tables being scanned.
  - To run data profile scans for BigQuery external tables that use Cloud Storage data: grant the [Dataplex Universal Catalog service account](/dataplex/docs/iam-and-access-control#service-agent) the **Storage Object Viewer** ( `  roles/storage.objectViewer  ` ) and **Storage Legacy Bucket Reader** ( `  roles/storage.legacyBucketReader  ` ) roles on the Cloud Storage bucket.
  - To view data profile scan results, jobs, and history: **Dataplex DataScan Viewer** ( `  roles/dataplex.dataScanViewer  ` ) role on the project containing the data scan.
  - To export data profile scan results to a BigQuery table: **BigQuery Data Editor** ( `  roles/bigquery.dataEditor  ` ) role on the table.
  - To publish data profile scan results to Dataplex Universal Catalog: **Dataplex Catalog Editor** ( `  roles/dataplex.catalogEditor  ` ) role on the `  @bigquery  ` entry group.
  - To view published data profile scan results in BigQuery on the **Data profile** tab: **BigQuery Data Viewer** ( `  roles/bigquery.dataViewer  ` ) role on the table.

For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

### Required permissions

If you use custom roles, you need to grant the following IAM permissions:

  - To create, run, update, and delete data profile scans:
      - `  dataplex.datascans.create  ` on project—Create a `  DataScan  `
      - `  dataplex.datascans.update  ` on data scan—Update the description of a `  DataScan  `
      - `  dataplex.datascans.delete  ` on data scan—Delete a `  DataScan  `
      - `  dataplex.datascans.run  ` on data scan—Run a `  DataScan  `
      - `  dataplex.datascans.get  ` on data scan—View `  DataScan  ` details excluding results
      - `  dataplex.datascans.list  ` on project—List `  DataScan  ` s
      - `  dataplex.dataScanJobs.get  ` on data scan job—Read DataScan job resources
      - `  dataplex.dataScanJobs.list  ` on data scan—List DataScan job resources in a project
  - To allow Dataplex Universal Catalog to run data profile scans against BigQuery data:
      - `  bigquery.jobs.create  ` on project—Run jobs
      - `  bigquery.tables.get  ` on table—Get table metadata
      - `  bigquery.tables.getData  ` on table—Get table data
  - To run data profile scans for BigQuery external tables that use Cloud Storage data:
      - `  storage.buckets.get  ` on bucket—Read bucket metadata
      - `  storage.objects.get  ` on object—Read object data
  - To view data profile scan results, jobs, and history:
      - `  dataplex.datascans.getData  ` on data scan—View `  DataScan  ` details including results
      - `  dataplex.datascans.list  ` on project—List `  DataScan  ` s
      - `  dataplex.dataScanJobs.get  ` on data scan job—Read DataScan job resources
      - `  dataplex.dataScanJobs.list  ` on data scan—List DataScan job resources in a project
  - To export data profile scan results to a BigQuery table:
      - `  bigquery.tables.create  ` on dataset—Create tables
      - `  bigquery.tables.updateData  ` on table—Write data to tables
  - To publish data profile scan results to Dataplex Universal Catalog:
      - `  dataplex.entryGroups.useDataProfileAspect  ` on entry group—Allows Dataplex Universal Catalog data profile scans to save their results to Dataplex Universal Catalog
      - Additionally, you need one of the following permissions:
          - `  bigquery.tables.update  ` on table—Update table metadata
          - `  dataplex.entries.update  ` on entry—Update entries
  - To view published data profile results for a table in BigQuery or Dataplex Universal Catalog:
      - `  bigquery.tables.get  ` on table—Get table metadata
      - `  bigquery.tables.getData  ` on table—Get table data

If a table uses BigQuery [row-level security](/bigquery/docs/row-level-security-intro) , then Dataplex Universal Catalog can only scan rows visible to the Dataplex Universal Catalog service account. To allow Dataplex Universal Catalog to scan all rows, add its service account to a row filter where the predicate is `  TRUE  ` .

If a table uses BigQuery [column-level security](/bigquery/docs/column-level-security) , then Dataplex Universal Catalog requires access to scan protected columns. To grant access, give the Dataplex Universal Catalog service account the **Data Catalog Fine-Grained Reader** ( `  roles/datacatalog.fineGrainedReader  ` ) role on all policy tags used in the table. The user creating or updating a data scan also needs permissions on protected columns.

### Grant roles to the Dataplex Universal Catalog service account

To run data profile scans, Dataplex Universal Catalog uses a service account that requires permissions to run BigQuery jobs and read BigQuery table data. To grant the required roles, follow these steps:

1.  Get the Dataplex Universal Catalog service account email address. If you haven't created a data profile or data quality scan in this project before, run the following `  gcloud  ` command to generate the service identity:
    
    ``` text
    gcloud beta services identity create --service=dataplex.googleapis.com
    ```
    
    The command returns the service account email, which has the following format: service- PROJECT\_ID @gcp-sa-dataplex.iam.gserviceaccount.com.
    
    If the service account already exists, you can find its email by viewing principals with the **Dataplex** name on the [**IAM** page](https://console.cloud.google.com/iam-admin/iam) in the Google Cloud console.

2.  Grant the service account the **BigQuery Job User** ( `  roles/bigquery.jobUser  ` ) role on your project. This role lets the service account run BigQuery jobs for the scan.
    
    ``` text
    gcloud projects add-iam-policy-binding PROJECT_ID \
        --member="serviceAccount:service-PROJECT_NUMBER@gcp-sa-dataplex.iam.gserviceaccount.com" \
        --role="roles/bigquery.jobUser"
    ```
    
    Replace the following:
    
      - `  PROJECT_ID  ` : your Google Cloud project ID.
      - `  service- PROJECT_NUMBER @gcp-sa-dataplex.iam.gserviceaccount.com  ` : the email of the Dataplex Universal Catalog service account.

3.  Grant the service account the **BigQuery Data Viewer** ( `  roles/bigquery.dataViewer  ` ) role for each table that you want to profile. This role grants read-only access to the tables.
    
    ``` text
    gcloud bigquery tables add-iam-policy-binding DATASET_ID.TABLE_ID \
        --member="serviceAccount:service-PROJECT_NUMBER@gcp-sa-dataplex.iam.gserviceaccount.com" \
        --role="roles/bigquery.dataViewer"
    ```
    
    Replace the following:
    
      - `  DATASET_ID  ` : the ID of the dataset containing the table.
    
      - `  TABLE_ID  ` : the ID of the table to profile.
    
      - `  service- PROJECT_NUMBER @gcp-sa-dataplex.iam.gserviceaccount.com  ` : the email of the Dataplex Universal Catalog service account.
        
        ## Create a data profile scan
        
        ### Console
        
        1.  In the Google Cloud console, on the BigQuery **Metadata curation** page, go to the **Data profiling & quality** tab.
        
        2.  Click **Create data profile scan** .
        
        3.  Optional: Enter a **Display name** .
        
        4.  Enter an **ID** . See the [Resource naming conventions](/compute/docs/naming-resources#resource-name-format) .
        
        5.  Optional: Enter a **Description** .
        
        6.  In the **Table** field, click **Browse** . Choose the table to scan, and then click **Select** .
            
            For tables in multi-region datasets, choose a region where to create the data scan.
            
            To browse the tables organized within Dataplex Universal Catalog lakes, click **Browse within Dataplex Lakes** .
        
        7.  In the **Scope** field, choose **Incremental** or **Entire data** .
            
              - If you choose **Incremental data** , in the **Timestamp column** field, select a column of type `  DATE  ` or `  TIMESTAMP  ` from your BigQuery table that increases as new records are added, and that can be used to identify new records. For tables partitioned on a column of type `  DATE  ` or `  TIMESTAMP  ` , we recommend using the partition column as the timestamp field.
        
        8.  Optional: To filter your data, do any of the following:
            
              - To filter by rows, click select the **Filter rows** checkbox. Enter a valid SQL expression that can be used in a [`  WHERE  ` clause in GoogleSQL syntax](/bigquery/docs/reference/standard-sql/query-syntax#where_clause) . For example: `  col1 >= 0  ` .
                
                The filter can be a combination of SQL conditions over multiple columns. For example: `  col1 >= 0 AND col2 < 10  ` .
            
              - To filter by columns, select the **Filter columns** checkbox.
                
                  - To include columns in the profile scan, in the **Include columns** field, click **Browse** . Select the columns to include, and then click **Select** .
                
                  - To exclude columns from the profile scan, in the **Exclude columns** field, click **Browse** . Select the columns to exclude, and then click **Select** .
                
                **Note:** You can use **Include columns** , **Exclude columns** , or both. If you use both the fields, then the data profile scan first selects the columns based on your input in the **Include columns** field and then excludes the columns based on your input in the **Exclude columns** field.
        
        9.  To apply sampling to your data profile scan, in the **Sampling size** list, select a sampling percentage. Choose a percentage value that ranges between 0.0% and 100.0% with up to 3 decimal digits.
            
              - For larger datasets, choose a lower sampling percentage. For example, for a 1 PB table, if you enter a value between 0.1% and 1.0%, the data profile samples between 1-10 TB of data.
            
              - There must be at least 100 records in the sampled data to return a result.
            
              - For incremental data scans, the data profile scan applies sampling to the latest increment.
        
        10. Optional: Publish the data profile scan results in the BigQuery and Dataplex Universal Catalog pages in the Google Cloud console for the source table. Select the **Publish results to Dataplex Catalog** checkbox.
            
            You can view the latest scan results in the **Data profile** tab in the BigQuery and Dataplex Universal Catalog pages for the source table. To enable users to access the published scan results, see the [Grant access to data profile scan results](#share-results) section of this document.
            
            The publishing option might not be available in the following cases:
            
              - You don't have the required permissions on the table.
              - Another data profile scan is set to publish results.
        
        11. In the **Schedule** section, choose one of the following options:
            
              - **Repeat** : Run the data profile scan on a schedule: hourly, daily, weekly, monthly, or custom. Specify how often the scan should run and at what time. If you choose custom, use [cron](https://en.wikipedia.org/wiki/Cron) format to specify the schedule.
            
              - **On-demand** : Run the data profile scan on demand.
            
              - **One-time** : Run the data profile scan once now, and remove the scan after the time-to-live period.
            
              - **Time to live** : The time-to-live value defines the duration a data profile scan remains active after execution. A data profile scan without a specified time-to-live is automatically removed after 24 hours. The time-to-live can range from 0 seconds (immediate deletion) to 365 days.
        
        12. Click **Continue** .
        
        13. Optional: Export the scan results to a BigQuery standard table. In the **Export scan results to BigQuery table** section, do the following:
            
            1.  In the **Select BigQuery dataset** field, click **Browse** . Select a BigQuery dataset to store the data profile scan results.
            
            2.  In the **BigQuery table** field, specify the table to store the data profile scan results. If you're using an existing table, make sure that it is compatible with the [export table schema](/dataplex/docs/use-data-profiling#table-schema) . If the specified table doesn't exist, Dataplex Universal Catalog creates it for you.
                
                **Note:** You can use the same results table for multiple data profile scans.
        
        14. Optional: Add labels. Labels are key-value pairs that let you group related objects together or with other Google Cloud resources.
        
        15. To create the scan, click **Create** .
            
            If you set the schedule to on-demand, you can also run the scan now by clicking **Run scan** .
        
        ### gcloud
        
        To create a data profile scan, use the [`  gcloud dataplex datascans create data-profile  ` command](/sdk/gcloud/reference/dataplex/datascans/create/data-profile) .
        
        If the source data is organized in a Dataplex Universal Catalog lake, include the `  --data-source-entity  ` flag:
        
        ``` text
        gcloud dataplex datascans create data-profile DATASCAN \
        --location=LOCATION \
        --data-source-entity=DATA_SOURCE_ENTITY
        ```
        
        If the source data isn't organized in a Dataplex Universal Catalog lake, include the `  --data-source-resource  ` flag:
        
        ``` text
        gcloud dataplex datascans create data-profile DATASCAN \
        --location=LOCATION \
        --data-source-resource=DATA_SOURCE_RESOURCE
        ```
        
        Replace the following variables:
        
          - `  DATASCAN  ` : The name of the data profile scan.
          - `  LOCATION  ` : The Google Cloud region in which to create the data profile scan.
          - `  DATA_SOURCE_ENTITY  ` : The Dataplex Universal Catalog entity that contains the data for the data profile scan. For example, `  projects/test-project/locations/test-location/lakes/test-lake/zones/test-zone/entities/test-entity  ` .
          - `  DATA_SOURCE_RESOURCE  ` : The name of the resource that contains the data for the data profile scan. For example, `  //bigquery.googleapis.com/projects/test-project/datasets/test-dataset/tables/test-table  ` .
        
        ### C\#
        
        ### C\#
        
        Before trying this sample, follow the C\# setup instructions in the [BigQuery quickstart using client libraries](/dataplex/docs/reference/libraries) . For more information, see the [BigQuery C\# API reference documentation](/dotnet/docs/reference/Google.Cloud.Dataplex.V1/latest) .
        
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
        
        Before trying this sample, follow the Go setup instructions in the [BigQuery quickstart using client libraries](/dataplex/docs/reference/libraries) . For more information, see the [BigQuery Go API reference documentation](https://pkg.go.dev/cloud.google.com/go/dataplex) .
        
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
        
        Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/dataplex/docs/reference/libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-dataplex/latest/overview) .
        
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
        
        ### Python
        
        ### Python
        
        Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/dataplex/docs/reference/libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/dataplex/latest) .
        
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
        
        Before trying this sample, follow the Ruby setup instructions in the [BigQuery quickstart using client libraries](/dataplex/docs/reference/libraries) . For more information, see the [BigQuery Ruby API reference documentation](/ruby/docs/reference/google-cloud-dataplex/latest) .
        
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
        
        To create a data profile scan, use the [`  dataScans.create  ` method](/dataplex/docs/reference/rest/v1/projects.locations.dataScans/create) .
        
        **Note:** If your BigQuery table is configured with the `  Require partition filter  ` setting set to `  true  ` , use the table's partition column as the data profile scan's row filter or timestamp column.
        
        ## Create multiple data profile scans
        
        You can configure data profile scans for multiple tables in a BigQuery dataset at the same time by using the Google Cloud console.
        
        1.  In the Google Cloud console, on the BigQuery **Metadata curation** page, go to the **Data profiling & quality** tab.
        
        2.  Click **Create data profile scan** .
        
        3.  Select the **Multiple data profile scans** option.
        
        4.  Enter an **ID prefix** . Dataplex Universal Catalog automatically generates scan IDs by using the provided prefix and unique suffixes.
        
        5.  Enter a **Description** for all of the data profile scans.
        
        6.  In the **Dataset** field, click **Browse** . Select a dataset to pick tables from. Click **Select** .
        
        7.  If the dataset is multi-regional, select a **Region** in which to create the data profile scans.
        
        8.  Configure the common settings for the scans:
            
            1.  In the **Scope** field, choose **Incremental** or **Entire data** .
                
                **Note:** If you choose **Incremental** data, you can select only tables that are partitioned on a column of type `  DATE  ` or `  TIMESTAMP  ` .
            
            2.  To apply sampling to the data profile scans, in the **Sampling size** list, select a sampling percentage.
                
                Choose a percentage value between 0.0% and 100.0% with up to 3 decimal digits.
            
            3.  Optional: Publish the data profile scan results in the BigQuery and Dataplex Universal Catalog pages in the Google Cloud console for the source table. Select the **Publish results to Dataplex Catalog** checkbox.
                
                You can view the latest scan results in the **Data profile** tab in the BigQuery and Dataplex Universal Catalog pages for the source table. To enable users to access the published scan results, see the [Grant access to data profile scan results](#share-results) section of this document.
                
                **Note:** You must choose tables that don't have any existing scans publishing their results.
            
            4.  In the **Schedule** section, choose one of the following options:
                
                  - **Repeat** : Run the data profile scans on a schedule: hourly, daily, weekly, monthly, or custom. Specify how often the scans should run and at what time. If you choose custom, use [cron](https://en.wikipedia.org/wiki/Cron) format to specify the schedule.
                
                  - **On-demand** : Run the data profile scans on demand.
        
        9.  Click **Continue** .
        
        10. In the **Choose tables** field, click **Browse** . Choose one or more tables to scan, and then click **Select** .
        
        11. Click **Continue** .
        
        12. Optional: Export the scan results to a BigQuery standard table. In the **Export scan results to BigQuery table** section, do the following:
            
            1.  In the **Select BigQuery dataset** field, click **Browse** . Select a BigQuery dataset to store the data profile scan results.
            
            2.  In the **BigQuery table** field, specify the table to store the data profile scan results. If you're using an existing table, make sure that it is compatible with the [export table schema](/dataplex/docs/use-data-profiling#table-schema) . If the specified table doesn't exist, Dataplex Universal Catalog creates it for you.
                
                Dataplex Universal Catalog uses the same results table for all of the data profile scans.
        
        13. Optional: Add labels. Labels are key-value pairs that let you group related objects together or with other Google Cloud resources.
        
        14. To create the scans, click **Create** .
            
            If you set the schedule to on-demand, you can also run the scans now by clicking **Run scan** .
        
        ## Run a data profile scan
        
        ### Console
        
        1.  In the Google Cloud console, on the BigQuery **Metadata curation** page, go to the **Data profiling & quality** tab.
        2.  Click the data profile scan to run.
        3.  Click **Run now** .
        
        ### gcloud
        
        To run a data profile scan, use the [`  gcloud dataplex datascans run  ` command](/sdk/gcloud/reference/dataplex/datascans/run) :
        
        ``` text
        gcloud dataplex datascans run DATASCAN \
        --location=LOCATION
        ```
        
        Replace the following variables:
        
          - `  DATASCAN  ` : The name of the data profile scan.
          - `  LOCATION  ` : The Google Cloud region in which the data profile scan was created.
        
        ### C\#
        
        ### C\#
        
        Before trying this sample, follow the C\# setup instructions in the [BigQuery quickstart using client libraries](/dataplex/docs/reference/libraries) . For more information, see the [BigQuery C\# API reference documentation](/dotnet/docs/reference/Google.Cloud.Dataplex.V1/latest) .
        
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
        
        Before trying this sample, follow the Go setup instructions in the [BigQuery quickstart using client libraries](/dataplex/docs/reference/libraries) . For more information, see the [BigQuery Go API reference documentation](https://pkg.go.dev/cloud.google.com/go/dataplex) .
        
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
        
        Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/dataplex/docs/reference/libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-dataplex/latest/overview) .
        
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
        
        Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/dataplex/docs/reference/libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/dataplex/latest) .
        
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
        
        Before trying this sample, follow the Ruby setup instructions in the [BigQuery quickstart using client libraries](/dataplex/docs/reference/libraries) . For more information, see the [BigQuery Ruby API reference documentation](/ruby/docs/reference/google-cloud-dataplex/latest) .
        
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
        
        To run a data profile scan, use the [`  dataScans.run  ` method](/dataplex/docs/reference/rest/v1/projects.locations.dataScans/run) .
        
        **Note:** Run isn't supported for data profile scans that are on a one-time schedule.
        
        ## View data profile scan results
        
        ### Console
        
        1.  In the Google Cloud console, on the BigQuery **Metadata curation** page, go to the **Data profiling & quality** tab.
        
        2.  Click the name of a data profile scan.
            
              - The **Overview** section displays information about the most recent jobs, including when the scan was run, the number of table records scanned, and the job status.
            
              - The **Data profile scan configuration** section displays details about the scan.
        
        3.  To see detailed information about a job, such as the scanned table's columns, statistics about the columns that were found in the scan, and the job logs, click the **Jobs history** tab. Then, click a job ID.
        
        **Note:** If you exported the scan results to a BigQuery table, then you can also access the scan results from the table.
        
        ### gcloud
        
        To view the results of a data profile scan job, use the [`  gcloud dataplex datascans jobs describe  ` command](/sdk/gcloud/reference/dataplex/datascans/jobs/describe) :
        
        ``` text
        gcloud dataplex datascans jobs describe JOB \
        --location=LOCATION \
        --datascan=DATASCAN \
        --view=FULL
        ```
        
        Replace the following variables:
        
          - `  JOB  ` : The job ID of the data profile scan job.
          - `  LOCATION  ` : The Google Cloud region in which the data profile scan was created.
          - `  DATASCAN  ` : The name of the data profile scan the job belongs to.
          - `  --view=FULL  ` : To see the scan job result, specify `  FULL  ` .
        
        ### C\#
        
        ### C\#
        
        Before trying this sample, follow the C\# setup instructions in the [BigQuery quickstart using client libraries](/dataplex/docs/reference/libraries) . For more information, see the [BigQuery C\# API reference documentation](/dotnet/docs/reference/Google.Cloud.Dataplex.V1/latest) .
        
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
        
        Before trying this sample, follow the Go setup instructions in the [BigQuery quickstart using client libraries](/dataplex/docs/reference/libraries) . For more information, see the [BigQuery Go API reference documentation](https://pkg.go.dev/cloud.google.com/go/dataplex) .
        
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
        
        Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/dataplex/docs/reference/libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-dataplex/latest/overview) .
        
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
        
        Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/dataplex/docs/reference/libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/dataplex/latest) .
        
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
        
        Before trying this sample, follow the Ruby setup instructions in the [BigQuery quickstart using client libraries](/dataplex/docs/reference/libraries) . For more information, see the [BigQuery Ruby API reference documentation](/ruby/docs/reference/google-cloud-dataplex/latest) .
        
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
        
        To view the results of a data profile scan, use the [`  dataScans.get  ` method](/dataplex/docs/reference/rest/v1/projects.locations.dataScans/get) .
        
        ### View published results
        
        If the data profile scan results are published to the BigQuery and Dataplex Universal Catalog pages in the Google Cloud console, then you can see the latest scan results on the source table's **Data profile** tab.
        
        1.  In the Google Cloud console, go to the BigQuery page.
        
        2.  In the left pane, click explore **Explorer** :
            
            If you don't see the left pane, click last\_page **Expand left pane** to open the pane.
        
        3.  In the **Explorer** pane, click **Datasets** , and then click your dataset.
        
        4.  Click **Overview \> Tables** , and then select the table whose data profile scan results you want to see.
        
        5.  Click the **Data profile** tab.
            
            The latest published results are displayed.
            
            **Note:** Published results might not be available if a scan is running for the first time.
        
        ### View the most recent data profile scan job
        
        ### Console
        
        1.  In the Google Cloud console, on the BigQuery **Metadata curation** page, go to the **Data profiling & quality** tab.
        
        2.  Click the name of a data profile scan.
        
        3.  Click the **Latest job results** tab.
            
            The **Latest job results** tab, when there is at least one successfully completed run, provides information about the most recent job. It lists the scanned table's columns and statistics about the columns that were found in the scan.
        
        ### gcloud
        
        To view the most recent successful data profile scan, use the [`  gcloud dataplex datascans describe  ` command](/sdk/gcloud/reference/dataplex/datascans/describe) :
        
        ``` text
        gcloud dataplex datascans describe DATASCAN \
        --location=LOCATION \
        --view=FULL
        ```
        
        Replace the following variables:
        
          - `  DATASCAN  ` : The name of the data profile scan to view the most recent job for.
          - `  LOCATION  ` : The Google Cloud region in which the data profile scan was created.
          - `  --view=FULL  ` : To see the scan job result, specify `  FULL  ` .
        
        ### REST
        
        To view the most recent scan job, use the [`  dataScans.get  ` method](/dataplex/docs/reference/rest/v1/projects.locations.dataScans/get) .
        
        ### View historical scan results
        
        Dataplex Universal Catalog saves the data profile scan history of the last 300 jobs or for the past year, whichever occurs first.
        
        ### Console
        
        1.  In the Google Cloud console, on the BigQuery **Metadata curation** page, go to the **Data profiling & quality** tab.
        
        2.  Click the name of a data profile scan.
        
        3.  Click the **Jobs history** tab.
            
            The **Jobs history** tab provides information about past jobs, such as the number of records scanned in each job, the job status, and the time the job was run.
        
        4.  To view detailed information about a job, click any of the jobs in the **Job ID** column.
        
        ### gcloud
        
        To view historical data profile scan jobs, use the [`  gcloud dataplex datascans jobs list  ` command](/sdk/gcloud/reference/dataplex/datascans/jobs/list) :
        
        ``` text
        gcloud dataplex datascans jobs list \
        --location=LOCATION \
        --datascan=DATASCAN
        ```
        
        Replace the following variables:
        
          - `  LOCATION  ` : The Google Cloud region in which the data profile scan was created.
          - `  DATASCAN  ` : The name of the data profile scan to view jobs for.
        
        ### C\#
        
        ### C\#
        
        Before trying this sample, follow the C\# setup instructions in the [BigQuery quickstart using client libraries](/dataplex/docs/reference/libraries) . For more information, see the [BigQuery C\# API reference documentation](/dotnet/docs/reference/Google.Cloud.Dataplex.V1/latest) .
        
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
        
        Before trying this sample, follow the Go setup instructions in the [BigQuery quickstart using client libraries](/dataplex/docs/reference/libraries) . For more information, see the [BigQuery Go API reference documentation](https://pkg.go.dev/cloud.google.com/go/dataplex) .
        
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
        
        Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/dataplex/docs/reference/libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-dataplex/latest/overview) .
        
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
        
        Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/dataplex/docs/reference/libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/dataplex/latest) .
        
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
        
        Before trying this sample, follow the Ruby setup instructions in the [BigQuery quickstart using client libraries](/dataplex/docs/reference/libraries) . For more information, see the [BigQuery Ruby API reference documentation](/ruby/docs/reference/google-cloud-dataplex/latest) .
        
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
        
        To view historical data profile scan jobs, use the [`  dataScans.jobs.list  ` method](/dataplex/docs/reference/rest/v1/projects.locations.dataScans.jobs/list) .
        
        ### View the data profile scans for a table
        
        To view the data profile scans that apply to a specific table, do the following:
        
        1.  In the Google Cloud console, on the BigQuery **Metadata curation** page, go to the **Data profiling & quality** tab.
        
        2.  Filter the list by table name and scan type.
        
        ## Grant access to data profile scan results
        
        To enable the users in your organization to view the scan results, do the following:
        
        1.  In the Google Cloud console, on the BigQuery **Metadata curation** page, go to the **Data profiling & quality** tab.
        
        2.  Click the data profile scan you want to share the results of.
        
        3.  Click the **Permissions** tab.
        
        4.  Do the following:
            
              - To grant access to a principal, click person\_add **Grant access** . Grant the **Dataplex DataScan DataViewer** role to the associated principal.
              - To remove access from a principal, select the principal that you want to remove the **Dataplex DataScan DataViewer** role from. Click person\_remove **Remove access** , and then confirm when prompted.
        
        ## Manage data profile scans for a specific table
        
        The steps in this document show how to manage data profile scans across your project by using the BigQuery **Metadata curation \> Data profiling & quality** page in the Google Cloud console.
        
        You can also create and manage data profile scans when working with a specific table. In the Google Cloud console, on the BigQuery page for the table, use the **Data profile** tab. Do the following:
        
        1.  In the Google Cloud console, go to the **BigQuery** page.
            
            In the **Explorer** pane (in the left pane), click **Datasets** , and then click your dataset. Now click **Overview \> Tables** , and select the table whose data profile scan results you want to see.
        
        2.  Click the **Data profile** tab.
        
        3.  Depending on whether the table has a data profile scan whose results are published, you can work with the table's data profile scans in the following ways:
            
              - **Data profile scan results are published** : the latest published scan results are displayed on the page.
                
                To manage the data profile scans for this table, click **Data profile scan** , and then select from the following options:
                
                  - **Create new scan** : create a new data profile scan. For more information, see the [Create a data profile scan](#create-scan) section of this document. When you create a scan from a table's details page, the table is preselected.
                
                  - **Run now** : run the scan.
                
                  - **Edit scan configuration** : edit settings including the display name, filters, sampling size, and schedule.
                
                  - **Manage scan permissions** : control who can access the scan results. For more information, see the [Grant access to data profile scan results](#share-results) section of this document.
                
                  - **View historical results** : view detailed information about previous data profile scan jobs. For more information, see the [View data profile scan results](#results) and [View historical scan results](#older-scans) sections of this document.
                
                  - **View all scans** : view a list of data profile scans that apply to this table.
            
              - **Data profile scan results aren't published** : click the menu next to **Quick data profile** , and then select from the following options:
                
                  - **Customize data profiling** : create a new data profile scan. For more information, see the [Create a data profile scan](#create-scan) section of this document. When you create a scan from a table's details page, the table is preselected.
                
                  - **View previous profiles** : view a list of data profile scans that apply to this table.
        
        ## Update a data profile scan
        
        ### Console
        
        1.  In the Google Cloud console, on the BigQuery **Metadata curation** page, go to the **Data profiling & quality** tab.
        
        2.  Click the name of a data profile scan.
        
        3.  Click **Edit** , and then edit the values.
        
        4.  Click **Save** .
        
        ### gcloud
        
        To update a data profile scan, use the [`  gcloud dataplex datascans update data-profile  ` command](/sdk/gcloud/reference/dataplex/datascans/update/data-profile) :
        
        ``` text
        gcloud dataplex datascans update data-profile DATASCAN \
        --location=LOCATION \
        --description=DESCRIPTION
        ```
        
        Replace the following variables:
        
          - `  DATASCAN  ` : The name of the data profile scan to update.
          - `  LOCATION  ` : The Google Cloud region in which the data profile scan was created.
          - `  DESCRIPTION  ` : The new description for the data profile scan.
        
        **Note:** You can update specification fields, such as `  rowFilter  ` , `  samplingPercent  ` , or `  includeFields  ` , in the data profile specification file. See the [JSON format](/dataplex/docs/reference/rest/v1/DataProfileSpec) .
        
        ### C\#
        
        ### C\#
        
        Before trying this sample, follow the C\# setup instructions in the [BigQuery quickstart using client libraries](/dataplex/docs/reference/libraries) . For more information, see the [BigQuery C\# API reference documentation](/dotnet/docs/reference/Google.Cloud.Dataplex.V1/latest) .
        
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
        
        Before trying this sample, follow the Go setup instructions in the [BigQuery quickstart using client libraries](/dataplex/docs/reference/libraries) . For more information, see the [BigQuery Go API reference documentation](https://pkg.go.dev/cloud.google.com/go/dataplex) .
        
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
        
        Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/dataplex/docs/reference/libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-dataplex/latest/overview) .
        
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
        
        Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/dataplex/docs/reference/libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/dataplex/latest) .
        
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
        
        Before trying this sample, follow the Ruby setup instructions in the [BigQuery quickstart using client libraries](/dataplex/docs/reference/libraries) . For more information, see the [BigQuery Ruby API reference documentation](/ruby/docs/reference/google-cloud-dataplex/latest) .
        
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
        
        To edit a data profile scan, use the [`  dataScans.patch  ` method](/dataplex/docs/reference/rest/v1/projects.locations.dataScans/patch) .
        
        **Note:** Update isn't supported for data profile scans that are on a one-time schedule.
        
        ## Delete a data profile scan
        
        ### Console
        
        1.  In the Google Cloud console, on the BigQuery **Metadata curation** page, go to the **Data profiling & quality** tab.
        
        2.  Click the scan you want to delete.
        
        3.  Click **Delete** , and then confirm when prompted.
        
        ### gcloud
        
        To delete a data profile scan, use the [`  gcloud dataplex datascans delete  ` command](/sdk/gcloud/reference/dataplex/datascans/delete) :
        
        ``` text
        gcloud dataplex datascans delete DATASCAN \
        --location=LOCATION --async
        ```
        
        Replace the following variables:
        
          - `  DATASCAN  ` : The name of the data profile scan to delete.
          - `  LOCATION  ` : The Google Cloud region in which the data profile scan was created.
        
        ### REST
        
        To delete a data profile scan, use the [`  dataScans.delete  ` method](/dataplex/docs/reference/rest/v1/projects.locations.dataScans/delete) .
        
        **Note:** Delete isn't supported for data profile scans that are on a one-time schedule.
        
        ## What's next
        
          - Learn how to [explore your data by generating data insights](/bigquery/docs/data-insights) .
          - Learn more about [data governance in BigQuery](/bigquery/docs/data-governance) .
          - Learn how to [scan your data for data quality issues](/bigquery/docs/data-quality-scan) .
          - Learn how to examine table data and create queries with [table explorer](/bigquery/docs/table-explorer) .
