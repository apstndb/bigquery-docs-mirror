---
name: documents/docs.cloud.google.com/bigquery/docs/security-bulletins
uri: https://docs.cloud.google.com/bigquery/docs/security-bulletins
title: Security bulletins
description: Read the latest security bulletins for BigQuery.
data_source: docs.cloud.google.com
---

# Security bulletins

This page describes all security bulletins related to BigQuery.

## GCP-2026-084

**Published:** 2026-11-19

### Description

| Description                                                                                                                                                                                                                                                                                                                                                                                                            | Severity | Notes                                                               |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|---------------------------------------------------------------------|
| A path traversal vulnerability in workspace directory handling and Git integration was discovered in Dataform, BigQuery Studio, and Colab Enterprise. What should I do? No customer action is required. This vulnerability was patched on October 10, 2026. What vulnerabilities are being addressed? An authenticated remote attacker could read private files and create arbitrary files across tenant repositories. | Critical | [CVE-2026-126054](https://www.cve.org/CVERecord?id=CVE-2026-126054) |

## GCP-2026-056

**Published** : 2026-08-26

| Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | Severity | Notes                                                                           |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|---------------------------------------------------------------------------------|
| An Improper Input Validation vulnerability was discovered in the [JDBC driver](https://docs.cloud.google.com/bigquery/docs/jdbc-for-bigquery) in BigQuery Data Transfer Service versions prior to May 1, 2026. What should I do? No customer action is required. This vulnerability was patched on May 1, 2026. What vulnerabilities are being addressed? An authenticated attacker could use crafted JDBC connection string parameters to achieve remote code execution in the connector container and escalate privileges in the tenant project. | Critical | [CVE-2026-12717](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2026-12717) |

## GCP-2026-047

**Published** : 2026-07-13

| Description                                                                                                                                                                                                                                                                                                                                                                                                                                  | Severity | Notes                                                                           |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|---------------------------------------------------------------------------------|
| A Missing Authorization vulnerability was discovered in repositories in BigQuery, Dataform, and Colab Enterprise. What should I do? No customer action is required. Google has already applied mitigations to all impacted products and services. What vulnerabilities are being addressed? During repository creation, an authenticated attacker could potentially escalate their permissions and perform cross-tenant repository takeover. | Critical | [CVE-2026-14934](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2026-14934) |
