---
name: documents/docs.cloud.google.com/bigquery/docs/git-repositories
uri: https://docs.cloud.google.com/bigquery/docs/git-repositories
title: Manage code with BigQuery Studio Git repositories
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# Manage code with BigQuery Studio Git repositories

> **Preview**
> 
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> **Note:** To provide feedback or ask questions that are related to this Preview feature, contact <bigquery-repositories-feedback@google.com> .

You can manage SQL scripts and notebooks using BigQuery Studio Git repositories. This feature integrates version control directly into the BigQuery Studio file browser, allowing you to clone repositories, manage branches, and perform Git operations without leaving Google Cloud console.

BigQuery Studio Git repositories offer a more streamlined, folder-based experience when compared to classic [repositories](https://docs.cloud.google.com/bigquery/docs/repositories) . BigQuery Studio Git repositories appear directly within the left pane under your user root folder.

By using BigQuery Studio Git repositories, you can interact with your code assets just like standard files and directories while maintaining a connection to a remote Git repository.

## Limitations

  - BigQuery Studio Git repositories are restricted to the user root folder context and are intended for private use. Don't share these repositories with other users. Although these repositories appear in your user root folder—which is a virtual representation of your assets in the project—they're technically created at the project level.

  - Using a Developer Connect account connector with a Git Proxy isn't supported.

  - File system operations within the [mount location](https://docs.cloud.google.com/bigquery/docs/git-repositories#notebook-mount) consume [Dataform quota](https://docs.cloud.google.com/dataform/docs/quotas) .

  - Repositories with a large number of files, large file sizes, many branches, or a deep and complex commit history take longer to clone. The cloning operation might exceed the operation timeout, which prevents the repository from being successfully created.

  - The size of notebook files stored in a BigQuery Studio Git repository mount can't exceed 30 MB. If your files are larger than 30 MB, save them to your Colab runtime's local storage outside of the mounted location.

  - When you make changes to a Git repository outside of the mount—for example, by editing or renaming files in the left pane—it can take up to 60 seconds for those changes to become visible within the mount on your notebook's runtime. You can adjust this duration by passing the `CACHE_TTL_SECONDS` parameter to the constructor:
    
    ``` 
      FuseWidget(CACHE_TTL_SECONDS=NUMBER)
    ```
    
    Replace `  NUMBER  ` with the number of seconds for the cache to remain valid. Decreasing this value increases the frequency of synchronization and consumes Dataform quota faster.

## Before you begin

Enable the Developer Connect API in your Google Cloud project.

### Required roles

To get the permissions that you need to manage code with BigQuery Studio Git repositories, ask your administrator to grant you the [Developer Connect OAuth User](https://docs.cloud.google.com/iam/docs/roles-permissions/developerconnect#developerconnect.oauthUser) ( `roles/developerconnect.oauthUser` ) IAM role on project. For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

This predefined role contains the permissions required to manage code with BigQuery Studio Git repositories. To see the exact permissions that are required, expand the **Required permissions** section:

#### Required permissions

The following permissions are required to manage code with BigQuery Studio Git repositories:

  - `resourcemanager.projects.get`
  - `resourcemanager.projects.list`
  - `developerconnect.operations.list`
  - `developerconnect.operations.get`
  - `developerconnect.locations.list`
  - `developerconnect.locations.get`
  - `developerconnect.users.startOAuth`
  - `developerconnect.users.finishOAuth`
  - `developerconnect.users.fetchAccessToken`
  - `developerconnect.users.getSelf`
  - `developerconnect.users.deleteSelf`
  - `developerconnect.accountConnectors.get`
  - `developerconnect.accountConnectors.list`
  - `developerconnect.accountConnectors.gitProxyUse`
  - `developerconnect.accountConnectors.httpProxyUse`
  - `developerconnect.accountConnectors.gitProxyRead`
  - `developerconnect.accountConnectors.gitProxyWrite`
  - `developerconnect.accountConnectors.httpProxyRead`
  - `developerconnect.accountConnectors.httpProxyWrite`
  - `developerconnect.accountConnectors.fetchUserRepositories`

You might also be able to get these permissions with [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

### Security considerations for repositories

Because code assets in BigQuery are powered by Dataform, you should consider the following security implications for users with access to these assets:

  - Visibility for code assets is governed by project-level Dataform permissions. Users with the `dataform.repositories.list` permission—which is included in standard BigQuery roles such as [BigQuery Job User](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.jobUser) , [BigQuery Studio User](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.studioUser) , and [BigQuery User](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.user) —can see all code assets in the **Explorer** panel of the Google Cloud project, regardless of whether they created these assets or these assets were shared with them. To restrict visibility, you can create [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) that exclude the `dataform.repositories.list` permission.
  - Any secrets shared with the Dataform service agent can potentially be accessed by users who can edit these assets. To secure your credentials, restrict creation and edit access to trusted users, and limit the secrets accessible to the Dataform service agent. For more information, see [Secrets access during package installation](https://docs.cloud.google.com/dataform/docs/access-control#secret-access-risk) .

For more information, see [Security considerations for Dataform permissions](https://docs.cloud.google.com/dataform/docs/access-control#security-considerations-permissions) .

## Create a BigQuery Studio Git repository

When creating a Git repository, take these requirements into account:

  - Connecting a remote Git repository to a Git repository can fail if the remote repository isn't open to the public internet, for example, if it's behind a firewall. In this case, add the required [Dataform egress IP address ranges](https://docs.cloud.google.com/dataform/docs/locations) to your firewall rules to enable connections to protected remote repositories.
  - To create a Git repository connected to a remote Git repository that is not allow-listed in the `dataform.restrictGitRemotes` organization policy, first add the remote Git repository to the `allowedValues` list in the policy, and then create the Git repository. For more information, see [Restrict remote repositories](https://docs.cloud.google.com/dataform/docs/restrict-git-remotes) .

To create a Git repository, do the following:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click folder **Files** to open the file browser.
    
    If you don't see the left pane, click last\_page **Expand left pane** to open the pane.

3.  Next to your user root node, click more\_vert **View actions** \> **Create** \> **Git repository** .

4.  Enter the URL for your remote Git repository.

5.  BigQuery Studio detects if an existing [Developer Connect account connector](https://docs.cloud.google.com/developer-connect/docs/configure-connectors) is available. You have the following options:
    
      - If an account connector is found, the display name for the Git repository is prefilled. You can edit these values.
      - If no account connector exists, click **Create account connector** to create a new account connector.
      - If you prefer not to use a Developer Connect account connector, click **Use different connection type** to [connect using HTTPS or SSH](https://docs.cloud.google.com/bigquery/docs/repositories#connect-third-party) .

6.  Click **Connect** .

## Edit a file

To edit a file, click a file node—such as a SQL script or notebook—to open the file in a new editor tab.

Any changes you make are automatically saved.

## Manage files

You can perform standard management tasks using the action menu associated with each item. To access these options, click more\_vert **Open actions** next to any directory or file.

At the directory level, you can perform the following tasks:

  - **Create in repository** : create new code assets including SQL queries, notebooks, data canvases, data preparations, files, or sub-directories.
  - **Upload to repository** : import existing files from your local machine into the selected directory.
  - **Rename** : change the name of the directory.
  - **Move** : relocate the directory. You can only move a directory to another location within the same Git repository. For more information, see [Move or copy files and directories](https://docs.cloud.google.com/bigquery/docs/git-repositories#move-copy) .
  - **Delete** : permanently remove the directory and all its contents from your local workspace.

At the file level, you can perform the following tasks:

  - **Open** or **Open in** : view the file in the default editor or a specific application, for example, a specific notebook environment.
  - **Rename** : change the filename.
  - **Copy** : create a duplicate of the file. You can only copy files to directories within the same Git repository.
  - **Move** : relocate the file to another directory within the same Git repository. For more information, see [Move or copy files and directories](https://docs.cloud.google.com/bigquery/docs/git-repositories#move-copy) .
  - **Download** : save a copy of the file to your local machine.
  - **Delete** : remove the file from your workspace.

### Move or copy files and directories

You can move or copy files and directories, but they must remain within the same Git repository.

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click folder **Files** to open the file browser.

3.  Find the file or directory you want to move or copy.

4.  Click more\_vert **Open actions** \> **Move** or **Copy** .

5.  In the dialog that appears, select the target directory within the same Git repository.

6.  Click **Move** or **Copy** .

## Commit and push changes

To synchronize your local edits with your remote repository, do the following:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click fork\_right **Repository** .

3.  Optional: Hover over a modified file and click **View diff** to see a line-by-line comparison between your local version and the last committed version.

4.  In the **Commit message** field, enter a description of your changes.

5.  Click **Commit** . Your changes are saved to the Git history of your local branch.

6.  Click **Push to remote branch** . Your changes are synchronized with the remote repository.

## Check out a new branch

You can manage local branches and create a new local branch based on an existing local or remote tracking branch.

In the **Repository** tab, in the **Branches** section, you can see your checked-out local branches. The **CURRENT** label indicates your active branch, and the **DEFAULT** label indicates the repository's default branch.

To check out a new branch, do the following:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click fork\_right **Repository** .

3.  Expand the **Branches** section.

4.  Click more\_vert **Open actions** next to a branch, and then click **Check out new branch** .

5.  In the **Source branch** menu, select the branch you want to base your new branch on, for example, `origin/main` .

6.  In the **Branch name** field, enter a name for the new branch.
    
    > **Note:** If you selected a remote tracking branch as the source, the **Branch name** field is prefilled with the corresponding branch name.

7.  Click **Check out** . BigQuery Studio checks out the source branch first. If the provided branch name indicates a new branch, it's then created based on that source. The new branch becomes the active branch, and the contents of your Git repository automatically update to reflect the state of the checked-out branch.

## Access notebook files in a Git repository mount

When you access a notebook from within a BigQuery Studio Git repository, you can mount the host Git repository to your notebook's runtime. A mount is a connection that makes your remote Git repository appear as if it were a local repository on your notebook's runtime. This lets your notebook directly access, read, and write to other files and query scripts within the same repository.

### Mount the Git repository

To mount the Git repository, run the following Python code in your notebook:

    from google_dataform_fuse_widget import FuseWidget
    FuseWidget()

> **Note:** We recommend running this code in a Colab scratch cell that isn't saved with the notebook. To create a scratch cell, click **Insert** \> **Scratch code cell** .

When the notebook is connected to the mount, the following changes occur:

  - The notebook session's current working directory is updated to reflect its relative path within the Git repository. This ensures that path-based file access works automatically.
  - The Git repository's path on the notebook's runtime is added to the Python system path, which lets you use standard Python import statements to load query scripts and files from your Git repository directly into your notebook.

### Manage the mount and connection

Use the following controls to manage your workspace:

  - **Mount workspace** : starts the mounting process for the Git repository. The mount is a shared resource, so if multiple notebooks on the same Colab runtime use the same Git repository, they use the same mount.
  - **Unmount workspace** : stops the mounting process for the Git repository. Unmounting the workspace makes the mount unavailable to all the notebooks on that Colab runtime that were using it.
  - **Connect workspace** : starts the connection to an active mount for the current notebook session. Connecting updates the notebook's working directory and system path to include the Git repository, which lets you access and import files.
  - **Disconnect workspace** : ends the mount connection for the current notebook session and resets it to the default state. Disconnecting doesn't affect the mount connection status for other active notebook sessions. To end your session's connection, we recommend using the **Disconnect workspace** button.
  - **Repair** : restores a mount or connection to a healthy state if it becomes unusable.

After you initialize the mount, refer to the **Status** bar for the real-time health and active path of the mount. The possible health states are **Connected** , **Mounted** , **Stopped** , and **Unhealthy** .

## What's next

  - Learn how to [create notebooks](https://docs.cloud.google.com/bigquery/docs/create-notebooks) .
  - Learn how to [create saved queries](https://docs.cloud.google.com/bigquery/docs/work-with-saved-queries) .
  - Learn how to [create and manage repositories](https://docs.cloud.google.com/bigquery/docs/repositories) .
  - Learn how to [organize code assets with folders](https://docs.cloud.google.com/bigquery/docs/code-asset-folders) .
