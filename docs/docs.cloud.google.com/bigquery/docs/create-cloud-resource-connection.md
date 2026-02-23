# Create and set up a Cloud resource connection

As a BigQuery administrator, you can create a Cloud resource connection that enables data analysts to perform the following tasks:

  - [Query structured Cloud Storage data](/bigquery/docs/query-cloud-storage-using-biglake) using BigLake tables. [BigLake tables](/bigquery/docs/biglake-intro) enable you to query external data with access delegation.
  - [Query unstructured data in Cloud Storage](/bigquery/docs/object-tables) using [object tables](/bigquery/docs/object-table-introduction) .
  - [Implement remote functions](/bigquery/docs/remote-functions) with any supported languages in Cloud Run functions or Cloud Run.
  - [Query Spanner data using Spanner external datasets](/bigquery/docs/spanner-external-datasets) . Spanner external datasets with a Cloud resource connection enable you to query external data source with access delegation.
  - Perform generative AI tasks using a [BigQuery ML remote model](/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-remote-model) .

For more information about connections, see [Introduction to connections](/bigquery/docs/connections-api-intro) .

## Before you begin

  - Enable the BigQuery Connection API.

  - To get the permissions that you need to create a Cloud Resource connection, ask your administrator to grant you the following IAM roles :
    
      - [BigQuery Connection Admin](/iam/docs/roles-permissions/bigquery#bigquery.connectionAdmin) ( `  roles/bigquery.connectionAdmin  ` ) on the project
      - [Storage Object Viewer](/iam/docs/roles-permissions/storage#storage.objectViewer) ( `  roles/storage.objectViewer  ` ) on the bucket
    
    For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .
    
    You might also be able to get the required permissions through [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .
    
    If you want to query structured data using [BigLake tables based on Cloud Storage](/bigquery/docs/query-cloud-storage-using-biglake) or unstructured data using [object tables](/bigquery/docs/object-tables) , then the service account associated with the connection must also have the Storage Viewer ( `  roles/storage.viewer  ` ), Storage Object User ( `  roles/storage.objectUser  ` ), and Storage Legacy Bucket Reader ( `  roles/storage.legacyBucketReader  ` ) roles on the bucket that contains the external data.  

  - Ensure that your version of the Google Cloud SDK is 366.0.0 or later:
    
    ``` bash
    gcloud version
    ```
    
    If needed, [update the Google Cloud SDK](/sdk/docs/quickstart) .

### Location consideration

When you use Cloud Storage to store data files, we recommend that you use Cloud Storage [single-region](/storage/docs/locations#available-locations) or [dual-region](/storage/docs/locations#location-dr) buckets for optimal performance, not multi-region buckets.

## Create Cloud resource connections

BigLake uses a connection to access Cloud Storage. You can use this connection with a single table or a group of tables.

You can skip this step if you either have a default connection configured, or you have the BigQuery Admin role.

Create a [Cloud resource connection](/bigquery/docs/create-cloud-resource-connection) for the remote model to use, and get the connection's service account. Create the connection in the same [location](/bigquery/docs/locations) as the dataset that you created in the previous step.

Select one of the following options:

### Console

1.  Go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :
    
    If you don't see the left pane, click last\_page **Expand left pane** to open the pane.

3.  In the **Explorer** pane, expand your project name, and then click **Connections** .

4.  On the **Connections** page, click **Create connection** .

5.  For **Connection type** , choose **Vertex AI remote models, remote functions, BigLake and Spanner (Cloud Resource)** .

6.  In the **Connection ID** field, enter a name for your connection.

7.  For **Location type** , select a location for your connection. The connection should be colocated with your other resources such as datasets.

8.  Click **Create connection** .

9.  Click **Go to connection** .

10. In the **Connection info** pane, copy the service account ID for use in a later step.

### bq

1.  In a command-line environment, create a connection:
    
    ``` text
    bq mk --connection --location=REGION --project_id=PROJECT_ID \
        --connection_type=CLOUD_RESOURCE CONNECTION_ID
    ```
    
    The `  --project_id  ` parameter overrides the default project.
    
    Replace the following:
    
      - `  REGION  ` : your [connection region](/bigquery/docs/locations#supported_locations)
      - `  PROJECT_ID  ` : your Google Cloud project ID
      - `  CONNECTION_ID  ` : an ID for your connection
    
    When you create a connection resource, BigQuery creates a unique system service account and associates it with the connection.
    
    **Troubleshooting** : If you get the following connection error, [update the Google Cloud SDK](/sdk/docs/quickstart) :
    
    ``` console
    Flags parsing error: flag --connection_type=CLOUD_RESOURCE: value should be one of...
    ```

2.  Retrieve and copy the service account ID for use in a later step:
    
    ``` text
    bq show --connection PROJECT_ID.REGION.CONNECTION_ID
    ```
    
    The output is similar to the following:
    
    ``` console
    name                          properties
    1234.REGION.CONNECTION_ID     {"serviceAccountId": "connection-1234-9u56h9@gcp-sa-bigquery-condel.iam.gserviceaccount.com"}
    ```

### Python

Before trying this sample, follow the Python setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Python API reference documentation](/python/docs/reference/bigquery/latest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` python
import google.api_core.exceptions
from google.cloud import bigquery_connection_v1

client = bigquery_connection_v1.ConnectionServiceClient()


def create_connection(
    project_id: str,
    location: str,
    connection_id: str,
):
    """Creates a BigQuery connection to a Cloud Resource.

    Cloud Resource connection creates a service account which can then be
    granted access to other Google Cloud resources for federated queries.

    Args:
        project_id: The Google Cloud project ID.
        location: The location of the connection (for example, "us-central1").
        connection_id: The ID of the connection to create.
    """

    parent = client.common_location_path(project_id, location)

    connection = bigquery_connection_v1.Connection(
        friendly_name="Example Connection",
        description="A sample connection for a Cloud Resource.",
        cloud_resource=bigquery_connection_v1.CloudResourceProperties(),
    )

    try:
        created_connection = client.create_connection(
            parent=parent, connection_id=connection_id, connection=connection
        )
        print(f"Successfully created connection: {created_connection.name}")
        print(f"Friendly name: {created_connection.friendly_name}")
        print(
            f"Service Account: {created_connection.cloud_resource.service_account_id}"
        )

    except google.api_core.exceptions.AlreadyExists:
        print(f"Connection with ID '{connection_id}' already exists.")
        print("Please use a different connection ID.")
    except Exception as e:
        print(f"An unexpected error occurred while creating the connection: {e}")
```

### Node.js

Before trying this sample, follow the Node.js setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Node.js API reference documentation](https://googleapis.dev/nodejs/bigquery/latest/index.html) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` javascript
const {ConnectionServiceClient} =
  require('@google-cloud/bigquery-connection').v1;
const {status} = require('@grpc/grpc-js');

const client = new ConnectionServiceClient();

/**
 * Creates a new BigQuery connection to a Cloud Resource.
 *
 * A Cloud Resource connection creates a service account that can be granted access
 * to other Google Cloud resources.
 *
 * @param {string} projectId The Google Cloud project ID. for example, 'example-project-id'
 * @param {string} location The location of the project to create the connection in. for example, 'us-central1'
 * @param {string} connectionId The ID of the connection to create. for example, 'example-connection-id'
 */
async function createConnection(projectId, location, connectionId) {
  const parent = client.locationPath(projectId, location);

  const connection = {
    friendlyName: 'Example Connection',
    description: 'A sample connection for a Cloud Resource',
    // The service account for this cloudResource will be created by the API.
    // Its ID will be available in the response.
    cloudResource: {},
  };

  const request = {
    parent,
    connectionId,
    connection,
  };

  try {
    const [response] = await client.createConnection(request);

    console.log(`Successfully created connection: ${response.name}`);
    console.log(`Friendly name: ${response.friendlyName}`);

    console.log(`Service Account: ${response.cloudResource.serviceAccountId}`);
  } catch (err) {
    if (err.code === status.ALREADY_EXISTS) {
      console.log(`Connection '${connectionId}' already exists.`);
    } else {
      console.error(`Error creating connection: ${err.message}`);
    }
  }
}
```

### Terraform

Use the [`  google_bigquery_connection  `](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/bigquery_connection) resource.

**Note:** To create BigQuery objects using Terraform, you must enable the [Cloud Resource Manager API](/resource-manager/reference/rest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

The following example creates a Cloud resource connection named `  my_cloud_resource_connection  ` in the `  US  ` region:

``` terraform
# This queries the provider for project information.
data "google_project" "default" {}

# This creates a cloud resource connection in the US region named my_cloud_resource_connection.
# Note: The cloud resource nested object has only one output field - serviceAccountId.
resource "google_bigquery_connection" "default" {
  connection_id = "my_cloud_resource_connection"
  project       = data.google_project.default.project_id
  location      = "US"
  cloud_resource {}
}
```

To apply your Terraform configuration in a Google Cloud project, complete the steps in the following sections.

## Prepare Cloud Shell

1.  Launch [Cloud Shell](https://shell.cloud.google.com/) .

2.  Set the default Google Cloud project where you want to apply your Terraform configurations.
    
    You only need to run this command once per project, and you can run it in any directory.
    
    ``` text
    export GOOGLE_CLOUD_PROJECT=PROJECT_ID
    ```
    
    Environment variables are overridden if you set explicit values in the Terraform configuration file.

## Prepare the directory

Each Terraform configuration file must have its own directory (also called a *root module* ).

1.  In [Cloud Shell](https://shell.cloud.google.com/) , create a directory and a new file within that directory. The filename must have the `  .tf  ` extension—for example `  main.tf  ` . In this tutorial, the file is referred to as `  main.tf  ` .
    
    ``` text
    mkdir DIRECTORY && cd DIRECTORY && touch main.tf
    ```

2.  If you are following a tutorial, you can copy the sample code in each section or step.
    
    Copy the sample code into the newly created `  main.tf  ` .
    
    Optionally, copy the code from GitHub. This is recommended when the Terraform snippet is part of an end-to-end solution.

3.  Review and modify the sample parameters to apply to your environment.

4.  Save your changes.

5.  Initialize Terraform. You only need to do this once per directory.
    
    ``` text
    terraform init
    ```
    
    Optionally, to use the latest Google provider version, include the `  -upgrade  ` option:
    
    ``` text
    terraform init -upgrade
    ```

## Apply the changes

1.  Review the configuration and verify that the resources that Terraform is going to create or update match your expectations:
    
    ``` text
    terraform plan
    ```
    
    Make corrections to the configuration as necessary.

2.  Apply the Terraform configuration by running the following command and entering `  yes  ` at the prompt:
    
    ``` text
    terraform apply
    ```
    
    Wait until Terraform displays the "Apply complete\!" message.

3.  [Open your Google Cloud project](https://console.cloud.google.com/) to view the results. In the Google Cloud console, navigate to your resources in the UI to make sure that Terraform has created or updated them.

**Note:** Terraform samples typically assume that the required APIs are enabled in your Google Cloud project.

## Grant access to the service account

To create remote functions, you must [grant required roles](/bigquery/docs/remote-functions#grant_permission_on_function) to Cloud Run functions or Cloud Run.

To connect to Cloud Storage, you must give the new connection read-only access to Cloud Storage so that BigQuery can access files on behalf of users.

Select one of the following options:

### Console

We recommend that you grant the connection resource service account the [Storage Object User IAM role](/storage/docs/access-control/iam-roles) ( `  roles/storage.objectUser  ` ), which lets the service account access Cloud Storage buckets.

1.  Go to the **IAM & Admin** page.

2.  Click person\_add **Grant access** .
    
    The **Add principals** dialog opens.

3.  In the **New principals** field, enter the service account ID that you copied earlier.

4.  In the **Select a role** field, select **Cloud Storage** , and then select **Storage Object User** .

5.  Click **Save** .

### gcloud

Use the [`  gcloud storage buckets add-iam-policy-binding  ` command](/sdk/gcloud/reference/storage/buckets/add-iam-policy-binding) :

``` text
gcloud storage buckets add-iam-policy-binding gs://BUCKET \
--member=serviceAccount:MEMBER \
--role=roles/storage.objectUser
```

Replace the following:

  - `  BUCKET  ` : the name of your storage bucket.
  - `  MEMBER  ` : the service account ID that you copied earlier.

For more information, see [Add a principal to a bucket-level policy](/storage/docs/access-control/using-iam-permissions#bucket-add) .

### Terraform

Use the [`  google_bigquery_connection  `](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/bigquery_connection) resource.

**Note:** To create BigQuery objects using Terraform, you must enable the [Cloud Resource Manager API](/resource-manager/reference/rest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

The following example grants IAM role access to the service account of the Cloud resource connection:

``` terraform
# This queries the provider for project information.
data "google_project" "default" {}

# This creates a cloud resource connection in the US region named my_cloud_resource_connection.
# Note: The cloud resource nested object has only one output field - serviceAccountId.
resource "google_bigquery_connection" "default" {
  connection_id = "my_cloud_resource_connection"
  project       = data.google_project.default.project_id
  location      = "US"
  cloud_resource {}
}

## This grants IAM role access to the service account of the connection created in the previous step.
resource "google_project_iam_member" "connectionPermissionGrant" {
  project = data.google_project.default.project_id
  role    = "roles/storage.objectViewer"
  member  = "serviceAccount:${google_bigquery_connection.default.cloud_resource[0].service_account_id}"
}
```

To apply your Terraform configuration in a Google Cloud project, complete the steps in the following sections.

## Prepare Cloud Shell

1.  Launch [Cloud Shell](https://shell.cloud.google.com/) .

2.  Set the default Google Cloud project where you want to apply your Terraform configurations.
    
    You only need to run this command once per project, and you can run it in any directory.
    
    ``` text
    export GOOGLE_CLOUD_PROJECT=PROJECT_ID
    ```
    
    Environment variables are overridden if you set explicit values in the Terraform configuration file.

## Prepare the directory

Each Terraform configuration file must have its own directory (also called a *root module* ).

1.  In [Cloud Shell](https://shell.cloud.google.com/) , create a directory and a new file within that directory. The filename must have the `  .tf  ` extension—for example `  main.tf  ` . In this tutorial, the file is referred to as `  main.tf  ` .
    
    ``` text
    mkdir DIRECTORY && cd DIRECTORY && touch main.tf
    ```

2.  If you are following a tutorial, you can copy the sample code in each section or step.
    
    Copy the sample code into the newly created `  main.tf  ` .
    
    Optionally, copy the code from GitHub. This is recommended when the Terraform snippet is part of an end-to-end solution.

3.  Review and modify the sample parameters to apply to your environment.

4.  Save your changes.

5.  Initialize Terraform. You only need to do this once per directory.
    
    ``` text
    terraform init
    ```
    
    Optionally, to use the latest Google provider version, include the `  -upgrade  ` option:
    
    ``` text
    terraform init -upgrade
    ```

## Apply the changes

1.  Review the configuration and verify that the resources that Terraform is going to create or update match your expectations:
    
    ``` text
    terraform plan
    ```
    
    Make corrections to the configuration as necessary.

2.  Apply the Terraform configuration by running the following command and entering `  yes  ` at the prompt:
    
    ``` text
    terraform apply
    ```
    
    Wait until Terraform displays the "Apply complete\!" message.

3.  [Open your Google Cloud project](https://console.cloud.google.com/) to view the results. In the Google Cloud console, navigate to your resources in the UI to make sure that Terraform has created or updated them.

**Note:** Terraform samples typically assume that the required APIs are enabled in your Google Cloud project.

**Note:** When you [migrate users to BigLake tables](/bigquery/docs/external-data-cloud-storage#upgrade-external-tables-to-biglake-tables) , remove their permissions to directly access Cloud Storage. Direct file access lets users bypass governance policies (such as row- and column-level security) set on BigLake tables.

## Share connections with users

You can grant the following roles to let users query data and manage connections:

  - `  roles/bigquery.connectionUser  ` : enables users to use connections to connect with external data sources and run queries on them.

  - `  roles/bigquery.connectionAdmin  ` : enables users to manage connections.

For more information about IAM roles and permissions in BigQuery, see [Predefined roles and permissions](/bigquery/access-control) .

Select one of the following options:

### Console

1.  Go to the **BigQuery** page.
    
    Connections are listed in your project, in a group called **Connections** .

2.  In the left pane, click explore **Explorer** :
    
    If you don't see the left pane, click last\_page **Expand left pane** to open the pane.

3.  Click your project, click **Connections** , and then select a connection.

4.  In the **Details** pane, click **Share** to share a connection. Then do the following:
    
    1.  In the **Connection permissions** dialog, share the connection with other principals by adding or editing principals.
    
    2.  Click **Save** .

### bq

You cannot share a connection with the bq command-line tool. To share a connection, use the Google Cloud console or the BigQuery Connections API method to share a connection.

### API

Use the [`  projects.locations.connections.setIAM  ` method](/bigquery/docs/reference/bigqueryconnection/rest/v1/projects.locations.connections#methods) in the BigQuery Connections REST API reference section, and supply an instance of the `  policy  ` resource.

### Java

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` java
import com.google.api.resourcenames.ResourceName;
import com.google.cloud.bigquery.connection.v1.ConnectionName;
import com.google.cloud.bigqueryconnection.v1.ConnectionServiceClient;
import com.google.iam.v1.Binding;
import com.google.iam.v1.Policy;
import com.google.iam.v1.SetIamPolicyRequest;
import java.io.IOException;

// Sample to share connections
public class ShareConnection {

  public static void main(String[] args) throws IOException {
    // TODO(developer): Replace these variables before running the sample.
    String projectId = "MY_PROJECT_ID";
    String location = "MY_LOCATION";
    String connectionId = "MY_CONNECTION_ID";
    shareConnection(projectId, location, connectionId);
  }

  static void shareConnection(String projectId, String location, String connectionId)
      throws IOException {
    try (ConnectionServiceClient client = ConnectionServiceClient.create()) {
      ResourceName resource = ConnectionName.of(projectId, location, connectionId);
      Binding binding =
          Binding.newBuilder()
              .addMembers("group:example-analyst-group@google.com")
              .setRole("roles/bigquery.connectionUser")
              .build();
      Policy policy = Policy.newBuilder().addBindings(binding).build();
      SetIamPolicyRequest request =
          SetIamPolicyRequest.newBuilder()
              .setResource(resource.toString())
              .setPolicy(policy)
              .build();
      client.setIamPolicy(request);
      System.out.println("Connection shared successfully");
    }
  }
}
```

## What's next

  - Learn about different [connection types](/bigquery/docs/connections-api-intro) .
  - Learn about [managing connections](/bigquery/docs/working-with-connections) .
  - Learn about [BigLake tables](/bigquery/docs/biglake-intro) .
  - Learn how to [create BigLake tables](/bigquery/docs/query-cloud-storage-using-biglake) .
  - Learn how to [upgrade external tables to BigLake tables](/bigquery/docs/external-data-cloud-storage#upgrade-external-tables-to-biglake-tables) .
  - Learn about [object tables](/bigquery/docs/object-table-introduction) and how to [create them](/bigquery/docs/object-tables) .
  - Learn how to [implement remote functions](/bigquery/docs/remote-functions) .
  - Learn how to [create Spanner external datasets](/bigquery/docs/spanner-external-datasets#create_an_external_dataset) .
