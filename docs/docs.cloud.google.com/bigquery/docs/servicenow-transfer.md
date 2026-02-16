# Load ServiceNow data into BigQuery

You can load data from ServiceNow to BigQuery using the BigQuery Data Transfer Service for ServiceNow connector. With the BigQuery Data Transfer Service, you can schedule recurring transfer jobs that add your latest data from ServiceNow to BigQuery.

## Limitations

ServiceNow data transfers are subject to the following limitations:

  - The ServiceNow connector only supports the [ServiceNow table API](https://www.servicenow.com/docs/bundle/zurich-api-reference/page/integrate/inbound-rest/concept/c_TableAPI.html) .
  - We don't recommend running concurrent data transfers on the same ServiceNow instance. This can lead to delays or failures due to load on the ServiceNow instance.
      - We recommend timing your transfer start times apart to prevent overlapping transfer runs.
  - To improve data transfer performance, we recommend limiting the number of assets to 20 items per data transfer.
  - The minimum interval time between recurring data transfers is 15 minutes. The default interval for a recurring transfer is 24 hours.
  - A single transfer configuration can only support one data transfer run at a given time. In the case where a second data transfer is scheduled to run before the first transfer is completed, then only the first data transfer completes while any other data transfers that overlap with the first transfer is skipped.
      - To avoid skipped transfers within a single transfer configuration, we recommend that you increase the duration of time between large data transfers by configuring the **Repeat frequency** .
  - To use a network attachment with this data transfer, you must first [create a network attachment by defining a static IP address](/bigquery/docs/connections-with-network-attachment) .

## Before you begin

Before you create a ServiceNow data transfer, do the following for ServiceNow and BigQuery.

### ServiceNow prerequisites

  - To access ServiceNow APIs, create [OAuth credentials](https://www.servicenow.com/docs/csh?topicname=t_CreateEndpointforExternalClients.html&version=latest) .

  - The following ServiceNow applications must all be enabled in the ServiceNow instance:
    
      - [Procurement](https://docs.servicenow.com/csh?topicname=t_ActivateProcurement.html&version=latest)
      - [Product Catalog](https://docs.servicenow.com/csh?topicname=c_ProductCatalog.html&version=latest)
      - [Contract Management](https://docs.servicenow.com/csh?topicname=c_ContractManagement.html&version=latest)

  - To start a ServiceNow transfer, you must have the correct credentials to connect to the ServiceNow instance.
    
      - To obtain your credentials to a ServiceNow developer instance, login to the [ServiceNow developer portal](https://developer.servicenow.com/dev.do) . You can use the username and password listed in the **Manage instance password** page. For information on resetting your ServiceNow password, see [Password Reset](https://www.servicenow.com/docs/csh?topicname=password-reset-landing-page.html&version=latest)
      - To obtain your credentials to a ServiceNow production or sub-production instance, contact your ServiceNow customer administrator to request the username and password.

### BigQuery prerequisites

  - Complete all actions required to [enable the BigQuery Data Transfer Service](/bigquery/docs/enable-transfer-service) .
  - [Create a BigQuery dataset](/bigquery/docs/datasets) for storing the data.
  - If you intend to set up transfer run notifications for Pub/Sub, ensure that you have the `  pubsub.topics.setIamPolicy  ` Identity and Access Management (IAM) permission. If you only set up email notifications, Pub/Sub permissions aren't required. For more information, see [BigQuery Data Transfer Service run notifications](/bigquery/docs/transfer-run-notifications) .

### Required BigQuery roles

To get the permissions that you need to create a BigQuery Data Transfer Service data transfer, ask your administrator to grant you the [BigQuery Admin](/iam/docs/roles-permissions/bigquery#bigquery.admin) ( `  roles/bigquery.admin  ` ) IAM role on your project. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

This predefined role contains the permissions required to create a BigQuery Data Transfer Service data transfer. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to create a BigQuery Data Transfer Service data transfer:

  - BigQuery Data Transfer Service permissions:
      - `  bigquery.transfers.update  `
      - `  bigquery.transfers.get  `
  - BigQuery permissions:
      - `  bigquery.datasets.get  `
      - `  bigquery.datasets.getIamPolicy  `
      - `  bigquery.datasets.update  `
      - `  bigquery.datasets.setIamPolicy  `
      - `  bigquery.jobs.create  `

You might also be able to get these permissions with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

For more information, see [Grant `  bigquery.admin  ` access](/bigquery/docs/enable-transfer-service#grant_bigqueryadmin_access) .

## Set up a ServiceNow data transfer

Add ServiceNow data into BigQuery by setting up a transfer configuration using one of the following options:

### Console

1.  Go to the Data transfers page in the Google Cloud console.

2.  Click add **Create transfer** .

3.  In the **Source type** section, for **Source** , select **ServiceNow** .

4.  In the **Data source details** section, do the following:
    
      - (Optional) For **Network attachment** , select a network attachment from the drop-down menu, or click **Create Network Attachment** .
          - Select a network attachment to configure this data transfer to use a single, consistent IP address. You can use this option if your ServiceNow instance is configured to only accept traffic from specific IP addresses.
          - For more information about creating a network attachment, see [Configure connections with network attachments](/bigquery/docs/connections-with-network-attachment)
          - For more information about defining IP addresses in ServiceNow, see [Define allowed ServiceNow internal IP addresses](https://www.servicenow.com/docs/csh?topicname=sc-ip-addresses-access-allowlist.html&version=latest)
      - For **Instance ID** , enter the ServiceNow instance ID. You can get this from your ServiceNow URL—for example, `  https:// INSTANCE_ID .service-now.com  ` .
      - (Optional) For **ServiceNow Cloud Type** , select the cloud type for your ServiceNow account:
          - Select **Commercial** if your ServiceNow instance URL follows the pattern `  https:// INSTANCE_ID .service-now.com  ` . This is the default value.
          - Select **Government Community Cloud (GCC)** if your ServiceNow instance URL follows the pattern `  https:// INSTANCE_ID .servicenowservices.com  ` .
      - For **Username** , enter the ServiceNow username to use for the connection.
      - For **Password** , enter the ServiceNow password.
      - For **Client ID** , enter the client ID from your OAuth credentials. To generate credentials, see [Create OAuth Credentials](https://docs.oracle.com/cd/B13789_01/server.101/b10759/statements_9013.htm) .
      - For **Client secret** , enter the client secret from your OAuth credentials.
      - For **ServiceNow tables to transfer** , enter the names of the ServiceNow tables to transfer, or click **Browse** and select the tables that you want to transfer.
      - For **Value type** , choose one of the following:
          - To transfer the values stored in the database, choose **Actual** .
          - To transfer the display values of the columns, choose **Display** .

5.  In the **Destination settings** section, for **Dataset** , select the dataset that you created to store your data.

6.  In the **Transfer config name** section, for **Display name** , enter a name for the data transfer.

7.  In the **Schedule options** section, do the following:
    
      - In the **Repeat frequency** list, select an option to specify how often this data transfer runs. To specify a custom repeat frequency, select **Custom** . If you select **On-demand** , then this data transfer runs when you [manually trigger the transfer](/bigquery/docs/working-with-transfers#manually_trigger_a_transfer) .
      - If applicable, select either **Start now** or **Start at set time** , and provide a start date and run time.

8.  Optional: In the **Notification options** section, do the following:
    
      - To enable email notifications, click the **Email notification** toggle. When you enable this option, the transfer administrator receives an email notification when a transfer run fails.
      - To enable [Pub/Sub transfer run notifications](/bigquery/docs/transfer-run-notifications) for this data transfer, click the **Pub/Sub notifications** toggle. You can select your [topic](/pubsub/docs/overview#types) name, or you can click **Create a topic** to create one.

9.  Click **Save** .

### bq

Enter the [`  bq mk  `](/bigquery/docs/reference/bq-cli-reference#bq_mk) command and supply the transfer creation flag, `  --transfer_config  ` :

``` text
bq mk
    --transfer_config
    --project_id=PROJECT_ID
    --data_source=DATA_SOURCE
    --display_name=DISPLAY_NAME
    --target_dataset=DATASET
    --params='PARAMETERS'
```

Replace the following:

  - `  PROJECT_ID  ` (optional): Your Google Cloud project ID. If a project ID isn't specified, the default project is used.

  - `  DATA_SOURCE  ` : the data source (for example, `  servicenow  ` ).

  - `  DISPLAY_NAME  ` : the display name for the transfer configuration. The data transfer name can be any value that lets you identify the transfer if you need to modify it later.

  - `  DATASET  ` : the target dataset for the transfer configuration.

  - `  PARAMETERS  ` : the parameters for the created transfer configuration in JSON format. For example: `  --params='{"param":"param_value"}'  ` . The following are the parameters for a ServiceNow data transfer:
    
    <table>
    <colgroup>
    <col style="width: 33%" />
    <col style="width: 33%" />
    <col style="width: 33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>ServiceNow parameter</th>
    <th>Required or optional</th>
    <th>Description</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><code dir="ltr" translate="no">           connector.instanceId          </code></td>
    <td>Required</td>
    <td>Instance ID of the ServiceNow instance</td>
    </tr>
    <tr class="even">
    <td><code dir="ltr" translate="no">           connector.authentication.username          </code></td>
    <td>Required</td>
    <td>Username of the credentials</td>
    </tr>
    <tr class="odd">
    <td><code dir="ltr" translate="no">           connector.authentication.password          </code></td>
    <td>Required</td>
    <td>Password of the credentials</td>
    </tr>
    <tr class="even">
    <td><code dir="ltr" translate="no">           connector.authentication.oauth.clientId          </code></td>
    <td>Required</td>
    <td>Client ID of generated OAuth</td>
    </tr>
    <tr class="odd">
    <td><code dir="ltr" translate="no">           connector.authentication.oauth.clientSecret          </code></td>
    <td>Required</td>
    <td>Client Secret of generated OAuth</td>
    </tr>
    <tr class="even">
    <td><code dir="ltr" translate="no">           connector.valueType          </code></td>
    <td>Optional</td>
    <td><code dir="ltr" translate="no">           Actual          </code> or <code dir="ltr" translate="no">           Display          </code> (default: <code dir="ltr" translate="no">           Actual          </code> )</td>
    </tr>
    <tr class="odd">
    <td><code dir="ltr" translate="no">           connector.instanceCloudType          </code></td>
    <td>Optional</td>
    <td>Specify the cloud type of your ServiceNow account. Supported values are:
    <ul>
    <li><code dir="ltr" translate="no">             COMMERCIAL_CLOUD            </code> , if your ServiceNow instance URL follows the pattern <code dir="ltr" translate="no">             https://                           INSTANCE_ID                          .service-now.com            </code></li>
    <li><code dir="ltr" translate="no">             GOVERNMENT_COMMUNITY_CLOUD            </code> if your ServiceNow instance URL follows the pattern <code dir="ltr" translate="no">             https://                           INSTANCE_ID                          .servicenowservices.com            </code></li>
    </ul></td>
    </tr>
    <tr class="even">
    <td><code dir="ltr" translate="no">           connector.networkAttachment          </code></td>
    <td>Optional</td>
    <td>Specify a network attachment to configure this data transfer to use a single, consistent IP address. You can use this option if your ServiceNow instance is secured to only accept traffic from specific IP addresses. For more information about defining IP addresses in ServiceNow, see <a href="https://www.servicenow.com/docs/csh?topicname=sc-ip-addresses-access-allowlist.html&amp;version=latest">Define allowed ServiceNow internal IP addresses</a> .</td>
    </tr>
    </tbody>
    </table>
    
    For example, the following command creates a ServiceNow data transfer in the default project with all the required parameters:
    
    ``` text
      bq mk
        --transfer_config
        --target_dataset=mydataset
        --data_source=servicenow
        --display_name='My Transfer'
        --params='{"connector.authentication.oauth.clientId": "1234567890",
            "connector.authentication.oauth.clientSecret":"ABC12345",
            "connector.authentication.username":"user1",
            "connector.authentication.password":"abcdef1234",
            "connector.instanceId":"https://dev-instance.service-now.com",
            "connector.networkAttachment": "projects/dev-project1/regions/us-central1/networkattachments/na1"}'
    ```

### API

Use the [`  projects.locations.transferConfigs.create  `](/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs/create) method and supply an instance of the [`  TransferConfig  `](/bigquery/docs/reference/datatransfer/rest/v1/projects.locations.transferConfigs#TransferConfig) resource.

When you save the transfer configuration, the ServiceNow connector automatically triggers a transfer run according to your schedule option. With every transfer run, the ServiceNow connector transfers all available data from ServiceNow into BigQuery.

To manually run a data transfer outside of your regular schedule, you can start a [backfill run](/bigquery/docs/working-with-transfers#manually_trigger_a_transfer) .

## Data type mapping

The following table shows how data types are mapped in a ServiceNow data transfer:

<table>
<thead>
<tr class="header">
<th>ServiceNow data type</th>
<th>BigQuery data type</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       decimal      </code></td>
<td><code dir="ltr" translate="no">       FLOAT64      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       integer      </code></td>
<td><code dir="ltr" translate="no">       INTEGER      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       boolean      </code></td>
<td><code dir="ltr" translate="no">       BOOLEAN      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       glide_date      </code></td>
<td><code dir="ltr" translate="no">       DATE      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       glide_date_time      </code></td>
<td><code dir="ltr" translate="no">       DATETIME      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       glide_time      </code></td>
<td><code dir="ltr" translate="no">       INT64      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       reference      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       currency      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       sys_class_name      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       domain_id      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       domain_path      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       guid      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       translated_html      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       journal      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       string      </code></td>
<td><code dir="ltr" translate="no">       STRING      </code></td>
</tr>
</tbody>
</table>

## Troubleshoot transfer issues

The following sections detail common problems when setting up a ServiceNow data transfer.

For more information, see [Troubleshoot transfer configurations](/bigquery/docs/transfer-troubleshooting) .

### Transfer fails due to ServiceNow enablement

An issue occurs causing data transfers to fail when the Procurement, Product Catalog, or Contract Management applications aren't enabled in ServiceNow. To fix it, enable all three applications:

  - [Procurement](https://www.servicenow.com/docs/csh?topicname=t_ActivateProcurement.html&version=latest)
  - [Product Catalog](https://www.servicenow.com/docs/csh?topicname=t_ActivateAProductCatalogItem.html&version=latest)
  - [Contract Management](https://www.servicenow.com/docs/csh?topicname=c_ContractManagement.html&version=latest) (enabled by default)

### Issue occurs during transfer run

An issue occurs causing the transfer run to not be created as intended. To resolve the issue, do the following:

  - Check that the ServiceNow account credentials, such as **Username** , **Password** , **Client ID** , and **Client secret** values, are valid.
  - Check that the Instance ID is the valid ID of your ServiceNow instance.

### Other errors

For information about other errors that occurred during a ServiceNow data transfer, see [ServiceNow transfer issues](/bigquery/docs/transfer-troubleshooting#servicenow-issues)

## Pricing

For pricing information about ServiceNow transfers, see [Data Transfer Service pricing](/bigquery/pricing#bqdts) .

## What's next

  - For an overview of BigQuery Data Transfer Service, see [Introduction to BigQuery Data Transfer Service](/bigquery/docs/dts-introduction) .
  - For information on using transfers including getting information about a transfer configuration, listing transfer configurations, and viewing a transfer's run history, see [Working with transfers](/bigquery/docs/working-with-transfers) .
  - Learn how to [load data with cross-cloud operations](/bigquery/docs/load-data-using-cross-cloud-transfer) .
