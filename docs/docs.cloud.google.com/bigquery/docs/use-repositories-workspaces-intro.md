---
name: documents/docs.cloud.google.com/bigquery/docs/use-repositories-workspaces-intro
uri: https://docs.cloud.google.com/bigquery/docs/use-repositories-workspaces-intro
title: Introduction to repositories and workspaces
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# Introduction to repositories and workspaces

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> **Note:** To provide feedback or ask questions that are related to this Preview feature, contact <bigquery-repositories-feedback@google.com> .

BigQuery repositories and workspaces let you apply Git version control to code assets such as SQL queries, Python notebooks, data canvases, and data preparations. Version control helps you track file changes over time, collaborate with your team without overwriting shared work, and revert to earlier commits when needed. You store your shared codebase in a built-in or connected third-party Git repository. You then use individual workspaces to edit files, commit changes, and push or pull updates across branches.

For a folder-based version control experience, we recommend using [BigQuery Studio Git repositories](https://docs.cloud.google.com/bigquery/docs/git-repositories) . This integration lets you work with Git branches directly in the BigQuery Studio file browser and clone multiple repositories at once without managing separate workspaces.

## Repositories

BigQuery repositories function as Git repositories that provide version control for the files you use within BigQuery. You can use the built-in Git capabilities of BigQuery or connect to an existing third-party Git repository. Within each repository, you create [workspaces](https://docs.cloud.google.com/bigquery/docs/use-repositories-workspaces-intro#workspaces) to edit the code stored there.

For more information about creating and managing repositories, see [Create and manage repositories](https://docs.cloud.google.com/bigquery/docs/repositories) .

## Workspaces

Workspaces in BigQuery let you edit and manage code stored in [repositories](https://docs.cloud.google.com/bigquery/docs/use-repositories-workspaces-intro#repositories) . Within a workspace, you can create and modify files while the parent repository uses Git to record changes and manage file versions.

For more information about creating and managing workspaces, see [Create and manage workspaces](https://docs.cloud.google.com/bigquery/docs/workspaces) .

## Locations

You can create repositories in all [BigQuery Studio locations](https://docs.cloud.google.com/bigquery/docs/locations#bqstudio-loc) . Each workspace within a repository uses the same location as the repository.

## Quotas

[Dataform quotas](https://docs.cloud.google.com/dataform/docs/quotas#quotas) apply to use of BigQuery workspaces and repositories.

## Pricing

You are not charged for creating, updating, or deleting a repository or a workspace, or for storage of the files in a workspace.

For more information about BigQuery pricing, see [Pricing](https://cloud.google.com/bigquery/pricing) .

## What's next

- To learn how to manage code with BigQuery Studio Git repositories, see [Manage code with BigQuery Studio Git repositories](https://docs.cloud.google.com/bigquery/docs/git-repositories) .
- To learn how to create and use repositories, see [Create and manage repositories](https://docs.cloud.google.com/bigquery/docs/repositories) .
- To learn how to create and use workspaces, see [Create and manage workspaces](https://docs.cloud.google.com/bigquery/docs/workspaces) .
