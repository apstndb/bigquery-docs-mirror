---
name: documents/docs.cloud.google.com/bigquery/docs/data-analysis-tools-intro
uri: https://docs.cloud.google.com/bigquery/docs/data-analysis-tools-intro
title: Introduction to analysis and business intelligence tools
description: Learn about the tools you can use to analyze and visualize your data in BigQuery.
data_source: docs.cloud.google.com
---

# Introduction to analysis and business intelligence tools

You can integrate analysis and business intelligence (BI) tools with BigQuery to discover actionable insights from your data warehouse. Several tools complement BigQuery, letting you build interactive dashboards, create custom data applications, or perform programmatic analysis without moving your datasets.

## Connected Sheets

[Connected Sheets](https://docs.cloud.google.com/bigquery/docs/connected-sheets) lets you access, analyze, visualize, and share billions of rows of BigQuery data from your [Google Sheets spreadsheets](https://www.google.com/sheets/about/) . The Connected Sheets interface simplifies collaboration with non-technical project stakeholders, requires no additional data exports, streamlines reporting, and provides powerful access control capabilities.

To learn more about using Connected Sheets with BigQuery, see [Use Connected Sheets](https://docs.cloud.google.com/bigquery/docs/connected-sheets) .

## Looker

[Looker](https://docs.cloud.google.com/bigquery/docs/looker) is Google's enterprise platform for data visualization and business intelligence. It is useful for advanced data analytics, predictive analysis, and custom data applications. It can also connect to transactional databases in other public clouds.

To learn more about using Looker with BigQuery, see [Analyze data with BigQuery BI Engine and Looker](https://docs.cloud.google.com/bigquery/docs/looker) .

## Data Studio

[Data Studio](https://docs.cloud.google.com/bigquery/docs/visualize-looker-studio) is a Google tool for data visualization and business intelligence. It connects to BigQuery directly from the Google Cloud console and is useful for building graphics, reports, and dashboards.

To learn more about using Data Studio with BigQuery, see [Analyze data with Data Studio](https://docs.cloud.google.com/bigquery/docs/visualize-looker-studio) .

## Programmatic analysis tools

[Programmatic analysis tools](https://docs.cloud.google.com/bigquery/docs/programmatic-analysis) can run code to analyze data managed in BigQuery. While SQL is a powerful query language, Python, Java, or R often provide a more simplified, expressive way to perform data analysis. Such tools include open source web-based applications like Jupyter Notebooks and Apache Zeppelin. [Vertex AI Workbench](https://docs.cloud.google.com/gemini-enterprise-agent-platform/notebooks/workbench/introduction) is a Google tool that offers JupyterLab notebook environments for programmatic analysis.

## Third-party tools

You can also connect to BigQuery using a number of popular third-party tools such as [Tableau](https://help.tableau.com/current/pro/desktop/en-us/examples_googlebigquery.htm) and [Microsoft Power BI](https://docs.microsoft.com/en-us/power-bi/connect-data/desktop-connect-bigquery) .

The BigQuery Ready program offers a [full list of validated partner solutions](https://docs.cloud.google.com/bigquery/docs/bigquery-ready-partners) .

If you need assistance with a solution, consider contacting a [Google Cloud Ready - BigQuery partner](https://console.cloud.google.com/bigquery/partner-center) . Third-party software isn't supported by Cloud Customer Care when it has been identified that BigQuery is working as intended.

### Network connectivity

All BI and data analytics solutions that are deployed on hosts and services with external IP addresses can access BigQuery through the public [BigQuery REST API](https://docs.cloud.google.com/bigquery/docs/reference/rest) and the RPC-based [BigQuery Storage API](https://docs.cloud.google.com/bigquery/docs/reference/storage) over the internet.

Third-party BI and data analytics solutions that are deployed on [Compute Engine](https://docs.cloud.google.com/compute) VM instances that only have internal IP addresses can use [Private Google Access](https://docs.cloud.google.com/vpc/docs/private-google-access) to reach Google APIs and services like BigQuery. To enable a subnet for Private Google Access and view the requirements, see [Configuring Private Google Access](https://docs.cloud.google.com/vpc/docs/configure-private-google-access) .

Third-party BI and data analytics solutions that are deployed on on-premises hosts can use [Private Google Access for on-premises hosts](https://docs.cloud.google.com/vpc/docs/private-google-access-hybrid) to reach Google APIs and services like BigQuery. This service establishes a private connection over a [Cloud VPN](https://docs.cloud.google.com/network-connectivity/docs/vpn) or [Cloud Interconnect](https://docs.cloud.google.com/network-connectivity/docs/interconnect) from your data center to Google Cloud. On-premises hosts don't need external IP addresses; instead, they use internal [RFC 1918](https://tools.ietf.org/html/rfc1918) IP addresses. To enable Private Google Access for on-premises hosts, you must configure DNS, firewall rules, and routes in your on-premises and VPC networks. For more details on Private Google Access for on-premises hosts, see [Configuring Private Google Access for on-premises hosts](https://docs.cloud.google.com/vpc/docs/configure-private-google-access-hybrid) .

If you manage your own instance of a third-party BI solution, consider deploying it on [Compute Engine](https://docs.cloud.google.com/compute) to minimize latency between your instance and BigQuery.

If your BI solution supports it, you might consider setting filters in report or dashboard queries whenever possible. This step pushes the filters as `WHERE` clauses to BigQuery. Although setting these filters doesn't reduce the amount of data that BigQuery scans, it does reduce the amount of data that comes back over the network.

For more information on network and query optimizations, see [Optimize workloads](https://docs.cloud.google.com/bigquery/docs/admin-intro#optimize_workloads) and the [Introduction to optimizing query performance](https://docs.cloud.google.com/bigquery/docs/best-practices-performance-overview) .

### ODBC and JDBC drivers

For third-party solutions and custom applications that don't integrate with the [BigQuery API](https://docs.cloud.google.com/bigquery/docs/reference/libraries-overview) , [Magnitude Simba](https://www.magnitude.com/products/data-connectivity) provides [ODBC](https://wikipedia.org/wiki/Open_Database_Connectivity) and [JDBC](https://wikipedia.org/wiki/Java_Database_Connectivity) drivers to help you use BigQuery with your existing tools.

### Authentication

The BigQuery API uses [OAuth 2.0](https://tools.ietf.org/html/rfc6749) access tokens to authenticate requests. An OAuth 2.0 access token is a string that grants temporary access to an API. [Google's OAuth 2.0 server](https://developers.google.com/identity/protocols/OAuth2WebServer#obtainingaccesstokens) grants access tokens for all Google APIs. Access tokens are associated with a [scope](https://tools.ietf.org/html/rfc6749#section-3.3) , which limits the token's access. For scopes associated with the BigQuery API, see the complete [list of Google API scopes](https://developers.google.com/identity/protocols/googlescopes#bigqueryv2) .

Solutions that offer native BigQuery integration can automatically generate access tokens for BigQuery by using [OAuth 2.0 protocols](https://developers.google.com/identity/protocols/OAuth2) or customer-supplied [service account private keys](https://docs.cloud.google.com/iam/docs/creating-managing-service-account-keys) . Similarly, solutions that rely on Simba ODBC/JDBC drivers can also obtain access tokens [for a Google user account](https://www.simba.com/products/BigQuery/doc/ODBC_InstallGuide/mac/content/odbc/bq/configuring/authenticating/useraccount.htm) or [for a Google service account](https://www.simba.com/products/BigQuery/doc/ODBC_InstallGuide/mac/content/odbc/bq/configuring/authenticating/serviceaccount.htm) .

## What's next

- Learn how to [use Connected Sheets](https://docs.cloud.google.com/bigquery/docs/connected-sheets) .
- Learn how to [visualize data in Data Studio](https://docs.cloud.google.com/bigquery/docs/visualize-looker-studio) .
- Learn how to [use Looker](https://docs.cloud.google.com/bigquery/docs/looker) .
- Learn how to [use ODBC and JDBC drivers](https://docs.cloud.google.com/bigquery/docs/reference/odbc-jdbc-drivers) .
- Learn how to [use programmatic analysis tools](https://docs.cloud.google.com/bigquery/docs/programmatic-analysis) .
