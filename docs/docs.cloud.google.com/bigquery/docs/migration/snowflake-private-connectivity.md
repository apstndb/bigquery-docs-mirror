---
name: documents/docs.cloud.google.com/bigquery/docs/migration/snowflake-private-connectivity
uri: https://docs.cloud.google.com/bigquery/docs/migration/snowflake-private-connectivity
title: Configure private connectivity for Snowflake transfers
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# Configure private connectivity for Snowflake transfers

This guide shows you how to configure private connectivity to create private data transfers from Snowflake to BigQuery. Private data transfers let you transfer data from one source to another all within a private network, and let you lower security risks when transferring data over the public internet.

The following sections show you the required steps to configure private connectivity before you can [create a Snowflake transfer](https://docs.cloud.google.com/bigquery/docs/migration/snowflake-transfer) .

Private transfers are supported for Snowflake instances that are hosted on Amazon Web Services (AWS), Microsoft Azure, and Google Cloud.

![Private Data transfers from AWS or Azure or Google Cloud-hosted Snowflake accounts to BigQuery](https://docs.cloud.google.com/static/bigquery/images/snowflake-private-overview.png)

## Create a private link to Snowflake

Create a private link that connects your Snowflake account to your cloud provider. For more information, select one of the following options:

### AWS

[Configure AWS PrivateLink](https://docs.snowflake.com/en/user-guide/admin-security-privatelink) to connect your Snowflake account to your AWS account. Your AWS account must contain the [Amazon S3 staging bucket required for a Snowflake transfer](https://docs.cloud.google.com/bigquery/docs/migration/snowflake-private-connectivity#aws_3) .

### Azure

[Configure Azure Private Link](https://docs.snowflake.com/en/user-guide/privatelink-azure) to connect your Azure Virtual Network (VNet) to the Snowflake VNet in Azure. Your Azure account must contain the [Blob staging bucket required for a Snowflake transfer](https://docs.cloud.google.com/bigquery/docs/migration/snowflake-private-connectivity#azure_3) .

### Google Cloud

[Configure Google Cloud Private Service Connect to connect your Virtual Private Cloud (VPC) network subnet](https://docs.snowflake.com/en/user-guide/private-service-connect-google) to your Snowflake account hosted on Google Cloud. Your Google Cloud must have a [Cloud Storage staging bucket required for a Snowflake transfer](https://docs.cloud.google.com/bigquery/docs/migration/snowflake-private-connectivity#dynamic_data.site_values.cloud_name_short_1) .

## Set up Cross-Cloud Interconnect or HA VPN

Set up either Cross-Cloud Interconnect or HA VPN from AWS or Azure. This step is not required for Google Cloud-hosted Snowflake accounts.

### AWS

A high availability VPN lets you transfer data through an encrypted VPN tunnel. To use an HA VPN for your private Snowflake transfer, see [Create HA VPN connections between Google Cloud and AWS](https://docs.cloud.google.com/network-connectivity/docs/vpn/tutorials/create-ha-vpn-connections-google-cloud-aws) .

A [Cross-Cloud Interconnect](https://docs.cloud.google.com/network-connectivity/docs/interconnect/concepts/cci-overview) connection creates a dedicated private link between cloud providers and is suitable for large data transfers with low-latency requirements. To use Cross-Cloud Interconnect for your private Snowflake transfer, see [Connect to AWS](https://docs.cloud.google.com/network-connectivity/docs/interconnect/how-to/cci/aws/connectivity-overview) .

### Azure

A high availability VPN lets you transfer data through an encrypted VPN tunnel. To use an HA VPN for your private Snowflake transfer, see [Create HA VPN connections between Google Cloud and Azure](https://docs.cloud.google.com/network-connectivity/docs/vpn/tutorials/create-ha-vpn-connections-google-cloud-azure) .

A [Cross-Cloud Interconnect](https://docs.cloud.google.com/network-connectivity/docs/interconnect/concepts/cci-overview) connection creates a dedicated private link between cloud providers and is suitable for large data transfers with low-latency requirements. To use Cross-Cloud Interconnect for your private Snowflake transfer, see [Connect to Azure](https://docs.cloud.google.com/network-connectivity/docs/interconnect/how-to/cci/azure/connectivity-overview) .

## Create proxy VM

To complete a private connection, a proxy VM is required to complete the connection between your data sources without your data reaching the public internet. This step is required for Snowflake instances hosted on AWS, Azure, or Google Cloud.

To create and configure a proxy VM for a Snowflake private transfer, do the following:

1.  [Create one or more Compute Engine VM instances](https://docs.cloud.google.com/compute/docs/instances/create-start-instance#create-instance-methods) within the consumer VPC network.
2.  Download a TCP proxy software, such as HAProxy or Nginx, and configure the following:
    1.  Specify a port. For example, `443` .
    2.  Forward all incoming TCP traffic to the private hostname and port on the Snowflake instance.
3.  Configure the VMs to resolve the Snowflake private hostname through the DNS configured in the consumer VPC network.
4.  Set up an internal passthrough load balancer by doing the following:
    1.  [Group the proxy VMs into a managed instance groups (MIG)](https://docs.cloud.google.com/compute/docs/instance-groups/creating-groups-of-managed-instances) .
    2.  [Set up an internal passthrough Network Load Balancer with VM instance group backends](https://docs.cloud.google.com/load-balancing/docs/internal/setting-up-internal) .

## Create service attachment

[Use Private Service Connect to create a network attachment and publish the service](https://docs.cloud.google.com/vpc/docs/configure-private-service-connect-producer#publish-service) . This step is required for Snowflake instances hosted on AWS, Azure, or Google Cloud.

Your service attachment must be in the same region as your BigQuery dataset.

If your service uses explicit approval ( `connection-preference` is set as `ACCEPT_MANUAL` ), then the service account used in your Snowflake private data transfer must have the following IAM permissions:

  - `compute.serviceAttachments.get`
  - `compute.serviceAttachments.update`
  - `compute.regionOperations.get`

Once you have created the service attachment, note the service attachment URI. You'll need this URI when you create your Snowflake transfer configuration.

## Create endpoint

Create an endpoint in your AWS or Azure account. This step is not required for Google Cloud-hosted Snowflake accounts.

### AWS

In AWS, create a VPC endpoint that connects to Amazon S3. For more information, see [Access an AWS service using an interface VPC endpoint](https://docs.aws.amazon.com/vpc/latest/privatelink/create-interface-endpoint.html) .

### Azure

Configure a Private Endpoint on the Storage Account in Azure. For more information, see [Use private endpoints for Azure Storage](https://learn.microsoft.com/en-us/azure/storage/common/storage-private-endpoints) .

Storage Transfer Service requires the `*.blob.core.windows.net` endpoint. The `*.dfs.core.windows.net` endpoint isn't supported.

Once created, note the endpoint's IP address. You'll need to specify the IP address when creating your load balancer in the following section.

## Create a network load balancer

In Google Cloud, set up a regional internal proxy Network Load Balancer with hybrid connectivity. This provides an internal IP address that's restricted to clients running in the same VPC network as the load balancer, and that routes traffic to the S3 VPC endpoints or Azure Storage private endpoints that you created in the previous section.

You should create the load balancer in the same project and VPC network as the VLAN attachment which interfaces with the Cloud Interconnect. While the interconnect itself can be in a different project within the same organization, the attachment must be in the same VPC and region as the load balancer.

  - [Set up a regional internal proxy Network Load Balancer with hybrid connectivity](https://docs.cloud.google.com/load-balancing/docs/tcp/set-up-int-tcp-proxy-hybrid#setup-google-environment)

Specify the S3 VPC endpoint or Azure Storage private endpoint IP address when you reach the steps labeled **Add endpoints to the hybrid connectivity NEG** .

Note the NLB's frontend IP address and port, as you'll need to specify them in the next section.

### Validate the connection

Before proceeding, we recommend that you validate that the load balancer can connect to the remote storage endpoint.

To do so:

1.  Create a Compute Engine VM in the same VPC network as your load balancer.

2.  From the VM, use `curl` to test connectivity to the load balancer's IP address and port:
    
        curl -v --resolve HOSTNAME:PORT:LOAD_BALANCER_IP https://HOSTNAME
    
    Replace the following:
    
      - HOSTNAME is the hostname of your source storage provider.
          - For AWS S3, use the S3 API endpoint for your bucket's region, for example `s3.us-west-1.amazonaws.com` .
          - For Azure Storage, use your storage account's blob endpoint, for example `mystorageaccount.blob.core.windows.net` .
      - PORT is the port you configured on the load balancer's forwarding rule, typically `443` .
      - LOAD\_BALANCER\_IP is the frontend IP address of your load balancer.

A response from the remote endpoint, even an error, indicates that connectivity is successful. A connection timeout indicates a misconfiguration in your network setup that you should resolve before continuing.

## Register your NLB

Register the NLB in Service Directory. BigQuery uses Service Directory to resolve the address of the load balancer and connect to it directly.

Follow the instructions to [register an internal load balancer](https://docs.cloud.google.com/service-directory/docs/configuring-ilb-in-sd) . Use the IP address and port of the load balancer that you created when specifying the forwarding rule.

Once created, note the self-link of the service. It uses the format `projects/{project_id}/locations/{location}/namespaces/{namespace}/services/{service}` . You'll need this value when creating the transfer job.

## Prepare staging bucket

To complete a Snowflake data transfer, you must create a staging bucket and then configure it to allow write access from Snowflake.

Select one of the following options:

### AWS

For AWS-hosted Snowflake accounts, create an Amazon S3 bucket to stage the Snowflake data before it is loaded into BigQuery.

1.  [Create an Amazon S3 bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/create-bucket-overview.html) .

2.  [Create and configure a Snowflake storage integration object](https://docs.snowflake.com/en/user-guide/data-load-s3-config-storage-integration) to allow Snowflake to write data into the Amazon S3 bucket as an external stage.

To allow read access on your Amazon S3 bucket, you must also do the following:

1.  Create a dedicated [Amazon IAM user](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users.html) and grant it the [`AmazonS3ReadOnlyAccess`](https://docs.aws.amazon.com/aws-managed-policy/latest/reference/AmazonS3ReadOnlyAccess.html) policy.

2.  [Create an Amazon access key pair](https://docs.aws.amazon.com/keyspaces/latest/devguide/create.keypair.html) for the IAM user.

### Azure

For Azure-hosted Snowflake accounts, create a Azure Blob Storage container to stage the Snowflake data before it is loaded into BigQuery.

1.  [Create an Azure storage account](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-create) and a [storage container](https://learn.microsoft.com/en-us/azure/storage/blobs/blob-containers-portal#create-a-container) within it.
2.  <span id="storage-azure-integration-container">[Create and configure a Snowflake storage integration object](https://docs.snowflake.com/en/user-guide/data-load-azure-config#option-1-configuring-a-snowflake-storage-integration) to allow Snowflake to write data into the Azure storage container as an external stage. You can skip the steps to create an external stage, as this is not required.</span>

To allow read access on your Azure container, [generate a SAS Token](https://learn.microsoft.com/en-us/azure/ai-services/translator/document-translation/how-to-guides/create-sas-tokens?tabs=Containers#create-sas-tokens-in-the-azure-portal) for it.

### Google Cloud

For Google Cloud-hosted Snowflake accounts, create a Cloud Storage bucket to stage the Snowflake data before it is loaded into BigQuery.

1.  [Create a Cloud Storage bucket](https://docs.cloud.google.com/storage/docs/creating-buckets) .

2.  <span id="storage-gcs-integration-bucket">[Create and configure a Snowflake storage integration object](https://docs.snowflake.com/en/user-guide/data-load-gcs-config) to allow Snowflake to write data into the Cloud Storage bucket as an external stage.</span>

3.  To allow access to staging bucket, Grant [DTS service agent](https://docs.cloud.google.com/bigquery/docs/enable-transfer-service#service_agent) the `roles/storage.objectViewer` role with the following command:
    
        gcloud storage buckets add-iam-policy-binding gs://STAGING_BUCKET_NAME \
          --member=serviceAccount:service-PROJECT_NUMBER@gcp-sa-bigquerydatatransfer.iam.gserviceaccount.com \
          --role=roles/storage.objectViewer

## Create a private Snowflake transfer configuration

[Create the Snowflake transfer](https://docs.cloud.google.com/bigquery/docs/migration/snowflake-transfer) . When you set up the transfer configuration, do the following:

### Console

  - For **Use Private Network** , select **True** .

  - For **PSC Service Attachment** , enter the service attachment URI. For information about finding the service attachment URI, see [View details for a published service](https://docs.cloud.google.com/vpc/docs/configure-private-service-connect-producer#attachment-details) . The service attachment URI is in the format ` projects/ PROJECT_ID /regions/ REGION /serviceAttachments/ SERVICE_ATTACHMENT  ` .

  - For **Private Network Service** , enter [the self-link of the NLB service](https://docs.cloud.google.com/storage-transfer/docs/create-transfers/agentless/customer-managed-private-network#register-your-nlb-with-service-directory) . It uses the format ` projects/ PROJECT_ID /locations/ LOCATION /namespaces/ NAMESPACE /services/ SERVICE_NAME  ` .

  - The URI of the staging bucket that you want to use for the transfer:
    
      - For an AWS-hosted Snowflake account, an [Amazon S3 bucket URI](https://docs.cloud.google.com/bigquery/docs/migration/snowflake-private-connectivity#aws_3) is required along with access credentials.
      - For an Azure-hosted Snowflake, an [Azure Blob Storage account and container](https://docs.cloud.google.com/bigquery/docs/migration/snowflake-private-connectivity#azure_3) is required.
      - For a Google Cloud-hosted Snowflake account, a [Cloud Storage bucket URI](https://docs.cloud.google.com/bigquery/docs/migration/snowflake-private-connectivity#dynamic_data.site_values.cloud_name_short_1) is required.

  - For **Cloud Provider** , select `AWS` or `AZURE` or `GCP` depending on which cloud provider is hosting your Snowflake account.
    
    ### AWS
    
      - For **Amazon S3 URI** , enter the [URI of the Amazon S3 bucket](https://docs.cloud.google.com/bigquery/docs/migration/snowflake-private-connectivity#aws_3) to use as a staging bucket.
      - For **Access key ID** and **Secret access key** , enter the [access key pair](https://docs.cloud.google.com/bigquery/docs/migration/snowflake-private-connectivity#snowflake_key_pair) .
    
    ### Azure
    
      - For **Azure storage account name** and **The container in the Azure storage account** , enter the [storage account and container name of the Azure Blob Storage](https://docs.cloud.google.com/bigquery/docs/migration/snowflake-private-connectivity#azure_3) to use as a staging bucket.
      - For **SAS Token** , enter the [SAS token generated for the container](https://docs.cloud.google.com/bigquery/docs/migration/snowflake-private-connectivity#azure_sas_token) .
    
    ### Google Cloud
    
      - For **GCS URI** , enter the [URI of the Cloud Storage](https://docs.cloud.google.com/bigquery/docs/migration/snowflake-private-connectivity#dynamic_data.site_values.cloud_name_short_1) to use as a staging bucket.

### bq

  - For the `use_private_network` parameter, set to `TRUE` .
  - For the `service_attachment` parameter, specify the service attachment URI. For information about finding the service attachment URI, see [View details for a published service](https://docs.cloud.google.com/vpc/docs/configure-private-service-connect-producer#attachment-details) . The service attachment URI is in the format ` projects/ PROJECT_ID /regions/ REGION /serviceAttachments/ SERVICE_ATTACHMENT  ` .
  - For the `private_network_service` parameter, provide the [the self-link of the NLB service](https://docs.cloud.google.com/storage-transfer/docs/create-transfers/agentless/customer-managed-private-network#register-your-nlb-with-service-directory) . It uses the format ` projects/ PROJECT_ID /locations/ LOCATION /namespaces/ NAMESPACE /services/ SERVICE_NAME  ` .
  - `cloud_provider` : enter `AWS` or `AZURE` or `GCP` depending on which cloud provider is hosting your Snowflake account.
  - `staging_s3_uri` : enter the [URI of the S3 bucket](https://docs.cloud.google.com/bigquery/docs/migration/snowflake-private-connectivity#aws_3) to use as a staging bucket. Only required when your `cloud_provider` is `AWS` .
  - `aws_access_key_id` : enter the [access key pair](https://docs.cloud.google.com/bigquery/docs/migration/snowflake-private-connectivity#snowflake_key_pair) . Only required when your `cloud_provider` is `AWS` .
  - `aws_secret_access_key` : enter the [access key pair](https://docs.cloud.google.com/bigquery/docs/migration/snowflake-private-connectivity#snowflake_key_pair) . Only required when your `cloud_provider` is `AWS` .
  - `azure_storage_account` : enter the [storage account name](https://docs.cloud.google.com/bigquery/docs/migration/snowflake-private-connectivity#azure_3) to use as a staging bucket. Only required when your `cloud_provider` is `AZURE` .
  - `staging_azure_container` : enter the [container within Azure Blob Storage](https://docs.cloud.google.com/bigquery/docs/migration/snowflake-private-connectivity#azure_3) to use as a staging bucket. Only required when your `cloud_provider` is `AZURE` .
  - `azure_sas_token` : enter the [SAS token](https://docs.cloud.google.com/bigquery/docs/migration/snowflake-private-connectivity#azure_sas_token) . Only required when your `cloud_provider` is `AZURE` .
  - `staging_gcs_uri` : enter the [URI of the Cloud Storage](https://docs.cloud.google.com/bigquery/docs/migration/snowflake-private-connectivity#dynamic_data.site_values.cloud_name_short_1) to use as a staging bucket. Only required when your `cloud_provider` is `GCP` .
