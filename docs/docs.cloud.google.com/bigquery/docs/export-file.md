---
name: documents/docs.cloud.google.com/bigquery/docs/export-file
uri: https://docs.cloud.google.com/bigquery/docs/export-file
title: Export query results to a file
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# Export query results to a file

To share or analyze query results in other tools, you can save BigQuery query results from the Google Cloud console to a local file, Google Drive, Google Sheets, or Cloud Storage. For local files, you can choose formats such as CSV or newline-delimited JSON.

## Limitations

BigQuery doesn't support exporting nested or repeated data ( `RECORD` / `STRUCT` or `ARRAY` data types) to CSV format. Even if `RECORD` or `STRUCT` fields don't seem deeply nested, BigQuery treats them as nested schema fields and returns an error indicating that the schema can't be nested.

To export query results to a CSV file, flatten the query into a single-level structure with one field per query column. You can flatten nested structs by selecting individual fields using dot notation, or flatten repeated arrays by using the `UNNEST` operator. Alternatively, to export nested or repeated data without flattening, export the query results in a format that supports nested schemas, such as newline-delimited JSON.

## Download query results to a local file

The bq command-line tool and the BigQuery API don't support downloading query results directly to a local file.

To download query results as a CSV or newline-delimited JSON file, use the Google Cloud console:

1.  In the Google Cloud console, open the BigQuery page.

2.  Click **SQL query** .

3.  In the **Query editor** field, enter a valid GoogleSQL query.

4.  Optional: To change the processing location, click **Edit** \> **Query settings** . By default, BigQuery automatically detects the location of your data. To change the location, under **Location** , clear the **Automatic location selection** checkbox, and then specify a region in the region list.

5.  Click **Save** .

6.  Click **Run** .

7.  When the results return, click **Save results** , and then under **Local download** , select **CSV** or **JSON** .

    The file downloads to your browser's default download location.

## Save query results to Google Drive

> **Beta**
>
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

The bq command-line tool and the BigQuery API don't support saving query results directly to Google Drive.

If you receive an error when trying to save BigQuery results to Google Drive, the Drive SDK API might be unable to access your Google Workspace account. To resolve the issue, your administrator must enable your user account to [access Google Drive](https://support.google.com/a/answer/6105699) with the Drive SDK API.

To save query results to Google Drive, use the Google Cloud console:

1.  In the Google Cloud console, open the BigQuery page.

2.  Click **SQL query** .

3.  In the **Query editor** field, enter a valid GoogleSQL query.

4.  Click **Run** .

5.  When the results return, click **Save results** .

6.  Under **Google Drive** , select **CSV** or **JSONL (newline delimited)** . When you save results to Google Drive, you can't choose a destination subfolder. Results are always saved to the root of your `My Drive` folder.

7.  Saving results to Google Drive might take several minutes. When the results are saved, a `Query result exported.` notification appears with a **Go to drive** button. The file is saved in `My Drive` using the format `bq-results-TIMESTAMP-RANDOM_CHARACTERS.csv` or `bq-results-TIMESTAMP-RANDOM_CHARACTERS.json` .

    ![Query result exported notification with Go to drive button](https://docs.cloud.google.com/static/bigquery/images/save_results_notification_open.png)

8.  In the notification, click **Go to drive** to view the file in Google Drive, or navigate to Google Drive and open `My Drive` .

## Save query results to Google Sheets

The bq command-line tool and the BigQuery API don't support saving query results directly to Google Sheets.

If you receive an error when trying to open BigQuery results in Google Sheets, the Drive SDK API might be unable to access your Google Workspace account. To resolve the issue, your administrator must enable your user account to [access Google Sheets](https://support.google.com/a/answer/6105699) with the Drive SDK API.

To save query results to Google Sheets, use the Google Cloud console:

1.  In the Google Cloud console, open the BigQuery page.

2.  Click **SQL query** .

3.  In the **Query editor** field, enter a valid GoogleSQL query.

4.  Optional: To change the processing location, click **Edit** \> **Query settings** . By default, BigQuery automatically detects the location of your data. To change the location, under **Location** , clear the **Automatic location selection** checkbox, and then specify a region in the region list.

5.  Click **Save** .

6.  Click **Run** .

7.  When the results return, click **Save results** , and then under **Google Drive** , select **Google Sheets** .

8.  If prompted, follow the instructions to sign in to your user account and click **Allow** to grant permission to write the data to your `My Drive` folder.

    After you grant permission, you receive an email confirming that BigQuery client tools have connected to your user account. The email details the permissions granted and includes steps to revoke access.

9.  When the results are saved, a message appears below the query results in the Google Cloud console: `Saved to Sheets as "results-YYYYMMDD-HHMMSS"` . Click **Open** to view your results in Google Sheets, or open the file from your `My Drive` folder.

To analyze larger datasets or refresh query results in Google Sheets, see [Use Connected Sheets](https://docs.cloud.google.com/bigquery/docs/connected-sheets) .

### Troubleshoot saving results to Google Sheets

When you save data from BigQuery to Google Sheets, cells in the sheet might appear blank if data exceeds the Google Sheets limit of 50,000 characters per cell. To resolve this, use a [string function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#split) in your GoogleSQL query to split long text into multiple columns, and then save the results to Google Sheets again.

## Save query results to Cloud Storage

You can export your query results to Cloud Storage in the Google Cloud console with the following steps:

1.  Open the BigQuery page in the Google Cloud console.

2.  Click **SQL query** .

3.  Enter a valid GoogleSQL query in the **Query editor** text area.

4.  Click **Run** .

5.  When the results are returned, click **Save results** \> **Cloud Storage** .

6.  In the **Export to Google Cloud Storage** dialog:

    - For **GCS Location** , browse for the bucket, folder, or file where you want to export the data.
    - For **Export format** , choose the format for your exported data: CSV, JSON (Newline Delimited), Avro, or Parquet.
    - For **Compression** , select a compression format or select `None` for no compression.

7.  Click **Save** to export the query results.

To check on the progress of the job, expand the **Job history** pane and look for the job with the `EXTRACT` type.

## Restrict downloading query results

To prevent users from downloading query results from the Google Cloud console, use one of the following methods:

- Configure a [VPC Service Controls](https://docs.cloud.google.com/vpc-service-controls/docs/overview) perimeter around BigQuery resources to prevent data exfiltration. When a project is protected by a service perimeter, users can't download or export data outside the established perimeter boundaries.

- Contact [Cloud Customer Care](https://docs.cloud.google.com/support) to request that your Google Cloud project or organization be added to a restricted list that disables data download and export options directly within the Google Cloud console.

## What's next

- Learn how to programmatically [export a table to a JSON file](https://docs.cloud.google.com/bigquery/docs/samples/bigquery-extract-table-json) .
- Learn about [quotas for extract jobs](https://docs.cloud.google.com/bigquery/quotas#export_jobs) .
- Learn about [BigQuery storage pricing](https://cloud.google.com/bigquery/pricing#storage) .
