# Enable the BigQuery Data Transfer Service

To use the BigQuery Data Transfer Service, you must complete the following steps as a project [Owner](/iam/docs/roles-overview#legacy-basic) :

  - Create a project and enable the BigQuery API.
  - Enable the BigQuery Data Transfer Service.

For more information on Identity and Access Management (IAM) roles, see [Roles and permissions](/iam/docs/roles-overview) in the IAM documentation.

**Note:** If you call the BigQuery Data Transfer Service API immediately after you enable BigQuery Data Transfer Service programmatically, you should implement a retry mechanism with backoff delays between consecutive calls. This is necessary because API enablement is asynchronous and subject to propagation delays caused by eventual consistency.

## Create a project and enable the BigQuery API

Before using the BigQuery Data Transfer Service, you must create a project and, in most cases, enable billing on that project. You can use an existing project with the BigQuery Data Transfer Service, or you can create a new one. If you are using an existing project, you may also need to enable the BigQuery API.

To create a project and enable the BigQuery API:

1.  In the Google Cloud console, go to the project selector page.

2.  Select or create a Google Cloud project.
    
    **Roles required to select or create a project**
    
      - **Select a project** : Selecting a project doesn't require a specific IAM role—you can select any project that you've been granted a role on.
      - **Create a project** : To create a project, you need the Project Creator role ( `  roles/resourcemanager.projectCreator  ` ), which contains the `  resourcemanager.projects.create  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .
    
    **Note** : If you don't plan to keep the resources that you create in this procedure, create a project instead of selecting an existing project. After you finish these steps, you can delete the project, removing all resources associated with the project.

3.  Enable billing on your project for all transfers. You are billed $0 for free transfers.
    
    Enabling billing is only required once per project, even if you are transferring data from multiple sources. Billing must also be enabled to query the data in BigQuery, after the data is transferred.
    
    [Learn how to confirm that billing is enabled on your project](/billing/docs/how-to/modify-project) .

4.  BigQuery is automatically enabled in new projects. To activate BigQuery in an existing project, enable the BigQuery API.  
      

## Enable the BigQuery Data Transfer Service

Before you can create a transfer, you must enable the BigQuery Data Transfer Service. To enable the BigQuery Data Transfer Service, you must be granted the [Owner](/iam/docs/roles-overview#legacy-basic) role for your project.

To enable the BigQuery Data Transfer Service:

1.  Open the [BigQuery Data Transfer API](https://console.cloud.google.com/apis/library/bigquerydatatransfer.googleapis.com) page in the API library.

2.  From the drop-down menu, select the appropriate project.

3.  Click the ENABLE button.

## Service Agent

The BigQuery Data Transfer Service uses a [service agent](/iam/docs/service-account-types#service-agents) to access and manage your resources. This includes, but is not limited to, the following resources:

  - Retrieving an access token for the service account to use when authorizing the data transfer.
  - Publishing notifications to the provided Pub/Sub topic if enabled.
  - Starting BigQuery jobs.
  - Retrieving events from the provided Pub/Sub subscription for Cloud Storage event-driven transfer

The service agent is created automatically on your behalf after you enable the BigQuery Data Transfer Service and use the API for the first time. Upon service agent creation, Google grants the predefined [service agent role](/bigquery/docs/access-control#bigquerydatatransfer.serviceAgent) automatically.

### Cross-project Service Account Authorization

If you authorize the data transfer using a service account from a project that is different from the project with the BigQuery Data Transfer Service enabled, you must grant the `  roles/iam.serviceAccountTokenCreator  ` role to the service agent using the following Google Cloud CLI command:

``` text
gcloud iam service-accounts add-iam-policy-binding service_account \
--member serviceAccount:service-project_number@gcp-sa-bigquerydatatransfer.iam.gserviceaccount.com \
--role roles/iam.serviceAccountTokenCreator
```

Where:

  - service\_account is the cross-project service account used for authorizing the data transfer.
  - project\_number is the project number of the project where the BigQuery Data Transfer Service is enabled.

For more information about cross-project resource configuration, see [Configuring for a resource in a different project](/iam/docs/attach-service-accounts#attaching-different-project) in the Identity and Access Management service account impersonation documentation.

### Manual Service Agent Creation

If you want to trigger service agent creation before you interact with the API, for example, if you need to grant extra roles to the service agent, you can use one of the following approaches:

  - API: [services.GenerateServiceIdentity](/service-usage/docs/reference/rest/v1beta1/services/generateServiceIdentity)
  - gcloud CLI: [gcloud beta services identity create](/sdk/gcloud/reference/beta/services/identity/create)
  - Terraform Provider: [google\_project\_service\_identity](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/project_service_identity)

When you manually trigger service agent creation, Google doesn't grant the predefined [service agent role](/bigquery/docs/access-control#bigquerydatatransfer.serviceAgent) automatically. You must manually grant the service agent the predefined role using the following Google Cloud CLI command:

``` text
gcloud projects add-iam-policy-binding project_number \
--member serviceAccount:service-project_number@gcp-sa-bigquerydatatransfer.iam.gserviceaccount.com \
--role roles/bigquerydatatransfer.serviceAgent
```

Where:

  - project\_number is the project number of the project where the BigQuery Data Transfer Service is enabled.

**Warning:** Don't revoke the service agent role from the service agent. If you revoke the role, the BigQuery Data Transfer Service will no longer work.

## Grant `     bigquery.admin    ` access

We recommend granting the `  bigquery.admin  ` predefined IAM role to users who create BigQuery Data Transfer Service transfers. The `  bigquery.admin  ` role includes the IAM permissions needed to perform the most common tasks. The `  bigquery.admin  ` role includes the following BigQuery Data Transfer Service permissions:

  - BigQuery Data Transfer Service permissions:
      - `  bigquery.transfers.update  `
      - `  bigquery.transfers.get  `
  - BigQuery permissions:
      - `  bigquery.datasets.get  `
      - `  bigquery.datasets.getIamPolicy  `
      - `  bigquery.datasets.update  `
      - `  bigquery.datasets.setIamPolicy  `
      - `  bigquery.jobs.create  `

**Note:** Starting March 17, 2026, the BigQuery Data Transfer Service will require the `  bigquery.datasets.getIamPolicy  ` and `  bigquery.datasets.setIamPolicy  ` permissions. For more information, see [Changes to dataset-level access controls](/bigquery/docs/dataset-access-control) .

**Note:** If the `  bigquery.admin  ` role is too broad for a specific use case, you can [create a custom IAM role](/iam/docs/creating-custom-roles) with only the necessary permissions.

In some cases, the required permissions might differ between different data sources. Refer to the "Required permissions" section in each data source transfer guide for specific IAM information. For example, see [Amazon S3 transfer permissions](/bigquery/docs/s3-transfer#required_permissions) or [Cloud Storage transfer permissions](/bigquery/docs/cloud-storage-transfer#required_permissions) .

To grant the `  bigquery.admin  ` role:

### Console

1.  Open the IAM page in the Google Cloud console

2.  Click **Select a project** .

3.  Select a project and click **Open** .

4.  Click **Add** to add new members to the project and set their permissions.

5.  In the **Add members** dialog:
    
      - For **Members** , enter the email address of the user or group.
    
      - In the **Select a role** drop-down, click **BigQuery \> BigQuery Admin** .
    
      - Click **Add** .

### gcloud

You can use the Google Cloud CLI to grant a user or group the `  bigquery.admin  ` role.

**Note:** When managing access for users in [external identity providers](/iam/docs/workforce-identity-federation) , replace instances of Google Account principal identifiers—like `  user:kiran@example.com  ` , `  group:support@example.com  ` , and `  domain:example.com  ` —with appropriate [Workforce Identity Federation principal identifiers](/iam/docs/principal-identifiers) .

To add a single binding to your project's IAM policy, type the following command. To add a user, supply the `  --member  ` flag in the format `  user:user@example.com  ` . To add a group, supply the `  --member  ` flag in the format `  group:group@example.com  ` .

``` text
gcloud projects add-iam-policy-binding project_id \
--member principal:address \
--role roles/bigquery.admin
```

Where:

  - project\_id is your project ID.
  - principal is either `  group  ` or `  user  ` .
  - address is the user or group's email address.

For example:

``` text
gcloud projects add-iam-policy-binding myproject \
--member group:group@example.com \
--role roles/bigquery.admin
```

The command outputs the updated policy:

``` text
    bindings:
    - members:
      - group:group@example.com
        role: roles/bigquery.admin
    
```

For more information on IAM roles in BigQuery, see [Predefined roles and permissions](/bigquery/access-control) .

## What's next

After enabling the BigQuery Data Transfer Service, create a transfer for your data source.

  - [Amazon S3](/bigquery/docs/s3-transfer)
  - [Amazon Redshift](/bigquery/docs/migration/redshift)
  - [Apache Hive](/bigquery/docs/hdfs-data-lake-transfer) ( [Preview](https://cloud.google.com/products/#product-launch-stages) )
  - [Azure Blob Storage](/bigquery/docs/blob-storage-transfer)
  - [Campaign Manager](/bigquery/docs/doubleclick-campaign-transfer)
  - [Cloud Storage](/bigquery/docs/cloud-storage-transfer)
  - [Comparison Shopping Service (CSS) Center](/bigquery/docs/css-center-transfer-schedule-transfers) ( [Preview](https://cloud.google.com/products/#product-launch-stages) )
  - [Display & Video 360](/bigquery/docs/display-video-transfer)
  - [Facebook Ads](/bigquery/docs/facebook-ads-transfer)
  - [Google Ad Manager](/bigquery/docs/doubleclick-publisher-transfer)
  - [Google Ads](/bigquery/docs/google-ads-transfer)
  - [Google Analytics 4](/bigquery/docs/google-analytics-4-transfer)
  - [Google Merchant Center](/bigquery/docs/merchant-center-transfer) ( [Preview](https://cloud.google.com/products/#product-launch-stages) )
  - [Google Play](/bigquery/docs/play-transfer)
  - [HubSpot](/bigquery/docs/hubspot-transfer) ( [Preview](https://cloud.google.com/products/#product-launch-stages) )
  - [Klaviyo](/bigquery/docs/klaviyo-transfer) ( [Preview](https://cloud.google.com/products/#product-launch-stages) )
  - [Mailchimp](/bigquery/docs/mailchimp-transfer) ( [Preview](https://cloud.google.com/products/#product-launch-stages) )
  - [Microsoft SQL Server](/bigquery/docs/sqlserver-transfer) ( [Preview](https://cloud.google.com/products/#product-launch-stages) )
  - [MySQL](/bigquery/docs/mysql-transfer)
  - [PayPal](/bigquery/docs/paypal-transfer) ( [Preview](https://cloud.google.com/products/#product-launch-stages) )
  - [Oracle](/bigquery/docs/oracle-transfer)
  - [PostgreSQL](/bigquery/docs/postgresql-transfer)
  - [Salesforce](/bigquery/docs/salesforce-transfer)
  - [Salesforce Marketing Cloud](/bigquery/docs/sfmc-transfer)
  - [Search Ads 360](/bigquery/docs/search-ads-transfer)
  - [ServiceNow](/bigquery/docs/servicenow-transfer)
  - [Shopify](/bigquery/docs/shopify-transfer) ( [Preview](https://cloud.google.com/products/#product-launch-stages) )
  - [Snowflake](/bigquery/docs/migration/snowflake-transfer) ( [Preview](https://cloud.google.com/products/#product-launch-stages) )
  - [Stripe](/bigquery/docs/stripe-transfer) ( [Preview](https://cloud.google.com/products/#product-launch-stages) )
  - [Teradata](/bigquery/docs/migration/teradata)
  - [YouTube Channel](/bigquery/docs/youtube-channel-transfer)
  - [YouTube Content Owner](/bigquery/docs/youtube-content-owner-transfer)
