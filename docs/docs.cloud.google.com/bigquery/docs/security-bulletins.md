---
name: documents/docs.cloud.google.com/bigquery/docs/security-bulletins
uri: https://docs.cloud.google.com/bigquery/docs/security-bulletins
title: Security bulletins
description: Read the latest security bulletins for BigQuery.
data_source: docs.cloud.google.com
---

# Security bulletins

This page describes all security bulletins related to BigQuery.

## GCP-2026-056

**Published** : 2026-08-26

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Description</th>
<th>Severity</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>An Improper Input Validation vulnerability was discovered in the <a href="https://docs.cloud.google.com/bigquery/docs/jdbc-for-bigquery">JDBC driver</a> in BigQuery Data Transfer Service versions prior to May 1, 2026.</p>
<h4 id="what-should-i-do" data-text="What should I do?" tabindex="-1">What should I do?</h4>
<p>No customer action is required. This vulnerability was patched on May 1, 2026.</p>
<h4 id="what-vulnerabilities-are-being-addressed" data-text="What vulnerabilities are being addressed?" tabindex="-1">What vulnerabilities are being addressed?</h4>
<p>An authenticated attacker could use crafted JDBC connection string parameters to achieve remote code execution in the connector container and escalate privileges in the tenant project.</p></td>
<td>Critical</td>
<td><a href="https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2026-12717">CVE-2026-12717</a></td>
</tr>
</tbody>
</table>

## GCP-2026-047

**Published** : 2026-07-13

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Description</th>
<th>Severity</th>
<th>Notes</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>A Missing Authorization vulnerability was discovered in repositories in BigQuery, Dataform, and Colab Enterprise.</p>
<h4 id="what-should-i-do_1" data-text="What should I do?" tabindex="-1">What should I do?</h4>
<p>No customer action is required. Google has already applied mitigations to all impacted products and services.</p>
<h4 id="what-vulnerabilities-are-being-addressed_1" data-text="What vulnerabilities are being addressed?" tabindex="-1">What vulnerabilities are being addressed?</h4>
<p>During repository creation, an authenticated attacker could potentially escalate their permissions and perform cross-tenant repository takeover.</p></td>
<td>Critical</td>
<td><a href="https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2026-14934">CVE-2026-14934</a></td>
</tr>
</tbody>
</table>
