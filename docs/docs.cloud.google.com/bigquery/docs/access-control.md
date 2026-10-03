---
name: documents/docs.cloud.google.com/bigquery/docs/access-control
uri: https://docs.cloud.google.com/bigquery/docs/access-control
title: BigQuery IAM roles and permissions
description: Lists the Identity and Access Management (IAM) predefined roles and permissions for BigQuery.
data_source: docs.cloud.google.com
---

# BigQuery IAM roles and permissions

This document provides a list of Identity and Access Management (IAM) predefined roles and permissions for BigQuery. This page includes roles and permissions for the following:

- BigQuery: Roles and permissions that apply to BigQuery resources such as datasets, tables, views, and routines. Many of these roles and permissions can also be granted to Resource Manager resources like projects, folders, and organizations.
- BigQuery Connection API: Role that grants a [service agent](https://docs.cloud.google.com/iam/docs/service-agents) access to a Cloud SQL connection.
- BigQuery Continuous Query: Role that grants a [service account](https://docs.cloud.google.com/iam/docs/service-account-overview) access to a continuous query.
- BigQuery Data Policy: Roles and permissions that apply to Data Policies in BigQuery.
- BigQuery Data Transfer Service: Role that grants a [service agent](https://docs.cloud.google.com/iam/docs/service-agents) access to create jobs that transfer data.
- BigQuery Engine for Apache Flink: Roles and permissions that apply to BigQuery Engine for Apache Flink resources.
- BigQuery Migration Service API: Roles and permissions that apply to BigQuery Migration Service resources.
- BigQuery Omni: Role that grants a [service agent](https://docs.cloud.google.com/iam/docs/service-agents) access to tables.
- BigQuery sharing: Roles and permissions that apply to BigQuery sharing resources.

## BigQuery predefined IAM roles

The following tables list the predefined BigQuery IAM roles with a corresponding list of all the [permissions](https://docs.cloud.google.com/bigquery/docs/access-control#bq-permissions) each role includes. Note that each permission is applicable to a particular resource type.

> **Note:** When new capabilities are added to BigQuery, new permissions might be added to predefined IAM roles, and new predefined IAM roles might be added to BigQuery. If your organization requires role definitions to remain unchanged, you should create [custom IAM roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) .

### BigQuery roles

This table lists the predefined IAM roles and permissions for BigQuery. To search through all roles and permissions, see the [role and permission index](https://docs.cloud.google.com/iam/docs/roles-permissions) .

For information on granting predefined roles on BigQuery resources like datasets, tables, and routines, see [Control access to resources with IAM](https://docs.cloud.google.com/bigquery/docs/control-access-to-resources-iam) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Role</th>
<th>Permissions</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>BigQuery Admin
<p>( <code>roles/ bigquery.admin</code> )</p>
<p>Provides permissions to manage all resources within the project. Can manage all data within the project, and can cancel jobs from other users running within the project.</p>
<p>It is possible to grant this role to the following lowest-level resources, but it is not recommended. Other predefined roles grant full permissions over these resources and are less permissive. BigQuery Admin is typically granted at the project level.</p>
<p>Lowest-level resources where you can grant this role:</p>
<ul>
<li>Dataset</li>
<li>These resources within a dataset:
<ul>
<li>Table</li>
<li>View</li>
<li>Routine</li>
</ul></li>
<li>Connection</li>
<li>Saved query</li>
<li>Data canvas</li>
<li>Pipeline</li>
<li>Data preparation</li>
<li>Repository</li>
</ul>
<p>This role can also be granted on Resource Manager resources (projects, folders, and organizations).</p></td>
<td><p><code>bigquery.bireservations.*</code></p>
<ul>
<li><code>bigquery.bireservations.get</code></li>
<li><code>bigquery.bireservations.update</code></li>
</ul>
<p><code>bigquery.capacityCommitments.*</code></p>
<ul>
<li><code>bigquery. capacityCommitments. create</code></li>
<li><code>bigquery. capacityCommitments. delete</code></li>
<li><code>bigquery. capacityCommitments. get</code></li>
<li><code>bigquery. capacityCommitments. list</code></li>
<li><code>bigquery. capacityCommitments. update</code></li>
</ul>
<p><code>bigquery.config.*</code></p>
<ul>
<li><code>bigquery.config.get</code></li>
<li><code>bigquery.config.update</code></li>
</ul>
<p><code>bigquery.connections.*</code></p>
<ul>
<li><code>bigquery.connections.create</code></li>
<li><code>bigquery.connections.delegate</code></li>
<li><code>bigquery.connections.delete</code></li>
<li><code>bigquery.connections.get</code></li>
<li><code>bigquery. connections. getIamPolicy</code></li>
<li><code>bigquery.connections.list</code></li>
<li><code>bigquery. connections. setIamPolicy</code></li>
<li><code>bigquery.connections.update</code></li>
<li><code>bigquery.connections.updateTag</code></li>
<li><code>bigquery.connections.use</code></li>
</ul>
<p><code>bigquery.dataPolicies.attach</code></p>
<p><code>bigquery.dataPolicies.create</code></p>
<p><code>bigquery.dataPolicies.delete</code></p>
<p><code>bigquery.dataPolicies.get</code></p>
<p><code>bigquery. dataPolicies. getIamPolicy</code></p>
<p><code>bigquery.dataPolicies.list</code></p>
<p><code>bigquery. dataPolicies. setIamPolicy</code></p>
<p><code>bigquery.dataPolicies.update</code></p>
<p><code>bigquery.datasets.*</code></p>
<ul>
<li><code>bigquery.datasets.create</code></li>
<li><code>bigquery. datasets. createTagBinding</code></li>
<li><code>bigquery.datasets.delete</code></li>
<li><code>bigquery. datasets. deleteTagBinding</code></li>
<li><code>bigquery.datasets.get</code></li>
<li><code>bigquery.datasets.getIamPolicy</code></li>
<li><code>bigquery.datasets.link</code></li>
<li><code>bigquery. datasets. listEffectiveTags</code></li>
<li><code>bigquery. datasets. listSharedDatasetUsage</code></li>
<li><code>bigquery. datasets. listTagBindings</code></li>
<li><code>bigquery.datasets.setIamPolicy</code></li>
<li><code>bigquery.datasets.update</code></li>
<li><code>bigquery.datasets.updateTag</code></li>
</ul>
<p><code>bigquery.jobs.*</code></p>
<ul>
<li><code>bigquery.jobs.create</code></li>
<li><code>bigquery. jobs. createGlobalQuery</code></li>
<li><code>bigquery.jobs.delete</code></li>
<li><code>bigquery.jobs.get</code></li>
<li><code>bigquery.jobs.list</code></li>
<li><code>bigquery.jobs.listAll</code></li>
<li><code>bigquery. jobs. listExecutionMetadata</code></li>
<li><code>bigquery.jobs.update</code></li>
</ul>
<p><code>bigquery.models.*</code></p>
<ul>
<li><code>bigquery.models.create</code></li>
<li><code>bigquery.models.delete</code></li>
<li><code>bigquery.models.export</code></li>
<li><code>bigquery.models.getData</code></li>
<li><code>bigquery.models.getMetadata</code></li>
<li><code>bigquery.models.list</code></li>
<li><code>bigquery.models.updateData</code></li>
<li><code>bigquery.models.updateMetadata</code></li>
<li><code>bigquery.models.updateTag</code></li>
</ul>
<p><code>bigquery.objectRefs.*</code></p>
<ul>
<li><code>bigquery.objectRefs.read</code></li>
<li><code>bigquery.objectRefs.write</code></li>
</ul>
<p><code>bigquery.propertyGraphs.*</code></p>
<ul>
<li><code>bigquery.propertyGraphs.create</code></li>
<li><code>bigquery.propertyGraphs.delete</code></li>
<li><code>bigquery.propertyGraphs.get</code></li>
<li><code>bigquery.propertyGraphs.list</code></li>
<li><code>bigquery.propertyGraphs.update</code></li>
</ul>
<p><code>bigquery.readsessions.*</code></p>
<ul>
<li><code>bigquery.readsessions.create</code></li>
<li><code>bigquery.readsessions.getData</code></li>
<li><code>bigquery.readsessions.update</code></li>
</ul>
<p><code>bigquery. reservationAssignments.*</code></p>
<ul>
<li><code>bigquery. reservationAssignments. create</code></li>
<li><code>bigquery. reservationAssignments. delete</code></li>
<li><code>bigquery. reservationAssignments. list</code></li>
<li><code>bigquery. reservationAssignments. search</code></li>
</ul>
<p><code>bigquery.reservationGroups.*</code></p>
<ul>
<li><code>bigquery. reservationGroups. create</code></li>
<li><code>bigquery. reservationGroups. delete</code></li>
<li><code>bigquery.reservationGroups.get</code></li>
<li><code>bigquery. reservationGroups. list</code></li>
<li><code>bigquery. reservationGroups. update</code></li>
</ul>
<p><code>bigquery.reservations.*</code></p>
<ul>
<li><code>bigquery.reservations.create</code></li>
<li><code>bigquery.reservations.delete</code></li>
<li><code>bigquery.reservations.get</code></li>
<li><code>bigquery. reservations. getIamPolicy</code></li>
<li><code>bigquery.reservations.list</code></li>
<li><code>bigquery. reservations. listFailoverDatasets</code></li>
<li><code>bigquery. reservations. setIamPolicy</code></li>
<li><code>bigquery.reservations.update</code></li>
<li><code>bigquery.reservations.use</code></li>
</ul>
<p><code>bigquery.routines.*</code></p>
<ul>
<li><code>bigquery.routines.create</code></li>
<li><code>bigquery.routines.delete</code></li>
<li><code>bigquery.routines.get</code></li>
<li><code>bigquery.routines.list</code></li>
<li><code>bigquery.routines.update</code></li>
<li><code>bigquery.routines.updateTag</code></li>
</ul>
<p><code>bigquery. rowAccessPolicies. create</code></p>
<p><code>bigquery. rowAccessPolicies. delete</code></p>
<p><code>bigquery.rowAccessPolicies.get</code></p>
<p><code>bigquery. rowAccessPolicies. getIamPolicy</code></p>
<p><code>bigquery. rowAccessPolicies. list</code></p>
<p><code>bigquery. rowAccessPolicies. overrideTimeTravelRestrictions</code></p>
<p><code>bigquery. rowAccessPolicies. setIamPolicy</code></p>
<p><code>bigquery. rowAccessPolicies. update</code></p>
<p><code>bigquery.savedqueries.*</code></p>
<ul>
<li><code>bigquery.savedqueries.create</code></li>
<li><code>bigquery.savedqueries.delete</code></li>
<li><code>bigquery.savedqueries.get</code></li>
<li><code>bigquery.savedqueries.list</code></li>
<li><code>bigquery.savedqueries.update</code></li>
</ul>
<p><code>bigquery.tables.*</code></p>
<ul>
<li><code>bigquery.tables.create</code></li>
<li><code>bigquery.tables.createIndex</code></li>
<li><code>bigquery.tables.createSnapshot</code></li>
<li><code>bigquery. tables. createTagBinding</code></li>
<li><code>bigquery.tables.delete</code></li>
<li><code>bigquery.tables.deleteIndex</code></li>
<li><code>bigquery.tables.deleteSnapshot</code></li>
<li><code>bigquery. tables. deleteTagBinding</code></li>
<li><code>bigquery.tables.export</code></li>
<li><code>bigquery.tables.get</code></li>
<li><code>bigquery.tables.getData</code></li>
<li><code>bigquery.tables.getIamPolicy</code></li>
<li><code>bigquery.tables.list</code></li>
<li><code>bigquery. tables. listEffectiveTags</code></li>
<li><code>bigquery. tables. listTagBindings</code></li>
<li><code>bigquery.tables.replicateData</code></li>
<li><code>bigquery. tables. restoreSnapshot</code></li>
<li><code>bigquery.tables.setCategory</code></li>
<li><code>bigquery. tables. setColumnDataPolicy</code></li>
<li><code>bigquery.tables.setIamPolicy</code></li>
<li><code>bigquery.tables.update</code></li>
<li><code>bigquery.tables.updateData</code></li>
<li><code>bigquery.tables.updateIndex</code></li>
<li><code>bigquery.tables.updateTag</code></li>
</ul>
<p><code>bigquery.transfers.*</code></p>
<ul>
<li><code>bigquery.transfers.get</code></li>
<li><code>bigquery.transfers.update</code></li>
</ul>
<p><code>bigquerymigration. translation. translate</code></p>
<p><code>cloudkms.keyHandles.*</code></p>
<ul>
<li><code>cloudkms.keyHandles.create</code></li>
<li><code>cloudkms.keyHandles.get</code></li>
<li><code>cloudkms.keyHandles.list</code></li>
</ul>
<p><code>cloudkms.operations.get</code></p>
<p><code>cloudkms. projects. showEffectiveAutokeyConfig</code></p>
<p><code>dataform.*</code></p>
<ul>
<li><code>dataform.commentThreads.create</code></li>
<li><code>dataform.commentThreads.delete</code></li>
<li><code>dataform.commentThreads.get</code></li>
<li><code>dataform.commentThreads.list</code></li>
<li><code>dataform.commentThreads.update</code></li>
<li><code>dataform.comments.create</code></li>
<li><code>dataform.comments.delete</code></li>
<li><code>dataform.comments.get</code></li>
<li><code>dataform.comments.list</code></li>
<li><code>dataform.comments.update</code></li>
<li><code>dataform. compilationResults. create</code></li>
<li><code>dataform. compilationResults. get</code></li>
<li><code>dataform. compilationResults. list</code></li>
<li><code>dataform. compilationResults. query</code></li>
<li><code>dataform.config.get</code></li>
<li><code>dataform.config.update</code></li>
<li><code>dataform.folders.addContents</code></li>
<li><code>dataform.folders.create</code></li>
<li><code>dataform.folders.delete</code></li>
<li><code>dataform.folders.deleteTree</code></li>
<li><code>dataform.folders.get</code></li>
<li><code>dataform.folders.getIamPolicy</code></li>
<li><code>dataform.folders.move</code></li>
<li><code>dataform.folders.queryContents</code></li>
<li><code>dataform.folders.setIamPolicy</code></li>
<li><code>dataform.folders.update</code></li>
<li><code>dataform.locations.get</code></li>
<li><code>dataform.locations.list</code></li>
<li><code>dataform.operations.cancel</code></li>
<li><code>dataform.operations.delete</code></li>
<li><code>dataform.operations.get</code></li>
<li><code>dataform.operations.list</code></li>
<li><code>dataform.releaseConfigs.create</code></li>
<li><code>dataform.releaseConfigs.delete</code></li>
<li><code>dataform.releaseConfigs.get</code></li>
<li><code>dataform.releaseConfigs.list</code></li>
<li><code>dataform.releaseConfigs.update</code></li>
<li><code>dataform.repositories.commit</code></li>
<li><code>dataform. repositories. computeAccessTokenStatus</code></li>
<li><code>dataform.repositories.create</code></li>
<li><code>dataform. repositories. createTagBinding</code></li>
<li><code>dataform.repositories.delete</code></li>
<li><code>dataform. repositories. deleteTagBinding</code></li>
<li><code>dataform. repositories. fetchHistory</code></li>
<li><code>dataform. repositories. fetchRemoteBranches</code></li>
<li><code>dataform.repositories.get</code></li>
<li><code>dataform. repositories. getIamPolicy</code></li>
<li><code>dataform.repositories.list</code></li>
<li><code>dataform. repositories. listEffectiveTags</code></li>
<li><code>dataform. repositories. listTagBindings</code></li>
<li><code>dataform.repositories.move</code></li>
<li><code>dataform. repositories. queryDirectoryContents</code></li>
<li><code>dataform.repositories.readFile</code></li>
<li><code>dataform. repositories. scheduleRelease</code></li>
<li><code>dataform. repositories. scheduleWorkflow</code></li>
<li><code>dataform. repositories. setIamPolicy</code></li>
<li><code>dataform.repositories.update</code></li>
<li><code>dataform.teamFolders.create</code></li>
<li><code>dataform.teamFolders.delete</code></li>
<li><code>dataform. teamFolders. deleteTree</code></li>
<li><code>dataform.teamFolders.get</code></li>
<li><code>dataform. teamFolders. getIamPolicy</code></li>
<li><code>dataform. teamFolders. setIamPolicy</code></li>
<li><code>dataform.teamFolders.update</code></li>
<li><code>dataform. workflowConfigs. create</code></li>
<li><code>dataform. workflowConfigs. delete</code></li>
<li><code>dataform.workflowConfigs.get</code></li>
<li><code>dataform.workflowConfigs.list</code></li>
<li><code>dataform. workflowConfigs. update</code></li>
<li><code>dataform. workflowInvocations. cancel</code></li>
<li><code>dataform. workflowInvocations. create</code></li>
<li><code>dataform. workflowInvocations. delete</code></li>
<li><code>dataform. workflowInvocations. get</code></li>
<li><code>dataform. workflowInvocations. list</code></li>
<li><code>dataform. workflowInvocations. query</code></li>
<li><code>dataform.workspaces.commit</code></li>
<li><code>dataform.workspaces.create</code></li>
<li><code>dataform.workspaces.delete</code></li>
<li><code>dataform. workspaces. fetchFileDiff</code></li>
<li><code>dataform. workspaces. fetchFileGitStatuses</code></li>
<li><code>dataform. workspaces. fetchGitAheadBehind</code></li>
<li><code>dataform.workspaces.get</code></li>
<li><code>dataform. workspaces. getIamPolicy</code></li>
<li><code>dataform. workspaces. installNpmPackages</code></li>
<li><code>dataform.workspaces.list</code></li>
<li><code>dataform. workspaces. makeDirectory</code></li>
<li><code>dataform. workspaces. moveDirectory</code></li>
<li><code>dataform.workspaces.moveFile</code></li>
<li><code>dataform.workspaces.pull</code></li>
<li><code>dataform.workspaces.push</code></li>
<li><code>dataform. workspaces. queryDirectoryContents</code></li>
<li><code>dataform.workspaces.readFile</code></li>
<li><code>dataform. workspaces. removeDirectory</code></li>
<li><code>dataform.workspaces.removeFile</code></li>
<li><code>dataform.workspaces.reset</code></li>
<li><code>dataform. workspaces. searchFiles</code></li>
<li><code>dataform. workspaces. setIamPolicy</code></li>
<li><code>dataform.workspaces.writeFile</code></li>
</ul>
<p><code>dataplex.datascans.*</code></p>
<ul>
<li><code>dataplex.datascans.cancel</code></li>
<li><code>dataplex.datascans.create</code></li>
<li><code>dataplex.datascans.delete</code></li>
<li><code>dataplex.datascans.get</code></li>
<li><code>dataplex.datascans.getData</code></li>
<li><code>dataplex. datascans. getIamPolicy</code></li>
<li><code>dataplex.datascans.list</code></li>
<li><code>dataplex.datascans.run</code></li>
<li><code>dataplex. datascans. setIamPolicy</code></li>
<li><code>dataplex.datascans.update</code></li>
</ul>
<p><code>dataplex.operations.get</code></p>
<p><code>dataplex.operations.list</code></p>
<p><code>dataplex.projects.search</code></p>
<p><code>resourcemanager.projects.get</code></p>
<p><code>resourcemanager.projects.list</code></p></td>
</tr>
<tr class="even">
<td>BigQuery Connection Admin
<p>( <code>roles/ bigquery.connectionAdmin</code> )</p>
<p>Lowest-level resources where you can grant this role:</p>
<ul>
<li>Connection</li>
</ul>
<p>This role can also be granted on Resource Manager resources (projects, folders, and organizations).</p></td>
<td><p><code>bigquery.connections.*</code></p>
<ul>
<li><code>bigquery.connections.create</code></li>
<li><code>bigquery.connections.delegate</code></li>
<li><code>bigquery.connections.delete</code></li>
<li><code>bigquery.connections.get</code></li>
<li><code>bigquery. connections. getIamPolicy</code></li>
<li><code>bigquery.connections.list</code></li>
<li><code>bigquery. connections. setIamPolicy</code></li>
<li><code>bigquery.connections.update</code></li>
<li><code>bigquery.connections.updateTag</code></li>
<li><code>bigquery.connections.use</code></li>
</ul></td>
</tr>
<tr class="odd">
<td>BigQuery Connection User
<p>( <code>roles/ bigquery.connectionUser</code> )</p>
<p>Lowest-level resources where you can grant this role:</p>
<ul>
<li>Connection</li>
</ul>
<p>This role can also be granted on Resource Manager resources (projects, folders, and organizations).</p></td>
<td><p><code>bigquery.connections.get</code></p>
<p><code>bigquery. connections. getIamPolicy</code></p>
<p><code>bigquery.connections.list</code></p>
<p><code>bigquery.connections.use</code></p></td>
</tr>
<tr class="even">
<td>BigQuery Data Editor
<p>( <code>roles/ bigquery.dataEditor</code> )</p>
<p>When granted on a dataset, this role grants these permissions:</p>
<ul>
<li>Get metadata and permissions for the dataset.</li>
<li>For tables and views:
<ul>
<li>Create, update, get, list, and delete the dataset's tables and views.</li>
<li>Read (query), export, replicate, and update table data.</li>
<li>Create, update, and delete indexes.</li>
<li>Create and restore snapshots.</li>
</ul></li>
<li>All permissions for the dataset's routines and models.</li>
</ul>
<blockquote>
<strong>Note:</strong> Principals that are granted the Data Editor role at the project level can also create new datasets and list datasets in the project that they have access to.
</blockquote>
<p>When granted on a table or view, this role grants these permissions:</p>
<ul>
<li>Get metadata, update metadata, get access controls, and delete the table or view.</li>
<li>Get (query), export, replicate, and update table data.</li>
<li>Create, update, and delete indexes.</li>
<li>Create and restore snapshots.</li>
</ul>
<ul>
<li>All permissions for the routine.</li>
</ul>
<p>The Data Editor role cannot be granted to individual models.</p>
<blockquote>
<strong>Note:</strong> The BigQuery Data Editor role is mapped to the <a href="https://docs.cloud.google.com/bigquery/docs/access-control-basic-roles#dataset-basic-roles"><code>WRITER</code></a> BigQuery basic role. When you grant the BigQuery Data Editor role to a principal at the dataset level, the principal is granted <code>WRITER</code> access to the dataset.
</blockquote>
<p>Lowest-level resources where you can grant this role:</p>
<ul>
<li>Dataset</li>
<li>These resources within a dataset:
<ul>
<li>Table</li>
<li>View</li>
<li>Routine</li>
</ul></li>
</ul>
<p>This role can also be granted on Resource Manager resources (projects, folders, and organizations).</p></td>
<td><p><code>bigquery.config.get</code></p>
<p><code>bigquery.datasets.create</code></p>
<p><code>bigquery.datasets.get</code></p>
<p><code>bigquery.datasets.getIamPolicy</code></p>
<p><code>bigquery.datasets.updateTag</code></p>
<p><code>bigquery.models.*</code></p>
<ul>
<li><code>bigquery.models.create</code></li>
<li><code>bigquery.models.delete</code></li>
<li><code>bigquery.models.export</code></li>
<li><code>bigquery.models.getData</code></li>
<li><code>bigquery.models.getMetadata</code></li>
<li><code>bigquery.models.list</code></li>
<li><code>bigquery.models.updateData</code></li>
<li><code>bigquery.models.updateMetadata</code></li>
<li><code>bigquery.models.updateTag</code></li>
</ul>
<p><code>bigquery.propertyGraphs.*</code></p>
<ul>
<li><code>bigquery.propertyGraphs.create</code></li>
<li><code>bigquery.propertyGraphs.delete</code></li>
<li><code>bigquery.propertyGraphs.get</code></li>
<li><code>bigquery.propertyGraphs.list</code></li>
<li><code>bigquery.propertyGraphs.update</code></li>
</ul>
<p><code>bigquery.routines.*</code></p>
<ul>
<li><code>bigquery.routines.create</code></li>
<li><code>bigquery.routines.delete</code></li>
<li><code>bigquery.routines.get</code></li>
<li><code>bigquery.routines.list</code></li>
<li><code>bigquery.routines.update</code></li>
<li><code>bigquery.routines.updateTag</code></li>
</ul>
<p><code>bigquery.tables.create</code></p>
<p><code>bigquery.tables.createIndex</code></p>
<p><code>bigquery.tables.createSnapshot</code></p>
<p><code>bigquery.tables.delete</code></p>
<p><code>bigquery.tables.deleteIndex</code></p>
<p><code>bigquery.tables.export</code></p>
<p><code>bigquery.tables.get</code></p>
<p><code>bigquery.tables.getData</code></p>
<p><code>bigquery.tables.getIamPolicy</code></p>
<p><code>bigquery.tables.list</code></p>
<p><code>bigquery.tables.replicateData</code></p>
<p><code>bigquery. tables. restoreSnapshot</code></p>
<p><code>bigquery.tables.update</code></p>
<p><code>bigquery.tables.updateData</code></p>
<p><code>bigquery.tables.updateIndex</code></p>
<p><code>bigquery.tables.updateTag</code></p>
<p><code>cloudkms.keyHandles.*</code></p>
<ul>
<li><code>cloudkms.keyHandles.create</code></li>
<li><code>cloudkms.keyHandles.get</code></li>
<li><code>cloudkms.keyHandles.list</code></li>
</ul>
<p><code>cloudkms.operations.get</code></p>
<p><code>cloudkms. projects. showEffectiveAutokeyConfig</code></p>
<p><code>dataplex.datascans.cancel</code></p>
<p><code>dataplex.datascans.create</code></p>
<p><code>dataplex.datascans.delete</code></p>
<p><code>dataplex.datascans.get</code></p>
<p><code>dataplex.datascans.getData</code></p>
<p><code>dataplex. datascans. getIamPolicy</code></p>
<p><code>dataplex.datascans.list</code></p>
<p><code>dataplex.datascans.run</code></p>
<p><code>dataplex.datascans.update</code></p>
<p><code>dataplex.operations.get</code></p>
<p><code>dataplex.operations.list</code></p>
<p><code>resourcemanager.projects.get</code></p>
<p><code>resourcemanager.projects.list</code></p></td>
</tr>
<tr class="odd">
<td>BigQuery Data Owner
<p>( <code>roles/ bigquery.dataOwner</code> )</p>
<p>When granted on a dataset, this role grants these permissions:</p>
<ul>
<li>All permissions for the dataset and for all of the resources within the dataset: tables and views, models, and routines.</li>
</ul>
<blockquote>
<strong>Note:</strong> Principals that are granted the Data Owner role at the project level can also create new datasets and list datasets in the project that they have access to.
</blockquote>
<p>When granted on a table or view, this role grants these permissions:</p>
<ul>
<li>All permissions for the table or view.</li>
<li>All permissions for row access policies except permission to override time travel restrictions.</li>
<li>Set categories and column-level data policies.</li>
</ul>
<p>When granted on a routine, this role grants these permissions:</p>
<ul>
<li>All permissions for the routine.</li>
</ul>
<p>You shouldn't grant the Data Owner role at the routine level. Data Editor also grants all permissions for the routine and is a less permissive role.</p>
<p>This role cannot be granted to individual models.</p>
<blockquote>
<strong>Note:</strong> The BigQuery Data Owner role is mapped to the <a href="https://docs.cloud.google.com/bigquery/docs/access-control-basic-roles#dataset-basic-roles"><code>OWNER</code></a> BigQuery basic role. When you grant the BigQuery Data Owner role to a principal at the dataset level, the principal is granted <code>OWNER</code> access to the dataset.
</blockquote>
<p>Lowest-level resources where you can grant this role:</p>
<ul>
<li>Dataset</li>
<li>These resources within a dataset:
<ul>
<li>Table</li>
<li>View</li>
<li>Routine</li>
</ul></li>
</ul>
<p>This role can also be granted on Resource Manager resources (projects, folders, and organizations).</p></td>
<td><p><code>bigquery.config.get</code></p>
<p><code>bigquery.dataPolicies.attach</code></p>
<p><code>bigquery.dataPolicies.create</code></p>
<p><code>bigquery.dataPolicies.delete</code></p>
<p><code>bigquery.dataPolicies.get</code></p>
<p><code>bigquery. dataPolicies. getIamPolicy</code></p>
<p><code>bigquery.dataPolicies.list</code></p>
<p><code>bigquery. dataPolicies. setIamPolicy</code></p>
<p><code>bigquery.dataPolicies.update</code></p>
<p><code>bigquery.datasets.*</code></p>
<ul>
<li><code>bigquery.datasets.create</code></li>
<li><code>bigquery. datasets. createTagBinding</code></li>
<li><code>bigquery.datasets.delete</code></li>
<li><code>bigquery. datasets. deleteTagBinding</code></li>
<li><code>bigquery.datasets.get</code></li>
<li><code>bigquery.datasets.getIamPolicy</code></li>
<li><code>bigquery.datasets.link</code></li>
<li><code>bigquery. datasets. listEffectiveTags</code></li>
<li><code>bigquery. datasets. listSharedDatasetUsage</code></li>
<li><code>bigquery. datasets. listTagBindings</code></li>
<li><code>bigquery.datasets.setIamPolicy</code></li>
<li><code>bigquery.datasets.update</code></li>
<li><code>bigquery.datasets.updateTag</code></li>
</ul>
<p><code>bigquery.models.*</code></p>
<ul>
<li><code>bigquery.models.create</code></li>
<li><code>bigquery.models.delete</code></li>
<li><code>bigquery.models.export</code></li>
<li><code>bigquery.models.getData</code></li>
<li><code>bigquery.models.getMetadata</code></li>
<li><code>bigquery.models.list</code></li>
<li><code>bigquery.models.updateData</code></li>
<li><code>bigquery.models.updateMetadata</code></li>
<li><code>bigquery.models.updateTag</code></li>
</ul>
<p><code>bigquery.propertyGraphs.*</code></p>
<ul>
<li><code>bigquery.propertyGraphs.create</code></li>
<li><code>bigquery.propertyGraphs.delete</code></li>
<li><code>bigquery.propertyGraphs.get</code></li>
<li><code>bigquery.propertyGraphs.list</code></li>
<li><code>bigquery.propertyGraphs.update</code></li>
</ul>
<p><code>bigquery.routines.*</code></p>
<ul>
<li><code>bigquery.routines.create</code></li>
<li><code>bigquery.routines.delete</code></li>
<li><code>bigquery.routines.get</code></li>
<li><code>bigquery.routines.list</code></li>
<li><code>bigquery.routines.update</code></li>
<li><code>bigquery.routines.updateTag</code></li>
</ul>
<p><code>bigquery. rowAccessPolicies. create</code></p>
<p><code>bigquery. rowAccessPolicies. delete</code></p>
<p><code>bigquery.rowAccessPolicies.get</code></p>
<p><code>bigquery. rowAccessPolicies. getIamPolicy</code></p>
<p><code>bigquery. rowAccessPolicies. list</code></p>
<p><code>bigquery. rowAccessPolicies. setIamPolicy</code></p>
<p><code>bigquery. rowAccessPolicies. update</code></p>
<p><code>bigquery.tables.*</code></p>
<ul>
<li><code>bigquery.tables.create</code></li>
<li><code>bigquery.tables.createIndex</code></li>
<li><code>bigquery.tables.createSnapshot</code></li>
<li><code>bigquery. tables. createTagBinding</code></li>
<li><code>bigquery.tables.delete</code></li>
<li><code>bigquery.tables.deleteIndex</code></li>
<li><code>bigquery.tables.deleteSnapshot</code></li>
<li><code>bigquery. tables. deleteTagBinding</code></li>
<li><code>bigquery.tables.export</code></li>
<li><code>bigquery.tables.get</code></li>
<li><code>bigquery.tables.getData</code></li>
<li><code>bigquery.tables.getIamPolicy</code></li>
<li><code>bigquery.tables.list</code></li>
<li><code>bigquery. tables. listEffectiveTags</code></li>
<li><code>bigquery. tables. listTagBindings</code></li>
<li><code>bigquery.tables.replicateData</code></li>
<li><code>bigquery. tables. restoreSnapshot</code></li>
<li><code>bigquery.tables.setCategory</code></li>
<li><code>bigquery. tables. setColumnDataPolicy</code></li>
<li><code>bigquery.tables.setIamPolicy</code></li>
<li><code>bigquery.tables.update</code></li>
<li><code>bigquery.tables.updateData</code></li>
<li><code>bigquery.tables.updateIndex</code></li>
<li><code>bigquery.tables.updateTag</code></li>
</ul>
<p><code>cloudkms.keyHandles.*</code></p>
<ul>
<li><code>cloudkms.keyHandles.create</code></li>
<li><code>cloudkms.keyHandles.get</code></li>
<li><code>cloudkms.keyHandles.list</code></li>
</ul>
<p><code>cloudkms.operations.get</code></p>
<p><code>cloudkms. projects. showEffectiveAutokeyConfig</code></p>
<p><code>dataplex.datascans.*</code></p>
<ul>
<li><code>dataplex.datascans.cancel</code></li>
<li><code>dataplex.datascans.create</code></li>
<li><code>dataplex.datascans.delete</code></li>
<li><code>dataplex.datascans.get</code></li>
<li><code>dataplex.datascans.getData</code></li>
<li><code>dataplex. datascans. getIamPolicy</code></li>
<li><code>dataplex.datascans.list</code></li>
<li><code>dataplex.datascans.run</code></li>
<li><code>dataplex. datascans. setIamPolicy</code></li>
<li><code>dataplex.datascans.update</code></li>
</ul>
<p><code>dataplex.operations.get</code></p>
<p><code>dataplex.operations.list</code></p>
<p><code>resourcemanager.projects.get</code></p>
<p><code>resourcemanager.projects.list</code></p></td>
</tr>
<tr class="even">
<td>BigQuery Data Viewer
<p>( <code>roles/ bigquery.dataViewer</code> )</p>
<p>When granted on a dataset, this role grants these permissions:</p>
<ul>
<li>Get metadata and permissions for the dataset.</li>
<li>List a dataset's tables, views, and models.</li>
<li>Get metadata and access controls for the dataset's tables and views.</li>
<li>Get (query), replicate, and export table data and create snapshots.</li>
<li>List and invoke the dataset's routines.</li>
</ul>
<p>When granted on a table or view, this role provides these permissions:</p>
<ul>
<li>Get metadata and access controls for the table or view.</li>
<li>Get (query), export, and replicate table data.</li>
<li>Create snapshots.</li>
</ul>
<p>When granted on a routine, this role grants these permissions:</p>
<ul>
<li>In a query, reference a routine created by someone else.</li>
</ul>
<p>This role cannot be granted to individual models.</p>
<blockquote>
<strong>Note:</strong> The BigQuery Data Viewer role is mapped to the <a href="https://docs.cloud.google.com/bigquery/docs/access-control-basic-roles#dataset-basic-roles"><code>READER</code></a> BigQuery basic role. When you grant the BigQuery Data Viewer role to a principal at the dataset level, the principal is granted <code>READER</code> access to the dataset.
</blockquote>
<p>Lowest-level resources where you can grant this role:</p>
<ul>
<li>Dataset</li>
<li>These resources within a dataset:
<ul>
<li>Table</li>
<li>View</li>
<li>Routine</li>
</ul></li>
</ul>
<p>This role can also be granted on Resource Manager resources (projects, folders, and organizations).</p></td>
<td><p><code>bigquery.datasets.get</code></p>
<p><code>bigquery.datasets.getIamPolicy</code></p>
<p><code>bigquery.models.export</code></p>
<p><code>bigquery.models.getData</code></p>
<p><code>bigquery.models.getMetadata</code></p>
<p><code>bigquery.models.list</code></p>
<p><code>bigquery.propertyGraphs.get</code></p>
<p><code>bigquery.propertyGraphs.list</code></p>
<p><code>bigquery.routines.get</code></p>
<p><code>bigquery.routines.list</code></p>
<p><code>bigquery.tables.createSnapshot</code></p>
<p><code>bigquery.tables.export</code></p>
<p><code>bigquery.tables.get</code></p>
<p><code>bigquery.tables.getData</code></p>
<p><code>bigquery.tables.getIamPolicy</code></p>
<p><code>bigquery.tables.list</code></p>
<p><code>bigquery.tables.replicateData</code></p>
<p><code>dataplex.datascans.get</code></p>
<p><code>dataplex.datascans.getData</code></p>
<p><code>dataplex. datascans. getIamPolicy</code></p>
<p><code>dataplex.datascans.list</code></p>
<p><code>resourcemanager.projects.get</code></p>
<p><code>resourcemanager.projects.list</code></p></td>
</tr>
<tr class="odd">
<td>BigQuery Job User
<p>( <code>roles/ bigquery.jobUser</code> )</p>
<p>Provides permissions to run jobs, including queries, within the project.</p>
<p>This role can only be granted on Resource Manager resources (projects, folders, and organizations).</p></td>
<td><p><code>bigquery.config.get</code></p>
<p><code>bigquery.jobs.create</code></p>
<p><code>dataform.folders.create</code></p>
<p><code>dataform.locations.*</code></p>
<ul>
<li><code>dataform.locations.get</code></li>
<li><code>dataform.locations.list</code></li>
</ul>
<p><code>dataform.repositories.create</code></p>
<p><code>dataform.repositories.list</code></p>
<p><code>geminidataanalytics. locations. chat</code></p>
<p><code>resourcemanager.projects.get</code></p>
<p><code>resourcemanager.projects.list</code></p></td>
</tr>
<tr class="even">
<td>BigQuery Metadata Viewer
<p>( <code>roles/ bigquery.metadataViewer</code> )</p>
<p>When granted on a dataset, this role grants these permissions:</p>
<ul>
<li>Get metadata and access controls for the dataset.</li>
<li>Get metadata and access controls for tables and views.</li>
<li>Get metadata from the dataset's models and routines.</li>
<li>List tables, views, models, and routines in the dataset.</li>
</ul>
<p>When granted on a table or view, this role provides these permissions:</p>
<ul>
<li>Get metadata and access controls for the table or view.</li>
</ul>
<p>When granted on a routine, this role grants these permissions:</p>
<ul>
<li>In a query, reference a routine created by someone else.</li>
</ul>
<p>This role cannot be granted to individual models.</p>
<p>Lowest-level resources where you can grant this role:</p>
<ul>
<li>Dataset</li>
<li>These resources within a dataset:
<ul>
<li>Table</li>
<li>View</li>
<li>Routine</li>
</ul></li>
</ul>
<p>This role can also be granted on Resource Manager resources (projects, folders, and organizations).</p></td>
<td><p><code>bigquery.datasets.get</code></p>
<p><code>bigquery.datasets.getIamPolicy</code></p>
<p><code>bigquery.models.getMetadata</code></p>
<p><code>bigquery.models.list</code></p>
<p><code>bigquery.propertyGraphs.get</code></p>
<p><code>bigquery.propertyGraphs.list</code></p>
<p><code>bigquery.routines.get</code></p>
<p><code>bigquery.routines.list</code></p>
<p><code>bigquery.tables.get</code></p>
<p><code>bigquery.tables.getIamPolicy</code></p>
<p><code>bigquery.tables.list</code></p>
<p><code>dataplex.projects.search</code></p>
<p><code>resourcemanager.projects.get</code></p>
<p><code>resourcemanager.projects.list</code></p></td>
</tr>
<tr class="odd">
<td>BigQuery Read Session User
<p>( <code>roles/ bigquery.readSessionUser</code> )</p>
<p>Provides the ability to create and use read sessions.</p>
<p>This role can only be granted on Resource Manager resources (projects, folders, and organizations).</p></td>
<td><p><code>bigquery.readsessions.*</code></p>
<ul>
<li><code>bigquery.readsessions.create</code></li>
<li><code>bigquery.readsessions.getData</code></li>
<li><code>bigquery.readsessions.update</code></li>
</ul>
<p><code>resourcemanager.projects.get</code></p>
<p><code>resourcemanager.projects.list</code></p></td>
</tr>
<tr class="even">
<td>BigQuery Resource Admin
<p>( <code>roles/ bigquery.resourceAdmin</code> )</p>
<p>Administers BigQuery workloads, including slot assignments, commitments, and reservations.</p>
<p>This role can only be granted on Resource Manager resources (projects, folders, and organizations).</p></td>
<td><p><code>bigquery.bireservations.*</code></p>
<ul>
<li><code>bigquery.bireservations.get</code></li>
<li><code>bigquery.bireservations.update</code></li>
</ul>
<p><code>bigquery.capacityCommitments.*</code></p>
<ul>
<li><code>bigquery. capacityCommitments. create</code></li>
<li><code>bigquery. capacityCommitments. delete</code></li>
<li><code>bigquery. capacityCommitments. get</code></li>
<li><code>bigquery. capacityCommitments. list</code></li>
<li><code>bigquery. capacityCommitments. update</code></li>
</ul>
<p><code>bigquery.jobs.get</code></p>
<p><code>bigquery.jobs.list</code></p>
<p><code>bigquery.jobs.listAll</code></p>
<p><code>bigquery. jobs. listExecutionMetadata</code></p>
<p><code>bigquery. reservationAssignments.*</code></p>
<ul>
<li><code>bigquery. reservationAssignments. create</code></li>
<li><code>bigquery. reservationAssignments. delete</code></li>
<li><code>bigquery. reservationAssignments. list</code></li>
<li><code>bigquery. reservationAssignments. search</code></li>
</ul>
<p><code>bigquery.reservationGroups.*</code></p>
<ul>
<li><code>bigquery. reservationGroups. create</code></li>
<li><code>bigquery. reservationGroups. delete</code></li>
<li><code>bigquery.reservationGroups.get</code></li>
<li><code>bigquery. reservationGroups. list</code></li>
<li><code>bigquery. reservationGroups. update</code></li>
</ul>
<p><code>bigquery.reservations.*</code></p>
<ul>
<li><code>bigquery.reservations.create</code></li>
<li><code>bigquery.reservations.delete</code></li>
<li><code>bigquery.reservations.get</code></li>
<li><code>bigquery. reservations. getIamPolicy</code></li>
<li><code>bigquery.reservations.list</code></li>
<li><code>bigquery. reservations. listFailoverDatasets</code></li>
<li><code>bigquery. reservations. setIamPolicy</code></li>
<li><code>bigquery.reservations.update</code></li>
<li><code>bigquery.reservations.use</code></li>
</ul>
<p><code>recommender. bigqueryCapacityCommitmentsInsights.*</code></p>
<ul>
<li><code>recommender. bigqueryCapacityCommitmentsInsights. get</code></li>
<li><code>recommender. bigqueryCapacityCommitmentsInsights. list</code></li>
<li><code>recommender. bigqueryCapacityCommitmentsInsights. update</code></li>
</ul>
<p><code>recommender. bigqueryCapacityCommitmentsRecommendations.*</code></p>
<ul>
<li><code>recommender. bigqueryCapacityCommitmentsRecommendations. get</code></li>
<li><code>recommender. bigqueryCapacityCommitmentsRecommendations. list</code></li>
<li><code>recommender. bigqueryCapacityCommitmentsRecommendations. update</code></li>
</ul>
<p><code>resourcemanager.projects.get</code></p>
<p><code>resourcemanager.projects.list</code></p></td>
</tr>
<tr class="odd">
<td>BigQuery Resource Editor
<p>( <code>roles/ bigquery.resourceEditor</code> )</p>
<p>Manages BigQuery workloads, but is unable to create or modify slot commitments.</p>
<p>This role can only be granted on Resource Manager resources (projects, folders, and organizations).</p></td>
<td><p><code>bigquery.bireservations.get</code></p>
<p><code>bigquery. capacityCommitments. get</code></p>
<p><code>bigquery. capacityCommitments. list</code></p>
<p><code>bigquery.jobs.get</code></p>
<p><code>bigquery.jobs.list</code></p>
<p><code>bigquery.jobs.listAll</code></p>
<p><code>bigquery. jobs. listExecutionMetadata</code></p>
<p><code>bigquery. reservationAssignments.*</code></p>
<ul>
<li><code>bigquery. reservationAssignments. create</code></li>
<li><code>bigquery. reservationAssignments. delete</code></li>
<li><code>bigquery. reservationAssignments. list</code></li>
<li><code>bigquery. reservationAssignments. search</code></li>
</ul>
<p><code>bigquery.reservationGroups.*</code></p>
<ul>
<li><code>bigquery. reservationGroups. create</code></li>
<li><code>bigquery. reservationGroups. delete</code></li>
<li><code>bigquery.reservationGroups.get</code></li>
<li><code>bigquery. reservationGroups. list</code></li>
<li><code>bigquery. reservationGroups. update</code></li>
</ul>
<p><code>bigquery.reservations.create</code></p>
<p><code>bigquery.reservations.delete</code></p>
<p><code>bigquery.reservations.get</code></p>
<p><code>bigquery.reservations.list</code></p>
<p><code>bigquery. reservations. listFailoverDatasets</code></p>
<p><code>bigquery.reservations.update</code></p>
<p><code>bigquery.reservations.use</code></p>
<p><code>resourcemanager.projects.get</code></p>
<p><code>resourcemanager.projects.list</code></p></td>
</tr>
<tr class="even">
<td>BigQuery Resource Viewer
<p>( <code>roles/ bigquery.resourceViewer</code> )</p>
<p>Can view BigQuery workloads, but cannot create or modify slot reservations or commitments.</p>
<p>This role can only be granted on Resource Manager resources (projects, folders, and organizations).</p></td>
<td><p><code>bigquery.bireservations.get</code></p>
<p><code>bigquery. capacityCommitments. get</code></p>
<p><code>bigquery. capacityCommitments. list</code></p>
<p><code>bigquery.jobs.get</code></p>
<p><code>bigquery.jobs.list</code></p>
<p><code>bigquery.jobs.listAll</code></p>
<p><code>bigquery. jobs. listExecutionMetadata</code></p>
<p><code>bigquery. reservationAssignments. list</code></p>
<p><code>bigquery. reservationAssignments. search</code></p>
<p><code>bigquery.reservationGroups.get</code></p>
<p><code>bigquery. reservationGroups. list</code></p>
<p><code>bigquery.reservations.get</code></p>
<p><code>bigquery.reservations.list</code></p>
<p><code>bigquery. reservations. listFailoverDatasets</code></p>
<p><code>resourcemanager.projects.get</code></p>
<p><code>resourcemanager.projects.list</code></p></td>
</tr>
<tr class="odd">
<td>BigQuery Studio Admin
<p>( <code>roles/ bigquery.studioAdmin</code> )</p>
<p>Combination role of BigQuery Admin, Dataform Admin, Notebook Runtime Admin and Dataproc Serverless Editor.</p>
<p>It is possible to grant this role to the following lowest-level resources, but it is not recommended. Other predefined roles grant full permissions over these resources and are less permissive. BigQuery Studio Admin is typically granted at the project level.</p>
<p>Lowest-level resources where you can grant this role:</p>
<ul>
<li>Dataset</li>
<li>These resources within a dataset:
<ul>
<li>Table</li>
<li>View</li>
<li>Routine</li>
</ul></li>
<li>Connection</li>
<li>Saved query</li>
<li>Data canvas</li>
<li>Data preparation</li>
<li>Pipeline</li>
<li>Repository</li>
</ul>
<p>This role can also be granted on Resource Manager resources (projects, folders, and organizations).</p></td>
<td><p><code>aiplatform.locations.get</code></p>
<p><code>aiplatform. notebookRuntimeTemplates.*</code></p>
<ul>
<li><code>aiplatform. notebookRuntimeTemplates. apply</code></li>
<li><code>aiplatform. notebookRuntimeTemplates. create</code></li>
<li><code>aiplatform. notebookRuntimeTemplates. delete</code></li>
<li><code>aiplatform. notebookRuntimeTemplates. get</code></li>
<li><code>aiplatform. notebookRuntimeTemplates. getIamPolicy</code></li>
<li><code>aiplatform. notebookRuntimeTemplates. list</code></li>
<li><code>aiplatform. notebookRuntimeTemplates. setDefault</code></li>
<li><code>aiplatform. notebookRuntimeTemplates. setIamPolicy</code></li>
<li><code>aiplatform. notebookRuntimeTemplates. update</code></li>
</ul>
<p><code>aiplatform.notebookRuntimes.*</code></p>
<ul>
<li><code>aiplatform. notebookRuntimes. assign</code></li>
<li><code>aiplatform. notebookRuntimes. delete</code></li>
<li><code>aiplatform. notebookRuntimes. get</code></li>
<li><code>aiplatform. notebookRuntimes. list</code></li>
<li><code>aiplatform. notebookRuntimes. start</code></li>
<li><code>aiplatform. notebookRuntimes. update</code></li>
<li><code>aiplatform. notebookRuntimes. upgrade</code></li>
</ul>
<p><code>aiplatform.operations.list</code></p>
<p><code>bigquery.bireservations.*</code></p>
<ul>
<li><code>bigquery.bireservations.get</code></li>
<li><code>bigquery.bireservations.update</code></li>
</ul>
<p><code>bigquery.capacityCommitments.*</code></p>
<ul>
<li><code>bigquery. capacityCommitments. create</code></li>
<li><code>bigquery. capacityCommitments. delete</code></li>
<li><code>bigquery. capacityCommitments. get</code></li>
<li><code>bigquery. capacityCommitments. list</code></li>
<li><code>bigquery. capacityCommitments. update</code></li>
</ul>
<p><code>bigquery.config.*</code></p>
<ul>
<li><code>bigquery.config.get</code></li>
<li><code>bigquery.config.update</code></li>
</ul>
<p><code>bigquery.connections.*</code></p>
<ul>
<li><code>bigquery.connections.create</code></li>
<li><code>bigquery.connections.delegate</code></li>
<li><code>bigquery.connections.delete</code></li>
<li><code>bigquery.connections.get</code></li>
<li><code>bigquery. connections. getIamPolicy</code></li>
<li><code>bigquery.connections.list</code></li>
<li><code>bigquery. connections. setIamPolicy</code></li>
<li><code>bigquery.connections.update</code></li>
<li><code>bigquery.connections.updateTag</code></li>
<li><code>bigquery.connections.use</code></li>
</ul>
<p><code>bigquery.dataPolicies.attach</code></p>
<p><code>bigquery.dataPolicies.create</code></p>
<p><code>bigquery.dataPolicies.delete</code></p>
<p><code>bigquery.dataPolicies.get</code></p>
<p><code>bigquery. dataPolicies. getIamPolicy</code></p>
<p><code>bigquery.dataPolicies.list</code></p>
<p><code>bigquery. dataPolicies. setIamPolicy</code></p>
<p><code>bigquery.dataPolicies.update</code></p>
<p><code>bigquery.datasets.*</code></p>
<ul>
<li><code>bigquery.datasets.create</code></li>
<li><code>bigquery. datasets. createTagBinding</code></li>
<li><code>bigquery.datasets.delete</code></li>
<li><code>bigquery. datasets. deleteTagBinding</code></li>
<li><code>bigquery.datasets.get</code></li>
<li><code>bigquery.datasets.getIamPolicy</code></li>
<li><code>bigquery.datasets.link</code></li>
<li><code>bigquery. datasets. listEffectiveTags</code></li>
<li><code>bigquery. datasets. listSharedDatasetUsage</code></li>
<li><code>bigquery. datasets. listTagBindings</code></li>
<li><code>bigquery.datasets.setIamPolicy</code></li>
<li><code>bigquery.datasets.update</code></li>
<li><code>bigquery.datasets.updateTag</code></li>
</ul>
<p><code>bigquery.jobs.*</code></p>
<ul>
<li><code>bigquery.jobs.create</code></li>
<li><code>bigquery. jobs. createGlobalQuery</code></li>
<li><code>bigquery.jobs.delete</code></li>
<li><code>bigquery.jobs.get</code></li>
<li><code>bigquery.jobs.list</code></li>
<li><code>bigquery.jobs.listAll</code></li>
<li><code>bigquery. jobs. listExecutionMetadata</code></li>
<li><code>bigquery.jobs.update</code></li>
</ul>
<p><code>bigquery.models.*</code></p>
<ul>
<li><code>bigquery.models.create</code></li>
<li><code>bigquery.models.delete</code></li>
<li><code>bigquery.models.export</code></li>
<li><code>bigquery.models.getData</code></li>
<li><code>bigquery.models.getMetadata</code></li>
<li><code>bigquery.models.list</code></li>
<li><code>bigquery.models.updateData</code></li>
<li><code>bigquery.models.updateMetadata</code></li>
<li><code>bigquery.models.updateTag</code></li>
</ul>
<p><code>bigquery.objectRefs.*</code></p>
<ul>
<li><code>bigquery.objectRefs.read</code></li>
<li><code>bigquery.objectRefs.write</code></li>
</ul>
<p><code>bigquery.propertyGraphs.*</code></p>
<ul>
<li><code>bigquery.propertyGraphs.create</code></li>
<li><code>bigquery.propertyGraphs.delete</code></li>
<li><code>bigquery.propertyGraphs.get</code></li>
<li><code>bigquery.propertyGraphs.list</code></li>
<li><code>bigquery.propertyGraphs.update</code></li>
</ul>
<p><code>bigquery.readsessions.*</code></p>
<ul>
<li><code>bigquery.readsessions.create</code></li>
<li><code>bigquery.readsessions.getData</code></li>
<li><code>bigquery.readsessions.update</code></li>
</ul>
<p><code>bigquery. reservationAssignments.*</code></p>
<ul>
<li><code>bigquery. reservationAssignments. create</code></li>
<li><code>bigquery. reservationAssignments. delete</code></li>
<li><code>bigquery. reservationAssignments. list</code></li>
<li><code>bigquery. reservationAssignments. search</code></li>
</ul>
<p><code>bigquery.reservationGroups.*</code></p>
<ul>
<li><code>bigquery. reservationGroups. create</code></li>
<li><code>bigquery. reservationGroups. delete</code></li>
<li><code>bigquery.reservationGroups.get</code></li>
<li><code>bigquery. reservationGroups. list</code></li>
<li><code>bigquery. reservationGroups. update</code></li>
</ul>
<p><code>bigquery.reservations.*</code></p>
<ul>
<li><code>bigquery.reservations.create</code></li>
<li><code>bigquery.reservations.delete</code></li>
<li><code>bigquery.reservations.get</code></li>
<li><code>bigquery. reservations. getIamPolicy</code></li>
<li><code>bigquery.reservations.list</code></li>
<li><code>bigquery. reservations. listFailoverDatasets</code></li>
<li><code>bigquery. reservations. setIamPolicy</code></li>
<li><code>bigquery.reservations.update</code></li>
<li><code>bigquery.reservations.use</code></li>
</ul>
<p><code>bigquery.routines.*</code></p>
<ul>
<li><code>bigquery.routines.create</code></li>
<li><code>bigquery.routines.delete</code></li>
<li><code>bigquery.routines.get</code></li>
<li><code>bigquery.routines.list</code></li>
<li><code>bigquery.routines.update</code></li>
<li><code>bigquery.routines.updateTag</code></li>
</ul>
<p><code>bigquery. rowAccessPolicies. create</code></p>
<p><code>bigquery. rowAccessPolicies. delete</code></p>
<p><code>bigquery.rowAccessPolicies.get</code></p>
<p><code>bigquery. rowAccessPolicies. getIamPolicy</code></p>
<p><code>bigquery. rowAccessPolicies. list</code></p>
<p><code>bigquery. rowAccessPolicies. overrideTimeTravelRestrictions</code></p>
<p><code>bigquery. rowAccessPolicies. setIamPolicy</code></p>
<p><code>bigquery. rowAccessPolicies. update</code></p>
<p><code>bigquery.savedqueries.*</code></p>
<ul>
<li><code>bigquery.savedqueries.create</code></li>
<li><code>bigquery.savedqueries.delete</code></li>
<li><code>bigquery.savedqueries.get</code></li>
<li><code>bigquery.savedqueries.list</code></li>
<li><code>bigquery.savedqueries.update</code></li>
</ul>
<p><code>bigquery.tables.*</code></p>
<ul>
<li><code>bigquery.tables.create</code></li>
<li><code>bigquery.tables.createIndex</code></li>
<li><code>bigquery.tables.createSnapshot</code></li>
<li><code>bigquery. tables. createTagBinding</code></li>
<li><code>bigquery.tables.delete</code></li>
<li><code>bigquery.tables.deleteIndex</code></li>
<li><code>bigquery.tables.deleteSnapshot</code></li>
<li><code>bigquery. tables. deleteTagBinding</code></li>
<li><code>bigquery.tables.export</code></li>
<li><code>bigquery.tables.get</code></li>
<li><code>bigquery.tables.getData</code></li>
<li><code>bigquery.tables.getIamPolicy</code></li>
<li><code>bigquery.tables.list</code></li>
<li><code>bigquery. tables. listEffectiveTags</code></li>
<li><code>bigquery. tables. listTagBindings</code></li>
<li><code>bigquery.tables.replicateData</code></li>
<li><code>bigquery. tables. restoreSnapshot</code></li>
<li><code>bigquery.tables.setCategory</code></li>
<li><code>bigquery. tables. setColumnDataPolicy</code></li>
<li><code>bigquery.tables.setIamPolicy</code></li>
<li><code>bigquery.tables.update</code></li>
<li><code>bigquery.tables.updateData</code></li>
<li><code>bigquery.tables.updateIndex</code></li>
<li><code>bigquery.tables.updateTag</code></li>
</ul>
<p><code>bigquery.transfers.*</code></p>
<ul>
<li><code>bigquery.transfers.get</code></li>
<li><code>bigquery.transfers.update</code></li>
</ul>
<p><code>bigquerymigration. translation. translate</code></p>
<p><code>cloudaicompanion. aiDevToolsSettings.*</code></p>
<ul>
<li><code>cloudaicompanion. aiDevToolsSettings. create</code></li>
<li><code>cloudaicompanion. aiDevToolsSettings. delete</code></li>
<li><code>cloudaicompanion. aiDevToolsSettings. get</code></li>
<li><code>cloudaicompanion. aiDevToolsSettings. list</code></li>
<li><code>cloudaicompanion. aiDevToolsSettings. update</code></li>
</ul>
<p><code>cloudaicompanion. codeToolsSettings.*</code></p>
<ul>
<li><code>cloudaicompanion. codeToolsSettings. create</code></li>
<li><code>cloudaicompanion. codeToolsSettings. delete</code></li>
<li><code>cloudaicompanion. codeToolsSettings. get</code></li>
<li><code>cloudaicompanion. codeToolsSettings. list</code></li>
<li><code>cloudaicompanion. codeToolsSettings. update</code></li>
</ul>
<p><code>cloudaicompanion.companions.*</code></p>
<ul>
<li><code>cloudaicompanion. companions. generateChat</code></li>
<li><code>cloudaicompanion. companions. generateCode</code></li>
</ul>
<p><code>cloudaicompanion. dataSharingWithGoogleSettings.*</code></p>
<ul>
<li><code>cloudaicompanion. dataSharingWithGoogleSettings. create</code></li>
<li><code>cloudaicompanion. dataSharingWithGoogleSettings. delete</code></li>
<li><code>cloudaicompanion. dataSharingWithGoogleSettings. get</code></li>
<li><code>cloudaicompanion. dataSharingWithGoogleSettings. list</code></li>
<li><code>cloudaicompanion. dataSharingWithGoogleSettings. update</code></li>
</ul>
<p><code>cloudaicompanion. entitlements. get</code></p>
<p><code>cloudaicompanion. geminiGcpEnablementSettings.*</code></p>
<ul>
<li><code>cloudaicompanion. geminiGcpEnablementSettings. create</code></li>
<li><code>cloudaicompanion. geminiGcpEnablementSettings. delete</code></li>
<li><code>cloudaicompanion. geminiGcpEnablementSettings. get</code></li>
<li><code>cloudaicompanion. geminiGcpEnablementSettings. list</code></li>
<li><code>cloudaicompanion. geminiGcpEnablementSettings. update</code></li>
</ul>
<p><code>cloudaicompanion. gibqObservabilitySettings.*</code></p>
<ul>
<li><code>cloudaicompanion. gibqObservabilitySettings. create</code></li>
<li><code>cloudaicompanion. gibqObservabilitySettings. delete</code></li>
<li><code>cloudaicompanion. gibqObservabilitySettings. get</code></li>
<li><code>cloudaicompanion. gibqObservabilitySettings. list</code></li>
<li><code>cloudaicompanion. gibqObservabilitySettings. update</code></li>
</ul>
<p><code>cloudaicompanion.instances.*</code></p>
<ul>
<li><code>cloudaicompanion. instances. completeCode</code></li>
<li><code>cloudaicompanion. instances. completeTask</code></li>
<li><code>cloudaicompanion. instances. exportMetrics</code></li>
<li><code>cloudaicompanion. instances. generateCode</code></li>
<li><code>cloudaicompanion. instances. generateText</code></li>
<li><code>cloudaicompanion. instances. queryEffectiveSetting</code></li>
<li><code>cloudaicompanion. instances. queryEffectiveSettingBindings</code></li>
</ul>
<p><code>cloudaicompanion. licenses. selfAssign</code></p>
<p><code>cloudaicompanion. loggingSettings.*</code></p>
<ul>
<li><code>cloudaicompanion. loggingSettings. create</code></li>
<li><code>cloudaicompanion. loggingSettings. delete</code></li>
<li><code>cloudaicompanion. loggingSettings. get</code></li>
<li><code>cloudaicompanion. loggingSettings. list</code></li>
<li><code>cloudaicompanion. loggingSettings. update</code></li>
</ul>
<p><code>cloudaicompanion. operations. get</code></p>
<p><code>cloudaicompanion. releaseChannelSettings.*</code></p>
<ul>
<li><code>cloudaicompanion. releaseChannelSettings. create</code></li>
<li><code>cloudaicompanion. releaseChannelSettings. delete</code></li>
<li><code>cloudaicompanion. releaseChannelSettings. get</code></li>
<li><code>cloudaicompanion. releaseChannelSettings. list</code></li>
<li><code>cloudaicompanion. releaseChannelSettings. update</code></li>
</ul>
<p><code>cloudaicompanion. settingBindings.*</code></p>
<ul>
<li><code>cloudaicompanion. settingBindings. aiDevToolsSettingsCreate</code></li>
<li><code>cloudaicompanion. settingBindings. aiDevToolsSettingsDelete</code></li>
<li><code>cloudaicompanion. settingBindings. aiDevToolsSettingsGet</code></li>
<li><code>cloudaicompanion. settingBindings. aiDevToolsSettingsList</code></li>
<li><code>cloudaicompanion. settingBindings. aiDevToolsSettingsUpdate</code></li>
<li><code>cloudaicompanion. settingBindings. aiDevToolsSettingsUse</code></li>
<li><code>cloudaicompanion. settingBindings. codeToolsSettingsCreate</code></li>
<li><code>cloudaicompanion. settingBindings. codeToolsSettingsDelete</code></li>
<li><code>cloudaicompanion. settingBindings. codeToolsSettingsGet</code></li>
<li><code>cloudaicompanion. settingBindings. codeToolsSettingsList</code></li>
<li><code>cloudaicompanion. settingBindings. codeToolsSettingsUpdate</code></li>
<li><code>cloudaicompanion. settingBindings. codeToolsSettingsUse</code></li>
<li><code>cloudaicompanion. settingBindings. dataSharingWithGoogleSettingsCreate</code></li>
<li><code>cloudaicompanion. settingBindings. dataSharingWithGoogleSettingsDelete</code></li>
<li><code>cloudaicompanion. settingBindings. dataSharingWithGoogleSettingsGet</code></li>
<li><code>cloudaicompanion. settingBindings. dataSharingWithGoogleSettingsList</code></li>
<li><code>cloudaicompanion. settingBindings. dataSharingWithGoogleSettingsUpdate</code></li>
<li><code>cloudaicompanion. settingBindings. dataSharingWithGoogleSettingsUse</code></li>
<li><code>cloudaicompanion. settingBindings. geminiGcpEnablementSettingsCreate</code></li>
<li><code>cloudaicompanion. settingBindings. geminiGcpEnablementSettingsDelete</code></li>
<li><code>cloudaicompanion. settingBindings. geminiGcpEnablementSettingsGet</code></li>
<li><code>cloudaicompanion. settingBindings. geminiGcpEnablementSettingsList</code></li>
<li><code>cloudaicompanion. settingBindings. geminiGcpEnablementSettingsUpdate</code></li>
<li><code>cloudaicompanion. settingBindings. geminiGcpEnablementSettingsUse</code></li>
<li><code>cloudaicompanion. settingBindings. gibqObservabilitySettingsCreate</code></li>
<li><code>cloudaicompanion. settingBindings. gibqObservabilitySettingsDelete</code></li>
<li><code>cloudaicompanion. settingBindings. gibqObservabilitySettingsGet</code></li>
<li><code>cloudaicompanion. settingBindings. gibqObservabilitySettingsList</code></li>
<li><code>cloudaicompanion. settingBindings. gibqObservabilitySettingsUpdate</code></li>
<li><code>cloudaicompanion. settingBindings. gibqObservabilitySettingsUse</code></li>
<li><code>cloudaicompanion. settingBindings. loggingSettingsCreate</code></li>
<li><code>cloudaicompanion. settingBindings. loggingSettingsDelete</code></li>
<li><code>cloudaicompanion. settingBindings. loggingSettingsGet</code></li>
<li><code>cloudaicompanion. settingBindings. loggingSettingsList</code></li>
<li><code>cloudaicompanion. settingBindings. loggingSettingsUpdate</code></li>
<li><code>cloudaicompanion. settingBindings. loggingSettingsUse</code></li>
<li><code>cloudaicompanion. settingBindings. releaseChannelSettingsCreate</code></li>
<li><code>cloudaicompanion. settingBindings. releaseChannelSettingsDelete</code></li>
<li><code>cloudaicompanion. settingBindings. releaseChannelSettingsGet</code></li>
<li><code>cloudaicompanion. settingBindings. releaseChannelSettingsList</code></li>
<li><code>cloudaicompanion. settingBindings. releaseChannelSettingsUpdate</code></li>
<li><code>cloudaicompanion. settingBindings. releaseChannelSettingsUse</code></li>
</ul>
<p><code>cloudaicompanion.topics.create</code></p>
<p><code>cloudkms.keyHandles.*</code></p>
<ul>
<li><code>cloudkms.keyHandles.create</code></li>
<li><code>cloudkms.keyHandles.get</code></li>
<li><code>cloudkms.keyHandles.list</code></li>
</ul>
<p><code>cloudkms.operations.get</code></p>
<p><code>cloudkms. projects. showEffectiveAutokeyConfig</code></p>
<p><code>compute.projects.get</code></p>
<p><code>compute.regions.*</code></p>
<ul>
<li><code>compute.regions.get</code></li>
<li><code>compute.regions.list</code></li>
</ul>
<p><code>compute.reservations.get</code></p>
<p><code>compute.reservations.list</code></p>
<p><code>compute.zones.*</code></p>
<ul>
<li><code>compute.zones.get</code></li>
<li><code>compute.zones.list</code></li>
</ul>
<p><code>dataform.*</code></p>
<ul>
<li><code>dataform.commentThreads.create</code></li>
<li><code>dataform.commentThreads.delete</code></li>
<li><code>dataform.commentThreads.get</code></li>
<li><code>dataform.commentThreads.list</code></li>
<li><code>dataform.commentThreads.update</code></li>
<li><code>dataform.comments.create</code></li>
<li><code>dataform.comments.delete</code></li>
<li><code>dataform.comments.get</code></li>
<li><code>dataform.comments.list</code></li>
<li><code>dataform.comments.update</code></li>
<li><code>dataform. compilationResults. create</code></li>
<li><code>dataform. compilationResults. get</code></li>
<li><code>dataform. compilationResults. list</code></li>
<li><code>dataform. compilationResults. query</code></li>
<li><code>dataform.config.get</code></li>
<li><code>dataform.config.update</code></li>
<li><code>dataform.folders.addContents</code></li>
<li><code>dataform.folders.create</code></li>
<li><code>dataform.folders.delete</code></li>
<li><code>dataform.folders.deleteTree</code></li>
<li><code>dataform.folders.get</code></li>
<li><code>dataform.folders.getIamPolicy</code></li>
<li><code>dataform.folders.move</code></li>
<li><code>dataform.folders.queryContents</code></li>
<li><code>dataform.folders.setIamPolicy</code></li>
<li><code>dataform.folders.update</code></li>
<li><code>dataform.locations.get</code></li>
<li><code>dataform.locations.list</code></li>
<li><code>dataform.operations.cancel</code></li>
<li><code>dataform.operations.delete</code></li>
<li><code>dataform.operations.get</code></li>
<li><code>dataform.operations.list</code></li>
<li><code>dataform.releaseConfigs.create</code></li>
<li><code>dataform.releaseConfigs.delete</code></li>
<li><code>dataform.releaseConfigs.get</code></li>
<li><code>dataform.releaseConfigs.list</code></li>
<li><code>dataform.releaseConfigs.update</code></li>
<li><code>dataform.repositories.commit</code></li>
<li><code>dataform. repositories. computeAccessTokenStatus</code></li>
<li><code>dataform.repositories.create</code></li>
<li><code>dataform. repositories. createTagBinding</code></li>
<li><code>dataform.repositories.delete</code></li>
<li><code>dataform. repositories. deleteTagBinding</code></li>
<li><code>dataform. repositories. fetchHistory</code></li>
<li><code>dataform. repositories. fetchRemoteBranches</code></li>
<li><code>dataform.repositories.get</code></li>
<li><code>dataform. repositories. getIamPolicy</code></li>
<li><code>dataform.repositories.list</code></li>
<li><code>dataform. repositories. listEffectiveTags</code></li>
<li><code>dataform. repositories. listTagBindings</code></li>
<li><code>dataform.repositories.move</code></li>
<li><code>dataform. repositories. queryDirectoryContents</code></li>
<li><code>dataform.repositories.readFile</code></li>
<li><code>dataform. repositories. scheduleRelease</code></li>
<li><code>dataform. repositories. scheduleWorkflow</code></li>
<li><code>dataform. repositories. setIamPolicy</code></li>
<li><code>dataform.repositories.update</code></li>
<li><code>dataform.teamFolders.create</code></li>
<li><code>dataform.teamFolders.delete</code></li>
<li><code>dataform. teamFolders. deleteTree</code></li>
<li><code>dataform.teamFolders.get</code></li>
<li><code>dataform. teamFolders. getIamPolicy</code></li>
<li><code>dataform. teamFolders. setIamPolicy</code></li>
<li><code>dataform.teamFolders.update</code></li>
<li><code>dataform. workflowConfigs. create</code></li>
<li><code>dataform. workflowConfigs. delete</code></li>
<li><code>dataform.workflowConfigs.get</code></li>
<li><code>dataform.workflowConfigs.list</code></li>
<li><code>dataform. workflowConfigs. update</code></li>
<li><code>dataform. workflowInvocations. cancel</code></li>
<li><code>dataform. workflowInvocations. create</code></li>
<li><code>dataform. workflowInvocations. delete</code></li>
<li><code>dataform. workflowInvocations. get</code></li>
<li><code>dataform. workflowInvocations. list</code></li>
<li><code>dataform. workflowInvocations. query</code></li>
<li><code>dataform.workspaces.commit</code></li>
<li><code>dataform.workspaces.create</code></li>
<li><code>dataform.workspaces.delete</code></li>
<li><code>dataform. workspaces. fetchFileDiff</code></li>
<li><code>dataform. workspaces. fetchFileGitStatuses</code></li>
<li><code>dataform. workspaces. fetchGitAheadBehind</code></li>
<li><code>dataform.workspaces.get</code></li>
<li><code>dataform. workspaces. getIamPolicy</code></li>
<li><code>dataform. workspaces. installNpmPackages</code></li>
<li><code>dataform.workspaces.list</code></li>
<li><code>dataform. workspaces. makeDirectory</code></li>
<li><code>dataform. workspaces. moveDirectory</code></li>
<li><code>dataform.workspaces.moveFile</code></li>
<li><code>dataform.workspaces.pull</code></li>
<li><code>dataform.workspaces.push</code></li>
<li><code>dataform. workspaces. queryDirectoryContents</code></li>
<li><code>dataform.workspaces.readFile</code></li>
<li><code>dataform. workspaces. removeDirectory</code></li>
<li><code>dataform.workspaces.removeFile</code></li>
<li><code>dataform.workspaces.reset</code></li>
<li><code>dataform. workspaces. searchFiles</code></li>
<li><code>dataform. workspaces. setIamPolicy</code></li>
<li><code>dataform.workspaces.writeFile</code></li>
</ul>
<p><code>dataplex.datascans.*</code></p>
<ul>
<li><code>dataplex.datascans.cancel</code></li>
<li><code>dataplex.datascans.create</code></li>
<li><code>dataplex.datascans.delete</code></li>
<li><code>dataplex.datascans.get</code></li>
<li><code>dataplex.datascans.getData</code></li>
<li><code>dataplex. datascans. getIamPolicy</code></li>
<li><code>dataplex.datascans.list</code></li>
<li><code>dataplex.datascans.run</code></li>
<li><code>dataplex. datascans. setIamPolicy</code></li>
<li><code>dataplex.datascans.update</code></li>
</ul>
<p><code>dataplex.operations.get</code></p>
<p><code>dataplex.operations.list</code></p>
<p><code>dataplex.projects.search</code></p>
<p><code>dataproc.batches.analyze</code></p>
<p><code>dataproc.batches.cancel</code></p>
<p><code>dataproc.batches.create</code></p>
<p><code>dataproc.batches.delete</code></p>
<p><code>dataproc.batches.get</code></p>
<p><code>dataproc.batches.list</code></p>
<p><code>dataproc. batches. sparkApplicationRead</code></p>
<p><code>dataproc. batches. sparkApplicationWrite</code></p>
<p><code>dataproc.operations.cancel</code></p>
<p><code>dataproc.operations.delete</code></p>
<p><code>dataproc.operations.get</code></p>
<p><code>dataproc.operations.list</code></p>
<p><code>dataproc.sessionTemplates.*</code></p>
<ul>
<li><code>dataproc. sessionTemplates. create</code></li>
<li><code>dataproc. sessionTemplates. delete</code></li>
<li><code>dataproc.sessionTemplates.get</code></li>
<li><code>dataproc.sessionTemplates.list</code></li>
<li><code>dataproc. sessionTemplates. update</code></li>
</ul>
<p><code>dataproc.sessions.*</code></p>
<ul>
<li><code>dataproc.sessions.create</code></li>
<li><code>dataproc.sessions.delete</code></li>
<li><code>dataproc.sessions.get</code></li>
<li><code>dataproc.sessions.list</code></li>
<li><code>dataproc. sessions. sparkApplicationRead</code></li>
<li><code>dataproc. sessions. sparkApplicationWrite</code></li>
<li><code>dataproc.sessions.terminate</code></li>
</ul>
<p><code>dataprocrm.nodePools.*</code></p>
<ul>
<li><code>dataprocrm.nodePools.create</code></li>
<li><code>dataprocrm.nodePools.delete</code></li>
<li><code>dataprocrm. nodePools. deleteNodes</code></li>
<li><code>dataprocrm.nodePools.get</code></li>
<li><code>dataprocrm.nodePools.list</code></li>
<li><code>dataprocrm.nodePools.resize</code></li>
</ul>
<p><code>dataprocrm.nodes.get</code></p>
<p><code>dataprocrm.nodes.heartbeat</code></p>
<p><code>dataprocrm.nodes.list</code></p>
<p><code>dataprocrm.nodes.update</code></p>
<p><code>dataprocrm.operations.get</code></p>
<p><code>dataprocrm.operations.list</code></p>
<p><code>dataprocrm.workloads.*</code></p>
<ul>
<li><code>dataprocrm.workloads.cancel</code></li>
<li><code>dataprocrm.workloads.create</code></li>
<li><code>dataprocrm.workloads.delete</code></li>
<li><code>dataprocrm.workloads.get</code></li>
<li><code>dataprocrm.workloads.list</code></li>
</ul>
<p><code>geminicloudassist. agents. invoke</code></p>
<p><code>geminidataanalytics.*</code></p>
<ul>
<li><code>geminidataanalytics. dataAgents. chat</code></li>
<li><code>geminidataanalytics. dataAgents. create</code></li>
<li><code>geminidataanalytics. dataAgents. delete</code></li>
<li><code>geminidataanalytics. dataAgents. get</code></li>
<li><code>geminidataanalytics. dataAgents. getIamPolicy</code></li>
<li><code>geminidataanalytics. dataAgents. list</code></li>
<li><code>geminidataanalytics. dataAgents. setIamPolicy</code></li>
<li><code>geminidataanalytics. dataAgents. update</code></li>
<li><code>geminidataanalytics. locations. chat</code></li>
<li><code>geminidataanalytics. locations. get</code></li>
<li><code>geminidataanalytics. locations. list</code></li>
<li><code>geminidataanalytics. locations. useDataEngineeringAgent</code></li>
<li><code>geminidataanalytics. operations. cancel</code></li>
<li><code>geminidataanalytics. operations. delete</code></li>
<li><code>geminidataanalytics. operations. get</code></li>
<li><code>geminidataanalytics. operations. list</code></li>
</ul>
<p><code>resourcemanager.projects.get</code></p>
<p><code>resourcemanager.projects.list</code></p></td>
</tr>
<tr class="even">
<td>BigQuery Studio User
<p>( <code>roles/ bigquery.studioUser</code> )</p>
<p>Combination role of BigQuery Job User, BigQuery Read Session User, Dataform Code Creator, Notebook Runtime User and Dataproc Serverless Editor.</p>
<p>Lowest-level resources where you can grant this role:</p>
<ul>
<li>Saved query</li>
<li>Data canvas</li>
<li>Data preparation</li>
<li>Pipeline</li>
<li>Repository</li>
</ul>
<p>This role can also be granted on Resource Manager resources (projects, folders, and organizations).</p></td>
<td><p><code>aiplatform.locations.get</code></p>
<p><code>aiplatform. notebookRuntimeTemplates. apply</code></p>
<p><code>aiplatform. notebookRuntimeTemplates. get</code></p>
<p><code>aiplatform. notebookRuntimeTemplates. getIamPolicy</code></p>
<p><code>aiplatform. notebookRuntimeTemplates. list</code></p>
<p><code>aiplatform. notebookRuntimes. assign</code></p>
<p><code>aiplatform. notebookRuntimes. get</code></p>
<p><code>aiplatform. notebookRuntimes. list</code></p>
<p><code>aiplatform.operations.list</code></p>
<p><code>bigquery.config.get</code></p>
<p><code>bigquery.jobs.create</code></p>
<p><code>bigquery.readsessions.*</code></p>
<ul>
<li><code>bigquery.readsessions.create</code></li>
<li><code>bigquery.readsessions.getData</code></li>
<li><code>bigquery.readsessions.update</code></li>
</ul>
<p><code>cloudaicompanion.companions.*</code></p>
<ul>
<li><code>cloudaicompanion. companions. generateChat</code></li>
<li><code>cloudaicompanion. companions. generateCode</code></li>
</ul>
<p><code>cloudaicompanion. entitlements. get</code></p>
<p><code>cloudaicompanion.instances.*</code></p>
<ul>
<li><code>cloudaicompanion. instances. completeCode</code></li>
<li><code>cloudaicompanion. instances. completeTask</code></li>
<li><code>cloudaicompanion. instances. exportMetrics</code></li>
<li><code>cloudaicompanion. instances. generateCode</code></li>
<li><code>cloudaicompanion. instances. generateText</code></li>
<li><code>cloudaicompanion. instances. queryEffectiveSetting</code></li>
<li><code>cloudaicompanion. instances. queryEffectiveSettingBindings</code></li>
</ul>
<p><code>cloudaicompanion. licenses. selfAssign</code></p>
<p><code>cloudaicompanion. operations. get</code></p>
<p><code>cloudaicompanion.topics.create</code></p>
<p><code>cloudkms.keyHandles.*</code></p>
<ul>
<li><code>cloudkms.keyHandles.create</code></li>
<li><code>cloudkms.keyHandles.get</code></li>
<li><code>cloudkms.keyHandles.list</code></li>
</ul>
<p><code>cloudkms.operations.get</code></p>
<p><code>cloudkms. projects. showEffectiveAutokeyConfig</code></p>
<p><code>compute.projects.get</code></p>
<p><code>compute.regions.*</code></p>
<ul>
<li><code>compute.regions.get</code></li>
<li><code>compute.regions.list</code></li>
</ul>
<p><code>compute.zones.*</code></p>
<ul>
<li><code>compute.zones.get</code></li>
<li><code>compute.zones.list</code></li>
</ul>
<p><code>dataform.commentThreads.get</code></p>
<p><code>dataform.commentThreads.list</code></p>
<p><code>dataform.comments.get</code></p>
<p><code>dataform.comments.list</code></p>
<p><code>dataform.folders.create</code></p>
<p><code>dataform.locations.*</code></p>
<ul>
<li><code>dataform.locations.get</code></li>
<li><code>dataform.locations.list</code></li>
</ul>
<p><code>dataform.repositories.create</code></p>
<p><code>dataform.repositories.list</code></p>
<p><code>dataplex.projects.search</code></p>
<p><code>dataproc.batches.analyze</code></p>
<p><code>dataproc.batches.cancel</code></p>
<p><code>dataproc.batches.create</code></p>
<p><code>dataproc.batches.delete</code></p>
<p><code>dataproc.batches.get</code></p>
<p><code>dataproc.batches.list</code></p>
<p><code>dataproc. batches. sparkApplicationRead</code></p>
<p><code>dataproc. batches. sparkApplicationWrite</code></p>
<p><code>dataproc.operations.cancel</code></p>
<p><code>dataproc.operations.delete</code></p>
<p><code>dataproc.operations.get</code></p>
<p><code>dataproc.operations.list</code></p>
<p><code>dataproc.sessionTemplates.*</code></p>
<ul>
<li><code>dataproc. sessionTemplates. create</code></li>
<li><code>dataproc. sessionTemplates. delete</code></li>
<li><code>dataproc.sessionTemplates.get</code></li>
<li><code>dataproc.sessionTemplates.list</code></li>
<li><code>dataproc. sessionTemplates. update</code></li>
</ul>
<p><code>dataproc.sessions.*</code></p>
<ul>
<li><code>dataproc.sessions.create</code></li>
<li><code>dataproc.sessions.delete</code></li>
<li><code>dataproc.sessions.get</code></li>
<li><code>dataproc.sessions.list</code></li>
<li><code>dataproc. sessions. sparkApplicationRead</code></li>
<li><code>dataproc. sessions. sparkApplicationWrite</code></li>
<li><code>dataproc.sessions.terminate</code></li>
</ul>
<p><code>dataprocrm.nodePools.*</code></p>
<ul>
<li><code>dataprocrm.nodePools.create</code></li>
<li><code>dataprocrm.nodePools.delete</code></li>
<li><code>dataprocrm. nodePools. deleteNodes</code></li>
<li><code>dataprocrm.nodePools.get</code></li>
<li><code>dataprocrm.nodePools.list</code></li>
<li><code>dataprocrm.nodePools.resize</code></li>
</ul>
<p><code>dataprocrm.nodes.get</code></p>
<p><code>dataprocrm.nodes.heartbeat</code></p>
<p><code>dataprocrm.nodes.list</code></p>
<p><code>dataprocrm.nodes.update</code></p>
<p><code>dataprocrm.operations.get</code></p>
<p><code>dataprocrm.operations.list</code></p>
<p><code>dataprocrm.workloads.*</code></p>
<ul>
<li><code>dataprocrm.workloads.cancel</code></li>
<li><code>dataprocrm.workloads.create</code></li>
<li><code>dataprocrm.workloads.delete</code></li>
<li><code>dataprocrm.workloads.get</code></li>
<li><code>dataprocrm.workloads.list</code></li>
</ul>
<p><code>geminicloudassist. agents. invoke</code></p>
<p><code>geminidataanalytics. dataAgents. get</code></p>
<p><code>geminidataanalytics. dataAgents. list</code></p>
<p><code>geminidataanalytics. locations. chat</code></p>
<p><code>geminidataanalytics. locations. useDataEngineeringAgent</code></p>
<p><code>resourcemanager.projects.get</code></p>
<p><code>resourcemanager.projects.list</code></p></td>
</tr>
<tr class="odd">
<td>BigQuery User
<p>( <code>roles/ bigquery.user</code> )</p>
<p>When granted on a dataset, this role provides the ability to read the dataset's metadata and list tables in the dataset.</p>
<p>When granted on a project, this role also provides the ability to run jobs, including queries, within the project. A principal with this role can enumerate their own jobs, cancel their own jobs, and enumerate datasets within a project. Additionally, allows the creation of new datasets within the project; the creator is granted the BigQuery Data Owner role ( <code>roles/bigquery.dataOwner</code> ) on these new datasets.</p>
<p>Lowest-level resources where you can grant this role:</p>
<ul>
<li>Dataset</li>
<li>These resources within a dataset:
<ul>
<li>Routine</li>
</ul></li>
</ul>
<p>This role can also be granted on Resource Manager resources (projects, folders, and organizations).</p></td>
<td><p><code>bigquery.bireservations.get</code></p>
<p><code>bigquery. capacityCommitments. get</code></p>
<p><code>bigquery. capacityCommitments. list</code></p>
<p><code>bigquery.config.get</code></p>
<p><code>bigquery.datasets.create</code></p>
<p><code>bigquery.datasets.get</code></p>
<p><code>bigquery.datasets.getIamPolicy</code></p>
<p><code>bigquery.jobs.create</code></p>
<p><code>bigquery.jobs.list</code></p>
<p><code>bigquery.models.list</code></p>
<p><code>bigquery.propertyGraphs.list</code></p>
<p><code>bigquery.readsessions.*</code></p>
<ul>
<li><code>bigquery.readsessions.create</code></li>
<li><code>bigquery.readsessions.getData</code></li>
<li><code>bigquery.readsessions.update</code></li>
</ul>
<p><code>bigquery. reservationAssignments. list</code></p>
<p><code>bigquery. reservationAssignments. search</code></p>
<p><code>bigquery.reservationGroups.get</code></p>
<p><code>bigquery. reservationGroups. list</code></p>
<p><code>bigquery.reservations.get</code></p>
<p><code>bigquery.reservations.list</code></p>
<p><code>bigquery. reservations. listFailoverDatasets</code></p>
<p><code>bigquery.reservations.use</code></p>
<p><code>bigquery.routines.list</code></p>
<p><code>bigquery.savedqueries.get</code></p>
<p><code>bigquery.savedqueries.list</code></p>
<p><code>bigquery.tables.list</code></p>
<p><code>bigquery.transfers.get</code></p>
<p><code>bigquerymigration. translation. translate</code></p>
<p><code>cloudkms.keyHandles.*</code></p>
<ul>
<li><code>cloudkms.keyHandles.create</code></li>
<li><code>cloudkms.keyHandles.get</code></li>
<li><code>cloudkms.keyHandles.list</code></li>
</ul>
<p><code>cloudkms.operations.get</code></p>
<p><code>cloudkms. projects. showEffectiveAutokeyConfig</code></p>
<p><code>dataform.folders.create</code></p>
<p><code>dataform.locations.*</code></p>
<ul>
<li><code>dataform.locations.get</code></li>
<li><code>dataform.locations.list</code></li>
</ul>
<p><code>dataform.repositories.create</code></p>
<p><code>dataform.repositories.list</code></p>
<p><code>dataplex.projects.search</code></p>
<p><code>resourcemanager.projects.get</code></p>
<p><code>resourcemanager.projects.list</code></p></td>
</tr>
<tr class="even">
<td>BigQuery Filtered Data Viewer
<p>( <code>roles/ bigquery.filteredDataViewer</code> )</p>
<p>Access to view filtered table data defined by a row access policy. <code>bigquery.filteredDataViewer</code> is a system-managed role. Grant the role by using row-level access policies. Don't apply the role directly to a resource through Identity and Access Management (IAM).</p></td>
<td><p><code>bigquery. rowAccessPolicies. getFilteredData</code></p></td>
</tr>
<tr class="odd">
<td>BigQuery ObjectRef Admin
<p>( <code>roles/ bigquery.objectRefAdmin</code> )</p>
<p>Administer ObjectRef resources that includes read and write permissions</p>
<p>Lowest-level resources where you can grant this role:</p>
<ul>
<li>Connection</li>
</ul>
<p>This role can also be granted on Resource Manager resources (projects, folders, and organizations).</p></td>
<td><p><code>bigquery.objectRefs.*</code></p>
<ul>
<li><code>bigquery.objectRefs.read</code></li>
<li><code>bigquery.objectRefs.write</code></li>
</ul></td>
</tr>
<tr class="even">
<td>BigQuery ObjectRef Reader
<p>( <code>roles/ bigquery.objectRefReader</code> )</p>
<p>Role for reading referenced objects via ObjectRefs in BigQuery</p>
<p>Lowest-level resources where you can grant this role:</p>
<ul>
<li>Connection</li>
</ul>
<p>This role can also be granted on Resource Manager resources (projects, folders, and organizations).</p></td>
<td><p><code>bigquery.objectRefs.read</code></p></td>
</tr>
<tr class="odd">
<td>BigQuery Authorized Routine Admin <sup>Beta</sup>
<p>( <code>roles/ bigquery.routineAdmin</code> )</p>
<p>Role for Authorized Routine to administer supported resources</p></td>
<td><p><code>bigquery.connections.use</code></p>
<p><code>bigquery.datasets.get</code></p>
<p><code>bigquery.models.getData</code></p>
<p><code>bigquery.models.getMetadata</code></p>
<p><code>bigquery.routines.get</code></p>
<p><code>bigquery.routines.list</code></p>
<p><code>bigquery.tables.create</code></p>
<p><code>bigquery.tables.delete</code></p>
<p><code>bigquery.tables.get</code></p>
<p><code>bigquery.tables.getData</code></p>
<p><code>bigquery.tables.list</code></p>
<p><code>bigquery.tables.update</code></p>
<p><code>bigquery.tables.updateData</code></p></td>
</tr>
<tr class="even">
<td>BigQuery Authorized Routine Data Editor <sup>Beta</sup>
<p>( <code>roles/ bigquery.routineDataEditor</code> )</p>
<p>Role for Authorized Routine to edit contents of supported resources</p></td>
<td><p><code>bigquery.datasets.get</code></p>
<p><code>bigquery.models.getData</code></p>
<p><code>bigquery.models.getMetadata</code></p>
<p><code>bigquery.routines.get</code></p>
<p><code>bigquery.routines.list</code></p>
<p><code>bigquery.tables.create</code></p>
<p><code>bigquery.tables.delete</code></p>
<p><code>bigquery.tables.get</code></p>
<p><code>bigquery.tables.getData</code></p>
<p><code>bigquery.tables.list</code></p>
<p><code>bigquery.tables.update</code></p>
<p><code>bigquery.tables.updateData</code></p></td>
</tr>
<tr class="odd">
<td>BigQuery Authorized Routine Data Viewer <sup>Beta</sup>
<p>( <code>roles/ bigquery.routineDataViewer</code> )</p>
<p>Role for Authorized Routine to view data and contents of supported resources</p></td>
<td><p><code>bigquery.datasets.get</code></p>
<p><code>bigquery.models.getData</code></p>
<p><code>bigquery.models.getMetadata</code></p>
<p><code>bigquery.routines.get</code></p>
<p><code>bigquery.routines.list</code></p>
<p><code>bigquery.tables.get</code></p>
<p><code>bigquery.tables.getData</code></p>
<p><code>bigquery.tables.list</code></p></td>
</tr>
<tr class="even">
<td>BigQuery Authorized Routine Metadata Viewer <sup>Beta</sup>
<p>( <code>roles/ bigquery.routineMetadataViewer</code> )</p>
<p>Role for Authorized Routine to view metadata of supported resources</p></td>
<td><p><code>bigquery.datasets.get</code></p>
<p><code>bigquery.models.getMetadata</code></p>
<p><code>bigquery.routines.get</code></p>
<p><code>bigquery.routines.list</code></p>
<p><code>bigquery.tables.get</code></p>
<p><code>bigquery.tables.list</code></p></td>
</tr>
<tr class="odd">
<td>BigQuery Security Admin <sup>Beta</sup>
<p>( <code>roles/ bigquery.securityAdmin</code> )</p>
<p>Administer all BigQuery security controls</p></td>
<td><p><code>bigquery.dataPolicies.attach</code></p>
<p><code>bigquery.dataPolicies.create</code></p>
<p><code>bigquery.dataPolicies.delete</code></p>
<p><code>bigquery.dataPolicies.get</code></p>
<p><code>bigquery. dataPolicies. getIamPolicy</code></p>
<p><code>bigquery.dataPolicies.list</code></p>
<p><code>bigquery. dataPolicies. setIamPolicy</code></p>
<p><code>bigquery.dataPolicies.update</code></p>
<p><code>bigquery. datasets. createTagBinding</code></p>
<p><code>bigquery. datasets. deleteTagBinding</code></p>
<p><code>bigquery.datasets.get</code></p>
<p><code>bigquery.datasets.getIamPolicy</code></p>
<p><code>bigquery. datasets. listEffectiveTags</code></p>
<p><code>bigquery. datasets. listSharedDatasetUsage</code></p>
<p><code>bigquery. datasets. listTagBindings</code></p>
<p><code>bigquery.datasets.setIamPolicy</code></p>
<p><code>bigquery.datasets.update</code></p>
<p><code>bigquery.datasets.updateTag</code></p>
<p><code>bigquery. rowAccessPolicies. create</code></p>
<p><code>bigquery. rowAccessPolicies. delete</code></p>
<p><code>bigquery.rowAccessPolicies.get</code></p>
<p><code>bigquery. rowAccessPolicies. getIamPolicy</code></p>
<p><code>bigquery. rowAccessPolicies. list</code></p>
<p><code>bigquery. rowAccessPolicies. setIamPolicy</code></p>
<p><code>bigquery. rowAccessPolicies. update</code></p>
<p><code>bigquery. tables. createTagBinding</code></p>
<p><code>bigquery. tables. deleteTagBinding</code></p>
<p><code>bigquery.tables.get</code></p>
<p><code>bigquery.tables.getIamPolicy</code></p>
<p><code>bigquery.tables.list</code></p>
<p><code>bigquery. tables. listEffectiveTags</code></p>
<p><code>bigquery. tables. listTagBindings</code></p>
<p><code>bigquery. tables. setColumnDataPolicy</code></p>
<p><code>bigquery.tables.setIamPolicy</code></p>
<p><code>bigquery.tables.update</code></p>
<p><code>bigquery.tables.updateTag</code></p>
<p><code>dataplex.projects.search</code></p></td>
</tr>
</tbody>
</table>

### Service agent roles

Service agent roles should only be granted to [service agents](https://docs.cloud.google.com/iam/docs/service-agents) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Role</th>
<th>Permissions</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Connected Sheets Service Agent
<p>( <code>roles/ bigquery.connectedSheetsServiceAgent</code> )</p>
<p>Grants Connected Sheets Service Account access to create and manage BigQuery jobs on the customers resources.</p>
<blockquote>
<strong>Warning:</strong> Do not grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote></td>
<td><p><code>bigquery.datasets.get</code></p>
<p><code>bigquery.jobs.create</code></p>
<p><code>bigquery.tables.create</code></p>
<p><code>bigquery.tables.update</code></p>
<p><code>bigquery.tables.updateData</code></p></td>
</tr>
</tbody>
</table>

### BigQuery Connection API roles

This table lists the predefined IAM roles and permissions for BigQuery Connection API. To search through all roles and permissions, see the [role and permission index](https://docs.cloud.google.com/iam/docs/roles-permissions) .

BigQuery Connection API offers the following service agent roles. Service agent roles should only be granted to [service agents](https://docs.cloud.google.com/iam/docs/service-agents) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Role</th>
<th>Permissions</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>BigQuery Connection Service Agent
<p>( <code>roles/ bigqueryconnection.serviceAgent</code> )</p>
<p>Gives BigQuery Connection Service access to Cloud SQL instances in user projects.</p>
<blockquote>
<strong>Warning:</strong> Do not grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote></td>
<td><p><code>cloudsql.instances.connect</code></p>
<p><code>cloudsql.instances.get</code></p>
<p><code>logging.logEntries.create</code></p>
<p><code>logging.logEntries.route</code></p>
<p><code>monitoring. metricDescriptors. create</code></p>
<p><code>monitoring. metricDescriptors. get</code></p>
<p><code>monitoring. metricDescriptors. list</code></p>
<p><code>monitoring. monitoredResourceDescriptors.*</code></p>
<ul>
<li><code>monitoring. monitoredResourceDescriptors. get</code></li>
<li><code>monitoring. monitoredResourceDescriptors. list</code></li>
</ul>
<p><code>monitoring.timeSeries.create</code></p></td>
</tr>
</tbody>
</table>

### BigQuery Continuous Query roles

This table lists the predefined IAM roles and permissions for BigQuery Continuous Query. To search through all roles and permissions, see the [role and permission index](https://docs.cloud.google.com/iam/docs/roles-permissions) .

BigQuery Continuous Query offers the following service agent roles. Service agent roles should only be granted to [service agents](https://docs.cloud.google.com/iam/docs/service-agents) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Role</th>
<th>Permissions</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>BigQuery Continuous Query Service Agent
<p>( <code>roles/ bigquerycontinuousquery.serviceAgent</code> )</p>
<p>Gives BigQuery Continuous Query access to the service accounts in the user project.</p>
<blockquote>
<strong>Warning:</strong> Do not grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote></td>
<td><p><code>iam. serviceAccounts. getAccessToken</code></p></td>
</tr>
</tbody>
</table>

### BigQuery Data Policy roles

This table lists the predefined IAM roles and permissions for BigQuery Data Policy. To search through all roles and permissions, see the [role and permission index](https://docs.cloud.google.com/iam/docs/roles-permissions) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Role</th>
<th>Permissions</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>BigQuery Data Policy Admin
<p>( <code>roles/ bigquerydatapolicy.admin</code> )</p>
<p>Role for managing Data Policies in BigQuery</p>
<p>This role can only be granted on Resource Manager resources (projects, folders, and organizations).</p></td>
<td><p><code>bigquery.dataPolicies.attach</code></p>
<p><code>bigquery.dataPolicies.create</code></p>
<p><code>bigquery.dataPolicies.delete</code></p>
<p><code>bigquery.dataPolicies.get</code></p>
<p><code>bigquery. dataPolicies. getIamPolicy</code></p>
<p><code>bigquery.dataPolicies.list</code></p>
<p><code>bigquery. dataPolicies. setIamPolicy</code></p>
<p><code>bigquery.dataPolicies.update</code></p></td>
</tr>
<tr class="even">
<td>BigQuery Data Policy Editor
<p>( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p>Editor role for BigQuery Data Policy</p></td>
<td><p><code>bigquery.bireservations.*</code></p>
<ul>
<li><code>bigquery.bireservations.get</code></li>
<li><code>bigquery.bireservations.update</code></li>
</ul>
<p><code>bigquery. capacityCommitments. get</code></p>
<p><code>bigquery. capacityCommitments. list</code></p>
<p><code>bigquery. capacityCommitments. update</code></p>
<p><code>bigquery.config.*</code></p>
<ul>
<li><code>bigquery.config.get</code></li>
<li><code>bigquery.config.update</code></li>
</ul>
<p><code>bigquery.connections.create</code></p>
<p><code>bigquery.connections.delete</code></p>
<p><code>bigquery.connections.get</code></p>
<p><code>bigquery. connections. getIamPolicy</code></p>
<p><code>bigquery.connections.list</code></p>
<p><code>bigquery.connections.update</code></p>
<p><code>bigquery.connections.updateTag</code></p>
<p><code>bigquery.connections.use</code></p>
<p><code>bigquery.dataPolicies.attach</code></p>
<p><code>bigquery.dataPolicies.create</code></p>
<p><code>bigquery.dataPolicies.delete</code></p>
<p><code>bigquery.dataPolicies.get</code></p>
<p><code>bigquery. dataPolicies. getIamPolicy</code></p>
<p><code>bigquery.dataPolicies.list</code></p>
<p><code>bigquery.dataPolicies.update</code></p>
<p><code>bigquery.datasets.create</code></p>
<p><code>bigquery.datasets.get</code></p>
<p><code>bigquery.datasets.getIamPolicy</code></p>
<p><code>bigquery. datasets. listEffectiveTags</code></p>
<p><code>bigquery. datasets. listTagBindings</code></p>
<p><code>bigquery.datasets.updateTag</code></p>
<p><code>bigquery.jobs.create</code></p>
<p><code>bigquery. jobs. createGlobalQuery</code></p>
<p><code>bigquery.jobs.delete</code></p>
<p><code>bigquery.jobs.get</code></p>
<p><code>bigquery.jobs.list</code></p>
<p><code>bigquery. jobs. listExecutionMetadata</code></p>
<p><code>bigquery.models.*</code></p>
<ul>
<li><code>bigquery.models.create</code></li>
<li><code>bigquery.models.delete</code></li>
<li><code>bigquery.models.export</code></li>
<li><code>bigquery.models.getData</code></li>
<li><code>bigquery.models.getMetadata</code></li>
<li><code>bigquery.models.list</code></li>
<li><code>bigquery.models.updateData</code></li>
<li><code>bigquery.models.updateMetadata</code></li>
<li><code>bigquery.models.updateTag</code></li>
</ul>
<p><code>bigquery.objectRefs.*</code></p>
<ul>
<li><code>bigquery.objectRefs.read</code></li>
<li><code>bigquery.objectRefs.write</code></li>
</ul>
<p><code>bigquery.propertyGraphs.*</code></p>
<ul>
<li><code>bigquery.propertyGraphs.create</code></li>
<li><code>bigquery.propertyGraphs.delete</code></li>
<li><code>bigquery.propertyGraphs.get</code></li>
<li><code>bigquery.propertyGraphs.list</code></li>
<li><code>bigquery.propertyGraphs.update</code></li>
</ul>
<p><code>bigquery.readsessions.*</code></p>
<ul>
<li><code>bigquery.readsessions.create</code></li>
<li><code>bigquery.readsessions.getData</code></li>
<li><code>bigquery.readsessions.update</code></li>
</ul>
<p><code>bigquery. reservationAssignments.*</code></p>
<ul>
<li><code>bigquery. reservationAssignments. create</code></li>
<li><code>bigquery. reservationAssignments. delete</code></li>
<li><code>bigquery. reservationAssignments. list</code></li>
<li><code>bigquery. reservationAssignments. search</code></li>
</ul>
<p><code>bigquery.reservationGroups.*</code></p>
<ul>
<li><code>bigquery. reservationGroups. create</code></li>
<li><code>bigquery. reservationGroups. delete</code></li>
<li><code>bigquery.reservationGroups.get</code></li>
<li><code>bigquery. reservationGroups. list</code></li>
<li><code>bigquery. reservationGroups. update</code></li>
</ul>
<p><code>bigquery.reservations.create</code></p>
<p><code>bigquery.reservations.delete</code></p>
<p><code>bigquery.reservations.get</code></p>
<p><code>bigquery. reservations. getIamPolicy</code></p>
<p><code>bigquery.reservations.list</code></p>
<p><code>bigquery. reservations. listFailoverDatasets</code></p>
<p><code>bigquery.reservations.update</code></p>
<p><code>bigquery.reservations.use</code></p>
<p><code>bigquery.routines.*</code></p>
<ul>
<li><code>bigquery.routines.create</code></li>
<li><code>bigquery.routines.delete</code></li>
<li><code>bigquery.routines.get</code></li>
<li><code>bigquery.routines.list</code></li>
<li><code>bigquery.routines.update</code></li>
<li><code>bigquery.routines.updateTag</code></li>
</ul>
<p><code>bigquery. rowAccessPolicies. create</code></p>
<p><code>bigquery. rowAccessPolicies. delete</code></p>
<p><code>bigquery.rowAccessPolicies.get</code></p>
<p><code>bigquery. rowAccessPolicies. getIamPolicy</code></p>
<p><code>bigquery. rowAccessPolicies. list</code></p>
<p><code>bigquery. rowAccessPolicies. update</code></p>
<p><code>bigquery.savedqueries.*</code></p>
<ul>
<li><code>bigquery.savedqueries.create</code></li>
<li><code>bigquery.savedqueries.delete</code></li>
<li><code>bigquery.savedqueries.get</code></li>
<li><code>bigquery.savedqueries.list</code></li>
<li><code>bigquery.savedqueries.update</code></li>
</ul>
<p><code>bigquery.tables.createIndex</code></p>
<p><code>bigquery.tables.createSnapshot</code></p>
<p><code>bigquery.tables.deleteIndex</code></p>
<p><code>bigquery.tables.getIamPolicy</code></p>
<p><code>bigquery. tables. listEffectiveTags</code></p>
<p><code>bigquery. tables. listTagBindings</code></p>
<p><code>bigquery.tables.replicateData</code></p>
<p><code>bigquery. tables. restoreSnapshot</code></p>
<p><code>bigquery.tables.updateIndex</code></p>
<p><code>bigquery.transfers.*</code></p>
<ul>
<li><code>bigquery.transfers.get</code></li>
<li><code>bigquery.transfers.update</code></li>
</ul>
<p><code>resourcemanager.projects.get</code></p>
<p><code>resourcemanager.projects.list</code></p></td>
</tr>
<tr class="odd">
<td>BigQuery Data Policy Viewer
<p>( <code>roles/ bigquerydatapolicy.viewer</code> )</p>
<p>Role for viewing Data Policies in BigQuery</p>
<p>This role can only be granted on Resource Manager resources (projects, folders, and organizations).</p></td>
<td><p><code>bigquery.dataPolicies.get</code></p>
<p><code>bigquery.dataPolicies.list</code></p></td>
</tr>
<tr class="even">
<td>Masked Reader
<p>( <code>roles/ bigquerydatapolicy.maskedReader</code> )</p>
<p>Masked read access to sub-resources tagged by the policy tag associated with a data policy, for example, BigQuery columns</p>
<p>This role can only be granted on Resource Manager resources (projects, folders, and organizations).</p></td>
<td><p><code>bigquery. dataPolicies. maskedGet</code></p></td>
</tr>
<tr class="odd">
<td>Raw Data Reader <sup>Beta</sup>
<p>( <code>roles/ bigquerydatapolicy.rawDataReader</code> )</p>
<p>Raw read access to sub-resources associated with a data policy, for example, BigQuery columns</p>
<p>This role can only be granted on Resource Manager resources (projects, folders, and organizations).</p></td>
<td><p><code>bigquery. dataPolicies. getRawData</code></p></td>
</tr>
</tbody>
</table>

### BigQuery Data Transfer Service roles

This table lists the predefined IAM roles and permissions for BigQuery Data Transfer Service. To search through all roles and permissions, see the [role and permission index](https://docs.cloud.google.com/iam/docs/roles-permissions) .

BigQuery Data Transfer Service offers the following service agent roles. Service agent roles should only be granted to [service agents](https://docs.cloud.google.com/iam/docs/service-agents) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Role</th>
<th>Permissions</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>BigQuery Data Transfer Service Agent
<p>( <code>roles/ bigquerydatatransfer.serviceAgent</code> )</p>
<p>Gives BigQuery Data Transfer Service access to start BigQuery jobs in consumer project.</p>
<blockquote>
<strong>Warning:</strong> Do not grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote></td>
<td><p><code>bigquery.config.get</code></p>
<p><code>bigquery.connections.delegate</code></p>
<p><code>bigquery.jobs.create</code></p>
<p><code>compute.networkAttachments.get</code></p>
<p><code>compute. networkAttachments. update</code></p>
<p><code>compute.regionOperations.get</code></p>
<p><code>compute.subnetworks.use</code></p>
<p><code>dataform.folders.create</code></p>
<p><code>dataform.locations.*</code></p>
<ul>
<li><code>dataform.locations.get</code></li>
<li><code>dataform.locations.list</code></li>
</ul>
<p><code>dataform.repositories.create</code></p>
<p><code>dataform.repositories.list</code></p>
<p><code>dataplex.entryGroups.get</code></p>
<p><code>dataplex. entryGroups. useContactsAspect</code></p>
<p><code>dataplex. entryGroups. useDataProfileAspect</code></p>
<p><code>dataplex. entryGroups. useDatabaseDataPolicyAspect</code></p>
<p><code>dataplex. entryGroups. useManagedConnectorTypes</code></p>
<p><code>dataplex. entryGroups. useMySQLConnectorTypes</code></p>
<p><code>dataplex. entryGroups. useOracleConnectorTypes</code></p>
<p><code>dataplex. entryGroups. useOverviewAspect</code></p>
<p><code>dataplex. entryGroups. usePostgreSQLConnectorTypes</code></p>
<p><code>dataplex. entryGroups. useSQLAccessAspect</code></p>
<p><code>dataplex. entryGroups. useSQLServerConnectorTypes</code></p>
<p><code>dataplex. entryGroups. useSQLTriggersAspect</code></p>
<p><code>dataplex. entryGroups. useSchemaAspect</code></p>
<p><code>dataplex. entryGroups. useSecondaryIndexesAspect</code></p>
<p><code>dataplex. entryGroups. useStorageAspect</code></p>
<p><code>dataplex.metadataJobs.create</code></p>
<p><code>dataplex.metadataJobs.get</code></p>
<p><code>dataplex.metadataJobs.list</code></p>
<p><code>geminidataanalytics. locations. chat</code></p>
<p><code>iam. serviceAccounts. getAccessToken</code></p>
<p><code>logging.logEntries.create</code></p>
<p><code>logging.logEntries.route</code></p>
<p><code>resourcemanager.projects.get</code></p>
<p><code>resourcemanager.projects.list</code></p>
<p><code>serviceusage.services.use</code></p></td>
</tr>
</tbody>
</table>

### BigQuery Engine for Apache Flink roles

This table lists the predefined IAM roles and permissions for BigQuery Engine for Apache Flink. To search through all roles and permissions, see the [role and permission index](https://docs.cloud.google.com/iam/docs/roles-permissions) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Role</th>
<th>Permissions</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Managed Flink Admin <sup>Beta</sup>
<p>( <code>roles/ managedflink.admin</code> )</p>
<p>Full access to Managed Flink resources.</p></td>
<td><p><code>managedflink.*</code></p>
<ul>
<li><code>managedflink. deployments. create</code></li>
<li><code>managedflink. deployments. delete</code></li>
<li><code>managedflink.deployments.get</code></li>
<li><code>managedflink.deployments.list</code></li>
<li><code>managedflink. deployments. update</code></li>
<li><code>managedflink.jobs.create</code></li>
<li><code>managedflink.jobs.delete</code></li>
<li><code>managedflink.jobs.get</code></li>
<li><code>managedflink.jobs.list</code></li>
<li><code>managedflink.jobs.update</code></li>
<li><code>managedflink.locations.get</code></li>
<li><code>managedflink.locations.list</code></li>
<li><code>managedflink.operations.cancel</code></li>
<li><code>managedflink.operations.delete</code></li>
<li><code>managedflink.operations.get</code></li>
<li><code>managedflink.operations.list</code></li>
<li><code>managedflink.sessions.create</code></li>
<li><code>managedflink.sessions.delete</code></li>
<li><code>managedflink.sessions.get</code></li>
<li><code>managedflink.sessions.list</code></li>
<li><code>managedflink.sessions.update</code></li>
</ul>
<p><code>resourcemanager.projects.get</code></p>
<p><code>resourcemanager.projects.list</code></p></td>
</tr>
<tr class="even">
<td>Managed Flink Viewer <sup>Beta</sup>
<p>( <code>roles/ managedflink.viewer</code> )</p>
<p>Readonly access to Managed Flink resources.</p></td>
<td><p><code>managedflink.deployments.get</code></p>
<p><code>managedflink.deployments.list</code></p>
<p><code>managedflink.jobs.get</code></p>
<p><code>managedflink.jobs.list</code></p>
<p><code>managedflink.locations.*</code></p>
<ul>
<li><code>managedflink.locations.get</code></li>
<li><code>managedflink.locations.list</code></li>
</ul>
<p><code>managedflink.operations.get</code></p>
<p><code>managedflink.operations.list</code></p>
<p><code>managedflink.sessions.get</code></p>
<p><code>managedflink.sessions.list</code></p>
<p><code>resourcemanager.projects.get</code></p>
<p><code>resourcemanager.projects.list</code></p></td>
</tr>
<tr class="odd">
<td>Managed Flink Developer <sup>Beta</sup>
<p>( <code>roles/ managedflink.developer</code> )</p>
<p>Full access to Managed Flink Jobs and Sessions and read access to Deployments.</p></td>
<td><p><code>managedflink.deployments.get</code></p>
<p><code>managedflink.deployments.list</code></p>
<p><code>managedflink.jobs.*</code></p>
<ul>
<li><code>managedflink.jobs.create</code></li>
<li><code>managedflink.jobs.delete</code></li>
<li><code>managedflink.jobs.get</code></li>
<li><code>managedflink.jobs.list</code></li>
<li><code>managedflink.jobs.update</code></li>
</ul>
<p><code>managedflink.locations.*</code></p>
<ul>
<li><code>managedflink.locations.get</code></li>
<li><code>managedflink.locations.list</code></li>
</ul>
<p><code>managedflink.operations.get</code></p>
<p><code>managedflink.operations.list</code></p>
<p><code>managedflink.sessions.*</code></p>
<ul>
<li><code>managedflink.sessions.create</code></li>
<li><code>managedflink.sessions.delete</code></li>
<li><code>managedflink.sessions.get</code></li>
<li><code>managedflink.sessions.list</code></li>
<li><code>managedflink.sessions.update</code></li>
</ul>
<p><code>resourcemanager.projects.get</code></p>
<p><code>resourcemanager.projects.list</code></p></td>
</tr>
</tbody>
</table>

### Service agent roles

Service agent roles should only be granted to [service agents](https://docs.cloud.google.com/iam/docs/service-agents) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Role</th>
<th>Permissions</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Managed Flink Service Agent
<p>( <code>roles/ managedflink.serviceAgent</code> )</p>
<p>Gives Managed Flink Service Agent access to Cloud Platform resources.</p>
<blockquote>
<strong>Warning:</strong> Do not grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote></td>
<td><p><code>compute. networkAttachments. create</code></p>
<p><code>compute. networkAttachments. delete</code></p>
<p><code>compute.networkAttachments.get</code></p>
<p><code>compute. networkAttachments. list</code></p>
<p><code>compute. networkAttachments. update</code></p>
<p><code>compute.networks.get</code></p>
<p><code>compute.networks.list</code></p>
<p><code>compute.regionOperations.get</code></p>
<p><code>compute.subnetworks.get</code></p>
<p><code>compute.subnetworks.list</code></p>
<p><code>compute.subnetworks.use</code></p>
<p><code>dns. networks. targetWithPeeringZone</code></p>
<p><code>managedkafka.clusters.get</code></p>
<p><code>managedkafka.clusters.list</code></p>
<p><code>managedkafka.clusters.update</code></p>
<p><code>monitoring. metricDescriptors. create</code></p>
<p><code>monitoring. metricDescriptors. get</code></p>
<p><code>monitoring. metricDescriptors. list</code></p>
<p><code>monitoring. monitoredResourceDescriptors.*</code></p>
<ul>
<li><code>monitoring. monitoredResourceDescriptors. get</code></li>
<li><code>monitoring. monitoredResourceDescriptors. list</code></li>
</ul>
<p><code>monitoring.timeSeries.create</code></p>
<p><code>serviceusage.services.use</code></p>
<p><code>storage.objects.get</code></p></td>
</tr>
</tbody>
</table>

### BigQuery Migration Service roles

This table lists the predefined IAM roles and permissions for BigQuery Migration Service. To search through all roles and permissions, see the [role and permission index](https://docs.cloud.google.com/iam/docs/roles-permissions) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Role</th>
<th>Permissions</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Bigquerymigration Admin
<p>( <code>roles/ bigquerymigration.admin</code> )</p>
<p>Admin role for bigquerymigration</p></td>
<td><p><code>bigquerymigration.*</code></p>
<ul>
<li><code>bigquerymigration.subtasks.get</code></li>
<li><code>bigquerymigration. subtasks. list</code></li>
<li><code>bigquerymigration. translation. translate</code></li>
<li><code>bigquerymigration. workflows. create</code></li>
<li><code>bigquerymigration. workflows. delete</code></li>
<li><code>bigquerymigration. workflows. enableAiOutputTypes</code></li>
<li><code>bigquerymigration. workflows. enableLineageOutputTypes</code></li>
<li><code>bigquerymigration. workflows. enableOutputTypePermissions</code></li>
<li><code>bigquerymigration. workflows. get</code></li>
<li><code>bigquerymigration. workflows. list</code></li>
<li><code>bigquerymigration. workflows. orchestrateTask</code></li>
<li><code>bigquerymigration. workflows. update</code></li>
</ul>
<p><code>resourcemanager.projects.get</code></p>
<p><code>resourcemanager.projects.list</code></p></td>
</tr>
<tr class="even">
<td>MigrationWorkflow Editor
<p>( <code>roles/ bigquerymigration.editor</code> )</p>
<p>Editor of EDW migration workflows.</p></td>
<td><p><code>bigquerymigration.subtasks.*</code></p>
<ul>
<li><code>bigquerymigration.subtasks.get</code></li>
<li><code>bigquerymigration. subtasks. list</code></li>
</ul>
<p><code>bigquerymigration. workflows. create</code></p>
<p><code>bigquerymigration. workflows. delete</code></p>
<p><code>bigquerymigration. workflows. enableAiOutputTypes</code></p>
<p><code>bigquerymigration. workflows. enableLineageOutputTypes</code></p>
<p><code>bigquerymigration. workflows. enableOutputTypePermissions</code></p>
<p><code>bigquerymigration. workflows. get</code></p>
<p><code>bigquerymigration. workflows. list</code></p>
<p><code>bigquerymigration. workflows. update</code></p></td>
</tr>
<tr class="odd">
<td>MigrationWorkflow Viewer
<p>( <code>roles/ bigquerymigration.viewer</code> )</p>
<p>Viewer of EDW migration MigrationWorkflow.</p></td>
<td><p><code>bigquerymigration.subtasks.*</code></p>
<ul>
<li><code>bigquerymigration.subtasks.get</code></li>
<li><code>bigquerymigration. subtasks. list</code></li>
</ul>
<p><code>bigquerymigration. workflows. get</code></p>
<p><code>bigquerymigration. workflows. list</code></p></td>
</tr>
<tr class="even">
<td>Migration Management Editor <sup>Beta</sup>
<p>( <code>roles/ bigquerymigration.migrationEditor</code> )</p>
<p>Admin of EDW migrations.</p></td>
<td></td>
</tr>
<tr class="odd">
<td>Migration Management Viewer <sup>Beta</sup>
<p>( <code>roles/ bigquerymigration.migrationViewer</code> )</p>
<p>Viewer of EDW migrations.</p></td>
<td></td>
</tr>
<tr class="even">
<td>Task Orchestrator
<p>( <code>roles/ bigquerymigration.orchestrator</code> )</p>
<p>Orchestrator of EDW migration tasks.</p></td>
<td><p><code>bigquerymigration. workflows. orchestrateTask</code></p>
<p><code>storage.objects.list</code></p></td>
</tr>
<tr class="odd">
<td>Migration Translation User
<p>( <code>roles/ bigquerymigration.translationUser</code> )</p>
<p>User of EDW migration interactive SQL translation service.</p></td>
<td><p><code>bigquerymigration. translation. translate</code></p></td>
</tr>
<tr class="even">
<td>Task Worker
<p>( <code>roles/ bigquerymigration.worker</code> )</p>
<p>Worker that executes EDW migration subtasks.</p></td>
<td><p><code>storage.objects.create</code></p>
<p><code>storage.objects.get</code></p>
<p><code>storage.objects.list</code></p></td>
</tr>
</tbody>
</table>

### Service agent roles

Service agent roles should only be granted to [service agents](https://docs.cloud.google.com/iam/docs/service-agents) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Role</th>
<th>Permissions</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>BigQuery Migration Service Agent
<p>( <code>roles/ bigquerymigration.serviceAgent</code> )</p>
<p>Access required for the BigQuery Migration Service to perform data discovery, metadata registration, and manage data transfers.</p>
<blockquote>
<strong>Warning:</strong> Do not grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote></td>
<td><p><code>resourcemanager.projects.get</code></p></td>
</tr>
</tbody>
</table>

### BigQuery Omni roles

This table lists the predefined IAM roles and permissions for BigQuery Omni. To search through all roles and permissions, see the [role and permission index](https://docs.cloud.google.com/iam/docs/roles-permissions) .

BigQuery Omni offers the following service agent roles. Service agent roles should only be granted to [service agents](https://docs.cloud.google.com/iam/docs/service-agents) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Role</th>
<th>Permissions</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>BigQuery Omni Service Agent
<p>( <code>roles/ bigqueryomni.serviceAgent</code> )</p>
<p>Gives BigQuery Omni access to tables in user projects.</p>
<blockquote>
<strong>Warning:</strong> Do not grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote></td>
<td><p><code>bigquery.jobs.create</code></p>
<p><code>bigquery.tables.updateData</code></p></td>
</tr>
</tbody>
</table>

### BigQuery sharing roles

This table lists the predefined IAM roles and permissions for BigQuery sharing. To search through all roles and permissions, see the [role and permission index](https://docs.cloud.google.com/iam/docs/roles-permissions) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Role</th>
<th>Permissions</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Analytics Hub Admin
<p>( <code>roles/ analyticshub.admin</code> )</p>
<p>Administer Data Exchanges and Listings</p></td>
<td><p><code>analyticshub. dataExchanges. create</code></p>
<p><code>analyticshub. dataExchanges. delete</code></p>
<p><code>analyticshub.dataExchanges.get</code></p>
<p><code>analyticshub. dataExchanges. getIamPolicy</code></p>
<p><code>analyticshub. dataExchanges. list</code></p>
<p><code>analyticshub. dataExchanges. setIamPolicy</code></p>
<p><code>analyticshub. dataExchanges. update</code></p>
<p><code>analyticshub. dataExchanges. viewSubscriptions</code></p>
<p><code>analyticshub.listings.create</code></p>
<p><code>analyticshub.listings.delete</code></p>
<p><code>analyticshub.listings.get</code></p>
<p><code>analyticshub. listings. getIamPolicy</code></p>
<p><code>analyticshub.listings.list</code></p>
<p><code>analyticshub. listings. setIamPolicy</code></p>
<p><code>analyticshub.listings.update</code></p>
<p><code>analyticshub. listings. viewSubscriptions</code></p>
<p><code>analyticshub.queryTemplates.*</code></p>
<ul>
<li><code>analyticshub. queryTemplates. approve</code></li>
<li><code>analyticshub. queryTemplates. create</code></li>
<li><code>analyticshub. queryTemplates. delete</code></li>
<li><code>analyticshub. queryTemplates. get</code></li>
<li><code>analyticshub. queryTemplates. list</code></li>
<li><code>analyticshub. queryTemplates. update</code></li>
</ul>
<p><code>analyticshub.subscriptions.*</code></p>
<ul>
<li><code>analyticshub. subscriptions. create</code></li>
<li><code>analyticshub. subscriptions. delete</code></li>
<li><code>analyticshub.subscriptions.get</code></li>
<li><code>analyticshub. subscriptions. list</code></li>
<li><code>analyticshub. subscriptions. update</code></li>
</ul>
<p><code>resourcemanager.projects.get</code></p>
<p><code>resourcemanager.projects.list</code></p></td>
</tr>
<tr class="even">
<td>Analytics Hub Editor
<p>( <code>roles/ analyticshub.editor</code> )</p>
<p>Editor role for Analytics Hub</p></td>
<td><p><code>analyticshub. dataExchanges. create</code></p>
<p><code>analyticshub. dataExchanges. delete</code></p>
<p><code>analyticshub.dataExchanges.get</code></p>
<p><code>analyticshub. dataExchanges. getIamPolicy</code></p>
<p><code>analyticshub. dataExchanges. list</code></p>
<p><code>analyticshub. dataExchanges. update</code></p>
<p><code>analyticshub.listings.create</code></p>
<p><code>analyticshub.listings.delete</code></p>
<p><code>analyticshub.listings.get</code></p>
<p><code>analyticshub. listings. getIamPolicy</code></p>
<p><code>analyticshub.listings.list</code></p>
<p><code>analyticshub.listings.update</code></p>
<p><code>analyticshub.queryTemplates.*</code></p>
<ul>
<li><code>analyticshub. queryTemplates. approve</code></li>
<li><code>analyticshub. queryTemplates. create</code></li>
<li><code>analyticshub. queryTemplates. delete</code></li>
<li><code>analyticshub. queryTemplates. get</code></li>
<li><code>analyticshub. queryTemplates. list</code></li>
<li><code>analyticshub. queryTemplates. update</code></li>
</ul>
<p><code>analyticshub.subscriptions.*</code></p>
<ul>
<li><code>analyticshub. subscriptions. create</code></li>
<li><code>analyticshub. subscriptions. delete</code></li>
<li><code>analyticshub.subscriptions.get</code></li>
<li><code>analyticshub. subscriptions. list</code></li>
<li><code>analyticshub. subscriptions. update</code></li>
</ul>
<p><code>resourcemanager.projects.get</code></p>
<p><code>resourcemanager.projects.list</code></p></td>
</tr>
<tr class="odd">
<td>Analytics Hub Viewer
<p>( <code>roles/ analyticshub.viewer</code> )</p>
<p>Can browse Data Exchanges and Listings</p></td>
<td><p><code>analyticshub.dataExchanges.get</code></p>
<p><code>analyticshub. dataExchanges. getIamPolicy</code></p>
<p><code>analyticshub. dataExchanges. list</code></p>
<p><code>analyticshub.listings.get</code></p>
<p><code>analyticshub. listings. getIamPolicy</code></p>
<p><code>analyticshub.listings.list</code></p>
<p><code>analyticshub. queryTemplates. get</code></p>
<p><code>analyticshub. queryTemplates. list</code></p>
<p><code>resourcemanager.projects.get</code></p>
<p><code>resourcemanager.projects.list</code></p></td>
</tr>
<tr class="even">
<td>Analytics Hub Listing Admin
<p>( <code>roles/ analyticshub.listingAdmin</code> )</p>
<p>Grants full control over the Listing, including updating, deleting and setting ACLs</p></td>
<td><p><code>analyticshub.dataExchanges.get</code></p>
<p><code>analyticshub. dataExchanges. getIamPolicy</code></p>
<p><code>analyticshub. dataExchanges. list</code></p>
<p><code>analyticshub.listings.delete</code></p>
<p><code>analyticshub.listings.get</code></p>
<p><code>analyticshub. listings. getIamPolicy</code></p>
<p><code>analyticshub.listings.list</code></p>
<p><code>analyticshub. listings. setIamPolicy</code></p>
<p><code>analyticshub.listings.update</code></p>
<p><code>analyticshub. listings. viewSubscriptions</code></p>
<p><code>analyticshub. queryTemplates. get</code></p>
<p><code>analyticshub. queryTemplates. list</code></p>
<p><code>resourcemanager.projects.get</code></p>
<p><code>resourcemanager.projects.list</code></p></td>
</tr>
<tr class="odd">
<td>Analytics Hub Publisher
<p>( <code>roles/ analyticshub.publisher</code> )</p>
<p>Can publish to Data Exchanges thus creating Listings</p></td>
<td><p><code>analyticshub.dataExchanges.get</code></p>
<p><code>analyticshub. dataExchanges. getIamPolicy</code></p>
<p><code>analyticshub. dataExchanges. list</code></p>
<p><code>analyticshub.listings.create</code></p>
<p><code>analyticshub.listings.get</code></p>
<p><code>analyticshub. listings. getIamPolicy</code></p>
<p><code>analyticshub.listings.list</code></p>
<p><code>analyticshub.queryTemplates.*</code></p>
<ul>
<li><code>analyticshub. queryTemplates. approve</code></li>
<li><code>analyticshub. queryTemplates. create</code></li>
<li><code>analyticshub. queryTemplates. delete</code></li>
<li><code>analyticshub. queryTemplates. get</code></li>
<li><code>analyticshub. queryTemplates. list</code></li>
<li><code>analyticshub. queryTemplates. update</code></li>
</ul>
<p><code>resourcemanager.projects.get</code></p>
<p><code>resourcemanager.projects.list</code></p></td>
</tr>
<tr class="even">
<td>Analytics Hub Subscriber
<p>( <code>roles/ analyticshub.subscriber</code> )</p>
<p>Can browse Data Exchanges and subscribe to Listings</p></td>
<td><p><code>analyticshub.dataExchanges.get</code></p>
<p><code>analyticshub. dataExchanges. getIamPolicy</code></p>
<p><code>analyticshub. dataExchanges. list</code></p>
<p><code>analyticshub. dataExchanges. subscribe</code></p>
<p><code>analyticshub.listings.get</code></p>
<p><code>analyticshub. listings. getIamPolicy</code></p>
<p><code>analyticshub.listings.list</code></p>
<p><code>analyticshub. listings. subscribe</code></p>
<p><code>analyticshub. queryTemplates. get</code></p>
<p><code>analyticshub. queryTemplates. list</code></p>
<p><code>resourcemanager.projects.get</code></p>
<p><code>resourcemanager.projects.list</code></p></td>
</tr>
<tr class="odd">
<td>Analytics Hub Subscription Owner
<p>( <code>roles/ analyticshub.subscriptionOwner</code> )</p>
<p>Grants full control over the Subscription, including updating and deleting</p></td>
<td><p><code>analyticshub.dataExchanges.get</code></p>
<p><code>analyticshub. dataExchanges. getIamPolicy</code></p>
<p><code>analyticshub. dataExchanges. list</code></p>
<p><code>analyticshub.listings.get</code></p>
<p><code>analyticshub. listings. getIamPolicy</code></p>
<p><code>analyticshub.listings.list</code></p>
<p><code>analyticshub. queryTemplates. get</code></p>
<p><code>analyticshub. queryTemplates. list</code></p>
<p><code>analyticshub.subscriptions.*</code></p>
<ul>
<li><code>analyticshub. subscriptions. create</code></li>
<li><code>analyticshub. subscriptions. delete</code></li>
<li><code>analyticshub.subscriptions.get</code></li>
<li><code>analyticshub. subscriptions. list</code></li>
<li><code>analyticshub. subscriptions. update</code></li>
</ul>
<p><code>resourcemanager.projects.get</code></p>
<p><code>resourcemanager.projects.list</code></p></td>
</tr>
</tbody>
</table>

### Service agent roles

Service agent roles should only be granted to [service agents](https://docs.cloud.google.com/iam/docs/service-agents) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Role</th>
<th>Permissions</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Analytics Hub Service Agent
<p>( <code>roles/ analyticshub.serviceAgent</code> )</p>
<p>Grants Analytics Hub Service Agent permissions required to manage resources in the consumer project.</p>
<blockquote>
<strong>Warning:</strong> Do not grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote></td>
<td><p><code>analyticshub. dataExchanges. list</code></p>
<p><code>resourcemanager.projects.get</code></p>
<p><code>resourcemanager.projects.list</code></p></td>
</tr>
</tbody>
</table>

## BigQuery permissions

The following tables list the permissions available in BigQuery. These are included in predefined roles and can be used in custom role definitions. To search through all roles and permissions, see the [role and permission index](https://docs.cloud.google.com/iam/docs/roles-permissions) .

### BigQuery permissions

This table lists the IAM permissions for BigQuery and the roles that include them. To search through all roles and permissions, see the [role and permission index](https://docs.cloud.google.com/iam/docs/roles-permissions) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Permission</th>
<th>Included in roles</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>bigquery.bireservations.get</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code>roles/ bigquery.resourceAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code>roles/ bigquery.resourceEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceViewer">BigQuery Resource Viewer</a> ( <code>roles/ bigquery.resourceViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code>roles/ bigquery.user</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.bireservations.update</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code>roles/ bigquery.resourceAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery. capacityCommitments. create</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code>roles/ bigquery.resourceAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery. capacityCommitments. delete</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code>roles/ bigquery.resourceAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery. capacityCommitments. get</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code>roles/ bigquery.resourceAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code>roles/ bigquery.resourceEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceViewer">BigQuery Resource Viewer</a> ( <code>roles/ bigquery.resourceViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code>roles/ bigquery.user</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery. capacityCommitments. list</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code>roles/ bigquery.resourceAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code>roles/ bigquery.resourceEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceViewer">BigQuery Resource Viewer</a> ( <code>roles/ bigquery.resourceViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code>roles/ bigquery.user</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code>roles/ iam.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code>roles/ iam.securityReviewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.securityAuditor">Security Auditor</a> ( <code>roles/ iam.securityAuditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery. capacityCommitments. update</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code>roles/ bigquery.resourceAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.config.get</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code>roles/ bigquery.dataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.jobUser">BigQuery Job User</a> ( <code>roles/ bigquery.jobUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioUser">BigQuery Studio User</a> ( <code>roles/ bigquery.studioUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code>roles/ bigquery.user</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatatransfer#bigquerydatatransfer.serviceAgent">BigQuery Data Transfer Service Agent</a> ( <code>roles/ bigquerydatatransfer.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/enterpriseknowledgegraph#enterpriseknowledgegraph.serviceAgent">Enterprise Knowledge Graph Service Agent</a> ( <code>roles/ enterpriseknowledgegraph.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/fleetengine#fleetengine.serviceAgent">FleetEngine Service Agent</a> ( <code>roles/ fleetengine.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/looker#looker.serviceAgent">(Legacy) Looker Service Agent</a> ( <code>roles/ looker.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.config.update</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/assuredworkloads#assuredworkloads.admin">Assured Workloads Administrator</a> ( <code>roles/ assuredworkloads.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/assuredworkloads#assuredworkloads.editor">Assured Workloads Editor</a> ( <code>roles/ assuredworkloads.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.connections.create</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.connectionAdmin">BigQuery Connection Admin</a> ( <code>roles/ bigquery.connectionAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/chronicle#chronicle.serviceAgent">Chronicle Service Agent</a> ( <code>roles/ chronicle.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.connections.delegate</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.connectionAdmin">BigQuery Connection Admin</a> ( <code>roles/ bigquery.connectionAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datastream#datastream.bigqueryWriter">Datastream Bigquery Writer</a> ( <code>roles/ datastream.bigqueryWriter</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatatransfer#bigquerydatatransfer.serviceAgent">BigQuery Data Transfer Service Agent</a> ( <code>roles/ bigquerydatatransfer.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/chronicle#chronicle.serviceAgent">Chronicle Service Agent</a> ( <code>roles/ chronicle.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.discoveryBigLakePublishingServiceAgent">Dataplex Discovery BigLake Publishing Service Agent</a> ( <code>roles/ dataplex.discoveryBigLakePublishingServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datastream#datastream.serviceAgent">Datastream Service Agent</a> ( <code>roles/ datastream.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.connections.delete</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.connectionAdmin">BigQuery Connection Admin</a> ( <code>roles/ bigquery.connectionAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/chronicle#chronicle.serviceAgent">Chronicle Service Agent</a> ( <code>roles/ chronicle.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.connections.get</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.connectionAdmin">BigQuery Connection Admin</a> ( <code>roles/ bigquery.connectionAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.connectionUser">BigQuery Connection User</a> ( <code>roles/ bigquery.connectionUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datacatalog#datacatalog.admin">Data Catalog Admin</a> ( <code>roles/ datacatalog.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datacatalog#datacatalog.editor">Data Catalog Editor</a> ( <code>roles/ datacatalog.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datacatalog#datacatalog.viewer">Data Catalog Viewer</a> ( <code>roles/ datacatalog.viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datastream#datastream.bigqueryWriter">Datastream Bigquery Writer</a> ( <code>roles/ datastream.bigqueryWriter</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/chronicle#chronicle.serviceAgent">Chronicle Service Agent</a> ( <code>roles/ chronicle.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/deploymentmanager#clouddeploymentmanager.serviceAgent">Cloud Deployment Manager Service Agent</a> ( <code>roles/ clouddeploymentmanager.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datastream#datastream.serviceAgent">Datastream Service Agent</a> ( <code>roles/ datastream.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery. connections. getIamPolicy</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.connectionAdmin">BigQuery Connection Admin</a> ( <code>roles/ bigquery.connectionAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.connectionUser">BigQuery Connection User</a> ( <code>roles/ bigquery.connectionUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code>roles/ iam.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code>roles/ iam.securityReviewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.securityAuditor">Security Auditor</a> ( <code>roles/ iam.securityAuditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/chronicle#chronicle.serviceAgent">Chronicle Service Agent</a> ( <code>roles/ chronicle.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.connections.list</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.connectionAdmin">BigQuery Connection Admin</a> ( <code>roles/ bigquery.connectionAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.connectionUser">BigQuery Connection User</a> ( <code>roles/ bigquery.connectionUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code>roles/ iam.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code>roles/ iam.securityReviewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.securityAuditor">Security Auditor</a> ( <code>roles/ iam.securityAuditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/chronicle#chronicle.serviceAgent">Chronicle Service Agent</a> ( <code>roles/ chronicle.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery. connections. setIamPolicy</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.connectionAdmin">BigQuery Connection Admin</a> ( <code>roles/ bigquery.connectionAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code>roles/ iam.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.connections.update</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.connectionAdmin">BigQuery Connection Admin</a> ( <code>roles/ bigquery.connectionAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/chronicle#chronicle.serviceAgent">Chronicle Service Agent</a> ( <code>roles/ chronicle.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.connections.updateTag</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.connectionAdmin">BigQuery Connection Admin</a> ( <code>roles/ bigquery.connectionAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datacatalog#datacatalog.admin">Data Catalog Admin</a> ( <code>roles/ datacatalog.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datacatalog#datacatalog.tagEditor">Data Catalog Tag Editor</a> ( <code>roles/ datacatalog.tagEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/chronicle#chronicle.serviceAgent">Chronicle Service Agent</a> ( <code>roles/ chronicle.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.connections.use</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.connectionAdmin">BigQuery Connection Admin</a> ( <code>roles/ bigquery.connectionAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.connectionUser">BigQuery Connection User</a> ( <code>roles/ bigquery.connectionUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.routineAdmin">BigQuery Authorized Routine Admin</a> ( <code>roles/ bigquery.routineAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/chronicle#chronicle.serviceAgent">Chronicle Service Agent</a> ( <code>roles/ chronicle.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.discoveryBigLakePublishingServiceAgent">Dataplex Discovery BigLake Publishing Service Agent</a> ( <code>roles/ dataplex.discoveryBigLakePublishingServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.dataPolicies.attach</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.admin">BigQuery Data Policy Admin</a> ( <code>roles/ bigquerydatapolicy.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code>roles/ bigquery.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.dataPolicies.create</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.admin">BigQuery Data Policy Admin</a> ( <code>roles/ bigquerydatapolicy.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code>roles/ bigquery.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.dataPolicies.delete</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.admin">BigQuery Data Policy Admin</a> ( <code>roles/ bigquerydatapolicy.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code>roles/ bigquery.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.dataPolicies.get</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.admin">BigQuery Data Policy Admin</a> ( <code>roles/ bigquerydatapolicy.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.viewer">BigQuery Data Policy Viewer</a> ( <code>roles/ bigquerydatapolicy.viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code>roles/ bigquery.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery. dataPolicies. getIamPolicy</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.admin">BigQuery Data Policy Admin</a> ( <code>roles/ bigquerydatapolicy.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code>roles/ iam.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code>roles/ iam.securityReviewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code>roles/ bigquery.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.securityAuditor">Security Auditor</a> ( <code>roles/ iam.securityAuditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery. dataPolicies. getRawData</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.rawDataReader">Raw Data Reader</a> ( <code>roles/ bigquerydatapolicy.rawDataReader</code> )</p></td>
</tr>
<tr class="even">
<td><code>bigquery.dataPolicies.list</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.admin">BigQuery Data Policy Admin</a> ( <code>roles/ bigquerydatapolicy.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.viewer">BigQuery Data Policy Viewer</a> ( <code>roles/ bigquerydatapolicy.viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code>roles/ iam.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code>roles/ iam.securityReviewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code>roles/ bigquery.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.securityAuditor">Security Auditor</a> ( <code>roles/ iam.securityAuditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery. dataPolicies. maskedGet</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.maskedReader">Masked Reader</a> ( <code>roles/ bigquerydatapolicy.maskedReader</code> )</p></td>
</tr>
<tr class="even">
<td><code>bigquery. dataPolicies. setIamPolicy</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.admin">BigQuery Data Policy Admin</a> ( <code>roles/ bigquerydatapolicy.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code>roles/ iam.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code>roles/ bigquery.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.dataPolicies.update</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.admin">BigQuery Data Policy Admin</a> ( <code>roles/ bigquerydatapolicy.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code>roles/ bigquery.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.datasets.create</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code>roles/ bigquery.dataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code>roles/ bigquery.user</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/commercebusinessenablement#commercebusinessenablement.admin">Commerce Business Enablement Configuration Admin</a> ( <code>roles/ commercebusinessenablement.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datastream#datastream.bigqueryWriter">Datastream Bigquery Writer</a> ( <code>roles/ datastream.bigqueryWriter</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.batchPredictionServiceAgent">Vertex AI Batch Prediction Service Agent</a> ( <code>roles/ aiplatform.batchPredictionServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.customCodeServiceAgent">Vertex AI Custom Code Service Agent</a> ( <code>roles/ aiplatform.customCodeServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.modelMonitoringServiceAgent">Vertex AI Model Monitoring Service Agent</a> ( <code>roles/ aiplatform.modelMonitoringServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.ragServiceAgent">Vertex AI RAG Data Service Agent</a> ( <code>roles/ aiplatform.ragServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.serviceAgent">Vertex AI Service Agent</a> ( <code>roles/ aiplatform.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.tuningServiceAgent">Vertex AI Tuning Service Agent</a> ( <code>roles/ aiplatform.tuningServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/automl#automl.serviceAgent">AutoML Service Agent</a> ( <code>roles/ automl.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/automlrecommendations#automlrecommendations.serviceAgent">Recommendations AI Service Agent</a> ( <code>roles/ automlrecommendations.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/ces#ces.serviceAgent">Customer Engagement Suite Service Agent</a> ( <code>roles/ ces.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/chronicle#chronicle.serviceAgent">Chronicle Service Agent</a> ( <code>roles/ chronicle.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/deploymentmanager#clouddeploymentmanager.serviceAgent">Cloud Deployment Manager Service Agent</a> ( <code>roles/ clouddeploymentmanager.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/contactcenterinsights#contactcenterinsights.serviceAgent">Contact Center AI Insights Service Agent</a> ( <code>roles/ contactcenterinsights.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/container#container.serviceAgent">Kubernetes Engine Service Agent</a> ( <code>roles/ container.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datalabeling#datalabeling.serviceAgent">Data Labeling Service Agent</a> ( <code>roles/ datalabeling.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.discoveryPublishingServiceAgent">Dataplex Discovery Publishing Service Agent</a> ( <code>roles/ dataplex.discoveryPublishingServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datastream#datastream.serviceAgent">Datastream Service Agent</a> ( <code>roles/ datastream.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dialogflow#dialogflow.serviceAgent">Dialogflow Service Agent</a> ( <code>roles/ dialogflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/discoveryengine#discoveryengine.serviceAgent">Discovery Engine Service Agent</a> ( <code>roles/ discoveryengine.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/enterpriseknowledgegraph#enterpriseknowledgegraph.serviceAgent">Enterprise Knowledge Graph Service Agent</a> ( <code>roles/ enterpriseknowledgegraph.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/firebase#firebase.managementServiceAgent">Firebase Service Management Service Agent</a> ( <code>roles/ firebase.managementServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/firebasecrash#firebasecrashlytics.serviceAgent">Firebase Crashlytics Service Agent</a> ( <code>roles/ firebasecrashlytics.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/fleetengine#fleetengine.serviceAgent">FleetEngine Service Agent</a> ( <code>roles/ fleetengine.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/logging#logging.serviceAgent">Cloud Logging Service Agent</a> ( <code>roles/ logging.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/ml#ml.serviceAgent">AI Platform Service Agent</a> ( <code>roles/ ml.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/observability#observability.serviceAgent">Observability Service Agent</a> ( <code>roles/ observability.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/retail#retail.serviceAgent">Retail Service Agent</a> ( <code>roles/ retail.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/spectrumsas#spectrumsas.serviceAgent">Spectrum SAS Service Agent</a> ( <code>roles/ spectrumsas.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/storageinsights#storageinsights.serviceAgent">StorageInsights Service Agent</a> ( <code>roles/ storageinsights.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/visionai#visionai.serviceAgent">Cloud Vision AI Service Agent</a> ( <code>roles/ visionai.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery. datasets. createTagBinding</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/resourcemanager#resourcemanager.tagUser">Tag User</a> ( <code>roles/ resourcemanager.tagUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code>roles/ bigquery.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dspm#dspm.serviceAgent">DSPM Service Agent</a> ( <code>roles/ dspm.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.datasets.delete</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/deploymentmanager#clouddeploymentmanager.serviceAgent">Cloud Deployment Manager Service Agent</a> ( <code>roles/ clouddeploymentmanager.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery. datasets. deleteTagBinding</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/resourcemanager#resourcemanager.tagUser">Tag User</a> ( <code>roles/ resourcemanager.tagUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code>roles/ bigquery.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dspm#dspm.serviceAgent">DSPM Service Agent</a> ( <code>roles/ dspm.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.datasets.get</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code>roles/ bigquery.dataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataViewer">BigQuery Data Viewer</a> ( <code>roles/ bigquery.dataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.metadataViewer">BigQuery Metadata Viewer</a> ( <code>roles/ bigquery.metadataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code>roles/ bigquery.user</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/commercebusinessenablement#commercebusinessenablement.admin">Commerce Business Enablement Configuration Admin</a> ( <code>roles/ commercebusinessenablement.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datacatalog#datacatalog.admin">Data Catalog Admin</a> ( <code>roles/ datacatalog.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datacatalog#datacatalog.editor">Data Catalog Editor</a> ( <code>roles/ datacatalog.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datacatalog#datacatalog.viewer">Data Catalog Viewer</a> ( <code>roles/ datacatalog.viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.routineAdmin">BigQuery Authorized Routine Admin</a> ( <code>roles/ bigquery.routineAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.routineDataEditor">BigQuery Authorized Routine Data Editor</a> ( <code>roles/ bigquery.routineDataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.routineDataViewer">BigQuery Authorized Routine Data Viewer</a> ( <code>roles/ bigquery.routineDataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.routineMetadataViewer">BigQuery Authorized Routine Metadata Viewer</a> ( <code>roles/ bigquery.routineMetadataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code>roles/ bigquery.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code>roles/ dataplex.storageDataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.storageDataReader">Dataplex Storage Data Reader</a> ( <code>roles/ dataplex.storageDataReader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datastream#datastream.bigqueryWriter">Datastream Bigquery Writer</a> ( <code>roles/ datastream.bigqueryWriter</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.securityAuditor">Security Auditor</a> ( <code>roles/ iam.securityAuditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.siteReliabilityEngineer">Site Reliability Engineer</a> ( <code>roles/ iam.siteReliabilityEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/securedlandingzone#securedlandingzone.bqdwProjectRemediator">SLZ BQDW Blueprint Project Level Remediator</a> ( <code>roles/ securedlandingzone.bqdwProjectRemediator</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.batchPredictionServiceAgent">Vertex AI Batch Prediction Service Agent</a> ( <code>roles/ aiplatform.batchPredictionServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.customCodeServiceAgent">Vertex AI Custom Code Service Agent</a> ( <code>roles/ aiplatform.customCodeServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.modelMonitoringServiceAgent">Vertex AI Model Monitoring Service Agent</a> ( <code>roles/ aiplatform.modelMonitoringServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.ragServiceAgent">Vertex AI RAG Data Service Agent</a> ( <code>roles/ aiplatform.ragServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.serviceAgent">Vertex AI Service Agent</a> ( <code>roles/ aiplatform.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.tuningServiceAgent">Vertex AI Tuning Service Agent</a> ( <code>roles/ aiplatform.tuningServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/auditmanager#auditmanager.serviceAgent">Audit Manager Auditing Service Agent</a> ( <code>roles/ auditmanager.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/automl#automl.serviceAgent">AutoML Service Agent</a> ( <code>roles/ automl.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/automlrecommendations#automlrecommendations.serviceAgent">Recommendations AI Service Agent</a> ( <code>roles/ automlrecommendations.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.connectedSheetsServiceAgent">Connected Sheets Service Agent</a> ( <code>roles/ bigquery.connectedSheetsServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/ces#ces.serviceAgent">Customer Engagement Suite Service Agent</a> ( <code>roles/ ces.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/cloudasset#cloudasset.serviceAgent">Cloud Asset Service Agent</a> ( <code>roles/ cloudasset.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/deploymentmanager#clouddeploymentmanager.serviceAgent">Cloud Deployment Manager Service Agent</a> ( <code>roles/ clouddeploymentmanager.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/cloudsecuritycompliance#cloudsecuritycompliance.serviceAgent">Cloud Security Compliance Service Agent</a> ( <code>roles/ cloudsecuritycompliance.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/contactcenterinsights#contactcenterinsights.serviceAgent">Contact Center AI Insights Service Agent</a> ( <code>roles/ contactcenterinsights.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/container#container.serviceAgent">Kubernetes Engine Service Agent</a> ( <code>roles/ container.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datalabeling#datalabeling.serviceAgent">Data Labeling Service Agent</a> ( <code>roles/ datalabeling.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.discoveryPublishingServiceAgent">Dataplex Discovery Publishing Service Agent</a> ( <code>roles/ dataplex.discoveryPublishingServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datastream#datastream.serviceAgent">Datastream Service Agent</a> ( <code>roles/ datastream.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datastudio#datastudio.managedStorageServiceAgent">Data Studio Managed Storage Service Agent</a> ( <code>roles/ datastudio.managedStorageServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/discoveryengine#discoveryengine.serviceAgent">Discovery Engine Service Agent</a> ( <code>roles/ discoveryengine.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/enterpriseknowledgegraph#enterpriseknowledgegraph.serviceAgent">Enterprise Knowledge Graph Service Agent</a> ( <code>roles/ enterpriseknowledgegraph.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/firebase#firebase.managementServiceAgent">Firebase Service Management Service Agent</a> ( <code>roles/ firebase.managementServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/firebasecrash#firebasecrashlytics.serviceAgent">Firebase Crashlytics Service Agent</a> ( <code>roles/ firebasecrashlytics.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/fleetengine#fleetengine.serviceAgent">FleetEngine Service Agent</a> ( <code>roles/ fleetengine.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/logging#logging.serviceAgent">Cloud Logging Service Agent</a> ( <code>roles/ logging.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/looker#looker.serviceAgent">(Legacy) Looker Service Agent</a> ( <code>roles/ looker.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/ml#ml.serviceAgent">AI Platform Service Agent</a> ( <code>roles/ ml.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/observability#observability.serviceAgent">Observability Service Agent</a> ( <code>roles/ observability.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/retail#retail.serviceAgent">Retail Service Agent</a> ( <code>roles/ retail.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/securitycenter#securitycenter.controlServiceAgent">Security Center Control Service Agent</a> ( <code>roles/ securitycenter.controlServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/securitycenter#securitycenter.securityHealthAnalyticsServiceAgent">Security Health Analytics Service Agent</a> ( <code>roles/ securitycenter.securityHealthAnalyticsServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/securitycenter#securitycenter.serviceAgent">Security Center Service Agent</a> ( <code>roles/ securitycenter.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/visionai#visionai.serviceAgent">Cloud Vision AI Service Agent</a> ( <code>roles/ visionai.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.datasets.getIamPolicy</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code>roles/ bigquery.dataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataViewer">BigQuery Data Viewer</a> ( <code>roles/ bigquery.dataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.metadataViewer">BigQuery Metadata Viewer</a> ( <code>roles/ bigquery.metadataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code>roles/ bigquery.user</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code>roles/ iam.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code>roles/ iam.securityReviewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code>roles/ bigquery.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.securityAuditor">Security Auditor</a> ( <code>roles/ iam.securityAuditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.siteReliabilityEngineer">Site Reliability Engineer</a> ( <code>roles/ iam.siteReliabilityEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/securedlandingzone#securedlandingzone.bqdwProjectRemediator">SLZ BQDW Blueprint Project Level Remediator</a> ( <code>roles/ securedlandingzone.bqdwProjectRemediator</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/deploymentmanager#clouddeploymentmanager.serviceAgent">Cloud Deployment Manager Service Agent</a> ( <code>roles/ clouddeploymentmanager.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/firebase#firebase.managementServiceAgent">Firebase Service Management Service Agent</a> ( <code>roles/ firebase.managementServiceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.datasets.link</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/logging#logging.serviceAgent">Cloud Logging Service Agent</a> ( <code>roles/ logging.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/observability#observability.serviceAgent">Observability Service Agent</a> ( <code>roles/ observability.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery. datasets. listEffectiveTags</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/resourcemanager#resourcemanager.tagUser">Tag User</a> ( <code>roles/ resourcemanager.tagUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/resourcemanager#resourcemanager.tagViewer">Tag Viewer</a> ( <code>roles/ resourcemanager.tagViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code>roles/ bigquery.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.securityAuditor">Security Auditor</a> ( <code>roles/ iam.securityAuditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dspm#dspm.serviceAgent">DSPM Service Agent</a> ( <code>roles/ dspm.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery. datasets. listSharedDatasetUsage</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code>roles/ bigquery.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery. datasets. listTagBindings</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/resourcemanager#resourcemanager.tagUser">Tag User</a> ( <code>roles/ resourcemanager.tagUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/resourcemanager#resourcemanager.tagViewer">Tag Viewer</a> ( <code>roles/ resourcemanager.tagViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code>roles/ bigquery.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.securityAuditor">Security Auditor</a> ( <code>roles/ iam.securityAuditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dspm#dspm.serviceAgent">DSPM Service Agent</a> ( <code>roles/ dspm.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.datasets.setIamPolicy</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code>roles/ iam.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code>roles/ bigquery.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/securedlandingzone#securedlandingzone.bqdwProjectRemediator">SLZ BQDW Blueprint Project Level Remediator</a> ( <code>roles/ securedlandingzone.bqdwProjectRemediator</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/firebase#firebase.managementServiceAgent">Firebase Service Management Service Agent</a> ( <code>roles/ firebase.managementServiceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.datasets.update</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/commercebusinessenablement#commercebusinessenablement.admin">Commerce Business Enablement Configuration Admin</a> ( <code>roles/ commercebusinessenablement.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code>roles/ bigquery.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/securedlandingzone#securedlandingzone.bqdwProjectRemediator">SLZ BQDW Blueprint Project Level Remediator</a> ( <code>roles/ securedlandingzone.bqdwProjectRemediator</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/deploymentmanager#clouddeploymentmanager.serviceAgent">Cloud Deployment Manager Service Agent</a> ( <code>roles/ clouddeploymentmanager.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/firebase#firebase.managementServiceAgent">Firebase Service Management Service Agent</a> ( <code>roles/ firebase.managementServiceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.datasets.updateTag</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code>roles/ bigquery.dataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datacatalog#datacatalog.admin">Data Catalog Admin</a> ( <code>roles/ datacatalog.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code>roles/ bigquery.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datacatalog#datacatalog.tagEditor">Data Catalog Tag Editor</a> ( <code>roles/ datacatalog.tagEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/ces#ces.serviceAgent">Customer Engagement Suite Service Agent</a> ( <code>roles/ ces.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.jobs.create</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.jobUser">BigQuery Job User</a> ( <code>roles/ bigquery.jobUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioUser">BigQuery Studio User</a> ( <code>roles/ bigquery.studioUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code>roles/ bigquery.user</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datastream#datastream.bigqueryWriter">Datastream Bigquery Writer</a> ( <code>roles/ datastream.bigqueryWriter</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.batchPredictionServiceAgent">Vertex AI Batch Prediction Service Agent</a> ( <code>roles/ aiplatform.batchPredictionServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.customCodeServiceAgent">Vertex AI Custom Code Service Agent</a> ( <code>roles/ aiplatform.customCodeServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.modelMonitoringServiceAgent">Vertex AI Model Monitoring Service Agent</a> ( <code>roles/ aiplatform.modelMonitoringServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.ragServiceAgent">Vertex AI RAG Data Service Agent</a> ( <code>roles/ aiplatform.ragServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.serviceAgent">Vertex AI Service Agent</a> ( <code>roles/ aiplatform.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.tuningServiceAgent">Vertex AI Tuning Service Agent</a> ( <code>roles/ aiplatform.tuningServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/automl#automl.serviceAgent">AutoML Service Agent</a> ( <code>roles/ automl.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/automlrecommendations#automlrecommendations.serviceAgent">Recommendations AI Service Agent</a> ( <code>roles/ automlrecommendations.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.connectedSheetsServiceAgent">Connected Sheets Service Agent</a> ( <code>roles/ bigquery.connectedSheetsServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatatransfer#bigquerydatatransfer.serviceAgent">BigQuery Data Transfer Service Agent</a> ( <code>roles/ bigquerydatatransfer.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigqueryomni#bigqueryomni.serviceAgent">BigQuery Omni Service Agent</a> ( <code>roles/ bigqueryomni.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/ces#ces.serviceAgent">Customer Engagement Suite Service Agent</a> ( <code>roles/ ces.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/chronicle#chronicle.serviceAgent">Chronicle Service Agent</a> ( <code>roles/ chronicle.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/cloudasset#cloudasset.serviceAgent">Cloud Asset Service Agent</a> ( <code>roles/ cloudasset.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/deploymentmanager#clouddeploymentmanager.serviceAgent">Cloud Deployment Manager Service Agent</a> ( <code>roles/ clouddeploymentmanager.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/contactcenterinsights#contactcenterinsights.serviceAgent">Contact Center AI Insights Service Agent</a> ( <code>roles/ contactcenterinsights.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datalabeling#datalabeling.serviceAgent">Data Labeling Service Agent</a> ( <code>roles/ datalabeling.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datastream#datastream.serviceAgent">Datastream Service Agent</a> ( <code>roles/ datastream.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datastudio#datastudio.serviceAgent">Data Studio Service Agent</a> ( <code>roles/ datastudio.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dialogflow#dialogflow.serviceAgent">Dialogflow Service Agent</a> ( <code>roles/ dialogflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/discoveryengine#discoveryengine.serviceAgent">Discovery Engine Service Agent</a> ( <code>roles/ discoveryengine.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dspm#dspm.serviceAgent">DSPM Service Agent</a> ( <code>roles/ dspm.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/enterpriseknowledgegraph#enterpriseknowledgegraph.serviceAgent">Enterprise Knowledge Graph Service Agent</a> ( <code>roles/ enterpriseknowledgegraph.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/fleetengine#fleetengine.serviceAgent">FleetEngine Service Agent</a> ( <code>roles/ fleetengine.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/looker#looker.serviceAgent">(Legacy) Looker Service Agent</a> ( <code>roles/ looker.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/ml#ml.serviceAgent">AI Platform Service Agent</a> ( <code>roles/ ml.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/monitoring#monitoring.notificationServiceAgent">Monitoring Service Agent</a> ( <code>roles/ monitoring.notificationServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/retail#retail.serviceAgent">Retail Service Agent</a> ( <code>roles/ retail.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/spectrumsas#spectrumsas.serviceAgent">Spectrum SAS Service Agent</a> ( <code>roles/ spectrumsas.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/visionai#visionai.serviceAgent">Cloud Vision AI Service Agent</a> ( <code>roles/ visionai.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery. jobs. createGlobalQuery</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.jobs.delete</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datastream#datastream.bigqueryWriter">Datastream Bigquery Writer</a> ( <code>roles/ datastream.bigqueryWriter</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datastream#datastream.serviceAgent">Datastream Service Agent</a> ( <code>roles/ datastream.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.jobs.get</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code>roles/ bigquery.resourceAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code>roles/ bigquery.resourceEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceViewer">BigQuery Resource Viewer</a> ( <code>roles/ bigquery.resourceViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datastream#datastream.bigqueryWriter">Datastream Bigquery Writer</a> ( <code>roles/ datastream.bigqueryWriter</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.batchPredictionServiceAgent">Vertex AI Batch Prediction Service Agent</a> ( <code>roles/ aiplatform.batchPredictionServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.customCodeServiceAgent">Vertex AI Custom Code Service Agent</a> ( <code>roles/ aiplatform.customCodeServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.modelMonitoringServiceAgent">Vertex AI Model Monitoring Service Agent</a> ( <code>roles/ aiplatform.modelMonitoringServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.ragServiceAgent">Vertex AI RAG Data Service Agent</a> ( <code>roles/ aiplatform.ragServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.serviceAgent">Vertex AI Service Agent</a> ( <code>roles/ aiplatform.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.tuningServiceAgent">Vertex AI Tuning Service Agent</a> ( <code>roles/ aiplatform.tuningServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/automlrecommendations#automlrecommendations.serviceAgent">Recommendations AI Service Agent</a> ( <code>roles/ automlrecommendations.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/chronicle#chronicle.serviceAgent">Chronicle Service Agent</a> ( <code>roles/ chronicle.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/cloudasset#cloudasset.serviceAgent">Cloud Asset Service Agent</a> ( <code>roles/ cloudasset.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/contactcenterinsights#contactcenterinsights.serviceAgent">Contact Center AI Insights Service Agent</a> ( <code>roles/ contactcenterinsights.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datalabeling#datalabeling.serviceAgent">Data Labeling Service Agent</a> ( <code>roles/ datalabeling.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datastream#datastream.serviceAgent">Datastream Service Agent</a> ( <code>roles/ datastream.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/discoveryengine#discoveryengine.serviceAgent">Discovery Engine Service Agent</a> ( <code>roles/ discoveryengine.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/ml#ml.serviceAgent">AI Platform Service Agent</a> ( <code>roles/ ml.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/retail#retail.serviceAgent">Retail Service Agent</a> ( <code>roles/ retail.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/visionai#visionai.serviceAgent">Cloud Vision AI Service Agent</a> ( <code>roles/ visionai.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.jobs.list</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code>roles/ bigquery.resourceAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code>roles/ bigquery.resourceEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceViewer">BigQuery Resource Viewer</a> ( <code>roles/ bigquery.resourceViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code>roles/ bigquery.user</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code>roles/ iam.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code>roles/ iam.securityReviewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datastream#datastream.bigqueryWriter">Datastream Bigquery Writer</a> ( <code>roles/ datastream.bigqueryWriter</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.securityAuditor">Security Auditor</a> ( <code>roles/ iam.securityAuditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/automlrecommendations#automlrecommendations.serviceAgent">Recommendations AI Service Agent</a> ( <code>roles/ automlrecommendations.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datastream#datastream.serviceAgent">Datastream Service Agent</a> ( <code>roles/ datastream.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/discoveryengine#discoveryengine.serviceAgent">Discovery Engine Service Agent</a> ( <code>roles/ discoveryengine.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/ml#ml.serviceAgent">AI Platform Service Agent</a> ( <code>roles/ ml.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/retail#retail.serviceAgent">Retail Service Agent</a> ( <code>roles/ retail.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.jobs.listAll</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code>roles/ bigquery.resourceAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code>roles/ bigquery.resourceEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceViewer">BigQuery Resource Viewer</a> ( <code>roles/ bigquery.resourceViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery. jobs. listExecutionMetadata</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code>roles/ bigquery.resourceAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code>roles/ bigquery.resourceEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceViewer">BigQuery Resource Viewer</a> ( <code>roles/ bigquery.resourceViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.jobs.update</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datastream#datastream.bigqueryWriter">Datastream Bigquery Writer</a> ( <code>roles/ datastream.bigqueryWriter</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/automlrecommendations#automlrecommendations.serviceAgent">Recommendations AI Service Agent</a> ( <code>roles/ automlrecommendations.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datastream#datastream.serviceAgent">Datastream Service Agent</a> ( <code>roles/ datastream.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/discoveryengine#discoveryengine.serviceAgent">Discovery Engine Service Agent</a> ( <code>roles/ discoveryengine.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/ml#ml.serviceAgent">AI Platform Service Agent</a> ( <code>roles/ ml.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/retail#retail.serviceAgent">Retail Service Agent</a> ( <code>roles/ retail.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.models.create</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code>roles/ bigquery.dataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code>roles/ dataplex.storageDataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.batchPredictionServiceAgent">Vertex AI Batch Prediction Service Agent</a> ( <code>roles/ aiplatform.batchPredictionServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.serviceAgent">Vertex AI Service Agent</a> ( <code>roles/ aiplatform.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.models.delete</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code>roles/ bigquery.dataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code>roles/ dataplex.storageDataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.models.export</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code>roles/ bigquery.dataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataViewer">BigQuery Data Viewer</a> ( <code>roles/ bigquery.dataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code>roles/ dataplex.storageDataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.storageDataReader">Dataplex Storage Data Reader</a> ( <code>roles/ dataplex.storageDataReader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.siteReliabilityEngineer">Site Reliability Engineer</a> ( <code>roles/ iam.siteReliabilityEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.batchPredictionServiceAgent">Vertex AI Batch Prediction Service Agent</a> ( <code>roles/ aiplatform.batchPredictionServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.serviceAgent">Vertex AI Service Agent</a> ( <code>roles/ aiplatform.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/looker#looker.serviceAgent">(Legacy) Looker Service Agent</a> ( <code>roles/ looker.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/visionai#visionai.serviceAgent">Cloud Vision AI Service Agent</a> ( <code>roles/ visionai.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.models.getData</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code>roles/ bigquery.dataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataViewer">BigQuery Data Viewer</a> ( <code>roles/ bigquery.dataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.routineAdmin">BigQuery Authorized Routine Admin</a> ( <code>roles/ bigquery.routineAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.routineDataEditor">BigQuery Authorized Routine Data Editor</a> ( <code>roles/ bigquery.routineDataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.routineDataViewer">BigQuery Authorized Routine Data Viewer</a> ( <code>roles/ bigquery.routineDataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code>roles/ dataplex.storageDataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.storageDataReader">Dataplex Storage Data Reader</a> ( <code>roles/ dataplex.storageDataReader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.siteReliabilityEngineer">Site Reliability Engineer</a> ( <code>roles/ iam.siteReliabilityEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.batchPredictionServiceAgent">Vertex AI Batch Prediction Service Agent</a> ( <code>roles/ aiplatform.batchPredictionServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.serviceAgent">Vertex AI Service Agent</a> ( <code>roles/ aiplatform.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/looker#looker.serviceAgent">(Legacy) Looker Service Agent</a> ( <code>roles/ looker.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.models.getMetadata</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code>roles/ bigquery.dataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataViewer">BigQuery Data Viewer</a> ( <code>roles/ bigquery.dataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.metadataViewer">BigQuery Metadata Viewer</a> ( <code>roles/ bigquery.metadataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datacatalog#datacatalog.admin">Data Catalog Admin</a> ( <code>roles/ datacatalog.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datacatalog#datacatalog.editor">Data Catalog Editor</a> ( <code>roles/ datacatalog.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datacatalog#datacatalog.viewer">Data Catalog Viewer</a> ( <code>roles/ datacatalog.viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.routineAdmin">BigQuery Authorized Routine Admin</a> ( <code>roles/ bigquery.routineAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.routineDataEditor">BigQuery Authorized Routine Data Editor</a> ( <code>roles/ bigquery.routineDataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.routineDataViewer">BigQuery Authorized Routine Data Viewer</a> ( <code>roles/ bigquery.routineDataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.routineMetadataViewer">BigQuery Authorized Routine Metadata Viewer</a> ( <code>roles/ bigquery.routineMetadataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code>roles/ dataplex.storageDataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.storageDataReader">Dataplex Storage Data Reader</a> ( <code>roles/ dataplex.storageDataReader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.securityAuditor">Security Auditor</a> ( <code>roles/ iam.securityAuditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.siteReliabilityEngineer">Site Reliability Engineer</a> ( <code>roles/ iam.siteReliabilityEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/looker#looker.serviceAgent">(Legacy) Looker Service Agent</a> ( <code>roles/ looker.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.models.list</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code>roles/ bigquery.dataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataViewer">BigQuery Data Viewer</a> ( <code>roles/ bigquery.dataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.metadataViewer">BigQuery Metadata Viewer</a> ( <code>roles/ bigquery.metadataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code>roles/ bigquery.user</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code>roles/ iam.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code>roles/ iam.securityReviewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code>roles/ dataplex.storageDataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.storageDataReader">Dataplex Storage Data Reader</a> ( <code>roles/ dataplex.storageDataReader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.securityAuditor">Security Auditor</a> ( <code>roles/ iam.securityAuditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.siteReliabilityEngineer">Site Reliability Engineer</a> ( <code>roles/ iam.siteReliabilityEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/looker#looker.serviceAgent">(Legacy) Looker Service Agent</a> ( <code>roles/ looker.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.models.updateData</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code>roles/ bigquery.dataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code>roles/ dataplex.storageDataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.models.updateMetadata</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code>roles/ bigquery.dataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code>roles/ dataplex.storageDataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.models.updateTag</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code>roles/ bigquery.dataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datacatalog#datacatalog.admin">Data Catalog Admin</a> ( <code>roles/ datacatalog.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datacatalog#datacatalog.tagEditor">Data Catalog Tag Editor</a> ( <code>roles/ datacatalog.tagEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.objectRefs.read</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.objectRefAdmin">BigQuery ObjectRef Admin</a> ( <code>roles/ bigquery.objectRefAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.objectRefReader">BigQuery ObjectRef Reader</a> ( <code>roles/ bigquery.objectRefReader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.serviceAgent">Vertex AI Service Agent</a> ( <code>roles/ aiplatform.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.objectRefs.write</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.objectRefAdmin">BigQuery ObjectRef Admin</a> ( <code>roles/ bigquery.objectRefAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.propertyGraphs.create</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code>roles/ bigquery.dataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.propertyGraphs.delete</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code>roles/ bigquery.dataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.propertyGraphs.get</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code>roles/ bigquery.dataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataViewer">BigQuery Data Viewer</a> ( <code>roles/ bigquery.dataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.metadataViewer">BigQuery Metadata Viewer</a> ( <code>roles/ bigquery.metadataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.securityAuditor">Security Auditor</a> ( <code>roles/ iam.securityAuditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.siteReliabilityEngineer">Site Reliability Engineer</a> ( <code>roles/ iam.siteReliabilityEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.propertyGraphs.list</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code>roles/ bigquery.dataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataViewer">BigQuery Data Viewer</a> ( <code>roles/ bigquery.dataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.metadataViewer">BigQuery Metadata Viewer</a> ( <code>roles/ bigquery.metadataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code>roles/ bigquery.user</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code>roles/ iam.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code>roles/ iam.securityReviewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.securityAuditor">Security Auditor</a> ( <code>roles/ iam.securityAuditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.siteReliabilityEngineer">Site Reliability Engineer</a> ( <code>roles/ iam.siteReliabilityEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.propertyGraphs.update</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code>roles/ bigquery.dataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.readsessions.create</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.readSessionUser">BigQuery Read Session User</a> ( <code>roles/ bigquery.readSessionUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioUser">BigQuery Studio User</a> ( <code>roles/ bigquery.studioUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code>roles/ bigquery.user</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.batchPredictionServiceAgent">Vertex AI Batch Prediction Service Agent</a> ( <code>roles/ aiplatform.batchPredictionServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.customCodeServiceAgent">Vertex AI Custom Code Service Agent</a> ( <code>roles/ aiplatform.customCodeServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.ragServiceAgent">Vertex AI RAG Data Service Agent</a> ( <code>roles/ aiplatform.ragServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.serviceAgent">Vertex AI Service Agent</a> ( <code>roles/ aiplatform.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/enterpriseknowledgegraph#enterpriseknowledgegraph.serviceAgent">Enterprise Knowledge Graph Service Agent</a> ( <code>roles/ enterpriseknowledgegraph.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/visionai#visionai.serviceAgent">Cloud Vision AI Service Agent</a> ( <code>roles/ visionai.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.readsessions.getData</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.readSessionUser">BigQuery Read Session User</a> ( <code>roles/ bigquery.readSessionUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioUser">BigQuery Studio User</a> ( <code>roles/ bigquery.studioUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code>roles/ bigquery.user</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.batchPredictionServiceAgent">Vertex AI Batch Prediction Service Agent</a> ( <code>roles/ aiplatform.batchPredictionServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.customCodeServiceAgent">Vertex AI Custom Code Service Agent</a> ( <code>roles/ aiplatform.customCodeServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.ragServiceAgent">Vertex AI RAG Data Service Agent</a> ( <code>roles/ aiplatform.ragServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.serviceAgent">Vertex AI Service Agent</a> ( <code>roles/ aiplatform.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/enterpriseknowledgegraph#enterpriseknowledgegraph.serviceAgent">Enterprise Knowledge Graph Service Agent</a> ( <code>roles/ enterpriseknowledgegraph.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.readsessions.update</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.readSessionUser">BigQuery Read Session User</a> ( <code>roles/ bigquery.readSessionUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioUser">BigQuery Studio User</a> ( <code>roles/ bigquery.studioUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code>roles/ bigquery.user</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery. reservationAssignments. create</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code>roles/ bigquery.resourceAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code>roles/ bigquery.resourceEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery. reservationAssignments. delete</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code>roles/ bigquery.resourceAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code>roles/ bigquery.resourceEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery. reservationAssignments. list</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code>roles/ bigquery.resourceAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code>roles/ bigquery.resourceEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceViewer">BigQuery Resource Viewer</a> ( <code>roles/ bigquery.resourceViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code>roles/ bigquery.user</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code>roles/ iam.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code>roles/ iam.securityReviewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.securityAuditor">Security Auditor</a> ( <code>roles/ iam.securityAuditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery. reservationAssignments. search</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code>roles/ bigquery.resourceAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code>roles/ bigquery.resourceEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceViewer">BigQuery Resource Viewer</a> ( <code>roles/ bigquery.resourceViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code>roles/ bigquery.user</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery. reservationGroups. create</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code>roles/ bigquery.resourceAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code>roles/ bigquery.resourceEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery. reservationGroups. delete</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code>roles/ bigquery.resourceAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code>roles/ bigquery.resourceEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.reservationGroups.get</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code>roles/ bigquery.resourceAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code>roles/ bigquery.resourceEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceViewer">BigQuery Resource Viewer</a> ( <code>roles/ bigquery.resourceViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code>roles/ bigquery.user</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery. reservationGroups. list</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code>roles/ bigquery.resourceAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code>roles/ bigquery.resourceEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceViewer">BigQuery Resource Viewer</a> ( <code>roles/ bigquery.resourceViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code>roles/ bigquery.user</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code>roles/ iam.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code>roles/ iam.securityReviewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.securityAuditor">Security Auditor</a> ( <code>roles/ iam.securityAuditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery. reservationGroups. update</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code>roles/ bigquery.resourceAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code>roles/ bigquery.resourceEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.reservations.create</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code>roles/ bigquery.resourceAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code>roles/ bigquery.resourceEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.reservations.delete</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code>roles/ bigquery.resourceAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code>roles/ bigquery.resourceEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.reservations.get</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code>roles/ bigquery.resourceAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code>roles/ bigquery.resourceEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceViewer">BigQuery Resource Viewer</a> ( <code>roles/ bigquery.resourceViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code>roles/ bigquery.user</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery. reservations. getIamPolicy</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code>roles/ bigquery.resourceAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code>roles/ iam.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code>roles/ iam.securityReviewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.securityAuditor">Security Auditor</a> ( <code>roles/ iam.securityAuditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.reservations.list</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code>roles/ bigquery.resourceAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code>roles/ bigquery.resourceEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceViewer">BigQuery Resource Viewer</a> ( <code>roles/ bigquery.resourceViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code>roles/ bigquery.user</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code>roles/ iam.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code>roles/ iam.securityReviewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.securityAuditor">Security Auditor</a> ( <code>roles/ iam.securityAuditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery. reservations. listFailoverDatasets</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code>roles/ bigquery.resourceAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code>roles/ bigquery.resourceEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceViewer">BigQuery Resource Viewer</a> ( <code>roles/ bigquery.resourceViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code>roles/ bigquery.user</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery. reservations. setIamPolicy</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code>roles/ bigquery.resourceAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code>roles/ iam.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.reservations.update</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code>roles/ bigquery.resourceAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code>roles/ bigquery.resourceEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.reservations.use</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code>roles/ bigquery.resourceAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code>roles/ bigquery.resourceEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code>roles/ bigquery.user</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.routines.create</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code>roles/ bigquery.dataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code>roles/ dataplex.storageDataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/deploymentmanager#clouddeploymentmanager.serviceAgent">Cloud Deployment Manager Service Agent</a> ( <code>roles/ clouddeploymentmanager.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.routines.delete</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code>roles/ bigquery.dataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code>roles/ dataplex.storageDataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.routines.get</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code>roles/ bigquery.dataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataViewer">BigQuery Data Viewer</a> ( <code>roles/ bigquery.dataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.metadataViewer">BigQuery Metadata Viewer</a> ( <code>roles/ bigquery.metadataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datacatalog#datacatalog.admin">Data Catalog Admin</a> ( <code>roles/ datacatalog.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datacatalog#datacatalog.editor">Data Catalog Editor</a> ( <code>roles/ datacatalog.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datacatalog#datacatalog.viewer">Data Catalog Viewer</a> ( <code>roles/ datacatalog.viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.routineAdmin">BigQuery Authorized Routine Admin</a> ( <code>roles/ bigquery.routineAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.routineDataEditor">BigQuery Authorized Routine Data Editor</a> ( <code>roles/ bigquery.routineDataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.routineDataViewer">BigQuery Authorized Routine Data Viewer</a> ( <code>roles/ bigquery.routineDataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.routineMetadataViewer">BigQuery Authorized Routine Metadata Viewer</a> ( <code>roles/ bigquery.routineMetadataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code>roles/ dataplex.storageDataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.storageDataReader">Dataplex Storage Data Reader</a> ( <code>roles/ dataplex.storageDataReader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.securityAuditor">Security Auditor</a> ( <code>roles/ iam.securityAuditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.siteReliabilityEngineer">Site Reliability Engineer</a> ( <code>roles/ iam.siteReliabilityEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/deploymentmanager#clouddeploymentmanager.serviceAgent">Cloud Deployment Manager Service Agent</a> ( <code>roles/ clouddeploymentmanager.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datastream#datastream.serviceAgent">Datastream Service Agent</a> ( <code>roles/ datastream.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.routines.list</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code>roles/ bigquery.dataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataViewer">BigQuery Data Viewer</a> ( <code>roles/ bigquery.dataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.metadataViewer">BigQuery Metadata Viewer</a> ( <code>roles/ bigquery.metadataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code>roles/ bigquery.user</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code>roles/ iam.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code>roles/ iam.securityReviewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.routineAdmin">BigQuery Authorized Routine Admin</a> ( <code>roles/ bigquery.routineAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.routineDataEditor">BigQuery Authorized Routine Data Editor</a> ( <code>roles/ bigquery.routineDataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.routineDataViewer">BigQuery Authorized Routine Data Viewer</a> ( <code>roles/ bigquery.routineDataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.routineMetadataViewer">BigQuery Authorized Routine Metadata Viewer</a> ( <code>roles/ bigquery.routineMetadataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code>roles/ dataplex.storageDataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.storageDataReader">Dataplex Storage Data Reader</a> ( <code>roles/ dataplex.storageDataReader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.securityAuditor">Security Auditor</a> ( <code>roles/ iam.securityAuditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.siteReliabilityEngineer">Site Reliability Engineer</a> ( <code>roles/ iam.siteReliabilityEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datastream#datastream.serviceAgent">Datastream Service Agent</a> ( <code>roles/ datastream.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.routines.update</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code>roles/ bigquery.dataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code>roles/ dataplex.storageDataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/deploymentmanager#clouddeploymentmanager.serviceAgent">Cloud Deployment Manager Service Agent</a> ( <code>roles/ clouddeploymentmanager.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.routines.updateTag</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code>roles/ bigquery.dataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datacatalog#datacatalog.admin">Data Catalog Admin</a> ( <code>roles/ datacatalog.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datacatalog#datacatalog.tagEditor">Data Catalog Tag Editor</a> ( <code>roles/ datacatalog.tagEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery. rowAccessPolicies. create</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code>roles/ bigquery.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery. rowAccessPolicies. delete</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code>roles/ bigquery.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.rowAccessPolicies.get</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code>roles/ bigquery.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery. rowAccessPolicies. getFilteredData</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.filteredDataViewer">BigQuery Filtered Data Viewer</a> ( <code>roles/ bigquery.filteredDataViewer</code> )</p></td>
</tr>
<tr class="even">
<td><code>bigquery. rowAccessPolicies. getIamPolicy</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code>roles/ iam.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code>roles/ iam.securityReviewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code>roles/ bigquery.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.securityAuditor">Security Auditor</a> ( <code>roles/ iam.securityAuditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery. rowAccessPolicies. list</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code>roles/ iam.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code>roles/ iam.securityReviewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code>roles/ bigquery.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.securityAuditor">Security Auditor</a> ( <code>roles/ iam.securityAuditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery. rowAccessPolicies. overrideTimeTravelRestrictions</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery. rowAccessPolicies. setIamPolicy</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code>roles/ iam.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code>roles/ bigquery.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery. rowAccessPolicies. update</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code>roles/ bigquery.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.savedqueries.create</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.savedqueries.delete</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.savedqueries.get</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code>roles/ bigquery.user</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.savedqueries.list</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code>roles/ bigquery.user</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code>roles/ iam.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code>roles/ iam.securityReviewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.securityAuditor">Security Auditor</a> ( <code>roles/ iam.securityAuditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.savedqueries.update</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.tables.create</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code>roles/ bigquery.dataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.routineAdmin">BigQuery Authorized Routine Admin</a> ( <code>roles/ bigquery.routineAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.routineDataEditor">BigQuery Authorized Routine Data Editor</a> ( <code>roles/ bigquery.routineDataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code>roles/ dataplex.storageDataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datastream#datastream.bigqueryWriter">Datastream Bigquery Writer</a> ( <code>roles/ datastream.bigqueryWriter</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.batchPredictionServiceAgent">Vertex AI Batch Prediction Service Agent</a> ( <code>roles/ aiplatform.batchPredictionServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.customCodeServiceAgent">Vertex AI Custom Code Service Agent</a> ( <code>roles/ aiplatform.customCodeServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.modelMonitoringServiceAgent">Vertex AI Model Monitoring Service Agent</a> ( <code>roles/ aiplatform.modelMonitoringServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.ragServiceAgent">Vertex AI RAG Data Service Agent</a> ( <code>roles/ aiplatform.ragServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.serviceAgent">Vertex AI Service Agent</a> ( <code>roles/ aiplatform.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.tuningServiceAgent">Vertex AI Tuning Service Agent</a> ( <code>roles/ aiplatform.tuningServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/automl#automl.serviceAgent">AutoML Service Agent</a> ( <code>roles/ automl.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/automlrecommendations#automlrecommendations.serviceAgent">Recommendations AI Service Agent</a> ( <code>roles/ automlrecommendations.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.connectedSheetsServiceAgent">Connected Sheets Service Agent</a> ( <code>roles/ bigquery.connectedSheetsServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/ces#ces.serviceAgent">Customer Engagement Suite Service Agent</a> ( <code>roles/ ces.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/chronicle#chronicle.serviceAgent">Chronicle Service Agent</a> ( <code>roles/ chronicle.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/cloudasset#cloudasset.serviceAgent">Cloud Asset Service Agent</a> ( <code>roles/ cloudasset.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/deploymentmanager#clouddeploymentmanager.serviceAgent">Cloud Deployment Manager Service Agent</a> ( <code>roles/ clouddeploymentmanager.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/contactcenterinsights#contactcenterinsights.serviceAgent">Contact Center AI Insights Service Agent</a> ( <code>roles/ contactcenterinsights.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/container#container.serviceAgent">Kubernetes Engine Service Agent</a> ( <code>roles/ container.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datalabeling#datalabeling.serviceAgent">Data Labeling Service Agent</a> ( <code>roles/ datalabeling.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datastream#datastream.serviceAgent">Datastream Service Agent</a> ( <code>roles/ datastream.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datastudio#datastudio.managedStorageServiceAgent">Data Studio Managed Storage Service Agent</a> ( <code>roles/ datastudio.managedStorageServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dialogflow#dialogflow.serviceAgent">Dialogflow Service Agent</a> ( <code>roles/ dialogflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/discoveryengine#discoveryengine.serviceAgent">Discovery Engine Service Agent</a> ( <code>roles/ discoveryengine.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/enterpriseknowledgegraph#enterpriseknowledgegraph.serviceAgent">Enterprise Knowledge Graph Service Agent</a> ( <code>roles/ enterpriseknowledgegraph.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/firebasecrash#firebasecrashlytics.serviceAgent">Firebase Crashlytics Service Agent</a> ( <code>roles/ firebasecrashlytics.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/looker#looker.serviceAgent">(Legacy) Looker Service Agent</a> ( <code>roles/ looker.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/ml#ml.serviceAgent">AI Platform Service Agent</a> ( <code>roles/ ml.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/retail#retail.serviceAgent">Retail Service Agent</a> ( <code>roles/ retail.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/spectrumsas#spectrumsas.serviceAgent">Spectrum SAS Service Agent</a> ( <code>roles/ spectrumsas.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/visionai#visionai.serviceAgent">Cloud Vision AI Service Agent</a> ( <code>roles/ visionai.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.tables.createIndex</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code>roles/ bigquery.dataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.tables.createSnapshot</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code>roles/ bigquery.dataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataViewer">BigQuery Data Viewer</a> ( <code>roles/ bigquery.dataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code>roles/ dataplex.storageDataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.siteReliabilityEngineer">Site Reliability Engineer</a> ( <code>roles/ iam.siteReliabilityEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.batchPredictionServiceAgent">Vertex AI Batch Prediction Service Agent</a> ( <code>roles/ aiplatform.batchPredictionServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.ragServiceAgent">Vertex AI RAG Data Service Agent</a> ( <code>roles/ aiplatform.ragServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/looker#looker.serviceAgent">(Legacy) Looker Service Agent</a> ( <code>roles/ looker.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery. tables. createTagBinding</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/resourcemanager#resourcemanager.tagUser">Tag User</a> ( <code>roles/ resourcemanager.tagUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code>roles/ bigquery.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dspm#dspm.serviceAgent">DSPM Service Agent</a> ( <code>roles/ dspm.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.tables.delete</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code>roles/ bigquery.dataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.routineAdmin">BigQuery Authorized Routine Admin</a> ( <code>roles/ bigquery.routineAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.routineDataEditor">BigQuery Authorized Routine Data Editor</a> ( <code>roles/ bigquery.routineDataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code>roles/ dataplex.storageDataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.tuningServiceAgent">Vertex AI Tuning Service Agent</a> ( <code>roles/ aiplatform.tuningServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/chronicle#chronicle.serviceAgent">Chronicle Service Agent</a> ( <code>roles/ chronicle.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/cloudasset#cloudasset.serviceAgent">Cloud Asset Service Agent</a> ( <code>roles/ cloudasset.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/deploymentmanager#clouddeploymentmanager.serviceAgent">Cloud Deployment Manager Service Agent</a> ( <code>roles/ clouddeploymentmanager.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datastudio#datastudio.managedStorageServiceAgent">Data Studio Managed Storage Service Agent</a> ( <code>roles/ datastudio.managedStorageServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.tables.deleteIndex</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code>roles/ bigquery.dataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.tables.deleteSnapshot</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code>roles/ dataplex.storageDataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.batchPredictionServiceAgent">Vertex AI Batch Prediction Service Agent</a> ( <code>roles/ aiplatform.batchPredictionServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.ragServiceAgent">Vertex AI RAG Data Service Agent</a> ( <code>roles/ aiplatform.ragServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery. tables. deleteTagBinding</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/resourcemanager#resourcemanager.tagUser">Tag User</a> ( <code>roles/ resourcemanager.tagUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code>roles/ bigquery.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dspm#dspm.serviceAgent">DSPM Service Agent</a> ( <code>roles/ dspm.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.tables.export</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code>roles/ bigquery.dataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataViewer">BigQuery Data Viewer</a> ( <code>roles/ bigquery.dataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code>roles/ dataplex.storageDataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.storageDataReader">Dataplex Storage Data Reader</a> ( <code>roles/ dataplex.storageDataReader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.siteReliabilityEngineer">Site Reliability Engineer</a> ( <code>roles/ iam.siteReliabilityEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.batchPredictionServiceAgent">Vertex AI Batch Prediction Service Agent</a> ( <code>roles/ aiplatform.batchPredictionServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.customCodeServiceAgent">Vertex AI Custom Code Service Agent</a> ( <code>roles/ aiplatform.customCodeServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.modelMonitoringServiceAgent">Vertex AI Model Monitoring Service Agent</a> ( <code>roles/ aiplatform.modelMonitoringServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.ragServiceAgent">Vertex AI RAG Data Service Agent</a> ( <code>roles/ aiplatform.ragServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.serviceAgent">Vertex AI Service Agent</a> ( <code>roles/ aiplatform.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/automl#automl.serviceAgent">AutoML Service Agent</a> ( <code>roles/ automl.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/automlrecommendations#automlrecommendations.serviceAgent">Recommendations AI Service Agent</a> ( <code>roles/ automlrecommendations.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/discoveryengine#discoveryengine.serviceAgent">Discovery Engine Service Agent</a> ( <code>roles/ discoveryengine.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/looker#looker.serviceAgent">(Legacy) Looker Service Agent</a> ( <code>roles/ looker.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/retail#retail.serviceAgent">Retail Service Agent</a> ( <code>roles/ retail.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/visionai#visionai.serviceAgent">Cloud Vision AI Service Agent</a> ( <code>roles/ visionai.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.tables.get</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code>roles/ bigquery.dataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataViewer">BigQuery Data Viewer</a> ( <code>roles/ bigquery.dataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.metadataViewer">BigQuery Metadata Viewer</a> ( <code>roles/ bigquery.metadataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datacatalog#datacatalog.admin">Data Catalog Admin</a> ( <code>roles/ datacatalog.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datacatalog#datacatalog.editor">Data Catalog Editor</a> ( <code>roles/ datacatalog.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datacatalog#datacatalog.viewer">Data Catalog Viewer</a> ( <code>roles/ datacatalog.viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.routineAdmin">BigQuery Authorized Routine Admin</a> ( <code>roles/ bigquery.routineAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.routineDataEditor">BigQuery Authorized Routine Data Editor</a> ( <code>roles/ bigquery.routineDataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.routineDataViewer">BigQuery Authorized Routine Data Viewer</a> ( <code>roles/ bigquery.routineDataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.routineMetadataViewer">BigQuery Authorized Routine Metadata Viewer</a> ( <code>roles/ bigquery.routineMetadataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code>roles/ bigquery.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code>roles/ dataplex.storageDataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.storageDataReader">Dataplex Storage Data Reader</a> ( <code>roles/ dataplex.storageDataReader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datastream#datastream.bigqueryWriter">Datastream Bigquery Writer</a> ( <code>roles/ datastream.bigqueryWriter</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.securityAuditor">Security Auditor</a> ( <code>roles/ iam.securityAuditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.siteReliabilityEngineer">Site Reliability Engineer</a> ( <code>roles/ iam.siteReliabilityEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.batchPredictionServiceAgent">Vertex AI Batch Prediction Service Agent</a> ( <code>roles/ aiplatform.batchPredictionServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.customCodeServiceAgent">Vertex AI Custom Code Service Agent</a> ( <code>roles/ aiplatform.customCodeServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.modelMonitoringServiceAgent">Vertex AI Model Monitoring Service Agent</a> ( <code>roles/ aiplatform.modelMonitoringServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.ragServiceAgent">Vertex AI RAG Data Service Agent</a> ( <code>roles/ aiplatform.ragServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.serviceAgent">Vertex AI Service Agent</a> ( <code>roles/ aiplatform.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.tuningServiceAgent">Vertex AI Tuning Service Agent</a> ( <code>roles/ aiplatform.tuningServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/automl#automl.serviceAgent">AutoML Service Agent</a> ( <code>roles/ automl.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/automlrecommendations#automlrecommendations.serviceAgent">Recommendations AI Service Agent</a> ( <code>roles/ automlrecommendations.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/ces#ces.serviceAgent">Customer Engagement Suite Service Agent</a> ( <code>roles/ ces.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/chronicle#chronicle.serviceAgent">Chronicle Service Agent</a> ( <code>roles/ chronicle.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/cloudasset#cloudasset.serviceAgent">Cloud Asset Service Agent</a> ( <code>roles/ cloudasset.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/deploymentmanager#clouddeploymentmanager.serviceAgent">Cloud Deployment Manager Service Agent</a> ( <code>roles/ clouddeploymentmanager.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/contactcenterinsights#contactcenterinsights.serviceAgent">Contact Center AI Insights Service Agent</a> ( <code>roles/ contactcenterinsights.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/container#container.serviceAgent">Kubernetes Engine Service Agent</a> ( <code>roles/ container.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datalabeling#datalabeling.serviceAgent">Data Labeling Service Agent</a> ( <code>roles/ datalabeling.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datapipelines#datapipelines.serviceAgent">Datapipelines Service Agent</a> ( <code>roles/ datapipelines.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datastream#datastream.serviceAgent">Datastream Service Agent</a> ( <code>roles/ datastream.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dialogflow#dialogflow.serviceAgent">Dialogflow Service Agent</a> ( <code>roles/ dialogflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/discoveryengine#discoveryengine.serviceAgent">Discovery Engine Service Agent</a> ( <code>roles/ discoveryengine.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/enterpriseknowledgegraph#enterpriseknowledgegraph.serviceAgent">Enterprise Knowledge Graph Service Agent</a> ( <code>roles/ enterpriseknowledgegraph.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/firebasecrash#firebasecrashlytics.serviceAgent">Firebase Crashlytics Service Agent</a> ( <code>roles/ firebasecrashlytics.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/looker#looker.serviceAgent">(Legacy) Looker Service Agent</a> ( <code>roles/ looker.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/ml#ml.serviceAgent">AI Platform Service Agent</a> ( <code>roles/ ml.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/retail#retail.serviceAgent">Retail Service Agent</a> ( <code>roles/ retail.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/visionai#visionai.serviceAgent">Cloud Vision AI Service Agent</a> ( <code>roles/ visionai.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.tables.getData</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code>roles/ bigquery.dataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataViewer">BigQuery Data Viewer</a> ( <code>roles/ bigquery.dataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.routineAdmin">BigQuery Authorized Routine Admin</a> ( <code>roles/ bigquery.routineAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.routineDataEditor">BigQuery Authorized Routine Data Editor</a> ( <code>roles/ bigquery.routineDataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.routineDataViewer">BigQuery Authorized Routine Data Viewer</a> ( <code>roles/ bigquery.routineDataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code>roles/ dataplex.storageDataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.storageDataReader">Dataplex Storage Data Reader</a> ( <code>roles/ dataplex.storageDataReader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datastream#datastream.bigqueryWriter">Datastream Bigquery Writer</a> ( <code>roles/ datastream.bigqueryWriter</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.siteReliabilityEngineer">Site Reliability Engineer</a> ( <code>roles/ iam.siteReliabilityEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.batchPredictionServiceAgent">Vertex AI Batch Prediction Service Agent</a> ( <code>roles/ aiplatform.batchPredictionServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.customCodeServiceAgent">Vertex AI Custom Code Service Agent</a> ( <code>roles/ aiplatform.customCodeServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.modelMonitoringServiceAgent">Vertex AI Model Monitoring Service Agent</a> ( <code>roles/ aiplatform.modelMonitoringServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.ragServiceAgent">Vertex AI RAG Data Service Agent</a> ( <code>roles/ aiplatform.ragServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.serviceAgent">Vertex AI Service Agent</a> ( <code>roles/ aiplatform.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.tuningServiceAgent">Vertex AI Tuning Service Agent</a> ( <code>roles/ aiplatform.tuningServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/automl#automl.serviceAgent">AutoML Service Agent</a> ( <code>roles/ automl.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/automlrecommendations#automlrecommendations.serviceAgent">Recommendations AI Service Agent</a> ( <code>roles/ automlrecommendations.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/ces#ces.serviceAgent">Customer Engagement Suite Service Agent</a> ( <code>roles/ ces.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/deploymentmanager#clouddeploymentmanager.serviceAgent">Cloud Deployment Manager Service Agent</a> ( <code>roles/ clouddeploymentmanager.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datalabeling#datalabeling.serviceAgent">Data Labeling Service Agent</a> ( <code>roles/ datalabeling.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datastream#datastream.serviceAgent">Datastream Service Agent</a> ( <code>roles/ datastream.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datastudio#datastudio.managedStorageServiceAgent">Data Studio Managed Storage Service Agent</a> ( <code>roles/ datastudio.managedStorageServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dialogflow#dialogflow.serviceAgent">Dialogflow Service Agent</a> ( <code>roles/ dialogflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/discoveryengine#discoveryengine.serviceAgent">Discovery Engine Service Agent</a> ( <code>roles/ discoveryengine.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dspm#dspm.serviceAgent">DSPM Service Agent</a> ( <code>roles/ dspm.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/enterpriseknowledgegraph#enterpriseknowledgegraph.serviceAgent">Enterprise Knowledge Graph Service Agent</a> ( <code>roles/ enterpriseknowledgegraph.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/firebasecrash#firebasecrashlytics.serviceAgent">Firebase Crashlytics Service Agent</a> ( <code>roles/ firebasecrashlytics.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/fleetengine#fleetengine.serviceAgent">FleetEngine Service Agent</a> ( <code>roles/ fleetengine.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/looker#looker.serviceAgent">(Legacy) Looker Service Agent</a> ( <code>roles/ looker.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/ml#ml.serviceAgent">AI Platform Service Agent</a> ( <code>roles/ ml.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/retail#retail.serviceAgent">Retail Service Agent</a> ( <code>roles/ retail.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/visionai#visionai.serviceAgent">Cloud Vision AI Service Agent</a> ( <code>roles/ visionai.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.tables.getIamPolicy</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code>roles/ bigquery.dataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataViewer">BigQuery Data Viewer</a> ( <code>roles/ bigquery.dataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.metadataViewer">BigQuery Metadata Viewer</a> ( <code>roles/ bigquery.metadataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code>roles/ iam.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code>roles/ iam.securityReviewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code>roles/ bigquery.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.securityAuditor">Security Auditor</a> ( <code>roles/ iam.securityAuditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.siteReliabilityEngineer">Site Reliability Engineer</a> ( <code>roles/ iam.siteReliabilityEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.tables.list</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code>roles/ bigquery.dataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataViewer">BigQuery Data Viewer</a> ( <code>roles/ bigquery.dataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.metadataViewer">BigQuery Metadata Viewer</a> ( <code>roles/ bigquery.metadataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code>roles/ bigquery.user</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code>roles/ iam.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code>roles/ iam.securityReviewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.routineAdmin">BigQuery Authorized Routine Admin</a> ( <code>roles/ bigquery.routineAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.routineDataEditor">BigQuery Authorized Routine Data Editor</a> ( <code>roles/ bigquery.routineDataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.routineDataViewer">BigQuery Authorized Routine Data Viewer</a> ( <code>roles/ bigquery.routineDataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.routineMetadataViewer">BigQuery Authorized Routine Metadata Viewer</a> ( <code>roles/ bigquery.routineMetadataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code>roles/ bigquery.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code>roles/ dataplex.storageDataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.storageDataReader">Dataplex Storage Data Reader</a> ( <code>roles/ dataplex.storageDataReader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datastream#datastream.bigqueryWriter">Datastream Bigquery Writer</a> ( <code>roles/ datastream.bigqueryWriter</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.securityAuditor">Security Auditor</a> ( <code>roles/ iam.securityAuditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.siteReliabilityEngineer">Site Reliability Engineer</a> ( <code>roles/ iam.siteReliabilityEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.serviceAgent">Vertex AI Service Agent</a> ( <code>roles/ aiplatform.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.tuningServiceAgent">Vertex AI Tuning Service Agent</a> ( <code>roles/ aiplatform.tuningServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/automlrecommendations#automlrecommendations.serviceAgent">Recommendations AI Service Agent</a> ( <code>roles/ automlrecommendations.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datastream#datastream.serviceAgent">Datastream Service Agent</a> ( <code>roles/ datastream.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datastudio#datastudio.managedStorageServiceAgent">Data Studio Managed Storage Service Agent</a> ( <code>roles/ datastudio.managedStorageServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/discoveryengine#discoveryengine.serviceAgent">Discovery Engine Service Agent</a> ( <code>roles/ discoveryengine.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dspm#dspm.serviceAgent">DSPM Service Agent</a> ( <code>roles/ dspm.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/enterpriseknowledgegraph#enterpriseknowledgegraph.serviceAgent">Enterprise Knowledge Graph Service Agent</a> ( <code>roles/ enterpriseknowledgegraph.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/looker#looker.serviceAgent">(Legacy) Looker Service Agent</a> ( <code>roles/ looker.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/ml#ml.serviceAgent">AI Platform Service Agent</a> ( <code>roles/ ml.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/retail#retail.serviceAgent">Retail Service Agent</a> ( <code>roles/ retail.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery. tables. listEffectiveTags</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/resourcemanager#resourcemanager.tagUser">Tag User</a> ( <code>roles/ resourcemanager.tagUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/resourcemanager#resourcemanager.tagViewer">Tag Viewer</a> ( <code>roles/ resourcemanager.tagViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code>roles/ bigquery.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.securityAuditor">Security Auditor</a> ( <code>roles/ iam.securityAuditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dspm#dspm.serviceAgent">DSPM Service Agent</a> ( <code>roles/ dspm.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery. tables. listTagBindings</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/resourcemanager#resourcemanager.tagUser">Tag User</a> ( <code>roles/ resourcemanager.tagUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/resourcemanager#resourcemanager.tagViewer">Tag Viewer</a> ( <code>roles/ resourcemanager.tagViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code>roles/ bigquery.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.securityAuditor">Security Auditor</a> ( <code>roles/ iam.securityAuditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dspm#dspm.serviceAgent">DSPM Service Agent</a> ( <code>roles/ dspm.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.tables.replicateData</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code>roles/ bigquery.dataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataViewer">BigQuery Data Viewer</a> ( <code>roles/ bigquery.dataViewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.siteReliabilityEngineer">Site Reliability Engineer</a> ( <code>roles/ iam.siteReliabilityEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery. tables. restoreSnapshot</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code>roles/ bigquery.dataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code>roles/ dataplex.storageDataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.batchPredictionServiceAgent">Vertex AI Batch Prediction Service Agent</a> ( <code>roles/ aiplatform.batchPredictionServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.ragServiceAgent">Vertex AI RAG Data Service Agent</a> ( <code>roles/ aiplatform.ragServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.tables.setCategory</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/deploymentmanager#clouddeploymentmanager.serviceAgent">Cloud Deployment Manager Service Agent</a> ( <code>roles/ clouddeploymentmanager.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery. tables. setColumnDataPolicy</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code>roles/ bigquery.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.tables.setIamPolicy</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code>roles/ iam.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code>roles/ bigquery.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.tables.update</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code>roles/ bigquery.dataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.routineAdmin">BigQuery Authorized Routine Admin</a> ( <code>roles/ bigquery.routineAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.routineDataEditor">BigQuery Authorized Routine Data Editor</a> ( <code>roles/ bigquery.routineDataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code>roles/ bigquery.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code>roles/ dataplex.storageDataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datastream#datastream.bigqueryWriter">Datastream Bigquery Writer</a> ( <code>roles/ datastream.bigqueryWriter</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.batchPredictionServiceAgent">Vertex AI Batch Prediction Service Agent</a> ( <code>roles/ aiplatform.batchPredictionServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.customCodeServiceAgent">Vertex AI Custom Code Service Agent</a> ( <code>roles/ aiplatform.customCodeServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.modelMonitoringServiceAgent">Vertex AI Model Monitoring Service Agent</a> ( <code>roles/ aiplatform.modelMonitoringServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.ragServiceAgent">Vertex AI RAG Data Service Agent</a> ( <code>roles/ aiplatform.ragServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.serviceAgent">Vertex AI Service Agent</a> ( <code>roles/ aiplatform.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.tuningServiceAgent">Vertex AI Tuning Service Agent</a> ( <code>roles/ aiplatform.tuningServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/automl#automl.serviceAgent">AutoML Service Agent</a> ( <code>roles/ automl.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/automlrecommendations#automlrecommendations.serviceAgent">Recommendations AI Service Agent</a> ( <code>roles/ automlrecommendations.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.connectedSheetsServiceAgent">Connected Sheets Service Agent</a> ( <code>roles/ bigquery.connectedSheetsServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/ces#ces.serviceAgent">Customer Engagement Suite Service Agent</a> ( <code>roles/ ces.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/chronicle#chronicle.serviceAgent">Chronicle Service Agent</a> ( <code>roles/ chronicle.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/cloudasset#cloudasset.serviceAgent">Cloud Asset Service Agent</a> ( <code>roles/ cloudasset.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/deploymentmanager#clouddeploymentmanager.serviceAgent">Cloud Deployment Manager Service Agent</a> ( <code>roles/ clouddeploymentmanager.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/contactcenterinsights#contactcenterinsights.serviceAgent">Contact Center AI Insights Service Agent</a> ( <code>roles/ contactcenterinsights.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/container#container.serviceAgent">Kubernetes Engine Service Agent</a> ( <code>roles/ container.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datastream#datastream.serviceAgent">Datastream Service Agent</a> ( <code>roles/ datastream.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datastudio#datastudio.managedStorageServiceAgent">Data Studio Managed Storage Service Agent</a> ( <code>roles/ datastudio.managedStorageServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/discoveryengine#discoveryengine.serviceAgent">Discovery Engine Service Agent</a> ( <code>roles/ discoveryengine.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/enterpriseknowledgegraph#enterpriseknowledgegraph.serviceAgent">Enterprise Knowledge Graph Service Agent</a> ( <code>roles/ enterpriseknowledgegraph.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/firebasecrash#firebasecrashlytics.serviceAgent">Firebase Crashlytics Service Agent</a> ( <code>roles/ firebasecrashlytics.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/retail#retail.serviceAgent">Retail Service Agent</a> ( <code>roles/ retail.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/visionai#visionai.serviceAgent">Cloud Vision AI Service Agent</a> ( <code>roles/ visionai.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.tables.updateData</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code>roles/ bigquery.dataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.routineAdmin">BigQuery Authorized Routine Admin</a> ( <code>roles/ bigquery.routineAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.routineDataEditor">BigQuery Authorized Routine Data Editor</a> ( <code>roles/ bigquery.routineDataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code>roles/ dataplex.storageDataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.storageDataWriter">Dataplex Storage Data Writer</a> ( <code>roles/ dataplex.storageDataWriter</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datastream#datastream.bigqueryWriter">Datastream Bigquery Writer</a> ( <code>roles/ datastream.bigqueryWriter</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.batchPredictionServiceAgent">Vertex AI Batch Prediction Service Agent</a> ( <code>roles/ aiplatform.batchPredictionServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.customCodeServiceAgent">Vertex AI Custom Code Service Agent</a> ( <code>roles/ aiplatform.customCodeServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.modelMonitoringServiceAgent">Vertex AI Model Monitoring Service Agent</a> ( <code>roles/ aiplatform.modelMonitoringServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.ragServiceAgent">Vertex AI RAG Data Service Agent</a> ( <code>roles/ aiplatform.ragServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.serviceAgent">Vertex AI Service Agent</a> ( <code>roles/ aiplatform.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.tuningServiceAgent">Vertex AI Tuning Service Agent</a> ( <code>roles/ aiplatform.tuningServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/automl#automl.serviceAgent">AutoML Service Agent</a> ( <code>roles/ automl.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/automlrecommendations#automlrecommendations.serviceAgent">Recommendations AI Service Agent</a> ( <code>roles/ automlrecommendations.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.connectedSheetsServiceAgent">Connected Sheets Service Agent</a> ( <code>roles/ bigquery.connectedSheetsServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigqueryomni#bigqueryomni.serviceAgent">BigQuery Omni Service Agent</a> ( <code>roles/ bigqueryomni.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/ces#ces.serviceAgent">Customer Engagement Suite Service Agent</a> ( <code>roles/ ces.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/chronicle#chronicle.serviceAgent">Chronicle Service Agent</a> ( <code>roles/ chronicle.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/cloudasset#cloudasset.serviceAgent">Cloud Asset Service Agent</a> ( <code>roles/ cloudasset.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/deploymentmanager#clouddeploymentmanager.serviceAgent">Cloud Deployment Manager Service Agent</a> ( <code>roles/ clouddeploymentmanager.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/contactcenterinsights#contactcenterinsights.serviceAgent">Contact Center AI Insights Service Agent</a> ( <code>roles/ contactcenterinsights.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/container#container.serviceAgent">Kubernetes Engine Service Agent</a> ( <code>roles/ container.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datastream#datastream.serviceAgent">Datastream Service Agent</a> ( <code>roles/ datastream.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datastudio#datastudio.managedStorageServiceAgent">Data Studio Managed Storage Service Agent</a> ( <code>roles/ datastudio.managedStorageServiceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dialogflow#dialogflow.serviceAgent">Dialogflow Service Agent</a> ( <code>roles/ dialogflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/discoveryengine#discoveryengine.serviceAgent">Discovery Engine Service Agent</a> ( <code>roles/ discoveryengine.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/enterpriseknowledgegraph#enterpriseknowledgegraph.serviceAgent">Enterprise Knowledge Graph Service Agent</a> ( <code>roles/ enterpriseknowledgegraph.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/firebasecrash#firebasecrashlytics.serviceAgent">Firebase Crashlytics Service Agent</a> ( <code>roles/ firebasecrashlytics.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/ml#ml.serviceAgent">AI Platform Service Agent</a> ( <code>roles/ ml.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/retail#retail.serviceAgent">Retail Service Agent</a> ( <code>roles/ retail.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/spectrumsas#spectrumsas.serviceAgent">Spectrum SAS Service Agent</a> ( <code>roles/ spectrumsas.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/visionai#visionai.serviceAgent">Cloud Vision AI Service Agent</a> ( <code>roles/ visionai.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.tables.updateIndex</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code>roles/ bigquery.dataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.tables.updateTag</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code>roles/ bigquery.dataEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code>roles/ bigquery.dataOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datacatalog#datacatalog.admin">Data Catalog Admin</a> ( <code>roles/ datacatalog.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code>roles/ bigquery.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datacatalog#datacatalog.tagEditor">Data Catalog Tag Editor</a> ( <code>roles/ datacatalog.tagEditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.dataScientist">Data Scientist</a> ( <code>roles/ iam.dataScientist</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.mlEngineer">ML Engineer</a> ( <code>roles/ iam.mlEngineer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code>roles/ datafusion.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code>roles/ dlp.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquery.transfers.get</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code>roles/ bigquery.user</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/firebase#firebase.managementServiceAgent">Firebase Service Management Service Agent</a> ( <code>roles/ firebase.managementServiceAgent</code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>bigquery.transfers.update</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.editor">BigQuery Data Policy Editor</a> ( <code>roles/ bigquerydatapolicy.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/firebase#firebase.managementServiceAgent">Firebase Service Management Service Agent</a> ( <code>roles/ firebase.managementServiceAgent</code> )</li>
</ul></td>
</tr>
</tbody>
</table>

### BigQuery Connection API permissions

There are no IAM permissions for this service.

### BigQuery Continuous Query permissions

There are no IAM permissions for this service.

### BigQuery Data Policy permissions

There are no IAM permissions for this service.

### BigQuery Data Transfer Service permissions

There are no IAM permissions for this service.

### BigQuery Engine for Apache Flink permissions

This table lists the IAM permissions for BigQuery Engine for Apache Flink and the roles that include them. To search through all roles and permissions, see the [role and permission index](https://docs.cloud.google.com/iam/docs/roles-permissions) .

| Permission                          | Included in roles                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|-------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `managedflink. deployments. create` | [Owner](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ owner` ) [Editor](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ editor` ) [Managed Flink Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.admin) ( `roles/ managedflink.admin` ) [Admin](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ admin` ) [Writer](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ writer` )                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `managedflink. deployments. delete` | [Owner](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ owner` ) [Editor](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ editor` ) [Managed Flink Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.admin) ( `roles/ managedflink.admin` ) [Admin](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ admin` ) [Writer](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ writer` )                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `managedflink.deployments.get`      | [Owner](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ owner` ) [Editor](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ editor` ) [Viewer](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ viewer` ) [Managed Flink Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.admin) ( `roles/ managedflink.admin` ) [Managed Flink Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.viewer) ( `roles/ managedflink.viewer` ) [Admin](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ admin` ) [Support User](https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser) ( `roles/ iam.supportUser` ) [Managed Flink Developer](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.developer) ( `roles/ managedflink.developer` ) [Reader](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ reader` ) [Writer](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ writer` )                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `managedflink.deployments.list`     | [Owner](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ owner` ) [Editor](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ editor` ) [Viewer](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ viewer` ) [Security Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityAdmin) ( `roles/ iam.securityAdmin` ) [Security Reviewer](https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityReviewer) ( `roles/ iam.securityReviewer` ) [Managed Flink Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.admin) ( `roles/ managedflink.admin` ) [Managed Flink Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.viewer) ( `roles/ managedflink.viewer` ) [Admin](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ admin` ) [Security Auditor](https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.securityAuditor) ( `roles/ iam.securityAuditor` ) [Support User](https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser) ( `roles/ iam.supportUser` ) [Managed Flink Developer](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.developer) ( `roles/ managedflink.developer` ) [Reader](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ reader` ) [Writer](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ writer` ) |
| `managedflink. deployments. update` | [Owner](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ owner` ) [Editor](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ editor` ) [Managed Flink Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.admin) ( `roles/ managedflink.admin` ) [Admin](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ admin` ) [Writer](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ writer` )                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `managedflink.jobs.create`          | [Owner](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ owner` ) [Editor](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ editor` ) [Managed Flink Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.admin) ( `roles/ managedflink.admin` ) [Admin](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ admin` ) [Managed Flink Developer](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.developer) ( `roles/ managedflink.developer` ) [Writer](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ writer` )                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `managedflink.jobs.delete`          | [Owner](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ owner` ) [Editor](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ editor` ) [Managed Flink Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.admin) ( `roles/ managedflink.admin` ) [Admin](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ admin` ) [Managed Flink Developer](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.developer) ( `roles/ managedflink.developer` ) [Writer](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ writer` )                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `managedflink.jobs.get`             | [Owner](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ owner` ) [Editor](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ editor` ) [Viewer](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ viewer` ) [Managed Flink Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.admin) ( `roles/ managedflink.admin` ) [Managed Flink Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.viewer) ( `roles/ managedflink.viewer` ) [Admin](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ admin` ) [Support User](https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser) ( `roles/ iam.supportUser` ) [Managed Flink Developer](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.developer) ( `roles/ managedflink.developer` ) [Reader](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ reader` ) [Writer](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ writer` )                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `managedflink.jobs.list`            | [Owner](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ owner` ) [Editor](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ editor` ) [Viewer](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ viewer` ) [Security Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityAdmin) ( `roles/ iam.securityAdmin` ) [Security Reviewer](https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityReviewer) ( `roles/ iam.securityReviewer` ) [Managed Flink Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.admin) ( `roles/ managedflink.admin` ) [Managed Flink Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.viewer) ( `roles/ managedflink.viewer` ) [Admin](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ admin` ) [Security Auditor](https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.securityAuditor) ( `roles/ iam.securityAuditor` ) [Support User](https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser) ( `roles/ iam.supportUser` ) [Managed Flink Developer](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.developer) ( `roles/ managedflink.developer` ) [Reader](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ reader` ) [Writer](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ writer` ) |
| `managedflink.jobs.update`          | [Owner](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ owner` ) [Editor](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ editor` ) [Managed Flink Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.admin) ( `roles/ managedflink.admin` ) [Admin](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ admin` ) [Managed Flink Developer](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.developer) ( `roles/ managedflink.developer` ) [Writer](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ writer` )                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `managedflink.locations.get`        | [Owner](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ owner` ) [Editor](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ editor` ) [Viewer](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ viewer` ) [Managed Flink Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.admin) ( `roles/ managedflink.admin` ) [Managed Flink Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.viewer) ( `roles/ managedflink.viewer` ) [Admin](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ admin` ) [Support User](https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser) ( `roles/ iam.supportUser` ) [Managed Flink Developer](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.developer) ( `roles/ managedflink.developer` ) [Reader](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ reader` ) [Writer](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ writer` )                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `managedflink.locations.list`       | [Owner](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ owner` ) [Editor](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ editor` ) [Viewer](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ viewer` ) [Security Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityAdmin) ( `roles/ iam.securityAdmin` ) [Security Reviewer](https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityReviewer) ( `roles/ iam.securityReviewer` ) [Managed Flink Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.admin) ( `roles/ managedflink.admin` ) [Managed Flink Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.viewer) ( `roles/ managedflink.viewer` ) [Admin](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ admin` ) [Security Auditor](https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.securityAuditor) ( `roles/ iam.securityAuditor` ) [Support User](https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser) ( `roles/ iam.supportUser` ) [Managed Flink Developer](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.developer) ( `roles/ managedflink.developer` ) [Reader](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ reader` ) [Writer](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ writer` ) |
| `managedflink.operations.cancel`    | [Owner](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ owner` ) [Editor](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ editor` ) [Managed Flink Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.admin) ( `roles/ managedflink.admin` ) [Admin](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ admin` ) [Writer](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ writer` )                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `managedflink.operations.delete`    | [Owner](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ owner` ) [Editor](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ editor` ) [Managed Flink Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.admin) ( `roles/ managedflink.admin` ) [Admin](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ admin` ) [Writer](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ writer` )                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `managedflink.operations.get`       | [Owner](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ owner` ) [Editor](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ editor` ) [Viewer](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ viewer` ) [Managed Flink Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.admin) ( `roles/ managedflink.admin` ) [Managed Flink Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.viewer) ( `roles/ managedflink.viewer` ) [Admin](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ admin` ) [Support User](https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser) ( `roles/ iam.supportUser` ) [Managed Flink Developer](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.developer) ( `roles/ managedflink.developer` ) [Reader](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ reader` ) [Writer](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ writer` )                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `managedflink.operations.list`      | [Owner](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ owner` ) [Editor](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ editor` ) [Viewer](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ viewer` ) [Security Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityAdmin) ( `roles/ iam.securityAdmin` ) [Security Reviewer](https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityReviewer) ( `roles/ iam.securityReviewer` ) [Managed Flink Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.admin) ( `roles/ managedflink.admin` ) [Managed Flink Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.viewer) ( `roles/ managedflink.viewer` ) [Admin](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ admin` ) [Security Auditor](https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.securityAuditor) ( `roles/ iam.securityAuditor` ) [Support User](https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser) ( `roles/ iam.supportUser` ) [Managed Flink Developer](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.developer) ( `roles/ managedflink.developer` ) [Reader](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ reader` ) [Writer](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ writer` ) |
| `managedflink.sessions.create`      | [Owner](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ owner` ) [Editor](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ editor` ) [Managed Flink Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.admin) ( `roles/ managedflink.admin` ) [Admin](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ admin` ) [Managed Flink Developer](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.developer) ( `roles/ managedflink.developer` ) [Writer](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ writer` )                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `managedflink.sessions.delete`      | [Owner](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ owner` ) [Editor](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ editor` ) [Managed Flink Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.admin) ( `roles/ managedflink.admin` ) [Admin](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ admin` ) [Managed Flink Developer](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.developer) ( `roles/ managedflink.developer` ) [Writer](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ writer` )                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `managedflink.sessions.get`         | [Owner](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ owner` ) [Editor](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ editor` ) [Viewer](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ viewer` ) [Managed Flink Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.admin) ( `roles/ managedflink.admin` ) [Managed Flink Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.viewer) ( `roles/ managedflink.viewer` ) [Admin](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ admin` ) [Support User](https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser) ( `roles/ iam.supportUser` ) [Managed Flink Developer](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.developer) ( `roles/ managedflink.developer` ) [Reader](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ reader` ) [Writer](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ writer` )                                                                                                                                                                                                                                                                                                                                                                                                                         |
| `managedflink.sessions.list`        | [Owner](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ owner` ) [Editor](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ editor` ) [Viewer](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ viewer` ) [Security Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityAdmin) ( `roles/ iam.securityAdmin` ) [Security Reviewer](https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityReviewer) ( `roles/ iam.securityReviewer` ) [Managed Flink Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.admin) ( `roles/ managedflink.admin` ) [Managed Flink Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.viewer) ( `roles/ managedflink.viewer` ) [Admin](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ admin` ) [Security Auditor](https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.securityAuditor) ( `roles/ iam.securityAuditor` ) [Support User](https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser) ( `roles/ iam.supportUser` ) [Managed Flink Developer](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.developer) ( `roles/ managedflink.developer` ) [Reader](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ reader` ) [Writer](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ writer` ) |
| `managedflink.sessions.update`      | [Owner](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ owner` ) [Editor](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ editor` ) [Managed Flink Admin](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.admin) ( `roles/ managedflink.admin` ) [Admin](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ admin` ) [Managed Flink Developer](https://docs.cloud.google.com/iam/docs/roles-permissions/managedflink#managedflink.developer) ( `roles/ managedflink.developer` ) [Writer](https://docs.cloud.google.com/iam/docs/roles-overview#basic) ( `roles/ writer` )                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |

### BigQuery Migration Service permissions

This table lists the IAM permissions for BigQuery Migration Service and the roles that include them. To search through all roles and permissions, see the [role and permission index](https://docs.cloud.google.com/iam/docs/roles-permissions) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Permission</th>
<th>Included in roles</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>bigquerymigration.subtasks.get</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.admin">Bigquerymigration Admin</a> ( <code>roles/ bigquerymigration.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.editor">MigrationWorkflow Editor</a> ( <code>roles/ bigquerymigration.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.viewer">MigrationWorkflow Viewer</a> ( <code>roles/ bigquerymigration.viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p></td>
</tr>
<tr class="even">
<td><code>bigquerymigration. subtasks. list</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.admin">Bigquerymigration Admin</a> ( <code>roles/ bigquerymigration.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.editor">MigrationWorkflow Editor</a> ( <code>roles/ bigquerymigration.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.viewer">MigrationWorkflow Viewer</a> ( <code>roles/ bigquerymigration.viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code>roles/ iam.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code>roles/ iam.securityReviewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.securityAuditor">Security Auditor</a> ( <code>roles/ iam.securityAuditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p></td>
</tr>
<tr class="odd">
<td><code>bigquerymigration. translation. translate</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code>roles/ bigquery.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code>roles/ bigquery.studioAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code>roles/ bigquery.user</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.admin">Bigquerymigration Admin</a> ( <code>roles/ bigquerymigration.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.translationUser">Migration Translation User</a> ( <code>roles/ bigquerymigration.translationUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code>roles/ dlp.orgdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code>roles/ dlp.projectdriver</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.databasesAdmin">Databases Admin</a> ( <code>roles/ iam.databasesAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code>roles/ dataflow.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code>roles/ dataplex.serviceAgent</code> )</li>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code>roles/ dataprep.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>bigquerymigration. workflows. create</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.admin">Bigquerymigration Admin</a> ( <code>roles/ bigquerymigration.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.editor">MigrationWorkflow Editor</a> ( <code>roles/ bigquerymigration.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p></td>
</tr>
<tr class="odd">
<td><code>bigquerymigration. workflows. delete</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.admin">Bigquerymigration Admin</a> ( <code>roles/ bigquerymigration.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.editor">MigrationWorkflow Editor</a> ( <code>roles/ bigquerymigration.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p></td>
</tr>
<tr class="even">
<td><code>bigquerymigration. workflows. enableAiOutputTypes</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.admin">Bigquerymigration Admin</a> ( <code>roles/ bigquerymigration.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.editor">MigrationWorkflow Editor</a> ( <code>roles/ bigquerymigration.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p></td>
</tr>
<tr class="odd">
<td><code>bigquerymigration. workflows. enableLineageOutputTypes</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.admin">Bigquerymigration Admin</a> ( <code>roles/ bigquerymigration.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.editor">MigrationWorkflow Editor</a> ( <code>roles/ bigquerymigration.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p></td>
</tr>
<tr class="even">
<td><code>bigquerymigration. workflows. enableOutputTypePermissions</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.admin">Bigquerymigration Admin</a> ( <code>roles/ bigquerymigration.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.editor">MigrationWorkflow Editor</a> ( <code>roles/ bigquerymigration.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p></td>
</tr>
<tr class="odd">
<td><code>bigquerymigration. workflows. get</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.admin">Bigquerymigration Admin</a> ( <code>roles/ bigquerymigration.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.editor">MigrationWorkflow Editor</a> ( <code>roles/ bigquerymigration.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.viewer">MigrationWorkflow Viewer</a> ( <code>roles/ bigquerymigration.viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p></td>
</tr>
<tr class="even">
<td><code>bigquerymigration. workflows. list</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.admin">Bigquerymigration Admin</a> ( <code>roles/ bigquerymigration.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.editor">MigrationWorkflow Editor</a> ( <code>roles/ bigquerymigration.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.viewer">MigrationWorkflow Viewer</a> ( <code>roles/ bigquerymigration.viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code>roles/ iam.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code>roles/ iam.securityReviewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.securityAuditor">Security Auditor</a> ( <code>roles/ iam.securityAuditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p></td>
</tr>
<tr class="odd">
<td><code>bigquerymigration. workflows. orchestrateTask</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.admin">Bigquerymigration Admin</a> ( <code>roles/ bigquerymigration.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.orchestrator">Task Orchestrator</a> ( <code>roles/ bigquerymigration.orchestrator</code> )</p></td>
</tr>
<tr class="even">
<td><code>bigquerymigration. workflows. update</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.admin">Bigquerymigration Admin</a> ( <code>roles/ bigquerymigration.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.editor">MigrationWorkflow Editor</a> ( <code>roles/ bigquerymigration.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p></td>
</tr>
</tbody>
</table>

### BigQuery Omni permissions

There are no IAM permissions for this service.

### BigQuery sharing permissions

This table lists the IAM permissions for BigQuery sharing and the roles that include them. To search through all roles and permissions, see the [role and permission index](https://docs.cloud.google.com/iam/docs/roles-permissions) .

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Permission</th>
<th>Included in roles</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>analyticshub. dataExchanges. create</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code>roles/ analyticshub.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.editor">Analytics Hub Editor</a> ( <code>roles/ analyticshub.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p></td>
</tr>
<tr class="even">
<td><code>analyticshub. dataExchanges. delete</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code>roles/ analyticshub.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.editor">Analytics Hub Editor</a> ( <code>roles/ analyticshub.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p></td>
</tr>
<tr class="odd">
<td><code>analyticshub.dataExchanges.get</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code>roles/ analyticshub.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.editor">Analytics Hub Editor</a> ( <code>roles/ analyticshub.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.viewer">Analytics Hub Viewer</a> ( <code>roles/ analyticshub.viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.listingAdmin">Analytics Hub Listing Admin</a> ( <code>roles/ analyticshub.listingAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.publisher">Analytics Hub Publisher</a> ( <code>roles/ analyticshub.publisher</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.subscriber">Analytics Hub Subscriber</a> ( <code>roles/ analyticshub.subscriber</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.subscriptionOwner">Analytics Hub Subscription Owner</a> ( <code>roles/ analyticshub.subscriptionOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p></td>
</tr>
<tr class="even">
<td><code>analyticshub. dataExchanges. getIamPolicy</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code>roles/ analyticshub.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.editor">Analytics Hub Editor</a> ( <code>roles/ analyticshub.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.viewer">Analytics Hub Viewer</a> ( <code>roles/ analyticshub.viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code>roles/ iam.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code>roles/ iam.securityReviewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.listingAdmin">Analytics Hub Listing Admin</a> ( <code>roles/ analyticshub.listingAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.publisher">Analytics Hub Publisher</a> ( <code>roles/ analyticshub.publisher</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.subscriber">Analytics Hub Subscriber</a> ( <code>roles/ analyticshub.subscriber</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.subscriptionOwner">Analytics Hub Subscription Owner</a> ( <code>roles/ analyticshub.subscriptionOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.securityAuditor">Security Auditor</a> ( <code>roles/ iam.securityAuditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p></td>
</tr>
<tr class="odd">
<td><code>analyticshub. dataExchanges. list</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code>roles/ analyticshub.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.editor">Analytics Hub Editor</a> ( <code>roles/ analyticshub.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.viewer">Analytics Hub Viewer</a> ( <code>roles/ analyticshub.viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code>roles/ iam.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code>roles/ iam.securityReviewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.listingAdmin">Analytics Hub Listing Admin</a> ( <code>roles/ analyticshub.listingAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.publisher">Analytics Hub Publisher</a> ( <code>roles/ analyticshub.publisher</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.subscriber">Analytics Hub Subscriber</a> ( <code>roles/ analyticshub.subscriber</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.subscriptionOwner">Analytics Hub Subscription Owner</a> ( <code>roles/ analyticshub.subscriptionOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.securityAuditor">Security Auditor</a> ( <code>roles/ iam.securityAuditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p>
<p>Service agent roles</p>
<blockquote>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="https://docs.cloud.google.com/iam/docs/service-agents">service agents</a> .
</blockquote>
<ul>
<li><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.serviceAgent">Analytics Hub Service Agent</a> ( <code>roles/ analyticshub.serviceAgent</code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><code>analyticshub. dataExchanges. setIamPolicy</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code>roles/ analyticshub.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code>roles/ iam.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p></td>
</tr>
<tr class="odd">
<td><code>analyticshub. dataExchanges. subscribe</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.subscriber">Analytics Hub Subscriber</a> ( <code>roles/ analyticshub.subscriber</code> )</p></td>
</tr>
<tr class="even">
<td><code>analyticshub. dataExchanges. update</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code>roles/ analyticshub.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.editor">Analytics Hub Editor</a> ( <code>roles/ analyticshub.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p></td>
</tr>
<tr class="odd">
<td><code>analyticshub. dataExchanges. viewSubscriptions</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code>roles/ analyticshub.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p></td>
</tr>
<tr class="even">
<td><code>analyticshub.listings.create</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code>roles/ analyticshub.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.editor">Analytics Hub Editor</a> ( <code>roles/ analyticshub.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.publisher">Analytics Hub Publisher</a> ( <code>roles/ analyticshub.publisher</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p></td>
</tr>
<tr class="odd">
<td><code>analyticshub.listings.delete</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code>roles/ analyticshub.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.editor">Analytics Hub Editor</a> ( <code>roles/ analyticshub.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.listingAdmin">Analytics Hub Listing Admin</a> ( <code>roles/ analyticshub.listingAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p></td>
</tr>
<tr class="even">
<td><code>analyticshub.listings.get</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code>roles/ analyticshub.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.editor">Analytics Hub Editor</a> ( <code>roles/ analyticshub.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.viewer">Analytics Hub Viewer</a> ( <code>roles/ analyticshub.viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.listingAdmin">Analytics Hub Listing Admin</a> ( <code>roles/ analyticshub.listingAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.publisher">Analytics Hub Publisher</a> ( <code>roles/ analyticshub.publisher</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.subscriber">Analytics Hub Subscriber</a> ( <code>roles/ analyticshub.subscriber</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.subscriptionOwner">Analytics Hub Subscription Owner</a> ( <code>roles/ analyticshub.subscriptionOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p></td>
</tr>
<tr class="odd">
<td><code>analyticshub. listings. getIamPolicy</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code>roles/ analyticshub.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.editor">Analytics Hub Editor</a> ( <code>roles/ analyticshub.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.viewer">Analytics Hub Viewer</a> ( <code>roles/ analyticshub.viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code>roles/ iam.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code>roles/ iam.securityReviewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.listingAdmin">Analytics Hub Listing Admin</a> ( <code>roles/ analyticshub.listingAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.publisher">Analytics Hub Publisher</a> ( <code>roles/ analyticshub.publisher</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.subscriber">Analytics Hub Subscriber</a> ( <code>roles/ analyticshub.subscriber</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.subscriptionOwner">Analytics Hub Subscription Owner</a> ( <code>roles/ analyticshub.subscriptionOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.securityAuditor">Security Auditor</a> ( <code>roles/ iam.securityAuditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p></td>
</tr>
<tr class="even">
<td><code>analyticshub.listings.list</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code>roles/ analyticshub.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.editor">Analytics Hub Editor</a> ( <code>roles/ analyticshub.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.viewer">Analytics Hub Viewer</a> ( <code>roles/ analyticshub.viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code>roles/ iam.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code>roles/ iam.securityReviewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.listingAdmin">Analytics Hub Listing Admin</a> ( <code>roles/ analyticshub.listingAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.publisher">Analytics Hub Publisher</a> ( <code>roles/ analyticshub.publisher</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.subscriber">Analytics Hub Subscriber</a> ( <code>roles/ analyticshub.subscriber</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.subscriptionOwner">Analytics Hub Subscription Owner</a> ( <code>roles/ analyticshub.subscriptionOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.securityAuditor">Security Auditor</a> ( <code>roles/ iam.securityAuditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p></td>
</tr>
<tr class="odd">
<td><code>analyticshub. listings. setIamPolicy</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code>roles/ analyticshub.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code>roles/ iam.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.listingAdmin">Analytics Hub Listing Admin</a> ( <code>roles/ analyticshub.listingAdmin</code> )</p></td>
</tr>
<tr class="even">
<td><code>analyticshub. listings. subscribe</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.subscriber">Analytics Hub Subscriber</a> ( <code>roles/ analyticshub.subscriber</code> )</p></td>
</tr>
<tr class="odd">
<td><code>analyticshub.listings.update</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code>roles/ analyticshub.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.editor">Analytics Hub Editor</a> ( <code>roles/ analyticshub.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.listingAdmin">Analytics Hub Listing Admin</a> ( <code>roles/ analyticshub.listingAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p></td>
</tr>
<tr class="even">
<td><code>analyticshub. listings. viewSubscriptions</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code>roles/ analyticshub.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.listingAdmin">Analytics Hub Listing Admin</a> ( <code>roles/ analyticshub.listingAdmin</code> )</p></td>
</tr>
<tr class="odd">
<td><code>analyticshub. queryTemplates. approve</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code>roles/ analyticshub.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.editor">Analytics Hub Editor</a> ( <code>roles/ analyticshub.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.publisher">Analytics Hub Publisher</a> ( <code>roles/ analyticshub.publisher</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p></td>
</tr>
<tr class="even">
<td><code>analyticshub. queryTemplates. create</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code>roles/ analyticshub.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.editor">Analytics Hub Editor</a> ( <code>roles/ analyticshub.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.publisher">Analytics Hub Publisher</a> ( <code>roles/ analyticshub.publisher</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p></td>
</tr>
<tr class="odd">
<td><code>analyticshub. queryTemplates. delete</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code>roles/ analyticshub.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.editor">Analytics Hub Editor</a> ( <code>roles/ analyticshub.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.publisher">Analytics Hub Publisher</a> ( <code>roles/ analyticshub.publisher</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p></td>
</tr>
<tr class="even">
<td><code>analyticshub. queryTemplates. get</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code>roles/ analyticshub.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.editor">Analytics Hub Editor</a> ( <code>roles/ analyticshub.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.viewer">Analytics Hub Viewer</a> ( <code>roles/ analyticshub.viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.listingAdmin">Analytics Hub Listing Admin</a> ( <code>roles/ analyticshub.listingAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.publisher">Analytics Hub Publisher</a> ( <code>roles/ analyticshub.publisher</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.subscriber">Analytics Hub Subscriber</a> ( <code>roles/ analyticshub.subscriber</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.subscriptionOwner">Analytics Hub Subscription Owner</a> ( <code>roles/ analyticshub.subscriptionOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p></td>
</tr>
<tr class="odd">
<td><code>analyticshub. queryTemplates. list</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code>roles/ analyticshub.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.editor">Analytics Hub Editor</a> ( <code>roles/ analyticshub.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.viewer">Analytics Hub Viewer</a> ( <code>roles/ analyticshub.viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code>roles/ iam.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code>roles/ iam.securityReviewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.listingAdmin">Analytics Hub Listing Admin</a> ( <code>roles/ analyticshub.listingAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.publisher">Analytics Hub Publisher</a> ( <code>roles/ analyticshub.publisher</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.subscriber">Analytics Hub Subscriber</a> ( <code>roles/ analyticshub.subscriber</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.subscriptionOwner">Analytics Hub Subscription Owner</a> ( <code>roles/ analyticshub.subscriptionOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.securityAuditor">Security Auditor</a> ( <code>roles/ iam.securityAuditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p></td>
</tr>
<tr class="even">
<td><code>analyticshub. queryTemplates. update</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code>roles/ analyticshub.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.editor">Analytics Hub Editor</a> ( <code>roles/ analyticshub.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.publisher">Analytics Hub Publisher</a> ( <code>roles/ analyticshub.publisher</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p></td>
</tr>
<tr class="odd">
<td><code>analyticshub. subscriptions. create</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code>roles/ analyticshub.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.editor">Analytics Hub Editor</a> ( <code>roles/ analyticshub.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.subscriptionOwner">Analytics Hub Subscription Owner</a> ( <code>roles/ analyticshub.subscriptionOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p></td>
</tr>
<tr class="even">
<td><code>analyticshub. subscriptions. delete</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code>roles/ analyticshub.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.editor">Analytics Hub Editor</a> ( <code>roles/ analyticshub.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.subscriptionOwner">Analytics Hub Subscription Owner</a> ( <code>roles/ analyticshub.subscriptionOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p></td>
</tr>
<tr class="odd">
<td><code>analyticshub.subscriptions.get</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code>roles/ analyticshub.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.editor">Analytics Hub Editor</a> ( <code>roles/ analyticshub.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.subscriptionOwner">Analytics Hub Subscription Owner</a> ( <code>roles/ analyticshub.subscriptionOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p></td>
</tr>
<tr class="even">
<td><code>analyticshub. subscriptions. list</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Viewer</a> ( <code>roles/ viewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code>roles/ analyticshub.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.editor">Analytics Hub Editor</a> ( <code>roles/ analyticshub.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code>roles/ iam.securityAdmin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code>roles/ iam.securityReviewer</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.subscriptionOwner">Analytics Hub Subscription Owner</a> ( <code>roles/ analyticshub.subscriptionOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.securityAuditor">Security Auditor</a> ( <code>roles/ iam.securityAuditor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/jobfunctions#iam.supportUser">Support User</a> ( <code>roles/ iam.supportUser</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Reader</a> ( <code>roles/ reader</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p></td>
</tr>
<tr class="odd">
<td><code>analyticshub. subscriptions. update</code></td>
<td><p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Owner</a> ( <code>roles/ owner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Editor</a> ( <code>roles/ editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code>roles/ analyticshub.admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.editor">Analytics Hub Editor</a> ( <code>roles/ analyticshub.editor</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Admin</a> ( <code>roles/ admin</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-permissions/analyticshub#analyticshub.subscriptionOwner">Analytics Hub Subscription Owner</a> ( <code>roles/ analyticshub.subscriptionOwner</code> )</p>
<p><a href="https://docs.cloud.google.com/iam/docs/roles-overview#basic">Writer</a> ( <code>roles/ writer</code> )</p></td>
</tr>
</tbody>
</table>

## Permissions for BigQuery ML tasks

The following table describes the permissions needed for common BigQuery ML tasks.

| Permission                                                                                                                              | Description                                                                                                                                                                                                                                   |
|-----------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `bigquery.jobs.create` `bigquery.models.create` `bigquery.models.getData` `bigquery.models.updateData`                                  | Create a new model using `CREATE MODEL` statement                                                                                                                                                                                             |
| `bigquery.jobs.create` `bigquery.models.create` `bigquery.models.getData` `bigquery.models.updateData` `bigquery.models.updateMetadata` | Replace an existing model using `CREATE OR REPLACE MODEL` statement                                                                                                                                                                           |
| `bigquery.models.delete`                                                                                                                | Delete model using [models.delete](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/models/delete) API                                                                                                                           |
| `bigquery.jobs.create` `bigquery.models.delete`                                                                                         | Delete model using `DROP MODEL` statement                                                                                                                                                                                                     |
| `bigquery.models.getMetadata`                                                                                                           | Get model metadata using [models.get](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/models/get) API                                                                                                                           |
| `bigquery.models.list`                                                                                                                  | List models and metadata on models using [models.list](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/models/list) API                                                                                                         |
| `bigquery.models.updateMetadata`                                                                                                        | Update model metadata using [models.delete](https://docs.cloud.google.com/bigquery/docs/reference/rest/v2/models/delete) API. If setting or updating a non-zero expiration time for Model, `bigquery.models.delete` permission is also needed |
| `bigquery.jobs.create` `bigquery.models.getData`                                                                                        | Perform evaluation, prediction and model and feature inspections using functions such as `ML.EVALUATE` , `ML.PREDICT` , `ML.TRAINING_INFO` , and `ML.WEIGHTS` .                                                                               |
| `bigquery.jobs.create` `bigquery.models.export`                                                                                         | Export a model                                                                                                                                                                                                                                |
| `bigquery.models.updateTag`                                                                                                             | Update [Data Catalog tags](https://docs.cloud.google.com/data-catalog/docs/tags-and-tag-templates) for a model.                                                                                                                               |

## What's next

- For more information about assigning roles at the dataset level, see [Controlling access to datasets](https://docs.cloud.google.com/bigquery/docs/dataset-access-controls) .
- For more information about assigning roles at the table or view level, see [Controlling access to tables and views](https://docs.cloud.google.com/bigquery/docs/table-access-controls) .
