# Running jobs programmatically

To run a BigQuery job programmatically using the REST API or client libraries, you:

1.  Call the [`  jobs.insert  `](/bigquery/docs/reference/rest/v2/jobs/insert) method.
2.  Periodically request the job resource and examine the status property to learn when the job is complete.
3.  Check to see whether the job finished successfully.

## Before you begin

Grant Identity and Access Management (IAM) roles that give users the necessary permissions to perform each task in this document.

### Required permissions

To run a BigQuery job, you need the `  bigquery.jobs.create  ` IAM permission.

Each of the following predefined IAM roles includes the permissions that you need in order to run a job:

  - `  roles/bigquery.user  `
  - `  roles/bigquery.jobUser  `
  - `  roles/bigquery.admin  `

Additionally, when you create a job, you are automatically granted the following permissions for that job:

  - `  bigquery.jobs.get  `
  - `  bigquery.jobs.update  `

For more information on IAM roles and permissions in BigQuery, see [Predefined roles and permissions](/bigquery/docs/access-control) .

## Running jobs

To run a job programmatically:

1.  Start the job by calling the `  jobs.insert  ` method. When you call the `  jobs.insert  ` method, include a [job resource](/bigquery/docs/reference/rest/v2/jobs) representation.

2.  In the [`  configuration  `](/bigquery/docs/reference/rest/v2/Job#JobConfiguration) section of the job resource, include a child property that specifies the job type — `  load  ` , `  query  ` , `  extract  ` , or `  copy  ` .

3.  After calling the `  jobs.insert  ` method, check the job status by calling `  jobs.get  ` with the job ID and location, and check the `  status.state  ` value to learn the job status. When `  status.state  ` is `  DONE  ` , the job has stopped running; however, a `  DONE  ` status does not mean that the job completed successfully, only that it is no longer running.
    
    **Note:** There are some wrapper functions that manage job status requests for you. For example, running `  jobs.query  ` creates a job and periodically polls for `  DONE  ` status for a specified period of time.

4.  Check for job success. If the job has an `  errorResult  ` property, the job has failed. The `  status.errorResult  ` property holds information describing what went wrong in a failed job. If `  status.errorResult  ` is absent, the job finished successfully, although there might have been some nonfatal errors, such as problems importing a few rows in a load job. Nonfatal errors are returned in the job's `  status.errors  ` list.

## Running jobs using client libraries

To create and run a job using the Cloud Client Libraries for BigQuery:

### C\#

Before trying this sample, follow the C\# setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery C\# API reference documentation](/dotnet/docs/reference/Google.Cloud.BigQuery.V2/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` csharp
using Google.Cloud.BigQuery.V2;
using System;
using System.Collections.Generic;

public class BigQueryCreateJob
{
    public BigQueryJob CreateJob(string projectId = "your-project-id")
    {
        string query = @"
            SELECT country_name from `bigquery-public-data.utility_us.country_code_iso";

        // Initialize client that will be used to send requests.
        BigQueryClient client = BigQueryClient.Create(projectId);

        QueryOptions queryOptions = new QueryOptions
        {
            JobLocation = "us",
            JobIdPrefix = "code_sample_",
            Labels = new Dictionary<string, string>
            {
                ["example-label"] = "example-value"
            },
            MaximumBytesBilled = 1000000
        };

        BigQueryJob queryJob = client.CreateQueryJob(
            sql: query,
            parameters: null,
            options: queryOptions);

        Console.WriteLine($"Started job: {queryJob.Reference.JobId}");
        return queryJob;
    }
}
```

### Java

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` java
import com.google.cloud.bigquery.BigQuery;
import com.google.cloud.bigquery.BigQueryException;
import com.google.cloud.bigquery.BigQueryOptions;
import com.google.cloud.bigquery.Job;
import com.google.cloud.bigquery.JobId;
import com.google.cloud.bigquery.JobInfo;
import com.google.cloud.bigquery.QueryJobConfiguration;
import com.google.common.collect.ImmutableMap;
import java.util.UUID;

// Sample to create a job
public class CreateJob {

  public static void main(String[] args) {
    // TODO(developer): Replace these variables before running the sample.
    String query = "SELECT country_name from `bigquery-public-data.utility_us.country_code_iso`";
    createJob(query);
  }

  public static void createJob(String query) {
    try {
      // Initialize client that will be used to send requests. This client only needs to be created
      // once, and can be reused for multiple requests.
      BigQuery bigquery = BigQueryOptions.getDefaultInstance().getService();

      // Specify a job configuration to set optional job resource properties.
      QueryJobConfiguration queryConfig =
          QueryJobConfiguration.newBuilder(query)
              .setLabels(ImmutableMap.of("example-label", "example-value"))
              .build();

      // The location and job name are optional,
      // if both are not specified then client will auto-create.
      String jobName = "jobId_" + UUID.randomUUID().toString();
      JobId jobId = JobId.newBuilder().setLocation("us").setJob(jobName).build();

      // Create a job with job ID
      bigquery.create(JobInfo.of(jobId, queryConfig));

      // Get a job that was just created
      Job job = bigquery.getJob(jobId);
      if (job.getJobId().getJob().equals(jobId.getJob())) {
        System.out.print("Job created successfully." + job.getJobId().getJob());
      } else {
        System.out.print("Job was not created");
      }
    } catch (BigQueryException e) {
      System.out.print("Job was not created. \n" + e.toString());
    }
  }
}
```

### Python

Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/bigquery/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` python
from google.cloud import bigquery

# Construct a BigQuery client object.
client = bigquery.Client()

query_job = client.query(
    "SELECT country_name from `bigquery-public-data.utility_us.country_code_iso`",
    # Explicitly force job execution to be routed to a specific processing
    # location.
    location="US",
    # Specify a job configuration to set optional job resource properties.
    job_config=bigquery.QueryJobConfig(
        labels={"example-label": "example-value"}, maximum_bytes_billed=1000000
    ),
    # The client libraries automatically generate a job ID. Override the
    # generated ID with either the job_id_prefix or job_id parameters.
    job_id_prefix="code_sample_",
)  # Make an API request.

print("Started job: {}".format(query_job.job_id))
```

## Adding job labels

Labels can be added to query jobs through the command line by using the bq command-line tool's `  --label  ` flag. The bq tool supports adding labels only to query jobs.

You can also add a label to a job when it's submitted through the API by specifying the `  labels  ` property in the job configuration when you call the [`  jobs.insert  `](/bigquery/docs/reference/rest/v2/jobs/insert) method. The API can be used to add labels to any job type.

You cannot add labels to or update labels on pending, running, or completed jobs.

When you add a label to a job, the label is included in your billing data.

For more information, see [Adding job labels](/bigquery/docs/adding-labels#job-label) .

## What's next

  - See [Running queries](/bigquery/docs/running-queries#batch) for a code example that starts and polls a query job.
  - For more information on creating a job resource representation, see the [Jobs overview page](/bigquery/docs/reference/v2/jobs) in the API reference.
