# Create and manage folders

**Preview**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

**Note:** To give feedback or request support for this feature, send an email to <bigquery-explorer-feedback@google.com> .

The following document describes how create and manage folders in BigQuery. You can use folders to organize and control access to single file code assets, such as [notebooks](/bigquery/docs/create-notebooks) , [saved queries](/bigquery/docs/work-with-saved-queries) , [data canvases](/bigquery/docs/data-canvas) , and [data preparation](/bigquery/docs/data-prep-get-suggestions) files. BigQuery offers user folders for individuals to manage their own code assets, and team folders to manage a team's code assets.

BigQuery folders are powered by [Dataform](/dataform/docs/overview) .

Before creating folders, learn how BigQuery folders work by reading [Organize code assets with folders](/bigquery/docs/code-asset-folders) .

## Before you begin

### Required roles

To get the permissions that you need to complete the tasks in this document, ask your administrator to grant you the appropriate IAM roles on the project, folder, or resource.

To get the permissions that you need to use the BigQuery file browser, ask your administrator to grant you the [BigQuery User](/bigquery/docs/access-control#bigquery.user) ( `  roles/bigquery.user  ` ) or [BigQuery Studio User](/bigquery/docs/access-control#bigquery.studioUser) ( `  roles/bigquery.studioUser  ` ) role on the project.

Permissions granted on a folder propagate to all the files and folders contained within it.

The following apply to files and the folders that contain them:

<table>
<thead>
<tr class="header">
<th style="text-align: left;">Role</th>
<th style="text-align: left;">Granted on</th>
<th style="text-align: left;">Permissions and use cases</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><a href="/iam/docs/roles-permissions/dataform#dataform.codeOwner">Code Owner</a> ( <code dir="ltr" translate="no">       roles/dataform.codeOwner      </code> )</td>
<td style="text-align: left;">File or folder</td>
<td style="text-align: left;">Grants full control over a resource in the files and folders system. A user with this role can perform all actions, including deleting the resource, setting its IAM policy, and moving it.</td>
</tr>
<tr class="even">
<td style="text-align: left;"><a href="/iam/docs/roles-permissions/dataform#dataform.codeEditor">Code Editor</a> ( <code dir="ltr" translate="no">       roles/dataform.codeEditor      </code> )</td>
<td style="text-align: left;">File or folder</td>
<td style="text-align: left;">Allows for editing and managing content. A user with this role can add content to folders, edit files, and get the IAM policy for a file or folder. This role is also required on the destination folder when moving a resource.</td>
</tr>
<tr class="odd">
<td style="text-align: left;"><a href="/iam/docs/roles-permissions/dataform#dataform.codeCommenter">Code Commenter</a> ( <code dir="ltr" translate="no">       roles/dataform.codeCommenter      </code> )</td>
<td style="text-align: left;">File or folder</td>
<td style="text-align: left;">Allows for commenting on code assets or folders.</td>
</tr>
<tr class="even">
<td style="text-align: left;"><a href="/iam/docs/roles-permissions/dataform#dataform.codeViewer">Code Viewer</a> ( <code dir="ltr" translate="no">       roles/dataform.codeViewer      </code> )</td>
<td style="text-align: left;">File or folder</td>
<td style="text-align: left;">Provides read-only access. A user with this role can query the contents of files and folders.</td>
</tr>
<tr class="odd">
<td style="text-align: left;"><a href="/iam/docs/roles-permissions/dataform#dataform.codeCreator">Code Creator</a> ( <code dir="ltr" translate="no">       roles/dataform.codeCreator      </code> )</td>
<td style="text-align: left;">Project</td>
<td style="text-align: left;">Grants permission to create new files and folders within a project.</td>
</tr>
</tbody>
</table>

The following roles are specific to managing team folders:

<table>
<thead>
<tr class="header">
<th style="text-align: left;">Role</th>
<th style="text-align: left;">Granted on</th>
<th style="text-align: left;">Permissions and use cases</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;"><a href="/iam/docs/roles-permissions/dataform#dataform.teamFolderOwner">Team Folder Owner</a> ( <code dir="ltr" translate="no">       roles/dataform.teamFolderOwner      </code> )</td>
<td style="text-align: left;">Team folder</td>
<td style="text-align: left;">Grants full control over a team folder in the files and folders system. A user with this role can delete the team folder and set its IAM policy.</td>
</tr>
<tr class="even">
<td style="text-align: left;"><a href="/iam/docs/roles-permissions/dataform#dataform.teamFolderContributor">Team Folder Contributor</a> ( <code dir="ltr" translate="no">       roles/dataform.teamFolderContributor      </code> )</td>
<td style="text-align: left;">Team folder</td>
<td style="text-align: left;">Allows for content management within a team folder. A user with this role can update a team folder.</td>
</tr>
<tr class="odd">
<td style="text-align: left;"><a href="/iam/docs/roles-permissions/dataform#dataform.teamFolderCommenter">Team Folder Commenter</a> ( <code dir="ltr" translate="no">       roles/dataform.teamFolderCommenter      </code> )</td>
<td style="text-align: left;">Team folder</td>
<td style="text-align: left;">Allows for commenting on a team folder and the code assets that it contains.</td>
</tr>
<tr class="even">
<td style="text-align: left;"><a href="/iam/docs/roles-permissions/dataform#dataform.teamFolderViewer">Team Folder Viewer</a> ( <code dir="ltr" translate="no">       roles/dataform.teamFolderViewer      </code> )</td>
<td style="text-align: left;">Team folder</td>
<td style="text-align: left;">Provides read-only access to a team folder and its contents. A user with this role can view a team folder and get its IAM policy.</td>
</tr>
<tr class="odd">
<td style="text-align: left;"><a href="/iam/docs/roles-permissions/dataform#dataform.teamFolderCreator">Team Folder Creator</a> ( <code dir="ltr" translate="no">       roles/dataform.teamFolderCreator      </code> )</td>
<td style="text-align: left;">Project</td>
<td style="text-align: left;">Grants permission to create new team folders within a project.</td>
</tr>
</tbody>
</table>

For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

These predefined roles contain the permissions required to complete the tasks in this document. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

  - Create a folder:
      - `  folders.create  ` on the parent user folder, team folder, or project
      - `  folders.addContents  ` on the parent folder or team folder
  - Retrieve the properties of a folder: `  folders.get  ` on the folder
  - Query the contents of a folder or team folder: `  folders.queryContents  ` on the folder
  - Update a folder: `  folders.update  ` on the folder
  - Delete a folder: `  folders.delete  ` on the folder
  - Get the IAM policy for a folder: `  folders.getIamPolicy  ` on the folder
  - Set the IAM policy for a folder: `  folders.setIamPolicy  ` on the folder
  - Move a folder:
      - `  folders.move  ` on the folder being moved
      - `  folders.addContents  ` on the destination folder or team folder (not needed if moving to a root folder)
  - Create a team folder: `  teamFolders.create  ` on the project
  - Delete a team folder: `  teamFolders.delete  ` on the team folder
  - Get the IAM policy for a team folder: `  teamFolders.getIamPolicy  ` on the team folder
  - Set the IAM policy for a team folder: `  teamFolders.setIamPolicy  ` on the team folder
  - Retrieve the properties of a team folder: `  teamFolders.get  ` on the team folder
  - Update a team folder: `  teamFolders.update  ` on the team folder

You might also be able to get these permissions with [custom roles](/iam/docs/creating-custom-roles) or other [predefined roles](/iam/docs/roles-overview#predefined) .

To gain full access to all the folders and files in your project, ask your administrator to grant you the following IAM roles on the project:

  - [Dataform Admin](/dataform/docs/access-control#dataform.admin) ( `  roles/dataform.admin  ` )
  - [Dataform Editor](/dataform/docs/access-control#dataform.editor) ( `  roles/dataform.editor  ` )
  - [Dataform Viewer](/dataform/docs/access-control#dataform.viewer) ( `  roles/dataform.viewer  ` )

## View resources

Follow these steps to view folders and code assets in BigQuery:

1.  Go to the **BigQuery** page.

2.  In the left pane, click folder **Files** to open the file browser:
    
    If you don't see the left pane, click last\_page **Expand left pane** to open the pane.

3.  Do one of the following to view folders and code assets in the selected project and code region:
    
      - Expand the **User (your email address)** node to see folders and files that you have created.
      - Expand the **Team folders** node to view all team folders that you have access to.
      - Expand the **Shared with me** node to view all folders and files that other users have shared with you.

### Change the code region

You can have folders and code assets in [different code regions](/bigquery/docs/code-asset-folders#folder_code_regions) . Follow these steps to change the code region that you are viewing:

1.  Go to the **BigQuery** page.

2.  In the left pane, click folder **Files** to open the file browser:

3.  Next to the project name, click more\_vert **View files panel actions** \> **Switch code region** .

4.  Select the code region that you want to view.

5.  Click **Save** .

## Create a folder or code asset

Use this procedure to create any of the following resources:

  - A user folder or code asset at any level.
  - A subfolder in a team folder.
  - A code asset in the subfolder of a team folder.

For information about creating a team folder, see [Create a team folder](#create_a_team_folder) .

Follow these steps to create a folder or code asset in BigQuery:

1.  Go to the **BigQuery** page.

2.  In the left pane, click folder **Files** to open the file browser:

3.  Select the user root node or the folder in which you want to create the resource.

4.  Click more\_vert **View actions** \> **Create** , and then select the type of resource that you want to create.

5.  In the create resource pane, type a name for the new resource.

6.  Click **Save** .

## Create a team folder

Follow these steps to create a team folder in BigQuery:

1.  Go to the **BigQuery** page.

2.  In the left pane, click folder **Files** to open the file browser:

3.  Select the team folder root node.

4.  Click more\_vert **View actions** \> **Create team folder** .

5.  In the **Create team folder** dialog, type a name for the team folder.

6.  Click **Create** .

## Upload a code asset

Follow these steps to upload a code asset in BigQuery:

1.  Go to the **BigQuery** page.

2.  In the left pane, click folder **Files** to open the file browser:

3.  Select the folder to which you want to upload the code asset.

4.  Click more\_vert **View actions** \> **Upload** , and then select the type of code asset that you want to upload.

5.  In the upload resource pane, do one of the following:
    
      - Click the **File upload** radio button, and then browse for and select a local file.
      - Click the **URL** radio button, and then type the URL for a code asset file that resides in a GitHub repository.

6.  Type a name for the code asset.

7.  Optional: Select a region in which to store the code asset. If you select a different region than the default value, the region that you select becomes the default region where all new code assets are created going forward.

8.  Click **Save** .

## Download a code asset

Follow these steps to download a code asset in BigQuery:

1.  Go to the **BigQuery** page.

2.  In the left pane, click folder **Files** to open the file browser:

3.  Select the code asset that you want to download.

4.  Click more\_vert **View actions** \> **Download** .

## Rename a folder or code asset

Follow these steps to rename a folder or code asset in BigQuery:

1.  Go to the **BigQuery** page.

2.  In the left pane, click folder **Files** to open the file browser:

3.  Select the folder or code asset that you want to rename.

4.  Click more\_vert **View actions** \> **Rename** .

5.  In the resource renaming dialog, type a new name for the resource.

6.  Click **Rename** .

## Share a folder or code asset

Follow these steps to share a folder or code asset in BigQuery:

1.  Go to the **BigQuery** page.

2.  In the left pane, click folder **Files** to open the file browser:

3.  Select the folder or code asset that you want to share.

4.  In the **Share permissions** pane, click **Add User/Group** .

5.  In the **New principals** field, enter a principal.

6.  Do one of the following:
    
      - In the **Role** list, select one of the following roles to share a code asset, including a user folder:
        
          - [`  roles/dataform.codeOwner  `](/dataform/docs/access-control#dataform.codeOwner) : Can perform any action on the code asset, including deleting or sharing it.
          - [`  roles/dataform.codeEditor  `](/dataform/docs/access-control#dataform.codeEditor) : Can perform any action on the code asset except for deleting or sharing it.
          - [`  roles/dataform.codeCommenter  `](/dataform/docs/access-control#dataform.codeCommenter) : Can view and comment on the code asset.
          - [`  roles/dataform.codeViewer  `](/dataform/docs/access-control#dataform.codeViewer) : Can view the code asset.
    
      - In the **Role** list, select one of the following roles to share a team folder:
        
          - [`  roles/dataform.teamFolderOwner  `](/dataform/docs/access-control#dataform.teamFolderOwner) : Can perform any action on the team folder, including deleting or sharing it.
          - [`  roles/dataform.teamFolderContributor  `](/dataform/docs/access-control#dataform.teamFolderContributor) : Can perform any action on the team folder except for deleting or sharing it.
          - [`  roles/dataform.teamFolderCommenter  `](/dataform/docs/access-control#dataform.teamFolderCommenter) : Can view and comment on the team folder and the code assets that it contains.
          - [`  roles/dataform.teamFolderViewer  `](/dataform/docs/access-control#dataform.teamFolderViewer) : Can view the team folder and the code assets that it contains.

7.  Click **Save** .

8.  To return to the notebook information page, click **Close** .

## Move a folder or code asset

Follow these steps to move a folder or code asset in BigQuery:

1.  Go to the **BigQuery** page.

2.  In the left pane, click folder **Files** to open the file browser:

3.  Select the folder or code asset that you want to move.

4.  Click more\_vert **View actions** \> **Move** .

5.  In the move resource dialog, select the user or team folder to which you want to move the resource.

6.  Click **Move** .

## Copy a folder or code asset

Follow these steps to copy a folder or code asset in BigQuery:

1.  Go to the **BigQuery** page.

2.  In the left pane, click folder **Files** to open the file browser:

3.  Select the folder or code asset that you want to copy.

4.  Click more\_vert **View actions** \> **Copy** .

5.  In the copy resource dialog, select the user or team folder to which you want to copy the resource.

6.  Click **Copy** .

## Delete a folder or code asset

Follow these steps to delete a folder or code asset in BigQuery:

1.  Go to the **BigQuery** page.

2.  In the left pane, click folder **Files** to open the file browser:

3.  Select the folder or code asset that you want to delete.

4.  Click more\_vert **View actions** \> **Delete** .

5.  In the delete resource dialog, click **Delete** .

## What's next

  - [Organize code assets with folders](/bigquery/docs/code-asset-folders)
  - [Create notebooks](/bigquery/docs/create-notebooks)
  - [Create saved queries](/bigquery/docs/work-with-saved-queries)
  - [Create data canvases](/bigquery/docs/data-canvas)
  - [Create data preparations](/bigquery/docs/data-prep-get-suggestions)
