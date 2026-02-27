# BigQuery IAM roles and permissions

This document provides a list of Identity and Access Management (IAM) predefined roles and permissions for BigQuery. This page includes roles and permissions for the following:

  - BigQuery: Roles and permissions that apply to BigQuery resources such as datasets, tables, views, and routines. Many of these roles and permissions can also be granted to Resource Manager resources like projects, folders, and organizations.
  - BigQuery Connection API: Role that grants a [service agent](/iam/docs/service-agents) access to a Cloud SQL connection.
  - BigQuery Continuous Query: Role that grants a [service account](/iam/docs/service-account-overview) access to a continuous query.
  - BigQuery Data Policy: Roles and permissions that apply to Data Policies in BigQuery.
  - BigQuery Data Transfer Service: Role that grants a [service agent](/iam/docs/service-agents) access to create jobs that transfer data.
  - BigQuery Engine for Apache Flink: Roles and permissions that apply to BigQuery Engine for Apache Flink resources.
  - BigQuery Migration Service API: Roles and permissions that apply to BigQuery Migration Service resources.
  - BigQuery Omni: Role that grants a [service agent](/iam/docs/service-agents) access to tables.
  - BigQuery sharing: Roles and permissions that apply to BigQuery sharing resources.

## BigQuery predefined IAM roles

