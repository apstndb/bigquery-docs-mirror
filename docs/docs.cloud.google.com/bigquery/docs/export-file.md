# Export query results to a file

This document describes how to save query results as a file, such as CSV or JSON.

## Download query results to a local file

Downloading query results to a local file is not supported by the bq command-line tool or the API.

To download query results as a CSV or newline-delimited JSON file, use the Google Cloud console:

1.  In the Google Cloud console, open the BigQuery page.

2.  Click add\_box **SQL query** .

3.  Enter a valid GoogleSQL query in the **Query editor** text area.

4.  Optional: To change the processing location, click **More** and select **Query settings** . For **Data location** , choose the [location](/bigquery/docs/locations) of your data.

5.  Click **Run** .

6.  When the results are returned, click **Save results** and select the format or location where you want to save the results.
    
    The file is downloaded to your browser's default download location.

## Save query results to Google Drive

**Beta**

This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

Saving query results to Google Drive is not supported by the bq command-line tool or the API.

You might get an error when you try to save the BigQuery results to Google Drive. This error is due to the Drive SDK API being unable to access Google Workspace. To resolve the issue, you must enable your user account to [access Google Drive](https://support.google.com/a/answer/6105699) with the Drive SDK API.

To save query results to Google Drive, use the Google Cloud console:

1.  In the Google Cloud console, open the BigQuery page.

2.  Click add\_box **SQL query** .

3.  Enter a valid GoogleSQL query in the **Query editor** text area.

4.  Click **Run** .

5.  When the results are returned, click **Save results** .

6.  Under **Google Drive** , select **CSV** or **JSON** . When you save results to Google Drive, you cannot choose the location. Results are always saved to the root "My Drive" location.

7.  It may take a few minutes to save the results to Google Drive. When the results are saved, you receive a dialog message that includes the filename — `  bq-results-[TIMESTAMP]-[RANDOM_CHARACTERS].[CSV or JSON]  ` .

8.  In the dialog message, click **Open** to open the file, or navigate to Google Drive and click **My Drive** .

## Save query results to Google Sheets

Saving query results to Google Sheets is not supported by the bq command-line tool or the API.

You might get an error when you try to open the BigQuery results from Google Sheets. This error is due to the Drive SDK API being unable to access Google Workspace. To resolve the issue, you must enable your user account to [access Google Sheets](https://support.google.com/a/answer/6105699) with the Drive SDK API.

To save query results to Google Sheets, use the Google Cloud console:

1.  In the Google Cloud console, open the BigQuery page.

2.  Click add\_box **SQL query** .

3.  Enter a valid GoogleSQL query in the **Query editor** text area.

4.  Optional: To change the processing location, click **More** and select **Query settings** . For **Data location** , choose the [location](/bigquery/docs/locations) of your data.

5.  Click **Run** .

6.  When the results are returned, click the **Save results** and select **Google Sheets** .

7.  If necessary, follow the prompts to log into your user account and click **Allow** to give BigQuery permission to write the data to your Google Drive `  MY Drive  ` folder.
    
    After following the prompts, you should receive an email confirming that BigQuery client tools have been connected to your user account. The email contains information on the permissions you granted along with steps to remove the permissions.

8.  When the results are saved, a message similar to the following appears below the query results in the Google Cloud console: `  Saved to Sheets as "results-20190225-103531. Open  ` . Click the link in the message to view your results in Google Sheets, or navigate to your `  My Drive  ` folder and open the file manually.
    
    When you save query results to Google Sheets, the filename begins with `  results-[DATE]  ` where `  [DATE]  ` is today's date in the format `  YYYYMMDD  ` .
    
    **Note:** Saving results to Google Sheets is not supported by the bq command-line tool or the API. For more information, see [Using Connected Sheets](/bigquery/docs/connected-sheets) .

### Troubleshoot saving results to Google Sheets

When saving data from BigQuery to Google Sheets, you might find that some cells in the sheets are blank. This happens when the data you are writing to the cell exceeds the Google Sheets limit of 50,000 characters. To resolve this, use a [string function](/bigquery/docs/reference/standard-sql/string_functions#split) in the GoogleSQL query to split the column with the long data into two or more columns, then save the result to sheets again.

## Save query results to Cloud Storage

You can export your query results to Cloud Storage in the Google Cloud console with the following steps:

1.  Open the BigQuery page in the Google Cloud console.

2.  Click add\_box **SQL query** .

3.  Enter a valid GoogleSQL query in the **Query editor** text area.

4.  Click **Run** .

5.  When the results are returned, click **Save results** \> **Cloud Storage** .

6.  In the **Export to Google Cloud Storage** dialog:
    
      - For **GCS Location** , browse for the bucket, folder, or file where you want to export the data.
      - For **Export format** , choose the format for your exported data: CSV, JSON (Newline Delimited), Avro, or Parquet.
      - For **Compression** , select a compression format or select `  None  ` for no compression.

7.  Click **Save** to export the query results.

To check on the progress of the job, expand the **Job history** pane and look for the job with the `  EXTRACT  ` type.

## What's next

  - Learn how to programmatically [export a table to a JSON file](/bigquery/docs/samples/bigquery-extract-table-json) .
  - Learn about [quotas for extract jobs](/bigquery/quotas#export_jobs) .
  - Learn about [BigQuery storage pricing](https://cloud.google.com/bigquery/pricing#storage) .
