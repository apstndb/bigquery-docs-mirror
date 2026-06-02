---
name: documents/docs.cloud.google.com/bigquery/docs/bigquery-agent-analytics
uri: https://docs.cloud.google.com/bigquery/docs/bigquery-agent-analytics
title: Use BigQuery agent analytics
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

# Use BigQuery agent analytics

BigQuery agent analytics is an open source solution that lets you capture, analyze, and visualize multimodal agent interaction data at scale by streaming raw agent interactions—such as requests, responses, tool calls, and errors—directly into BigQuery. This solution lets you perform AI-powered evaluations, optimize agent prompts, and extract long-term memory to enhance future interactions. BigQuery agent analytics is supported in [Agent Development Kit (ADK)](https://google.github.io/adk-docs/integrations/bigquery-agent-analytics/) and [LangGraph](https://docs.langchain.com/oss/python/integrations/callbacks/google_bigquery) (Preview).

## Architecture

BigQuery agent analytics streams agent activity data to BigQuery using the [BigQuery Storage Write API](https://docs.cloud.google.com/bigquery/docs/write-api) , which provides high-throughput, low-latency log streaming without blocking agent execution.

The data flow consists of these stages:

1.  **Capture** . Use plugins in the Agent Development Kit (ADK) or callbacks in LangGraph intercept interaction events to capture agent events.
2.  **Stream** . Interaction events are sent to BigQuery through the Storage Write API. If a standardized schema doesn't exist, the agent creates one automatically.
3.  **Consume** . Analyze and evaluate logged agent data. You can query raw data with SQL, track metrics on custom dashboards, or use the [BigQuery agent analytics SDK](https://github.com/GoogleCloudPlatform/BigQuery-Agent-Analytics-SDK) to reconstruct and evaluate complex multi-turn agent execution traces.

![Diagram showing agent activity data flowing from orchestration frameworks into BigQuery for analysis.](https://docs.cloud.google.com/static/bigquery/images/agent-analytics-architecture.png)

### Agent analytics benefits

  - Enable comprehensive logging with a single line of code and automate schema management.
  - Log and analyze multimodal data, such as text, images, video, and audio, by using object tables.
  - Track operational metrics, such as token consumption and latency, within a robust, predefined schema.
  - Identify optimization opportunities by using BigQuery generative AI functions and vector search.
  - Secure agent logs with granular access controls, data masking, and encryption.

## Ways to capture agent log data

To capture your agent's interaction telemetry (requests, responses, tool calls, and error logs) natively into BigQuery, you can log event data in several ways:

  - **Orchestration framework plugins** : use standard logging plugins provided by your agent orchestration toolkit. For example, the `BigQueryAgentAnalyticsPlugin` in the Agent Development Kit (ADK) hooks into the agent runner to automatically intercept, serialize, and stream events.
  - **Framework callback handlers** : integrate standard callbacks in popular agent environments. For example, you can use the built-in BigQuery handler in LangGraph and LangChain to intercept and forward traces.
  - **Direct API ingestion** : for custom or proprietary frameworks, use the Google Cloud client libraries to stream structured events directly to your events table using the Storage Write API.

Regardless of the method, all logging options use the low-latency, high-throughput **[BigQuery Storage Write API](https://docs.cloud.google.com/bigquery/docs/write-api)** . This API provides a robust streaming endpoint that buffers and serializes rows (using the PyArrow engine) asynchronously in memory before committing them, ensuring that observability pipeline tasks don't block your user-facing agent execution turns.

## Ways to analyze agent log data

To understand and optimize your agent's performance, analyze and evaluate interaction logs in the following ways:

  - **Direct SQL queries** : run custom queries in BigQuery to compute metrics like token consumption and execution latency. You can also use [`AI.GENERATE`](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate) for automated root-cause analysis of errors, or perform joins with business tables to measure business impact.
  - **Interactive dashboards** : connect visualization tools like [Data Studio](https://docs.cloud.google.com/data-studio/welcome) to prebuilt or custom BigQuery views to track agent health, error rates, and usage trends over time.
  - **Jupyter notebooks** : [explore and experiment](https://docs.cloud.google.com/bigquery/docs/bigquery-agent-analytics#use-a-notebook) with log data using Python libraries, pandas, or BigFrames in interactive environments.
  - **Python SDK** : [programmatically](https://docs.cloud.google.com/bigquery/docs/bigquery-agent-analytics#use-the-sdk) query, reconstruct, and audit agent execution traces directly in your application code or automated evaluation pipelines.

## Examples of working with agent log data

The following are common use cases and examples of working with agent log data in BigQuery.

### Observability and operational metrics

  - [Query data](https://adk.dev/integrations/bigquery-agent-analytics/#query-recipes) to break down costs by agent flows and determine if a specific agent, such as a refinement agent, consumes a disproportionate amount of tokens compared to its contribution to final responses.
  - Use the [BigQuery conversational analytics agent](https://docs.cloud.google.com/bigquery/docs/conversational-analytics) for AI-powered root cause analysis by running queries with [the `AI.GENERATE` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-generate) . For example, "Analyze this conversation log and explain the root cause of the failure."

### Agent evaluation and quality analysis

  - Rank conversations and measure agent rank over time by using the [`AI.SCORE` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-score) .
  - Identify conversation clusters where the agent failed to assist users by using a SQL query with [Vector Search](https://docs.cloud.google.com/bigquery/docs/vector-search-intro) , and then compare them to the user's original intent. This helps you identify gaps in the agent's tools or knowledge base.

### Business insights and contextualization

To contextualize agent data, join the `agent_events` table with other business tables . For example, show the average order value (AOV) for customers who interacted with the AI agent versus customers who used the search bar.

For more examples, see [Advanced analysis queries](https://google.github.io/adk-docs/integrations/bigquery-agent-analytics/#advanced-analysis-queries) .

### Use a Jupyter notebook to work with agent logs

Use this [example Colab Jupyter notebook](https://github.com/GoogleCloudPlatform/BigQuery-Agent-Analytics-SDK/blob/main/examples/dashboard_v2.ipynb) to interactively query, visualize, and evaluate agent logs.

## Use the BigQuery agent analytics SDK

The [BigQuery agent analytics SDK](https://github.com/GoogleCloudPlatform/BigQuery-Agent-Analytics-SDK) is an open-source Python library that provides a consumption and evaluation layer for long-term agent observability. Dashboards and notebooks are excellent for ad hoc exploration, and the SDK provides a way to systematically analyze and audit agent behavior at scale.

### What you can do with the SDK

You can perform the following tasks using the BigQuery agent analytics SDK. For detailed examples of log analysis, see the [GitHub repository for the SDK](https://github.com/GoogleCloudPlatform/BigQuery-Agent-Analytics-SDK/blob/main/SDK.md) .

  - **Trace reconstruction** : reconstruct polymorphic event logs into causal chains of events to debug sessions across multiple turns, including nested tool and LLM calls.
  - **Deterministic and semantic evaluation** : assess agent quality against rule-based criteria, such as latency, turn counts, and error rates, as well as semantic criteria, such as correctness, sentiment, and hallucination.
  - **Trajectory matching** : compare actual agent execution paths against expected golden trajectories to verify step efficiency and whether tools were used in the correct order.
  - **Behavioral monitoring and drift detection** : perform statistical analyses over non-deterministic agent outputs, monitor user request distributions, and detect production regression or semantic drift.
  - **Long-horizon agent memory** : provide agents with cross-session context, user profile semantic retrieval, and token-budget-aware episodic memory stored natively in BigQuery.

### Log and analyze agent activity

Integrating the SDK into your agent workflows typically involves the following steps:

1.  **Log interactions** : Attach a logger plugin (such as the `BigQueryAgentAnalyticsPlugin` in ADK) or a callback handler in your agent orchestration framework. When users interact with your agent, the logs are streamed asynchronously to BigQuery using the high-throughput Storage Write API.

2.  **Initialize the client** : Connect to your log dataset from the Python SDK:
    
        from google.cloud import bigquery
        from bigquery_agent_analytics import Client
        
        client = Client(
            project_id="YOUR_PROJECT_ID",
            dataset_id="YOUR_DATASET_ID",
            table_id="agent_events",
        )
    
    The snippet uses the following components:
    
      - `client` : the parent `Client` instance that programmatically routes queries and manages active database connections.
      - `project_id` : the Google Cloud project ID housing the target dataset.
      - `dataset_id` : the BigQuery dataset name storing logs.
      - `table_id` : the specific table storing telemetry events ( `agent_events` by default).

3.  **Reconstruct a session trace** : Fetch a specific conversation session to visualize and review the exact sequence of events:
    
        trace = client.get_trace(
            session_id="YOUR_SESSION_ID"
        )
        trace.render()
    
    The snippet uses the following components:
    
      - `trace` : the hydrated `Trace` object housing the reconstructed causally linked hierarchical DAG span tree of all user and agent actions.
      - `  YOUR_SESSION_ID  ` : the unique ID of the session you want to inspect.

4.  **Run automated evaluations** : Programmatically score session trajectories or check for regression against a golden test suite:
    
        from bigquery_agent_analytics.evaluators import CodeEvaluator, LLMAsJudge
        from bigquery_agent_analytics.grader_pipeline import GraderPipeline
        
        # Create a grader pipeline with deterministic and semantic metrics
        evaluator = GraderPipeline(
            graders=[
                CodeEvaluator.latency(threshold_ms=5000),
                LLMAsJudge.correctness(),
            ]
        )
        report = client.evaluate(evaluator, session_ids=["session_1", "session_2"])
        print(f"Evaluation Pass Rate: {report.pass_rate:.2%}")
    
    The snippet uses the following components:
    
      - `evaluator` : the structured `GraderPipeline` compiled logic composing heterogeneous rule-based and semantic evaluation metrics.
      - `session_ids` : the list of session ID strings to run batch evaluations against in BigQuery.
      - `report` : the resulting `EvaluationReport` object containing raw session grades, metric summaries, trial stats, and auto-rater feedback.

## Integrate BigQuery agent analytics into your workflow

To integrate BigQuery agent analytics into your workflow, see the documentation for your framework:

  - [ADK BigQuery Analytics plugin guide](https://google.github.io/adk-docs/integrations/bigquery-agent-analytics/)
  - [BigQuery callback handler integration](https://docs.langchain.com/oss/python/integrations/callbacks/google_bigquery) (LangChain and LangGraph)

## What's next

  - [Explore the codelab](https://codelabs.developers.google.com/adk-bigquery-agent-analytics-plugin#0) .