The following tables list the predefined BigQuery IAM roles with a corresponding list of all the [permissions](#bq-permissions) each role includes. Note that each permission is applicable to a particular resource type.

**Note:** When new capabilities are added to BigQuery, new permissions might be added to predefined IAM roles, and new predefined IAM roles might be added to BigQuery. If your organization requires role definitions to remain unchanged, you should create [custom IAM roles](/iam/docs/creating-custom-roles) .

### BigQuery roles

This table lists the predefined IAM roles and permissions for BigQuery. To search through all roles and permissions, see the [role and permission index](/iam/docs/roles-permissions) .

For information on granting predefined roles on BigQuery resources like datasets, tables, and routines, see [Control access to resources with IAM](/bigquery/docs/control-access-to-resources-iam) .

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
<td><h4 id="bigquery.admin" class="role-title add-link" data-text="BigQuery Admin" tabindex="-1">BigQuery Admin</h4>
<p>( <code dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p>Provides permissions to manage all resources within the project. Can manage all data within the project, and can cancel jobs from other users running within the project.</p>
<p>It is possible to grant this role to the following lowest-level resources, but it is not recommended. Other predefined roles grant full permissions over these resources and are less permissive. BigQuery Admin is typically granted at the project level.</p>
<p>Lowest-level resources where you can grant this role:</p>
Dataset
These resources within a dataset:
<ul>
<li>Table</li>
<li>View</li>
<li>Routine</li>
</ul>
Connection
Saved query
Data canvas
Pipeline
Data preparation
Repository
<p>This role can also be granted on Resource Manager resources (projects, folders, and organizations).</p></td>
<td><p><code dir="ltr" translate="no">           bigquery.bireservations.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.bireservations.get          </code></li>
<li><code dir="ltr" translate="no">           bigquery.bireservations.update          </code></li>
</ul>
<p><code dir="ltr" translate="no">           bigquery.capacityCommitments.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.                      capacityCommitments.                      create          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      capacityCommitments.                      delete          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      capacityCommitments.                      get          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      capacityCommitments.                      list          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      capacityCommitments.                      update          </code></li>
</ul>
<p><code dir="ltr" translate="no">           bigquery.config.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.config.get          </code></li>
<li><code dir="ltr" translate="no">           bigquery.config.update          </code></li>
</ul>
<p><code dir="ltr" translate="no">           bigquery.connections.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.connections.create          </code></li>
<li><code dir="ltr" translate="no">           bigquery.connections.delegate          </code></li>
<li><code dir="ltr" translate="no">           bigquery.connections.delete          </code></li>
<li><code dir="ltr" translate="no">           bigquery.connections.get          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      connections.                      getIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           bigquery.connections.list          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      connections.                      setIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           bigquery.connections.update          </code></li>
<li><code dir="ltr" translate="no">           bigquery.connections.updateTag          </code></li>
<li><code dir="ltr" translate="no">           bigquery.connections.use          </code></li>
</ul>
<p><code dir="ltr" translate="no">         bigquery.dataPolicies.attach        </code></p>
<p><code dir="ltr" translate="no">         bigquery.dataPolicies.create        </code></p>
<p><code dir="ltr" translate="no">         bigquery.dataPolicies.delete        </code></p>
<p><code dir="ltr" translate="no">         bigquery.dataPolicies.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  dataPolicies.                  getIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         bigquery.dataPolicies.list        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  dataPolicies.                  setIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         bigquery.dataPolicies.update        </code></p>
<p><code dir="ltr" translate="no">           bigquery.datasets.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.datasets.create          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      datasets.                      createTagBinding          </code></li>
<li><code dir="ltr" translate="no">           bigquery.datasets.delete          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      datasets.                      deleteTagBinding          </code></li>
<li><code dir="ltr" translate="no">           bigquery.datasets.get          </code></li>
<li><code dir="ltr" translate="no">           bigquery.datasets.getIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           bigquery.datasets.link          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      datasets.                      listEffectiveTags          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      datasets.                      listSharedDatasetUsage          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      datasets.                      listTagBindings          </code></li>
<li><code dir="ltr" translate="no">           bigquery.datasets.setIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           bigquery.datasets.update          </code></li>
<li><code dir="ltr" translate="no">           bigquery.datasets.updateTag          </code></li>
</ul>
<p><code dir="ltr" translate="no">           bigquery.jobs.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.jobs.create          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      jobs.                      createGlobalQuery          </code></li>
<li><code dir="ltr" translate="no">           bigquery.jobs.delete          </code></li>
<li><code dir="ltr" translate="no">           bigquery.jobs.get          </code></li>
<li><code dir="ltr" translate="no">           bigquery.jobs.list          </code></li>
<li><code dir="ltr" translate="no">           bigquery.jobs.listAll          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      jobs.                      listExecutionMetadata          </code></li>
<li><code dir="ltr" translate="no">           bigquery.jobs.update          </code></li>
</ul>
<p><code dir="ltr" translate="no">           bigquery.models.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.models.create          </code></li>
<li><code dir="ltr" translate="no">           bigquery.models.delete          </code></li>
<li><code dir="ltr" translate="no">           bigquery.models.export          </code></li>
<li><code dir="ltr" translate="no">           bigquery.models.getData          </code></li>
<li><code dir="ltr" translate="no">           bigquery.models.getMetadata          </code></li>
<li><code dir="ltr" translate="no">           bigquery.models.list          </code></li>
<li><code dir="ltr" translate="no">           bigquery.models.updateData          </code></li>
<li><code dir="ltr" translate="no">           bigquery.models.updateMetadata          </code></li>
<li><code dir="ltr" translate="no">           bigquery.models.updateTag          </code></li>
</ul>
<p><code dir="ltr" translate="no">           bigquery.objectRefs.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.objectRefs.read          </code></li>
<li><code dir="ltr" translate="no">           bigquery.objectRefs.write          </code></li>
</ul>
<p><code dir="ltr" translate="no">           bigquery.readsessions.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.readsessions.create          </code></li>
<li><code dir="ltr" translate="no">           bigquery.readsessions.getData          </code></li>
<li><code dir="ltr" translate="no">           bigquery.readsessions.update          </code></li>
</ul>
<p><code dir="ltr" translate="no">           bigquery.                      reservationAssignments.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.                      reservationAssignments.                      create          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      reservationAssignments.                      delete          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      reservationAssignments.                      list          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      reservationAssignments.                      search          </code></li>
</ul>
<p><code dir="ltr" translate="no">           bigquery.reservationGroups.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.                      reservationGroups.                      create          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      reservationGroups.                      delete          </code></li>
<li><code dir="ltr" translate="no">           bigquery.reservationGroups.get          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      reservationGroups.                      list          </code></li>
</ul>
<p><code dir="ltr" translate="no">           bigquery.reservations.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.reservations.create          </code></li>
<li><code dir="ltr" translate="no">           bigquery.reservations.delete          </code></li>
<li><code dir="ltr" translate="no">           bigquery.reservations.get          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      reservations.                      getIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           bigquery.reservations.list          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      reservations.                      listFailoverDatasets          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      reservations.                      setIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           bigquery.reservations.update          </code></li>
<li><code dir="ltr" translate="no">           bigquery.reservations.use          </code></li>
</ul>
<p><code dir="ltr" translate="no">           bigquery.routines.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.routines.create          </code></li>
<li><code dir="ltr" translate="no">           bigquery.routines.delete          </code></li>
<li><code dir="ltr" translate="no">           bigquery.routines.get          </code></li>
<li><code dir="ltr" translate="no">           bigquery.routines.list          </code></li>
<li><code dir="ltr" translate="no">           bigquery.routines.update          </code></li>
<li><code dir="ltr" translate="no">           bigquery.routines.updateTag          </code></li>
</ul>
<p><code dir="ltr" translate="no">         bigquery.                  rowAccessPolicies.                  create        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  rowAccessPolicies.                  delete        </code></p>
<p><code dir="ltr" translate="no">         bigquery.rowAccessPolicies.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  rowAccessPolicies.                  getIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  rowAccessPolicies.                  list        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  rowAccessPolicies.                  overrideTimeTravelRestrictions        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  rowAccessPolicies.                  setIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  rowAccessPolicies.                  update        </code></p>
<p><code dir="ltr" translate="no">           bigquery.savedqueries.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.savedqueries.create          </code></li>
<li><code dir="ltr" translate="no">           bigquery.savedqueries.delete          </code></li>
<li><code dir="ltr" translate="no">           bigquery.savedqueries.get          </code></li>
<li><code dir="ltr" translate="no">           bigquery.savedqueries.list          </code></li>
<li><code dir="ltr" translate="no">           bigquery.savedqueries.update          </code></li>
</ul>
<p><code dir="ltr" translate="no">           bigquery.tables.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.tables.create          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.createIndex          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.createSnapshot          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      tables.                      createTagBinding          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.delete          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.deleteIndex          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.deleteSnapshot          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      tables.                      deleteTagBinding          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.export          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.get          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.getData          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.getIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.list          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      tables.                      listEffectiveTags          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      tables.                      listTagBindings          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.replicateData          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      tables.                      restoreSnapshot          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.setCategory          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      tables.                      setColumnDataPolicy          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.setIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.update          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.updateData          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.updateIndex          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.updateTag          </code></li>
</ul>
<p><code dir="ltr" translate="no">           bigquery.transfers.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.transfers.get          </code></li>
<li><code dir="ltr" translate="no">           bigquery.transfers.update          </code></li>
</ul>
<p><code dir="ltr" translate="no">         bigquerymigration.                  translation.                  translate        </code></p>
<p><code dir="ltr" translate="no">           cloudkms.keyHandles.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           cloudkms.keyHandles.create          </code></li>
<li><code dir="ltr" translate="no">           cloudkms.keyHandles.get          </code></li>
<li><code dir="ltr" translate="no">           cloudkms.keyHandles.list          </code></li>
</ul>
<p><code dir="ltr" translate="no">         cloudkms.operations.get        </code></p>
<p><code dir="ltr" translate="no">         cloudkms.                  projects.                  showEffectiveAutokeyConfig        </code></p>
<p><code dir="ltr" translate="no">           dataform.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           dataform.commentThreads.create          </code></li>
<li><code dir="ltr" translate="no">           dataform.commentThreads.delete          </code></li>
<li><code dir="ltr" translate="no">           dataform.commentThreads.get          </code></li>
<li><code dir="ltr" translate="no">           dataform.commentThreads.list          </code></li>
<li><code dir="ltr" translate="no">           dataform.commentThreads.update          </code></li>
<li><code dir="ltr" translate="no">           dataform.comments.create          </code></li>
<li><code dir="ltr" translate="no">           dataform.comments.delete          </code></li>
<li><code dir="ltr" translate="no">           dataform.comments.get          </code></li>
<li><code dir="ltr" translate="no">           dataform.comments.list          </code></li>
<li><code dir="ltr" translate="no">           dataform.comments.update          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      compilationResults.                      create          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      compilationResults.                      get          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      compilationResults.                      list          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      compilationResults.                      query          </code></li>
<li><code dir="ltr" translate="no">           dataform.config.get          </code></li>
<li><code dir="ltr" translate="no">           dataform.config.update          </code></li>
<li><code dir="ltr" translate="no">           dataform.folders.addContents          </code></li>
<li><code dir="ltr" translate="no">           dataform.folders.create          </code></li>
<li><code dir="ltr" translate="no">           dataform.folders.delete          </code></li>
<li><code dir="ltr" translate="no">           dataform.folders.get          </code></li>
<li><code dir="ltr" translate="no">           dataform.folders.getIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           dataform.folders.move          </code></li>
<li><code dir="ltr" translate="no">           dataform.folders.queryContents          </code></li>
<li><code dir="ltr" translate="no">           dataform.folders.setIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           dataform.folders.update          </code></li>
<li><code dir="ltr" translate="no">           dataform.locations.get          </code></li>
<li><code dir="ltr" translate="no">           dataform.locations.list          </code></li>
<li><code dir="ltr" translate="no">           dataform.operations.cancel          </code></li>
<li><code dir="ltr" translate="no">           dataform.operations.delete          </code></li>
<li><code dir="ltr" translate="no">           dataform.operations.get          </code></li>
<li><code dir="ltr" translate="no">           dataform.operations.list          </code></li>
<li><code dir="ltr" translate="no">           dataform.releaseConfigs.create          </code></li>
<li><code dir="ltr" translate="no">           dataform.releaseConfigs.delete          </code></li>
<li><code dir="ltr" translate="no">           dataform.releaseConfigs.get          </code></li>
<li><code dir="ltr" translate="no">           dataform.releaseConfigs.list          </code></li>
<li><code dir="ltr" translate="no">           dataform.releaseConfigs.update          </code></li>
<li><code dir="ltr" translate="no">           dataform.repositories.commit          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      repositories.                      computeAccessTokenStatus          </code></li>
<li><code dir="ltr" translate="no">           dataform.repositories.create          </code></li>
<li><code dir="ltr" translate="no">           dataform.repositories.delete          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      repositories.                      fetchHistory          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      repositories.                      fetchRemoteBranches          </code></li>
<li><code dir="ltr" translate="no">           dataform.repositories.get          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      repositories.                      getIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           dataform.repositories.list          </code></li>
<li><code dir="ltr" translate="no">           dataform.repositories.move          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      repositories.                      queryDirectoryContents          </code></li>
<li><code dir="ltr" translate="no">           dataform.repositories.readFile          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      repositories.                      scheduleRelease          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      repositories.                      scheduleWorkflow          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      repositories.                      setIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           dataform.repositories.update          </code></li>
<li><code dir="ltr" translate="no">           dataform.teamFolders.create          </code></li>
<li><code dir="ltr" translate="no">           dataform.teamFolders.delete          </code></li>
<li><code dir="ltr" translate="no">           dataform.teamFolders.get          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      teamFolders.                      getIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      teamFolders.                      setIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           dataform.teamFolders.update          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      workflowConfigs.                      create          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      workflowConfigs.                      delete          </code></li>
<li><code dir="ltr" translate="no">           dataform.workflowConfigs.get          </code></li>
<li><code dir="ltr" translate="no">           dataform.workflowConfigs.list          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      workflowConfigs.                      update          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      workflowInvocations.                      cancel          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      workflowInvocations.                      create          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      workflowInvocations.                      delete          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      workflowInvocations.                      get          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      workflowInvocations.                      list          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      workflowInvocations.                      query          </code></li>
<li><code dir="ltr" translate="no">           dataform.workspaces.commit          </code></li>
<li><code dir="ltr" translate="no">           dataform.workspaces.create          </code></li>
<li><code dir="ltr" translate="no">           dataform.workspaces.delete          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      workspaces.                      fetchFileDiff          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      workspaces.                      fetchFileGitStatuses          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      workspaces.                      fetchGitAheadBehind          </code></li>
<li><code dir="ltr" translate="no">           dataform.workspaces.get          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      workspaces.                      getIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      workspaces.                      installNpmPackages          </code></li>
<li><code dir="ltr" translate="no">           dataform.workspaces.list          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      workspaces.                      makeDirectory          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      workspaces.                      moveDirectory          </code></li>
<li><code dir="ltr" translate="no">           dataform.workspaces.moveFile          </code></li>
<li><code dir="ltr" translate="no">           dataform.workspaces.pull          </code></li>
<li><code dir="ltr" translate="no">           dataform.workspaces.push          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      workspaces.                      queryDirectoryContents          </code></li>
<li><code dir="ltr" translate="no">           dataform.workspaces.readFile          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      workspaces.                      removeDirectory          </code></li>
<li><code dir="ltr" translate="no">           dataform.workspaces.removeFile          </code></li>
<li><code dir="ltr" translate="no">           dataform.workspaces.reset          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      workspaces.                      searchFiles          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      workspaces.                      setIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           dataform.workspaces.writeFile          </code></li>
</ul>
<p><code dir="ltr" translate="no">           dataplex.datascans.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           dataplex.datascans.create          </code></li>
<li><code dir="ltr" translate="no">           dataplex.datascans.delete          </code></li>
<li><code dir="ltr" translate="no">           dataplex.datascans.get          </code></li>
<li><code dir="ltr" translate="no">           dataplex.datascans.getData          </code></li>
<li><code dir="ltr" translate="no">           dataplex.                      datascans.                      getIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           dataplex.datascans.list          </code></li>
<li><code dir="ltr" translate="no">           dataplex.datascans.run          </code></li>
<li><code dir="ltr" translate="no">           dataplex.                      datascans.                      setIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           dataplex.datascans.update          </code></li>
</ul>
<p><code dir="ltr" translate="no">         dataplex.operations.get        </code></p>
<p><code dir="ltr" translate="no">         dataplex.operations.list        </code></p>
<p><code dir="ltr" translate="no">         dataplex.projects.search        </code></p>
<p><code dir="ltr" translate="no">         resourcemanager.projects.get        </code></p>
<p><code dir="ltr" translate="no">         resourcemanager.projects.list        </code></p></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.connectedSheetsServiceAgent" class="role-title add-link" data-text="Connected Sheets Service Agent" tabindex="-1">Connected Sheets Service Agent</h4>
<p>( <code dir="ltr" translate="no">         roles/                  bigquery.connectedSheetsServiceAgent        </code> )</p>
<p>Grants Connected Sheets Service Account access to create and manage BigQuery jobs on the customers resources.</p>
<strong>Warning:</strong> Do not grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .</td>
<td><p><code dir="ltr" translate="no">         bigquery.datasets.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.jobs.create        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.create        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.update        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.updateData        </code></p></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.connectionAdmin" class="role-title add-link" data-text="BigQuery Connection Admin" tabindex="-1">BigQuery Connection Admin</h4>
<p>( <code dir="ltr" translate="no">         roles/                  bigquery.connectionAdmin        </code> )</p>
<p>Lowest-level resources where you can grant this role:</p>
<ul>
<li>Connection</li>
</ul>
<p>This role can also be granted on Resource Manager resources (projects, folders, and organizations).</p></td>
<td><p><code dir="ltr" translate="no">           bigquery.connections.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.connections.create          </code></li>
<li><code dir="ltr" translate="no">           bigquery.connections.delegate          </code></li>
<li><code dir="ltr" translate="no">           bigquery.connections.delete          </code></li>
<li><code dir="ltr" translate="no">           bigquery.connections.get          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      connections.                      getIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           bigquery.connections.list          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      connections.                      setIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           bigquery.connections.update          </code></li>
<li><code dir="ltr" translate="no">           bigquery.connections.updateTag          </code></li>
<li><code dir="ltr" translate="no">           bigquery.connections.use          </code></li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.connectionUser" class="role-title add-link" data-text="BigQuery Connection User" tabindex="-1">BigQuery Connection User</h4>
<p>( <code dir="ltr" translate="no">         roles/                  bigquery.connectionUser        </code> )</p>
<p>Lowest-level resources where you can grant this role:</p>
<ul>
<li>Connection</li>
</ul>
<p>This role can also be granted on Resource Manager resources (projects, folders, and organizations).</p></td>
<td><p><code dir="ltr" translate="no">         bigquery.connections.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  connections.                  getIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         bigquery.connections.list        </code></p>
<p><code dir="ltr" translate="no">         bigquery.connections.use        </code></p></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.dataEditor" class="role-title add-link" data-text="BigQuery Data Editor" tabindex="-1">BigQuery Data Editor</h4>
<p>( <code dir="ltr" translate="no">         roles/                  bigquery.dataEditor        </code> )</p>
<p>When granted on a dataset, this role grants these permissions:</p>
Get metadata and permissions for the dataset.
For tables and views:
<ul>
<li>Create, update, get, list, and delete the dataset's tables and views.</li>
<li>Read (query), export, replicate, and update table data.</li>
<li>Create, update, and delete indexes.</li>
<li>Create and restore snapshots.</li>
</ul>
All permissions for the dataset's routines and models.
<strong>Note:</strong> Principals that are granted the Data Editor role at the project level can also create new datasets and list datasets in the project that they have access to.
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
<strong>Note:</strong> The BigQuery Data Editor role is mapped to the <a href="/bigquery/docs/access-control-basic-roles#dataset-basic-roles"><code dir="ltr" translate="no">           WRITER          </code></a> BigQuery basic role. When you grant the BigQuery Data Editor role to a principal at the dataset level, the principal is granted <code dir="ltr" translate="no">          WRITER         </code> access to the dataset.
<p>Lowest-level resources where you can grant this role:</p>
Dataset
These resources within a dataset:
<ul>
<li>Table</li>
<li>View</li>
<li>Routine</li>
</ul>
<p>This role can also be granted on Resource Manager resources (projects, folders, and organizations).</p></td>
<td><p><code dir="ltr" translate="no">         bigquery.config.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.datasets.create        </code></p>
<p><code dir="ltr" translate="no">         bigquery.datasets.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.datasets.getIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         bigquery.datasets.updateTag        </code></p>
<p><code dir="ltr" translate="no">           bigquery.models.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.models.create          </code></li>
<li><code dir="ltr" translate="no">           bigquery.models.delete          </code></li>
<li><code dir="ltr" translate="no">           bigquery.models.export          </code></li>
<li><code dir="ltr" translate="no">           bigquery.models.getData          </code></li>
<li><code dir="ltr" translate="no">           bigquery.models.getMetadata          </code></li>
<li><code dir="ltr" translate="no">           bigquery.models.list          </code></li>
<li><code dir="ltr" translate="no">           bigquery.models.updateData          </code></li>
<li><code dir="ltr" translate="no">           bigquery.models.updateMetadata          </code></li>
<li><code dir="ltr" translate="no">           bigquery.models.updateTag          </code></li>
</ul>
<p><code dir="ltr" translate="no">           bigquery.routines.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.routines.create          </code></li>
<li><code dir="ltr" translate="no">           bigquery.routines.delete          </code></li>
<li><code dir="ltr" translate="no">           bigquery.routines.get          </code></li>
<li><code dir="ltr" translate="no">           bigquery.routines.list          </code></li>
<li><code dir="ltr" translate="no">           bigquery.routines.update          </code></li>
<li><code dir="ltr" translate="no">           bigquery.routines.updateTag          </code></li>
</ul>
<p><code dir="ltr" translate="no">         bigquery.tables.create        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.createIndex        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.createSnapshot        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.delete        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.deleteIndex        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.export        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.getData        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.getIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.list        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.replicateData        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  tables.                  restoreSnapshot        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.update        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.updateData        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.updateIndex        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.updateTag        </code></p>
<p><code dir="ltr" translate="no">           cloudkms.keyHandles.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           cloudkms.keyHandles.create          </code></li>
<li><code dir="ltr" translate="no">           cloudkms.keyHandles.get          </code></li>
<li><code dir="ltr" translate="no">           cloudkms.keyHandles.list          </code></li>
</ul>
<p><code dir="ltr" translate="no">         cloudkms.operations.get        </code></p>
<p><code dir="ltr" translate="no">         cloudkms.                  projects.                  showEffectiveAutokeyConfig        </code></p>
<p><code dir="ltr" translate="no">         dataplex.datascans.create        </code></p>
<p><code dir="ltr" translate="no">         dataplex.datascans.delete        </code></p>
<p><code dir="ltr" translate="no">         dataplex.datascans.get        </code></p>
<p><code dir="ltr" translate="no">         dataplex.datascans.getData        </code></p>
<p><code dir="ltr" translate="no">         dataplex.                  datascans.                  getIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         dataplex.datascans.list        </code></p>
<p><code dir="ltr" translate="no">         dataplex.datascans.run        </code></p>
<p><code dir="ltr" translate="no">         dataplex.datascans.update        </code></p>
<p><code dir="ltr" translate="no">         dataplex.operations.get        </code></p>
<p><code dir="ltr" translate="no">         dataplex.operations.list        </code></p>
<p><code dir="ltr" translate="no">         resourcemanager.projects.get        </code></p>
<p><code dir="ltr" translate="no">         resourcemanager.projects.list        </code></p></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.dataOwner" class="role-title add-link" data-text="BigQuery Data Owner" tabindex="-1">BigQuery Data Owner</h4>
<p>( <code dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p>When granted on a dataset, this role grants these permissions:</p>
<ul>
<li>All permissions for the dataset and for all of the resources within the dataset: tables and views, models, and routines.</li>
</ul>
<strong>Note:</strong> Principals that are granted the Data Owner role at the project level can also create new datasets and list datasets in the project that they have access to.
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
<strong>Note:</strong> The BigQuery Data Owner role is mapped to the <a href="/bigquery/docs/access-control-basic-roles#dataset-basic-roles"><code dir="ltr" translate="no">           OWNER          </code></a> BigQuery basic role. When you grant the BigQuery Data Owner role to a principal at the dataset level, the principal is granted <code dir="ltr" translate="no">          OWNER         </code> access to the dataset.
<p>Lowest-level resources where you can grant this role:</p>
Dataset
These resources within a dataset:
<ul>
<li>Table</li>
<li>View</li>
<li>Routine</li>
</ul>
<p>This role can also be granted on Resource Manager resources (projects, folders, and organizations).</p></td>
<td><p><code dir="ltr" translate="no">         bigquery.config.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.dataPolicies.attach        </code></p>
<p><code dir="ltr" translate="no">         bigquery.dataPolicies.create        </code></p>
<p><code dir="ltr" translate="no">         bigquery.dataPolicies.delete        </code></p>
<p><code dir="ltr" translate="no">         bigquery.dataPolicies.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  dataPolicies.                  getIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         bigquery.dataPolicies.list        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  dataPolicies.                  setIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         bigquery.dataPolicies.update        </code></p>
<p><code dir="ltr" translate="no">           bigquery.datasets.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.datasets.create          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      datasets.                      createTagBinding          </code></li>
<li><code dir="ltr" translate="no">           bigquery.datasets.delete          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      datasets.                      deleteTagBinding          </code></li>
<li><code dir="ltr" translate="no">           bigquery.datasets.get          </code></li>
<li><code dir="ltr" translate="no">           bigquery.datasets.getIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           bigquery.datasets.link          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      datasets.                      listEffectiveTags          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      datasets.                      listSharedDatasetUsage          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      datasets.                      listTagBindings          </code></li>
<li><code dir="ltr" translate="no">           bigquery.datasets.setIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           bigquery.datasets.update          </code></li>
<li><code dir="ltr" translate="no">           bigquery.datasets.updateTag          </code></li>
</ul>
<p><code dir="ltr" translate="no">           bigquery.models.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.models.create          </code></li>
<li><code dir="ltr" translate="no">           bigquery.models.delete          </code></li>
<li><code dir="ltr" translate="no">           bigquery.models.export          </code></li>
<li><code dir="ltr" translate="no">           bigquery.models.getData          </code></li>
<li><code dir="ltr" translate="no">           bigquery.models.getMetadata          </code></li>
<li><code dir="ltr" translate="no">           bigquery.models.list          </code></li>
<li><code dir="ltr" translate="no">           bigquery.models.updateData          </code></li>
<li><code dir="ltr" translate="no">           bigquery.models.updateMetadata          </code></li>
<li><code dir="ltr" translate="no">           bigquery.models.updateTag          </code></li>
</ul>
<p><code dir="ltr" translate="no">           bigquery.routines.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.routines.create          </code></li>
<li><code dir="ltr" translate="no">           bigquery.routines.delete          </code></li>
<li><code dir="ltr" translate="no">           bigquery.routines.get          </code></li>
<li><code dir="ltr" translate="no">           bigquery.routines.list          </code></li>
<li><code dir="ltr" translate="no">           bigquery.routines.update          </code></li>
<li><code dir="ltr" translate="no">           bigquery.routines.updateTag          </code></li>
</ul>
<p><code dir="ltr" translate="no">         bigquery.                  rowAccessPolicies.                  create        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  rowAccessPolicies.                  delete        </code></p>
<p><code dir="ltr" translate="no">         bigquery.rowAccessPolicies.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  rowAccessPolicies.                  getIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  rowAccessPolicies.                  list        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  rowAccessPolicies.                  setIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  rowAccessPolicies.                  update        </code></p>
<p><code dir="ltr" translate="no">           bigquery.tables.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.tables.create          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.createIndex          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.createSnapshot          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      tables.                      createTagBinding          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.delete          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.deleteIndex          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.deleteSnapshot          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      tables.                      deleteTagBinding          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.export          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.get          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.getData          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.getIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.list          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      tables.                      listEffectiveTags          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      tables.                      listTagBindings          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.replicateData          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      tables.                      restoreSnapshot          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.setCategory          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      tables.                      setColumnDataPolicy          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.setIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.update          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.updateData          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.updateIndex          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.updateTag          </code></li>
</ul>
<p><code dir="ltr" translate="no">           cloudkms.keyHandles.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           cloudkms.keyHandles.create          </code></li>
<li><code dir="ltr" translate="no">           cloudkms.keyHandles.get          </code></li>
<li><code dir="ltr" translate="no">           cloudkms.keyHandles.list          </code></li>
</ul>
<p><code dir="ltr" translate="no">         cloudkms.operations.get        </code></p>
<p><code dir="ltr" translate="no">         cloudkms.                  projects.                  showEffectiveAutokeyConfig        </code></p>
<p><code dir="ltr" translate="no">           dataplex.datascans.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           dataplex.datascans.create          </code></li>
<li><code dir="ltr" translate="no">           dataplex.datascans.delete          </code></li>
<li><code dir="ltr" translate="no">           dataplex.datascans.get          </code></li>
<li><code dir="ltr" translate="no">           dataplex.datascans.getData          </code></li>
<li><code dir="ltr" translate="no">           dataplex.                      datascans.                      getIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           dataplex.datascans.list          </code></li>
<li><code dir="ltr" translate="no">           dataplex.datascans.run          </code></li>
<li><code dir="ltr" translate="no">           dataplex.                      datascans.                      setIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           dataplex.datascans.update          </code></li>
</ul>
<p><code dir="ltr" translate="no">         dataplex.operations.get        </code></p>
<p><code dir="ltr" translate="no">         dataplex.operations.list        </code></p>
<p><code dir="ltr" translate="no">         resourcemanager.projects.get        </code></p>
<p><code dir="ltr" translate="no">         resourcemanager.projects.list        </code></p></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.dataViewer" class="role-title add-link" data-text="BigQuery Data Viewer" tabindex="-1">BigQuery Data Viewer</h4>
<p>( <code dir="ltr" translate="no">         roles/                  bigquery.dataViewer        </code> )</p>
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
<strong>Note:</strong> The BigQuery Data Viewer role is mapped to the <a href="/bigquery/docs/access-control-basic-roles#dataset-basic-roles"><code dir="ltr" translate="no">           READER          </code></a> BigQuery basic role. When you grant the BigQuery Data Viewer role to a principal at the dataset level, the principal is granted <code dir="ltr" translate="no">          READER         </code> access to the dataset.
<p>Lowest-level resources where you can grant this role:</p>
Dataset
These resources within a dataset:
<ul>
<li>Table</li>
<li>View</li>
<li>Routine</li>
</ul>
<p>This role can also be granted on Resource Manager resources (projects, folders, and organizations).</p></td>
<td><p><code dir="ltr" translate="no">         bigquery.datasets.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.datasets.getIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         bigquery.models.export        </code></p>
<p><code dir="ltr" translate="no">         bigquery.models.getData        </code></p>
<p><code dir="ltr" translate="no">         bigquery.models.getMetadata        </code></p>
<p><code dir="ltr" translate="no">         bigquery.models.list        </code></p>
<p><code dir="ltr" translate="no">         bigquery.routines.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.routines.list        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.createSnapshot        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.export        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.getData        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.getIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.list        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.replicateData        </code></p>
<p><code dir="ltr" translate="no">         dataplex.datascans.get        </code></p>
<p><code dir="ltr" translate="no">         dataplex.datascans.getData        </code></p>
<p><code dir="ltr" translate="no">         dataplex.                  datascans.                  getIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         dataplex.datascans.list        </code></p>
<p><code dir="ltr" translate="no">         resourcemanager.projects.get        </code></p>
<p><code dir="ltr" translate="no">         resourcemanager.projects.list        </code></p></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.filteredDataViewer" class="role-title add-link" data-text="BigQuery Filtered Data Viewer" tabindex="-1">BigQuery Filtered Data Viewer</h4>
<p>( <code dir="ltr" translate="no">         roles/                  bigquery.filteredDataViewer        </code> )</p>
<p>Access to view filtered table data defined by a row access policy. <code dir="ltr" translate="no">          bigquery.filteredDataViewer         </code> is a system-managed role. Grant the role by using row-level access policies. Don't apply the role directly to a resource through Identity and Access Management (IAM).</p></td>
<td><p><code dir="ltr" translate="no">         bigquery.                  rowAccessPolicies.                  getFilteredData        </code></p></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.jobUser" class="role-title add-link" data-text="BigQuery Job User" tabindex="-1">BigQuery Job User</h4>
<p>( <code dir="ltr" translate="no">         roles/                  bigquery.jobUser        </code> )</p>
<p>Provides permissions to run jobs, including queries, within the project.</p>
<p>This role can only be granted on Resource Manager resources (projects, folders, and organizations).</p></td>
<td><p><code dir="ltr" translate="no">         bigquery.config.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.jobs.create        </code></p>
<p><code dir="ltr" translate="no">         dataform.folders.create        </code></p>
<p><code dir="ltr" translate="no">           dataform.locations.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           dataform.locations.get          </code></li>
<li><code dir="ltr" translate="no">           dataform.locations.list          </code></li>
</ul>
<p><code dir="ltr" translate="no">         dataform.repositories.create        </code></p>
<p><code dir="ltr" translate="no">         dataform.repositories.list        </code></p>
<p><code dir="ltr" translate="no">         resourcemanager.projects.get        </code></p>
<p><code dir="ltr" translate="no">         resourcemanager.projects.list        </code></p></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.metadataViewer" class="role-title add-link" data-text="BigQuery Metadata Viewer" tabindex="-1">BigQuery Metadata Viewer</h4>
<p>( <code dir="ltr" translate="no">         roles/                  bigquery.metadataViewer        </code> )</p>
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
Dataset
These resources within a dataset:
<ul>
<li>Table</li>
<li>View</li>
<li>Routine</li>
</ul>
<p>This role can also be granted on Resource Manager resources (projects, folders, and organizations).</p></td>
<td><p><code dir="ltr" translate="no">         bigquery.datasets.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.datasets.getIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         bigquery.models.getMetadata        </code></p>
<p><code dir="ltr" translate="no">         bigquery.models.list        </code></p>
<p><code dir="ltr" translate="no">         bigquery.routines.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.routines.list        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.getIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.list        </code></p>
<p><code dir="ltr" translate="no">         dataplex.projects.search        </code></p>
<p><code dir="ltr" translate="no">         resourcemanager.projects.get        </code></p>
<p><code dir="ltr" translate="no">         resourcemanager.projects.list        </code></p></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.objectRefAdmin" class="role-title add-link" data-text="BigQuery ObjectRef Admin" tabindex="-1">BigQuery ObjectRef Admin</h4>
<p>( <code dir="ltr" translate="no">         roles/                  bigquery.objectRefAdmin        </code> )</p>
<p>Administer ObjectRef resources that includes read and write permissions</p>
<p>Lowest-level resources where you can grant this role:</p>
<ul>
<li>Connection</li>
</ul>
<p>This role can also be granted on Resource Manager resources (projects, folders, and organizations).</p></td>
<td><p><code dir="ltr" translate="no">           bigquery.objectRefs.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.objectRefs.read          </code></li>
<li><code dir="ltr" translate="no">           bigquery.objectRefs.write          </code></li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.objectRefReader" class="role-title add-link" data-text="BigQuery ObjectRef Reader" tabindex="-1">BigQuery ObjectRef Reader</h4>
<p>( <code dir="ltr" translate="no">         roles/                  bigquery.objectRefReader        </code> )</p>
<p>Role for reading referenced objects via ObjectRefs in BigQuery</p>
<p>Lowest-level resources where you can grant this role:</p>
<ul>
<li>Connection</li>
</ul>
<p>This role can also be granted on Resource Manager resources (projects, folders, and organizations).</p></td>
<td><p><code dir="ltr" translate="no">         bigquery.objectRefs.read        </code></p></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.readSessionUser" class="role-title add-link" data-text="BigQuery Read Session User" tabindex="-1">BigQuery Read Session User</h4>
<p>( <code dir="ltr" translate="no">         roles/                  bigquery.readSessionUser        </code> )</p>
<p>Provides the ability to create and use read sessions.</p>
<p>This role can only be granted on Resource Manager resources (projects, folders, and organizations).</p></td>
<td><p><code dir="ltr" translate="no">           bigquery.readsessions.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.readsessions.create          </code></li>
<li><code dir="ltr" translate="no">           bigquery.readsessions.getData          </code></li>
<li><code dir="ltr" translate="no">           bigquery.readsessions.update          </code></li>
</ul>
<p><code dir="ltr" translate="no">         resourcemanager.projects.get        </code></p>
<p><code dir="ltr" translate="no">         resourcemanager.projects.list        </code></p></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.resourceAdmin" class="role-title add-link" data-text="BigQuery Resource Admin" tabindex="-1">BigQuery Resource Admin</h4>
<p>( <code dir="ltr" translate="no">         roles/                  bigquery.resourceAdmin        </code> )</p>
<p>Administers BigQuery workloads, including slot assignments, commitments, and reservations.</p>
<p>This role can only be granted on Resource Manager resources (projects, folders, and organizations).</p></td>
<td><p><code dir="ltr" translate="no">           bigquery.bireservations.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.bireservations.get          </code></li>
<li><code dir="ltr" translate="no">           bigquery.bireservations.update          </code></li>
</ul>
<p><code dir="ltr" translate="no">           bigquery.capacityCommitments.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.                      capacityCommitments.                      create          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      capacityCommitments.                      delete          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      capacityCommitments.                      get          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      capacityCommitments.                      list          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      capacityCommitments.                      update          </code></li>
</ul>
<p><code dir="ltr" translate="no">         bigquery.jobs.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.jobs.list        </code></p>
<p><code dir="ltr" translate="no">         bigquery.jobs.listAll        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  jobs.                  listExecutionMetadata        </code></p>
<p><code dir="ltr" translate="no">           bigquery.                      reservationAssignments.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.                      reservationAssignments.                      create          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      reservationAssignments.                      delete          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      reservationAssignments.                      list          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      reservationAssignments.                      search          </code></li>
</ul>
<p><code dir="ltr" translate="no">           bigquery.reservationGroups.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.                      reservationGroups.                      create          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      reservationGroups.                      delete          </code></li>
<li><code dir="ltr" translate="no">           bigquery.reservationGroups.get          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      reservationGroups.                      list          </code></li>
</ul>
<p><code dir="ltr" translate="no">           bigquery.reservations.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.reservations.create          </code></li>
<li><code dir="ltr" translate="no">           bigquery.reservations.delete          </code></li>
<li><code dir="ltr" translate="no">           bigquery.reservations.get          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      reservations.                      getIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           bigquery.reservations.list          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      reservations.                      listFailoverDatasets          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      reservations.                      setIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           bigquery.reservations.update          </code></li>
<li><code dir="ltr" translate="no">           bigquery.reservations.use          </code></li>
</ul>
<p><code dir="ltr" translate="no">           recommender.                      bigqueryCapacityCommitmentsInsights.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           recommender.                      bigqueryCapacityCommitmentsInsights.                      get          </code></li>
<li><code dir="ltr" translate="no">           recommender.                      bigqueryCapacityCommitmentsInsights.                      list          </code></li>
<li><code dir="ltr" translate="no">           recommender.                      bigqueryCapacityCommitmentsInsights.                      update          </code></li>
</ul>
<p><code dir="ltr" translate="no">           recommender.                      bigqueryCapacityCommitmentsRecommendations.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           recommender.                      bigqueryCapacityCommitmentsRecommendations.                      get          </code></li>
<li><code dir="ltr" translate="no">           recommender.                      bigqueryCapacityCommitmentsRecommendations.                      list          </code></li>
<li><code dir="ltr" translate="no">           recommender.                      bigqueryCapacityCommitmentsRecommendations.                      update          </code></li>
</ul>
<p><code dir="ltr" translate="no">         resourcemanager.projects.get        </code></p>
<p><code dir="ltr" translate="no">         resourcemanager.projects.list        </code></p></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.resourceEditor" class="role-title add-link" data-text="BigQuery Resource Editor" tabindex="-1">BigQuery Resource Editor</h4>
<p>( <code dir="ltr" translate="no">         roles/                  bigquery.resourceEditor        </code> )</p>
<p>Manages BigQuery workloads, but is unable to create or modify slot commitments.</p>
<p>This role can only be granted on Resource Manager resources (projects, folders, and organizations).</p></td>
<td><p><code dir="ltr" translate="no">         bigquery.bireservations.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  capacityCommitments.                  get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  capacityCommitments.                  list        </code></p>
<p><code dir="ltr" translate="no">         bigquery.jobs.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.jobs.list        </code></p>
<p><code dir="ltr" translate="no">         bigquery.jobs.listAll        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  jobs.                  listExecutionMetadata        </code></p>
<p><code dir="ltr" translate="no">           bigquery.                      reservationAssignments.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.                      reservationAssignments.                      create          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      reservationAssignments.                      delete          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      reservationAssignments.                      list          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      reservationAssignments.                      search          </code></li>
</ul>
<p><code dir="ltr" translate="no">           bigquery.reservationGroups.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.                      reservationGroups.                      create          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      reservationGroups.                      delete          </code></li>
<li><code dir="ltr" translate="no">           bigquery.reservationGroups.get          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      reservationGroups.                      list          </code></li>
</ul>
<p><code dir="ltr" translate="no">         bigquery.reservations.create        </code></p>
<p><code dir="ltr" translate="no">         bigquery.reservations.delete        </code></p>
<p><code dir="ltr" translate="no">         bigquery.reservations.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.reservations.list        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  reservations.                  listFailoverDatasets        </code></p>
<p><code dir="ltr" translate="no">         bigquery.reservations.update        </code></p>
<p><code dir="ltr" translate="no">         bigquery.reservations.use        </code></p>
<p><code dir="ltr" translate="no">         resourcemanager.projects.get        </code></p>
<p><code dir="ltr" translate="no">         resourcemanager.projects.list        </code></p></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.resourceViewer" class="role-title add-link" data-text="BigQuery Resource Viewer" tabindex="-1">BigQuery Resource Viewer</h4>
<p>( <code dir="ltr" translate="no">         roles/                  bigquery.resourceViewer        </code> )</p>
<p>Can view BigQuery workloads, but cannot create or modify slot reservations or commitments.</p>
<p>This role can only be granted on Resource Manager resources (projects, folders, and organizations).</p></td>
<td><p><code dir="ltr" translate="no">         bigquery.bireservations.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  capacityCommitments.                  get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  capacityCommitments.                  list        </code></p>
<p><code dir="ltr" translate="no">         bigquery.jobs.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.jobs.list        </code></p>
<p><code dir="ltr" translate="no">         bigquery.jobs.listAll        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  jobs.                  listExecutionMetadata        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  reservationAssignments.                  list        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  reservationAssignments.                  search        </code></p>
<p><code dir="ltr" translate="no">         bigquery.reservationGroups.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  reservationGroups.                  list        </code></p>
<p><code dir="ltr" translate="no">         bigquery.reservations.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.reservations.list        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  reservations.                  listFailoverDatasets        </code></p>
<p><code dir="ltr" translate="no">         resourcemanager.projects.get        </code></p>
<p><code dir="ltr" translate="no">         resourcemanager.projects.list        </code></p></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.routineAdmin" class="role-title add-link" data-text="BigQuery Authorized Routine Admin Beta" tabindex="-1">BigQuery Authorized Routine Admin <sup>Beta</sup></h4>
<p>( <code dir="ltr" translate="no">         roles/                  bigquery.routineAdmin        </code> )</p>
<p>Role for Authorized Routine to administer supported resources</p></td>
<td><p><code dir="ltr" translate="no">         bigquery.connections.use        </code></p>
<p><code dir="ltr" translate="no">         bigquery.datasets.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.models.getData        </code></p>
<p><code dir="ltr" translate="no">         bigquery.models.getMetadata        </code></p>
<p><code dir="ltr" translate="no">         bigquery.routines.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.routines.list        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.create        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.delete        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.getData        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.list        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.update        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.updateData        </code></p></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.routineDataEditor" class="role-title add-link" data-text="BigQuery Authorized Routine Data Editor Beta" tabindex="-1">BigQuery Authorized Routine Data Editor <sup>Beta</sup></h4>
<p>( <code dir="ltr" translate="no">         roles/                  bigquery.routineDataEditor        </code> )</p>
<p>Role for Authorized Routine to edit contents of supported resources</p></td>
<td><p><code dir="ltr" translate="no">         bigquery.datasets.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.models.getData        </code></p>
<p><code dir="ltr" translate="no">         bigquery.models.getMetadata        </code></p>
<p><code dir="ltr" translate="no">         bigquery.routines.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.routines.list        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.create        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.delete        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.getData        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.list        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.update        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.updateData        </code></p></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.routineDataViewer" class="role-title add-link" data-text="BigQuery Authorized Routine Data Viewer Beta" tabindex="-1">BigQuery Authorized Routine Data Viewer <sup>Beta</sup></h4>
<p>( <code dir="ltr" translate="no">         roles/                  bigquery.routineDataViewer        </code> )</p>
<p>Role for Authorized Routine to view data and contents of supported resources</p></td>
<td><p><code dir="ltr" translate="no">         bigquery.datasets.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.models.getData        </code></p>
<p><code dir="ltr" translate="no">         bigquery.models.getMetadata        </code></p>
<p><code dir="ltr" translate="no">         bigquery.routines.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.routines.list        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.getData        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.list        </code></p></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.routineMetadataViewer" class="role-title add-link" data-text="BigQuery Authorized Routine Metadata Viewer Beta" tabindex="-1">BigQuery Authorized Routine Metadata Viewer <sup>Beta</sup></h4>
<p>( <code dir="ltr" translate="no">         roles/                  bigquery.routineMetadataViewer        </code> )</p>
<p>Role for Authorized Routine to view metadata of supported resources</p></td>
<td><p><code dir="ltr" translate="no">         bigquery.datasets.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.models.getMetadata        </code></p>
<p><code dir="ltr" translate="no">         bigquery.routines.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.routines.list        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.list        </code></p></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.securityAdmin" class="role-title add-link" data-text="BigQuery Security Admin Beta" tabindex="-1">BigQuery Security Admin <sup>Beta</sup></h4>
<p>( <code dir="ltr" translate="no">         roles/                  bigquery.securityAdmin        </code> )</p>
<p>Administer all BigQuery security controls</p></td>
<td><p><code dir="ltr" translate="no">         bigquery.dataPolicies.attach        </code></p>
<p><code dir="ltr" translate="no">         bigquery.dataPolicies.create        </code></p>
<p><code dir="ltr" translate="no">         bigquery.dataPolicies.delete        </code></p>
<p><code dir="ltr" translate="no">         bigquery.dataPolicies.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  dataPolicies.                  getIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         bigquery.dataPolicies.list        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  dataPolicies.                  setIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         bigquery.dataPolicies.update        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  datasets.                  createTagBinding        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  datasets.                  deleteTagBinding        </code></p>
<p><code dir="ltr" translate="no">         bigquery.datasets.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.datasets.getIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  datasets.                  listEffectiveTags        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  datasets.                  listSharedDatasetUsage        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  datasets.                  listTagBindings        </code></p>
<p><code dir="ltr" translate="no">         bigquery.datasets.setIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         bigquery.datasets.update        </code></p>
<p><code dir="ltr" translate="no">         bigquery.datasets.updateTag        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  rowAccessPolicies.                  create        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  rowAccessPolicies.                  delete        </code></p>
<p><code dir="ltr" translate="no">         bigquery.rowAccessPolicies.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  rowAccessPolicies.                  getIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  rowAccessPolicies.                  list        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  rowAccessPolicies.                  setIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  rowAccessPolicies.                  update        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  tables.                  createTagBinding        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  tables.                  deleteTagBinding        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.getIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.list        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  tables.                  listEffectiveTags        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  tables.                  listTagBindings        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  tables.                  setColumnDataPolicy        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.setIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.update        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.updateTag        </code></p>
<p><code dir="ltr" translate="no">         dataplex.projects.search        </code></p></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.studioAdmin" class="role-title add-link" data-text="BigQuery Studio Admin" tabindex="-1">BigQuery Studio Admin</h4>
<p>( <code dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p>Combination role of BigQuery Admin, Dataform Admin, Notebook Runtime Admin and Dataproc Serverless Editor.</p>
<p>It is possible to grant this role to the following lowest-level resources, but it is not recommended. Other predefined roles grant full permissions over these resources and are less permissive. BigQuery Studio Admin is typically granted at the project level.</p>
<p>Lowest-level resources where you can grant this role:</p>
Dataset
These resources within a dataset:
<ul>
<li>Table</li>
<li>View</li>
<li>Routine</li>
</ul>
Connection
Saved query
Data canvas
Data preparation
Pipeline
Repository
<p>This role can also be granted on Resource Manager resources (projects, folders, and organizations).</p></td>
<td><p><code dir="ltr" translate="no">         aiplatform.locations.get        </code></p>
<p><code dir="ltr" translate="no">           aiplatform.                      notebookRuntimeTemplates.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           aiplatform.                      notebookRuntimeTemplates.                      apply          </code></li>
<li><code dir="ltr" translate="no">           aiplatform.                      notebookRuntimeTemplates.                      create          </code></li>
<li><code dir="ltr" translate="no">           aiplatform.                      notebookRuntimeTemplates.                      delete          </code></li>
<li><code dir="ltr" translate="no">           aiplatform.                      notebookRuntimeTemplates.                      get          </code></li>
<li><code dir="ltr" translate="no">           aiplatform.                      notebookRuntimeTemplates.                      getIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           aiplatform.                      notebookRuntimeTemplates.                      list          </code></li>
<li><code dir="ltr" translate="no">           aiplatform.                      notebookRuntimeTemplates.                      setIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           aiplatform.                      notebookRuntimeTemplates.                      update          </code></li>
</ul>
<p><code dir="ltr" translate="no">           aiplatform.notebookRuntimes.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           aiplatform.                      notebookRuntimes.                      assign          </code></li>
<li><code dir="ltr" translate="no">           aiplatform.                      notebookRuntimes.                      delete          </code></li>
<li><code dir="ltr" translate="no">           aiplatform.                      notebookRuntimes.                      get          </code></li>
<li><code dir="ltr" translate="no">           aiplatform.                      notebookRuntimes.                      list          </code></li>
<li><code dir="ltr" translate="no">           aiplatform.                      notebookRuntimes.                      start          </code></li>
<li><code dir="ltr" translate="no">           aiplatform.                      notebookRuntimes.                      update          </code></li>
<li><code dir="ltr" translate="no">           aiplatform.                      notebookRuntimes.                      upgrade          </code></li>
</ul>
<p><code dir="ltr" translate="no">         aiplatform.operations.list        </code></p>
<p><code dir="ltr" translate="no">           bigquery.bireservations.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.bireservations.get          </code></li>
<li><code dir="ltr" translate="no">           bigquery.bireservations.update          </code></li>
</ul>
<p><code dir="ltr" translate="no">           bigquery.capacityCommitments.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.                      capacityCommitments.                      create          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      capacityCommitments.                      delete          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      capacityCommitments.                      get          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      capacityCommitments.                      list          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      capacityCommitments.                      update          </code></li>
</ul>
<p><code dir="ltr" translate="no">           bigquery.config.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.config.get          </code></li>
<li><code dir="ltr" translate="no">           bigquery.config.update          </code></li>
</ul>
<p><code dir="ltr" translate="no">           bigquery.connections.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.connections.create          </code></li>
<li><code dir="ltr" translate="no">           bigquery.connections.delegate          </code></li>
<li><code dir="ltr" translate="no">           bigquery.connections.delete          </code></li>
<li><code dir="ltr" translate="no">           bigquery.connections.get          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      connections.                      getIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           bigquery.connections.list          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      connections.                      setIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           bigquery.connections.update          </code></li>
<li><code dir="ltr" translate="no">           bigquery.connections.updateTag          </code></li>
<li><code dir="ltr" translate="no">           bigquery.connections.use          </code></li>
</ul>
<p><code dir="ltr" translate="no">         bigquery.dataPolicies.attach        </code></p>
<p><code dir="ltr" translate="no">         bigquery.dataPolicies.create        </code></p>
<p><code dir="ltr" translate="no">         bigquery.dataPolicies.delete        </code></p>
<p><code dir="ltr" translate="no">         bigquery.dataPolicies.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  dataPolicies.                  getIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         bigquery.dataPolicies.list        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  dataPolicies.                  setIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         bigquery.dataPolicies.update        </code></p>
<p><code dir="ltr" translate="no">           bigquery.datasets.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.datasets.create          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      datasets.                      createTagBinding          </code></li>
<li><code dir="ltr" translate="no">           bigquery.datasets.delete          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      datasets.                      deleteTagBinding          </code></li>
<li><code dir="ltr" translate="no">           bigquery.datasets.get          </code></li>
<li><code dir="ltr" translate="no">           bigquery.datasets.getIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           bigquery.datasets.link          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      datasets.                      listEffectiveTags          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      datasets.                      listSharedDatasetUsage          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      datasets.                      listTagBindings          </code></li>
<li><code dir="ltr" translate="no">           bigquery.datasets.setIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           bigquery.datasets.update          </code></li>
<li><code dir="ltr" translate="no">           bigquery.datasets.updateTag          </code></li>
</ul>
<p><code dir="ltr" translate="no">           bigquery.jobs.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.jobs.create          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      jobs.                      createGlobalQuery          </code></li>
<li><code dir="ltr" translate="no">           bigquery.jobs.delete          </code></li>
<li><code dir="ltr" translate="no">           bigquery.jobs.get          </code></li>
<li><code dir="ltr" translate="no">           bigquery.jobs.list          </code></li>
<li><code dir="ltr" translate="no">           bigquery.jobs.listAll          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      jobs.                      listExecutionMetadata          </code></li>
<li><code dir="ltr" translate="no">           bigquery.jobs.update          </code></li>
</ul>
<p><code dir="ltr" translate="no">           bigquery.models.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.models.create          </code></li>
<li><code dir="ltr" translate="no">           bigquery.models.delete          </code></li>
<li><code dir="ltr" translate="no">           bigquery.models.export          </code></li>
<li><code dir="ltr" translate="no">           bigquery.models.getData          </code></li>
<li><code dir="ltr" translate="no">           bigquery.models.getMetadata          </code></li>
<li><code dir="ltr" translate="no">           bigquery.models.list          </code></li>
<li><code dir="ltr" translate="no">           bigquery.models.updateData          </code></li>
<li><code dir="ltr" translate="no">           bigquery.models.updateMetadata          </code></li>
<li><code dir="ltr" translate="no">           bigquery.models.updateTag          </code></li>
</ul>
<p><code dir="ltr" translate="no">           bigquery.objectRefs.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.objectRefs.read          </code></li>
<li><code dir="ltr" translate="no">           bigquery.objectRefs.write          </code></li>
</ul>
<p><code dir="ltr" translate="no">           bigquery.readsessions.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.readsessions.create          </code></li>
<li><code dir="ltr" translate="no">           bigquery.readsessions.getData          </code></li>
<li><code dir="ltr" translate="no">           bigquery.readsessions.update          </code></li>
</ul>
<p><code dir="ltr" translate="no">           bigquery.                      reservationAssignments.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.                      reservationAssignments.                      create          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      reservationAssignments.                      delete          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      reservationAssignments.                      list          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      reservationAssignments.                      search          </code></li>
</ul>
<p><code dir="ltr" translate="no">           bigquery.reservationGroups.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.                      reservationGroups.                      create          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      reservationGroups.                      delete          </code></li>
<li><code dir="ltr" translate="no">           bigquery.reservationGroups.get          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      reservationGroups.                      list          </code></li>
</ul>
<p><code dir="ltr" translate="no">           bigquery.reservations.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.reservations.create          </code></li>
<li><code dir="ltr" translate="no">           bigquery.reservations.delete          </code></li>
<li><code dir="ltr" translate="no">           bigquery.reservations.get          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      reservations.                      getIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           bigquery.reservations.list          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      reservations.                      listFailoverDatasets          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      reservations.                      setIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           bigquery.reservations.update          </code></li>
<li><code dir="ltr" translate="no">           bigquery.reservations.use          </code></li>
</ul>
<p><code dir="ltr" translate="no">           bigquery.routines.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.routines.create          </code></li>
<li><code dir="ltr" translate="no">           bigquery.routines.delete          </code></li>
<li><code dir="ltr" translate="no">           bigquery.routines.get          </code></li>
<li><code dir="ltr" translate="no">           bigquery.routines.list          </code></li>
<li><code dir="ltr" translate="no">           bigquery.routines.update          </code></li>
<li><code dir="ltr" translate="no">           bigquery.routines.updateTag          </code></li>
</ul>
<p><code dir="ltr" translate="no">         bigquery.                  rowAccessPolicies.                  create        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  rowAccessPolicies.                  delete        </code></p>
<p><code dir="ltr" translate="no">         bigquery.rowAccessPolicies.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  rowAccessPolicies.                  getIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  rowAccessPolicies.                  list        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  rowAccessPolicies.                  overrideTimeTravelRestrictions        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  rowAccessPolicies.                  setIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  rowAccessPolicies.                  update        </code></p>
<p><code dir="ltr" translate="no">           bigquery.savedqueries.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.savedqueries.create          </code></li>
<li><code dir="ltr" translate="no">           bigquery.savedqueries.delete          </code></li>
<li><code dir="ltr" translate="no">           bigquery.savedqueries.get          </code></li>
<li><code dir="ltr" translate="no">           bigquery.savedqueries.list          </code></li>
<li><code dir="ltr" translate="no">           bigquery.savedqueries.update          </code></li>
</ul>
<p><code dir="ltr" translate="no">           bigquery.tables.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.tables.create          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.createIndex          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.createSnapshot          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      tables.                      createTagBinding          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.delete          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.deleteIndex          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.deleteSnapshot          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      tables.                      deleteTagBinding          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.export          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.get          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.getData          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.getIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.list          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      tables.                      listEffectiveTags          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      tables.                      listTagBindings          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.replicateData          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      tables.                      restoreSnapshot          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.setCategory          </code></li>
<li><code dir="ltr" translate="no">           bigquery.                      tables.                      setColumnDataPolicy          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.setIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.update          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.updateData          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.updateIndex          </code></li>
<li><code dir="ltr" translate="no">           bigquery.tables.updateTag          </code></li>
</ul>
<p><code dir="ltr" translate="no">           bigquery.transfers.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.transfers.get          </code></li>
<li><code dir="ltr" translate="no">           bigquery.transfers.update          </code></li>
</ul>
<p><code dir="ltr" translate="no">         bigquerymigration.                  translation.                  translate        </code></p>
<p><code dir="ltr" translate="no">           cloudaicompanion.                      aiDevToolsSettings.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      aiDevToolsSettings.                      create          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      aiDevToolsSettings.                      delete          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      aiDevToolsSettings.                      get          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      aiDevToolsSettings.                      list          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      aiDevToolsSettings.                      update          </code></li>
</ul>
<p><code dir="ltr" translate="no">           cloudaicompanion.                      codeToolsSettings.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      codeToolsSettings.                      create          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      codeToolsSettings.                      delete          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      codeToolsSettings.                      get          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      codeToolsSettings.                      list          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      codeToolsSettings.                      update          </code></li>
</ul>
<p><code dir="ltr" translate="no">           cloudaicompanion.companions.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      companions.                      generateChat          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      companions.                      generateCode          </code></li>
</ul>
<p><code dir="ltr" translate="no">           cloudaicompanion.                      dataSharingWithGoogleSettings.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      dataSharingWithGoogleSettings.                      create          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      dataSharingWithGoogleSettings.                      delete          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      dataSharingWithGoogleSettings.                      get          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      dataSharingWithGoogleSettings.                      list          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      dataSharingWithGoogleSettings.                      update          </code></li>
</ul>
<p><code dir="ltr" translate="no">         cloudaicompanion.                  entitlements.                  get        </code></p>
<p><code dir="ltr" translate="no">           cloudaicompanion.                      geminiGcpEnablementSettings.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      geminiGcpEnablementSettings.                      create          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      geminiGcpEnablementSettings.                      delete          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      geminiGcpEnablementSettings.                      get          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      geminiGcpEnablementSettings.                      list          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      geminiGcpEnablementSettings.                      update          </code></li>
</ul>
<p><code dir="ltr" translate="no">           cloudaicompanion.instances.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      instances.                      completeCode          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      instances.                      completeTask          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      instances.                      exportMetrics          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      instances.                      generateCode          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      instances.                      generateText          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      instances.                      queryEffectiveSetting          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      instances.                      queryEffectiveSettingBindings          </code></li>
</ul>
<p><code dir="ltr" translate="no">         cloudaicompanion.                  licenses.                  selfAssign        </code></p>
<p><code dir="ltr" translate="no">           cloudaicompanion.                      loggingSettings.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      loggingSettings.                      create          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      loggingSettings.                      delete          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      loggingSettings.                      get          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      loggingSettings.                      list          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      loggingSettings.                      update          </code></li>
</ul>
<p><code dir="ltr" translate="no">         cloudaicompanion.                  operations.                  get        </code></p>
<p><code dir="ltr" translate="no">           cloudaicompanion.                      releaseChannelSettings.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      releaseChannelSettings.                      create          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      releaseChannelSettings.                      delete          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      releaseChannelSettings.                      get          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      releaseChannelSettings.                      list          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      releaseChannelSettings.                      update          </code></li>
</ul>
<p><code dir="ltr" translate="no">           cloudaicompanion.                      settingBindings.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      settingBindings.                      aiDevToolsSettingsCreate          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      settingBindings.                      aiDevToolsSettingsDelete          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      settingBindings.                      aiDevToolsSettingsGet          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      settingBindings.                      aiDevToolsSettingsList          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      settingBindings.                      aiDevToolsSettingsUpdate          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      settingBindings.                      aiDevToolsSettingsUse          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      settingBindings.                      codeToolsSettingsCreate          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      settingBindings.                      codeToolsSettingsDelete          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      settingBindings.                      codeToolsSettingsGet          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      settingBindings.                      codeToolsSettingsList          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      settingBindings.                      codeToolsSettingsUpdate          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      settingBindings.                      codeToolsSettingsUse          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      settingBindings.                      dataSharingWithGoogleSettingsCreate          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      settingBindings.                      dataSharingWithGoogleSettingsDelete          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      settingBindings.                      dataSharingWithGoogleSettingsGet          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      settingBindings.                      dataSharingWithGoogleSettingsList          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      settingBindings.                      dataSharingWithGoogleSettingsUpdate          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      settingBindings.                      dataSharingWithGoogleSettingsUse          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      settingBindings.                      geminiGcpEnablementSettingsCreate          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      settingBindings.                      geminiGcpEnablementSettingsDelete          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      settingBindings.                      geminiGcpEnablementSettingsGet          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      settingBindings.                      geminiGcpEnablementSettingsList          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      settingBindings.                      geminiGcpEnablementSettingsUpdate          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      settingBindings.                      geminiGcpEnablementSettingsUse          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      settingBindings.                      loggingSettingsCreate          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      settingBindings.                      loggingSettingsDelete          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      settingBindings.                      loggingSettingsGet          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      settingBindings.                      loggingSettingsList          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      settingBindings.                      loggingSettingsUpdate          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      settingBindings.                      loggingSettingsUse          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      settingBindings.                      releaseChannelSettingsCreate          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      settingBindings.                      releaseChannelSettingsDelete          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      settingBindings.                      releaseChannelSettingsGet          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      settingBindings.                      releaseChannelSettingsList          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      settingBindings.                      releaseChannelSettingsUpdate          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      settingBindings.                      releaseChannelSettingsUse          </code></li>
</ul>
<p><code dir="ltr" translate="no">         cloudaicompanion.topics.create        </code></p>
<p><code dir="ltr" translate="no">           cloudkms.keyHandles.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           cloudkms.keyHandles.create          </code></li>
<li><code dir="ltr" translate="no">           cloudkms.keyHandles.get          </code></li>
<li><code dir="ltr" translate="no">           cloudkms.keyHandles.list          </code></li>
</ul>
<p><code dir="ltr" translate="no">         cloudkms.operations.get        </code></p>
<p><code dir="ltr" translate="no">         cloudkms.                  projects.                  showEffectiveAutokeyConfig        </code></p>
<p><code dir="ltr" translate="no">         compute.projects.get        </code></p>
<p><code dir="ltr" translate="no">           compute.regions.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           compute.regions.get          </code></li>
<li><code dir="ltr" translate="no">           compute.regions.list          </code></li>
</ul>
<p><code dir="ltr" translate="no">         compute.reservations.get        </code></p>
<p><code dir="ltr" translate="no">         compute.reservations.list        </code></p>
<p><code dir="ltr" translate="no">           compute.zones.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           compute.zones.get          </code></li>
<li><code dir="ltr" translate="no">           compute.zones.list          </code></li>
</ul>
<p><code dir="ltr" translate="no">           dataform.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           dataform.commentThreads.create          </code></li>
<li><code dir="ltr" translate="no">           dataform.commentThreads.delete          </code></li>
<li><code dir="ltr" translate="no">           dataform.commentThreads.get          </code></li>
<li><code dir="ltr" translate="no">           dataform.commentThreads.list          </code></li>
<li><code dir="ltr" translate="no">           dataform.commentThreads.update          </code></li>
<li><code dir="ltr" translate="no">           dataform.comments.create          </code></li>
<li><code dir="ltr" translate="no">           dataform.comments.delete          </code></li>
<li><code dir="ltr" translate="no">           dataform.comments.get          </code></li>
<li><code dir="ltr" translate="no">           dataform.comments.list          </code></li>
<li><code dir="ltr" translate="no">           dataform.comments.update          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      compilationResults.                      create          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      compilationResults.                      get          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      compilationResults.                      list          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      compilationResults.                      query          </code></li>
<li><code dir="ltr" translate="no">           dataform.config.get          </code></li>
<li><code dir="ltr" translate="no">           dataform.config.update          </code></li>
<li><code dir="ltr" translate="no">           dataform.folders.addContents          </code></li>
<li><code dir="ltr" translate="no">           dataform.folders.create          </code></li>
<li><code dir="ltr" translate="no">           dataform.folders.delete          </code></li>
<li><code dir="ltr" translate="no">           dataform.folders.get          </code></li>
<li><code dir="ltr" translate="no">           dataform.folders.getIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           dataform.folders.move          </code></li>
<li><code dir="ltr" translate="no">           dataform.folders.queryContents          </code></li>
<li><code dir="ltr" translate="no">           dataform.folders.setIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           dataform.folders.update          </code></li>
<li><code dir="ltr" translate="no">           dataform.locations.get          </code></li>
<li><code dir="ltr" translate="no">           dataform.locations.list          </code></li>
<li><code dir="ltr" translate="no">           dataform.operations.cancel          </code></li>
<li><code dir="ltr" translate="no">           dataform.operations.delete          </code></li>
<li><code dir="ltr" translate="no">           dataform.operations.get          </code></li>
<li><code dir="ltr" translate="no">           dataform.operations.list          </code></li>
<li><code dir="ltr" translate="no">           dataform.releaseConfigs.create          </code></li>
<li><code dir="ltr" translate="no">           dataform.releaseConfigs.delete          </code></li>
<li><code dir="ltr" translate="no">           dataform.releaseConfigs.get          </code></li>
<li><code dir="ltr" translate="no">           dataform.releaseConfigs.list          </code></li>
<li><code dir="ltr" translate="no">           dataform.releaseConfigs.update          </code></li>
<li><code dir="ltr" translate="no">           dataform.repositories.commit          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      repositories.                      computeAccessTokenStatus          </code></li>
<li><code dir="ltr" translate="no">           dataform.repositories.create          </code></li>
<li><code dir="ltr" translate="no">           dataform.repositories.delete          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      repositories.                      fetchHistory          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      repositories.                      fetchRemoteBranches          </code></li>
<li><code dir="ltr" translate="no">           dataform.repositories.get          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      repositories.                      getIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           dataform.repositories.list          </code></li>
<li><code dir="ltr" translate="no">           dataform.repositories.move          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      repositories.                      queryDirectoryContents          </code></li>
<li><code dir="ltr" translate="no">           dataform.repositories.readFile          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      repositories.                      scheduleRelease          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      repositories.                      scheduleWorkflow          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      repositories.                      setIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           dataform.repositories.update          </code></li>
<li><code dir="ltr" translate="no">           dataform.teamFolders.create          </code></li>
<li><code dir="ltr" translate="no">           dataform.teamFolders.delete          </code></li>
<li><code dir="ltr" translate="no">           dataform.teamFolders.get          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      teamFolders.                      getIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      teamFolders.                      setIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           dataform.teamFolders.update          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      workflowConfigs.                      create          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      workflowConfigs.                      delete          </code></li>
<li><code dir="ltr" translate="no">           dataform.workflowConfigs.get          </code></li>
<li><code dir="ltr" translate="no">           dataform.workflowConfigs.list          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      workflowConfigs.                      update          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      workflowInvocations.                      cancel          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      workflowInvocations.                      create          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      workflowInvocations.                      delete          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      workflowInvocations.                      get          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      workflowInvocations.                      list          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      workflowInvocations.                      query          </code></li>
<li><code dir="ltr" translate="no">           dataform.workspaces.commit          </code></li>
<li><code dir="ltr" translate="no">           dataform.workspaces.create          </code></li>
<li><code dir="ltr" translate="no">           dataform.workspaces.delete          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      workspaces.                      fetchFileDiff          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      workspaces.                      fetchFileGitStatuses          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      workspaces.                      fetchGitAheadBehind          </code></li>
<li><code dir="ltr" translate="no">           dataform.workspaces.get          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      workspaces.                      getIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      workspaces.                      installNpmPackages          </code></li>
<li><code dir="ltr" translate="no">           dataform.workspaces.list          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      workspaces.                      makeDirectory          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      workspaces.                      moveDirectory          </code></li>
<li><code dir="ltr" translate="no">           dataform.workspaces.moveFile          </code></li>
<li><code dir="ltr" translate="no">           dataform.workspaces.pull          </code></li>
<li><code dir="ltr" translate="no">           dataform.workspaces.push          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      workspaces.                      queryDirectoryContents          </code></li>
<li><code dir="ltr" translate="no">           dataform.workspaces.readFile          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      workspaces.                      removeDirectory          </code></li>
<li><code dir="ltr" translate="no">           dataform.workspaces.removeFile          </code></li>
<li><code dir="ltr" translate="no">           dataform.workspaces.reset          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      workspaces.                      searchFiles          </code></li>
<li><code dir="ltr" translate="no">           dataform.                      workspaces.                      setIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           dataform.workspaces.writeFile          </code></li>
</ul>
<p><code dir="ltr" translate="no">           dataplex.datascans.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           dataplex.datascans.create          </code></li>
<li><code dir="ltr" translate="no">           dataplex.datascans.delete          </code></li>
<li><code dir="ltr" translate="no">           dataplex.datascans.get          </code></li>
<li><code dir="ltr" translate="no">           dataplex.datascans.getData          </code></li>
<li><code dir="ltr" translate="no">           dataplex.                      datascans.                      getIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           dataplex.datascans.list          </code></li>
<li><code dir="ltr" translate="no">           dataplex.datascans.run          </code></li>
<li><code dir="ltr" translate="no">           dataplex.                      datascans.                      setIamPolicy          </code></li>
<li><code dir="ltr" translate="no">           dataplex.datascans.update          </code></li>
</ul>
<p><code dir="ltr" translate="no">         dataplex.operations.get        </code></p>
<p><code dir="ltr" translate="no">         dataplex.operations.list        </code></p>
<p><code dir="ltr" translate="no">         dataplex.projects.search        </code></p>
<p><code dir="ltr" translate="no">           dataproc.batches.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           dataproc.batches.analyze          </code></li>
<li><code dir="ltr" translate="no">           dataproc.batches.cancel          </code></li>
<li><code dir="ltr" translate="no">           dataproc.batches.create          </code></li>
<li><code dir="ltr" translate="no">           dataproc.batches.delete          </code></li>
<li><code dir="ltr" translate="no">           dataproc.batches.get          </code></li>
<li><code dir="ltr" translate="no">           dataproc.batches.list          </code></li>
<li><code dir="ltr" translate="no">           dataproc.                      batches.                      sparkApplicationRead          </code></li>
<li><code dir="ltr" translate="no">           dataproc.                      batches.                      sparkApplicationWrite          </code></li>
</ul>
<p><code dir="ltr" translate="no">         dataproc.operations.cancel        </code></p>
<p><code dir="ltr" translate="no">         dataproc.operations.delete        </code></p>
<p><code dir="ltr" translate="no">         dataproc.operations.get        </code></p>
<p><code dir="ltr" translate="no">         dataproc.operations.list        </code></p>
<p><code dir="ltr" translate="no">           dataproc.sessionTemplates.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           dataproc.                      sessionTemplates.                      create          </code></li>
<li><code dir="ltr" translate="no">           dataproc.                      sessionTemplates.                      delete          </code></li>
<li><code dir="ltr" translate="no">           dataproc.sessionTemplates.get          </code></li>
<li><code dir="ltr" translate="no">           dataproc.sessionTemplates.list          </code></li>
<li><code dir="ltr" translate="no">           dataproc.                      sessionTemplates.                      update          </code></li>
</ul>
<p><code dir="ltr" translate="no">           dataproc.sessions.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           dataproc.sessions.create          </code></li>
<li><code dir="ltr" translate="no">           dataproc.sessions.delete          </code></li>
<li><code dir="ltr" translate="no">           dataproc.sessions.get          </code></li>
<li><code dir="ltr" translate="no">           dataproc.sessions.list          </code></li>
<li><code dir="ltr" translate="no">           dataproc.                      sessions.                      sparkApplicationRead          </code></li>
<li><code dir="ltr" translate="no">           dataproc.                      sessions.                      sparkApplicationWrite          </code></li>
<li><code dir="ltr" translate="no">           dataproc.sessions.terminate          </code></li>
</ul>
<p><code dir="ltr" translate="no">           dataprocrm.nodePools.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           dataprocrm.nodePools.create          </code></li>
<li><code dir="ltr" translate="no">           dataprocrm.nodePools.delete          </code></li>
<li><code dir="ltr" translate="no">           dataprocrm.                      nodePools.                      deleteNodes          </code></li>
<li><code dir="ltr" translate="no">           dataprocrm.nodePools.get          </code></li>
<li><code dir="ltr" translate="no">           dataprocrm.nodePools.list          </code></li>
<li><code dir="ltr" translate="no">           dataprocrm.nodePools.resize          </code></li>
</ul>
<p><code dir="ltr" translate="no">         dataprocrm.nodes.get        </code></p>
<p><code dir="ltr" translate="no">         dataprocrm.nodes.heartbeat        </code></p>
<p><code dir="ltr" translate="no">         dataprocrm.nodes.list        </code></p>
<p><code dir="ltr" translate="no">         dataprocrm.nodes.update        </code></p>
<p><code dir="ltr" translate="no">         dataprocrm.operations.get        </code></p>
<p><code dir="ltr" translate="no">         dataprocrm.operations.list        </code></p>
<p><code dir="ltr" translate="no">           dataprocrm.workloads.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           dataprocrm.workloads.cancel          </code></li>
<li><code dir="ltr" translate="no">           dataprocrm.workloads.create          </code></li>
<li><code dir="ltr" translate="no">           dataprocrm.workloads.delete          </code></li>
<li><code dir="ltr" translate="no">           dataprocrm.workloads.get          </code></li>
<li><code dir="ltr" translate="no">           dataprocrm.workloads.list          </code></li>
</ul>
<p><code dir="ltr" translate="no">         resourcemanager.projects.get        </code></p>
<p><code dir="ltr" translate="no">         resourcemanager.projects.list        </code></p></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.studioUser" class="role-title add-link" data-text="BigQuery Studio User" tabindex="-1">BigQuery Studio User</h4>
<p>( <code dir="ltr" translate="no">         roles/                  bigquery.studioUser        </code> )</p>
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
<td><p><code dir="ltr" translate="no">         aiplatform.locations.get        </code></p>
<p><code dir="ltr" translate="no">         aiplatform.                  notebookRuntimeTemplates.                  apply        </code></p>
<p><code dir="ltr" translate="no">         aiplatform.                  notebookRuntimeTemplates.                  get        </code></p>
<p><code dir="ltr" translate="no">         aiplatform.                  notebookRuntimeTemplates.                  getIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         aiplatform.                  notebookRuntimeTemplates.                  list        </code></p>
<p><code dir="ltr" translate="no">         aiplatform.                  notebookRuntimes.                  assign        </code></p>
<p><code dir="ltr" translate="no">         aiplatform.                  notebookRuntimes.                  get        </code></p>
<p><code dir="ltr" translate="no">         aiplatform.                  notebookRuntimes.                  list        </code></p>
<p><code dir="ltr" translate="no">         aiplatform.operations.list        </code></p>
<p><code dir="ltr" translate="no">         bigquery.config.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.jobs.create        </code></p>
<p><code dir="ltr" translate="no">           bigquery.readsessions.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.readsessions.create          </code></li>
<li><code dir="ltr" translate="no">           bigquery.readsessions.getData          </code></li>
<li><code dir="ltr" translate="no">           bigquery.readsessions.update          </code></li>
</ul>
<p><code dir="ltr" translate="no">           cloudaicompanion.companions.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      companions.                      generateChat          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      companions.                      generateCode          </code></li>
</ul>
<p><code dir="ltr" translate="no">         cloudaicompanion.                  entitlements.                  get        </code></p>
<p><code dir="ltr" translate="no">           cloudaicompanion.instances.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      instances.                      completeCode          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      instances.                      completeTask          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      instances.                      exportMetrics          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      instances.                      generateCode          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      instances.                      generateText          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      instances.                      queryEffectiveSetting          </code></li>
<li><code dir="ltr" translate="no">           cloudaicompanion.                      instances.                      queryEffectiveSettingBindings          </code></li>
</ul>
<p><code dir="ltr" translate="no">         cloudaicompanion.                  licenses.                  selfAssign        </code></p>
<p><code dir="ltr" translate="no">         cloudaicompanion.                  operations.                  get        </code></p>
<p><code dir="ltr" translate="no">         cloudaicompanion.topics.create        </code></p>
<p><code dir="ltr" translate="no">           cloudkms.keyHandles.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           cloudkms.keyHandles.create          </code></li>
<li><code dir="ltr" translate="no">           cloudkms.keyHandles.get          </code></li>
<li><code dir="ltr" translate="no">           cloudkms.keyHandles.list          </code></li>
</ul>
<p><code dir="ltr" translate="no">         cloudkms.operations.get        </code></p>
<p><code dir="ltr" translate="no">         cloudkms.                  projects.                  showEffectiveAutokeyConfig        </code></p>
<p><code dir="ltr" translate="no">         compute.projects.get        </code></p>
<p><code dir="ltr" translate="no">           compute.regions.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           compute.regions.get          </code></li>
<li><code dir="ltr" translate="no">           compute.regions.list          </code></li>
</ul>
<p><code dir="ltr" translate="no">           compute.zones.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           compute.zones.get          </code></li>
<li><code dir="ltr" translate="no">           compute.zones.list          </code></li>
</ul>
<p><code dir="ltr" translate="no">         dataform.commentThreads.get        </code></p>
<p><code dir="ltr" translate="no">         dataform.commentThreads.list        </code></p>
<p><code dir="ltr" translate="no">         dataform.comments.get        </code></p>
<p><code dir="ltr" translate="no">         dataform.comments.list        </code></p>
<p><code dir="ltr" translate="no">         dataform.folders.create        </code></p>
<p><code dir="ltr" translate="no">           dataform.locations.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           dataform.locations.get          </code></li>
<li><code dir="ltr" translate="no">           dataform.locations.list          </code></li>
</ul>
<p><code dir="ltr" translate="no">         dataform.repositories.create        </code></p>
<p><code dir="ltr" translate="no">         dataform.repositories.list        </code></p>
<p><code dir="ltr" translate="no">         dataplex.projects.search        </code></p>
<p><code dir="ltr" translate="no">           dataproc.batches.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           dataproc.batches.analyze          </code></li>
<li><code dir="ltr" translate="no">           dataproc.batches.cancel          </code></li>
<li><code dir="ltr" translate="no">           dataproc.batches.create          </code></li>
<li><code dir="ltr" translate="no">           dataproc.batches.delete          </code></li>
<li><code dir="ltr" translate="no">           dataproc.batches.get          </code></li>
<li><code dir="ltr" translate="no">           dataproc.batches.list          </code></li>
<li><code dir="ltr" translate="no">           dataproc.                      batches.                      sparkApplicationRead          </code></li>
<li><code dir="ltr" translate="no">           dataproc.                      batches.                      sparkApplicationWrite          </code></li>
</ul>
<p><code dir="ltr" translate="no">         dataproc.operations.cancel        </code></p>
<p><code dir="ltr" translate="no">         dataproc.operations.delete        </code></p>
<p><code dir="ltr" translate="no">         dataproc.operations.get        </code></p>
<p><code dir="ltr" translate="no">         dataproc.operations.list        </code></p>
<p><code dir="ltr" translate="no">           dataproc.sessionTemplates.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           dataproc.                      sessionTemplates.                      create          </code></li>
<li><code dir="ltr" translate="no">           dataproc.                      sessionTemplates.                      delete          </code></li>
<li><code dir="ltr" translate="no">           dataproc.sessionTemplates.get          </code></li>
<li><code dir="ltr" translate="no">           dataproc.sessionTemplates.list          </code></li>
<li><code dir="ltr" translate="no">           dataproc.                      sessionTemplates.                      update          </code></li>
</ul>
<p><code dir="ltr" translate="no">           dataproc.sessions.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           dataproc.sessions.create          </code></li>
<li><code dir="ltr" translate="no">           dataproc.sessions.delete          </code></li>
<li><code dir="ltr" translate="no">           dataproc.sessions.get          </code></li>
<li><code dir="ltr" translate="no">           dataproc.sessions.list          </code></li>
<li><code dir="ltr" translate="no">           dataproc.                      sessions.                      sparkApplicationRead          </code></li>
<li><code dir="ltr" translate="no">           dataproc.                      sessions.                      sparkApplicationWrite          </code></li>
<li><code dir="ltr" translate="no">           dataproc.sessions.terminate          </code></li>
</ul>
<p><code dir="ltr" translate="no">           dataprocrm.nodePools.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           dataprocrm.nodePools.create          </code></li>
<li><code dir="ltr" translate="no">           dataprocrm.nodePools.delete          </code></li>
<li><code dir="ltr" translate="no">           dataprocrm.                      nodePools.                      deleteNodes          </code></li>
<li><code dir="ltr" translate="no">           dataprocrm.nodePools.get          </code></li>
<li><code dir="ltr" translate="no">           dataprocrm.nodePools.list          </code></li>
<li><code dir="ltr" translate="no">           dataprocrm.nodePools.resize          </code></li>
</ul>
<p><code dir="ltr" translate="no">         dataprocrm.nodes.get        </code></p>
<p><code dir="ltr" translate="no">         dataprocrm.nodes.heartbeat        </code></p>
<p><code dir="ltr" translate="no">         dataprocrm.nodes.list        </code></p>
<p><code dir="ltr" translate="no">         dataprocrm.nodes.update        </code></p>
<p><code dir="ltr" translate="no">         dataprocrm.operations.get        </code></p>
<p><code dir="ltr" translate="no">         dataprocrm.operations.list        </code></p>
<p><code dir="ltr" translate="no">           dataprocrm.workloads.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           dataprocrm.workloads.cancel          </code></li>
<li><code dir="ltr" translate="no">           dataprocrm.workloads.create          </code></li>
<li><code dir="ltr" translate="no">           dataprocrm.workloads.delete          </code></li>
<li><code dir="ltr" translate="no">           dataprocrm.workloads.get          </code></li>
<li><code dir="ltr" translate="no">           dataprocrm.workloads.list          </code></li>
</ul>
<p><code dir="ltr" translate="no">         resourcemanager.projects.get        </code></p>
<p><code dir="ltr" translate="no">         resourcemanager.projects.list        </code></p></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.user" class="role-title add-link" data-text="BigQuery User" tabindex="-1">BigQuery User</h4>
<p>( <code dir="ltr" translate="no">         roles/                  bigquery.user        </code> )</p>
<p>When granted on a dataset, this role provides the ability to read the dataset's metadata and list tables in the dataset.</p>
<p>When granted on a project, this role also provides the ability to run jobs, including queries, within the project. A principal with this role can enumerate their own jobs, cancel their own jobs, and enumerate datasets within a project. Additionally, allows the creation of new datasets within the project; the creator is granted the BigQuery Data Owner role ( <code dir="ltr" translate="no">          roles/bigquery.dataOwner         </code> ) on these new datasets.</p>
<p>Lowest-level resources where you can grant this role:</p>
Dataset
These resources within a dataset:
<ul>
<li>Routine</li>
</ul>
<p>This role can also be granted on Resource Manager resources (projects, folders, and organizations).</p></td>
<td><p><code dir="ltr" translate="no">         bigquery.bireservations.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  capacityCommitments.                  get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  capacityCommitments.                  list        </code></p>
<p><code dir="ltr" translate="no">         bigquery.config.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.datasets.create        </code></p>
<p><code dir="ltr" translate="no">         bigquery.datasets.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.datasets.getIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         bigquery.jobs.create        </code></p>
<p><code dir="ltr" translate="no">         bigquery.jobs.list        </code></p>
<p><code dir="ltr" translate="no">         bigquery.models.list        </code></p>
<p><code dir="ltr" translate="no">           bigquery.readsessions.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquery.readsessions.create          </code></li>
<li><code dir="ltr" translate="no">           bigquery.readsessions.getData          </code></li>
<li><code dir="ltr" translate="no">           bigquery.readsessions.update          </code></li>
</ul>
<p><code dir="ltr" translate="no">         bigquery.                  reservationAssignments.                  list        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  reservationAssignments.                  search        </code></p>
<p><code dir="ltr" translate="no">         bigquery.reservationGroups.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  reservationGroups.                  list        </code></p>
<p><code dir="ltr" translate="no">         bigquery.reservations.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.reservations.list        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  reservations.                  listFailoverDatasets        </code></p>
<p><code dir="ltr" translate="no">         bigquery.reservations.use        </code></p>
<p><code dir="ltr" translate="no">         bigquery.routines.list        </code></p>
<p><code dir="ltr" translate="no">         bigquery.savedqueries.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.savedqueries.list        </code></p>
<p><code dir="ltr" translate="no">         bigquery.tables.list        </code></p>
<p><code dir="ltr" translate="no">         bigquery.transfers.get        </code></p>
<p><code dir="ltr" translate="no">         bigquerymigration.                  translation.                  translate        </code></p>
<p><code dir="ltr" translate="no">           cloudkms.keyHandles.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           cloudkms.keyHandles.create          </code></li>
<li><code dir="ltr" translate="no">           cloudkms.keyHandles.get          </code></li>
<li><code dir="ltr" translate="no">           cloudkms.keyHandles.list          </code></li>
</ul>
<p><code dir="ltr" translate="no">         cloudkms.operations.get        </code></p>
<p><code dir="ltr" translate="no">         cloudkms.                  projects.                  showEffectiveAutokeyConfig        </code></p>
<p><code dir="ltr" translate="no">         dataform.folders.create        </code></p>
<p><code dir="ltr" translate="no">           dataform.locations.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           dataform.locations.get          </code></li>
<li><code dir="ltr" translate="no">           dataform.locations.list          </code></li>
</ul>
<p><code dir="ltr" translate="no">         dataform.repositories.create        </code></p>
<p><code dir="ltr" translate="no">         dataform.repositories.list        </code></p>
<p><code dir="ltr" translate="no">         dataplex.projects.search        </code></p>
<p><code dir="ltr" translate="no">         resourcemanager.projects.get        </code></p>
<p><code dir="ltr" translate="no">         resourcemanager.projects.list        </code></p></td>
</tr>
</tbody>
</table>

### BigQuery Connection API roles

This table lists the predefined IAM roles and permissions for BigQuery Connection API. To search through all roles and permissions, see the [role and permission index](/iam/docs/roles-permissions) .

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
<td><h4 id="bigqueryconnection.serviceAgent" class="role-title add-link" data-text="BigQuery Connection Service Agent" tabindex="-1">BigQuery Connection Service Agent</h4>
<p>( <code dir="ltr" translate="no">        roles/                bigqueryconnection.serviceAgent       </code> )</p>
<p>Gives BigQuery Connection Service access to Cloud SQL instances in user projects.</p>
<strong>Warning:</strong> Do not grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .</td>
<td><p><code dir="ltr" translate="no">        cloudsql.instances.connect       </code></p>
<p><code dir="ltr" translate="no">        cloudsql.instances.get       </code></p>
<p><code dir="ltr" translate="no">        logging.logEntries.create       </code></p>
<p><code dir="ltr" translate="no">        logging.logEntries.route       </code></p>
<p><code dir="ltr" translate="no">        monitoring.                metricDescriptors.                create       </code></p>
<p><code dir="ltr" translate="no">        monitoring.                metricDescriptors.                get       </code></p>
<p><code dir="ltr" translate="no">        monitoring.                metricDescriptors.                list       </code></p>
<p><code dir="ltr" translate="no">          monitoring.                    monitoredResourceDescriptors.*         </code></p>
<ul>
<li><code dir="ltr" translate="no">          monitoring.                    monitoredResourceDescriptors.                    get         </code></li>
<li><code dir="ltr" translate="no">          monitoring.                    monitoredResourceDescriptors.                    list         </code></li>
</ul>
<p><code dir="ltr" translate="no">        monitoring.timeSeries.create       </code></p>
<p><code dir="ltr" translate="no">        telemetry.metrics.write       </code></p></td>
</tr>
</tbody>
</table>

### BigQuery Continuous Query roles

This table lists the predefined IAM roles and permissions for BigQuery Continuous Query. To search through all roles and permissions, see the [role and permission index](/iam/docs/roles-permissions) .

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
<td><h4 id="bigquerycontinuousquery.serviceAgent" class="role-title add-link" data-text="BigQuery Continuous Query Service Agent" tabindex="-1">BigQuery Continuous Query Service Agent</h4>
<p>( <code dir="ltr" translate="no">        roles/                bigquerycontinuousquery.serviceAgent       </code> )</p>
<p>Gives BigQuery Continuous Query access to the service accounts in the user project.</p>
<strong>Warning:</strong> Do not grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .</td>
<td><p><code dir="ltr" translate="no">        iam.                serviceAccounts.                getAccessToken       </code></p></td>
</tr>
</tbody>
</table>

### BigQuery Data Policy roles

This table lists the predefined IAM roles and permissions for BigQuery Data Policy. To search through all roles and permissions, see the [role and permission index](/iam/docs/roles-permissions) .

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
<td><h4 id="bigquerydatapolicy.admin" class="role-title add-link" data-text="BigQuery Data Policy Admin" tabindex="-1">BigQuery Data Policy Admin</h4>
<p>( <code dir="ltr" translate="no">         roles/                  bigquerydatapolicy.admin        </code> )</p>
<p>Role for managing Data Policies in BigQuery</p>
<p>This role can only be granted on Resource Manager resources (projects, folders, and organizations).</p></td>
<td><p><code dir="ltr" translate="no">         bigquery.dataPolicies.attach        </code></p>
<p><code dir="ltr" translate="no">         bigquery.dataPolicies.create        </code></p>
<p><code dir="ltr" translate="no">         bigquery.dataPolicies.delete        </code></p>
<p><code dir="ltr" translate="no">         bigquery.dataPolicies.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  dataPolicies.                  getIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         bigquery.dataPolicies.list        </code></p>
<p><code dir="ltr" translate="no">         bigquery.                  dataPolicies.                  setIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         bigquery.dataPolicies.update        </code></p></td>
</tr>
<tr class="even">
<td><h4 id="bigquerydatapolicy.maskedReader" class="role-title add-link" data-text="Masked Reader" tabindex="-1">Masked Reader</h4>
<p>( <code dir="ltr" translate="no">         roles/                  bigquerydatapolicy.maskedReader        </code> )</p>
<p>Masked read access to sub-resources tagged by the policy tag associated with a data policy, for example, BigQuery columns</p>
<p>This role can only be granted on Resource Manager resources (projects, folders, and organizations).</p></td>
<td><p><code dir="ltr" translate="no">         bigquery.                  dataPolicies.                  maskedGet        </code></p></td>
</tr>
<tr class="odd">
<td><h4 id="bigquerydatapolicy.rawDataReader" class="role-title add-link" data-text="Raw Data Reader Beta" tabindex="-1">Raw Data Reader <sup>Beta</sup></h4>
<p>( <code dir="ltr" translate="no">         roles/                  bigquerydatapolicy.rawDataReader        </code> )</p>
<p>Raw read access to sub-resources associated with a data policy, for example, BigQuery columns</p>
<p>This role can only be granted on Resource Manager resources (projects, folders, and organizations).</p></td>
<td><p><code dir="ltr" translate="no">         bigquery.                  dataPolicies.                  getRawData        </code></p></td>
</tr>
<tr class="even">
<td><h4 id="bigquerydatapolicy.viewer" class="role-title add-link" data-text="BigQuery Data Policy Viewer" tabindex="-1">BigQuery Data Policy Viewer</h4>
<p>( <code dir="ltr" translate="no">         roles/                  bigquerydatapolicy.viewer        </code> )</p>
<p>Role for viewing Data Policies in BigQuery</p>
<p>This role can only be granted on Resource Manager resources (projects, folders, and organizations).</p></td>
<td><p><code dir="ltr" translate="no">         bigquery.dataPolicies.get        </code></p>
<p><code dir="ltr" translate="no">         bigquery.dataPolicies.list        </code></p></td>
</tr>
</tbody>
</table>

### BigQuery Data Transfer Service roles

This table lists the predefined IAM roles and permissions for BigQuery Data Transfer Service. To search through all roles and permissions, see the [role and permission index](/iam/docs/roles-permissions) .

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
<td><h4 id="bigquerydatatransfer.serviceAgent" class="role-title add-link" data-text="BigQuery Data Transfer Service Agent" tabindex="-1">BigQuery Data Transfer Service Agent</h4>
<p>( <code dir="ltr" translate="no">        roles/                bigquerydatatransfer.serviceAgent       </code> )</p>
<p>Gives BigQuery Data Transfer Service access to start BigQuery jobs in consumer project.</p>
<strong>Warning:</strong> Do not grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .</td>
<td><p><code dir="ltr" translate="no">        bigquery.config.get       </code></p>
<p><code dir="ltr" translate="no">        bigquery.connections.delegate       </code></p>
<p><code dir="ltr" translate="no">        bigquery.jobs.create       </code></p>
<p><code dir="ltr" translate="no">        compute.networkAttachments.get       </code></p>
<p><code dir="ltr" translate="no">        compute.                networkAttachments.                update       </code></p>
<p><code dir="ltr" translate="no">        compute.regionOperations.get       </code></p>
<p><code dir="ltr" translate="no">        compute.subnetworks.use       </code></p>
<p><code dir="ltr" translate="no">        dataform.folders.create       </code></p>
<p><code dir="ltr" translate="no">          dataform.locations.*         </code></p>
<ul>
<li><code dir="ltr" translate="no">          dataform.locations.get         </code></li>
<li><code dir="ltr" translate="no">          dataform.locations.list         </code></li>
</ul>
<p><code dir="ltr" translate="no">        dataform.repositories.create       </code></p>
<p><code dir="ltr" translate="no">        dataform.repositories.list       </code></p>
<p><code dir="ltr" translate="no">        iam.                serviceAccounts.                getAccessToken       </code></p>
<p><code dir="ltr" translate="no">        logging.logEntries.create       </code></p>
<p><code dir="ltr" translate="no">        logging.logEntries.route       </code></p>
<p><code dir="ltr" translate="no">        resourcemanager.projects.get       </code></p>
<p><code dir="ltr" translate="no">        resourcemanager.projects.list       </code></p>
<p><code dir="ltr" translate="no">        serviceusage.services.use       </code></p></td>
</tr>
</tbody>
</table>

### BigQuery Engine for Apache Flink roles

This table lists the predefined IAM roles and permissions for BigQuery Engine for Apache Flink. To search through all roles and permissions, see the [role and permission index](/iam/docs/roles-permissions) .

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
<td><h4 id="managedflink.admin" class="role-title add-link" data-text="Managed Flink Admin Beta" tabindex="-1">Managed Flink Admin <sup>Beta</sup></h4>
<p>( <code dir="ltr" translate="no">         roles/                  managedflink.admin        </code> )</p>
<p>Full access to Managed Flink resources.</p></td>
<td><p><code dir="ltr" translate="no">           managedflink.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           managedflink.                      deployments.                      create          </code></li>
<li><code dir="ltr" translate="no">           managedflink.                      deployments.                      delete          </code></li>
<li><code dir="ltr" translate="no">           managedflink.deployments.get          </code></li>
<li><code dir="ltr" translate="no">           managedflink.deployments.list          </code></li>
<li><code dir="ltr" translate="no">           managedflink.                      deployments.                      update          </code></li>
<li><code dir="ltr" translate="no">           managedflink.jobs.create          </code></li>
<li><code dir="ltr" translate="no">           managedflink.jobs.delete          </code></li>
<li><code dir="ltr" translate="no">           managedflink.jobs.get          </code></li>
<li><code dir="ltr" translate="no">           managedflink.jobs.list          </code></li>
<li><code dir="ltr" translate="no">           managedflink.jobs.update          </code></li>
<li><code dir="ltr" translate="no">           managedflink.locations.get          </code></li>
<li><code dir="ltr" translate="no">           managedflink.locations.list          </code></li>
<li><code dir="ltr" translate="no">           managedflink.operations.cancel          </code></li>
<li><code dir="ltr" translate="no">           managedflink.operations.delete          </code></li>
<li><code dir="ltr" translate="no">           managedflink.operations.get          </code></li>
<li><code dir="ltr" translate="no">           managedflink.operations.list          </code></li>
<li><code dir="ltr" translate="no">           managedflink.sessions.create          </code></li>
<li><code dir="ltr" translate="no">           managedflink.sessions.delete          </code></li>
<li><code dir="ltr" translate="no">           managedflink.sessions.get          </code></li>
<li><code dir="ltr" translate="no">           managedflink.sessions.list          </code></li>
<li><code dir="ltr" translate="no">           managedflink.sessions.update          </code></li>
</ul>
<p><code dir="ltr" translate="no">         resourcemanager.projects.get        </code></p>
<p><code dir="ltr" translate="no">         resourcemanager.projects.list        </code></p></td>
</tr>
<tr class="even">
<td><h4 id="managedflink.developer" class="role-title add-link" data-text="Managed Flink Developer Beta" tabindex="-1">Managed Flink Developer <sup>Beta</sup></h4>
<p>( <code dir="ltr" translate="no">         roles/                  managedflink.developer        </code> )</p>
<p>Full access to Managed Flink Jobs and Sessions and read access to Deployments.</p></td>
<td><p><code dir="ltr" translate="no">         managedflink.deployments.get        </code></p>
<p><code dir="ltr" translate="no">         managedflink.deployments.list        </code></p>
<p><code dir="ltr" translate="no">           managedflink.jobs.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           managedflink.jobs.create          </code></li>
<li><code dir="ltr" translate="no">           managedflink.jobs.delete          </code></li>
<li><code dir="ltr" translate="no">           managedflink.jobs.get          </code></li>
<li><code dir="ltr" translate="no">           managedflink.jobs.list          </code></li>
<li><code dir="ltr" translate="no">           managedflink.jobs.update          </code></li>
</ul>
<p><code dir="ltr" translate="no">           managedflink.locations.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           managedflink.locations.get          </code></li>
<li><code dir="ltr" translate="no">           managedflink.locations.list          </code></li>
</ul>
<p><code dir="ltr" translate="no">         managedflink.operations.get        </code></p>
<p><code dir="ltr" translate="no">         managedflink.operations.list        </code></p>
<p><code dir="ltr" translate="no">           managedflink.sessions.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           managedflink.sessions.create          </code></li>
<li><code dir="ltr" translate="no">           managedflink.sessions.delete          </code></li>
<li><code dir="ltr" translate="no">           managedflink.sessions.get          </code></li>
<li><code dir="ltr" translate="no">           managedflink.sessions.list          </code></li>
<li><code dir="ltr" translate="no">           managedflink.sessions.update          </code></li>
</ul>
<p><code dir="ltr" translate="no">         resourcemanager.projects.get        </code></p>
<p><code dir="ltr" translate="no">         resourcemanager.projects.list        </code></p></td>
</tr>
<tr class="odd">
<td><h4 id="managedflink.serviceAgent" class="role-title add-link" data-text="Managed Flink Service Agent" tabindex="-1">Managed Flink Service Agent</h4>
<p>( <code dir="ltr" translate="no">         roles/                  managedflink.serviceAgent        </code> )</p>
<p>Gives Managed Flink Service Agent access to Cloud Platform resources.</p>
<strong>Warning:</strong> Do not grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .</td>
<td><p><code dir="ltr" translate="no">         compute.                  networkAttachments.                  create        </code></p>
<p><code dir="ltr" translate="no">         compute.                  networkAttachments.                  delete        </code></p>
<p><code dir="ltr" translate="no">         compute.networkAttachments.get        </code></p>
<p><code dir="ltr" translate="no">         compute.                  networkAttachments.                  list        </code></p>
<p><code dir="ltr" translate="no">         compute.                  networkAttachments.                  update        </code></p>
<p><code dir="ltr" translate="no">         compute.networks.get        </code></p>
<p><code dir="ltr" translate="no">         compute.networks.list        </code></p>
<p><code dir="ltr" translate="no">         compute.regionOperations.get        </code></p>
<p><code dir="ltr" translate="no">         compute.subnetworks.get        </code></p>
<p><code dir="ltr" translate="no">         compute.subnetworks.list        </code></p>
<p><code dir="ltr" translate="no">         compute.subnetworks.use        </code></p>
<p><code dir="ltr" translate="no">         dns.                  networks.                  targetWithPeeringZone        </code></p>
<p><code dir="ltr" translate="no">         managedkafka.clusters.get        </code></p>
<p><code dir="ltr" translate="no">         managedkafka.clusters.list        </code></p>
<p><code dir="ltr" translate="no">         managedkafka.clusters.update        </code></p>
<p><code dir="ltr" translate="no">         monitoring.                  metricDescriptors.                  create        </code></p>
<p><code dir="ltr" translate="no">         monitoring.                  metricDescriptors.                  get        </code></p>
<p><code dir="ltr" translate="no">         monitoring.                  metricDescriptors.                  list        </code></p>
<p><code dir="ltr" translate="no">           monitoring.                      monitoredResourceDescriptors.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           monitoring.                      monitoredResourceDescriptors.                      get          </code></li>
<li><code dir="ltr" translate="no">           monitoring.                      monitoredResourceDescriptors.                      list          </code></li>
</ul>
<p><code dir="ltr" translate="no">         monitoring.timeSeries.create        </code></p>
<p><code dir="ltr" translate="no">         serviceusage.services.use        </code></p>
<p><code dir="ltr" translate="no">         storage.objects.get        </code></p></td>
</tr>
<tr class="even">
<td><h4 id="managedflink.viewer" class="role-title add-link" data-text="Managed Flink Viewer Beta" tabindex="-1">Managed Flink Viewer <sup>Beta</sup></h4>
<p>( <code dir="ltr" translate="no">         roles/                  managedflink.viewer        </code> )</p>
<p>Readonly access to Managed Flink resources.</p></td>
<td><p><code dir="ltr" translate="no">         managedflink.deployments.get        </code></p>
<p><code dir="ltr" translate="no">         managedflink.deployments.list        </code></p>
<p><code dir="ltr" translate="no">         managedflink.jobs.get        </code></p>
<p><code dir="ltr" translate="no">         managedflink.jobs.list        </code></p>
<p><code dir="ltr" translate="no">           managedflink.locations.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           managedflink.locations.get          </code></li>
<li><code dir="ltr" translate="no">           managedflink.locations.list          </code></li>
</ul>
<p><code dir="ltr" translate="no">         managedflink.operations.get        </code></p>
<p><code dir="ltr" translate="no">         managedflink.operations.list        </code></p>
<p><code dir="ltr" translate="no">         managedflink.sessions.get        </code></p>
<p><code dir="ltr" translate="no">         managedflink.sessions.list        </code></p>
<p><code dir="ltr" translate="no">         resourcemanager.projects.get        </code></p>
<p><code dir="ltr" translate="no">         resourcemanager.projects.list        </code></p></td>
</tr>
</tbody>
</table>

### BigQuery Migration Service roles

This table lists the predefined IAM roles and permissions for BigQuery Migration Service. To search through all roles and permissions, see the [role and permission index](/iam/docs/roles-permissions) .

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
<td><h4 id="bigquerymigration.editor" class="role-title add-link" data-text="MigrationWorkflow Editor" tabindex="-1">MigrationWorkflow Editor</h4>
<p>( <code dir="ltr" translate="no">         roles/                  bigquerymigration.editor        </code> )</p>
<p>Editor of EDW migration workflows.</p></td>
<td><p><code dir="ltr" translate="no">           bigquerymigration.subtasks.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquerymigration.subtasks.get          </code></li>
<li><code dir="ltr" translate="no">           bigquerymigration.                      subtasks.                      list          </code></li>
</ul>
<p><code dir="ltr" translate="no">         bigquerymigration.                  workflows.                  create        </code></p>
<p><code dir="ltr" translate="no">         bigquerymigration.                  workflows.                  delete        </code></p>
<p><code dir="ltr" translate="no">         bigquerymigration.                  workflows.                  enableAiOutputTypes        </code></p>
<p><code dir="ltr" translate="no">         bigquerymigration.                  workflows.                  enableLineageOutputTypes        </code></p>
<p><code dir="ltr" translate="no">         bigquerymigration.                  workflows.                  enableOutputTypePermissions        </code></p>
<p><code dir="ltr" translate="no">         bigquerymigration.                  workflows.                  get        </code></p>
<p><code dir="ltr" translate="no">         bigquerymigration.                  workflows.                  list        </code></p>
<p><code dir="ltr" translate="no">         bigquerymigration.                  workflows.                  update        </code></p></td>
</tr>
<tr class="even">
<td><h4 id="bigquerymigration.orchestrator" class="role-title add-link" data-text="Task Orchestrator" tabindex="-1">Task Orchestrator</h4>
<p>( <code dir="ltr" translate="no">         roles/                  bigquerymigration.orchestrator        </code> )</p>
<p>Orchestrator of EDW migration tasks.</p></td>
<td><p><code dir="ltr" translate="no">         bigquerymigration.                  workflows.                  orchestrateTask        </code></p>
<p><code dir="ltr" translate="no">         storage.objects.list        </code></p></td>
</tr>
<tr class="odd">
<td><h4 id="bigquerymigration.translationUser" class="role-title add-link" data-text="Migration Translation User" tabindex="-1">Migration Translation User</h4>
<p>( <code dir="ltr" translate="no">         roles/                  bigquerymigration.translationUser        </code> )</p>
<p>User of EDW migration interactive SQL translation service.</p></td>
<td><p><code dir="ltr" translate="no">         bigquerymigration.                  translation.                  translate        </code></p></td>
</tr>
<tr class="even">
<td><h4 id="bigquerymigration.viewer" class="role-title add-link" data-text="MigrationWorkflow Viewer" tabindex="-1">MigrationWorkflow Viewer</h4>
<p>( <code dir="ltr" translate="no">         roles/                  bigquerymigration.viewer        </code> )</p>
<p>Viewer of EDW migration MigrationWorkflow.</p></td>
<td><p><code dir="ltr" translate="no">           bigquerymigration.subtasks.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           bigquerymigration.subtasks.get          </code></li>
<li><code dir="ltr" translate="no">           bigquerymigration.                      subtasks.                      list          </code></li>
</ul>
<p><code dir="ltr" translate="no">         bigquerymigration.                  workflows.                  get        </code></p>
<p><code dir="ltr" translate="no">         bigquerymigration.                  workflows.                  list        </code></p></td>
</tr>
<tr class="odd">
<td><h4 id="bigquerymigration.worker" class="role-title add-link" data-text="Task Worker" tabindex="-1">Task Worker</h4>
<p>( <code dir="ltr" translate="no">         roles/                  bigquerymigration.worker        </code> )</p>
<p>Worker that executes EDW migration subtasks.</p></td>
<td><p><code dir="ltr" translate="no">         storage.objects.create        </code></p>
<p><code dir="ltr" translate="no">         storage.objects.get        </code></p>
<p><code dir="ltr" translate="no">         storage.objects.list        </code></p></td>
</tr>
</tbody>
</table>

### BigQuery Omni roles

This table lists the predefined IAM roles and permissions for BigQuery Omni. To search through all roles and permissions, see the [role and permission index](/iam/docs/roles-permissions) .

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
<td><h4 id="bigqueryomni.serviceAgent" class="role-title add-link" data-text="BigQuery Omni Service Agent" tabindex="-1">BigQuery Omni Service Agent</h4>
<p>( <code dir="ltr" translate="no">        roles/                bigqueryomni.serviceAgent       </code> )</p>
<p>Gives BigQuery Omni access to tables in user projects.</p>
<strong>Warning:</strong> Do not grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .</td>
<td><p><code dir="ltr" translate="no">        bigquery.jobs.create       </code></p>
<p><code dir="ltr" translate="no">        bigquery.tables.updateData       </code></p></td>
</tr>
</tbody>
</table>

### BigQuery sharing roles

This table lists the predefined IAM roles and permissions for BigQuery sharing. To search through all roles and permissions, see the [role and permission index](/iam/docs/roles-permissions) .

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
<td><h4 id="analyticshub.admin" class="role-title add-link" data-text="Analytics Hub Admin" tabindex="-1">Analytics Hub Admin</h4>
<p>( <code dir="ltr" translate="no">         roles/                  analyticshub.admin        </code> )</p>
<p>Administer Data Exchanges and Listings</p></td>
<td><p><code dir="ltr" translate="no">         analyticshub.                  dataExchanges.                  create        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.                  dataExchanges.                  delete        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.dataExchanges.get        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.                  dataExchanges.                  getIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.                  dataExchanges.                  list        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.                  dataExchanges.                  setIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.                  dataExchanges.                  update        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.                  dataExchanges.                  viewSubscriptions        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.listings.create        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.listings.delete        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.listings.get        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.                  listings.                  getIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.listings.list        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.                  listings.                  setIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.listings.update        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.                  listings.                  viewSubscriptions        </code></p>
<p><code dir="ltr" translate="no">           analyticshub.subscriptions.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           analyticshub.                      subscriptions.                      create          </code></li>
<li><code dir="ltr" translate="no">           analyticshub.                      subscriptions.                      delete          </code></li>
<li><code dir="ltr" translate="no">           analyticshub.subscriptions.get          </code></li>
<li><code dir="ltr" translate="no">           analyticshub.                      subscriptions.                      list          </code></li>
<li><code dir="ltr" translate="no">           analyticshub.                      subscriptions.                      update          </code></li>
</ul>
<p><code dir="ltr" translate="no">         resourcemanager.projects.get        </code></p>
<p><code dir="ltr" translate="no">         resourcemanager.projects.list        </code></p></td>
</tr>
<tr class="even">
<td><h4 id="analyticshub.listingAdmin" class="role-title add-link" data-text="Analytics Hub Listing Admin" tabindex="-1">Analytics Hub Listing Admin</h4>
<p>( <code dir="ltr" translate="no">         roles/                  analyticshub.listingAdmin        </code> )</p>
<p>Grants full control over the Listing, including updating, deleting and setting ACLs</p></td>
<td><p><code dir="ltr" translate="no">         analyticshub.dataExchanges.get        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.                  dataExchanges.                  getIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.                  dataExchanges.                  list        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.listings.delete        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.listings.get        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.                  listings.                  getIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.listings.list        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.                  listings.                  setIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.listings.update        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.                  listings.                  viewSubscriptions        </code></p>
<p><code dir="ltr" translate="no">         resourcemanager.projects.get        </code></p>
<p><code dir="ltr" translate="no">         resourcemanager.projects.list        </code></p></td>
</tr>
<tr class="odd">
<td><h4 id="analyticshub.publisher" class="role-title add-link" data-text="Analytics Hub Publisher" tabindex="-1">Analytics Hub Publisher</h4>
<p>( <code dir="ltr" translate="no">         roles/                  analyticshub.publisher        </code> )</p>
<p>Can publish to Data Exchanges thus creating Listings</p></td>
<td><p><code dir="ltr" translate="no">         analyticshub.dataExchanges.get        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.                  dataExchanges.                  getIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.                  dataExchanges.                  list        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.listings.create        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.listings.get        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.                  listings.                  getIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.listings.list        </code></p>
<p><code dir="ltr" translate="no">         resourcemanager.projects.get        </code></p>
<p><code dir="ltr" translate="no">         resourcemanager.projects.list        </code></p></td>
</tr>
<tr class="even">
<td><h4 id="analyticshub.subscriber" class="role-title add-link" data-text="Analytics Hub Subscriber" tabindex="-1">Analytics Hub Subscriber</h4>
<p>( <code dir="ltr" translate="no">         roles/                  analyticshub.subscriber        </code> )</p>
<p>Can browse Data Exchanges and subscribe to Listings</p></td>
<td><p><code dir="ltr" translate="no">         analyticshub.dataExchanges.get        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.                  dataExchanges.                  getIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.                  dataExchanges.                  list        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.                  dataExchanges.                  subscribe        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.listings.get        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.                  listings.                  getIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.listings.list        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.                  listings.                  subscribe        </code></p>
<p><code dir="ltr" translate="no">         resourcemanager.projects.get        </code></p>
<p><code dir="ltr" translate="no">         resourcemanager.projects.list        </code></p></td>
</tr>
<tr class="odd">
<td><h4 id="analyticshub.subscriptionOwner" class="role-title add-link" data-text="Analytics Hub Subscription Owner" tabindex="-1">Analytics Hub Subscription Owner</h4>
<p>( <code dir="ltr" translate="no">         roles/                  analyticshub.subscriptionOwner        </code> )</p>
<p>Grants full control over the Subscription, including updating and deleting</p></td>
<td><p><code dir="ltr" translate="no">         analyticshub.dataExchanges.get        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.                  dataExchanges.                  getIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.                  dataExchanges.                  list        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.listings.get        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.                  listings.                  getIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.listings.list        </code></p>
<p><code dir="ltr" translate="no">           analyticshub.subscriptions.*          </code></p>
<ul>
<li><code dir="ltr" translate="no">           analyticshub.                      subscriptions.                      create          </code></li>
<li><code dir="ltr" translate="no">           analyticshub.                      subscriptions.                      delete          </code></li>
<li><code dir="ltr" translate="no">           analyticshub.subscriptions.get          </code></li>
<li><code dir="ltr" translate="no">           analyticshub.                      subscriptions.                      list          </code></li>
<li><code dir="ltr" translate="no">           analyticshub.                      subscriptions.                      update          </code></li>
</ul>
<p><code dir="ltr" translate="no">         resourcemanager.projects.get        </code></p>
<p><code dir="ltr" translate="no">         resourcemanager.projects.list        </code></p></td>
</tr>
<tr class="even">
<td><h4 id="analyticshub.viewer" class="role-title add-link" data-text="Analytics Hub Viewer" tabindex="-1">Analytics Hub Viewer</h4>
<p>( <code dir="ltr" translate="no">         roles/                  analyticshub.viewer        </code> )</p>
<p>Can browse Data Exchanges and Listings</p></td>
<td><p><code dir="ltr" translate="no">         analyticshub.dataExchanges.get        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.                  dataExchanges.                  getIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.                  dataExchanges.                  list        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.listings.get        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.                  listings.                  getIamPolicy        </code></p>
<p><code dir="ltr" translate="no">         analyticshub.listings.list        </code></p>
<p><code dir="ltr" translate="no">         resourcemanager.projects.get        </code></p>
<p><code dir="ltr" translate="no">         resourcemanager.projects.list        </code></p></td>
</tr>
</tbody>
</table>

## BigQuery permissions

The following tables list the permissions available in BigQuery. These are included in predefined roles and can be used in custom role definitions. To search through all roles and permissions, see the [role and permission index](/iam/docs/roles-permissions) .

### BigQuery permissions

This table lists the IAM permissions for BigQuery and the roles that include them. To search through all roles and permissions, see the [role and permission index](/iam/docs/roles-permissions) .

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
<td><h4 id="bigquery.bireservations.get" class="permission-name add-link" data-text="bigquery.bireservations.get" tabindex="-1"><code dir="ltr" translate="no">         bigquery.bireservations.get        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceViewer">BigQuery Resource Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.user        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.bireservations.update" class="permission-name add-link" data-text="bigquery.bireservations.update" tabindex="-1"><code dir="ltr" translate="no">         bigquery.bireservations.update        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.capacityCommitments.create" class="permission-name add-link" data-text="bigquery.capacityCommitments.create" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  capacityCommitments.                  create        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.capacityCommitments.delete" class="permission-name add-link" data-text="bigquery.capacityCommitments.delete" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  capacityCommitments.                  delete        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.capacityCommitments.get" class="permission-name add-link" data-text="bigquery.capacityCommitments.get" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  capacityCommitments.                  get        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceViewer">BigQuery Resource Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.user        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.capacityCommitments.list" class="permission-name add-link" data-text="bigquery.capacityCommitments.list" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  capacityCommitments.                  list        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceViewer">BigQuery Resource Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.user        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAuditor">Security Auditor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAuditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityReviewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.capacityCommitments.update" class="permission-name add-link" data-text="bigquery.capacityCommitments.update" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  capacityCommitments.                  update        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.config.get" class="permission-name add-link" data-text="bigquery.config.get" tabindex="-1"><code dir="ltr" translate="no">         bigquery.config.get        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.jobUser">BigQuery Job User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.jobUser        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioUser">BigQuery Studio User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioUser        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.user        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.dataScientist">Data Scientist</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.dataScientist        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/enterpriseknowledgegraph#enterpriseknowledgegraph.serviceAgent">Enterprise Knowledge Graph Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      enterpriseknowledgegraph.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/fleetengine#fleetengine.serviceAgent">FleetEngine Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      fleetengine.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/looker#looker.serviceAgent">Looker Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      looker.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/bigquerydatatransfer#bigquerydatatransfer.serviceAgent">BigQuery Data Transfer Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      bigquerydatatransfer.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.config.update" class="permission-name add-link" data-text="bigquery.config.update" tabindex="-1"><code dir="ltr" translate="no">         bigquery.config.update        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/assuredworkloads#assuredworkloads.admin">Assured Workloads Administrator</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  assuredworkloads.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/assuredworkloads#assuredworkloads.editor">Assured Workloads Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  assuredworkloads.editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.connections.create" class="permission-name add-link" data-text="bigquery.connections.create" tabindex="-1"><code dir="ltr" translate="no">         bigquery.connections.create        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.connectionAdmin">BigQuery Connection Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.connectionAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/chronicle#chronicle.serviceAgent">Chronicle Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      chronicle.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.connections.delegate" class="permission-name add-link" data-text="bigquery.connections.delegate" tabindex="-1"><code dir="ltr" translate="no">         bigquery.connections.delegate        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.connectionAdmin">BigQuery Connection Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.connectionAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/datastream#datastream.bigqueryWriter">Datastream Bigquery Writer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  datastream.bigqueryWriter        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/chronicle#chronicle.serviceAgent">Chronicle Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      chronicle.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.discoveryBigLakePublishingServiceAgent">Dataplex Discovery BigLake Publishing Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.discoveryBigLakePublishingServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datastream#datastream.serviceAgent">Datastream Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datastream.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/bigquerydatatransfer#bigquerydatatransfer.serviceAgent">BigQuery Data Transfer Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      bigquerydatatransfer.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.connections.delete" class="permission-name add-link" data-text="bigquery.connections.delete" tabindex="-1"><code dir="ltr" translate="no">         bigquery.connections.delete        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.connectionAdmin">BigQuery Connection Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.connectionAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/chronicle#chronicle.serviceAgent">Chronicle Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      chronicle.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.connections.get" class="permission-name add-link" data-text="bigquery.connections.get" tabindex="-1"><code dir="ltr" translate="no">         bigquery.connections.get        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.connectionAdmin">BigQuery Connection Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.connectionAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.connectionUser">BigQuery Connection User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.connectionUser        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/datacatalog#datacatalog.admin">Data Catalog Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  datacatalog.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/datacatalog#datacatalog.viewer">Data Catalog Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  datacatalog.viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/datastream#datastream.bigqueryWriter">Datastream Bigquery Writer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  datastream.bigqueryWriter        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/deploymentmanager#clouddeploymentmanager.serviceAgent">Cloud Deployment Manager Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      clouddeploymentmanager.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datastream#datastream.serviceAgent">Datastream Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datastream.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/chronicle#chronicle.serviceAgent">Chronicle Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      chronicle.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.connections.getIamPolicy" class="permission-name add-link" data-text="bigquery.connections.getIamPolicy" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  connections.                  getIamPolicy        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.connectionAdmin">BigQuery Connection Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.connectionAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.connectionUser">BigQuery Connection User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.connectionUser        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAuditor">Security Auditor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAuditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityReviewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/chronicle#chronicle.serviceAgent">Chronicle Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      chronicle.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.connections.list" class="permission-name add-link" data-text="bigquery.connections.list" tabindex="-1"><code dir="ltr" translate="no">         bigquery.connections.list        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.connectionAdmin">BigQuery Connection Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.connectionAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.connectionUser">BigQuery Connection User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.connectionUser        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAuditor">Security Auditor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAuditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityReviewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/chronicle#chronicle.serviceAgent">Chronicle Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      chronicle.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.connections.setIamPolicy" class="permission-name add-link" data-text="bigquery.connections.setIamPolicy" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  connections.                  setIamPolicy        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.connectionAdmin">BigQuery Connection Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.connectionAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAdmin        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.connections.update" class="permission-name add-link" data-text="bigquery.connections.update" tabindex="-1"><code dir="ltr" translate="no">         bigquery.connections.update        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.connectionAdmin">BigQuery Connection Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.connectionAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/chronicle#chronicle.serviceAgent">Chronicle Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      chronicle.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.connections.updateTag" class="permission-name add-link" data-text="bigquery.connections.updateTag" tabindex="-1"><code dir="ltr" translate="no">         bigquery.connections.updateTag        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.connectionAdmin">BigQuery Connection Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.connectionAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/datacatalog#datacatalog.admin">Data Catalog Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  datacatalog.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/datacatalog#datacatalog.tagEditor">Data Catalog Tag Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  datacatalog.tagEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/chronicle#chronicle.serviceAgent">Chronicle Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      chronicle.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.connections.use" class="permission-name add-link" data-text="bigquery.connections.use" tabindex="-1"><code dir="ltr" translate="no">         bigquery.connections.use        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.connectionAdmin">BigQuery Connection Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.connectionAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.connectionUser">BigQuery Connection User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.connectionUser        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.routineAdmin">BigQuery Authorized Routine Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.routineAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.discoveryBigLakePublishingServiceAgent">Dataplex Discovery BigLake Publishing Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.discoveryBigLakePublishingServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/chronicle#chronicle.serviceAgent">Chronicle Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      chronicle.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.dataPolicies.attach" class="permission-name add-link" data-text="bigquery.dataPolicies.attach" tabindex="-1"><code dir="ltr" translate="no">         bigquery.dataPolicies.attach        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.admin">BigQuery Data Policy Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquerydatapolicy.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.dataPolicies.create" class="permission-name add-link" data-text="bigquery.dataPolicies.create" tabindex="-1"><code dir="ltr" translate="no">         bigquery.dataPolicies.create        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.admin">BigQuery Data Policy Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquerydatapolicy.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.dataPolicies.delete" class="permission-name add-link" data-text="bigquery.dataPolicies.delete" tabindex="-1"><code dir="ltr" translate="no">         bigquery.dataPolicies.delete        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.admin">BigQuery Data Policy Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquerydatapolicy.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.dataPolicies.get" class="permission-name add-link" data-text="bigquery.dataPolicies.get" tabindex="-1"><code dir="ltr" translate="no">         bigquery.dataPolicies.get        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.admin">BigQuery Data Policy Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquerydatapolicy.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.viewer">BigQuery Data Policy Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquerydatapolicy.viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.dataPolicies.getIamPolicy" class="permission-name add-link" data-text="bigquery.dataPolicies.getIamPolicy" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  dataPolicies.                  getIamPolicy        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.admin">BigQuery Data Policy Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquerydatapolicy.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAuditor">Security Auditor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAuditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityReviewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.dataPolicies.getRawData" class="permission-name add-link" data-text="bigquery.dataPolicies.getRawData" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  dataPolicies.                  getRawData        </code></h4></td>
<td><p><a href="/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.rawDataReader">Raw Data Reader</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquerydatapolicy.rawDataReader        </code> )</p></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.dataPolicies.list" class="permission-name add-link" data-text="bigquery.dataPolicies.list" tabindex="-1"><code dir="ltr" translate="no">         bigquery.dataPolicies.list        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.admin">BigQuery Data Policy Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquerydatapolicy.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.viewer">BigQuery Data Policy Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquerydatapolicy.viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAuditor">Security Auditor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAuditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityReviewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.dataPolicies.maskedGet" class="permission-name add-link" data-text="bigquery.dataPolicies.maskedGet" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  dataPolicies.                  maskedGet        </code></h4></td>
<td><p><a href="/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.maskedReader">Masked Reader</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquerydatapolicy.maskedReader        </code> )</p></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.dataPolicies.setIamPolicy" class="permission-name add-link" data-text="bigquery.dataPolicies.setIamPolicy" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  dataPolicies.                  setIamPolicy        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.admin">BigQuery Data Policy Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquerydatapolicy.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAdmin        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.dataPolicies.update" class="permission-name add-link" data-text="bigquery.dataPolicies.update" tabindex="-1"><code dir="ltr" translate="no">         bigquery.dataPolicies.update        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquerydatapolicy#bigquerydatapolicy.admin">BigQuery Data Policy Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquerydatapolicy.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.datasets.create" class="permission-name add-link" data-text="bigquery.datasets.create" tabindex="-1"><code dir="ltr" translate="no">         bigquery.datasets.create        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.user        </code> )</p>
<p><a href="/iam/docs/roles-permissions/commercebusinessenablement#commercebusinessenablement.admin">Commerce Business Enablement Configuration Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  commercebusinessenablement.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/datastream#datastream.bigqueryWriter">Datastream Bigquery Writer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  datastream.bigqueryWriter        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.dataScientist">Data Scientist</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.dataScientist        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.customCodeServiceAgent">Vertex AI Custom Code Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.customCodeServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.modelMonitoringServiceAgent">Vertex AI Model Monitoring Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.modelMonitoringServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.ragServiceAgent">Vertex AI RAG Data Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.ragServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.serviceAgent">Vertex AI Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.tuningServiceAgent">Vertex AI Tuning Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.tuningServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/automl#automl.serviceAgent">AutoML Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      automl.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/automlrecommendations#automlrecommendations.serviceAgent">Recommendations AI Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      automlrecommendations.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/ces#ces.serviceAgent">Customer Engagement Suite Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      ces.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/chronicle#chronicle.serviceAgent">Chronicle Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      chronicle.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/deploymentmanager#clouddeploymentmanager.serviceAgent">Cloud Deployment Manager Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      clouddeploymentmanager.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/contactcenterinsights#contactcenterinsights.serviceAgent">Contact Center AI Insights Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      contactcenterinsights.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/container#container.serviceAgent">Kubernetes Engine Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      container.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datalabeling#datalabeling.serviceAgent">Data Labeling Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datalabeling.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.discoveryPublishingServiceAgent">Dataplex Discovery Publishing Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.discoveryPublishingServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datastream#datastream.serviceAgent">Datastream Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datastream.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dialogflow#dialogflow.serviceAgent">Dialogflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dialogflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/discoveryengine#discoveryengine.serviceAgent">Discovery Engine Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      discoveryengine.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/enterpriseknowledgegraph#enterpriseknowledgegraph.serviceAgent">Enterprise Knowledge Graph Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      enterpriseknowledgegraph.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/firebase#firebase.managementServiceAgent">Firebase Service Management Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      firebase.managementServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/firebasecrash#firebasecrashlytics.serviceAgent">Firebase Crashlytics Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      firebasecrashlytics.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/fleetengine#fleetengine.serviceAgent">FleetEngine Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      fleetengine.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/logging#logging.serviceAgent">Cloud Logging Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      logging.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/ml#ml.serviceAgent">AI Platform Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      ml.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/observability#observability.serviceAgent">Observability Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      observability.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/retail#retail.serviceAgent">Retail Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      retail.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/spectrumsas#spectrumsas.serviceAgent">Spectrum SAS Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      spectrumsas.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/storageinsights#storageinsights.serviceAgent">StorageInsights Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      storageinsights.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/visionai#visionai.serviceAgent">Cloud Vision AI Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      visionai.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.batchPredictionServiceAgent">Vertex AI Batch Prediction Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.batchPredictionServiceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.datasets.createTagBinding" class="permission-name add-link" data-text="bigquery.datasets.createTagBinding" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  datasets.                  createTagBinding        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/resourcemanager#resourcemanager.tagUser">Tag User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  resourcemanager.tagUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dspm#dspm.serviceAgent">DSPM Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dspm.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.datasets.delete" class="permission-name add-link" data-text="bigquery.datasets.delete" tabindex="-1"><code dir="ltr" translate="no">         bigquery.datasets.delete        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/deploymentmanager#clouddeploymentmanager.serviceAgent">Cloud Deployment Manager Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      clouddeploymentmanager.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.datasets.deleteTagBinding" class="permission-name add-link" data-text="bigquery.datasets.deleteTagBinding" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  datasets.                  deleteTagBinding        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/resourcemanager#resourcemanager.tagUser">Tag User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  resourcemanager.tagUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dspm#dspm.serviceAgent">DSPM Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dspm.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.datasets.get" class="permission-name add-link" data-text="bigquery.datasets.get" tabindex="-1"><code dir="ltr" translate="no">         bigquery.datasets.get        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataViewer">BigQuery Data Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.metadataViewer">BigQuery Metadata Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.metadataViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.routineAdmin">BigQuery Authorized Routine Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.routineAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.routineDataEditor">BigQuery Authorized Routine Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.routineDataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.routineDataViewer">BigQuery Authorized Routine Data Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.routineDataViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.routineMetadataViewer">BigQuery Authorized Routine Metadata Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.routineMetadataViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.user        </code> )</p>
<p><a href="/iam/docs/roles-permissions/commercebusinessenablement#commercebusinessenablement.admin">Commerce Business Enablement Configuration Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  commercebusinessenablement.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/datacatalog#datacatalog.admin">Data Catalog Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  datacatalog.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/datacatalog#datacatalog.viewer">Data Catalog Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  datacatalog.viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dataplex.storageDataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dataplex#dataplex.storageDataReader">Dataplex Storage Data Reader</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dataplex.storageDataReader        </code> )</p>
<p><a href="/iam/docs/roles-permissions/datastream#datastream.bigqueryWriter">Datastream Bigquery Writer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  datastream.bigqueryWriter        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.dataScientist">Data Scientist</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.dataScientist        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAuditor">Security Auditor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAuditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.siteReliabilityEngineer">Site Reliability Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.siteReliabilityEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p><a href="/iam/docs/roles-permissions/securedlandingzone#securedlandingzone.bqdwProjectRemediator">SLZ BQDW Blueprint Project Level Remediator</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  securedlandingzone.bqdwProjectRemediator        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.customCodeServiceAgent">Vertex AI Custom Code Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.customCodeServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.modelMonitoringServiceAgent">Vertex AI Model Monitoring Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.modelMonitoringServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.ragServiceAgent">Vertex AI RAG Data Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.ragServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.serviceAgent">Vertex AI Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.tuningServiceAgent">Vertex AI Tuning Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.tuningServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/auditmanager#auditmanager.serviceAgent">Audit Manager Auditing Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      auditmanager.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/automl#automl.serviceAgent">AutoML Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      automl.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/automlrecommendations#automlrecommendations.serviceAgent">Recommendations AI Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      automlrecommendations.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/bigquery#bigquery.connectedSheetsServiceAgent">Connected Sheets Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      bigquery.connectedSheetsServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/ces#ces.serviceAgent">Customer Engagement Suite Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      ces.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/cloudasset#cloudasset.serviceAgent">Cloud Asset Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      cloudasset.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/deploymentmanager#clouddeploymentmanager.serviceAgent">Cloud Deployment Manager Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      clouddeploymentmanager.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/cloudsecuritycompliance#cloudsecuritycompliance.serviceAgent">Cloud Security Compliance Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      cloudsecuritycompliance.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/contactcenterinsights#contactcenterinsights.serviceAgent">Contact Center AI Insights Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      contactcenterinsights.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/container#container.serviceAgent">Kubernetes Engine Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      container.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datalabeling#datalabeling.serviceAgent">Data Labeling Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datalabeling.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.discoveryPublishingServiceAgent">Dataplex Discovery Publishing Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.discoveryPublishingServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datastream#datastream.serviceAgent">Datastream Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datastream.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/discoveryengine#discoveryengine.serviceAgent">Discovery Engine Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      discoveryengine.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/enterpriseknowledgegraph#enterpriseknowledgegraph.serviceAgent">Enterprise Knowledge Graph Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      enterpriseknowledgegraph.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/firebase#firebase.managementServiceAgent">Firebase Service Management Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      firebase.managementServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/firebasecrash#firebasecrashlytics.serviceAgent">Firebase Crashlytics Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      firebasecrashlytics.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/fleetengine#fleetengine.serviceAgent">FleetEngine Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      fleetengine.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/logging#logging.serviceAgent">Cloud Logging Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      logging.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/looker#looker.serviceAgent">Looker Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      looker.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/ml#ml.serviceAgent">AI Platform Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      ml.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/observability#observability.serviceAgent">Observability Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      observability.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/retail#retail.serviceAgent">Retail Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      retail.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/securitycenter#securitycenter.controlServiceAgent">Security Center Control Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      securitycenter.controlServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/securitycenter#securitycenter.securityHealthAnalyticsServiceAgent">Security Health Analytics Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      securitycenter.securityHealthAnalyticsServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/securitycenter#securitycenter.serviceAgent">Security Center Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      securitycenter.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/visionai#visionai.serviceAgent">Cloud Vision AI Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      visionai.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.batchPredictionServiceAgent">Vertex AI Batch Prediction Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.batchPredictionServiceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.datasets.getIamPolicy" class="permission-name add-link" data-text="bigquery.datasets.getIamPolicy" tabindex="-1"><code dir="ltr" translate="no">         bigquery.datasets.getIamPolicy        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataViewer">BigQuery Data Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.metadataViewer">BigQuery Metadata Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.metadataViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.user        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.dataScientist">Data Scientist</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.dataScientist        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAuditor">Security Auditor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAuditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityReviewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.siteReliabilityEngineer">Site Reliability Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.siteReliabilityEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p><a href="/iam/docs/roles-permissions/securedlandingzone#securedlandingzone.bqdwProjectRemediator">SLZ BQDW Blueprint Project Level Remediator</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  securedlandingzone.bqdwProjectRemediator        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/firebase#firebase.managementServiceAgent">Firebase Service Management Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      firebase.managementServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/deploymentmanager#clouddeploymentmanager.serviceAgent">Cloud Deployment Manager Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      clouddeploymentmanager.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.datasets.link" class="permission-name add-link" data-text="bigquery.datasets.link" tabindex="-1"><code dir="ltr" translate="no">         bigquery.datasets.link        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/logging#logging.serviceAgent">Cloud Logging Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      logging.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/observability#observability.serviceAgent">Observability Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      observability.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.datasets.listEffectiveTags" class="permission-name add-link" data-text="bigquery.datasets.listEffectiveTags" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  datasets.                  listEffectiveTags        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAuditor">Security Auditor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAuditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p><a href="/iam/docs/roles-permissions/resourcemanager#resourcemanager.tagUser">Tag User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  resourcemanager.tagUser        </code> )</p>
<p><a href="/iam/docs/roles-permissions/resourcemanager#resourcemanager.tagViewer">Tag Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  resourcemanager.tagViewer        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dspm#dspm.serviceAgent">DSPM Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dspm.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.datasets.listSharedDatasetUsage" class="permission-name add-link" data-text="bigquery.datasets.listSharedDatasetUsage" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  datasets.                  listSharedDatasetUsage        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.datasets.listTagBindings" class="permission-name add-link" data-text="bigquery.datasets.listTagBindings" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  datasets.                  listTagBindings        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAuditor">Security Auditor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAuditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p><a href="/iam/docs/roles-permissions/resourcemanager#resourcemanager.tagUser">Tag User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  resourcemanager.tagUser        </code> )</p>
<p><a href="/iam/docs/roles-permissions/resourcemanager#resourcemanager.tagViewer">Tag Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  resourcemanager.tagViewer        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dspm#dspm.serviceAgent">DSPM Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dspm.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.datasets.setIamPolicy" class="permission-name add-link" data-text="bigquery.datasets.setIamPolicy" tabindex="-1"><code dir="ltr" translate="no">         bigquery.datasets.setIamPolicy        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/securedlandingzone#securedlandingzone.bqdwProjectRemediator">SLZ BQDW Blueprint Project Level Remediator</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  securedlandingzone.bqdwProjectRemediator        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/firebase#firebase.managementServiceAgent">Firebase Service Management Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      firebase.managementServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.datasets.update" class="permission-name add-link" data-text="bigquery.datasets.update" tabindex="-1"><code dir="ltr" translate="no">         bigquery.datasets.update        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/commercebusinessenablement#commercebusinessenablement.admin">Commerce Business Enablement Configuration Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  commercebusinessenablement.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/securedlandingzone#securedlandingzone.bqdwProjectRemediator">SLZ BQDW Blueprint Project Level Remediator</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  securedlandingzone.bqdwProjectRemediator        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/firebase#firebase.managementServiceAgent">Firebase Service Management Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      firebase.managementServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/deploymentmanager#clouddeploymentmanager.serviceAgent">Cloud Deployment Manager Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      clouddeploymentmanager.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.datasets.updateTag" class="permission-name add-link" data-text="bigquery.datasets.updateTag" tabindex="-1"><code dir="ltr" translate="no">         bigquery.datasets.updateTag        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/datacatalog#datacatalog.admin">Data Catalog Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  datacatalog.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/datacatalog#datacatalog.tagEditor">Data Catalog Tag Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  datacatalog.tagEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.dataScientist">Data Scientist</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.dataScientist        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/ces#ces.serviceAgent">Customer Engagement Suite Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      ces.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.jobs.create" class="permission-name add-link" data-text="bigquery.jobs.create" tabindex="-1"><code dir="ltr" translate="no">         bigquery.jobs.create        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.jobUser">BigQuery Job User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.jobUser        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioUser">BigQuery Studio User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioUser        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.user        </code> )</p>
<p><a href="/iam/docs/roles-permissions/datastream#datastream.bigqueryWriter">Datastream Bigquery Writer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  datastream.bigqueryWriter        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.dataScientist">Data Scientist</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.dataScientist        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.customCodeServiceAgent">Vertex AI Custom Code Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.customCodeServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.modelMonitoringServiceAgent">Vertex AI Model Monitoring Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.modelMonitoringServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.ragServiceAgent">Vertex AI RAG Data Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.ragServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.serviceAgent">Vertex AI Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.tuningServiceAgent">Vertex AI Tuning Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.tuningServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/automl#automl.serviceAgent">AutoML Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      automl.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/automlrecommendations#automlrecommendations.serviceAgent">Recommendations AI Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      automlrecommendations.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/bigquery#bigquery.connectedSheetsServiceAgent">Connected Sheets Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      bigquery.connectedSheetsServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/bigquerydatatransfer#bigquerydatatransfer.serviceAgent">BigQuery Data Transfer Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      bigquerydatatransfer.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/bigqueryomni#bigqueryomni.serviceAgent">BigQuery Omni Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      bigqueryomni.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/ces#ces.serviceAgent">Customer Engagement Suite Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      ces.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/chronicle#chronicle.serviceAgent">Chronicle Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      chronicle.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/cloudasset#cloudasset.serviceAgent">Cloud Asset Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      cloudasset.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/deploymentmanager#clouddeploymentmanager.serviceAgent">Cloud Deployment Manager Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      clouddeploymentmanager.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/contactcenterinsights#contactcenterinsights.serviceAgent">Contact Center AI Insights Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      contactcenterinsights.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datalabeling#datalabeling.serviceAgent">Data Labeling Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datalabeling.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datastream#datastream.serviceAgent">Datastream Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datastream.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datastudio#datastudio.serviceAgent">Data Studio Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datastudio.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dialogflow#dialogflow.serviceAgent">Dialogflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dialogflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/discoveryengine#discoveryengine.serviceAgent">Discovery Engine Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      discoveryengine.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dspm#dspm.serviceAgent">DSPM Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dspm.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/enterpriseknowledgegraph#enterpriseknowledgegraph.serviceAgent">Enterprise Knowledge Graph Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      enterpriseknowledgegraph.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/fleetengine#fleetengine.serviceAgent">FleetEngine Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      fleetengine.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/looker#looker.serviceAgent">Looker Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      looker.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/ml#ml.serviceAgent">AI Platform Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      ml.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/monitoring#monitoring.notificationServiceAgent">Monitoring Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      monitoring.notificationServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/retail#retail.serviceAgent">Retail Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      retail.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/spectrumsas#spectrumsas.serviceAgent">Spectrum SAS Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      spectrumsas.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/visionai#visionai.serviceAgent">Cloud Vision AI Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      visionai.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.batchPredictionServiceAgent">Vertex AI Batch Prediction Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.batchPredictionServiceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.jobs.createGlobalQuery" class="permission-name add-link" data-text="bigquery.jobs.createGlobalQuery" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  jobs.                  createGlobalQuery        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.jobs.delete" class="permission-name add-link" data-text="bigquery.jobs.delete" tabindex="-1"><code dir="ltr" translate="no">         bigquery.jobs.delete        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/datastream#datastream.bigqueryWriter">Datastream Bigquery Writer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  datastream.bigqueryWriter        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datastream#datastream.serviceAgent">Datastream Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datastream.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.jobs.get" class="permission-name add-link" data-text="bigquery.jobs.get" tabindex="-1"><code dir="ltr" translate="no">         bigquery.jobs.get        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceViewer">BigQuery Resource Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/datastream#datastream.bigqueryWriter">Datastream Bigquery Writer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  datastream.bigqueryWriter        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.customCodeServiceAgent">Vertex AI Custom Code Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.customCodeServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.modelMonitoringServiceAgent">Vertex AI Model Monitoring Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.modelMonitoringServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.ragServiceAgent">Vertex AI RAG Data Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.ragServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.serviceAgent">Vertex AI Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.tuningServiceAgent">Vertex AI Tuning Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.tuningServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/automlrecommendations#automlrecommendations.serviceAgent">Recommendations AI Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      automlrecommendations.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/chronicle#chronicle.serviceAgent">Chronicle Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      chronicle.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/cloudasset#cloudasset.serviceAgent">Cloud Asset Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      cloudasset.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/contactcenterinsights#contactcenterinsights.serviceAgent">Contact Center AI Insights Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      contactcenterinsights.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datalabeling#datalabeling.serviceAgent">Data Labeling Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datalabeling.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datastream#datastream.serviceAgent">Datastream Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datastream.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/discoveryengine#discoveryengine.serviceAgent">Discovery Engine Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      discoveryengine.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/ml#ml.serviceAgent">AI Platform Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      ml.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/retail#retail.serviceAgent">Retail Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      retail.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/visionai#visionai.serviceAgent">Cloud Vision AI Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      visionai.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.batchPredictionServiceAgent">Vertex AI Batch Prediction Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.batchPredictionServiceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.jobs.list" class="permission-name add-link" data-text="bigquery.jobs.list" tabindex="-1"><code dir="ltr" translate="no">         bigquery.jobs.list        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceViewer">BigQuery Resource Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.user        </code> )</p>
<p><a href="/iam/docs/roles-permissions/datastream#datastream.bigqueryWriter">Datastream Bigquery Writer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  datastream.bigqueryWriter        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAuditor">Security Auditor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAuditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityReviewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datastream#datastream.serviceAgent">Datastream Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datastream.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/discoveryengine#discoveryengine.serviceAgent">Discovery Engine Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      discoveryengine.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/ml#ml.serviceAgent">AI Platform Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      ml.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/retail#retail.serviceAgent">Retail Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      retail.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/automlrecommendations#automlrecommendations.serviceAgent">Recommendations AI Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      automlrecommendations.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.jobs.listAll" class="permission-name add-link" data-text="bigquery.jobs.listAll" tabindex="-1"><code dir="ltr" translate="no">         bigquery.jobs.listAll        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceViewer">BigQuery Resource Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.jobs.listExecutionMetadata" class="permission-name add-link" data-text="bigquery.jobs.listExecutionMetadata" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  jobs.                  listExecutionMetadata        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceViewer">BigQuery Resource Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.jobs.update" class="permission-name add-link" data-text="bigquery.jobs.update" tabindex="-1"><code dir="ltr" translate="no">         bigquery.jobs.update        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/datastream#datastream.bigqueryWriter">Datastream Bigquery Writer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  datastream.bigqueryWriter        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datastream#datastream.serviceAgent">Datastream Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datastream.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/discoveryengine#discoveryengine.serviceAgent">Discovery Engine Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      discoveryengine.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/ml#ml.serviceAgent">AI Platform Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      ml.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/retail#retail.serviceAgent">Retail Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      retail.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/automlrecommendations#automlrecommendations.serviceAgent">Recommendations AI Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      automlrecommendations.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.models.create" class="permission-name add-link" data-text="bigquery.models.create" tabindex="-1"><code dir="ltr" translate="no">         bigquery.models.create        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dataplex.storageDataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.dataScientist">Data Scientist</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.dataScientist        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.serviceAgent">Vertex AI Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.batchPredictionServiceAgent">Vertex AI Batch Prediction Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.batchPredictionServiceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.models.delete" class="permission-name add-link" data-text="bigquery.models.delete" tabindex="-1"><code dir="ltr" translate="no">         bigquery.models.delete        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dataplex.storageDataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.dataScientist">Data Scientist</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.dataScientist        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.models.export" class="permission-name add-link" data-text="bigquery.models.export" tabindex="-1"><code dir="ltr" translate="no">         bigquery.models.export        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataViewer">BigQuery Data Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dataplex.storageDataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dataplex#dataplex.storageDataReader">Dataplex Storage Data Reader</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dataplex.storageDataReader        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.dataScientist">Data Scientist</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.dataScientist        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.siteReliabilityEngineer">Site Reliability Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.siteReliabilityEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.serviceAgent">Vertex AI Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/looker#looker.serviceAgent">Looker Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      looker.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/visionai#visionai.serviceAgent">Cloud Vision AI Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      visionai.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.batchPredictionServiceAgent">Vertex AI Batch Prediction Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.batchPredictionServiceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.models.getData" class="permission-name add-link" data-text="bigquery.models.getData" tabindex="-1"><code dir="ltr" translate="no">         bigquery.models.getData        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataViewer">BigQuery Data Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.routineAdmin">BigQuery Authorized Routine Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.routineAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.routineDataEditor">BigQuery Authorized Routine Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.routineDataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.routineDataViewer">BigQuery Authorized Routine Data Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.routineDataViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dataplex.storageDataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dataplex#dataplex.storageDataReader">Dataplex Storage Data Reader</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dataplex.storageDataReader        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.dataScientist">Data Scientist</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.dataScientist        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.siteReliabilityEngineer">Site Reliability Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.siteReliabilityEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.serviceAgent">Vertex AI Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/looker#looker.serviceAgent">Looker Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      looker.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.batchPredictionServiceAgent">Vertex AI Batch Prediction Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.batchPredictionServiceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.models.getMetadata" class="permission-name add-link" data-text="bigquery.models.getMetadata" tabindex="-1"><code dir="ltr" translate="no">         bigquery.models.getMetadata        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataViewer">BigQuery Data Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.metadataViewer">BigQuery Metadata Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.metadataViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.routineAdmin">BigQuery Authorized Routine Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.routineAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.routineDataEditor">BigQuery Authorized Routine Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.routineDataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.routineDataViewer">BigQuery Authorized Routine Data Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.routineDataViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.routineMetadataViewer">BigQuery Authorized Routine Metadata Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.routineMetadataViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/datacatalog#datacatalog.admin">Data Catalog Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  datacatalog.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/datacatalog#datacatalog.viewer">Data Catalog Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  datacatalog.viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dataplex.storageDataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dataplex#dataplex.storageDataReader">Dataplex Storage Data Reader</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dataplex.storageDataReader        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.dataScientist">Data Scientist</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.dataScientist        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAuditor">Security Auditor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAuditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.siteReliabilityEngineer">Site Reliability Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.siteReliabilityEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/looker#looker.serviceAgent">Looker Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      looker.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.models.list" class="permission-name add-link" data-text="bigquery.models.list" tabindex="-1"><code dir="ltr" translate="no">         bigquery.models.list        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataViewer">BigQuery Data Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.metadataViewer">BigQuery Metadata Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.metadataViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.user        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dataplex.storageDataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dataplex#dataplex.storageDataReader">Dataplex Storage Data Reader</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dataplex.storageDataReader        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.dataScientist">Data Scientist</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.dataScientist        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAuditor">Security Auditor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAuditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityReviewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.siteReliabilityEngineer">Site Reliability Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.siteReliabilityEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/looker#looker.serviceAgent">Looker Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      looker.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.models.updateData" class="permission-name add-link" data-text="bigquery.models.updateData" tabindex="-1"><code dir="ltr" translate="no">         bigquery.models.updateData        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dataplex.storageDataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.dataScientist">Data Scientist</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.dataScientist        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.models.updateMetadata" class="permission-name add-link" data-text="bigquery.models.updateMetadata" tabindex="-1"><code dir="ltr" translate="no">         bigquery.models.updateMetadata        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dataplex.storageDataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.dataScientist">Data Scientist</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.dataScientist        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.models.updateTag" class="permission-name add-link" data-text="bigquery.models.updateTag" tabindex="-1"><code dir="ltr" translate="no">         bigquery.models.updateTag        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/datacatalog#datacatalog.admin">Data Catalog Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  datacatalog.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/datacatalog#datacatalog.tagEditor">Data Catalog Tag Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  datacatalog.tagEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.dataScientist">Data Scientist</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.dataScientist        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.objectRefs.read" class="permission-name add-link" data-text="bigquery.objectRefs.read" tabindex="-1"><code dir="ltr" translate="no">         bigquery.objectRefs.read        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.objectRefAdmin">BigQuery ObjectRef Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.objectRefAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.objectRefReader">BigQuery ObjectRef Reader</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.objectRefReader        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.serviceAgent">Vertex AI Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.objectRefs.write" class="permission-name add-link" data-text="bigquery.objectRefs.write" tabindex="-1"><code dir="ltr" translate="no">         bigquery.objectRefs.write        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.objectRefAdmin">BigQuery ObjectRef Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.objectRefAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.readsessions.create" class="permission-name add-link" data-text="bigquery.readsessions.create" tabindex="-1"><code dir="ltr" translate="no">         bigquery.readsessions.create        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.readSessionUser">BigQuery Read Session User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.readSessionUser        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioUser">BigQuery Studio User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioUser        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.user        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.dataScientist">Data Scientist</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.dataScientist        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.customCodeServiceAgent">Vertex AI Custom Code Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.customCodeServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.ragServiceAgent">Vertex AI RAG Data Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.ragServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.serviceAgent">Vertex AI Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/enterpriseknowledgegraph#enterpriseknowledgegraph.serviceAgent">Enterprise Knowledge Graph Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      enterpriseknowledgegraph.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/visionai#visionai.serviceAgent">Cloud Vision AI Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      visionai.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.batchPredictionServiceAgent">Vertex AI Batch Prediction Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.batchPredictionServiceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.readsessions.getData" class="permission-name add-link" data-text="bigquery.readsessions.getData" tabindex="-1"><code dir="ltr" translate="no">         bigquery.readsessions.getData        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.readSessionUser">BigQuery Read Session User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.readSessionUser        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioUser">BigQuery Studio User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioUser        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.user        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.dataScientist">Data Scientist</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.dataScientist        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.customCodeServiceAgent">Vertex AI Custom Code Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.customCodeServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.ragServiceAgent">Vertex AI RAG Data Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.ragServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.serviceAgent">Vertex AI Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/enterpriseknowledgegraph#enterpriseknowledgegraph.serviceAgent">Enterprise Knowledge Graph Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      enterpriseknowledgegraph.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.batchPredictionServiceAgent">Vertex AI Batch Prediction Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.batchPredictionServiceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.readsessions.update" class="permission-name add-link" data-text="bigquery.readsessions.update" tabindex="-1"><code dir="ltr" translate="no">         bigquery.readsessions.update        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.readSessionUser">BigQuery Read Session User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.readSessionUser        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioUser">BigQuery Studio User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioUser        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.user        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.dataScientist">Data Scientist</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.dataScientist        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.reservationAssignments.create" class="permission-name add-link" data-text="bigquery.reservationAssignments.create" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  reservationAssignments.                  create        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.reservationAssignments.delete" class="permission-name add-link" data-text="bigquery.reservationAssignments.delete" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  reservationAssignments.                  delete        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.reservationAssignments.list" class="permission-name add-link" data-text="bigquery.reservationAssignments.list" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  reservationAssignments.                  list        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceViewer">BigQuery Resource Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.user        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAuditor">Security Auditor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAuditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityReviewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.reservationAssignments.search" class="permission-name add-link" data-text="bigquery.reservationAssignments.search" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  reservationAssignments.                  search        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceViewer">BigQuery Resource Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.user        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.reservationGroups.create" class="permission-name add-link" data-text="bigquery.reservationGroups.create" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  reservationGroups.                  create        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.reservationGroups.delete" class="permission-name add-link" data-text="bigquery.reservationGroups.delete" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  reservationGroups.                  delete        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.reservationGroups.get" class="permission-name add-link" data-text="bigquery.reservationGroups.get" tabindex="-1"><code dir="ltr" translate="no">         bigquery.reservationGroups.get        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceViewer">BigQuery Resource Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.user        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.reservationGroups.list" class="permission-name add-link" data-text="bigquery.reservationGroups.list" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  reservationGroups.                  list        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceViewer">BigQuery Resource Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.user        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAuditor">Security Auditor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAuditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityReviewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.reservations.create" class="permission-name add-link" data-text="bigquery.reservations.create" tabindex="-1"><code dir="ltr" translate="no">         bigquery.reservations.create        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.reservations.delete" class="permission-name add-link" data-text="bigquery.reservations.delete" tabindex="-1"><code dir="ltr" translate="no">         bigquery.reservations.delete        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.reservations.get" class="permission-name add-link" data-text="bigquery.reservations.get" tabindex="-1"><code dir="ltr" translate="no">         bigquery.reservations.get        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceViewer">BigQuery Resource Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.user        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.reservations.getIamPolicy" class="permission-name add-link" data-text="bigquery.reservations.getIamPolicy" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  reservations.                  getIamPolicy        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAuditor">Security Auditor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAuditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityReviewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.reservations.list" class="permission-name add-link" data-text="bigquery.reservations.list" tabindex="-1"><code dir="ltr" translate="no">         bigquery.reservations.list        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceViewer">BigQuery Resource Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.user        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAuditor">Security Auditor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAuditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityReviewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.reservations.listFailoverDatasets" class="permission-name add-link" data-text="bigquery.reservations.listFailoverDatasets" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  reservations.                  listFailoverDatasets        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceViewer">BigQuery Resource Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.user        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.reservations.setIamPolicy" class="permission-name add-link" data-text="bigquery.reservations.setIamPolicy" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  reservations.                  setIamPolicy        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAdmin        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.reservations.update" class="permission-name add-link" data-text="bigquery.reservations.update" tabindex="-1"><code dir="ltr" translate="no">         bigquery.reservations.update        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.reservations.use" class="permission-name add-link" data-text="bigquery.reservations.use" tabindex="-1"><code dir="ltr" translate="no">         bigquery.reservations.use        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceAdmin">BigQuery Resource Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.resourceEditor">BigQuery Resource Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.resourceEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.user        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.routines.create" class="permission-name add-link" data-text="bigquery.routines.create" tabindex="-1"><code dir="ltr" translate="no">         bigquery.routines.create        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dataplex.storageDataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.dataScientist">Data Scientist</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.dataScientist        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/deploymentmanager#clouddeploymentmanager.serviceAgent">Cloud Deployment Manager Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      clouddeploymentmanager.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.routines.delete" class="permission-name add-link" data-text="bigquery.routines.delete" tabindex="-1"><code dir="ltr" translate="no">         bigquery.routines.delete        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dataplex.storageDataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.dataScientist">Data Scientist</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.dataScientist        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.routines.get" class="permission-name add-link" data-text="bigquery.routines.get" tabindex="-1"><code dir="ltr" translate="no">         bigquery.routines.get        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataViewer">BigQuery Data Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.metadataViewer">BigQuery Metadata Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.metadataViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.routineAdmin">BigQuery Authorized Routine Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.routineAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.routineDataEditor">BigQuery Authorized Routine Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.routineDataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.routineDataViewer">BigQuery Authorized Routine Data Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.routineDataViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.routineMetadataViewer">BigQuery Authorized Routine Metadata Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.routineMetadataViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/datacatalog#datacatalog.admin">Data Catalog Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  datacatalog.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/datacatalog#datacatalog.viewer">Data Catalog Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  datacatalog.viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dataplex.storageDataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dataplex#dataplex.storageDataReader">Dataplex Storage Data Reader</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dataplex.storageDataReader        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.dataScientist">Data Scientist</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.dataScientist        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAuditor">Security Auditor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAuditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.siteReliabilityEngineer">Site Reliability Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.siteReliabilityEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datastream#datastream.serviceAgent">Datastream Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datastream.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/deploymentmanager#clouddeploymentmanager.serviceAgent">Cloud Deployment Manager Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      clouddeploymentmanager.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.routines.list" class="permission-name add-link" data-text="bigquery.routines.list" tabindex="-1"><code dir="ltr" translate="no">         bigquery.routines.list        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataViewer">BigQuery Data Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.metadataViewer">BigQuery Metadata Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.metadataViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.routineAdmin">BigQuery Authorized Routine Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.routineAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.routineDataEditor">BigQuery Authorized Routine Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.routineDataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.routineDataViewer">BigQuery Authorized Routine Data Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.routineDataViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.routineMetadataViewer">BigQuery Authorized Routine Metadata Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.routineMetadataViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.user        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dataplex.storageDataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dataplex#dataplex.storageDataReader">Dataplex Storage Data Reader</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dataplex.storageDataReader        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.dataScientist">Data Scientist</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.dataScientist        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAuditor">Security Auditor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAuditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityReviewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.siteReliabilityEngineer">Site Reliability Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.siteReliabilityEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datastream#datastream.serviceAgent">Datastream Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datastream.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.routines.update" class="permission-name add-link" data-text="bigquery.routines.update" tabindex="-1"><code dir="ltr" translate="no">         bigquery.routines.update        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dataplex.storageDataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.dataScientist">Data Scientist</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.dataScientist        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/deploymentmanager#clouddeploymentmanager.serviceAgent">Cloud Deployment Manager Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      clouddeploymentmanager.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.routines.updateTag" class="permission-name add-link" data-text="bigquery.routines.updateTag" tabindex="-1"><code dir="ltr" translate="no">         bigquery.routines.updateTag        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/datacatalog#datacatalog.admin">Data Catalog Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  datacatalog.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/datacatalog#datacatalog.tagEditor">Data Catalog Tag Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  datacatalog.tagEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.dataScientist">Data Scientist</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.dataScientist        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.rowAccessPolicies.create" class="permission-name add-link" data-text="bigquery.rowAccessPolicies.create" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  rowAccessPolicies.                  create        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.rowAccessPolicies.delete" class="permission-name add-link" data-text="bigquery.rowAccessPolicies.delete" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  rowAccessPolicies.                  delete        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.rowAccessPolicies.get" class="permission-name add-link" data-text="bigquery.rowAccessPolicies.get" tabindex="-1"><code dir="ltr" translate="no">         bigquery.rowAccessPolicies.get        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.rowAccessPolicies.getFilteredData" class="permission-name add-link" data-text="bigquery.rowAccessPolicies.getFilteredData" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  rowAccessPolicies.                  getFilteredData        </code></h4></td>
<td><p><a href="/iam/docs/roles-permissions/bigquery#bigquery.filteredDataViewer">BigQuery Filtered Data Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.filteredDataViewer        </code> )</p></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.rowAccessPolicies.getIamPolicy" class="permission-name add-link" data-text="bigquery.rowAccessPolicies.getIamPolicy" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  rowAccessPolicies.                  getIamPolicy        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAuditor">Security Auditor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAuditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityReviewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.rowAccessPolicies.list" class="permission-name add-link" data-text="bigquery.rowAccessPolicies.list" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  rowAccessPolicies.                  list        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAuditor">Security Auditor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAuditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityReviewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.rowAccessPolicies.overrideTimeTravelRestrictions" class="permission-name add-link" data-text="bigquery.rowAccessPolicies.overrideTimeTravelRestrictions" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  rowAccessPolicies.                  overrideTimeTravelRestrictions        </code></h4></td>
<td><p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.rowAccessPolicies.setIamPolicy" class="permission-name add-link" data-text="bigquery.rowAccessPolicies.setIamPolicy" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  rowAccessPolicies.                  setIamPolicy        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAdmin        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.rowAccessPolicies.update" class="permission-name add-link" data-text="bigquery.rowAccessPolicies.update" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  rowAccessPolicies.                  update        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.savedqueries.create" class="permission-name add-link" data-text="bigquery.savedqueries.create" tabindex="-1"><code dir="ltr" translate="no">         bigquery.savedqueries.create        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.savedqueries.delete" class="permission-name add-link" data-text="bigquery.savedqueries.delete" tabindex="-1"><code dir="ltr" translate="no">         bigquery.savedqueries.delete        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.savedqueries.get" class="permission-name add-link" data-text="bigquery.savedqueries.get" tabindex="-1"><code dir="ltr" translate="no">         bigquery.savedqueries.get        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.user        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.savedqueries.list" class="permission-name add-link" data-text="bigquery.savedqueries.list" tabindex="-1"><code dir="ltr" translate="no">         bigquery.savedqueries.list        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.user        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAuditor">Security Auditor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAuditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityReviewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.savedqueries.update" class="permission-name add-link" data-text="bigquery.savedqueries.update" tabindex="-1"><code dir="ltr" translate="no">         bigquery.savedqueries.update        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.tables.create" class="permission-name add-link" data-text="bigquery.tables.create" tabindex="-1"><code dir="ltr" translate="no">         bigquery.tables.create        </code></h4></td>
<td><p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.routineAdmin">BigQuery Authorized Routine Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.routineAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.routineDataEditor">BigQuery Authorized Routine Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.routineDataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dataplex.storageDataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/datastream#datastream.bigqueryWriter">Datastream Bigquery Writer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  datastream.bigqueryWriter        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.dataScientist">Data Scientist</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.dataScientist        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.customCodeServiceAgent">Vertex AI Custom Code Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.customCodeServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.modelMonitoringServiceAgent">Vertex AI Model Monitoring Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.modelMonitoringServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.ragServiceAgent">Vertex AI RAG Data Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.ragServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.serviceAgent">Vertex AI Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.tuningServiceAgent">Vertex AI Tuning Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.tuningServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/automl#automl.serviceAgent">AutoML Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      automl.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/automlrecommendations#automlrecommendations.serviceAgent">Recommendations AI Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      automlrecommendations.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/bigquery#bigquery.connectedSheetsServiceAgent">Connected Sheets Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      bigquery.connectedSheetsServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/ces#ces.serviceAgent">Customer Engagement Suite Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      ces.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/chronicle#chronicle.serviceAgent">Chronicle Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      chronicle.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/cloudasset#cloudasset.serviceAgent">Cloud Asset Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      cloudasset.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/deploymentmanager#clouddeploymentmanager.serviceAgent">Cloud Deployment Manager Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      clouddeploymentmanager.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/contactcenterinsights#contactcenterinsights.serviceAgent">Contact Center AI Insights Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      contactcenterinsights.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/container#container.serviceAgent">Kubernetes Engine Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      container.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datalabeling#datalabeling.serviceAgent">Data Labeling Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datalabeling.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datastream#datastream.serviceAgent">Datastream Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datastream.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dialogflow#dialogflow.serviceAgent">Dialogflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dialogflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/discoveryengine#discoveryengine.serviceAgent">Discovery Engine Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      discoveryengine.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/enterpriseknowledgegraph#enterpriseknowledgegraph.serviceAgent">Enterprise Knowledge Graph Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      enterpriseknowledgegraph.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/firebasecrash#firebasecrashlytics.serviceAgent">Firebase Crashlytics Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      firebasecrashlytics.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/looker#looker.serviceAgent">Looker Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      looker.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/ml#ml.serviceAgent">AI Platform Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      ml.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/retail#retail.serviceAgent">Retail Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      retail.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/spectrumsas#spectrumsas.serviceAgent">Spectrum SAS Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      spectrumsas.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/visionai#visionai.serviceAgent">Cloud Vision AI Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      visionai.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.batchPredictionServiceAgent">Vertex AI Batch Prediction Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.batchPredictionServiceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.tables.createIndex" class="permission-name add-link" data-text="bigquery.tables.createIndex" tabindex="-1"><code dir="ltr" translate="no">         bigquery.tables.createIndex        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.dataScientist">Data Scientist</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.dataScientist        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.tables.createSnapshot" class="permission-name add-link" data-text="bigquery.tables.createSnapshot" tabindex="-1"><code dir="ltr" translate="no">         bigquery.tables.createSnapshot        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataViewer">BigQuery Data Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dataplex.storageDataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.dataScientist">Data Scientist</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.dataScientist        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.siteReliabilityEngineer">Site Reliability Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.siteReliabilityEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.ragServiceAgent">Vertex AI RAG Data Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.ragServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/looker#looker.serviceAgent">Looker Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      looker.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.batchPredictionServiceAgent">Vertex AI Batch Prediction Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.batchPredictionServiceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.tables.createTagBinding" class="permission-name add-link" data-text="bigquery.tables.createTagBinding" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  tables.                  createTagBinding        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/resourcemanager#resourcemanager.tagUser">Tag User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  resourcemanager.tagUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dspm#dspm.serviceAgent">DSPM Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dspm.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.tables.delete" class="permission-name add-link" data-text="bigquery.tables.delete" tabindex="-1"><code dir="ltr" translate="no">         bigquery.tables.delete        </code></h4></td>
<td><p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.routineAdmin">BigQuery Authorized Routine Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.routineAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.routineDataEditor">BigQuery Authorized Routine Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.routineDataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dataplex.storageDataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.dataScientist">Data Scientist</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.dataScientist        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/chronicle#chronicle.serviceAgent">Chronicle Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      chronicle.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/cloudasset#cloudasset.serviceAgent">Cloud Asset Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      cloudasset.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/deploymentmanager#clouddeploymentmanager.serviceAgent">Cloud Deployment Manager Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      clouddeploymentmanager.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.tuningServiceAgent">Vertex AI Tuning Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.tuningServiceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.tables.deleteIndex" class="permission-name add-link" data-text="bigquery.tables.deleteIndex" tabindex="-1"><code dir="ltr" translate="no">         bigquery.tables.deleteIndex        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.dataScientist">Data Scientist</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.dataScientist        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.tables.deleteSnapshot" class="permission-name add-link" data-text="bigquery.tables.deleteSnapshot" tabindex="-1"><code dir="ltr" translate="no">         bigquery.tables.deleteSnapshot        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dataplex.storageDataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.ragServiceAgent">Vertex AI RAG Data Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.ragServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.batchPredictionServiceAgent">Vertex AI Batch Prediction Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.batchPredictionServiceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.tables.deleteTagBinding" class="permission-name add-link" data-text="bigquery.tables.deleteTagBinding" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  tables.                  deleteTagBinding        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/resourcemanager#resourcemanager.tagUser">Tag User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  resourcemanager.tagUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dspm#dspm.serviceAgent">DSPM Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dspm.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.tables.export" class="permission-name add-link" data-text="bigquery.tables.export" tabindex="-1"><code dir="ltr" translate="no">         bigquery.tables.export        </code></h4></td>
<td><p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataViewer">BigQuery Data Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dataplex.storageDataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dataplex#dataplex.storageDataReader">Dataplex Storage Data Reader</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dataplex.storageDataReader        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.dataScientist">Data Scientist</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.dataScientist        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.siteReliabilityEngineer">Site Reliability Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.siteReliabilityEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.customCodeServiceAgent">Vertex AI Custom Code Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.customCodeServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.modelMonitoringServiceAgent">Vertex AI Model Monitoring Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.modelMonitoringServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.ragServiceAgent">Vertex AI RAG Data Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.ragServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.serviceAgent">Vertex AI Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/automl#automl.serviceAgent">AutoML Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      automl.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/automlrecommendations#automlrecommendations.serviceAgent">Recommendations AI Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      automlrecommendations.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/discoveryengine#discoveryengine.serviceAgent">Discovery Engine Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      discoveryengine.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/looker#looker.serviceAgent">Looker Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      looker.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/retail#retail.serviceAgent">Retail Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      retail.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/visionai#visionai.serviceAgent">Cloud Vision AI Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      visionai.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.batchPredictionServiceAgent">Vertex AI Batch Prediction Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.batchPredictionServiceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.tables.get" class="permission-name add-link" data-text="bigquery.tables.get" tabindex="-1"><code dir="ltr" translate="no">         bigquery.tables.get        </code></h4></td>
<td><p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataViewer">BigQuery Data Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.metadataViewer">BigQuery Metadata Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.metadataViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.routineAdmin">BigQuery Authorized Routine Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.routineAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.routineDataEditor">BigQuery Authorized Routine Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.routineDataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.routineDataViewer">BigQuery Authorized Routine Data Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.routineDataViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.routineMetadataViewer">BigQuery Authorized Routine Metadata Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.routineMetadataViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/datacatalog#datacatalog.admin">Data Catalog Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  datacatalog.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/datacatalog#datacatalog.viewer">Data Catalog Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  datacatalog.viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dataplex.storageDataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dataplex#dataplex.storageDataReader">Dataplex Storage Data Reader</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dataplex.storageDataReader        </code> )</p>
<p><a href="/iam/docs/roles-permissions/datastream#datastream.bigqueryWriter">Datastream Bigquery Writer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  datastream.bigqueryWriter        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.dataScientist">Data Scientist</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.dataScientist        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAuditor">Security Auditor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAuditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.siteReliabilityEngineer">Site Reliability Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.siteReliabilityEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.customCodeServiceAgent">Vertex AI Custom Code Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.customCodeServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.modelMonitoringServiceAgent">Vertex AI Model Monitoring Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.modelMonitoringServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.ragServiceAgent">Vertex AI RAG Data Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.ragServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.serviceAgent">Vertex AI Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.tuningServiceAgent">Vertex AI Tuning Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.tuningServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/automl#automl.serviceAgent">AutoML Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      automl.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/automlrecommendations#automlrecommendations.serviceAgent">Recommendations AI Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      automlrecommendations.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/ces#ces.serviceAgent">Customer Engagement Suite Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      ces.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/chronicle#chronicle.serviceAgent">Chronicle Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      chronicle.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/cloudasset#cloudasset.serviceAgent">Cloud Asset Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      cloudasset.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/deploymentmanager#clouddeploymentmanager.serviceAgent">Cloud Deployment Manager Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      clouddeploymentmanager.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/contactcenterinsights#contactcenterinsights.serviceAgent">Contact Center AI Insights Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      contactcenterinsights.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/container#container.serviceAgent">Kubernetes Engine Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      container.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datalabeling#datalabeling.serviceAgent">Data Labeling Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datalabeling.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datapipelines#datapipelines.serviceAgent">Datapipelines Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datapipelines.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datastream#datastream.serviceAgent">Datastream Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datastream.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dialogflow#dialogflow.serviceAgent">Dialogflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dialogflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/discoveryengine#discoveryengine.serviceAgent">Discovery Engine Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      discoveryengine.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/enterpriseknowledgegraph#enterpriseknowledgegraph.serviceAgent">Enterprise Knowledge Graph Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      enterpriseknowledgegraph.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/firebasecrash#firebasecrashlytics.serviceAgent">Firebase Crashlytics Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      firebasecrashlytics.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/looker#looker.serviceAgent">Looker Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      looker.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/ml#ml.serviceAgent">AI Platform Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      ml.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/retail#retail.serviceAgent">Retail Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      retail.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/visionai#visionai.serviceAgent">Cloud Vision AI Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      visionai.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.batchPredictionServiceAgent">Vertex AI Batch Prediction Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.batchPredictionServiceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.tables.getData" class="permission-name add-link" data-text="bigquery.tables.getData" tabindex="-1"><code dir="ltr" translate="no">         bigquery.tables.getData        </code></h4></td>
<td><p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataViewer">BigQuery Data Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.routineAdmin">BigQuery Authorized Routine Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.routineAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.routineDataEditor">BigQuery Authorized Routine Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.routineDataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.routineDataViewer">BigQuery Authorized Routine Data Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.routineDataViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dataplex.storageDataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dataplex#dataplex.storageDataReader">Dataplex Storage Data Reader</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dataplex.storageDataReader        </code> )</p>
<p><a href="/iam/docs/roles-permissions/datastream#datastream.bigqueryWriter">Datastream Bigquery Writer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  datastream.bigqueryWriter        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.dataScientist">Data Scientist</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.dataScientist        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.siteReliabilityEngineer">Site Reliability Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.siteReliabilityEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.customCodeServiceAgent">Vertex AI Custom Code Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.customCodeServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.modelMonitoringServiceAgent">Vertex AI Model Monitoring Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.modelMonitoringServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.ragServiceAgent">Vertex AI RAG Data Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.ragServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.serviceAgent">Vertex AI Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.tuningServiceAgent">Vertex AI Tuning Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.tuningServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/automl#automl.serviceAgent">AutoML Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      automl.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/automlrecommendations#automlrecommendations.serviceAgent">Recommendations AI Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      automlrecommendations.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/ces#ces.serviceAgent">Customer Engagement Suite Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      ces.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/deploymentmanager#clouddeploymentmanager.serviceAgent">Cloud Deployment Manager Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      clouddeploymentmanager.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datalabeling#datalabeling.serviceAgent">Data Labeling Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datalabeling.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datastream#datastream.serviceAgent">Datastream Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datastream.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dialogflow#dialogflow.serviceAgent">Dialogflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dialogflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/discoveryengine#discoveryengine.serviceAgent">Discovery Engine Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      discoveryengine.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dspm#dspm.serviceAgent">DSPM Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dspm.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/enterpriseknowledgegraph#enterpriseknowledgegraph.serviceAgent">Enterprise Knowledge Graph Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      enterpriseknowledgegraph.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/firebasecrash#firebasecrashlytics.serviceAgent">Firebase Crashlytics Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      firebasecrashlytics.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/fleetengine#fleetengine.serviceAgent">FleetEngine Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      fleetengine.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/looker#looker.serviceAgent">Looker Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      looker.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/ml#ml.serviceAgent">AI Platform Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      ml.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/retail#retail.serviceAgent">Retail Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      retail.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/visionai#visionai.serviceAgent">Cloud Vision AI Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      visionai.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.batchPredictionServiceAgent">Vertex AI Batch Prediction Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.batchPredictionServiceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.tables.getIamPolicy" class="permission-name add-link" data-text="bigquery.tables.getIamPolicy" tabindex="-1"><code dir="ltr" translate="no">         bigquery.tables.getIamPolicy        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataViewer">BigQuery Data Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.metadataViewer">BigQuery Metadata Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.metadataViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.dataScientist">Data Scientist</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.dataScientist        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAuditor">Security Auditor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAuditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityReviewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.siteReliabilityEngineer">Site Reliability Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.siteReliabilityEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.tables.list" class="permission-name add-link" data-text="bigquery.tables.list" tabindex="-1"><code dir="ltr" translate="no">         bigquery.tables.list        </code></h4></td>
<td><p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataViewer">BigQuery Data Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.metadataViewer">BigQuery Metadata Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.metadataViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.routineAdmin">BigQuery Authorized Routine Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.routineAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.routineDataEditor">BigQuery Authorized Routine Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.routineDataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.routineDataViewer">BigQuery Authorized Routine Data Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.routineDataViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.routineMetadataViewer">BigQuery Authorized Routine Metadata Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.routineMetadataViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.user        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dataplex.storageDataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dataplex#dataplex.storageDataReader">Dataplex Storage Data Reader</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dataplex.storageDataReader        </code> )</p>
<p><a href="/iam/docs/roles-permissions/datastream#datastream.bigqueryWriter">Datastream Bigquery Writer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  datastream.bigqueryWriter        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.dataScientist">Data Scientist</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.dataScientist        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAuditor">Security Auditor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAuditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityReviewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.siteReliabilityEngineer">Site Reliability Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.siteReliabilityEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/automlrecommendations#automlrecommendations.serviceAgent">Recommendations AI Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      automlrecommendations.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datastream#datastream.serviceAgent">Datastream Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datastream.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/discoveryengine#discoveryengine.serviceAgent">Discovery Engine Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      discoveryengine.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dspm#dspm.serviceAgent">DSPM Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dspm.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/enterpriseknowledgegraph#enterpriseknowledgegraph.serviceAgent">Enterprise Knowledge Graph Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      enterpriseknowledgegraph.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/looker#looker.serviceAgent">Looker Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      looker.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/ml#ml.serviceAgent">AI Platform Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      ml.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/retail#retail.serviceAgent">Retail Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      retail.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.tuningServiceAgent">Vertex AI Tuning Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.tuningServiceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.tables.listEffectiveTags" class="permission-name add-link" data-text="bigquery.tables.listEffectiveTags" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  tables.                  listEffectiveTags        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAuditor">Security Auditor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAuditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p><a href="/iam/docs/roles-permissions/resourcemanager#resourcemanager.tagUser">Tag User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  resourcemanager.tagUser        </code> )</p>
<p><a href="/iam/docs/roles-permissions/resourcemanager#resourcemanager.tagViewer">Tag Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  resourcemanager.tagViewer        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dspm#dspm.serviceAgent">DSPM Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dspm.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.tables.listTagBindings" class="permission-name add-link" data-text="bigquery.tables.listTagBindings" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  tables.                  listTagBindings        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAuditor">Security Auditor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAuditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p><a href="/iam/docs/roles-permissions/resourcemanager#resourcemanager.tagUser">Tag User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  resourcemanager.tagUser        </code> )</p>
<p><a href="/iam/docs/roles-permissions/resourcemanager#resourcemanager.tagViewer">Tag Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  resourcemanager.tagViewer        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dspm#dspm.serviceAgent">DSPM Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dspm.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.tables.replicateData" class="permission-name add-link" data-text="bigquery.tables.replicateData" tabindex="-1"><code dir="ltr" translate="no">         bigquery.tables.replicateData        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataViewer">BigQuery Data Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataViewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.dataScientist">Data Scientist</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.dataScientist        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.siteReliabilityEngineer">Site Reliability Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.siteReliabilityEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.tables.restoreSnapshot" class="permission-name add-link" data-text="bigquery.tables.restoreSnapshot" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  tables.                  restoreSnapshot        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dataplex.storageDataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.dataScientist">Data Scientist</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.dataScientist        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.ragServiceAgent">Vertex AI RAG Data Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.ragServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.batchPredictionServiceAgent">Vertex AI Batch Prediction Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.batchPredictionServiceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.tables.setCategory" class="permission-name add-link" data-text="bigquery.tables.setCategory" tabindex="-1"><code dir="ltr" translate="no">         bigquery.tables.setCategory        </code></h4></td>
<td><p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/deploymentmanager#clouddeploymentmanager.serviceAgent">Cloud Deployment Manager Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      clouddeploymentmanager.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.tables.setColumnDataPolicy" class="permission-name add-link" data-text="bigquery.tables.setColumnDataPolicy" tabindex="-1"><code dir="ltr" translate="no">         bigquery.                  tables.                  setColumnDataPolicy        </code></h4></td>
<td><p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.tables.setIamPolicy" class="permission-name add-link" data-text="bigquery.tables.setIamPolicy" tabindex="-1"><code dir="ltr" translate="no">         bigquery.tables.setIamPolicy        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAdmin        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.tables.update" class="permission-name add-link" data-text="bigquery.tables.update" tabindex="-1"><code dir="ltr" translate="no">         bigquery.tables.update        </code></h4></td>
<td><p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.routineAdmin">BigQuery Authorized Routine Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.routineAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.routineDataEditor">BigQuery Authorized Routine Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.routineDataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dataplex.storageDataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/datastream#datastream.bigqueryWriter">Datastream Bigquery Writer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  datastream.bigqueryWriter        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.dataScientist">Data Scientist</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.dataScientist        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.customCodeServiceAgent">Vertex AI Custom Code Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.customCodeServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.modelMonitoringServiceAgent">Vertex AI Model Monitoring Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.modelMonitoringServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.ragServiceAgent">Vertex AI RAG Data Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.ragServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.serviceAgent">Vertex AI Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.tuningServiceAgent">Vertex AI Tuning Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.tuningServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/automl#automl.serviceAgent">AutoML Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      automl.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/automlrecommendations#automlrecommendations.serviceAgent">Recommendations AI Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      automlrecommendations.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/bigquery#bigquery.connectedSheetsServiceAgent">Connected Sheets Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      bigquery.connectedSheetsServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/ces#ces.serviceAgent">Customer Engagement Suite Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      ces.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/chronicle#chronicle.serviceAgent">Chronicle Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      chronicle.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/cloudasset#cloudasset.serviceAgent">Cloud Asset Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      cloudasset.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/deploymentmanager#clouddeploymentmanager.serviceAgent">Cloud Deployment Manager Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      clouddeploymentmanager.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/contactcenterinsights#contactcenterinsights.serviceAgent">Contact Center AI Insights Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      contactcenterinsights.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/container#container.serviceAgent">Kubernetes Engine Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      container.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datastream#datastream.serviceAgent">Datastream Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datastream.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/discoveryengine#discoveryengine.serviceAgent">Discovery Engine Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      discoveryengine.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/enterpriseknowledgegraph#enterpriseknowledgegraph.serviceAgent">Enterprise Knowledge Graph Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      enterpriseknowledgegraph.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/firebasecrash#firebasecrashlytics.serviceAgent">Firebase Crashlytics Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      firebasecrashlytics.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/retail#retail.serviceAgent">Retail Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      retail.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/visionai#visionai.serviceAgent">Cloud Vision AI Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      visionai.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.batchPredictionServiceAgent">Vertex AI Batch Prediction Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.batchPredictionServiceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.tables.updateData" class="permission-name add-link" data-text="bigquery.tables.updateData" tabindex="-1"><code dir="ltr" translate="no">         bigquery.tables.updateData        </code></h4></td>
<td><p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.routineAdmin">BigQuery Authorized Routine Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.routineAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.routineDataEditor">BigQuery Authorized Routine Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.routineDataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dataplex#dataplex.storageDataOwner">Dataplex Storage Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dataplex.storageDataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dataplex#dataplex.storageDataWriter">Dataplex Storage Data Writer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dataplex.storageDataWriter        </code> )</p>
<p><a href="/iam/docs/roles-permissions/datastream#datastream.bigqueryWriter">Datastream Bigquery Writer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  datastream.bigqueryWriter        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.dataScientist">Data Scientist</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.dataScientist        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.customCodeServiceAgent">Vertex AI Custom Code Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.customCodeServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.modelMonitoringServiceAgent">Vertex AI Model Monitoring Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.modelMonitoringServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.ragServiceAgent">Vertex AI RAG Data Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.ragServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.serviceAgent">Vertex AI Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.tuningServiceAgent">Vertex AI Tuning Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.tuningServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/automl#automl.serviceAgent">AutoML Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      automl.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/automlrecommendations#automlrecommendations.serviceAgent">Recommendations AI Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      automlrecommendations.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/bigquery#bigquery.connectedSheetsServiceAgent">Connected Sheets Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      bigquery.connectedSheetsServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/bigqueryomni#bigqueryomni.serviceAgent">BigQuery Omni Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      bigqueryomni.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/ces#ces.serviceAgent">Customer Engagement Suite Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      ces.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/chronicle#chronicle.serviceAgent">Chronicle Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      chronicle.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/cloudasset#cloudasset.serviceAgent">Cloud Asset Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      cloudasset.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/deploymentmanager#clouddeploymentmanager.serviceAgent">Cloud Deployment Manager Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      clouddeploymentmanager.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/contactcenterinsights#contactcenterinsights.serviceAgent">Contact Center AI Insights Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      contactcenterinsights.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/container#container.serviceAgent">Kubernetes Engine Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      container.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/datastream#datastream.serviceAgent">Datastream Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datastream.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dialogflow#dialogflow.serviceAgent">Dialogflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dialogflow.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/discoveryengine#discoveryengine.serviceAgent">Discovery Engine Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      discoveryengine.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/enterpriseknowledgegraph#enterpriseknowledgegraph.serviceAgent">Enterprise Knowledge Graph Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      enterpriseknowledgegraph.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/firebasecrash#firebasecrashlytics.serviceAgent">Firebase Crashlytics Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      firebasecrashlytics.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/ml#ml.serviceAgent">AI Platform Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      ml.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/retail#retail.serviceAgent">Retail Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      retail.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/spectrumsas#spectrumsas.serviceAgent">Spectrum SAS Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      spectrumsas.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/visionai#visionai.serviceAgent">Cloud Vision AI Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      visionai.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/aiplatform#aiplatform.batchPredictionServiceAgent">Vertex AI Batch Prediction Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      aiplatform.batchPredictionServiceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.tables.updateIndex" class="permission-name add-link" data-text="bigquery.tables.updateIndex" tabindex="-1"><code dir="ltr" translate="no">         bigquery.tables.updateIndex        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.dataScientist">Data Scientist</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.dataScientist        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.tables.updateTag" class="permission-name add-link" data-text="bigquery.tables.updateTag" tabindex="-1"><code dir="ltr" translate="no">         bigquery.tables.updateTag        </code></h4></td>
<td><p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataEditor">BigQuery Data Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.dataOwner">BigQuery Data Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.dataOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.securityAdmin">BigQuery Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/datacatalog#datacatalog.admin">Data Catalog Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  datacatalog.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/datacatalog#datacatalog.tagEditor">Data Catalog Tag Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  datacatalog.tagEditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.dataScientist">Data Scientist</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.dataScientist        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.mlEngineer">ML Engineer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.mlEngineer        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/datafusion#datafusion.serviceAgent">Cloud Data Fusion API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      datafusion.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dlp#dlp.serviceAgent">DLP API Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dlp.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquery.transfers.get" class="permission-name add-link" data-text="bigquery.transfers.get" tabindex="-1"><code dir="ltr" translate="no">         bigquery.transfers.get        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.user        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/firebase#firebase.managementServiceAgent">Firebase Service Management Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      firebase.managementServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="odd">
<td><h4 id="bigquery.transfers.update" class="permission-name add-link" data-text="bigquery.transfers.update" tabindex="-1"><code dir="ltr" translate="no">         bigquery.transfers.update        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/firebase#firebase.managementServiceAgent">Firebase Service Management Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      firebase.managementServiceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
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

This table lists the IAM permissions for BigQuery Engine for Apache Flink and the roles that include them. To search through all roles and permissions, see the [role and permission index](/iam/docs/roles-permissions) .

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
<td><h4 id="managedflink.deployments.create" class="permission-name add-link" data-text="managedflink.deployments.create" tabindex="-1"><code dir="ltr" translate="no">         managedflink.                  deployments.                  create        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.admin">Managed Flink Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.admin        </code> )</p></td>
</tr>
<tr class="even">
<td><h4 id="managedflink.deployments.delete" class="permission-name add-link" data-text="managedflink.deployments.delete" tabindex="-1"><code dir="ltr" translate="no">         managedflink.                  deployments.                  delete        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.admin">Managed Flink Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.admin        </code> )</p></td>
</tr>
<tr class="odd">
<td><h4 id="managedflink.deployments.get" class="permission-name add-link" data-text="managedflink.deployments.get" tabindex="-1"><code dir="ltr" translate="no">         managedflink.deployments.get        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.admin">Managed Flink Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.developer">Managed Flink Developer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.developer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.viewer">Managed Flink Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.viewer        </code> )</p></td>
</tr>
<tr class="even">
<td><h4 id="managedflink.deployments.list" class="permission-name add-link" data-text="managedflink.deployments.list" tabindex="-1"><code dir="ltr" translate="no">         managedflink.deployments.list        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAuditor">Security Auditor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAuditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityReviewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.admin">Managed Flink Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.developer">Managed Flink Developer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.developer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.viewer">Managed Flink Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.viewer        </code> )</p></td>
</tr>
<tr class="odd">
<td><h4 id="managedflink.deployments.update" class="permission-name add-link" data-text="managedflink.deployments.update" tabindex="-1"><code dir="ltr" translate="no">         managedflink.                  deployments.                  update        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.admin">Managed Flink Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.admin        </code> )</p></td>
</tr>
<tr class="even">
<td><h4 id="managedflink.jobs.create" class="permission-name add-link" data-text="managedflink.jobs.create" tabindex="-1"><code dir="ltr" translate="no">         managedflink.jobs.create        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.admin">Managed Flink Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.developer">Managed Flink Developer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.developer        </code> )</p></td>
</tr>
<tr class="odd">
<td><h4 id="managedflink.jobs.delete" class="permission-name add-link" data-text="managedflink.jobs.delete" tabindex="-1"><code dir="ltr" translate="no">         managedflink.jobs.delete        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.admin">Managed Flink Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.developer">Managed Flink Developer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.developer        </code> )</p></td>
</tr>
<tr class="even">
<td><h4 id="managedflink.jobs.get" class="permission-name add-link" data-text="managedflink.jobs.get" tabindex="-1"><code dir="ltr" translate="no">         managedflink.jobs.get        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.admin">Managed Flink Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.developer">Managed Flink Developer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.developer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.viewer">Managed Flink Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.viewer        </code> )</p></td>
</tr>
<tr class="odd">
<td><h4 id="managedflink.jobs.list" class="permission-name add-link" data-text="managedflink.jobs.list" tabindex="-1"><code dir="ltr" translate="no">         managedflink.jobs.list        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAuditor">Security Auditor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAuditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityReviewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.admin">Managed Flink Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.developer">Managed Flink Developer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.developer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.viewer">Managed Flink Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.viewer        </code> )</p></td>
</tr>
<tr class="even">
<td><h4 id="managedflink.jobs.update" class="permission-name add-link" data-text="managedflink.jobs.update" tabindex="-1"><code dir="ltr" translate="no">         managedflink.jobs.update        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.admin">Managed Flink Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.developer">Managed Flink Developer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.developer        </code> )</p></td>
</tr>
<tr class="odd">
<td><h4 id="managedflink.locations.get" class="permission-name add-link" data-text="managedflink.locations.get" tabindex="-1"><code dir="ltr" translate="no">         managedflink.locations.get        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.admin">Managed Flink Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.developer">Managed Flink Developer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.developer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.viewer">Managed Flink Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.viewer        </code> )</p></td>
</tr>
<tr class="even">
<td><h4 id="managedflink.locations.list" class="permission-name add-link" data-text="managedflink.locations.list" tabindex="-1"><code dir="ltr" translate="no">         managedflink.locations.list        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAuditor">Security Auditor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAuditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityReviewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.admin">Managed Flink Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.developer">Managed Flink Developer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.developer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.viewer">Managed Flink Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.viewer        </code> )</p></td>
</tr>
<tr class="odd">
<td><h4 id="managedflink.operations.cancel" class="permission-name add-link" data-text="managedflink.operations.cancel" tabindex="-1"><code dir="ltr" translate="no">         managedflink.operations.cancel        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.admin">Managed Flink Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.admin        </code> )</p></td>
</tr>
<tr class="even">
<td><h4 id="managedflink.operations.delete" class="permission-name add-link" data-text="managedflink.operations.delete" tabindex="-1"><code dir="ltr" translate="no">         managedflink.operations.delete        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.admin">Managed Flink Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.admin        </code> )</p></td>
</tr>
<tr class="odd">
<td><h4 id="managedflink.operations.get" class="permission-name add-link" data-text="managedflink.operations.get" tabindex="-1"><code dir="ltr" translate="no">         managedflink.operations.get        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.admin">Managed Flink Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.developer">Managed Flink Developer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.developer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.viewer">Managed Flink Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.viewer        </code> )</p></td>
</tr>
<tr class="even">
<td><h4 id="managedflink.operations.list" class="permission-name add-link" data-text="managedflink.operations.list" tabindex="-1"><code dir="ltr" translate="no">         managedflink.operations.list        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAuditor">Security Auditor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAuditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityReviewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.admin">Managed Flink Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.developer">Managed Flink Developer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.developer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.viewer">Managed Flink Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.viewer        </code> )</p></td>
</tr>
<tr class="odd">
<td><h4 id="managedflink.sessions.create" class="permission-name add-link" data-text="managedflink.sessions.create" tabindex="-1"><code dir="ltr" translate="no">         managedflink.sessions.create        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.admin">Managed Flink Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.developer">Managed Flink Developer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.developer        </code> )</p></td>
</tr>
<tr class="even">
<td><h4 id="managedflink.sessions.delete" class="permission-name add-link" data-text="managedflink.sessions.delete" tabindex="-1"><code dir="ltr" translate="no">         managedflink.sessions.delete        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.admin">Managed Flink Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.developer">Managed Flink Developer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.developer        </code> )</p></td>
</tr>
<tr class="odd">
<td><h4 id="managedflink.sessions.get" class="permission-name add-link" data-text="managedflink.sessions.get" tabindex="-1"><code dir="ltr" translate="no">         managedflink.sessions.get        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.admin">Managed Flink Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.developer">Managed Flink Developer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.developer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.viewer">Managed Flink Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.viewer        </code> )</p></td>
</tr>
<tr class="even">
<td><h4 id="managedflink.sessions.list" class="permission-name add-link" data-text="managedflink.sessions.list" tabindex="-1"><code dir="ltr" translate="no">         managedflink.sessions.list        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAuditor">Security Auditor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAuditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityReviewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.admin">Managed Flink Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.developer">Managed Flink Developer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.developer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.viewer">Managed Flink Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.viewer        </code> )</p></td>
</tr>
<tr class="odd">
<td><h4 id="managedflink.sessions.update" class="permission-name add-link" data-text="managedflink.sessions.update" tabindex="-1"><code dir="ltr" translate="no">         managedflink.sessions.update        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.admin">Managed Flink Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/managedflink#managedflink.developer">Managed Flink Developer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  managedflink.developer        </code> )</p></td>
</tr>
</tbody>
</table>

