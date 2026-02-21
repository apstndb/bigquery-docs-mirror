# Manage Sharing data exchanges and listings using custom constraints

**Preview**

This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

**Note:** To provide feedback or request support, contact <bq-data-sharing-feedback@google.com> .

This page shows you how to use Organization Policy Service custom constraints to restrict specific operations on the following Google Cloud resources:

  - `  analyticshub.googleapis.com/DataExchange  `
  - `  analyticshub.googleapis.com/Listing  `

To learn more about Organization Policy, see [Custom organization policies](/resource-manager/docs/organization-policy/overview#custom-organization-policies) .

## About organization policies and constraints

The Google Cloud Organization Policy Service gives you centralized, programmatic control over your organization's resources. As the [organization policy administrator](/iam/docs/roles-permissions/orgpolicy#orgpolicy.policyAdmin) , you can define an organization policy, which is a set of restrictions called *constraints* that apply to Google Cloud resources and descendants of those resources in the [Google Cloud resource hierarchy](/resource-manager/docs/cloud-platform-resource-hierarchy) . You can enforce organization policies at the organization, folder, or project level.

Organization Policy provides built-in [managed constraints](/resource-manager/docs/organization-policy/org-policy-constraints) for various Google Cloud services. However, if you want more granular, customizable control over the specific fields that are restricted in your organization policies, you can also create *custom constraints* and use those custom constraints in an organization policy.

### Policy inheritance

By default, organization policies are inherited by the descendants of the resources on which you enforce the policy. For example, if you enforce a policy on a folder, Google Cloud enforces the policy on all projects in the folder. To learn more about this behavior and how to change it, refer to [Hierarchy evaluation rules](/resource-manager/docs/organization-policy/understanding-hierarchy#disallow_inheritance) .

## Limitations

  - You can set up custom constraints for BigQuery sharing resources only by using the Google Cloud console or Google Cloud CLI.
  - You can enforce custom constraints only on the `  CREATE  ` or `  UPDATE  ` methods for BigQuery sharing resources.
  - New custom constraints don't automatically apply to existing resources. You must update existing resources for the constraint to apply. To find existing resources that need to be updated, enforce a [dry-run organization policy](/resource-manager/docs/organization-policy/dry-run-policy) . Existing [listings published to data clean rooms](/bigquery/docs/data-clean-rooms#add-data) aren't checked during the dry run of existing resources.
  - Simulating constraints on current resources is not supported.
  - You must set the value in the `  resource.bigqueryDataset.replicaLocations  ` field in lowercase letters. For more information, see [Supported resources](#supported_resources) .

## Before you begin

1.  Sign in to your Google Cloud account. If you're new to Google Cloud, [create an account](https://console.cloud.google.com/freetrial) to evaluate how our products perform in real-world scenarios. New customers also get $300 in free credits to run, test, and deploy workloads.

2.  In the Google Cloud console, on the project selector page, select or create a Google Cloud project.
    
    **Roles required to select or create a project**
    
      - **Select a project** : Selecting a project doesn't require a specific IAM role—you can select any project that you've been granted a role on.
      - **Create a project** : To create a project, you need the Project Creator role ( `  roles/resourcemanager.projectCreator  ` ), which contains the `  resourcemanager.projects.create  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .
    
    **Note** : If you don't plan to keep the resources that you create in this procedure, create a project instead of selecting an existing project. After you finish these steps, you can delete the project, removing all resources associated with the project.

3.  [Verify that billing is enabled for your Google Cloud project](/billing/docs/how-to/verify-billing-enabled#confirm_billing_is_enabled_on_a_project) .

4.  [Install](/sdk/docs/install) the Google Cloud CLI.

5.  If you're using an external identity provider (IdP), you must first [sign in to the gcloud CLI with your federated identity](/iam/docs/workforce-log-in-gcloud) .

6.  To [initialize](/sdk/docs/initializing) the gcloud CLI, run the following command:
    
    ``` text
    gcloud init
    ```

7.  In the Google Cloud console, on the project selector page, select or create a Google Cloud project.
    
    **Roles required to select or create a project**
    
      - **Select a project** : Selecting a project doesn't require a specific IAM role—you can select any project that you've been granted a role on.
      - **Create a project** : To create a project, you need the Project Creator role ( `  roles/resourcemanager.projectCreator  ` ), which contains the `  resourcemanager.projects.create  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .
    
    **Note** : If you don't plan to keep the resources that you create in this procedure, create a project instead of selecting an existing project. After you finish these steps, you can delete the project, removing all resources associated with the project.

8.  [Verify that billing is enabled for your Google Cloud project](/billing/docs/how-to/verify-billing-enabled#confirm_billing_is_enabled_on_a_project) .

9.  [Install](/sdk/docs/install) the Google Cloud CLI.

10. If you're using an external identity provider (IdP), you must first [sign in to the gcloud CLI with your federated identity](/iam/docs/workforce-log-in-gcloud) .

11. To [initialize](/sdk/docs/initializing) the gcloud CLI, run the following command:
    
    ``` text
    gcloud init
    ```

12. Ensure that you know your [organization ID](/resource-manager/docs/creating-managing-organization#retrieving_your_organization_id) .

### Required roles

To get the permissions that you need to manage custom organization policies, ask your administrator to grant you the [Organization Policy Administrator](/iam/docs/roles-permissions/orgpolicy#orgpolicy.policyAdmin) ( `  roles/orgpolicy.policyAdmin  ` ) IAM role on the organization resource. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

## Set up a custom constraint

A custom constraint is defined in a YAML file by the resources, methods, conditions, and actions that are supported by the service on which you are enforcing the organization policy. Conditions for your custom constraints are defined using [Common Expression Language (CEL)](https://github.com/google/cel-spec/blob/master/doc/intro.md) . For more information about how to build conditions in custom constraints using CEL, see the CEL section of [Creating and managing custom constraints](/resource-manager/docs/organization-policy/creating-managing-custom-constraints#common_expression_language) .

### Console

To create a custom constraint, do the following:

In the Google Cloud console, go to the **Organization policies** page.

From the project picker, select the project that you want to set the organization policy for.

Click add **Custom constraint** .

In the **Display name** box, enter a human-readable name for the constraint. This name is used in error messages and can be used for identification and debugging. Don't use PII or sensitive data in display names because this name could be exposed in error messages. This field can contain up to 200 characters.

In the **Constraint ID** box, enter the name that you want for your new custom constraint. A custom constraint can only contain letters (including upper and lowercase) or numbers, for example `  custom.disableGkeAutoUpgrade  ` . This field can contain up to 70 characters, not counting the prefix ( `  custom.  ` ), for example, `  organizations/123456789/customConstraints/custom  ` . Don't include PII or sensitive data in your constraint ID, because it could be exposed in error messages.

In the **Description** box, enter a human-readable description of the constraint. This description is used as an error message when the policy is violated. Include details about why the policy violation occurred and how to resolve the policy violation. Don't include PII or sensitive data in your description, because it could be exposed in error messages. This field can contain up to 2000 characters.

In the **Resource type** box, select the name of the Google Cloud REST resource containing the object and field that you want to restrict—for example, `  container.googleapis.com/NodePool  ` . Most resource types support up to 20 custom constraints. If you attempt to create more custom constraints, the operation fails.

Under **Enforcement method** , select whether to enforce the constraint on a REST **CREATE** method or on both **CREATE** and **UPDATE** methods. If you enforce the constraint with the **UPDATE** method on a resource that violates the constraint, changes to that resource are blocked by the organization policy unless the change resolves the violation.

Not all Google Cloud services support both methods. To see supported methods for each service, find the service in [Supported services](/resource-manager/docs/organization-policy/custom-constraint-supported-services) .

To define a condition, click edit **Edit condition** .

1.  In the **Add condition** panel, create a CEL condition that refers to a supported service resource, for example, `  resource.management.autoUpgrade == false  ` . This field can contain up to 1000 characters. For details about CEL usage, see [Common Expression Language](/resource-manager/docs/organization-policy/creating-managing-custom-constraints#common_expression_language) . For more information about the service resources you can use in your custom constraints, see [Custom constraint supported services](/resource-manager/docs/organization-policy/custom-constraint-supported-services) .
2.  Click **Save** .

Under **Action** , select whether to allow or deny the evaluated method if the condition is met.

The deny action means that the operation to create or update the resource is blocked if the condition evaluates to true.

The allow action means that the operation to create or update the resource is permitted only if the condition evaluates to true. Every other case except ones explicitly listed in the condition is blocked.

Click **Create constraint** .

When you have entered a value into each field, the equivalent YAML configuration for this custom constraint appears on the right.

### gcloud

To create a custom constraint, create a YAML file using the following format:

``` text
name: organizations/ORGANIZATION_ID/customConstraints/CONSTRAINT_NAME
resourceTypes: RESOURCE_NAME
methodTypes:
  - CREATE
- UPDATE 
condition: "CONDITION"
actionType: ACTION
displayName: DISPLAY_NAME
description: DESCRIPTION
```

Replace the following:

  - `  ORGANIZATION_ID  ` : your organization ID, such as `  123456789  ` .
  - `  CONSTRAINT_NAME  ` : the name that you want for your new custom constraint. A custom constraint can only contain letters (including upper and lowercase) or numbers, for example, `  custom.enforceDataExchangeDiscovery  ` . This field can contain up to 70 characters.
  - `  RESOURCE_NAME  ` : the fully qualified name of the Google Cloud resource containing the object and field that you want to restrict. For example, `  analyticshub.googleapis.com/DataExchange  ` .
  - `  CONDITION  ` : a [CEL condition](/resource-manager/docs/organization-policy/creating-managing-custom-constraints#common_expression_language) that is written against a representation of a supported service resource. This field can contain up to 1000 characters. For example, `  "resource.discoveryType == 'DISCOVERY_TYPE_PUBLIC'"  ` .
  - `  ACTION  ` : the action to take if the `  condition  ` is met. Possible values are `  ALLOW  ` and `  DENY  ` .
  - `  DISPLAY_NAME  ` : a human-friendly name for the constraint. This field can contain up to 200 characters.
  - `  DESCRIPTION  ` : a human-friendly description of the constraint to display as an error message when the policy is violated. This field can contain up to 2000 characters.

After you have created the YAML file for a new custom constraint, you must set it up to make it available for organization policies in your organization. To set up a custom constraint, use the [`  gcloud org-policies set-custom-constraint  `](/sdk/gcloud/reference/org-policies/set-custom-constraint) command:

``` text
gcloud org-policies set-custom-constraint CONSTRAINT_PATH
```

Replace `  CONSTRAINT_PATH  ` with the full path to your custom constraint file. For example, `  /home/user/customconstraint.yaml  ` .

After this operation is complete, your custom constraints are available as organization policies in your list of Google Cloud organization policies.

To verify that the custom constraint exists, use the [`  gcloud org-policies list-custom-constraints  `](/sdk/gcloud/reference/org-policies/list-custom-constraints) command:

``` text
gcloud org-policies list-custom-constraints --organization=ORGANIZATION_ID
```

Replace `  ORGANIZATION_ID  ` with the ID of your organization resource.

For more information, see [Viewing organization policies](/resource-manager/docs/organization-policy/creating-managing-policies#viewing_organization_policies) .

## Enforce a custom organization policy

You can enforce a constraint by creating an organization policy that references it, and then applying that organization policy to a Google Cloud resource.

### Console

1.  In the Google Cloud console, go to the **Organization policies** page.
2.  From the project picker, select the project that you want to set the organization policy for.
3.  From the list on the **Organization policies** page, select your constraint to view the **Policy details** page for that constraint.
4.  To configure the organization policy for this resource, click **Manage policy** .
5.  On the **Edit policy** page, select **Override parent's policy** .
6.  Click **Add a rule** .
7.  In the **Enforcement** section, select whether this organization policy is enforced or not.
8.  Optional: To make the organization policy conditional on a tag, click **Add condition** . Note that if you add a conditional rule to an organization policy, you must add at least one unconditional rule or the policy cannot be saved. For more information, see [Setting an organization policy with tags](/resource-manager/docs/organization-policy/tags-organization-policy) .
9.  Click **Test changes** to simulate the effect of the organization policy. For more information, see [Test organization policy changes with Policy Simulator](/policy-intelligence/docs/test-organization-policies) .
10. To enforce the organization policy in dry-run mode, click **Set dry run policy** . For more information, see [Create an organization policy in dry-run mode](/resource-manager/docs/organization-policy/dry-run-policy) .
11. After you verify that the organization policy in dry-run mode works as intended, set the live policy by clicking **Set policy** .

### gcloud

To create an organization policy with boolean rules, create a policy YAML file that references the constraint:

``` text
name: projects/PROJECT_ID/policies/CONSTRAINT_NAME
spec:
  rules:
  - enforce: true

dryRunSpec:
  rules:
  - enforce: true
```

Replace the following:

  - `  PROJECT_ID  ` : the project that you want to enforce your constraint on.
  - `  CONSTRAINT_NAME  ` : the name you defined for your custom constraint. For example, `  custom.enforceDataExchangeDiscovery  ` .

To enforce the organization policy in [dry-run mode](/resource-manager/docs/organization-policy/dry-run-policy) , run the following command with the `  dryRunSpec  ` flag:

``` text
gcloud org-policies set-policy POLICY_PATH --update-mask=dryRunSpec
```

Replace `  POLICY_PATH  ` with the full path to your organization policy YAML file. The policy requires up to 15 minutes to take effect.

After you verify that the organization policy in dry-run mode works as intended, set the live policy with the `  org-policies set-policy  ` command and the `  spec  ` flag:

``` text
gcloud org-policies set-policy POLICY_PATH --update-mask=spec
```

Replace `  POLICY_PATH  ` with the full path to your organization policy YAML file. The policy requires up to 15 minutes to take effect.

## Test the custom organization policy

The following example shows how you can create a custom constraint and policy that requires all `  analyticshub.googleapis.com/DataExchange  ` resources to be private.

Before you begin, you must have the following:

  - Your organization ID
  - A project ID

### Create the constraint

To create a custom constraint, follow these steps:

1.  Save the following file as `  constraint-enforce-dataExchangeDiscovery.yaml  ` :
    
    ``` text
    name: organizations/ORGANIZATION_ID/customConstraints/custom.enforceDataExchangeDiscovery
    resourceTypes:
    - analyticshub.googleapis.com/DataExchange
    methodTypes:
    - CREATE
    condition: "resource.discoveryType == 'DISCOVERY_TYPE_PUBLIC'"
    actionType: DENY
    displayName: Reject public DataExchanges.
    description: All DataExchange resources must be private.
    ```
    
    Replace `  ORGANIZATION_ID  ` with your organization ID.
    
    This constraint denies operations to create or configure new `  analyticshub.googleapis.com/DataExchange  ` resources if their discovery type is public.

2.  Apply the constraint:
    
    ``` text
    gcloud org-policies set-custom-constraint ~/constraint-enforce-dataExchangeDiscovery.yaml
    ```

3.  Verify that the constraint exists:
    
    ``` text
    gcloud org-policies list-custom-constraints --organization=ORGANIZATION_ID
    ```
    
    The output is similar to the following:
    
    ``` text
    CUSTOM_CONSTRAINT                       ACTION_TYPE  METHOD_TYPES   RESOURCE_TYPES                           DISPLAY_NAME
    custom.enforceDataExchangeDiscovery     DENY         CREATE,UPDATE  analyticshub.googleapis.com/DataExchange Reject public DataExchanges.
    ...
    ```

### Create the policy

Create a policy and apply that policy to the custom constraint that you created.

1.  Save the following file as `  policy-enforce-dataExchangeDiscovery.yaml  ` :
    
    ``` text
    name: projects/PROJECT_ID/policies/custom.enforceDataExchangeDiscovery
    spec:
      rules:
      - enforce: true
    ```
    
    Replace `  PROJECT_ID  ` with your project ID.

2.  Apply the policy:
    
    ``` text
    gcloud org-policies set-policy ~/policy-enforce-dataExchangeDiscovery.yaml
    ```

3.  Verify that the policy exists:
    
    ``` text
    gcloud org-policies list --project=PROJECT_ID
    ```
    
    The output is similar to the following:
    
    ``` text
    CONSTRAINT                           LIST_POLICY    BOOLEAN_POLICY    ETAG
    custom.enforceDataExchangeDiscovery  -              SET               ETAG
    ```

After you apply the policy, wait about two minutes for Google Cloud to start enforcing the policy.

### Test the policy

Follow the steps in [Create a data exchange](/bigquery/docs/analytics-hub-manage-exchanges#create-exchange) to create a `  analyticshub.googleapis.com/DataExchange  ` resource in your project. Make it publicly discoverable.

The output is the following:

``` text
Operation failed, please try again. Error Message: Operation denied by org policy on resource 'projects/PROJECT_ID/locations/us':
["customConstraints/custom.enforceDataExchangeDiscovery": "All DataExchange resources must be private."]
```

## Example custom organization policies for common use cases

This table provides syntax examples for some common custom constraints.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Description</th>
<th>Constraint syntax</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       DataExchange      </code> resources can't be publicly discoverable.</td>
<td><pre class="text" dir="ltr" data-is-upgraded="" data-syntax="YAML" translate="no"><code>    name: organizations/ORGANIZATION_ID/customConstraints/custom.enforceDataExchangeDiscovery
    resource_types: analyticshub.googleapis.com/DataExchange
    method_types:
      - CREATE
      - UPDATE
    condition: resource.discoveryType == &#39;DISCOVERY_TYPE_PUBLIC&#39;
    action_type: DENY
    display_name: Reject public DataExchanges.
    description: All DataExchange resources must be private.
    </code></pre></td>
</tr>
<tr class="even">
<td>Only allow creating a <code dir="ltr" translate="no">       DataExchange      </code> resource in a data clean room (DCR).</td>
<td><pre class="text" dir="ltr" data-is-upgraded="" data-syntax="YAML" translate="no"><code>    name:
      organizations/ORGANIZATION_ID/customConstraints/custom.analyticsHubAllowDCRDataExchange
    resource_types: analyticshub.googleapis.com/DataExchange
    method_types:
      - CREATE
    condition: has(resource.sharingEnvironmentConfig.dcrExchangeConfig)
    action_type: ALLOW
    display_name: Allow a DataExchange in a DCR.
    description: Only allow the creation of a DataExchange resource in a DCR.
    </code></pre></td>
</tr>
<tr class="odd">
<td>Only allow a <code dir="ltr" translate="no">       DataExchange      </code> resource with subscriber email logging enabled.</td>
<td><pre class="text" dir="ltr" data-is-upgraded="" data-syntax="YAML" translate="no"><code>    name: organizations/ORGANIZATION_ID/customConstraints/custom.subscriberEmailLoggingAllowed
    resource_types: analyticshub.googleapis.com/DataExchange
    method_types:
      - CREATE
      - UPDATE
    condition: resource.logLinkedDatasetQueryUserEmail == true
    action_type: ALLOW
    display_name: Subscriber email logging must be enabled.
    description: Subscriber email logging must be enabled for DataExchange resources.
    </code></pre></td>
</tr>
<tr class="even">
<td>The <code dir="ltr" translate="no">       Listing      </code> resource can't be publicly discoverable.</td>
<td><pre class="text" dir="ltr" data-is-upgraded="" data-syntax="YAML" translate="no"><code>    name: organizations/ORGANIZATION_ID/customConstraints/custom.noPublicListing
    resource_types: analyticshub.googleapis.com/Listing
    method_types:
      - CREATE
      - UPDATE
    condition: resource.discoveryType == &#39;DISCOVERY_TYPE_PUBLIC&#39;
    action_type: DENY
    display_name: Reject public Listings.
    description: All Listing resources must be undiscoverable.
    </code></pre></td>
</tr>
<tr class="odd">
<td>The <code dir="ltr" translate="no">       Listing      </code> resource must refer to a BigQuery dataset.</td>
<td><pre class="text" dir="ltr" data-is-upgraded="" data-syntax="YAML" translate="no"><code>    name: organizations/ORGANIZATION_ID/customConstraints/custom.listingWithBQDataset
    resource_types: analyticshub.googleapis.com/Listing
    method_types:
      - CREATE
      - UPDATE
    condition: has(resource.bigqueryDataset) &amp;&amp; resource.bigqueryDataset.dataset.contains(&#39;test&#39;)
    action_type: ALLOW
    display_name: Listing must have a BigQuery dataset.
    description: Listing must have a BigQuery dataset whose name contains the string &quot;test&quot;.
    </code></pre></td>
</tr>
<tr class="even">
<td>The <code dir="ltr" translate="no">       Listing      </code> resource must have the <code dir="ltr" translate="no">       restrictedExportPolicy      </code> object enabled.</td>
<td><pre class="text" dir="ltr" data-is-upgraded="" data-syntax="YAML" translate="no"><code>    name: organizations/ORGANIZATION_ID/customConstraints/custom.listingWithRestrictedExportPolicy
    resource_types: analyticshub.googleapis.com/Listing
    method_types:
      - CREATE
      - UPDATE
    condition: has(resource.bigqueryDataset) &amp;&amp; has(resource.bigqueryDataset.restrictedExportPolicy) &amp;&amp; resource.bigqueryDataset.restrictedExportPolicy.enabled == true
    action_type: DENY
    display_name: The Listing must have restricted export policy.
    description: The Listing resource must have restrictedExportPolicy enabled to allow egress controls.
    </code></pre></td>
</tr>
</tbody>
</table>

## BigQuery sharing supported resources

The following table lists the BigQuery sharing resources that you can reference in custom constraints.

Resource

Field

analyticshub.googleapis.com/DataExchange

`  resource.description  `

`  resource.discoveryType  `

`  resource.displayName  `

`  resource.documentation  `

`  resource.icon  `

`  resource.logLinkedDatasetQueryUserEmail  `

`  resource.primaryContact  `

analyticshub.googleapis.com/Listing

`  resource.allowOnlyMetadataSharing  `

`  resource.bigqueryDataset.dataset  `

`  resource.bigqueryDataset.replicaLocations  `

`  resource.bigqueryDataset.restrictedExportPolicy.enabled  `

`  resource.bigqueryDataset.restrictedExportPolicy.restrictDirectTableAccess  `

`  resource.bigqueryDataset.restrictedExportPolicy.restrictQueryResult  `

`  resource.bigqueryDataset.selectedResources.routine  `

`  resource.bigqueryDataset.selectedResources.table  `

`  resource.categories  `

`  resource.dataProvider.name  `

`  resource.dataProvider.primaryContact  `

`  resource.description  `

`  resource.discoveryType  `

`  resource.displayName  `

`  resource.documentation  `

`  resource.icon  `

`  resource.logLinkedDatasetQueryUserEmail  `

`  resource.primaryContact  `

`  resource.publisher.name  `

`  resource.publisher.primaryContact  `

`  resource.pubsubTopic.dataAffinityRegions  `

`  resource.pubsubTopic.topic  `

`  resource.requestAccess  `

`  resource.restrictedExportConfig.enabled  `

`  resource.restrictedExportConfig.restrictQueryResult  `

## What's next

  - Learn more about [custom constraints](/resource-manager/docs/organization-policy/creating-managing-custom-constraints) .
  - Learn more about [Organization Policy Service](/resource-manager/docs/organization-policy/overview) .
  - Learn more about how to [create and manage organization policies](/resource-manager/docs/organization-policy/using-constraints) .
  - See the full list of managed [organization policy constraints](/resource-manager/docs/organization-policy/org-policy-constraints) .
