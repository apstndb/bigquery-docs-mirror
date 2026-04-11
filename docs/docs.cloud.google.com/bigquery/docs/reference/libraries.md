This page shows how to get started with the Cloud Client Libraries for the BigQuery API. Client libraries make it easier to access Google Cloud APIs from a supported language. Although you can use Google Cloud APIs directly by making raw requests to the server, client libraries provide simplifications that significantly reduce the amount of code you need to write.

Read more about the Cloud Client Libraries and the older Google API Client Libraries in [Client libraries explained](https://docs.cloud.google.com/apis/docs/client-libraries-explained) .

<span id="installing_the_client_library"></span>

## Install the client library

### C\#

``` notranslate
Install-Package Google.Cloud.BigQuery.V2 -Pre
```

For more information, see [Setting Up a C\# Development Environment](https://docs.cloud.google.com/dotnet/docs/setup) .

### Go

``` notranslate
go get cloud.google.com/go/bigquery
```

For more information, see [Setting Up a Go Development Environment](https://docs.cloud.google.com/go/docs/setup) .

### Java

If you are using [Maven](https://maven.apache.org/) , add the following to your `pom.xml` file. For more information about BOMs, see [The Google Cloud Platform Libraries BOM](https://cloud.google.com/java/docs/bom) .

    <!--  Using libraries-bom to manage versions.
    See https://github.com/GoogleCloudPlatform/cloud-opensource-java/wiki/The-Google-Cloud-Platform-Libraries-BOM -->
    <dependencyManagement>
      <dependencies>
        <dependency>
          <groupId>com.google.cloud</groupId>
          <artifactId>libraries-bom</artifactId>
          <version>26.62.0</version>
          <type>pom</type>
          <scope>import</scope>
        </dependency>
      </dependencies>
    </dependencyManagement>
    
    <dependencies>
      <dependency>
        <groupId>com.google.cloud</groupId>
        <artifactId>google-cloud-bigquery</artifactId>
      </dependency>
    </dependencies>

If you are using [Gradle](https://gradle.org/) , add the following to your dependencies:

    implementation platform('com.google.cloud:libraries-bom:26.45.0')
    
    implementation 'com.google.cloud:google-cloud-bigquery'

If you are using [sbt](https://www.scala-sbt.org/) , add the following to your dependencies:

    libraryDependencies += "com.google.cloud" % "google-cloud-bigquery" % "2.42.2"

If you're using Visual Studio Code or IntelliJ, you can add client libraries to your project using the following IDE plugins:

  - [Cloud Code for VS Code](https://docs.cloud.google.com/code/docs/vscode/client-libraries)
  - [Cloud Code for IntelliJ](https://docs.cloud.google.com/code/docs/intellij/client-libraries)

The plugins provide additional functionality, such as key management for service accounts. Refer to each plugin's documentation for details.

**Note:** Cloud Java client libraries do not currently support Android.

For more information, see [Setting Up a Java Development Environment](https://docs.cloud.google.com/java/docs/setup) .

### Node.js

``` notranslate
npm install @google-cloud/bigquery
```

For more information, see [Setting Up a Node.js Development Environment](https://docs.cloud.google.com/nodejs/docs/setup) .

### PHP

``` notranslate
composer require google/cloud-bigquery
```

For more information, see [Using PHP on Google Cloud](https://docs.cloud.google.com/php/docs) .

### Python

``` notranslate
pip install --upgrade google-cloud-bigquery
```

For more information, see [Setting Up a Python Development Environment](https://docs.cloud.google.com/python/docs/setup) .

### Ruby

``` notranslate
gem install google-cloud-bigquery
```

For more information, see [Setting Up a Ruby Development Environment](https://docs.cloud.google.com/ruby/docs/setup) .

<span id="setting_up_authentication"></span>

## Set up authentication

To authenticate calls to Google Cloud APIs, client libraries support [Application Default Credentials (ADC)](https://docs.cloud.google.com/docs/authentication/application-default-credentials) ; the libraries look for credentials in a set of defined locations and use those credentials to authenticate requests to the API. With ADC, you can make credentials available to your application in a variety of environments, such as local development or production, without needing to modify your application code.

For production environments, the way you set up ADC depends on the service and context. For more information, see [Set up Application Default Credentials](https://docs.cloud.google.com/docs/authentication/provide-credentials-adc) .

For a local development environment, you can set up ADC with the credentials that are associated with your Google Account:

1.  [Install](https://docs.cloud.google.com/sdk/docs/install) the Google Cloud CLI. After installation, [initialize](https://docs.cloud.google.com/sdk/docs/initializing) the Google Cloud CLI by running the following command:
    
        gcloud init
    
    If you're using an external identity provider (IdP), you must first [sign in to the gcloud CLI with your federated identity](https://docs.cloud.google.com/iam/docs/workforce-log-in-gcloud) .

2.  If you're using a local shell, then create local authentication credentials for your user account:
    
        gcloud auth application-default login
    
    You don't need to do this if you're using Cloud Shell.
    
    If an authentication error is returned, and you are using an external identity provider (IdP), confirm that you have [signed in to the gcloud CLI with your federated identity](https://docs.cloud.google.com/iam/docs/workforce-log-in-gcloud) .
    
    A sign-in screen appears. After you sign in, your credentials are stored in the [local credential file used by ADC](https://docs.cloud.google.com/docs/authentication/application-default-credentials#personal) .

<span id="using_the_client_library"></span>

## Use the client library

The following example shows how to initialize a client and perform a query on a BigQuery API public dataset.

**Note:** JRuby is not supported.

### C\#

    using Google.Cloud.BigQuery.V2;
    using System;
    
    public class BigQueryQuery
    {
        public void Query(
            string projectId = "your-project-id"
        )
        {
            BigQueryClient client = BigQueryClient.Create(projectId);
            string query = @"
                SELECT name FROM `bigquery-public-data.usa_names.usa_1910_2013`
                WHERE state = 'TX'
                LIMIT 100";
            BigQueryJob job = client.CreateQueryJob(
                sql: query,
                parameters: null,
                options: new QueryOptions { UseQueryCache = false });
            // Wait for the job to complete.
            job = job.PollUntilCompleted().ThrowOnAnyError();
            // Display the results
            foreach (BigQueryRow row in client.GetQueryResults(job.Reference))
            {
                Console.WriteLine($"{row["name"]}");
            }
        }
    }

### Go

    import (
     "context"
     "fmt"
     "io"
    
     "cloud.google.com/go/bigquery"
     "google.golang.org/api/iterator"
    )
    
    // queryBasic demonstrates issuing a query and reading results.
    func queryBasic(w io.Writer, projectID string) error {
     // projectID := "my-project-id"
     ctx := context.Background()
     client, err := bigquery.NewClient(ctx, projectID)
     if err != nil {
         return fmt.Errorf("bigquery.NewClient: %v", err)
     }
     defer client.Close()
    
     q := client.Query(
         "SELECT name FROM `bigquery-public-data.usa_names.usa_1910_2013` " +
             "WHERE state = \"TX\" " +
             "LIMIT 100")
     // Location must match that of the dataset(s) referenced in the query.
     q.Location = "US"
     // Run the query and print results when the query job is completed.
     job, err := q.Run(ctx)
     if err != nil {
         return err
     }
     status, err := job.Wait(ctx)
     if err != nil {
         return err
     }
     if err := status.Err(); err != nil {
         return err
     }
     it, err := job.Read(ctx)
     for {
         var row []bigquery.Value
         err := it.Next(&row)
         if err == iterator.Done {
             break
         }
         if err != nil {
             return err
         }
         fmt.Fprintln(w, row)
     }
     return nil
    }

### Java

    import com.google.cloud.bigquery.BigQuery;
    import com.google.cloud.bigquery.BigQueryException;
    import com.google.cloud.bigquery.BigQueryOptions;
    import com.google.cloud.bigquery.FieldValueList;
    import com.google.cloud.bigquery.Job;
    import com.google.cloud.bigquery.JobId;
    import com.google.cloud.bigquery.JobInfo;
    import com.google.cloud.bigquery.QueryJobConfiguration;
    import com.google.cloud.bigquery.TableResult;
    
    
    public class SimpleApp {
    
      public static void main(String... args) throws Exception {
        // TODO(developer): Replace these variables before running the app.
        String projectId = "MY_PROJECT_ID";
        simpleApp(projectId);
      }
    
      public static void simpleApp(String projectId) {
        try {
          BigQuery bigquery = BigQueryOptions.getDefaultInstance().getService();
          QueryJobConfiguration queryConfig =
              QueryJobConfiguration.newBuilder(
                      "SELECT CONCAT('https://stackoverflow.com/questions/', "
                          + "CAST(id as STRING)) as url, view_count "
                          + "FROM `bigquery-public-data.stackoverflow.posts_questions` "
                          + "WHERE tags like '%google-bigquery%' "
                          + "ORDER BY view_count DESC "
                          + "LIMIT 10")
                  // Use standard SQL syntax for queries.
                  // See: https://cloud.google.com/bigquery/sql-reference/
                  .setUseLegacySql(false)
                  .build();
    
          JobId jobId = JobId.newBuilder().setProject(projectId).build();
          Job queryJob = bigquery.create(JobInfo.newBuilder(queryConfig).setJobId(jobId).build());
    
          // Wait for the query to complete.
          queryJob = queryJob.waitFor();
    
          // Check for errors
          if (queryJob == null) {
            throw new RuntimeException("Job no longer exists");
          } else if (queryJob.getStatus().getExecutionErrors() != null
              && queryJob.getStatus().getExecutionErrors().size() > 0) {
            // TODO(developer): Handle errors here. An error here do not necessarily mean that the job
            // has completed or was unsuccessful.
            // For more details: https://cloud.google.com/bigquery/troubleshooting-errors
            throw new RuntimeException("An unhandled error has occurred");
          }
    
          // Get the results.
          TableResult result = queryJob.getQueryResults();
    
          // Print all pages of the results.
          for (FieldValueList row : result.iterateAll()) {
            // String type
            String url = row.get("url").getStringValue();
            String viewCount = row.get("view_count").getStringValue();
            System.out.printf("%s : %s views\n", url, viewCount);
          }
        } catch (BigQueryException | InterruptedException e) {
          System.out.println("Simple App failed due to error: \n" + e.toString());
        }
      }
    }

### Node.js

    // Import the Google Cloud client library using default credentials
    const {BigQuery} = require('@google-cloud/bigquery');
    const bigquery = new BigQuery();
    async function query() {
      // Queries the U.S. given names dataset for the state of Texas.
    
      const query = `SELECT name
        FROM \`bigquery-public-data.usa_names.usa_1910_2013\`
        WHERE state = 'TX'
        LIMIT 100`;
    
      // For all options, see https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs/query
      const options = {
        query: query,
        // Location must match that of the dataset(s) referenced in the query.
        location: 'US',
      };
    
      // Run the query as a job
      const [job] = await bigquery.createQueryJob(options);
      console.log(`Job ${job.id} started.`);
    
      // Wait for the query to finish
      const [rows] = await job.getQueryResults();
    
      // Print the results
      console.log('Rows:');
      rows.forEach(row => console.log(row));
    }

### PHP

    use Google\Cloud\BigQuery\BigQueryClient;
    use Google\Cloud\Core\ExponentialBackoff;
    
    /** Uncomment and populate these variables in your code */
    // $projectId = 'The Google project ID';
    // $query = 'SELECT id, view_count FROM `bigquery-public-data.stackoverflow.posts_questions`';
    
    $bigQuery = new BigQueryClient([
        'projectId' => $projectId,
    ]);
    $jobConfig = $bigQuery->query($query);
    $job = $bigQuery->startQuery($jobConfig);
    
    $backoff = new ExponentialBackoff(10);
    $backoff->execute(function () use ($job) {
        print('Waiting for job to complete' . PHP_EOL);
        $job->reload();
        if (!$job->isComplete()) {
            throw new Exception('Job has not yet completed', 500);
        }
    });
    $queryResults = $job->queryResults();
    
    $i = 0;
    foreach ($queryResults as $row) {
        printf('--- Row %s ---' . PHP_EOL, ++$i);
        foreach ($row as $column => $value) {
            printf('%s: %s' . PHP_EOL, $column, json_encode($value));
        }
    }
    printf('Found %s row(s)' . PHP_EOL, $i);

### Python

    from google.cloud import bigquery
    
    # Construct a BigQuery client object.
    client = bigquery.Client()
    
    query = """
        SELECT name, SUM(number) as total_people
        FROM `bigquery-public-data.usa_names.usa_1910_2013`
        WHERE state = 'TX'
        GROUP BY name, state
        ORDER BY total_people DESC
        LIMIT 20
    """
    rows = client.query_and_wait(query)  # Make an API request.
    
    print("The query data:")
    for row in rows:
        # Row values can be accessed by field name or index.
        print("name={}, count={}".format(row[0], row["total_people"]))

### Ruby

    require "google/cloud/bigquery"
    
    def query
      bigquery = Google::Cloud::Bigquery.new
      sql = "SELECT name FROM `bigquery-public-data.usa_names.usa_1910_2013` " \
            "WHERE state = 'TX' " \
            "LIMIT 100"
    
      # Location must match that of the dataset(s) referenced in the query.
      results = bigquery.query sql do |config|
        config.location = "US"
      end
    
      results.each do |row|
        puts row.inspect
      end
    end

<span id="additional_resources"></span>

## Additional resources

### C\#

The following list contains links to more resources related to the client library for C\#:

  - [API reference](https://docs.cloud.google.com/dotnet/docs/reference)
  - [Client libraries best practices](https://docs.cloud.google.com/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/google-cloud-dotnet/issues)
  - [`google-bigquery` on Stack Overflow](https://stackoverflow.com/search?q=%5Bgoogle-bigquery%5D+%5Bc%23%5D)
  - [Source code](https://github.com/googleapis/google-cloud-dotnet)

### Go

The following list contains links to more resources related to the client library for Go:

  - [API reference](https://docs.cloud.google.com/go/docs/reference)
  - [Client libraries best practices](https://docs.cloud.google.com/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/google-cloud-go/issues)
  - [`google-bigquery` on Stack Overflow](https://stackoverflow.com/search?q=%5Bgoogle-bigquery%5D+%5Bgo%5D)
  - [Source code](https://github.com/googleapis/google-cloud-go)

### Java

The following list contains links to more resources related to the client library for Java:

  - [API reference](https://docs.cloud.google.com/java/docs/reference/google-cloud-bigquery/latest/overview)
  - [Client libraries best practices](https://docs.cloud.google.com/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/java-bigquery/issues)
  - [`google-bigquery` on Stack Overflow](https://stackoverflow.com/search?q=%5Bgoogle-bigquery%5D+%5Bjava%5D)
  - [Source code](https://github.com/googleapis/java-bigquery)

### Node.js

The following list contains links to more resources related to the client library for Node.js:

  - [API reference](https://googleapis.dev/nodejs/bigquery/latest/index.html)
  - [Client libraries best practices](https://docs.cloud.google.com/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/nodejs-bigquery/issues)
  - [`google-bigquery` on Stack Overflow](https://stackoverflow.com/search?q=%5Bgoogle-bigquery%5D+%5Bnode.js%5D)
  - [Source code](https://github.com/googleapis/nodejs-bigquery)

### PHP

The following list contains links to more resources related to the client library for PHP:

  - [API reference](https://docs.cloud.google.com/php/docs/reference)
  - [Client libraries best practices](https://docs.cloud.google.com/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/google-cloud-php/issues)
  - [`google-bigquery` on Stack Overflow](https://stackoverflow.com/search?q=%5Bgoogle-bigquery%5D+%5Bphp%5D)
  - [Source code](https://github.com/googleapis/google-cloud-php)

### Python

The following list contains links to more resources related to the client library for Python:

  - [API reference](https://docs.cloud.google.com/python/docs/reference/bigquery/latest)
  - [Client libraries best practices](https://docs.cloud.google.com/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/python-bigquery/issues)
  - [`google-bigquery` on Stack Overflow](https://stackoverflow.com/search?q=%5Bgoogle-bigquery%5D+%5Bpython%5D)
  - [Source code](https://github.com/googleapis/python-bigquery)

### Ruby

The following list contains links to more resources related to the client library for Ruby:

  - [API reference](https://docs.cloud.google.com/ruby/docs/reference)
  - [Client libraries best practices](https://docs.cloud.google.com/apis/docs/client-libraries-best-practices)
  - [Issue tracker](https://github.com/googleapis/google-cloud-ruby/issues)
  - [`google-bigquery` on Stack Overflow](https://stackoverflow.com/search?q=%5Bgoogle-bigquery%5D+%5Bruby%5D)
  - [Source code](https://github.com/googleapis/google-cloud-ruby)

<span id="bigquery-dataframes"></span>

## BigQuery DataFrames (BigFrames)

[BigQuery DataFrames](https://dataframes.bigquery.dev/) is a pythonic DataFrame and machine learning (ML) API powered by the BigQuery engine. It implements the pandas and scikit-learn APIs by pushing the processing down to BigQuery through SQL conversion.

To get started with BigQuery DataFrames, install the library:

``` notranslate
pip install --upgrade bigframes
```

The following example shows how to initialize BigQuery DataFrames and perform a simple query.

    import bigframes.pandas as bpd
    
    # Set BigQuery DataFrames options
    # Note: The project option is not required in all environments.
    # On BigQuery Studio, the project ID is automatically detected.
    bpd.options.bigquery.project = your_gcp_project_id
    
    # Use "partial" ordering mode to generate more efficient queries, but the
    # order of the rows in DataFrames may not be deterministic if you have not
    # explictly sorted it. Some operations that depend on the order, such as
    # head() will not function until you explictly order the DataFrame. Set the
    # ordering mode to "strict" (default) for more pandas compatibility.
    bpd.options.bigquery.ordering_mode = "partial"
    
    # Create a DataFrame from a BigQuery table
    query_or_table = "bigquery-public-data.ml_datasets.penguins"
    df = bpd.read_gbq(query_or_table)
    
    # Efficiently preview the results using the .peek() method.
    df.peek()

For more information, see the [BigQuery DataFrames reference documentation](https://dataframes.bigquery.dev/) and [Getting started with BigQuery DataFrames](https://docs.cloud.google.com/bigquery/docs/dataframes-quickstart) .

<span id="third-party_client_libraries"></span>

## Third-party BigQuery API client libraries

In addition to the Google-supported client libraries listed in the tables above, a set of third-party libraries are available.

| Language | Library                                                                                                                                                                                                                                               |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Python   | [pandas-gbq](https://github.com/googleapis/python-bigquery-pandas) ( [usage guide](https://docs.cloud.google.com/bigquery/docs/pandas-gbq-migration) ), [ibis](https://ibis-project.org/) ( [tutorial](https://ibis-project.org/backends/bigquery/) ) |
| R        | [bigrquery](https://github.com/r-dbi/bigrquery) , [BigQueryR](https://github.com/cloudyr/bigQueryR)                                                                                                                                                   |
| Scala    | [spark-bigquery-connector](https://github.com/GoogleCloudDataproc/spark-bigquery-connector)                                                                                                                                                           |

### What's next?

  - [View available BigQuery code samples](https://docs.cloud.google.com/bigquery/docs/samples) .
  - [Query a public dataset with the BigQuery API client libraries](https://docs.cloud.google.com/bigquery/docs/quickstarts/quickstart-client-libraries) .
  - [Visualize BigQuery API public data using a Jupyter notebook](https://docs.cloud.google.com/bigquery/docs/visualize-jupyter) .