### BigQuery Migration Service permissions

This table lists the IAM permissions for BigQuery Migration Service and the roles that include them. To search through all roles and permissions, see the [role and permission index](/iam/docs/roles-permissions) .

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
<td><h4 id="bigquerymigration.subtasks.get" class="permission-name add-link" data-text="bigquerymigration.subtasks.get" tabindex="-1"><code dir="ltr" translate="no">         bigquerymigration.subtasks.get        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.editor">MigrationWorkflow Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquerymigration.editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.viewer">MigrationWorkflow Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquerymigration.viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p></td>
</tr>
<tr class="even">
<td><h4 id="bigquerymigration.subtasks.list" class="permission-name add-link" data-text="bigquerymigration.subtasks.list" tabindex="-1"><code dir="ltr" translate="no">         bigquerymigration.                  subtasks.                  list        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.editor">MigrationWorkflow Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquerymigration.editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.viewer">MigrationWorkflow Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquerymigration.viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAuditor">Security Auditor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAuditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityReviewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p></td>
</tr>
<tr class="odd">
<td><h4 id="bigquerymigration.translation.translate" class="permission-name add-link" data-text="bigquerymigration.translation.translate" tabindex="-1"><code dir="ltr" translate="no">         bigquerymigration.                  translation.                  translate        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.admin">BigQuery Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.studioAdmin">BigQuery Studio Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.studioAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquery#bigquery.user">BigQuery User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquery.user        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.translationUser">Migration Translation User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquerymigration.translationUser        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.orgdriver">DLP Organization Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.orgdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/dlp#dlp.projectdriver">DLP Project Data Profiles Driver</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  dlp.projectdriver        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.databasesAdmin">Databases Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.databasesAdmin        </code> )</p>
<p>Service agent roles</p>
<strong>Warning:</strong> Don't grant service agent roles to any principals except <a href="/iam/docs/service-agents">service agents</a> .
<ul>
<li><a href="/iam/docs/roles-permissions/dataplex#dataplex.serviceAgent">Cloud Dataplex Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataplex.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataprep#dataprep.serviceAgent">Dataprep Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataprep.serviceAgent          </code> )</li>
<li><a href="/iam/docs/roles-permissions/dataflow#dataflow.serviceAgent">Cloud Dataflow Service Agent</a> ( <code class="role-name" dir="ltr" translate="no">           roles/                      dataflow.serviceAgent          </code> )</li>
</ul></td>
</tr>
<tr class="even">
<td><h4 id="bigquerymigration.workflows.create" class="permission-name add-link" data-text="bigquerymigration.workflows.create" tabindex="-1"><code dir="ltr" translate="no">         bigquerymigration.                  workflows.                  create        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.editor">MigrationWorkflow Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquerymigration.editor        </code> )</p></td>
</tr>
<tr class="odd">
<td><h4 id="bigquerymigration.workflows.delete" class="permission-name add-link" data-text="bigquerymigration.workflows.delete" tabindex="-1"><code dir="ltr" translate="no">         bigquerymigration.                  workflows.                  delete        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.editor">MigrationWorkflow Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquerymigration.editor        </code> )</p></td>
</tr>
<tr class="even">
<td><h4 id="bigquerymigration.workflows.enableAiOutputTypes" class="permission-name add-link" data-text="bigquerymigration.workflows.enableAiOutputTypes" tabindex="-1"><code dir="ltr" translate="no">         bigquerymigration.                  workflows.                  enableAiOutputTypes        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.editor">MigrationWorkflow Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquerymigration.editor        </code> )</p></td>
</tr>
<tr class="odd">
<td><h4 id="bigquerymigration.workflows.enableLineageOutputTypes" class="permission-name add-link" data-text="bigquerymigration.workflows.enableLineageOutputTypes" tabindex="-1"><code dir="ltr" translate="no">         bigquerymigration.                  workflows.                  enableLineageOutputTypes        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.editor">MigrationWorkflow Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquerymigration.editor        </code> )</p></td>
</tr>
<tr class="even">
<td><h4 id="bigquerymigration.workflows.enableOutputTypePermissions" class="permission-name add-link" data-text="bigquerymigration.workflows.enableOutputTypePermissions" tabindex="-1"><code dir="ltr" translate="no">         bigquerymigration.                  workflows.                  enableOutputTypePermissions        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.editor">MigrationWorkflow Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquerymigration.editor        </code> )</p></td>
</tr>
<tr class="odd">
<td><h4 id="bigquerymigration.workflows.get" class="permission-name add-link" data-text="bigquerymigration.workflows.get" tabindex="-1"><code dir="ltr" translate="no">         bigquerymigration.                  workflows.                  get        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.editor">MigrationWorkflow Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquerymigration.editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.viewer">MigrationWorkflow Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquerymigration.viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p></td>
</tr>
<tr class="even">
<td><h4 id="bigquerymigration.workflows.list" class="permission-name add-link" data-text="bigquerymigration.workflows.list" tabindex="-1"><code dir="ltr" translate="no">         bigquerymigration.                  workflows.                  list        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.editor">MigrationWorkflow Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquerymigration.editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.viewer">MigrationWorkflow Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquerymigration.viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAuditor">Security Auditor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAuditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityReviewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p></td>
</tr>
<tr class="odd">
<td><h4 id="bigquerymigration.workflows.orchestrateTask" class="permission-name add-link" data-text="bigquerymigration.workflows.orchestrateTask" tabindex="-1"><code dir="ltr" translate="no">         bigquerymigration.                  workflows.                  orchestrateTask        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.orchestrator">Task Orchestrator</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquerymigration.orchestrator        </code> )</p></td>
</tr>
<tr class="even">
<td><h4 id="bigquerymigration.workflows.update" class="permission-name add-link" data-text="bigquerymigration.workflows.update" tabindex="-1"><code dir="ltr" translate="no">         bigquerymigration.                  workflows.                  update        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/bigquerymigration#bigquerymigration.editor">MigrationWorkflow Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  bigquerymigration.editor        </code> )</p></td>
</tr>
</tbody>
</table>

