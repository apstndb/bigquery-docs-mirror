# Where Gemini in BigQuery processes your data

This document helps you understand where Gemini in BigQuery processes your data. This behavior applies to the following Gemini in BigQuery features:

  - [SQL code assist](#sql-editor-canvas)
  - [BigQuery data canvas](#sql-editor-canvas)
  - [BigQuery data insights](#bigquery-data-insights)
  - [BigQuery data preparation](#bigquery-data-preparation)

For these features, Gemini processing occurs in the jurisdictional boundaries of the query location, or where the BigQuery dataset is stored. For example, if your BigQuery query location or dataset is in the `  europe-west1  ` region, Gemini processing occurs in a location within the `  EU  ` jurisdictional boundary. This design minimizes data movement and follows data governance best practices. For more information about restrictions on available jurisdictions, see [Limitations](#limitations) .

For most Gemini in BigQuery features, the Gemini processing location can be controlled by an administrator by using the **Global Default Location** setting at the project or organization level. BigQuery users can override this global default location by using the **Query Location** setting in BigQuery Studio. In cases where a query location setting isn't specified in configuration settings by an administrator or explicitly by the user in the query, Gemini in BigQuery uses the location derived from the query being edited. To learn more about how BigQuery determines query location see [Run a query](/bigquery/docs/running-queries) .

Gemini in BigQuery determines the jurisdiction of `  US  ` or `  EU  ` based upon these controls. If a jurisdiction cannot be determined, then the global processing location is used based upon the [Gemini serving locations](/gemini/docs/locations) .

The following sections explain how you can manage where each Gemini in BigQuery feature processes your data.

## SQL editor and data canvas

When you [generate code using the SQL editor](/bigquery/docs/write-sql-gemini) , or use [data canvas](/bigquery/docs/data-canvas) to create data analysis workflows, Gemini in BigQuery uses the following logic to determine the processing location:

  - A BigQuery administrator can specify a default organization-level or project-level location. To learn how to specify a default location, see [Specify the default organization-level or project-level location](#specify-default-location) .

  - A BigQuery user can specify a query location in BigQuery Studio that overrides the administrator setting. To learn how to specify a default query location setting in BigQuery, see [Specify locations](/bigquery/docs/locations#specify_locations) .

  - If a dataset's location cannot be determined, or if the user's default query location is unspecified,BigQuery attempts to determine the location of the dataset or query based on the [dry run](/bigquery/docs/running-queries#dry-run) . For example:
    
      - SQL editor example: If your Gemini request for **Transform SQL with Gemini** references a dataset in `  europe-west1  ` , then Gemini processes the data in the `  EU  ` jurisdictional boundary.
      - Data canvas example: If your data canvas visualizes data from a dataset located in `  us-east4  ` , any Gemini in BigQuery analyses or suggestions are processed in the `  US  ` jurisdictional boundaries.

### Specify the default organization-level or project-level location

A BigQuery administrator can specify an organization-level or project-level default location where Gemini requests are processed. The default location is cached for the duration of the user's session while they are editing within the current SQL editor tab.

#### Prerequisite

To the specify the organization-level or project-level default location where data is processed, a BigQuery administrator must first opt in to the BigQuery feature by completing this [form](https://docs.google.com/forms/d/e/1FAIpQLSexsL9QmmqL7pOS_WIX02nntswdvaUucOXDamE9j7zuOX5suA/viewform) and then receive an email confirming that the feature was enabled.

#### Required roles

To specify a default organization or project location, you must be granted the [BigQuery Admin role](/iam/docs/roles-permissions/bigquery#bigquery.admin) ( `  roles/bigquery.admin  ` ), which includes the `  bigquery.config.update  ` permission that is required to specify a configuration setting. For more information about granting roles, see [Manage access to projects, folders, and organizations](/iam/docs/granting-changing-revoking-access) .

#### Set the default location

To set an organization-level or project-level default location, complete the following steps:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the navigation pane, click explore **Explorer** .

3.  Select the organization or project for which you want to specify a default location.

4.  In the BigQuery SQL editor, enter the following statement:
    
      - Organization-level settings:
        
        ``` text
        ALTER ORGANIZATION SET OPTIONS(default_location='my-default-region');
        ```
    
      - Project-level settings:
        
        ``` text
        ALTER PROJECT SET OPTIONS(default_location='my-default-region');
        ```

This command sets the value of `  default_location  ` to `  my-default-region  ` .

### Verify default location for data processing

To verify the default location for data processing of a Gemini in BigQuery-assisted SQL query, follow these steps:

1.  In the Google Cloud console, go to the **BigQuery** page.

2.  In the BigQuery Studio SQL editor, run the following query:
    
    ``` text
    SELECT
        COALESCE(
            (
                SELECT
                    option_value
                FROM INFORMATION_SCHEMA.PROJECT_OPTIONS
                WHERE option_name = 'default_location'
            ),
            (
                SELECT
                    option_value
                FROM INFORMATION_SCHEMA.ORGANIZATION_OPTIONS
                WHERE option_name = 'default_location'
            ));
    ```

The result shows the `  default_location  ` value set to the value you defined as `  my-default-region  ` . This query returns the default location of the project if defined. Otherwise, the query returns the default location for the organization. The location where Gemini in BigQuery operations run is not explicitly specified by the user.

## BigQuery data insights

To generate insights using [BigQuery data insights](/bigquery/docs/data-insights) , you can run data scan operations on selected tables and dataset resources. These scans are created in the same location as the BigQuery dataset resource. Within the `  US  ` or `  EU  ` jurisdictions, Gemini in BigQuery processing is restricted to the jurisdiction where the scan runs. Outside of the `  US  ` and `  EU  ` jurisdictions, processing runs globally. To learn about where global Gemini global data processing takes place, see [Gemini serving locations](/gemini/docs/locations) .

## BigQuery data preparation

The location where [BigQuery data preparation](/bigquery/docs/data-prep-introduction) processes data depends upon which data preparation feature you are using.

  - For standalone data preparation, the Gemini in BigQuery processing location is the location where the BigQuery dataset is located.
  - If you run data preparation as part of Dataform or BigQuery pipelines, then the Gemini in BigQuery data processing location is determined by the Dataform [`  defaultLocation  ` setting](/dataform/docs/manage-repository#about-workflow-settings-yaml) , if it's set. The `  defaultLocation  ` setting also determines the BigQuery job location. This ensures that Gemini in BigQuery processing is done in the same jurisdictional boundaries.
  - If `  defaultLocation  ` for Dataform or the BigQuery pipeline that contains your data preparation is not set, then the Gemini in BigQuery processing region is determined by using the repository's [region setting](/dataform/docs/create-repository#repository-settings) . A pipeline without a `  defaultLocation  ` setting specified can run different BigQuery jobs in different locations based on the location of the tables used in pipeline nodes. As a best practice, you should set `  defaultLocation  ` to ensure a consistent processing location.

## Limitations

The following limitations apply when you identify where Gemini in BigQuery processes data:

  - Gemini in BigQuery doesn't provide data residency for individual locations. Data processing can be specified for `  US  ` and `  EU  ` supported jurisdictions. Data outside these jurisdictions is processed globally.

  - Gemini in BigQuery jurisdiction processing is only available for Gemini in BigQuery features that are generally available (GA). For a list of Gemini in BigQuery features, see [Overview of Gemini in BigQuery](/bigquery/docs/gemini-overview) .

  - BigQuery Python notebook code assist and the Data Science Agent for Colab Enterprise in BigQuery only support global Gemini processing.
    
    **Note:** To opt out of the Colab Enterprise preview feature without turning off other Gemini features, contact <vertex-notebooks-previews-external@google.com> or fill out the [Data Science Agent Public Preview Opt-out form](https://forms.gle/KuTAunuLT2YmFAcs8) . To learn more about how to turn off Data Science Agent, see [Turn off Gemini in Colab Enterprise](/colab/docs/use-data-science-agent#turn-off) .

  - Gemini in Cloud Assist chat (GCA) only supports global Gemini processing. You can deny access to the GCA chat panel by removing the `  cloudaicompanion.instances.completeTask  ` Identity and Access Management (IAM) permission for your users. To learn more about how to create custom roles, see [Create and manage custom roles](/iam/docs/creating-custom-roles) .

## What's next

  - Read the [Gemini in BigQuery overview](/bigquery/docs/gemini-overview) .
  - Learn how to [set up Gemini in BigQuery](/bigquery/docs/gemini-set-up) .
  - Learn how to [write queries with Gemini assistance](/bigquery/docs/write-sql-gemini) .
  - Learn more about [Google Cloud compliance](https://cloud.google.com/security/compliance) .
  - Learn about [security, privacy, and compliance for Gemini in BigQuery](/bigquery/docs/gemini-security-privacy-compliance) .
  - Learn more about [how Gemini for Google Cloud uses your data](/gemini/docs/discover/data-governance) .
