# Use the BigQuery JupyterLab plugin

**Preview**

This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

To request feedback or support for this feature, send an email to <bigquery-ide-plugin@google.com> .

This document shows you how to install and use the BigQuery JupyterLab plugin to do the following:

  - Explore your BigQuery data.
  - Use the BigQuery DataFrames API.
  - Deploy a BigQuery DataFrames notebook to [Cloud Composer](/composer/docs/concepts/overview) .

The BigQuery JupyterLab plugin includes all the functionality of the [Dataproc JupyterLab plugin](/dataproc-serverless/docs/quickstarts/jupyterlab-sessions) , such as creating a Dataproc Serverless runtime template, launching and managing notebooks, developing with Apache Spark, deploying your code, and managing your resources.

## Install the BigQuery JupyterLab plugin

To install and use the BigQuery JupyterLab plugin, follow these steps:

1.  In your local terminal, check to make sure you have Python 3.8 or later installed on your system:
    
    ``` text
    python3 --version
    ```

2.  [Install the gcloud CLI.](/sdk/docs/install)

3.  In your local terminal, [initialize the gcloud CLI](/sdk/docs/initializing) :
    
    ``` text
    gcloud init
    ```

4.  Install Pipenv, a Python virtual environment tool:
    
    ``` text
    pip3 install pipenv
    ```

5.  Create a new virtual environment:
    
    ``` text
    pipenv shell
    ```

6.  Install JupyterLab in the new virtual environment:
    
    ``` text
    pipenv install jupyterlab
    ```

7.  Install the BigQuery JupyterLab plugin:
    
    ``` text
    pipenv install bigquery-jupyter-plugin
    ```

8.  If your installed version of JupyterLab is earlier than 4.0.0, then enable the plugin extension:
    
    ``` text
    jupyter server extension enable bigquery_jupyter_plugin
    ```

9.  Launch JupyterLab:
    
    ``` text
    jupyter lab
    ```
    
    JupyterLab opens in your browser.

**Note:** On macOS, if you receive an `  SSL: CERTIFICATE_VERIFY_FAILED  ` error in your terminal when you launch JupyterLab, update your Python SSL certificate by executing `  /Applications/Python 3.11/Install Certificates.command  ` . This file is located in the Python home directory.

## Update your project and region settings

By default, your session runs in the project and region that you set when you ran `  gcloud init  ` . To change the project and region settings for your session, do the following:

  - In the JupyterLab menu, click **Settings \> Google BigQuery Settings** .

You must restart the plugin for the changes to take effect.

## Explore data

To work with your BigQuery data in JupyterLab, do the following:

1.  In the JupyterLab sidebar, open the **Dataset Explorer** pane: click the datasets icon.

2.  To expand a project, in the **Dataset Explorer** pane, click the arrow\_right expander arrow next to the project name.
    
    The **Dataset Explorer** pane shows all of the datasets in a project that are located in the BigQuery region that you configured for the session. You can interact with a project and dataset in various ways:
    
      - To view information about a dataset, click the name of the dataset.
      - To display all of the tables in a dataset, click the arrow\_right expander arrow next to the dataset.
      - To view information about a table, click the name of the table.
      - To change the project or BigQuery region, [update your settings](#configure) .

## Execute notebooks

To query your BigQuery data from JupyterLab, do the following:

1.  To open the launcher page, click **File \> New Launcher** .
2.  In the **BigQuery Notebooks** section, click the **BigQuery DataFrames** card. A new notebook opens that shows you how to get started with BigQuery DataFrames.

BigQuery DataFrames notebooks support Python development in a local Python kernel. BigQuery DataFrames operations are executed remotely on BigQuery, but the rest of code is executed locally on your machine. When an operation is executed in BigQuery, a query job ID and link to the job appear below the code cell.

  - To view the job in the Google Cloud console, click **Open Job** .

## Deploy a BigQuery DataFrames notebook

You can deploy a BigQuery DataFrames notebook to Cloud Composer by using a [Dataproc Serverless runtime template](/dataproc-serverless/docs/quickstarts/jupyterlab-sessions#create_a_serverless_runtime_template) . You must use runtime version 2.1 or later.

1.  In your JupyterLab notebook, click calendar\_month **Job Scheduler** .

2.  For **Job name** , enter a unique name for your job.

3.  For **Environment** , enter the name of the Cloud Composer environment to which you want to deploy the job.

4.  If your notebook is parameterized, add parameters.

5.  Enter the name of the [Serverless runtime template](/dataproc-serverless/docs/quickstarts/jupyterlab-sessions#create_a_serverless_runtime_template) .

6.  To handle notebook execution failures, enter an integer for **Retry count** and a value (in minutes) for **Retry delay** .

7.  Select which execution notifications to send, and then enter the recipients.
    
    Notifications are sent using the Airflow SMTP configuration.

8.  Select a schedule for the notebook.

9.  Click **Create** .

When you successfully schedule your notebook, it appears on the list of scheduled jobs in your selected Cloud Composer environment.

## What's next

  - Try the [BigQuery DataFrames quickstart](/bigquery/docs/dataframes-quickstart) .
  - Learn more about the [BigQuery DataFrames Python API](/bigquery/docs/reference/bigquery-dataframes) .
  - Use the JupyterLab for [serverless batch and notebook sessions](/dataproc-serverless/docs/quickstarts/jupyterlab-sessions) with Dataproc.