### BigQuery Omni permissions

There are no IAM permissions for this service.

### BigQuery sharing permissions

This table lists the IAM permissions for BigQuery sharing and the roles that include them. To search through all roles and permissions, see the [role and permission index](/iam/docs/roles-permissions) .

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
<td><h4 id="analyticshub.dataExchanges.create" class="permission-name add-link" data-text="analyticshub.dataExchanges.create" tabindex="-1"><code dir="ltr" translate="no">         analyticshub.                  dataExchanges.                  create        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.admin        </code> )</p></td>
</tr>
<tr class="even">
<td><h4 id="analyticshub.dataExchanges.delete" class="permission-name add-link" data-text="analyticshub.dataExchanges.delete" tabindex="-1"><code dir="ltr" translate="no">         analyticshub.                  dataExchanges.                  delete        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.admin        </code> )</p></td>
</tr>
<tr class="odd">
<td><h4 id="analyticshub.dataExchanges.get" class="permission-name add-link" data-text="analyticshub.dataExchanges.get" tabindex="-1"><code dir="ltr" translate="no">         analyticshub.dataExchanges.get        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.listingAdmin">Analytics Hub Listing Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.listingAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.publisher">Analytics Hub Publisher</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.publisher        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.subscriber">Analytics Hub Subscriber</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.subscriber        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.subscriptionOwner">Analytics Hub Subscription Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.subscriptionOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.viewer">Analytics Hub Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p></td>
</tr>
<tr class="even">
<td><h4 id="analyticshub.dataExchanges.getIamPolicy" class="permission-name add-link" data-text="analyticshub.dataExchanges.getIamPolicy" tabindex="-1"><code dir="ltr" translate="no">         analyticshub.                  dataExchanges.                  getIamPolicy        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.listingAdmin">Analytics Hub Listing Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.listingAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.publisher">Analytics Hub Publisher</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.publisher        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.subscriber">Analytics Hub Subscriber</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.subscriber        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.subscriptionOwner">Analytics Hub Subscription Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.subscriptionOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.viewer">Analytics Hub Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAuditor">Security Auditor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAuditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityReviewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p></td>
</tr>
<tr class="odd">
<td><h4 id="analyticshub.dataExchanges.list" class="permission-name add-link" data-text="analyticshub.dataExchanges.list" tabindex="-1"><code dir="ltr" translate="no">         analyticshub.                  dataExchanges.                  list        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.listingAdmin">Analytics Hub Listing Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.listingAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.publisher">Analytics Hub Publisher</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.publisher        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.subscriber">Analytics Hub Subscriber</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.subscriber        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.subscriptionOwner">Analytics Hub Subscription Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.subscriptionOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.viewer">Analytics Hub Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAuditor">Security Auditor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAuditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityReviewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p></td>
</tr>
<tr class="even">
<td><h4 id="analyticshub.dataExchanges.setIamPolicy" class="permission-name add-link" data-text="analyticshub.dataExchanges.setIamPolicy" tabindex="-1"><code dir="ltr" translate="no">         analyticshub.                  dataExchanges.                  setIamPolicy        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAdmin        </code> )</p></td>
</tr>
<tr class="odd">
<td><h4 id="analyticshub.dataExchanges.subscribe" class="permission-name add-link" data-text="analyticshub.dataExchanges.subscribe" tabindex="-1"><code dir="ltr" translate="no">         analyticshub.                  dataExchanges.                  subscribe        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.subscriber">Analytics Hub Subscriber</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.subscriber        </code> )</p></td>
</tr>
<tr class="even">
<td><h4 id="analyticshub.dataExchanges.update" class="permission-name add-link" data-text="analyticshub.dataExchanges.update" tabindex="-1"><code dir="ltr" translate="no">         analyticshub.                  dataExchanges.                  update        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.admin        </code> )</p></td>
</tr>
<tr class="odd">
<td><h4 id="analyticshub.dataExchanges.viewSubscriptions" class="permission-name add-link" data-text="analyticshub.dataExchanges.viewSubscriptions" tabindex="-1"><code dir="ltr" translate="no">         analyticshub.                  dataExchanges.                  viewSubscriptions        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.admin        </code> )</p></td>
</tr>
<tr class="even">
<td><h4 id="analyticshub.listings.create" class="permission-name add-link" data-text="analyticshub.listings.create" tabindex="-1"><code dir="ltr" translate="no">         analyticshub.listings.create        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.publisher">Analytics Hub Publisher</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.publisher        </code> )</p></td>
</tr>
<tr class="odd">
<td><h4 id="analyticshub.listings.delete" class="permission-name add-link" data-text="analyticshub.listings.delete" tabindex="-1"><code dir="ltr" translate="no">         analyticshub.listings.delete        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.listingAdmin">Analytics Hub Listing Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.listingAdmin        </code> )</p></td>
</tr>
<tr class="even">
<td><h4 id="analyticshub.listings.get" class="permission-name add-link" data-text="analyticshub.listings.get" tabindex="-1"><code dir="ltr" translate="no">         analyticshub.listings.get        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.listingAdmin">Analytics Hub Listing Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.listingAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.publisher">Analytics Hub Publisher</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.publisher        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.subscriber">Analytics Hub Subscriber</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.subscriber        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.subscriptionOwner">Analytics Hub Subscription Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.subscriptionOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.viewer">Analytics Hub Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p></td>
</tr>
<tr class="odd">
<td><h4 id="analyticshub.listings.getIamPolicy" class="permission-name add-link" data-text="analyticshub.listings.getIamPolicy" tabindex="-1"><code dir="ltr" translate="no">         analyticshub.                  listings.                  getIamPolicy        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.listingAdmin">Analytics Hub Listing Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.listingAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.publisher">Analytics Hub Publisher</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.publisher        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.subscriber">Analytics Hub Subscriber</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.subscriber        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.subscriptionOwner">Analytics Hub Subscription Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.subscriptionOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.viewer">Analytics Hub Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAuditor">Security Auditor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAuditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityReviewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p></td>
</tr>
<tr class="even">
<td><h4 id="analyticshub.listings.list" class="permission-name add-link" data-text="analyticshub.listings.list" tabindex="-1"><code dir="ltr" translate="no">         analyticshub.listings.list        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.listingAdmin">Analytics Hub Listing Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.listingAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.publisher">Analytics Hub Publisher</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.publisher        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.subscriber">Analytics Hub Subscriber</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.subscriber        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.subscriptionOwner">Analytics Hub Subscription Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.subscriptionOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.viewer">Analytics Hub Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAuditor">Security Auditor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAuditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityReviewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p></td>
</tr>
<tr class="odd">
<td><h4 id="analyticshub.listings.setIamPolicy" class="permission-name add-link" data-text="analyticshub.listings.setIamPolicy" tabindex="-1"><code dir="ltr" translate="no">         analyticshub.                  listings.                  setIamPolicy        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.listingAdmin">Analytics Hub Listing Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.listingAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAdmin        </code> )</p></td>
</tr>
<tr class="even">
<td><h4 id="analyticshub.listings.subscribe" class="permission-name add-link" data-text="analyticshub.listings.subscribe" tabindex="-1"><code dir="ltr" translate="no">         analyticshub.                  listings.                  subscribe        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.subscriber">Analytics Hub Subscriber</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.subscriber        </code> )</p></td>
</tr>
<tr class="odd">
<td><h4 id="analyticshub.listings.update" class="permission-name add-link" data-text="analyticshub.listings.update" tabindex="-1"><code dir="ltr" translate="no">         analyticshub.listings.update        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.listingAdmin">Analytics Hub Listing Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.listingAdmin        </code> )</p></td>
</tr>
<tr class="even">
<td><h4 id="analyticshub.listings.viewSubscriptions" class="permission-name add-link" data-text="analyticshub.listings.viewSubscriptions" tabindex="-1"><code dir="ltr" translate="no">         analyticshub.                  listings.                  viewSubscriptions        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.listingAdmin">Analytics Hub Listing Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.listingAdmin        </code> )</p></td>
</tr>
<tr class="odd">
<td><h4 id="analyticshub.subscriptions.create" class="permission-name add-link" data-text="analyticshub.subscriptions.create" tabindex="-1"><code dir="ltr" translate="no">         analyticshub.                  subscriptions.                  create        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.subscriptionOwner">Analytics Hub Subscription Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.subscriptionOwner        </code> )</p></td>
</tr>
<tr class="even">
<td><h4 id="analyticshub.subscriptions.delete" class="permission-name add-link" data-text="analyticshub.subscriptions.delete" tabindex="-1"><code dir="ltr" translate="no">         analyticshub.                  subscriptions.                  delete        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.subscriptionOwner">Analytics Hub Subscription Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.subscriptionOwner        </code> )</p></td>
</tr>
<tr class="odd">
<td><h4 id="analyticshub.subscriptions.get" class="permission-name add-link" data-text="analyticshub.subscriptions.get" tabindex="-1"><code dir="ltr" translate="no">         analyticshub.subscriptions.get        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.subscriptionOwner">Analytics Hub Subscription Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.subscriptionOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p></td>
</tr>
<tr class="even">
<td><h4 id="analyticshub.subscriptions.list" class="permission-name add-link" data-text="analyticshub.subscriptions.list" tabindex="-1"><code dir="ltr" translate="no">         analyticshub.                  subscriptions.                  list        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Viewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  viewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.subscriptionOwner">Analytics Hub Subscription Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.subscriptionOwner        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAdmin">Security Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAdmin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityAuditor">Security Auditor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityAuditor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.securityReviewer">Security Reviewer</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.securityReviewer        </code> )</p>
<p><a href="/iam/docs/roles-permissions/iam#iam.supportUser">Support User</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  iam.supportUser        </code> )</p></td>
</tr>
<tr class="odd">
<td><h4 id="analyticshub.subscriptions.update" class="permission-name add-link" data-text="analyticshub.subscriptions.update" tabindex="-1"><code dir="ltr" translate="no">         analyticshub.                  subscriptions.                  update        </code></h4></td>
<td><p><a href="/iam/docs/roles-overview#basic">Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  owner        </code> )</p>
<p><a href="/iam/docs/roles-overview#basic">Editor</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  editor        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.admin">Analytics Hub Admin</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.admin        </code> )</p>
<p><a href="/iam/docs/roles-permissions/analyticshub#analyticshub.subscriptionOwner">Analytics Hub Subscription Owner</a> ( <code class="role-name" dir="ltr" translate="no">         roles/                  analyticshub.subscriptionOwner        </code> )</p></td>
</tr>
</tbody>
</table>

