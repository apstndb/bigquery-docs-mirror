# Schedule Airflow DAGs

This document describes how to schedule [Airflow directed acyclic graphs (DAGs)](/composer/docs/composer-3/composer-overview#about-airflow) from [Cloud Composer 3](/composer/docs/composer-3/composer-overview) on the **Scheduling** page in BigQuery, including how to trigger DAGs manually, and how to view the history and logs of past DAG runs.

## About managing Airflow DAGs in BigQuery

The **Scheduling** page in BigQuery provides tools to schedule Airflow DAGs that run in your Cloud Composer 3 environments.

Airflow DAGs that you schedule in BigQuery are executed in one or more Cloud Composer environments in your project. The **Scheduling** page in BigQuery combines information for all Airflow DAGs in your project.

During a DAG run, Airflow schedules and executes individual tasks that make up a DAG in a sequence defined by the DAG. On the **Scheduling** page in BigQuery, you can view statuses of past DAG runs, explore detailed logs of all DAG runs and all tasks from these DAG runs, and view details about DAGs.

**Note:** You can't manage Cloud Composer environments in BigQuery. To manage environments, for example, to create an environment, install dependencies for your DAG files, upload, delete, or change individual DAGs, you use Cloud Composer.

To learn more about Airflow's core concepts such as Airflow DAGs, DAG runs, tasks, or operators, see the [Core Concepts](https://airflow.apache.org/docs/apache-airflow/stable/core-concepts/index.html) page in the Airflow documentation.

To learn more about Cloud Composer environments, see the [Cloud Composer 3 overview](/composer/docs/composer-3/composer-overview) page in the Cloud Composer documentation.

## Before you begin

Enable the Cloud Composer API.

**Roles required to enable APIs**

To enable APIs, you need the Service Usage Admin IAM role ( `  roles/serviceusage.serviceUsageAdmin  ` ), which contains the `  serviceusage.services.enable  ` permission. [Learn how to grant roles](/iam/docs/granting-changing-revoking-access) .

Make sure that your Google Cloud project has at least one Cloud Composer 3 environment, with at least one already uploaded DAG file:

  - To get started with Airflow DAGs, follow the instructions in the [Run an Apache Airflow DAG in Cloud Composer 3](/composer/docs/composer-3/run-apache-airflow-dag) guide. As a part of this guide, you create a Cloud Composer 3 environment with the default configuration, upload a DAG to it, and check that Airflow runs it.
  - For detailed instructions to upload an Airflow DAG to a Cloud Composer 3 environment, see [Add and update DAGs](/composer/docs/composer-3/manage-dags) .
  - For detailed instructions to create a Cloud Composer 3 environment, see [Create Cloud Composer environments](/composer/docs/composer-3/create-environments) .

### Required permissions

To get the permissions that you need to schedule Airflow DAGs, ask your administrator to grant you the following IAM roles on the project:

  - To view Airflow DAGs and their details: [Environment and Storage Object Viewer](/iam/docs/roles-permissions/composer#composer.environmentAndStorageObjectViewer) ( `  roles/composer.environmentAndStorageObjectViewer  ` )
  - To trigger and pause Airflow DAGs: [Environment and Storage Object User](/iam/docs/roles-permissions/composer#composer.environmentAndStorageObjectUser) ( `  roles/composer.environmentAndStorageObjectUser  ` )

For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

These predefined roles contain the permissions required to schedule Airflow DAGs. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to schedule Airflow DAGs:

  - To view Airflow DAGs and their details: `  composers.dags.list, composer.environments.list  `
  - To trigger and pause Airflow DAGs: `  composers.dags.list, composer.environments.list, composer.dags.execute  `

You might also be able to get these permissions with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

For more information about Cloud Composer 3 IAM, see [Access control with IAM](/composer/docs/composer-3/access-control) in Cloud Composer documentation.

## Manually trigger an Airflow DAG

When you manually trigger an Airflow DAG, Airflow runs the DAG once, independently from the schedule specified for the DAG.

To manually trigger a selected Airflow DAG, follow these steps:

1.  In the Google Cloud console, go to the **Scheduling** page.

2.  Do either of the following:
    
      - Click the name of the selected DAG, and then on the **DAG details** page, click **Trigger DAG** .
    
      - In the row that contains the selected DAG, click more\_vert **View actions** in the **Actions** column, and then click **Trigger DAG** .

## View Airflow DAG run logs and details

To view details of a selected Airflow DAG, follow these steps:

1.  In the Google Cloud console, go to the **Scheduling** page.

2.  Click the name of the selected DAG.

3.  On the **DAG details** page, select the **Details** tab.

4.  To view past DAG runs, select the **Runs** tab.
    
    1.  Optional: The **Runs** tab displays DAG runs from the last 10 days by default. To filter DAG runs by a different time range, in the **10 days** drop-down menu, select a time range, and then click **OK** .
    
    2.  Optional: To display additional columns with DAG run details in the list of all DAG runs, click view\_column **Column display options** , and then select columns and click **OK** .
    
    3.  To view details and logs for a selected DAG run, select a DAG run.

5.  To view a visualization of the DAG with task dependencies, select the **Diagram** tab.
    
    1.  To view task details, select a task on the diagram.

6.  To view the source code of the DAG, select the **Code** tab.

7.  Optional: To refresh the displayed data, click **Refresh** .

## View all Airflow DAGs

To view Airflow DAGs from all Cloud Composer 3 environments in your Google Cloud project, follow these steps:

1.  In the Google Cloud console, go to the **Scheduling** page.

2.  Optional: To display additional columns with DAG details, click view\_column **Column display options** , and then select columns and click **OK** .

## Pause an Airflow DAG

To pause a selected Airflow DAG, follow these steps:

1.  In the Google Cloud console, go to the **Scheduling** page.

2.  Do either of the following:
    
      - Click the name of the selected DAG, and then on the **DAG details** page, click **Pause DAG** .
    
      - In the row that contains the selected DAG, click more\_vert **View actions** in the **Actions** column, and then click **Pause DAG** .

## Troubleshooting

For instructions to troubleshoot Airflow DAGs, see [Troubleshooting Airflow DAGs](/composer/docs/composer-3/troubleshooting-dags) in Cloud Composer documentation.

## What's next

  - Learn more about [writing Airflow DAGs](/composer/docs/composer-3/write-dags) .
  - Learn more about [Airflow in Cloud Composer 3](/composer/docs/composer-3/composer-overview#about-airflow) .
