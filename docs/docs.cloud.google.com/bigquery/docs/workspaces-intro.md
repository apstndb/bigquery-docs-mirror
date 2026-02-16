# Introduction to workspaces

**Preview**

This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

**Note:** To provide feedback or ask questions that are related to this Preview feature, contact [bigquery-repositories-feedback@google.com](mailto:%20bigquery-repositories-feedback@google.com) .

This document helps you understand the concept of workspaces in BigQuery. You can use workspaces within [repositories](/bigquery/docs/repository-intro) to edit the code stored in the repository. Repositories perform version control on files by using Git to record changes and manage file versions.

On the BigQuery page, your workspaces are displayed in alphabetical order under the repository they are associated with. To view repositories, do the following:

1.  In the left pane, click explore **Explorer** :
    
    If you don't see the left pane, click last\_page **Expand left pane** to open the pane.

2.  In the **Explorer** pane, click **Repositories** .

## Supported file types

You can create or upload the following types of files to a repository:

  - SQL queries
  - Python notebooks
  - [Data canvases](/bigquery/docs/data-canvas)
  - [Data preparations](/bigquery/docs/data-prep-introduction)
  - Any other types of files

For more information, see [Work with files in a workspace](/bigquery/docs/workspaces#work_with_files_in_a_workspace) .

## Git integration

As you create and modify files in a workspace, you can perform Git actions like committing changes and pushing changes to the repository. For more information, see [Use version control with a file](/bigquery/docs/workspaces#use_version_control_with_a_file) .

## Locations

Each workspace uses the same [location](/bigquery/docs/repository-intro#locations) as the repository that contains it.

## Quotas

[Dataform quotas](/dataform/docs/quotas#quotas) apply to use of BigQuery workspaces.

## Pricing

You are not charged for creating, updating, or deleting a workspace, or for storage of the files in a workspace.

For more information on BigQuery pricing, see [Pricing](https://cloud.google.com/bigquery/pricing) .

## What's next

  - To learn how to create and use repositories, see [Create a repository](/bigquery/docs/repositories) .
  - To learn how to create and use workspaces, see [Create a workspace](/bigquery/docs/workspaces) .