## Permissions for BigQuery ML tasks

The following table describes the permissions needed for common BigQuery ML tasks.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Permission</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.jobs.create      </code><br />
<code dir="ltr" translate="no">       bigquery.models.create      </code><br />
<code dir="ltr" translate="no">       bigquery.models.getData      </code><br />
<code dir="ltr" translate="no">       bigquery.models.updateData      </code><br />
</td>
<td>Create a new model using <code dir="ltr" translate="no">       CREATE MODEL      </code> statement</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.jobs.create      </code><br />
<code dir="ltr" translate="no">       bigquery.models.create      </code><br />
<code dir="ltr" translate="no">       bigquery.models.getData      </code><br />
<code dir="ltr" translate="no">       bigquery.models.updateData      </code><br />
<code dir="ltr" translate="no">       bigquery.models.updateMetadata      </code><br />
</td>
<td>Replace an existing model using <code dir="ltr" translate="no">       CREATE OR REPLACE MODEL      </code> statement</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.models.delete      </code></td>
<td>Delete model using <a href="/bigquery/docs/reference/rest/v2/models/delete">models.delete</a> API</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.jobs.create      </code><br />
<code dir="ltr" translate="no">       bigquery.models.delete      </code><br />
</td>
<td>Delete model using <code dir="ltr" translate="no">       DROP MODEL      </code> statement</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.models.getMetadata      </code></td>
<td>Get model metadata using <a href="/bigquery/docs/reference/rest/v2/models/get">models.get</a> API</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.models.list      </code></td>
<td>List models and metadata on models using <a href="/bigquery/docs/reference/rest/v2/models/list">models.list</a> API</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.models.updateMetadata      </code></td>
<td>Update model metadata using <a href="/bigquery/docs/reference/rest/v2/models/delete">models.delete</a> API. If setting or updating a non-zero expiration time for Model, <code dir="ltr" translate="no">       bigquery.models.delete      </code> permission is also needed</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.jobs.create      </code><br />
<code dir="ltr" translate="no">       bigquery.models.getData      </code></td>
<td>Perform evaluation, prediction and model and feature inspections using functions such as <code dir="ltr" translate="no">       ML.EVALUATE      </code> , <code dir="ltr" translate="no">       ML.PREDICT      </code> , <code dir="ltr" translate="no">       ML.TRAINING_INFO      </code> , and <code dir="ltr" translate="no">       ML.WEIGHTS      </code> .</td>
</tr>
<tr class="odd">
<td><code dir="ltr" translate="no">       bigquery.jobs.create      </code><br />
<code dir="ltr" translate="no">       bigquery.models.export      </code></td>
<td>Export a model</td>
</tr>
<tr class="even">
<td><code dir="ltr" translate="no">       bigquery.models.updateTag      </code></td>
<td>Update <a href="/data-catalog/docs/tags-and-tag-templates">Data Catalog tags</a> for a model.</td>
</tr>
</tbody>
</table>

## What's next

  - For more information about assigning roles at the dataset level, see [Controlling access to datasets](/bigquery/docs/dataset-access-controls) .
  - For more information about assigning roles at the table or view level, see [Controlling access to tables and views](/bigquery/docs/table-access-controls) .
