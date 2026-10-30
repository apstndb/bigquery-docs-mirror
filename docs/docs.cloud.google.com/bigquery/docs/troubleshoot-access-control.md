---
name: documents/docs.cloud.google.com/bigquery/docs/troubleshoot-access-control
uri: https://docs.cloud.google.com/bigquery/docs/troubleshoot-access-control
title: Troubleshoot access control issues
description: How to troubleshoot security issues with IAM permissions, column-level access control, and customer-managed encryption keys (CMEK) in BigQuery.
data_source: docs.cloud.google.com
---

# Troubleshoot access control issues

This document shows you how to troubleshoot security issues with Identity and Access Management (IAM) permissions, column-level access control, and customer-managed encryption keys (CMEK) in BigQuery. IAM permission issues typically result in `Access Denied` errors like the following:

- `Access Denied: Project `` PROJECT_ID `` : User does not have bigquery.jobs.create permission in project `` PROJECT_ID `` .`
- `Access Denied: Project `` PROJECT_ID `` : User does not have bigquery.datasets.get permission on dataset `` DATASET `` .`
- `User does not have permission to query table `` PROJECT_ID:DATASET.TABLE `` .`
- `Access Denied: Table `` PROJECT_ID:DATASET.TABLE `` : User does not have permission to query table `` PROJECT_ID:DATASET.TABLE `` , or perhaps it does not exist.`
- `Access Denied: User `` PRINCIPAL `` does not have permission to perform bigquery.tables.getData on resource 'projects/ `` PROJECT_ID `` /datasets/ `` DATASET `` /tables/ `` TABLE `` '.`

## Before you begin

- To troubleshoot a principal's access to a BigQuery resource, ensure that you have the [required IAM permissions](https://docs.cloud.google.com/policy-intelligence/docs/troubleshoot-access#required-permissions) .

## Gather information about the issue

The first step in troubleshooting a resource access issue is to determine the permission that is missing, the IAM principal that was denied access, and the resource the principal was attempting to access.

### Get information from the error or job history

To get information about the principal, the resource, and the permissions, examine the output from the bq command-line tool, the API response, or BigQuery in the Google Cloud console.

For example, if you attempt to run a query with insufficient permissions, you see an error like the following on the **Job information** tab in the **Query results** section of the Google Cloud console.

