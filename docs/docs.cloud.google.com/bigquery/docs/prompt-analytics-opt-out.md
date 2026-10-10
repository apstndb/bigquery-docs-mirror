---
name: documents/docs.cloud.google.com/bigquery/docs/prompt-analytics-opt-out
uri: https://docs.cloud.google.com/bigquery/docs/prompt-analytics-opt-out
title: Opt out from prompt analytics
description: Learn how to opt out from prompt analytics.
data_source: docs.cloud.google.com
---

# Opt out from prompt analytics

To improve the quality, accuracy, and reliability of conversational analytics, Google analyzes anonymized prompt data across customer interactions. This data helps identify common usage patterns, detect gaps in comprehension, and improve overall product performance. This data isn't used to train or fine tune Google's foundational AI models. This data processing is enabled by default.

To opt out from prompt analytics, do one of the following:

- To opt out *before* November 23, 2026, complete the following steps:
  1.  Use the Resource Manager API, CLI, or the Google Cloud console to obtain project numbers, or find your organization ID to opt out all existing BigQuery projects in an organization.
  2.  Submit the [opt-out form](https://docs.google.com/forms/d/e/1FAIpQLSc3Jtc0cM2t2HXcyN_yRQJ0xVm3giGDCXvHft_l1jid_Jp7tw/viewform) , including the project IDs that you want to exclude.
- To opt out *on or after* November 23, 2026, apply the custom, hierarchical Organization Policy Service constraint `constraints/gcp.disablePromptAnalytics` to block prompt ingestion at the Organization, Folder, or Project level.

You can re-enable prompt analytics within the Google Cloud console administrator settings. You must remove the custom Organization Policy Service constraint if you previously applied it.

To learn more, see [Service Specific Terms](https://cloud.google.com/terms/service-terms) for BigQuery conversational analytics.

## What's next

- [Learn about conversational analytics in BigQuery](https://docs.cloud.google.com/bigquery/docs/conversational-analytics) .
- [Create data agents](https://docs.cloud.google.com/bigquery/docs/create-data-agents) .
