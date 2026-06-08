---
name: documents/docs.cloud.google.com/bigquery/docs/graph-search
uri: https://docs.cloud.google.com/bigquery/docs/graph-search
title: Search a graph
description: A fully managed, petabyte-scale analytics data warehouse that lets you run analytics over vast amounts of data in near real time.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> **Note:** To request support or provide feedback for this feature, send email to <bq-graph-preview-support@google.com> .

This tutorial shows you how to perform semantic search on your graph data by using [autonomous embedding generation](https://docs.cloud.google.com/bigquery/docs/autonomous-embedding-generation) and the [`AI.SEARCH` function](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-search) .

## Objectives

This tutorial covers the following tasks:

  - Create tables that hold information about people, financial accounts, account ownership, and account transfers.
  - Use autonomous embedding generation to simplify your embedding maintenance workflow.
  - Create a graph that defines the relationships between data stored in your tables.
  - Use the `AI.SEARCH` function on your graph nodes to perform semantic search on account descriptions.
  - Use the `AI.SEARCH` function on your graph edges to perform semantic search on account transfer notes.

## Costs

In this document, you use the following billable components of Google Cloud:

  - [BigQuery](https://cloud.google.com/bigquery/pricing) : You incur costs for the data that you process in BigQuery.

To generate a cost estimate based on your projected usage, use the [pricing calculator](https://docs.cloud.google.com/products/calculator) .

New Google Cloud users might be eligible for a [free trial](https://docs.cloud.google.com/free) .

When you finish the tasks that are described in this document, you can avoid continued billing by deleting the resources that you created. For more information, see [Clean up](https://docs.cloud.google.com/bigquery/docs/graph-search#clean-up) .

## Before you begin

### Console

1.  Make sure that you have the following role or roles on the project: **BigQuery Data Editor** , **Project IAM Admin**
    
    #### Check for the roles
    
    1.  In the Google Cloud console, go to the **IAM** page.
    
    2.  Select the project.
    
    3.  In the **Principal** column, find all rows that identify you or a group that you're included in. To learn which groups you're included in, contact your administrator.
    
    4.  For all rows that specify or include you, check the **Role** column to see whether the list of roles includes the required roles.
    
    #### Grant the roles
    
    1.  In the Google Cloud console, go to the **IAM** page.
    
    2.  Select the project.
    
    3.  Click person\_add **Grant access** .
    
    4.  In the **New principals** field, enter your user identifier. This is typically the email address for a Google Account.
    
    5.  Click **Select a role** , then search for the role.
    
    6.  To grant additional roles, click add **Add another role** and add each additional role.
    
    7.  Click **Save** .

### gcloud

1.  Grant roles to your user account. Run the following command once for each of the following IAM roles: `roles/bigquery.dataEditor, roles/resourcemanager.projectIamAdmin`
    
        gcloud projects add-iam-policy-binding PROJECT_ID --member="user:USER_IDENTIFIER" --role=ROLE
    
    Replace the following:
    
      - `  PROJECT_ID  ` : Your project ID.
      - `  USER_IDENTIFIER  ` : The identifier for your user account. For example, `myemail@example.com` .
      - `  ROLE  ` : The IAM role that you grant to your user account.

## Create tables

To store the tables and graph that you create in the following examples, [create a dataset](https://docs.cloud.google.com/bigquery/docs/datasets) . The following query creates a dataset called `graph_search` :

    CREATE SCHEMA IF NOT EXISTS graph_search;

The following tables contain information about people and accounts, and the relationships between each of these entities:

  - `Person` : information about people.
  - `Account` : information about bank accounts.
  - `PersonOwnAccount` : information about who owns which accounts.
  - `AccountTransferAccount` : information about transfers between accounts.

To create these tables, run the following [`CREATE TABLE` statements](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/data-definition-language#create_table_statement) :

    CREATE OR REPLACE TABLE graph_search.Person (
      id               INT64,
      name             STRING,
      PRIMARY KEY (id) NOT ENFORCED
    );
    
    CREATE OR REPLACE TABLE graph_search.Account (
      id                    INT64,
      create_time           TIMESTAMP,
      is_blocked            BOOL,
      description           STRING,
      description_embedding STRUCT<result ARRAY<FLOAT64>, status STRING>
                              GENERATED ALWAYS AS (
                              AI.EMBED(description, model => 'embeddinggemma-300m')
                              ) STORED OPTIONS( asynchronous = TRUE ),
      PRIMARY KEY (id) NOT ENFORCED
    );
    
    CREATE OR REPLACE TABLE graph_search.PersonOwnAccount (
      id               INT64 NOT NULL,
      account_id       INT64 NOT NULL,
      create_time      TIMESTAMP,
      PRIMARY KEY (id, account_id) NOT ENFORCED,
      FOREIGN KEY (id) REFERENCES graph_search.Person(id) NOT ENFORCED,
      FOREIGN KEY (account_id) REFERENCES graph_search.Account(id) NOT ENFORCED
    );
    
    CREATE OR REPLACE TABLE graph_search.AccountTransferAccount (
      id               INT64 NOT NULL,
      to_id            INT64 NOT NULL,
      amount           FLOAT64,
      create_time      TIMESTAMP NOT NULL,
      order_number     STRING,
      notes            STRING,
      notes_embedding  STRUCT<result ARRAY<FLOAT64>, status STRING>
                         GENERATED ALWAYS AS (
                         AI.EMBED(notes, model => 'embeddinggemma-300m')
                         ) STORED OPTIONS( asynchronous = TRUE ),
      PRIMARY KEY (id, to_id, create_time) NOT ENFORCED,
      FOREIGN KEY (id) REFERENCES graph_search.Account(id) NOT ENFORCED,
      FOREIGN KEY (to_id) REFERENCES graph_search.Account(id) NOT ENFORCED
    );

The `Account` and `AccountTransferAccount` tables use autonomous embedding generation to maintain embeddings for their `description` and `notes` columns.

In this tutorial we use the `embeddinggemma-300m` model because it runs in BigQuery and works well for short strings. For longer strings that exceed 128 tokens, you should choose a different embedding model, such as `text-embedding-005` . For more information, read about [choosing an embedding model](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-ai-embed#choose_a_model) .

## Insert data

The following queries insert some sample data into your tables. The [`INSERT` statements](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/dml-syntax#insert_statement) omit the embedding columns and BigQuery populates them automatically.

    INSERT INTO graph_search.Account
      (id, create_time, is_blocked, description)
    VALUES
      (7,"2020-01-10 06:22:20.222",false,"Fund for a refreshing tropical vacation"),
      (16,"2020-01-27 17:55:09.206",true,"Fund for a rainy day!"),
      (20,"2020-02-18 05:44:20.655",false,"Saving up for travel");
    
    INSERT INTO graph_search.Person
      (id, name)
    VALUES
      (1,"Alex"),
      (2,"Dana"),
      (3,"Lee");
    
    INSERT INTO graph_search.AccountTransferAccount
      (id, to_id, amount, create_time, order_number, notes)
    VALUES
      (7,16,300,"2020-08-29 15:28:58.647","304330008004315", "wedding present"),
      (7,16,100,"2020-10-04 16:55:05.342","304120005529714", "birthday gift"),
      (16,20,300,"2020-09-25 02:36:14.926","103650009791820", "for shared cost of dinner"),
      (20,7,500,"2020-10-04 16:55:05.342","304120005529714", "fees for tuition"),
      (20,16,200,"2020-10-17 03:59:40.247","302290001484851", "loved the lunch");
    
    INSERT INTO graph_search.PersonOwnAccount
      (id, account_id, create_time)
    VALUES
      (1,7,"2020-01-10 06:22:20.222"),
      (2,20,"2020-01-27 17:55:09.206"),
      (3,16,"2020-02-18 05:44:20.655");

## Create a graph

The following query uses the [`CREATE PROPERTY GRAPH` statement](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/graph-schema-statements#gql_create_graph) to create a graph called `FinGraph` in the `graph_search` dataset. The `Account` and `Person` tables are the node tables. The `AccountTransferAccount` and `PersonOwnAccount` tables are the edge tables, which represent relationships between the node tables.

    CREATE OR REPLACE PROPERTY GRAPH graph_search.FinGraph
    NODE TABLES (graph_search.Account, graph_search.Person)
    EDGE TABLES (
      graph_search.PersonOwnAccount
        SOURCE KEY (id) REFERENCES Person (id)
        DESTINATION KEY (account_id) REFERENCES Account (id)
        LABEL Owns,
      graph_search.AccountTransferAccount
        SOURCE KEY (id) REFERENCES Account (id)
        DESTINATION KEY (to_id) REFERENCES Account (id)
        LABEL Transfers
    );

## Search nodes

The following queries show who owns accounts for leisure travel and vacation. The first query uses a [`DECLARE` statement](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/procedural-language#declare) to create a variable called `similar_account` . The variable is initialized in the `DEFAULT` clause with a call to `AI.SEARCH` that find accounts whose descriptions are most semantically similar to `accounts for leisure travel and vacation` . The query sets the `top_k` argument to `2` in the call to `AI.SEARCH` to limit the number of results. The second query is a graph query that returns the account owner's name along with the account description.

    DECLARE similar_account DEFAULT ((
    SELECT ARRAY_AGG(base.id)
    FROM
      AI.SEARCH(
        (SELECT * FROM graph_search.Account WHERE description_embedding IS NOT NULL),
        'description',
        'accounts for leisure travel and vacation',
        top_k => 2)
    ));
    
    GRAPH graph_search.FinGraph
    MATCH (p:Person)-[:Owns]->(a:Account)
    WHERE a.id IN UNNEST(similar_account)
    RETURN p.name, a.description;

The result is similar to the following:

    +------+-----------------------------------------+
    | name | description                             |
    +------+-----------------------------------------+
    | Dana | Saving up for travel                    |
    | Alex | Fund for a refreshing tropical vacation |
    +------+-----------------------------------------+

## Search edges

The following queries show who made account transfers related to food payments. The first query uses the `AI.SEARCH` function to populate a variable called `food_transfers` . This variable holds the order number of transfers whose associated note is most semantically similar to `food` . The query sets the `top_k` argument to `2` in the call to `AI.SEARCH` to limit the number of results. The second query is a graph query that returns the account owner's name along with the transfer note.

    DECLARE food_transfers DEFAULT ((
    SELECT ARRAY_AGG(base.order_number)
    FROM
      AI.SEARCH(
        (SELECT * FROM graph_search.AccountTransferAccount WHERE notes_embedding IS NOT NULL),
        'notes',
        'food',
        top_k => 2)
    ));
    
    GRAPH graph_search.FinGraph
    MATCH (p:Person)-[:Owns]->(:Account)-[t:Transfers]->(:Account)
    WHERE t.order_number IN UNNEST(food_transfers)
    RETURN p.name, t.notes;

The result is similar to the following:

    +------+---------------------------+
    | name | notes                     |
    +------+---------------------------+
    | Dana | loved the lunch           |
    | Lee  | for shared cost of dinner |
    +------+---------------------------+

## Create a vector index

[Vector indexes](https://docs.cloud.google.com/bigquery/docs/vector-index-intro) reduce the latency and computational cost of your searches. The tables in this tutorial are too small to use a vector index. Vector indexes are useful when your tables are large, typically with millions of rows. BigQuery offers two types of index: IVF and TreeAH. For more information about creating an index and choosing a type, see [Manage vector indexes](https://docs.cloud.google.com/bigquery/docs/vector-index) .

## Clean up

To avoid incurring charges to your Google Cloud account for the resources used in this tutorial, either delete the project that contains the resources, or keep the project and delete the individual resources.

### Delete the project

> **Caution** : Deleting a project has the following effects:
> 
>   - **Everything in the project is deleted.** If you used an existing project for the tasks in this document, when you delete it, you also delete any other work you've done in the project.
>   - **Custom project IDs are lost.** When you created this project, you might have created a custom project ID that you want to use in the future. To preserve the URLs that use the project ID, such as an `appspot.com` URL, delete selected resources inside the project instead of deleting the whole project.
> 
> If you plan to explore multiple architectures, tutorials, or quickstarts, reusing projects can help you avoid exceeding project quota limits.

Delete a Google Cloud project:

    gcloud projects delete PROJECT_ID

## What's next

  - Learn more about [BigQuery Graph](https://docs.cloud.google.com/bigquery/docs/graph-overview) .
  - Learn how to [create and query a graph](https://docs.cloud.google.com/bigquery/docs/graph-create) .
  - Learn more about creating a vector index and performing [semantic search and RAG](https://docs.cloud.google.com/bigquery/docs/vector-index-text-search-tutorial) .
