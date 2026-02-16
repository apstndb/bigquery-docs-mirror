# Connect to Amazon S3

As a BigQuery administrator, you can create a [connection](/bigquery/docs/connections-api-intro) to let data analysts access data stored in Amazon Simple Storage Service (Amazon S3) buckets.

[BigQuery Omni](/bigquery/docs/omni-introduction) accesses Amazon S3 data through connections. Each connection has its unique Amazon Web Services (AWS) Identity and Access Management (IAM) user. You grant permissions to users through AWS IAM roles. The policies within the AWS IAM roles determine what data BigQuery can access for each connection.

Connections are required to [query the Amazon S3 data](/bigquery/docs/omni-aws-create-external-table) and [export query results from BigQuery to your Amazon S3 bucket](/bigquery/docs/omni-aws-export-results-to-s3) .

## Before you begin

Ensure that you've created the following resources:

  - A [Google Cloud project](/docs/overview#projects) with [BigQuery Connection API](https://console.cloud.google.com/apis/library/bigqueryconnection.googleapis.com) enabled.
  - If you are on the capacity-based pricing model, then ensure that you have enabled [BigQuery Reservation API](https://console.cloud.google.com/apis/library/bigqueryreservation.googleapis.com) for your project. For information about pricing, see [BigQuery Omni pricing](https://cloud.google.com/bigquery/pricing#bqomni) .
  - An [AWS account](https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/) with permissions to modify IAM policies in AWS.

## Required roles

To get the permissions that you need to create a connection to access Amazon S3 data, ask your administrator to grant you the [BigQuery Connection Admin](/iam/docs/roles-permissions/bigquery#bigquery.connectionAdmin) ( `  roles/bigquery.connectionAdmin  ` ) IAM role on the project. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

## Create an AWS IAM policy for BigQuery

Ensure that you follow [security best practices for Amazon S3](https://docs.aws.amazon.com/AmazonS3/latest/dev/security-best-practices.html) . We recommend that you do the following:

  - Set up an AWS policy that prevents access to your Amazon S3 bucket through HTTP.
  - Set up an AWS policy that prevents public access to your Amazon S3 bucket.
  - Use Amazon S3 server-side encryption.
  - Limit permissions granted to the Google Account to the required minimum.
  - Set up CloudTrails and enable Amazon S3 data events.

To create an AWS IAM policy, use the AWS console or Terraform:

### AWS console

1.  Go to the AWS IAM console. Ensure that you're in the account that owns the Amazon S3 bucket that you want to access.

2.  Select **Policies \> Create policy** (opens in a new tab).

3.  Click **JSON** and paste the following into the editor:
    
    ``` text
    {
     "Version": "2012-10-17",
     "Statement": [
        {
         "Effect": "Allow",
         "Action": [
           "s3:ListBucket"
         ],
         "Resource": [
           "arn:aws:s3:::BUCKET_NAME"
          ]
        },
       {
         "Effect": "Allow",
         "Action": [
           "s3:GetObject",
           EXPORT_PERM
         ],
         "Resource": [
           "arn:aws:s3:::BUCKET_NAME",
            "arn:aws:s3:::BUCKET_NAME/*"
          ]
        }
     ]
    }
    ```
    
    Replace the following:
    
      - `  BUCKET_NAME  ` : the Amazon S3 bucket that you want BigQuery to access.
      - `  EXPORT_PERM  ` (optional): additional permission if you want to [export data to an Amazon S3 bucket](/bigquery/docs/omni-aws-export-results-to-s3) . Replace with `  "s3:PutObject"  `
          - To separate export access control, we recommend that you create another connection with a separate AWS IAM role and grant the role write-only access. For more granular access control, you can also limit a role's access to a specific path of the bucket.
    
    **Note:** If you get an error after pasting the JSON into the editor, format the JSON text using a JSON editor.

4.  In the **Name** field, enter a policy name, such as `  bq_omni_read_only  ` .

5.  Click **Create policy** .

Your policy is created with an Amazon Resource Name (ARN) in the following format:

``` text
arn:aws:iam::AWS_ACCOUNT_ID:policy/POLICY_NAME
```

Replace the following:

  - `  AWS_ACCOUNT_ID  ` : the ID number of the connection's AWS IAM user.
  - `  POLICY_NAME  ` : the policy name you chose.

### AWS CLI

To create an AWS IAM policy, use the [`  aws iam create-policy  ` command](https://docs.aws.amazon.com/cli/latest/reference/iam/create-policy.html) :

``` text
  aws iam create-policy \
   --policy-name POLICY_NAME \
   --policy-document '{
     "Version": "2012-10-17",
     "Statement": [
        {
         "Effect": "Allow",
         "Action": [
           "s3:ListBucket"
         ],
         "Resource": [
           "arn:aws:s3:::BUCKET_NAME"
          ]
        },
       {
         "Effect": "Allow",
         "Action": [
           "s3:GetObject",
           EXPORT_PERM
         ],
         "Resource": [
           "arn:aws:s3:::BUCKET_NAME",
            "arn:aws:s3:::BUCKET_NAME/*"
          ]
        }
     ]
    }'
```

Replace the following:

  - `  POLICY_NAME  ` : the name of the policy you are creating.
  - `  BUCKET_NAME  ` : the Amazon S3 bucket that you want BigQuery to access.
  - `  EXPORT_PERM  ` (optional): additional permission if you want to [export data to an Amazon S3 bucket](/bigquery/docs/omni-aws-export-results-to-s3) . Replace with `  "s3:PutObject"  `
      - To separate export access control, we recommend that you create another connection with a separate AWS IAM role and grant the role write-only access. For more granular access control, you can also limit a role's access to a specific path of the bucket.

Your policy is created with an Amazon Resource Name (ARN) in the following format:

``` text
arn:aws:iam::AWS_ACCOUNT_ID:policy/POLICY_NAME
```

Replace the following:

  - `  AWS_ACCOUNT_ID  ` : the ID number of the connection's AWS IAM user.
  - `  POLICY_NAME  ` : the policy name you chose.

### Terraform

Add the following to your Terraform config to attach a policy to an Amazon S3 bucket resource:

``` text
  resource "aws_iam_policy" "bigquery-omni-connection-policy" {
    name = "bigquery-omni-connection-policy"

    policy = <<-EOF
            {
              "Version": "2012-10-17",
              "Statement": [
                  {
                      "Sid": "BucketLevelAccess",
                      "Effect": "Allow",
                      "Action": ["s3:ListBucket"],
                      "Resource": ["arn:aws:s3:::BUCKET_NAME"]
                  },
                  {
                      "Sid": "ObjectLevelAccess",
                      "Effect": "Allow",
                      "Action": ["s3:GetObject",EXPORT_PERM],
                      "Resource": [
                          "arn:aws:s3:::BUCKET_NAME",
                          "arn:aws:s3:::BUCKET_NAME/*"
                          ]
                  }
              ]
            }
            EOF
  }
```

Replace the following:

  - `  BUCKET_NAME  ` : the Amazon S3 bucket that you want BigQuery to access.
  - `  EXPORT_PERM  ` (optional): additional permission if you want to [export data to an Amazon S3 bucket](/bigquery/docs/omni-aws-export-results-to-s3) . Replace with `  "s3:PutObject"  `
      - To separate export access control, we recommend that you create another connection with a separate AWS IAM role and grant the role write-only access. For more granular access control, you can also limit a role's access to a specific path of the bucket.

## Create an AWS IAM role for BigQuery

Next, create a role that allows access to the Amazon S3 bucket from within BigQuery. This role uses the policy that you created in the previous section.

To create an AWS IAM role, use the AWS console or Terraform:

### AWS console

1.  Go to the AWS IAM console. Ensure that you're in the account that owns the Amazon S3 bucket that you want to access.

2.  Select **Roles \> Create role** .

3.  For **Select type of trusted entity** , select **Web Identity** .

4.  For **Identity Provider** , select **Google** .

5.  For **Audience** , enter `  00000  ` as a placeholder value. You'll replace the value later.

6.  Click **Next: Permissions** .

7.  To grant the role access to your Amazon S3 data, attach an IAM policy to the role. Search for the policy that you created in the previous section, and click the toggle.

8.  Click **Next: Tags** .

9.  Click **Next: Review** . Enter a name for the role, such as `  BQ_Read_Only  ` .

10. Click **Create role** .

### AWS CLI

Use the following command to create an IAM role and assign the policy to the role created:

``` text
  aws iam create-role \
   --role-name bigquery-omni-connection \
   --max-session-duration 43200 \
   --assume-role-policy-document '{
     "Version": "2012-10-17",
     "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "Federated": "accounts.google.com"
            },
            "Action": "sts:AssumeRoleWithWebIdentity",
            "Condition": {
                "StringEquals": {
                    "accounts.google.com:sub": "00000"
                }
            }
        }
    ]
}'
```

### Terraform

Add the following to your Terraform config to create an IAM role and assign the policy to the role created:

``` text
  resource "aws_iam_role" "bigquery-omni-connection-role" {
    name                 = "bigquery-omni-connection"
    max_session_duration = 43200

    assume_role_policy = <<-EOF
    {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Effect": "Allow",
          "Principal": {
            "Federated": "accounts.google.com"
          },
          "Action": "sts:AssumeRoleWithWebIdentity",
          "Condition": {
            "StringEquals": {
              "accounts.google.com:sub": "00000"
            }
          }
        }
      ]
    }
    EOF
  }

  resource "aws_iam_role_policy_attachment" "bigquery-omni-connection-role-attach" {
    role       = aws_iam_role.bigquery-omni-connection-role.name
    policy_arn = aws_iam_policy.bigquery-omni-connection-policy.arn
  }

  output "bigquery_omni_role" {
    value = aws_iam_role.bigquery-omni-connection-role.arn
  }
```

Then, attach the policy to the role:

``` text
  aws iam attach-role-policy \
    --role-name bigquery-omni-connection \
    --policy-arn arn:aws:iam::AWS_ACCOUNT_ID:policy/POLICY_NAME
```

Replace the following:

  - `  AWS_ACCOUNT_ID  ` : the ID number of the connection's AWS IAM user.
  - `  POLICY_NAME  ` : the policy name you chose.

## Create connections

To connect to your Amazon S3 bucket, use the Google Cloud console, the bq command-line tool, or the client library:

### Console

**Key Point:** Create your connection in the Google Cloud project that contains the Amazon S3 instance that you want to query.

1.  Go to the **BigQuery** page.

2.  In the **Explorer** pane, click add **Add data** .
    
    The **Add data** dialog opens.

3.  In the **Filter By** pane, in the **Data Source Type** section, select **Storage/Data Lakes** .
    
    Alternatively, in the **Search for data sources** field, you can enter `  aws  ` or `  Amazon S3  ` .

4.  In the **Featured data sources** section, click **Amazon S3** .

5.  Click the **Amazon S3 Omni: BigQuery Federation** solution card.

6.  In the **Create table** dialog, in the **Connection ID** field, select **Create a new S3 connection** .

7.  In the **External data source** pane, enter the following information:
    
      - For **Connection type** , select **BigLake on AWS (via BigQuery Omni)** .
    
      - For **Connection ID** , enter an identifier for the connection resource. You can use letters, numbers, dashes, and underscores.
    
      - For **Region** , select the location where you want to create the connection.
    
      - Optional: For **Friendly name** , enter a user-friendly name for the connection, such as `  My connection resource  ` . The friendly name can be any value that helps you identify the connection resource if you need to modify it later.
    
      - Optional: For **Description** , enter a description for this connection resource.
    
      - For **AWS role id** , enter the full IAM role ID that you created in this format:
        
        ``` text
        arn:aws:iam::AWS_ACCOUNT_ID:role/ROLE_NAME
        ```

8.  Click **Create connection** .

9.  Click **Go to connection** .

10. In the **Connection info** pane, copy the **BigQuery Google identity** . This is a Google principal that is specific to each connection. Example:
    
    ``` text
      BigQuery Google identity: IDENTITY_ID
      
    ```

### Terraform

``` text
  resource "google_bigquery_connection" "connection" {
    connection_id = "bigquery-omni-aws-connection"
    friendly_name = "bigquery-omni-aws-connection"
    description   = "Created by Terraform"

    location      = "AWS_LOCATION"
    aws {
      access_role {
        # This must be constructed as a string instead of referencing the
        # AWS resources directly to avoid a resource dependency cycle
        # in Terraform.
        iam_role_id = "arn:aws:iam::AWS_ACCOUNT:role/IAM_ROLE_NAME"
      }
    }
  }
```

Replace the following:

  - `  AWS_LOCATION  ` : an [Amazon S3 location](/bigquery/docs/omni-introduction#locations) in Google Cloud
  - `  AWS_ACCOUNT  ` : your AWS account ID.
  - `  IAM_ROLE_NAME  ` : the role that allows access to the Amazon S3 bucket from BigQuery. Use the value of the `  name  ` argument from the `  aws_iam_role  ` resource in [Create an AWS IAM role for BigQuery](#creating-aws-iam-role) .

### bq

``` text
bq mk --connection --connection_type='AWS' \
--iam_role_id=arn:aws:iam::AWS_ACCOUNT_ID:role/ROLE_NAME \
--location=AWS_LOCATION \
CONNECTION_ID
```

Replace the following:

  - `  AWS_ACCOUNT_ID  ` : the ID number of the connection's AWS IAM user
  - `  ROLE_NAME  ` : the role policy name you chose
  - `  AWS_LOCATION  ` : an [Amazon S3 location](/bigquery/docs/omni-introduction#locations) in Google Cloud
  - `  CONNECTION_ID  ` : the ID that you give this connection resource.

The command line shows the following output:

``` text
  Identity: IDENTITY_ID
```

The output contains the following:

  - `  IDENTITY_ID  ` : a Google principal that Google Cloud controls that is specific to each connection.

Take note of the `  IDENTITY_ID  ` value.

**Note:** To override the default project, use the `  --project_id= PROJECT_ID  ` parameter. Replace `  PROJECT_ID  ` with the ID of your Google Cloud project.

### Java

Before trying this sample, follow the Java setup instructions in the [BigQuery quickstart using client libraries](/bigquery/docs/quickstarts/quickstart-client-libraries) . For more information, see the [BigQuery Java API reference documentation](/java/docs/reference/google-cloud-bigquery/latest/overview) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](/bigquery/docs/authentication#client-libs) .

``` java
import com.google.cloud.bigquery.connection.v1.AwsAccessRole;
import com.google.cloud.bigquery.connection.v1.AwsProperties;
import com.google.cloud.bigquery.connection.v1.Connection;
import com.google.cloud.bigquery.connection.v1.CreateConnectionRequest;
import com.google.cloud.bigquery.connection.v1.LocationName;
import com.google.cloud.bigqueryconnection.v1.ConnectionServiceClient;
import java.io.IOException;

// Sample to create aws connection
public class CreateAwsConnection {

  public static void main(String[] args) throws IOException {
    // TODO(developer): Replace these variables before running the sample.
    String projectId = "MY_PROJECT_ID";
    // Example of location: aws-us-east-1
    String location = "MY_LOCATION";
    String connectionId = "MY_CONNECTION_ID";
    // Example of role id: arn:aws:iam::accountId:role/myrole
    String iamRoleId = "MY_AWS_ROLE_ID";
    AwsAccessRole role = AwsAccessRole.newBuilder().setIamRoleId(iamRoleId).build();
    AwsProperties awsProperties = AwsProperties.newBuilder().setAccessRole(role).build();
    Connection connection = Connection.newBuilder().setAws(awsProperties).build();
    createAwsConnection(projectId, location, connectionId, connection);
  }

  static void createAwsConnection(
      String projectId, String location, String connectionId, Connection connection)
      throws IOException {
    try (ConnectionServiceClient client = ConnectionServiceClient.create()) {
      LocationName parent = LocationName.of(projectId, location);
      CreateConnectionRequest request =
          CreateConnectionRequest.newBuilder()
              .setParent(parent.toString())
              .setConnection(connection)
              .setConnectionId(connectionId)
              .build();
      Connection response = client.createConnection(request);
      AwsAccessRole role = response.getAws().getAccessRole();
      System.out.println(
          "Aws connection created successfully : Aws userId :"
              + role.getIamRoleId()
              + " Aws externalId :"
              + role.getIdentity());
    }
  }
}
```

## Add a trust relationship to the AWS role

BigQuery Omni provides two methods for securely accessing data from Amazon S3. You can either grant the Google Cloud service account access to your AWS role, or if your AWS account has a [custom identity provider](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers_create_oidc.html) for `  accounts.google.com  ` , then you must add the Google Cloud service account as an audience to the provider:

  - [Add the trust policy to the AWS role](#add-trust-policy) .
  - [Configure a custom AWS identity provider](#configuring-custom-idp) .

### Add a trust policy to the AWS role

The trust relationship lets the connection assume the role and access the Amazon S3 data as specified in the roles policy.

To add a trust relationship, use the AWS console or Terraform:

### AWS console

1.  Go to the AWS IAM console. Ensure that you're in the account that owns the Amazon S3 bucket that you want to access.

2.  Select **Roles** .

3.  Select the `  ROLE_NAME  ` that you created.

4.  Click **Edit** and then do the following:
    
    1.  Set **Maximum session duration** to **12 hours** . As each query can run for up to six hours, this duration allows for one additional retry. Increasing the session duration beyond 12 hours won't allow for additional retries. For more information, see the [query/multi-statement query execution-time limit](/bigquery/quotas#query_script_execution_time_limit) .
    
    2.  Click **Save changes** .

5.  Select **Trust Relationships** and click **Edit trust relationship** . Replace the policy content with the following:
    
    ``` text
    {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Effect": "Allow",
          "Principal": {
            "Federated": "accounts.google.com"
          },
          "Action": "sts:AssumeRoleWithWebIdentity",
          "Condition": {
            "StringEquals": {
              "accounts.google.com:sub": "IDENTITY_ID"
            }
          }
        }
      ]
    }
    ```
    
    Replace `  IDENTITY_ID  ` with the **BigQuery Google identity** value, which you can find on the Google Cloud console for the [connection you created](#creating-aws-connection) .

6.  Click **Update Trust Policy** .

### AWS CLI

To create a trust relationship with the BigQuery connection, use the [`  aws iam update-assume-role-policy  ` command](https://docs.aws.amazon.com/cli/latest/reference/iam/update-assume-role-policy.html) :

``` text
  aws iam update-assume-role-policy \
    --role-name bigquery-omni-connection \
    --policy-document '{
      "Version": "2012-10-17",
      "Statement": [
        {
          "Effect": "Allow",
          "Principal": {
            "Federated": "accounts.google.com"
          },
          "Action": "sts:AssumeRoleWithWebIdentity",
          "Condition": {
            "StringEquals": {
              "accounts.google.com:sub": "IDENTITY_ID"
            }
          }
        }
      ]
    }'
  aws iam update-assume-role-policy \
    --role-name bigquery-omni-connection \
    --policy-document '{
      "Version": "2012-10-17",
      "Statement": [
        {
          "Effect": "Allow",
          "Principal": {
            "Federated": "accounts.google.com"
          },
          "Action": "sts:AssumeRoleWithWebIdentity",
          "Condition": {
            "StringEquals": {
              "accounts.google.com:sub": "IDENTITY_ID"
            }
          }
        }
      ]
    }'
```

Replace the following:

  - `  IDENTITY_ID  ` : the **BigQuery Google identity** value, which you can find on the Google Cloud console for the [connection you created](#creating-aws-connection) .

### Terraform

Update the `  aws_iam_role  ` resource in the Terraform configuration to add a trust relationship:

``` text
    resource "aws_iam_role" "bigquery-omni-connection-role" {
      name                 = "bigquery-omni-connection"
      max_session_duration = 43200

      assume_role_policy = <<-EOF
          {
            "Version": "2012-10-17",
            "Statement": [
              {
                "Effect": "Allow",
                "Principal": {
                  "Federated": "accounts.google.com"
                },
                "Action": "sts:AssumeRoleWithWebIdentity",
                "Condition": {
                  "StringEquals": {
                    "accounts.google.com:sub": "${google_bigquery_connection.connection.aws[0].access_role[0].identity}"
                  }
                }
              }
            ]
          }
          EOF
    }
```

**Note:** There may be a propagation delay for role assignment in AWS. If you receive an error of this type when using a new connection, waiting and trying again later may resolve the issue.

The connection is now ready to use.

### Configure a custom AWS identity provider

If your AWS account has a [custom identity provider](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers_create_oidc.html) for `  accounts.google.com  ` , you will need to add the IDENTITY\_ID as an audience to the provider. You can accomplish this by:

1.  Go to the AWS IAM console. Ensure that you're in the account that owns the Amazon S3 bucket that you want to access.

2.  Navigate to the **IAM** \> **Identity Providers** .

3.  Select the identity provider for *accounts.google.com* .

4.  Click **Add Audience** and add the IDENTITY\_ID as the audience.

The connection is now ready to use.

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
  - Learn about [BigQuery Omni](/bigquery/docs/omni-introduction) .
  - Use the [BigQuery Omni with AWS lab](https://www.cloudskillsboost.google/catalog_lab/5345) .
  - Learn about [BigLake tables](/bigquery/docs/biglake-intro) .
  - Learn how to [query Amazon S3 data](/bigquery/docs/omni-aws-create-external-table) .
  - Learn how to [export query results to an Amazon S3 bucket](/bigquery/docs/omni-aws-export-results-to-s3) .
