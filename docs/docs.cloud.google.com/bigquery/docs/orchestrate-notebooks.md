# Schedule notebooks

This document describes how to schedule [Colab Enterprise notebooks in BigQuery](/bigquery/docs/notebooks-introduction) , and inspect scheduled notebook runs.

Notebooks are code assets powered by [Dataform](/dataform/docs/overview) . However, notebooks aren't visible in [Dataform](/dataform/docs/overview) .

You can schedule a notebook to automatically run at a specified time and frequency—for example, to train an ML model, call external APIs, or run BigQuery DataFrames code.

Changes that you make to a notebook are automatically saved, but are available only to you and to users who have [access to the notebook](/bigquery/docs/manage-notebooks#grant_access_to_notebooks) . To update the schedule with a new version of the notebook, you need to [deploy the notebook](#deploy) . By deploying a notebook, you update its schedule with your current version of the notebook. Schedules run the latest deployed version of the notebook.

Each notebook schedule is run using your Google Account user credentials or a [custom service account](/dataform/docs/access-control#about-service-accounts) that you select when you configure the schedule.

Dataform writes the output of scheduled notebook runs to the [Cloud Storage bucket](/storage/docs/buckets) selected during schedule creation.

Notebook schedules use a [standard E2 runtime](/colab/docs/runtimes) . Colab Enterprise charges for runtimes apply. You are charged for runtime processing based on the E2 machine type. For information about pricing of standard E2 runtimes, see [Colab Enterprise pricing](https://cloud.google.com/colab/pricing) .

## Before you begin

Before you begin, [create a notebook](/bigquery/docs/create-notebooks) .

### Enable notebook scheduling

To schedule notebooks, you must grant the following roles to the custom service account that you plan to use for notebook schedules:

  - [Notebook Executor User](/iam/docs/roles-permissions/aiplatform#aiplatform.notebookExecutorUser) ( `  roles/aiplatform.notebookExecutorUser  ` )  
    Follow [Grant a single role on a project](/iam/docs/granting-changing-revoking-access#grant-single-role) to grant the Notebook Executor User role to your service account on the selected project.
  - [Storage Admin](/iam/docs/roles-permissions/storage#storage.admin) ( `  roles/storage.admin  ` )  
    Follow [Add a principal to a bucket-level policy](/storage/docs/access-control/using-iam-permissions#bucket-add) to add your service account as a principal to the Cloud Storage bucket that you plan to use for storing the output of scheduled notebook runs, and grant the Storage Admin role to this principal.
  - [Service Account User](/iam/docs/roles-permissions/iam#iam.serviceAccountUser) ( `  roles/iam.serviceAccountUser  ` )  
    Follow [Grant a single role on a service account](/iam/docs/manage-access-service-accounts#grant-single-role) to add your service account as a principal to itself. In other words, add the service account as a principal to the same service account. Then, grant the Service Account User role to this principal.

Additionally, you must grant the following roles to the default Dataform service agent:

  - [Service Account Token Creator](/iam/docs/service-account-permissions#token-creator-role) ( `  roles/iam.serviceAccountTokenCreator  ` )  
    Follow [Grant token creation access to a custom Dataform service account](/dataform/docs/access-control#grant-token-creation-access) to add the default Dataform service agent as a principal to your service account, and grant the Service Account Token Creator role to this principal.
  - [Service Account User](/iam/docs/roles-permissions/iam#iam.serviceAccountUser) ( `  roles/iam.serviceAccountUser  ` )  
    Follow [Grant or revoke multiple IAM roles using Google Cloud console](/iam/docs/manage-access-service-accounts#multiple-roles-console) to grant the Service Account User role to the default Dataform service agent on the custom service account.

To learn more about service accounts in Dataform, see [About service accounts in Dataform](/dataform/docs/access-control#about-service-accounts) .

### Required roles

To create notebook schedules, you need the following roles:

  - [Dataform Admin](/dataform/docs/access-control#dataform.admin) ( `  roles/dataform.admin  ` )
  - [BigQuery Read Session User](/bigquery/docs/access-control#bigquery.readSessionUser) ( `  roles/bigquery.readSessionUser  ` ) or [BigQuery Studio User](/bigquery/docs/access-control#bigquery.studioUser) ( `  roles/bigquery.studioUser  ` )
  - [Notebook Runtime User](/iam/docs/roles-permissions/aiplatform#aiplatform.notebookRuntimeUser) ( `  roles/aiplatform.notebookRuntimeUser  ` )
  - [Service Account User role](/iam/docs/roles-permissions/iam#iam.serviceAccountUser) ( `  roles/iam.serviceAccountUser  ` ) on the custom service account

To use notebook runtime templates when scheduling notebooks, you need the [Notebook Runtime User ( `  roles/aiplatform.notebookRuntimeUser  ` )](/iam/docs/roles-permissions/aiplatform#aiplatform.notebookRuntimeUser) role.

To edit and delete notebook schedules, you need the [Dataform Editor ( `  roles/dataform.editor  ` )](/dataform/docs/access-control#dataform.editor) role.

To view notebook schedules, you need the [Dataform Viewer ( `  roles/dataform.viewer  ` )](/dataform/docs/access-control#dataform.viewer) role.

To enhance security for scheduling, see [Implement enhanced scheduling permissions](/dataform/docs/access-control#enhanced-scheduling-permissions) .

For more information about BigQuery IAM, see [BigQuery IAM roles and permissions](/bigquery/docs/access-control) .

For more information about Dataform IAM, see [Control access with IAM](/dataform/docs/access-control) .

## Create a schedule

To create a notebook schedule, follow these steps:

### **Explorer** pane

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :
    
    If you don't see the left pane, click last\_page **Expand left pane** to open the pane.

3.  In the **Explorer** pane, expand your project and click **Notebooks** .

4.  Click the name of the notebook that you want to schedule. You can use the search feature or filters to find your notebook.

5.  In the **Notebook** toolbar, click **Schedule** .
    
    Alternatively, click calendar\_month **Schedule** , and then click **Create schedule** .

6.  In the **Schedule Notebook** pane, in the **Schedule name** field, enter a name for the schedule.

7.  In the **Authentication** section, authorize the notebook with your Google Account user credentials or a service account.
    
      - To use your Google Account user credentials ( [Preview](https://cloud.google.com/products#product-launch-stages) ), select **Execute with my user credentials** .
      - To use a service account, select **Execute with selected service account** , then select a service account.

8.  In the **Notebook options** section, in the **Runtime template** field, select a Colab notebook runtime template or the default runtime specifications. For details on creating a Colab notebook runtime template, see [Create a runtime template](/colab/docs/create-runtime-template) .
    
    **Note:** A notebook runtime template must be in the same region as the notebook.
    
    **Note:** If you don't have the [required role](#required_permissions) for using notebook runtime templates, you can still run and schedule notebooks with the default runtime specifications.

9.  In the **Cloud Storage bucket** field, click **Browse** and select or create a Cloud Storage bucket.
    
    The selected service account must be granted the [Storage Admin ( `  roles/storage.admin  ` )](/iam/docs/roles-permissions/storage#storage.admin) IAM role on the selected bucket. For more information, see [Enable notebook scheduling](#enable-scheduling) .

10. In the **Schedule frequency** section, do the following:
    
    1.  In the **Repeats** menu, select the frequency of scheduled notebook runs.
    2.  In the **At time** field, enter the time for scheduled notebook runs.
    3.  In the **Timezone** menu, select the timezone for the schedule.

11. Click **Create schedule** . If you selected **Execute with my user credentials** for your authentication method, you must [authorize your Google Account](#authorize-google-account) ( [Preview](https://cloud.google.com/products#product-launch-stages) ).

When you create the schedule, the current version of the notebook is automatically deployed. To update the schedule with a new version of the notebook, [deploy the notebook](#deploy) .

The latest deployed version of the notebook runs at the selected time and frequency.

### **Scheduling** page

1.  In the Google Cloud console, go to the **Scheduling** page.

2.  Click **Create** , and then select **Notebook schedule** from the menu.

3.  In the **Schedule notebook** pane, in the **Notebook** field, select the notebook you want to schedule.

4.  In the **Schedule name** field, enter a name for the schedule.

5.  In the **Authentication** section, authorize the notebook with your Google Account user credentials or a service account.
    
      - To use your Google Account user credentials ( [Preview](https://cloud.google.com/products#product-launch-stages) ), select **Execute with my user credentials** .
      - To use a service account, select **Execute with selected service account** , and then select a service account.

6.  In the **Notebook options** section, in the **Runtime template** field, select a Colab notebook runtime template or the default runtime specifications. For details on creating a Colab notebook runtime template, see [Create a runtime template](/colab/docs/create-runtime-template) .
    
    **Note:** A notebook runtime template must be in the same region as the notebook.
    
    **Note:** If you don't have the [required role](#required_permissions) for using notebook runtime templates, you can still run and schedule notebooks with the default runtime specifications.

7.  In the **Cloud Storage bucket** field, click **Browse** and select or create a Cloud Storage bucket.
    
    The selected service account must be granted the [Storage Admin ( `  roles/storage.admin  ` )](/iam/docs/roles-permissions/storage#storage.admin) IAM role on the selected bucket. For more information, see [Enable notebook scheduling](#enable-scheduling) .

8.  In the **Schedule frequency** section, do the following:
    
    1.  In the **Repeats** menu, select the frequency of scheduled notebook runs.
    2.  In the **At time** field, enter the time for scheduled notebook runs.
    3.  In the **Timezone** menu, select the timezone for the schedule.

9.  Click **Create schedule** . If you selected **Execute with my user credentials** for your authentication method, you must [authorize your Google Account](#authorize-google-account) ( [Preview](https://cloud.google.com/products#product-launch-stages) ).

When you create the schedule, the current version of the notebook is automatically deployed. To update the schedule with a new version of the notebook, [deploy the notebook](#deploy) .

The latest deployed version of the notebook runs at the selected time and frequency.

### Authorize your Google Account

**Preview**

This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

**Note:** To request support or provide feedback for this feature, contact <dataform-preview-support@google.com> .

To authenticate the resource with your [Google Account](/iam/docs/principals-overview#google-account) user credentials, you must manually grant permission for BigQuery pipelines to get the access token for your Google Account and access the source data on your behalf. You can grant manual approval with the OAuth dialog interface.

You only need to give permission to BigQuery pipelines once.

To revoke the permission that you granted, follow these steps:

1.  Go to your [Google Account page](https://myaccount.google.com/) .
2.  Click **BigQuery Pipelines** .
3.  Click **Remove access** .

**Warning:** Revoking access permissions prevents any future pipeline runs that this Google Account owns across all regions.

Changing the notebook schedule owner by updating credentials also requires manual approval if the new Google Account owner has never created a schedule before.

## Deploy a notebook

Deploying a notebook updates its schedule with the current version of the notebook. Schedules run the latest deployed version of the notebook.

If you have a schedule for this notebook, BigQuery prompts you to deploy changes to update your schedule when you edit the notebook.

To deploy a notebook, follow these steps:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :

3.  In the **Explorer** pane, expand your project and click **Notebooks** .

4.  Click the name of the selected notebook.

5.  Click **Deploy** .

The corresponding schedule is updated with the current version of the notebook. The latest deployed version of the notebook runs at the scheduled time.

## Manually run a deployed notebook

When you manually run a notebook deployed in a selected schedule, BigQuery executes the deployed notebook once, independently from the schedule.

To manually run a deployed notebook, follow these steps:

1.  In the Google Cloud console, go to the **Scheduling** page.

2.  Click the name of the selected notebook schedule.

3.  On the **Schedule details** page, click **Run** .

## View all schedules

To view all notebook schedules in your project, follow these steps:

1.  In the Google Cloud console, go to the **Scheduling** page.

2.  Optional: To display additional columns with notebook schedule details, click view\_column **Column display options** , and then select columns and click **OK** .

## View schedule details

You can view details of a selected schedule in the **Explorer** pane or on the **Scheduling** page.

To view schedule details for a selected notebook, follow these steps:

### **Explorer** pane

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :

3.  In the **Explorer** pane, expand your project and click **Notebooks** .

4.  Click the name of the selected notebook.

5.  In the **Notebook** toolbar, click **Schedule** .
    
    Alternatively, click calendar\_month **Schedule** :

### **Scheduling** page

1.  In the Google Cloud console, go to the **Scheduling** page.

2.  Click the name of the selected notebook schedule.

## View past executions

You can view past executions of a selected notebook schedule in the **Explorer** pane or on the **Scheduling** page.

To view past executions of a selected notebook schedule, follow these steps:

### **Explorer** pane

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :

3.  In the **Explorer** pane, expand your project and click **Notebooks** .

4.  Click the name of the selected notebook.

5.  Click **Schedule** , and then click **View past executions** .

### **Scheduling** page

1.  In the Google Cloud console, go to the **Scheduling** page.

2.  Click the name of the selected notebook schedule.

3.  On the **Schedule details** page, in the **Past executions** section, inspect past executions.

4.  Optional: To refresh the list of past executions, click **Refresh** .

## Disable a schedule

To pause scheduled runs of a selected notebook without deleting the schedule, you can disable the schedule.

To disable a schedule for a selected notebook, follow these steps:

### **Explorer** pane

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :

3.  In the **Explorer** pane, expand your project and click **Notebooks** .

4.  Click the name of the selected notebook.

5.  In the **Notebook** toolbar, click **Schedule** .
    
    Alternatively, click calendar\_month **Schedule** :

6.  In the schedule details table, in the **Schedule state** row, click the **Schedule is enabled** toggle.

### **Scheduling** page

1.  In the Google Cloud console, go to the **Scheduling** page.

2.  Click the name of the selected notebook.

3.  On the **Schedule details** page, click **Disable** .

## Enable a schedule

To resume scheduled runs of a disabled notebook schedule, follow these steps:

### **Explorer** pane

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :

3.  In the **Explorer** pane, expand your project and click **Notebooks** .

4.  Click the name of the selected notebook.

5.  In the **Notebook** toolbar, click **Schedule** .
    
    Alternatively, click calendar\_month **Schedule** .

6.  In the schedule details table, in the **Schedule state** row, click the **Schedule is disabled** toggle.

### **Scheduling** page

1.  In the Google Cloud console, go to the **Scheduling** page.

2.  Click the name of the selected notebook.

3.  On the **Schedule details** page, click **Enable** .

## Edit a schedule

You can edit a schedule in the **Explorer** pane or on the **Scheduling** page.

To edit a schedule, follow these steps:

### **Explorer** pane

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click explore **Explorer** :

3.  In the **Explorer** pane, expand your project and click **Notebooks** .

4.  Click the name of the selected notebook.

5.  Click **Schedule** , and then click **Edit** .

6.  In the **Schedule details** dialog, edit the schedule, and then click **Update schedule** .

### **Scheduling** page

1.  In the Google Cloud console, go to the **Scheduling** page.

2.  Click the name of the selected notebook schedule.

3.  On the **Schedule details** page, click **Edit** .

4.  Click **View schedule** , and then click **Edit** .

5.  In the **Schedule notebook** dialog, edit the schedule, and then click **Update schedule** .

## Delete a schedule

To permanently delete a schedule for a selected notebook, follow these steps:

1.  In the Google Cloud console, go to the **Scheduling** page.

2.  Do either of the following:
    
      - Click the name of the selected schedule, and then on the **Schedule details** page, click **Delete** .
    
      - In the row that contains the selected schedule, click more\_vert **View actions** in the **Actions** column, and then click **Delete** .

3.  In the dialog that appears, click **Delete** .

## What's next

  - Learn more about [Colab Enterprise notebooks in BigQuery](/bigquery/docs/notebooks-introduction) .
  - Learn how to [create notebooks](/bigquery/docs/create-notebooks) .
