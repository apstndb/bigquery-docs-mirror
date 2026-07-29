---
name: documents/docs.cloud.google.com/bigquery/docs/agent-skills-overview
uri: https://docs.cloud.google.com/bigquery/docs/agent-skills-overview
title: BigQuery agent skills
description: BigQuery provides agent skills, including bigquery-basics and bigquery-ai-ml, that help your agent accomplish common tasks.
data_source: docs.cloud.google.com
---

# BigQuery agent skills

BigQuery provides agent skills that can help your agent accomplish common tasks. Agents that use these skills can then accomplish tasks with higher fidelity than an agent without the skills.

Agent skills are a standardized way to give AI agents specific knowledge and instructions they can reuse. They contain resources like scripts, reference materials, and templates that help the agent complete tasks accurately and reliably. For more information about skills, see [Agent Skills Overview](https://agentskills.io/home) .

## The BigQuery basics skill

The BigQuery basics skill, [`bigquery-basics`](https://github.com/google/skills/tree/main/skills/cloud/bigquery-basics) , contains instructions for completing basic tasks in BigQuery, such as creating a dataset or running a query.

### Install the BigQuery basics skill

To install the `bigquery-basics` skill, run the following command in your agentic client or terminal:

    npx skills add google/skills --skill bigquery-basics

### BigQuery basics reference files

The BigQuery basics agent skill includes several reference files that provide technical depth. These references let the skill execute functions or commands accurately by providing specific context to the underlying model. By default, the BigQuery basics skill includes the following reference files:

  - [bq command-line tool usage](https://github.com/google/skills/blob/main/skills/cloud/bigquery-basics/references/cli-usage.md)
  - [Cloud Client Libraries usage](https://github.com/google/skills/blob/main/skills/cloud/bigquery-basics/references/client-library-usage.md)
  - [Core concepts](https://github.com/google/skills/blob/main/skills/cloud/bigquery-basics/references/core-concepts.md)
  - [Infrastructure as code (IAC) usage](https://github.com/google/skills/blob/main/skills/cloud/bigquery-basics/references/iac-usage.md)
  - [Identity and Access Management (IAM) security](https://github.com/google/skills/blob/main/skills/cloud/bigquery-basics/references/iam-security.md)
  - [Model Context Protocol (MCP) usage](https://github.com/google/skills/blob/main/skills/cloud/bigquery-basics/references/mcp-usage.md)

## The BigQuery AI & ML skill

The BigQuery AI & ML skill, [`bigquery-ai-ml`](https://github.com/google/skills/tree/main/skills/cloud/bigquery-ai-ml) , contains instructions for completing data science, machine learning, and AI tasks in BigQuery.

### Install the BigQuery AI & ML skill

To install the `bigquery-ai-ml` skill, run the following command in your agentic client or terminal:

    npx skills add google/skills --skill bigquery-ai-ml

### BigQuery AI & ML reference files

The BigQuery AI & ML agent skill includes reference files that provide technical depth. By default, the BigQuery AI & ML skill includes the following reference files:

  - [`AI.DETECT_ANOMALIES`](https://github.com/google/skills/blob/main/skills/cloud/bigquery-ai-ml/references/ai_detect_anomalies.md)
  - [`AI.FORECAST`](https://github.com/google/skills/blob/main/skills/cloud/bigquery-ai-ml/references/ai_forecast.md)
  - [`AI.GENERATE`](https://github.com/google/skills/blob/main/skills/cloud/bigquery-ai-ml/references/ai_generate.md)

## What's next

  - To view the BigQuery basics `SKILL.md` file, see [`SKILL.md` (basics)](https://github.com/google/skills/blob/main/skills/cloud/bigquery-basics/SKILL.md) .
  - To view the BigQuery AI & ML `SKILL.md` file, see [`SKILL.md` (AI & ML)](https://github.com/google/skills/blob/main/skills/cloud/bigquery-ai-ml/SKILL.md) .
  - To learn more about agent skills, see [Agent Skills Overview](https://agentskills.io/home) .
  - To view `SKILL.md` files for other Google Cloud products, see [`google/skills`](https://github.com/google/skills#agent-skills) .
