---
name: documents/docs.cloud.google.com/bigquery/docs/git-repositories
uri: https://docs.cloud.google.com/bigquery/docs/git-repositories
title: Manage code with BigQuery Studio Git repositories
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# Manage code with BigQuery Studio Git repositories

BigQuery Studio Git repositories let you version control SQL scripts, notebooks, and other code assets directly in the BigQuery Studio file browser. You can clone remote Git repositories, manage branches, and perform Git operations without leaving the Google Cloud console.

Compared to classic [repositories](https://docs.cloud.google.com/bigquery/docs/repositories) , this integration provides a streamlined, folder-based experience under your user root folder in the left pane. You can interact with your code assets like standard files and directories while maintaining a connection to a remote Git repository.

## Limitations

- BigQuery Studio Git repositories are restricted to the user root folder context and are intended for private use. Don't share these repositories with other users. Although these repositories appear in your user root folder—which is a virtual representation of your assets in the project—they're technically created at the project level.

- File system operations within the [mount location](https://docs.cloud.google.com/bigquery/docs/git-repositories#notebook-mount) consume [Dataform quota](https://docs.cloud.google.com/dataform/docs/quotas) .

- Repositories with a large number of files, large file sizes, many branches, or a deep and complex commit history take longer to clone. The cloning operation might exceed the operation timeout, which prevents the repository from being successfully created. To reduce the cloning time for repositories with deep commit histories, you can create a [shallow clone](https://docs.cloud.google.com/bigquery/docs/git-repositories#create-git-repository) . You can [fetch more commits](https://docs.cloud.google.com/bigquery/docs/git-repositories#view-commit-history) later as needed.

- The size of notebook files stored in a BigQuery Studio Git repository mount can't exceed 30 MB. If your files are larger than 30 MB, save them to your Colab runtime's local storage outside of the mounted location.

- When you make changes to a Git repository outside of the mount—for example, by editing or renaming files in the left pane—it can take up to 60 seconds for those changes to become visible within the mount on your notebook's runtime. You can adjust this duration by passing the `CACHE_TTL_SECONDS` parameter to the constructor:

  ```
    FuseWidget(CACHE_TTL_SECONDS=NUMBER)
  ```

  Replace `NUMBER` with the number of seconds for the cache to remain valid. Decreasing this value increases the frequency of synchronization and consumes Dataform quota faster.

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

#### Security recommendations for Developer Connect permissions

BigQuery Studio Git repositories use Developer Connect to connect to remote repositories. Also, predefined BigQuery and Dataform roles include Developer Connect permissions. Due to these security features, we recommend that you do the following:

- **Use custom roles to enforce separation of duties:** if your organization requires strict separation between data analytics tasks and source code management, deploy [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) that omit Developer Connect permissions. Predefined roles such as [BigQuery User ( `roles/bigquery.user` )](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.user) and [BigQuery Studio User ( `roles/bigquery.studioUser` )](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.studioUser) include Developer Connect permissions, which let users assigned these roles start OAuth flows and proxy Git traffic.
- **Enforce guardrails with IAM deny policies:** apply organization-level [deny policies](https://docs.cloud.google.com/iam/docs/deny-overview) to prevent sensitive actions for broad analytics groups. Consider denying the `developerconnect.googleapis.com/gitRepositoryLinks.fetchReadWriteToken` permission to prevent token extraction, and the `developerconnect.googleapis.com/accountConnectors.gitProxyWrite` permission to prevent unintended write access to repositories. Administrative roles such as [BigQuery Admin ( `roles/bigquery.admin` )](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.admin) and [BigQuery Studio Admin ( `roles/bigquery.studioAdmin` )](https://docs.cloud.google.com/bigquery/docs/access-control#bigquery.studioAdmin) include token accessor permissions that let principals retrieve active plaintext third-party source code management (SCM) tokens, such as GitHub App installation tokens.
- **Isolate sensitive CI/CD projects:** keep sensitive CI/CD pipelines, such as Cloud Build or Vertex AI, in dedicated Google Cloud projects that are separated from general data analytics environments. Because Developer Connect permissions are scoped at the project level, a BigQuery user in a shared, multi-tenant project can list and use any Developer Connect connection in that project to proxy Git requests, which might grant access to repositories configured for CI/CD or infrastructure automation.
- **Restrict resource access using IAM Conditions:** attach [IAM Conditions](https://docs.cloud.google.com/iam/docs/conditions-overview) to role bindings to restrict Developer Connect permissions to specific resources. You can limit access based on resource name prefixes or scope access to specific `Connection` and `GitRepositoryLink` resources. This ensures that users can interact only with Developer Connect connections that are intended for their workflows.
- **Protect sensitive metadata in resource names:** don't embed sensitive credentials, project codenames, or confidential information in repository names, branch names, or connection IDs. The permissions required to list these resources ( `developerconnect.connections.list` and `developerconnect.accountConnectors.list` ) are granted to standard BigQuery roles. Anyone with basic project access can enumerate these resources and discover sensitive metadata.

## Create a BigQuery Studio Git repository

When creating a Git repository, take these requirements into account:

- Connecting a remote Git repository to a Git repository can fail if the remote repository isn't open to the public internet, for example, if it's behind a firewall. In this case, add the required [Dataform egress IP address ranges](https://docs.cloud.google.com/dataform/docs/locations) to your firewall rules to enable connections to protected remote repositories.
- To create a Git repository connected to a remote Git repository that is not allow-listed in the `dataform.restrictGitRemotes` organization policy, first add the remote Git repository to the `allowedValues` list in the policy, and then create the Git repository. For more information, see [Restrict remote repositories](https://docs.cloud.google.com/dataform/docs/restrict-git-remotes) .

To create a Git repository, do the following:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click folder **Files** to open the file browser.

    If you don't see the left pane, click last_page **Expand left pane** to open the pane.

3.  Next to your user root node, click more_vert **View actions** \> **Create** \> **Git repository** .

4.  Enter the URL for your remote Git repository.

5.  BigQuery Studio detects if an existing [Developer Connect account connector](https://docs.cloud.google.com/developer-connect/docs/configure-connectors) is available. You have the following options:

    - If an account connector is found, the display name for the Git repository is prefilled. You can edit these values.
    - If no account connector exists, click **Create account connector** to create a new account connector.
    - If you prefer not to use a Developer Connect account connector, click **Use a different connection type** to [connect using HTTPS or SSH](https://docs.cloud.google.com/bigquery/docs/repositories#connect-third-party) .

6.  Optional: To create a shallow clone repository with limited commit history, click **Advanced options** , and then select the **Shallow clone** checkbox.

    1.  In the **Depth** field, enter the number of commits to retrieve in the limited commit history.

7.  Click **Connect** .

## Edit a file

To edit a file, click a file node—such as a SQL script or notebook—to open the file in a new editor tab.

Any changes you make are automatically saved.

## Manage files

You can perform standard management tasks using the action menu associated with each item. To access these options, click more_vert **View actions** next to any directory or file.

At the directory level, you can perform the following tasks:

- **Create in repository** : create new code assets including SQL queries, notebooks, data canvases, data preparations, files, or sub-directories.
- **Upload to repository** : import existing files from your local machine into the selected directory.
- **Rename** : change the name of the directory.
- **Move** : relocate the directory. You can only move a directory to another location within the same Git repository. For more information, see [Move a directory or file](https://docs.cloud.google.com/bigquery/docs/git-repositories#move) .
- **Delete** : permanently remove the directory and all its contents from your local workspace. For more information, see [Delete a directory or file](https://docs.cloud.google.com/bigquery/docs/git-repositories#delete) .

At the file level, you can perform the following tasks:

- **Open** or **Open in** : view the file in the default editor or a specific application, for example, a specific notebook environment.
- **Rename** : change the filename.
- **Copy** : create a duplicate of the file. You can only copy files to directories within the same Git repository. For more information, see [Copy a file](https://docs.cloud.google.com/bigquery/docs/git-repositories#copy) .
- **Move** : relocate the file to another directory within the same Git repository. For more information, see [Move a directory or file](https://docs.cloud.google.com/bigquery/docs/git-repositories#move) .
- **Download** : save a copy of the file to your local machine.
- **Delete** : remove the file from your workspace. For more information, see [Delete a directory or file](https://docs.cloud.google.com/bigquery/docs/git-repositories#delete) .

### Move a directory or file

To move a directory or file in a BigQuery Studio Git repository, do the following:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click folder **Files** to open the file browser.

3.  Depending on how many resources you want to move, do one of the following:

    - To move a single resource, in the file browser, select the directory or file you want to move, and then click more_vert **View actions** \> **Move** .
    - To move multiple resources, in the folder view, select the checkbox next to each resource that you want to move, and then click **Move** .

4.  In the move resource dialog, select the target directory within the same Git repository. You can only move resources to locations within the same Git repository.

5.  Click **Move** .

> **Note:** Bulk move operations are independent. If one resource fails to move, the operation still attempts to complete the move for all other selected resources.

### Copy a file

To copy a file in a BigQuery Studio Git repository, do the following:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click folder **Files** to open the file browser.

3.  Select the file that you want to copy.

4.  Click more_vert **View actions** \> **Copy** .

5.  In the copy resource dialog, select the target directory within the same Git repository. You can only copy files to locations within the same Git repository.

6.  Click **Copy** .

### Delete a directory or file

To delete a directory or file in a BigQuery Studio Git repository, do the following:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click folder **Files** to open the file browser.

3.  Depending on how many resources you want to delete, do one of the following:

    - To delete a single resource, in the file browser, select the directory or file you want to delete, and then click more_vert **View actions** \> **Delete** .
    - To delete multiple resources, in the folder view, select the checkbox next to each resource that you want to delete, and then click **Delete** .

4.  In the delete confirmation dialog, click **Delete** .

## Commit and push changes

To synchronize your local edits with your remote repository, do the following:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the left pane, click fork_right **Source control** to open the **Source control** panel.

3.  Optional: Hover over a modified file and click **Show diff** to see a line-by-line comparison between your local version and the last committed version.

4.  In the **Commit message** field, enter a description of your changes.

5.  Click **Commit** . Your changes are saved to the Git history of your local branch.

6.  Click **Push to remote** . Your changes are synchronized with the remote repository.

## Check out a new branch

You can manage local branches and create a new local branch based on an existing local or remote tracking branch.

In the **Source control** panel, in the **Branches** section, you can see your checked-out local branches. The **CURRENT** label indicates your active branch, and the **DEFAULT** label indicates the repository's default branch.

> **Note:** You can't check out a new branch or switch branches if you have uncommitted changes in your workspace. You must commit your changes before switching or checking out branches.

To check out a new branch, do the following:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  Open the **Source control** panel.

3.  In the **Branches** section, next to **Branches** , click more_vert **Actions** \> **Check out new branch** .

4.  In the **Source branch** menu, select the branch you want to base your new branch on, for example, `origin/main` .

5.  In the **Branch name** field, enter a name for the new branch.

    > **Note:** If you selected a remote tracking branch as the source, the **Branch name** field is prefilled with the corresponding branch name.

6.  Click **Checkout branch** . BigQuery Studio checks out the source branch first. If the provided branch name indicates a new branch, it's then created based on that source. The new branch becomes the active branch, and the contents of your Git repository automatically update to reflect the state of the checked-out branch.

To switch to an existing branch, do the following:

1.  In the **Source control** panel, expand the **Branches** section.
2.  Next to the branch you want to switch to, click more_vert **Actions** \> **Switch to ` BRANCH_NAME `** .

## View commit history

You can view commit history for your active branch. If your repository was created as a shallow clone, the **Branch commit history** pane displays an informational banner indicating that the repository has limited commit history. You can expand your local history by fetching more commits.

To view the commit history, do the following:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  Open the **Source control** panel.

3.  Next to the primary version control action button, click the expander_arrow arrow drop-down, and then click **View commit history** .

    The **Branch commit history** pane opens, displaying the commit history for your active branch.

4.  Optional: To fetch commits from the remote repository, do one of the following:

    - Next to the primary version control action button, click the expander_arrow arrow drop-down, and then click **Fetch from remote** .
    - In the **Branch commit history** pane, click **Fetch** .

    For shallow clone repositories, in the **Fetch (shallow clone)** dialog, in the **Additional commits to fetch** field, enter the number of additional commits to retrieve from the repository history.

    If you enter `0` , no additional historical commits are retrieved, but BigQuery Studio performs a standard fetch to synchronize remote references and metadata.

5.  Click **Fetch** .

    You can repeat fetching as needed until all commits are retrieved.

## Delete a Git repository

Deleting a BigQuery Studio Git repository removes the repository and all of its contents from your BigQuery Studio environment.

To delete a Git repository, do the following:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  Delete the repository using one of the following methods:

    - To delete the repository from the file browser, in the left pane, click folder **Files** . Next to the Git repository that you want to delete, click more_vert **View actions** \> **Delete** .
    - To delete the repository from the control panel, under the **Source control** panel header, click more_vert **Source control options** \> **Delete ` REPOSITORY_NAME `** .

3.  In the delete confirmation dialog, click **Delete** .

## Access notebook files in a Git repository mount

When you access a notebook from within a BigQuery Studio Git repository, you can mount the host Git repository to your notebook's runtime. A mount is a connection that makes your remote Git repository appear as if it were a local repository on your notebook's runtime. This lets your notebook directly access, read, and write to other files and query scripts within the same repository.

### Mount the Git repository

To mount the Git repository, run the following Python code in your notebook:

```
from google_dataform_fuse_widget import FuseWidget
FuseWidget()
```

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
