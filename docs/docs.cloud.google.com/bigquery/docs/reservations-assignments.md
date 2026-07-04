---
name: documents/docs.cloud.google.com/bigquery/docs/reservations-assignments
uri: https://docs.cloud.google.com/bigquery/docs/reservations-assignments
title: Manage workload assignments
description: Learn how to work with capacity commitments, reservations, and assignments in BigQuery. It includes tasks such as purchasing and deleting commitments; and creating, assigning, and deleting reservations.
data_source: docs.cloud.google.com
---

# Manage workload assignments

The BigQuery Reservation API lets you purchase dedicated slots (called [*commitments*](https://docs.cloud.google.com/bigquery/docs/reservations-workload-management#slot_commitments) ), create pools of slots (called [*reservations*](https://docs.cloud.google.com/bigquery/docs/reservations-intro#reservations) ), and assign projects, folders, and organizations to those reservations.

> **Caution:** The assignee and the reservation must be in the same organization and in the same location. If you move the assignee to a different organization after the assignment is created, [reservations monitoring](https://docs.cloud.google.com/bigquery/docs/reservations-monitoring) will be inaccurate.

## Create reservation assignments

To use the slots that you purchase, you create an *assignment* which assigns a project, folder, organization, or principal to a slot reservation. You can't assign or allocate a specific number of slots at the assignment level; slots are managed and assigned at the reservation level.

### Assignment logic and criteria

Projects use the single most specific reservation in the resource hierarchy to which they are assigned. BigQuery uses the following evaluation logic to select the correct reservation:

1.  **Resource hierarchy priority:** BigQuery evaluates assignments based on the assignee resource ancestry (project \> folder \> organization). Folder and organization assignments aren't available to [standard edition](https://docs.cloud.google.com/bigquery/docs/editions-intro) reservations.

2.  **User-specific assignments using the `principal` property ( [Preview](https://cloud.google.com/products#product-launch-stages) ):** BigQuery reservation assignments support an optional `principal` property, which lets administrators route queries to specific reservations based on the identity of the user or service account executing the job. Within a specific assignee resource, an assignment with a matching principal takes priority over a generic assignment where the principal is unset.
    
    The default per-project limit of user-specific assignments is 10. For help changing the default limit, contact <bigquery-wlm-feedback@google.com> .
    
    > **Tip:** To ensure that a specific user is routed correctly despite a project-level generic assignment, create another user-specific assignment at that same project level.

To create an assignment on a reservation, the reservation must fulfill at least one of the following criteria:

  - It is configured with a non-zero amount of assigned baseline slots.

  - It is configured with a non-zero amount of autoscaling slots.

  - It is configured to use idle slots, and there are available idle slots within the project.

If you attempt to assign a resource to a reservation that doesn't meet at least one of these criteria, you receive the following message: `Assignment is pending, your project will be executed as on-demand.`

You can assign a resource to a [failover reservation](https://docs.cloud.google.com/bigquery/docs/managed-disaster-recovery) , but the assignment pends in the secondary location.

### Required permissions

To create a reservation assignment, you need the following Identity and Access Management (IAM) permission:

  - `bigquery.reservationAssignments.create` on the [administration project](https://docs.cloud.google.com/bigquery/docs/reservations-workload-management#admin-project) and the assignee.

Each of the following predefined IAM roles includes this permission:

  - `BigQuery Admin`
  - `BigQuery Resource Admin`
  - `BigQuery Resource Editor`

For more information about IAM roles in BigQuery, see [Predefined roles and permissions](https://docs.cloud.google.com/bigquery/docs/access-control) .

### Assign an organization to a reservation

### Console

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the navigation menu, click **Workload management** .

3.  Click the **Reservations** tab.

4.  Find the reservation in the table of reservations.

5.  Expand the more\_vert **Actions** option.

6.  Click **Create assignment** .

7.  In the **Create an assignment** section, click **Browse** .

8.  Browse or search for the organization and select it.

9.  In the **Job Type** section, select a job type to assign for this reservation. Options include the following:
    
      - `QUERY`
      - `CONTINUOUS`
      - `PIPELINE`
      - `BACKGROUND`
      - `ML_EXTERNAL`
    
    For more information about job types, see [Reservation assignments](https://docs.cloud.google.com/bigquery/docs/reservations-workload-management#assignments) . This default value is `QUERY` .
    
    To learn more about allowing users to use Gemini in BigQuery with Enterprise Plus edition assignments, see [Setup Gemini in BigQuery](https://docs.cloud.google.com/bigquery/docs/gemini-set-up) .

10. Optional: In the **User** field, enter the email address of the user, service account, or third-party identity.

11. Click **Create** .

### SQL

To assign an organization to a reservation, use the [`CREATE ASSIGNMENT` DDL statement](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_assignment_statement) .

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
        CREATE ASSIGNMENT
          `ADMIN_PROJECT_ID.region-LOCATION.RESERVATION_NAME.ASSIGNMENT_ID`
        OPTIONS (
          assignee = 'organizations/ORGANIZATION_ID',
          job_type = 'JOB_TYPE',
          principal = 'PRINCIPAL');
    
    Replace the following:
    
      - `  ADMIN_PROJECT_ID  ` : the project ID of the [administration project](https://docs.cloud.google.com/bigquery/docs/reservations-workload-management#admin-project) that owns the reservation resource
    
      - `  LOCATION  ` : the [location](https://docs.cloud.google.com/bigquery/docs/locations) of the reservation
    
      - `  RESERVATION_NAME  ` : the name of the reservation
    
      - `  ASSIGNMENT_ID  ` : the ID of the assignment
        
        The ID must be unique to the project and location, start and end with a lowercase letter or a number, and contain only lowercase letters, numbers, and dashes.
    
      - `  ORGANIZATION_ID  ` : the [organization ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-organization#retrieving_your_organization_id)
    
      - `  JOB_TYPE  ` : the [type of job](https://docs.cloud.google.com/bigquery/docs/reservations-workload-management#assignments) to assign to this reservation, such as `QUERY` , `CONTINUOUS` , `PIPELINE` , `BACKGROUND` , or `ML_EXTERNAL`
    
      - Optional: `  PRINCIPAL  ` : the identity format specifying the user, service account, or third-party identity
        
        The `principal` field supports only the following [IAM Principal identifier](https://docs.cloud.google.com/iam/docs/principal-identifiers) formats:
        
          - Google Account
          - Service account
          - Single identity in a workforce identity pool
          - Single identity in a workload identity pool

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](https://docs.cloud.google.com/bigquery/docs/running-queries#queries) .

### bq

To assign an organization's jobs to a reservation, use the `bq mk` command with the `--reservation_assignment` flag:

    bq mk \
        --project_id=ADMIN_PROJECT_ID \
        --location=LOCATION \
        --reservation_assignment \
        --reservation_id=RESERVATION_NAME \
        --assignee_type=ORGANIZATION \
        --assignee_id=ORGANIZATION_ID \
        --job_type=JOB_TYPE \
        --principal=PRINCIPAL

Replace the following:

  - `  ADMIN_PROJECT_ID  ` : the project ID of the [administration project](https://docs.cloud.google.com/bigquery/docs/reservations-workload-management#admin-project) that owns the reservation resource

  - `  LOCATION  ` : the [location](https://docs.cloud.google.com/bigquery/docs/locations) of the reservation

  - `  RESERVATION_NAME  ` : the name of the reservation

  - `  ORGANIZATION_ID  ` : the [organization ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-organization#retrieving_your_organization_id)

  - `  JOB_TYPE  ` : the [type of job](https://docs.cloud.google.com/bigquery/docs/reservations-workload-management#assignments) to assign to this reservation, such as `QUERY` , `CONTINUOUS` , `PIPELINE` , `BACKGROUND` , or `ML_EXTERNAL`

  - Optional: `  PRINCIPAL  ` : the identity format specifying the user, service account, or third-party identity.
    
    The `--principal` flag supports only the following [IAM principal identifier](https://docs.cloud.google.com/iam/docs/principal-identifiers) formats:
    
      - Google Account
      - Service account
      - Single identity in a workforce identity pool
      - Single identity in a workload identity pool

When you create a reservation assignment, wait at least 5 minutes before running a query. Otherwise the query might be billed using on-demand pricing.

### Configure project caps and scheduling policy overrides

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

To request support or provide feedback for this feature, contact <bigquery-wlm-feedback@google.com> .

You can create project caps, which are a type of assignment rule, to configure project-specific overrides for a reservation's default [scheduling policies](https://docs.cloud.google.com/bigquery/docs/reservations-workload-management#scheduling-policies) . For example, you can limit the slot consumption and the number of concurrent queries for the project.

Unlike other kinds of reservation assignments that determine which reservation a project uses, project caps are assignment resources that control only the scheduling behavior for a specific project.

When you create a project cap, the following limitations apply:

  - The *assignee* must be a Google Cloud project. Folders and organizations aren't supported.
  - The *job type* must be unset or explicitly set to `JOB_TYPE_UNSPECIFIED` .
  - Changes to the `max_slots` policy value require a new query to start before the update takes effect.

To create project caps through these scheduling policy assignments, select one of the following options:

### Console

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the navigation menu, go to **Administration \> Workload management** .

3.  Click the **Assignment rules** tab.

4.  Click **Create assignment rule** .

5.  In the **Rule type** list, select **Project cap** .

6.  In the **Select a project** list, select a project, and then click **Continue** .

7.  In the **Reservation** list, select a reservation, and then click **Continue** .

8.  In the **Project override** section, enter values in the **Max slots** and **Max concurrency** fields.

9.  Click **Create** .

### SQL

To create a project scheduling policy assignment, use the `CREATE ASSIGNMENT` DDL statement with the `scheduling_policy_max_slots` and `scheduling_policy_concurrency` options.

    CREATE ASSIGNMENT
      `ADMIN_PROJECT_ID.region-LOCATION.RESERVATION_NAME.ASSIGNMENT_ID`
    OPTIONS (
      assignee = 'projects/PROJECT_ID',
      scheduling_policy_max_slots = MAX_SLOTS,
      scheduling_policy_concurrency = MAX_CONCURRENCY);

Replace the following:

  - `  ADMIN_PROJECT_ID  ` : the project ID of the [administration project](https://docs.cloud.google.com/bigquery/docs/reservations-workload-management#admin-project) that owns the reservation resource
  - `  LOCATION  ` : the [location](https://docs.cloud.google.com/bigquery/docs/locations) of the reservation
  - `  RESERVATION_NAME  ` : the name of the reservation
  - `  ASSIGNMENT_ID  ` : the ID of the assignment
  - `  PROJECT_ID  ` : the Google Cloud project identifier being assigned
  - `  MAX_SLOTS  ` : the maximum limit on the slot consumption of queries running in the project
  - `  MAX_CONCURRENCY  ` : the upper bound on the number of simultaneous queries admitted for the project

### bq

To create a scheduling policy assignment using the `bq` command-line tool, use the `bq mk` command with the `--scheduling_policy_max_slots` and `--scheduling_policy_concurrency` flags.

    bq mk \
        --project_id=ADMIN_PROJECT_ID \
        --location=LOCATION \
        --reservation_assignment \
        --reservation_id=RESERVATION_NAME \
        --assignee_id=PROJECT_ID \
        --assignee_type=PROJECT \
        --scheduling_policy_max_slots=MAX_SLOTS \
        --scheduling_policy_concurrency=MAX_CONCURRENCY

Replace the following:

  - `  ADMIN_PROJECT_ID  ` : the project ID of the [administration project](https://docs.cloud.google.com/bigquery/docs/reservations-workload-management#admin-project) that owns the reservation resource
  - `  LOCATION  ` : the [location](https://docs.cloud.google.com/bigquery/docs/locations) of the reservation
  - `  RESERVATION_NAME  ` : the name of the reservation
  - `  PROJECT_ID  ` : the Google Cloud project identifier being assigned
  - `  MAX_SLOTS  ` : the maximum limit on the slot consumption of queries running in the project
  - `  MAX_CONCURRENCY  ` : the upper bound on the number of simultaneous queries admitted for the project

To modify or remove an existing scheduling policy assignment, use the `ALTER ASSIGNMENT` DDL statement:

``` 
ALTER ASSIGNMENT
  `ADMIN_PROJECT_ID.region-LOCATION.RESERVATION_NAME.ASSIGNMENT_ID`
SET OPTIONS (
  scheduling_policy_max_slots = NEW_MAX_SLOTS,
  scheduling_policy_concurrency = NEW_MAX_CONCURRENCY);
-- To remove a scheduling policy setting, set its values to null. To all
   settings, delete the assignment.
   
```

Replace the following:

  - `  ADMIN_PROJECT_ID  ` : the project ID of the [administration project](https://docs.cloud.google.com/bigquery/docs/reservations-workload-management#admin-project) that owns the reservation resource
  - `  LOCATION  ` : the [location](https://docs.cloud.google.com/bigquery/docs/locations) of the reservation
  - `  RESERVATION_NAME  ` : the name of the reservation
  - `  ASSIGNMENT_ID  ` : the ID of the assignment
  - `  NEW_MAX_SLOTS  ` : the maximum limit on the slot consumption of queries running in the project
  - `  NEW_MAX_CONCURRENCY  ` : the upper bound on the number of simultaneous queries admitted for the project

To view active scheduling policy overrides, check the `scheduling_policy` and `assignment_type` columns in the `INFORMATION_SCHEMA.ASSIGNMENTS` view.

### Assign a project or folder to a reservation

### Console

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the navigation menu, click **Workload management** .

3.  Click the **Reservations** tab.

4.  Find the reservation in the table of reservations.

5.  Expand the more\_vert **Actions** option.

6.  Click **Create assignment** .

7.  In the **Create an assignment** section, click **Browse** .

8.  Browse or search for the project or folder and select it.

9.  In the **Job Type** section, select a job type to assign for this reservation. Options include the following:
    
      - `QUERY`
      - `CONTINUOUS`
      - `PIPELINE`
      - `BACKGROUND`
      - `ML_EXTERNAL`
    
    Creation and modification of more granular background job types such as `BACKGROUND_COLUMN_METADATA_INDEX` are not yet supported through the console.
    
    For more information about job types, see [reservation assignments](https://docs.cloud.google.com/bigquery/docs/reservations-workload-management#assignments) . This default value is `QUERY` .

10. Optional: In the **User** field, enter the email address of the user, service account, or third-party identity.

11. Click **Create** .

### SQL

To assign a project to a reservation, use the [`CREATE ASSIGNMENT` DDL statement](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_assignment_statement) .

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
        CREATE ASSIGNMENT
          `ADMIN_PROJECT_ID.region-LOCATION.RESERVATION_NAME.ASSIGNMENT_ID`
        OPTIONS(
          assignee="projects/PROJECT_ID",
          job_type="JOB_TYPE",
          principal="PRINCIPAL");
    
    Replace the following:
    
      - `  ADMIN_PROJECT_ID  ` : the project ID of the [administration project](https://docs.cloud.google.com/bigquery/docs/reservations-workload-management#admin-project) that owns the reservation resource
    
      - `  LOCATION  ` : the [location](https://docs.cloud.google.com/bigquery/docs/locations) of the reservation
    
      - `  RESERVATION_NAME  ` : the name of the reservation
    
      - `  ASSIGNMENT_ID  ` : the ID of the assignment
        
        The ID must be unique to the project and location, start and end with a lowercase letter or a number, and contain only lowercase letters, numbers, and dashes.
    
      - `  PROJECT_ID  ` : the ID of the project to assign to the reservation
    
      - `  JOB_TYPE  ` : the [type of job](https://docs.cloud.google.com/bigquery/docs/reservations-workload-management#assignments) to assign to this reservation, such as `QUERY` , `CONTINUOUS` , `PIPELINE` , `BACKGROUND_CHANGE_DATA_CAPTURE` , `BACKGROUND_COLUMN_METADATA_INDEX` , `BACKGROUND_SEARCH_INDEX_REFRESH` , `BACKGROUND` , or `ML_EXTERNAL`
    
      - Optional: `  PRINCIPAL  ` : the identity format specifying the user, service account, or third-party identity. The `principal` field supports only the following [IAM principal identifier](https://docs.cloud.google.com/iam/docs/principal-identifiers) formats:
        
          - Google Account
          - Service account
          - Single identity in a workforce identity pool
          - Single identity in a workload identity pool

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](https://docs.cloud.google.com/bigquery/docs/running-queries#queries) .

### bq

To assign jobs to a reservation, use the `bq mk` command with the `--reservation_assignment` flag:

    bq mk \
        --project_id=ADMIN_PROJECT_ID \
        --location=LOCATION \
        --reservation_assignment \
        --reservation_id=RESERVATION_NAME \
        --assignee_type=PROJECT \
        --assignee_id=PROJECT_ID \
        --job_type=JOB_TYPE \
        --principal=PRINCIPAL

Replace the following:

  - `  ADMIN_PROJECT_ID  ` : the project ID of the [administration project](https://docs.cloud.google.com/bigquery/docs/reservations-workload-management#admin-project) that owns the reservation resource

  - `  LOCATION  ` : the [location](https://docs.cloud.google.com/bigquery/docs/locations) of the reservation

  - `  RESERVATION_NAME  ` : the name of the reservation

  - `  PROJECT_ID  ` : the ID of the project to assign to this reservation

  - `  JOB_TYPE  ` : the [type of job](https://docs.cloud.google.com/bigquery/docs/reservations-workload-management#assignments) to assign to this reservation, such as `QUERY` , `CONTINUOUS` , `PIPELINE` , `BACKGROUND_CHANGE_DATA_CAPTURE` , `BACKGROUND_COLUMN_METADATA_INDEX` , `BACKGROUND_SEARCH_INDEX_REFRESH` , `BACKGROUND` , or `ML_EXTERNAL`

  - Optional: `  PRINCIPAL  ` : the identity format specifying the user, service account, or third-party identity.
    
    The `--principal` flag supports only the following [IAM principal identifier](https://docs.cloud.google.com/iam/docs/principal-identifiers) formats:
    
      - Google Account
      - Service account
      - Single identity in a workforce identity pool
      - Single identity in a workload identity pool

### Terraform

Use the [`google_bigquery_reservation_assignment`](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/bigquery_reservation_assignment) resource.

> **Note:** To create BigQuery objects using Terraform, you must enable the [Cloud Resource Manager API](https://docs.cloud.google.com/resource-manager/reference/rest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](https://docs.cloud.google.com/bigquery/docs/authentication#client-libs) .

The following example assigns a project to the reservation named `my-reservation` :

```terraform
resource "google_bigquery_reservation" "default" {
  name              = "my-reservation"
  location          = "us-central1"
  slot_capacity     = 100
  edition           = "ENTERPRISE"
  ignore_idle_slots = false # Use idle slots from other reservations
  concurrency       = 0     # Automatically adjust query concurrency based on available resources
  autoscale {
    max_slots = 200 # Allow the reservation to scale up to 300 slots (slot_capacity + max_slots) if needed
  }
}

data "google_project" "project" {}

resource "google_bigquery_reservation_assignment" "default" {
  assignee    = "projects/${data.google_project.project.project_id}"
  job_type    = "QUERY"
  reservation = google_bigquery_reservation.default.id
}
```

To apply your Terraform configuration in a Google Cloud project, complete the steps in the following sections.

## Prepare Cloud Shell

1.  Launch [Cloud Shell](https://shell.cloud.google.com/) .

2.  Set the default Google Cloud project where you want to apply your Terraform configurations.
    
    You only need to run this command once per project, and you can run it in any directory.
    
        export GOOGLE_CLOUD_PROJECT=PROJECT_ID
    
    Environment variables are overridden if you set explicit values in the Terraform configuration file.

## Prepare the directory

Each Terraform configuration file must have its own directory (also called a *root module* ).

1.  In [Cloud Shell](https://shell.cloud.google.com/) , create a directory and a new file within that directory. The filename must have the `.tf` extension—for example `main.tf` . In this tutorial, the file is referred to as `main.tf` .
    
        mkdir DIRECTORY && cd DIRECTORY && touch main.tf

2.  If you are following a tutorial, you can copy the sample code in each section or step.
    
    Copy the sample code into the newly created `main.tf` .
    
    Optionally, copy the code from GitHub. This is recommended when the Terraform snippet is part of an end-to-end solution.

3.  Review and modify the sample parameters to apply to your environment.

4.  Save your changes.

5.  Initialize Terraform. You only need to do this once per directory.
    
        terraform init
    
    Optionally, to use the latest Google provider version, include the `-upgrade` option:
    
        terraform init -upgrade

## Apply the changes

1.  Review the configuration and verify that the resources that Terraform is going to create or update match your expectations:
    
        terraform plan
    
    Make corrections to the configuration as necessary.

2.  Apply the Terraform configuration by running the following command and entering `yes` at the prompt:
    
        terraform apply
    
    Wait until Terraform displays the "Apply complete\!" message.

3.  [Open your Google Cloud project](https://console.cloud.google.com/) to view the results. In the Google Cloud console, navigate to your resources in the UI to make sure that Terraform has created or updated them.

> **Note:** Terraform samples typically assume that the required APIs are enabled in your Google Cloud project.

When you create a reservation assignment, wait at least 5 minutes before running a query. Otherwise the query might be billed using on-demand pricing.

To make a project that only uses [idle slots](https://docs.cloud.google.com/bigquery/docs/slots#idle_slots) , [create a reservation](https://docs.cloud.google.com/bigquery/docs/reservations-tasks#create_reservations) with `0` slots assigned to it, then follow the prior steps to assign the project to that reservation.

> **Note:** A project can be assigned to at most one reservation in a single region.

### User-specific assignments

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

You can assign a reservation to a specific principal such as a user or service account within a project, folder, or organization. This is useful for routing specific users' workloads to dedicated reservations.

When resolving which reservation to use for a job, BigQuery evaluates assignments in the following order:

1.  Evaluate the resource hierarchy, starting with the project, then parent folders, and then the organization.
2.  At each level of the hierarchy, BigQuery first checks for an assignment that matches the specific principal that is running the job.
3.  If no assignment matches the principal at that level, check for a general assignment without a principal at the same level.
4.  If no assignment is found, move to the next level in the hierarchy.

A project-level assignment without a principal overrides a folder-level assignment with a principal.

#### Supported principal formats

The `principal` option supports the following [IAM v2 principal](https://docs.cloud.google.com/iam/docs/principal-identifiers) formats:

| Identity type                      | Principal format                                                                                                                                                               |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Users                              | ` principal://goog/subject/         EMAIL_ADDRESS        `                                                                                                                     |
| Service accounts                   | ` principal://iam.googleapis.com/projects/-/serviceAccounts/         EMAIL_ADDRESS        `                                                                                    |
| Workforce identity pool identities | ` principal://iam.googleapis.com/locations/global/workforcePools/         POOL_ID        /subject/         SUBJECT_ID        `                                                 |
| Workload identity pool identities  | ` principal://iam.googleapis.com/projects/         PROJECT_NUMBER        /locations/global/workloadIdentityPools/         POOL_ID        /subject/         SUBJECT_ID        ` |

> **Note:** The value `unknown_or_deleted_user` is a sentinel value used by the system to represent a deleted or disabled user account. You can't assign reservations using this value.

#### Assign a principal to a reservation

### SQL

To create a user-specific assignment, use the `CREATE ASSIGNMENT` DDL statement with the `principal` option.

    CREATE ASSIGNMENT
      `ADMIN_PROJECT_ID.region-LOCATION.RESERVATION_NAME.ASSIGNMENT_ID`
    OPTIONS (
      assignee = 'projects/PROJECT_ID',
      principal = 'principal://goog/subject/EMAIL_ADDRESS',
      job_type = 'QUERY');

Replace the following:

  - `  ADMIN_PROJECT_ID  ` : the project ID of the [administration project](https://docs.cloud.google.com/bigquery/docs/reservations-workload-management#admin-project) that owns the reservation resource
  - `  LOCATION  ` : the [location](https://docs.cloud.google.com/bigquery/docs/locations) of the reservation
  - `  RESERVATION_NAME  ` : the name of the reservation
  - `  ASSIGNMENT_ID  ` : the assignment ID
  - `  PROJECT_ID  ` : the project ID
  - \` EMAIL\_ADDRESS : the user's email address
  - `  JOB_TYPE  ` : the [type of job](https://docs.cloud.google.com/bigquery/docs/reservations-workload-management#assignments) to assign to this reservation, such as `QUERY` , `CONTINUOUS` , `PIPELINE` , `BACKGROUND` , or `ML_EXTERNAL`

### bq

To create a user-specific assignment, use the `bq mk` command with the `--principal` flag:

    bq mk \
        --project_id=ADMIN_PROJECT_ID \
        --location=LOCATION \
        --reservation_assignment \
        --reservation_id=RESERVATION_NAME \
        --assignee_id=PROJECT_ID \
        --assignee_type=PROJECT \
        --principal=PRINCIPAL \
        --job_type=JOB_TYPE

Replace the following:

  - `  ADMIN_PROJECT_ID  ` : the project ID of the [administration project](https://docs.cloud.google.com/bigquery/docs/reservations-workload-management#admin-project) that owns the reservation resource
  - `  LOCATION  ` : the [location](https://docs.cloud.google.com/bigquery/docs/locations) of the reservation
  - `  RESERVATION_NAME  ` : the name of the reservation
  - `  ASSIGNMENT_ID  ` : the assignment ID
  - `  PROJECT_ID  ` : the project ID
  - `  PRINCIPAL: the principal identifier, for example,  ` principal://goog/subject/ EMAIL\_ADDRESS \`
  - `  JOB_TYPE  ` : the [type of job](https://docs.cloud.google.com/bigquery/docs/reservations-workload-management#assignments) to assign to this reservation, such as `QUERY` , `CONTINUOUS` , `PIPELINE` , `BACKGROUND` , or `ML_EXTERNAL`

### Assign a project to `none`

Assignments to `none` represent the absence of an assignment. Projects assigned to `none` use on-demand pricing.

> **Note:** Assignments to `none` are supported for QUERY jobs only.

### SQL

To assign a project to `none` , use the [`CREATE ASSIGNMENT` DDL statement](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_assignment_statement) .

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
        CREATE ASSIGNMENT
          `ADMIN_PROJECT_ID.region-LOCATION.none.ASSIGNMENT_ID`
        OPTIONS(
          assignee="projects/PROJECT_ID",
          job_type="QUERY");
    
    Replace the following:
    
      - `  LOCATION  ` : the [location](https://docs.cloud.google.com/bigquery/docs/locations) of jobs that should use on-demand pricing
    
      - `  ASSIGNMENT_ID  ` : the ID of the assignment
        
        The ID must be unique to the project and location, start and end with a lowercase letter or a number, and contain only lowercase letters, numbers, and dashes.
    
      - `  PROJECT_ID  ` : the ID of the project to assign to the reservation

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](https://docs.cloud.google.com/bigquery/docs/running-queries#queries) .

### bq

To assign a project to `none` , use the `bq mk` command with the `--reservation_assignment` flag:

    bq mk \
        --project_id=ADMIN_PROJECT_ID \
        --location=LOCATION \
        --reservation_assignment \
        --reservation_id=none \
        --job_type=QUERY \
        --assignee_id=PROJECT_ID \
        --assignee_type=PROJECT

Replace the following:

  - `  ADMIN_PROJECT_ID  ` : the project ID of the [administration project](https://docs.cloud.google.com/bigquery/docs/reservations-workload-management#admin-project) that owns the reservation resource
  - `  LOCATION  ` : the [location](https://docs.cloud.google.com/bigquery/docs/locations) of jobs that should use on-demand pricing
  - `  PROJECT_ID  ` : the ID of the project to assign to `none`

### Terraform

Use the [`google_bigquery_reservation_assignment`](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/bigquery_reservation_assignment) resource.

> **Note:** To create BigQuery objects using Terraform, you must enable the [Cloud Resource Manager API](https://docs.cloud.google.com/resource-manager/reference/rest) .

To authenticate to BigQuery, set up Application Default Credentials. For more information, see [Set up authentication for client libraries](https://docs.cloud.google.com/bigquery/docs/authentication#client-libs) .

The following example assigns a project to `none` :

```terraform
data "google_project" "project" {}

resource "google_bigquery_reservation_assignment" "default" {
  assignee    = "projects/${data.google_project.project.project_id}"
  job_type    = "QUERY"
  reservation = "projects/${data.google_project.project.project_id}/locations/us/reservations/none"
}
```

To apply your Terraform configuration in a Google Cloud project, complete the steps in the following sections.

## Prepare Cloud Shell

1.  Launch [Cloud Shell](https://shell.cloud.google.com/) .

2.  Set the default Google Cloud project where you want to apply your Terraform configurations.
    
    You only need to run this command once per project, and you can run it in any directory.
    
        export GOOGLE_CLOUD_PROJECT=PROJECT_ID
    
    Environment variables are overridden if you set explicit values in the Terraform configuration file.

## Prepare the directory

Each Terraform configuration file must have its own directory (also called a *root module* ).

1.  In [Cloud Shell](https://shell.cloud.google.com/) , create a directory and a new file within that directory. The filename must have the `.tf` extension—for example `main.tf` . In this tutorial, the file is referred to as `main.tf` .
    
        mkdir DIRECTORY && cd DIRECTORY && touch main.tf

2.  If you are following a tutorial, you can copy the sample code in each section or step.
    
    Copy the sample code into the newly created `main.tf` .
    
    Optionally, copy the code from GitHub. This is recommended when the Terraform snippet is part of an end-to-end solution.

3.  Review and modify the sample parameters to apply to your environment.

4.  Save your changes.

5.  Initialize Terraform. You only need to do this once per directory.
    
        terraform init
    
    Optionally, to use the latest Google provider version, include the `-upgrade` option:
    
        terraform init -upgrade

## Apply the changes

1.  Review the configuration and verify that the resources that Terraform is going to create or update match your expectations:
    
        terraform plan
    
    Make corrections to the configuration as necessary.

2.  Apply the Terraform configuration by running the following command and entering `yes` at the prompt:
    
        terraform apply
    
    Wait until Terraform displays the "Apply complete\!" message.

3.  [Open your Google Cloud project](https://console.cloud.google.com/) to view the results. In the Google Cloud console, navigate to your resources in the UI to make sure that Terraform has created or updated them.

> **Note:** Terraform samples typically assume that the required APIs are enabled in your Google Cloud project.

If there are no reservations in the administration project, then you must use the bq command-line tool to view projects assigned to `none` .

### Override a reservation on a query

To use a specific reservation in a query, you need the following Identity and Access Management (IAM) permission:

  - `bigquery.reservations.use` on the reservation or its [administration project](https://docs.cloud.google.com/bigquery/docs/reservations-workload-management#admin-project) .

To assign a query to run in a specific reservation, do one of the following:

### Console

1.  Go to the **BigQuery** page.

2.  Click add\_box **SQL query** .

3.  In the query editor, enter a valid GoogleSQL query.

4.  Click **Edit** \> **Query settings** .

5.  Clear the **Automatic location setting** checkbox, and then select the region or multi-region the reservation is in.

6.  In the **Reservation** list, select the reservation you want the query to run in.

7.  Click **Save** .

8.  [Write a query in the editor tab and run it](https://docs.cloud.google.com/bigquery/docs/running-queries) . The query runs in the reservation you specified.

### SQL

Set the `@@reservation` system variable in the session to assign the reservation your query runs in:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
        SET @@reservation='RESERVATION';
        SELECT QUERY;
    
    Replace the following:
    
      - `  RESERVATION  ` : the reservation you want the query to run in.
    
      - `  QUERY  ` : the query you want to run.

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](https://docs.cloud.google.com/bigquery/docs/running-queries#queries) .

For example, the following query uses the [`SET`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/procedural-language#set) statement to set the reservation to the `test-reservation` in the `US` multi-region, then calls a basic query:

    SET @@reservation='projects/project1/locations/US/reservations/test-reservation';
    SELECT 42;

### bq

1.  In the Google Cloud console, activate Cloud Shell.
    
    At the bottom of the Google Cloud console, a [Cloud Shell](https://docs.cloud.google.com/shell/docs/how-cloud-shell-works) session starts and displays a command-line prompt. Cloud Shell is a shell environment with the Google Cloud CLI already installed and with values already set for your current project. It can take a few seconds for the session to initialize.

2.  In Cloud Shell, run the query by using the [`bq query` command](https://docs.cloud.google.com/bigquery/docs/reference/bq-cli-reference#bq_query) with the `--reservation_id` flag:
    
        bq query --use_legacy_sql=false --reservation_id=RESERVATION_ID
        'QUERY'
    
    Replace the following:
    
      - `  RESERVATION_ID  ` : the reservation you want to run the query in.
    
      - `  QUERY  ` : the SQL statement for the query.
    
    For example, the following query runs in the `test-reservation` reservation in the `US` multi-region:
    
        bq query --reservation_id=project1.US:test-reservation 'SELECT 42;'

### API

To specify a reservation using the API, [insert a new job](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/jobs/insert) and populate the `query` job configuration property. Specify your reservation in the `reservation` field.

> **Caution:** A query can use a reservation declared in another project. However, the query and the reservation must be in the same organization and in the same location.

### Assign slots to BigQuery ML workloads

The following sections provide information on reservation assignment requirements for BigQuery ML models. You can create these reservation assignments by following the procedures in [Assign an organization to a reservation](https://docs.cloud.google.com/bigquery/docs/reservations-assignments#assign-organization) or [Assign a project or folder to a reservation](https://docs.cloud.google.com/bigquery/docs/reservations-assignments#assign_my_prod_project_to_prod_reservation) .

#### External models

The following BigQuery ML model types use external services:

  - [Autoencoder](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-autoencoder)
  - [AutoML](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-automl)
  - [Boosted tree](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-boosted-tree)
  - [Deep Neural Network (DNN)](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-dnn-models)
  - [Random forest](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-random-forest)
  - [Wide-and-Deep Network](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-create-wnd-models)

You can assign reserved slots to queries using these services by creating a reservation assignment that uses the `ML_EXTERNAL` job type. If no reservation assignment with an `ML_EXTERNAL` job type is found, the query job runs using [on-demand pricing](https://cloud.google.com/bigquery/pricing#on_demand_pricing) .

For external model training jobs, the slots in the reservation assignment are used for preprocessing, training, and postprocessing steps. During training, the slots aren't preemptible, but during preprocessing and postprocessing, idle slots can be used.

#### Matrix factorization models

To create a matrix factorization model you must [create a reservation](https://docs.cloud.google.com/bigquery/docs/reservations-tasks#create_reservations) that uses the BigQuery [Enterprise or Enterprise Plus edition](https://docs.cloud.google.com/bigquery/docs/editions-intro) , and then create a reservation assignment that uses the `QUERY` job type.

#### Other model types

For BigQuery ML models that aren't external models or matrix factorization models, you can assign reserved slots to queries using these services by creating a reservation assignment that uses the `QUERY` job type. If no reservation assignment with a `QUERY` job type is found, the query job runs using [on-demand pricing](https://cloud.google.com/bigquery/pricing#on_demand_pricing) .

## Find reservation assignments

### Required permissions

To search for a reservation assignment for a given project, folder, or organization, you need the following Identity and Access Management (IAM) permission:

  - `bigquery.reservationAssignments.list` on the administration project.

Each of the following predefined IAM roles includes this permission:

  - `BigQuery Admin`
  - `BigQuery Resource Admin`
  - `BigQuery Resource Editor`
  - `BigQuery Resource Viewer`
  - `BigQuery User`

For more information about IAM roles in BigQuery, see [Predefined roles and permissions](https://docs.cloud.google.com/bigquery/docs/access-control) .

### Find a project's reservation assignment

You can find out if your project, folder, or organization is assigned to a reservation by doing the following:

### Console

1.  In the Google Cloud console, go to the BigQuery page.

2.  In the navigation menu, click **Workload management** .

3.  Click the **Reservations** tab.

4.  In the table of reservations, expand a reservation to see what resources are assigned to that reservation, or use the **Filter** field to filter by resource name.

### SQL

To find which reservation your project's query jobs are assigned to, query the [`INFORMATION_SCHEMA.ASSIGNMENTS_BY_PROJECT` view](https://docs.cloud.google.com/bigquery/docs/information-schema-reservations#schema) .

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
    ``` 
      SELECT
        assignment_id
      FROM `region-LOCATION`.INFORMATION_SCHEMA.ASSIGNMENTS_BY_PROJECT
      WHERE
        assignee_id = 'PROJECT_ID'
        AND job_type = 'JOB_TYPE';
    ```
    
    Replace the following:
    
      - `  LOCATION  ` : the [location](https://docs.cloud.google.com/bigquery/docs/locations) of reservations to view
      - `  ADMIN_PROJECT_ID  ` : the project ID of the [administration project](https://docs.cloud.google.com/bigquery/docs/reservations-workload-management#admin-project) that owns the reservation resource
      - `  PROJECT_ID  ` : the ID of the project to assign to the reservation
      - `  JOB_TYPE  ` : the [type of job](https://docs.cloud.google.com/bigquery/docs/reservations-workload-management#assignments) to assign to this reservation, such as `QUERY` , `CONTINUOUS` , `PIPELINE` , `BACKGROUND` , or `ML_EXTERNAL`

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](https://docs.cloud.google.com/bigquery/docs/running-queries#queries) .

### bq

> **Caution:** This command does not work in Cloud Shell. To use this command, run it from a local command line.

To find which reservation your project's query jobs are assigned to, use the `bq show` command with the `--reservation_assignment` flag:

    bq show \
        --project_id=ADMIN_PROJECT_ID \
        --location=LOCATION \
        --reservation_assignment \
        --job_type=JOB_TYPE \
        --assignee_id=PROJECT_ID \
        --assignee_type=PROJECT

To find a user-specific assignment, include the `--principal` flag:

    bq show \
        --project_id=ADMIN_PROJECT_ID \
        --location=LOCATION \
        --reservation_assignment \
        --job_type=JOB_TYPE \
        --assignee_id=PROJECT_ID \
        --assignee_type=PROJECT \
        --principal=PRINCIPAL

Replace the following:

  - `  ADMIN_PROJECT_ID  ` : the ID of the project that owns the reservation resource
  - `  LOCATION  ` : the [location](https://docs.cloud.google.com/bigquery/docs/locations) of reservations to view
  - `  JOB_TYPE  ` : the [type of job](https://docs.cloud.google.com/bigquery/docs/reservations-workload-management#assignments) to assign to this reservation, such as `QUERY` , `CONTINUOUS` , `PIPELINE` , `BACKGROUND` , or `ML_EXTERNAL`
  - `  PROJECT_ID  ` : the ID of the project
  - `  PRINCIPAL  ` : the principal identifier, for example, ` principal://goog/subject/ EMAIL_ADDRESS  `

To view active user-specific assignment rules, check the `principal` column in the `INFORMATION_SCHEMA.ASSIGNMENTS` view or execute `bq ls --reservation_assignment` . Additionally, you can verify which reservation executed a specific job by querying the `INFORMATION_SCHEMA.JOBS` view. When using the `bq show --reservation_assignment` command, you can include the optional `--principal` flag to filter for a specific user assignment.

## Update reservation assignments

### Move an assignment to a different reservation

You can move an assignment from one reservation to another reservation.

To move a reservation assignment, you need the following Identity and Access Management (IAM) permissions on the [administration project](https://docs.cloud.google.com/bigquery/docs/reservations-workload-management#admin-project) and the assignee.

  - `bigquery.reservationAssignments.create`
  - `bigquery.reservationAssignments.delete`

Each of the following predefined IAM roles includes these permissions:

  - `BigQuery Admin`
  - `BigQuery Resource Admin`
  - `BigQuery Resource Editor`

For more information about IAM roles in BigQuery, see [Predefined roles and permissions](https://docs.cloud.google.com/bigquery/docs/access-control) .

To move an assignment, use the `bq update` command:

    bq update \
        --project_id=ADMIN_PROJECT_ID \
        --location=LOCATION \
        --reservation_assignment \
        --destination_reservation_id=DESTINATION_RESERVATION \
        ADMIN_PROJECT_ID:LOCATION.RESERVATION_NAME.ASSIGNMENT_ID

Replace the following:

  - `  ADMIN_PROJECT_ID  ` : the ID of the project that owns the reservation resource

  - `  LOCATION  ` : the [location](https://docs.cloud.google.com/bigquery/docs/locations) of the new reservation

  - `  RESERVATION_NAME  ` : the reservation to move the assignment from

  - `  DESTINATION_RESERVATION  ` : the reservation to move the assignment to

  - `  ASSIGNMENT_ID  ` : the ID of the assignment
    
    To get the assignment ID, see [List a project's reservation assignment](https://docs.cloud.google.com/bigquery/docs/reservations-assignments#list-assignment) .

> **Note:** Updated reservation assignments only apply to new jobs. Existing jobs continue to use their original reservation assignment.

## Delete reservation assignments

You can remove a project from a reservation by deleting the reservation assignment. If a project is not assigned to any reservations, it inherits any assignments in its parent folders or organizations, or else uses on-demand pricing if there are no parent assignments.

When you delete a reservation assignment, the jobs executing with slots from that reservation continue to run until completion.

### Required permissions

To delete a reservation assignment, you need the following Identity and Access Management (IAM) permission:

  - `bigquery.reservationAssignments.delete` on the [administration project](https://docs.cloud.google.com/bigquery/docs/reservations-workload-management#admin-project) and the assignee.

Each of the following predefined IAM roles includes this permission:

  - `BigQuery Admin`
  - `BigQuery Resource Admin`
  - `BigQuery Resource Editor`

### Remove a project from a reservation

To remove a project from a reservation:

### Console

1.  In the Google Cloud console, go to the BigQuery page.

2.  In the navigation menu, click **Workload management** .

3.  Click the **Reservations** tab.

4.  In the table of reservations, expand the reservation to find the project.

5.  Expand the more\_vert **Actions** option.

6.  Click **Delete** .

### SQL

Use the [`DROP ASSIGNMENT` DDL statement](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#drop_assignment_statement) .

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the query editor, enter the following statement:
    
        DROP ASSIGNMENT
          `ADMIN_PROJECT_ID.region-LOCATION.RESERVATION_NAME.ASSIGNMENT_ID`;
    
    Replace the following:
    
      - `  ADMIN_PROJECT_ID  ` : the project ID of the [administration project](https://docs.cloud.google.com/bigquery/docs/reservations-workload-management#admin-project) that owns the reservation resource
    
      - `  LOCATION  ` : the [location](https://docs.cloud.google.com/bigquery/docs/locations) of the reservation
    
      - `  RESERVATION_NAME  ` : the name of the reservation
    
      - `  ASSIGNMENT_ID  ` : the ID of the assignment
        
        To find the assignment ID, see [List a project's reservation assignment](https://docs.cloud.google.com/bigquery/docs/reservations-assignments#list-assignment) .

3.  Click play\_circle **Run** .

For more information about how to run queries, see [Run an interactive query](https://docs.cloud.google.com/bigquery/docs/running-queries#queries) .

### bq

To remove a project from a reservation, use the `bq rm` command with the `--reservation_assignment` flag:

    bq rm \
        --project_id=ADMIN_PROJECT_ID \
        --location=LOCATION \
        --reservation_assignment RESERVATION_NAME.ASSIGNMENT_ID

Replace the following:

  - `  ADMIN_PROJECT_ID  ` : the ID of the project that owns the reservation resource

  - `  LOCATION  ` : the [location](https://docs.cloud.google.com/bigquery/docs/locations) of the reservation

  - `  RESERVATION_NAME  ` : the name of the reservation

  - `  ASSIGNMENT_ID  ` : the ID of the assignment
    
    To get the assignment ID, see [Find a project's reservation assignment](https://docs.cloud.google.com/bigquery/docs/reservations-assignments#list-assignment) .