![An access denied error on the Job Information tab in the Query Results section.](https://docs.cloud.google.com/bigquery/images/job-info-error.png)

Examine the error to determine the principal, the resource, and the permissions.

> **Note:** You can also view job details by using the [job history](https://docs.cloud.google.com/bigquery/docs/managing-jobs#view-job) .

In some cases, you may be able to request missing permissions directly from the error message. For more information, see [Permission error messages](https://docs.cloud.google.com/iam/docs/permission-error-messages) in the IAM documentation.

### Get information from the Cloud Audit Logs

If the error message is generic, missing information, or if the action failed in a background process, use the Cloud Audit Logs Logs Explorer to get information about the error.

1.  In the Google Cloud console, go to the **Logs Explorer** page.

    Alternatively, from the navigation menu, choose **Monitoring \> Logs Explorer** .

2.  In the Logs Explorer, for the logs scope, choose **Project logs** .

3.  In the query window, enter the following query to get permission-related errors from the BigQuery data access logs:

    ```
    resource.type=("bigquery_resource" OR "bigquery_project" OR "bigquery_dataset") AND
    logName=("projects/PROJECT_ID/logs/cloudaudit.googleapis.com%2Fdata_access" OR
      "projects/PROJECT_ID/logs/cloudaudit.googleapis.com%2Factivity") AND
    (protoPayload.status.message:"Access Denied" OR
      protoPayload.status.message:"Permission denied" OR
      protoPayload.status.code=7)
    ```

    Replace ` PROJECT_ID ` with your project ID.

4.  In the query results, expand the log entry that corresponds to your failed operation.

5.  In the `protoPayload` section, expand the `authorizationInfo` array, and then expand each node in the `authorizationInfo` array.

    The `authorizationInfo` array shows every permission check performed during the API call.

6.  To see the cause of the error, look for the `granted: false` entry. The `granted: false` entry shows the following information:

    - `permission` : The IAM permission string that was checked. For example, `bigquery.tables.getData` .
    - `resource` : The fully qualified name of the resource that the principal attempted to access. For example, `projects/myproject/datasets/mydataset/tables/mytable` .
    - `principalEmail` (if available): Referenced in `protoPayload.authenticationInfo` , this is the principal that attempted the action.

    ![The authorizationInfo section of the protoPayload that shows the permission, resource, and principalEmail.](https://docs.cloud.google.com/bigquery/images/authinfo.png)

> **Note:** You can find additional BigQuery audit log sample queries on the Google Cloud Observability [**Sample queries** page](https://docs.cloud.google.com/logging/docs/view/query-library#bigquery-filters) .

## Use the Policy Analyzer for allow policies

Policy Analyzer for allow policies lets you find out which [IAM principals](https://docs.cloud.google.com/iam/docs/principals-overview) have what access to which BigQuery resources based on your [IAM allow policies](https://docs.cloud.google.com/iam/docs/policies) .

> **Note:** Policy Intelligence also provides a [Policy Troubleshooter for IAM](https://docs.cloud.google.com/policy-intelligence/docs/troubleshoot-access) that lets you troubleshoot access for a specific principal.

After you gather information about the permissions error, you can use the Policy Analyzer to understand why the principal lacks the required access. This tool analyzes all relevant policies, memberships in Google Groups, and inheritance from parent resources such as a project, a folder, and your organization.

To use Policy Analyzer for allow policies, you create an analysis query, specify a scope for the analysis, and then run the query.

1.  In the Google Cloud console, go to the **Policy Analyzer** page.

    Alternatively, from the navigation menu, choose **IAM & Admin \> Policy Analyzer** .

2.  Click **Create Custom Query** .

3.  On the **Configure your query** page, enter the information you gathered previously:

    1.  In the **Select the scope** section, in the **Select query scope** field, verify that your current project appears or click **Browse** to choose another resource.

    2.  In the **Set the query parameters** section, for **Parameter 1** , choose **Principal** , and in the **Principal** field, enter the email of the user, group, or service account.

    3.  Click add **Add parameter** .

    4.  For **Parameter 2** , choose **Permission** , and in the **Permission** field, click **Select** , choose the BigQuery permission, and then click **Add** . For example, select **`bigquery.tables.getData`** .

    5.  Click add **Add parameter** .

    6.  For **Parameter 3** , choose **Resource** , and in the **Resource** field, enter the fully qualified resource name. The resource name must include the service prefix as in the following examples:

        - **BigQuery project** : `//cloudresourcemanager.googleapis.com/projects/ `` PROJECT_ID`
        - **BigQuery dataset** : `//bigquery.googleapis.com/projects/ `` PROJECT_ID `` /datasets/ `` DATASET`
        - **BigQuery table** : `//bigquery.googleapis.com/projects/ `` PROJECT `` /datasets/ `` DATASET `` /tables/ `` TABLE`

4.  In the **Custom query** pane, click **Analyze \> Run query** .

5.  Examine the query results. The result can be one of the following:

    - **An empty list** . No results confirm that the principal doesn't have the required permission. You'll need to [grant the principal a role](https://docs.cloud.google.com/bigquery/docs/troubleshoot-access-control#find-role) that provides the correct permissions.
    - **One or more results** . If the analyzer finds an allow policy, some form of access exists. Click **View Binding** on each result to view the roles that provide access to the resource that the principal is a member of. The policy binding shows whether access is granted through group membership or inheritance, or whether access is denied by an [IAM condition](https://docs.cloud.google.com/bigquery/docs/conditions) or an [IAM deny policy](https://docs.cloud.google.com/bigquery/docs/control-access-to-resources-iam#deny_access_to_a_resource) .

## Find the correct IAM role that grants the required permissions

After you confirm that the principal doesn't have sufficient access, the next step is to find the appropriate predefined or custom IAM role that grants the required permissions. The role you choose should adhere to the principle of least privilege.

If your organization uses custom roles, you can find the correct role by [listing all custom roles created in your project or organization](https://docs.cloud.google.com/iam/docs/creating-custom-roles#roles-list) . For example, in the Google Cloud console, on the **Roles** page, you can filter the list by **Type:Custom** to see only custom roles.

To find the correct predefined IAM role, follow these steps.

1.  Open the [BigQuery permissions section](https://docs.cloud.google.com/bigquery/docs/access-control#bq-permissions) of the BigQuery IAM roles and permissions page.

2.  In the **Enter a permission** search bar, enter the permission you retrieved from the error message, job history, or audit logs. For example, `bigquery.tables.getData` .

    The search results show all predefined BigQuery roles that grant the permission.

3.  Apply the principle of least privilege: in the list of roles, choose the least permissive role that grants the required permissions. For example, if you searched for `bigquery.tables.getData` to grant the ability to query table data, [BigQuery Data Viewer](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.dataViewer) is the least permissive role that grants that permission.

4.  Grant the principal the appropriate role. For information about how to grant an IAM role to a BigQuery resource, see [Control access to resources with IAM](https://docs.cloud.google.com/bigquery/docs/control-access-to-resources-iam) .

## Troubleshoot common Access Denied scenarios

When an operation fails with `403 accessDenied` ( `Access Denied: `` RESOURCE_TYPE `` `` RESOURCE_ID `` : `` DETAILS` ), check the following common scenarios in addition to the preceding general IAM steps:

- **Non-existent resource or location mismatch ( `or perhaps it does not exist` ).** When an error message ends with `or perhaps it does not exist` , BigQuery masks whether the table, view, or routine exists because the principal lacks dataset or project metadata permissions ( `bigquery.tables.get` or `bigquery.datasets.get` ). Verify that the project ID, dataset ID, and table name are spelled correctly, and confirm that your query runs in the same location as the dataset.
- **Authorized views and routines.** When a user queries an [authorized view](https://docs.cloud.google.com/bigquery/docs/authorized-views) or [authorized routine](https://docs.cloud.google.com/bigquery/docs/authorized-routines) , the user needs permission to query the view or routine, and the view or routine itself must be authorized on the source dataset's access control list (ACL). If the query fails with `Access Denied` on the underlying base table, add the view or routine (or its entire dataset as an [authorized dataset](https://docs.cloud.google.com/bigquery/docs/authorized-datasets) ) to the source dataset's authorized access list. If a view queries another view, every view in the chain must be authorized on the dataset that it reads from. If an authorized view was deleted and then recreated with the same name, the deleted view can remain in the source dataset's authorized access list for up to 24 hours, and authorizing the new view fails with `Duplicate authorized views` . Remove the old entry from the list and then authorize the new view, or [update the view's SQL query](https://docs.cloud.google.com/bigquery/docs/managing-views#update-sql) instead of deleting and recreating the view. If you modify an authorized routine with a `CREATE OR REPLACE` statement or the `routines.update` method, you must re-authorize the routine.
- **VPC Service Controls.** If your organization uses [VPC Service Controls](https://docs.cloud.google.com/bigquery/docs/vpc-sc) , requests that cross a service perimeter boundary fail with `403 accessDenied` or `policyViolation` . Search Cloud Audit Logs around the time of the failure for the `vpcServiceControlsUniqueIdentifier` value from the error message, and use the [Violation Analyzer](https://docs.cloud.google.com/vpc-service-controls/docs/violation-analyzer) to inspect ingress and egress rules. For the Logs Explorer query to use, see [Request is prohibited by organization's policy](https://docs.cloud.google.com/bigquery/docs/troubleshoot-access-control#ts-policy-violation-vpc-sc) .
- **Basic roles ( `roles/owner` , `roles/editor` , `roles/viewer` ).** Basic project roles don't include organization-level permissions required for views such as `INFORMATION_SCHEMA.TABLE_STORAGE_USAGE_TIMELINE_BY_ORGANIZATION` , or specialized permissions such as `bigquery.rowAccessPolicies.overrideTimeTravelRestrictions` , which is required to access the historical data of a table that has or had row-level access policies (see [Time travel and row-level access](https://docs.cloud.google.com/bigquery/docs/time-travel#time_travel_and_row-level_access) ). Grant predefined [BigQuery IAM roles](https://docs.cloud.google.com/bigquery/docs/access-control) instead of relying on basic roles.
- **Transient IAM policy overwrites ( `SetIamPolicy` ).** If permissions work intermittently and then fail, search the Admin Activity audit logs for `protoPayload.methodName=~"SetIamPolicy"` to check whether an automated script or infrastructure-as-code pipeline is overwriting existing policy bindings instead of merging them.
- **External data sources (Google Drive, Cloud Storage, BigLake):**
  - **Google Drive ( `Permission denied while getting Drive credentials` ).** Grant the user or service account viewer access to the Google Drive file or Google Sheet, ensure the caller provides the `https://www.googleapis.com/auth/drive` OAuth scope, or update [scheduled query credentials](https://docs.cloud.google.com/bigquery/docs/troubleshoot-queries#error_code_invalid_userid) .
  - **Cloud Storage and BigLake tables.** Grant `roles/storage.objectViewer` on the Cloud Storage bucket to the user (for standard external tables) or to the [BigLake connection service account](https://docs.cloud.google.com/bigquery/docs/biglake-intro) (for BigLake tables).
- **Customer-managed encryption keys (CMEK).** If the query references a table that's protected by CMEK, make sure that the corresponding Cloud KMS key exists and is enabled. If a query or load job fails with `Cloud KMS Error: Permission 'cloudkms.cryptoKeyVersions.useToEncrypt' denied` (or `useToDecrypt` ), grant the BigQuery Encryption Service Agent ( `bq- `` PROJECT_NUMBER `` @bigquery-encryption.iam.gserviceaccount.com` ) the `roles/cloudkms.cryptoKeyEncrypterDecrypter` role on the Cloud Key Management Service key. See [Grant encryption and decryption permission](https://docs.cloud.google.com/bigquery/docs/customer-managed-encryption#grant_permission) . For other CMEK errors, see [Troubleshoot customer-managed encryption keys](https://docs.cloud.google.com/bigquery/docs/troubleshoot-access-control#troubleshoot-cmek) .
- **Service account impersonation.** If a request using service account impersonation fails with `Permission 'iam.serviceAccounts.getAccessToken' denied` , grant the calling principal `roles/iam.serviceAccountTokenCreator` on the target service account.
- **Column-level security (policy tags) and row-level security.** If a query or DML statement fails with `Requires fineGrainedGet permission on the read columns` or `User does not have permission to access data protected by policy tag` , grant the principal the Data Catalog [Fine-Grained Reader](https://docs.cloud.google.com/bigquery/docs/column-level-security#fine_grained_reader) ( `roles/datacatalog.categoryFineGrainedReader` ) role on the policy tag, or exclude the protected columns from your `SELECT` list. See [Insufficient column-level access control permissions](https://docs.cloud.google.com/bigquery/docs/troubleshoot-queries#column-dml) . If the table uses [row-level security](https://docs.cloud.google.com/bigquery/docs/row-level-security-intro) , review its active row-level access policies in the Google Cloud console or by running `bq ls --row_access_policies` . See [List table row-level access policies](https://docs.cloud.google.com/bigquery/docs/managing-row-level-security#list_table_row-level_access_policies) .
- **IAM and metadata propagation delays.** Newly granted IAM roles and dataset ACL updates are eventually consistent and typically take a few minutes to propagate across caches. If a permission was just granted, wait a few minutes and retry the request.

## BigQuery Terms of Service not accepted

Error string: `BigQuery Terms of Service have not been accepted`

This HTTP `403 Forbidden` error ( `reason: termsOfServiceNotAccepted` ) occurs when the BigQuery Terms of Service haven't been accepted. The error isn't caused by missing IAM permissions. It can be returned for requests such as creating a dataset or loading data.

To resolve this issue, do the following:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  If the welcome page appears, select your country, select the **Terms of Service** checkbox, and then click **Agree and continue** . For more information, see [Enable the BigQuery sandbox](https://docs.cloud.google.com/bigquery/docs/sandbox#setup) .

After the Terms of Service are accepted, retry the request.

## Troubleshoot policy violation errors

When you receive an HTTP `403 PERMISSION_DENIED` error in BigQuery with the `policyViolation` error reason, it indicates a failure driven by organizational policies, data perimeters, or VPC Service Controls.

The following sections describe the most common error messages associated with this error reason, what causes them, and how to resolve them.

### Request is prohibited by organization's policy

Error string: `VPC Service Controls: Request is prohibited by organization's policy. vpcServiceControlsUniqueIdentifier: `` VPC_SERVICE_CONTROLS_UNIQUE_IDENTIFIER`

#### Diagnosis

Your request originated from a network address or client that is outside the designated VPC Service Controls perimeter, or the request violated the defined ingress and egress rules for your workspace. This frequently occurs when your query spans multiple projects. For example, the query billing project is outside the data project's secure perimeter.

#### Resolution

1.  **Find the Unique ID.** Retrieve the `vpcServiceControlsUniqueIdentifier` included in the error message. Use this ID to filter your Google Cloud Logs Explorer to find the corresponding VPC Service Controls log with the details of the reason:

    ```
    protoPayload.metadata.@type="type.googleapis.com/google.cloud.audit.VpcServiceControlAuditMetadata"
    protoPayload.metadata.vpcServiceControlsUniqueId="VPC_SERVICE_CONTROLS_UNIQUE_IDENTIFIER"
    ```

    Look for the `violationReason` value under `protoPayload.metadata.violationReason` . Once identified, study the additional details in the log entry and follow the existing [VPC Service Controls troubleshooting guide](https://docs.cloud.google.com/vpc-service-controls/docs/troubleshooting#debugging) . Additionally, consider using the [Violation Analyzer](https://docs.cloud.google.com/vpc-service-controls/docs/violation-analyzer) .

2.  **Fix Cross-Project Billing.** For cross-project queries, ensure the billing project that executes the query resides in the same perimeter as the queried data within the perimeter. If needed, specify a compliant billing project manually using the Google Cloud console project picker, the [`--project_id` flag](https://docs.cloud.google.com/bigquery/docs/reference/bq-cli-reference#project_id_flag) in the bq command-line tool, or your [API or client library request](https://docs.cloud.google.com/bigquery/docs/running-queries#queries) .

3.  **Verify Access Levels.** Make sure your client network, IP, or user account is permitted using [Access Context Manager](https://docs.cloud.google.com/access-context-manager/docs/overview) . The Google Cloud console requires ingress rules specifically configured to allow user access to protected environments.

### Export to Google Drive is blocked for projects with VPC Service Controls enabled

Error string: `Export to Google Drive is blocked for projects with VPC-SC enabled`

#### Diagnosis

Google Drive doesn't support VPC Service Controls. Because Google Drive can't enforce the security perimeter, BigQuery automatically disables exporting API extracts to Google Drive for any request originating inside a VPC Service Controls boundary to prevent data exfiltration.

#### Resolution

Instead of exporting directly to Google Drive, extract your query results to a Cloud Storage bucket located inside the same VPC Service Controls perimeter, or save the results as a local file.

### Google Drive external tables are blocked for projects with VPC Service Controls enabled

Error string: `Google Drive external tables are blocked for projects with VPC-SC enabled`

#### Diagnosis

By default, VPC Service Controls does not block querying Google Drive external tables (such as Connected Sheets). However, this error appears because your Google Cloud organization has explicitly requested that Google Cloud enforce a strict blocking configuration for your project to override the default permissive behavior, preventing any inbound queries to Google Drive data from within a VPC Service Controls perimeter.

#### Resolution

Import the data from the Google Sheet or Google Drive file directly into a standard BigQuery table inside your VPC Service Controls perimeter, rather than querying it dynamically as an external federated table. Alternatively, contact your internal Cloud Administrator to discuss your organization's data export boundaries.

### Export to Google Drive is blocked for your project

Error string: `Export to Google Drive is blocked for your project.`

#### Diagnosis

Even without a VPC Service Controls perimeter, your Google Cloud administrators have requested a specific, strict organizational configuration to be applied to your project denying all data extraction capabilities to Google Drive.

#### Resolution

Choose an alternative extraction destination such as a Cloud Storage bucket or a local file, or contact your internal Cloud Administrator to discuss your organization's data export boundaries.

### Location violates organization policy constraint

Error string: `LOCATION `` violates constraint `` CONSTRAINT_NAME `` on the resource projects/ `` PROJECT_ID` or `LOCATION `` violates constraint `` CONSTRAINT_NAME `` on the resource projects/ `` PROJECT_ID `` /datasets/ `` DATASET_ID`

#### Diagnosis

Your Cloud Administrator has configured an [Organization Policy Constraint](https://docs.cloud.google.com/organization-policy/reference/org-policy-constraints) to restrict exactly where resources can be created or analyzed. This error commonly appears when:

- Creating a dataset in an unauthorized geographic region (for example, restricted by `constraints/gcp.resourceLocations` ).
- Attempting to use BigQuery Omni across external clouds when it isn't allowed (for example, blocked by `constraints/bigquery.disableBQOmniAWS` or `constraints/bigquery.disableBQOmniAzure` ).

#### Resolution

1.  Check the exact `CONSTRAINT_NAME` provided in the error message to understand what action is being blocked.
2.  Select a different, unblocked region for your data, or work with your Google Cloud organization administrator to review the organizational policy at the Folder or Organization level. See [structuring and defining resource locations](https://docs.cloud.google.com/organization-policy/restrict-locations) for more details.

## Troubleshoot unauthenticated errors

When you receive an HTTP `401 Unauthorized` (gRPC `UNAUTHENTICATED` ) error in BigQuery with the `unauthenticated` error reason, the request lacks valid authentication credentials, the OAuth 2.0 access token has expired, or the caller can't authenticate as the specified identity.

The following sections describe the most common `unauthenticated` scenarios, what causes them, and how to resolve them.

### Invalid or expired credentials

Error strings:

- `Invalid credential`
- `User credential was invalid.`
- `Credentials expired`
- `Credentials missing required scope.`
- `Request had invalid authentication credentials. Expected OAuth 2 access token, login cookie or other valid authentication credential.`

#### Diagnosis

The access token, service account key, or Application Default Credentials (ADC) supplied with the request are expired, revoked, or missing required OAuth 2.0 scopes. This error also occurs when the request is signed with a system clock that has drifted from Network Time Protocol (NTP) time.

#### Resolution

- **Refresh your credentials.** If you are authenticating from a local development environment, run `gcloud auth application-default login` (for ADC) or `gcloud auth login` to obtain a fresh token.
- **Verify service account keys and OAuth scopes.** If your application uses `GOOGLE_APPLICATION_CREDENTIALS` , verify that the variable points to a valid, unrevoked JSON key file, that the service account is enabled in the Google Cloud console, and that the credential includes the required `https://www.googleapis.com/auth/bigquery` or `https://www.googleapis.com/auth/cloud-platform` scope.
- **Use current client libraries and synchronize system clocks.** Update your [BigQuery client library](https://docs.cloud.google.com/bigquery/docs/reference/libraries) or [ODBC](https://docs.cloud.google.com/bigquery/docs/odbc-for-bigquery) or [JDBC](https://docs.cloud.google.com/bigquery/docs/jdbc-for-bigquery) driver to the latest version so that OAuth 2.0 token refreshes and federated credentials are handled automatically. Also ensure that the host machine's system clock is synchronized using NTP.

### Missing end-user credentials or service account impersonation permission

Error strings:

- `Current user can not act as user for service account `` SERVICE_ACCOUNT_EMAIL`
- `No end user credentials found when accessing `` PROJECT_ID `` : `` DATASET_ID `` . `` TABLE_ID `` . Please use end user credentials to call BigQuery APIs.`

#### Diagnosis

The job or continuous query is configured to run as a custom service account that the caller doesn't have permission to act as, or the target table or security policy requires end-user credentials (EUC) so that BigQuery can evaluate access against an interactive user identity.

#### Resolution

- **Grant service account impersonation permissions.** When running a [continuous query](https://docs.cloud.google.com/bigquery/docs/continuous-queries) or job configured with a custom service account, grant the caller the Service Account User role ( `roles/iam.serviceAccountUser` , which includes the `iam.serviceAccounts.actAs` permission) on that service account. When impersonating a service account or exchanging federated credentials for a short-lived token, grant the caller the Service Account Token Creator role ( `roles/iam.serviceAccountTokenCreator` ) on the target service account.
- **Authenticate with end-user credentials.** When the target resource requires end-user credentials, authenticate the request using an interactive user's OAuth 2.0 credentials (for example, by running `gcloud auth application-default login` or configuring user OAuth in your BI tool) rather than standalone service account credentials.
- **Verify VPC Service Controls ingress and egress rules.** If the request crosses a VPC Service Controls boundary, verify that the perimeter's ingress and egress rules permit the caller identity and target resource.

### Account restricted, suspended, or deleted

Error strings:

- `The account was restricted due to `` REASON`
- `Account deleted`

#### Diagnosis

The Google Account or Google Workspace account issuing the request has been suspended, disabled, restricted, or deleted by an administrator or account security policy.

#### Resolution

Contact your Google Workspace or Cloud Identity administrator to review the account status in the Google Admin console and restore or un-suspend the user account, or update the workload to authenticate with an active service account.

## Troubleshoot column-level access control

The following sections explain how to troubleshoot issues with [column-level access control](https://docs.cloud.google.com/bigquery/docs/column-level-security) and Data Catalog policy tags.

### I can't see the Data Catalog roles

If you can't see roles such as Data Catalog Fine-Grained Reader, it's possible that you haven't enabled the Data Catalog API in your project. To learn how to enable the Data Catalog API, see [Before you begin](https://docs.cloud.google.com/bigquery/docs/column-level-security#before_you_begin) . The Data Catalog roles appear several minutes after you enable the Data Catalog API.

### I can't view the Taxonomies page

You need additional permissions to view the **Policy tag taxonomies** page in the Google Cloud console. For example, the Data Catalog [Policy Tag Admin](https://docs.cloud.google.com/bigquery/docs/column-level-security#policy_tags_admin) role has access to the **Taxonomies** page.

### I enforced policy tags, but it doesn't seem to work

If you're still receiving query results for an account that shouldn't have access, it's possible that the account is receiving cached results. Specifically, if you previously ran the query successfully and then enforced policy tags, you might be getting results from the [query result cache](https://docs.cloud.google.com/bigquery/docs/cached-results) . By default, query results are cached for 24 hours. The query fails immediately if you [disable the result cache](https://docs.cloud.google.com/bigquery/docs/cached-results#disabling_retrieval_of_cached_results) . For more details about caching, see [Impact of column-level access control](https://docs.cloud.google.com/bigquery/docs/cached-results#security) .

In general, IAM updates take about 30 seconds to propagate. Changes in the policy tag hierarchy can take up to 30 minutes to propagate.

### I don't have the permission to read from a table with column-level security

You need either the [Fine-Grained Reader role](https://docs.cloud.google.com/bigquery/docs/column-level-security#fine_grained_reader) or the [Masked Reader role](https://docs.cloud.google.com/bigquery/docs/column-data-masking-intro#roles_for_querying_masked_data) at different levels, such as organization, folder, project, and policy tag. The Fine-Grained Reader role grants raw data access, while the Masked Reader role grants access to [masked data](https://docs.cloud.google.com/bigquery/docs/column-data-masking-intro) . You can use the [IAM Policy Troubleshooter](https://docs.cloud.google.com/policy-intelligence/docs/troubleshoot-access) to check this permission at the project level.

### I set fine-grained access control in policy tag taxonomy, but users see protected data

To troubleshoot this issue, confirm the following details:

- On the [**Policy tag taxonomies** page](https://console.cloud.google.com/bigquery/security/secure/policy-tags) of the BigQuery **Security center** , confirm that the **Enforce access control** toggle is in the **On** position.

- Ensure that your queries aren't using [cached query results](https://docs.cloud.google.com/bigquery/docs/cached-results) . If you use the bq command-line tool to test your queries, then use the `--nouse_cache` flag to disable the query cache. For example:

  ```
  bq query --nouse_cache --use_legacy_sql=false "SELECT * EXCEPT (customer_pii) FROM my_table;"
  ```

### Project migration considerations

Policy tags and taxonomies are homed within a specific Google Cloud organization and aren't automatically re-associated when a project is migrated to a new organization. If you migrate a project that uses policy tags for column-level access control to a different organization, the following issues occur:

- The policy tags are no longer manageable in the Google Cloud console within the migrated project.
- You can't apply these policy tags to new columns in the migrated project.
- Existing column-level access controls might appear to still be in place, but the link to the source taxonomy in the original organization is broken for management purposes.

Resolving this issue requires manual intervention by Google Cloud Support to re-associate the taxonomy with the new organization. If you migrated a project with policy tags and encounter these issues, [contact Cloud Customer Care](https://docs.cloud.google.com/support) .

## Troubleshoot customer-managed encryption keys

The following list describes common errors and recommended resolutions when you use customer-managed encryption keys (CMEK) with Cloud Key Management Service:

Error: `Please grant Cloud KMS CryptoKey Encrypter/Decrypter role`  
**Resolution:** The BigQuery service account associated with your project doesn't have sufficient IAM permission to operate on the specified Cloud KMS key. To grant the required IAM permission, follow the instructions in the error message or in [Grant encryption and decryption permission](https://docs.cloud.google.com/bigquery/docs/customer-managed-encryption#grant_permission) .

Error: `Existing table encryption settings don't match encryption settings specified in the request`  
**Resolution:** This error can occur when the destination table has encryption settings that don't match the encryption settings in your request. To resolve this issue, use the `TRUNCATE` write disposition to replace the table, or specify a different destination table.

Error: `This region is not supported`  
**Resolution:** The region of the Cloud KMS key doesn't match the region of the BigQuery dataset for the destination table. To resolve this issue, select a key in a region that matches your dataset, or load data into a dataset that matches the key region.

Error: `Your administrator requires that you specify an encryption key for queries in project `` PROJECT_ID `` .`  
**Resolution:** An organization policy prevented creating a resource or running a query. To learn more about this policy, see [Require CMEKs for all resources](https://docs.cloud.google.com/bigquery/docs/customer-managed-encryption#services_constraint) .

Error: `Your administrator prevents using KMS keys from project `` KMS_PROJECT_ID `` to protect resources in project `` PROJECT_ID `` .`  
**Resolution:** An organization policy prevented creating a resource or running a query. To learn more about this policy, see [Restrict Cloud KMS keys for a BigQuery project](https://docs.cloud.google.com/bigquery/docs/customer-managed-encryption#projects_constraint) .

## What's next

- For a list of all BigQuery IAM roles and permissions, see [BigQuery IAM roles and permissions](https://docs.cloud.google.com/bigquery/docs/access-control) .
- For more information about column-level security, see [Restrict access with column-level access control](https://docs.cloud.google.com/bigquery/docs/column-level-security) .
- For more information about customer-managed encryption keys, see [Protect data with Cloud KMS keys](https://docs.cloud.google.com/bigquery/docs/customer-managed-encryption) .
- For more information about troubleshooting allow and deny policies in IAM, see [Troubleshoot policies](https://docs.cloud.google.com/iam/docs/troubleshoot-policies) .
- For more information about the Policy Intelligence Policy Analyzer, see [Policy Analyzer for allow policies](https://docs.cloud.google.com/policy-intelligence/docs/policy-analyzer-overview) .
- For more information about the Policy Troubleshooter, see [Use Policy Troubleshooter](https://docs.cloud.google.com/iam/docs/troubleshoot-policies#troubleshooter) .
