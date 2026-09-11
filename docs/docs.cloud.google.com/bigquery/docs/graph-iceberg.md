---
name: documents/docs.cloud.google.com/bigquery/docs/graph-iceberg
uri: https://docs.cloud.google.com/bigquery/docs/graph-iceberg
title: Build a cross-cloud BigQuery Graph over an open borderless lakehouse
description: Build a single BigQuery Graph that unifies data silos across two clouds using an open borderless Lakehouse without data movement.
data_source: docs.cloud.google.com
---

# Build a cross-cloud property graph over an open borderless Lakehouse

The following tutorial shows you how to build a single BigQuery Graph that unifies data silos across two different clouds using an open borderless Lakehouse and Apache Iceberg REST catalog endpoints without moving data.

## Before you begin

Before you begin, set up your environment and enable the required APIs.

1.  Set your project and region, and enable the APIs:
    
        export PROJECT_ID="your-gcp-project-id"
        export REGION="us-east4"
        
        gcloud config set project "$PROJECT_ID"
        
        gcloud services enable \
          biglake.googleapis.com \
          bigquery.googleapis.com \
          secretmanager.googleapis.com \
          storage.googleapis.com

2.  Create a Python virtual environment for the loader:
    
        python3 -m venv iceberg-venv
        source iceberg-venv/bin/activate
        pip install --quiet "pyiceberg[pyarrow]"

## Create the Google Cloud spoke

Set up an open Apache Iceberg REST catalog backed by a Cloud Storage bucket, and load three Iceberg tables into it.

1.  Create the bucket and catalog:
    
        export GCS_BUCKET="gs://${PROJECT_ID}-xcloud-lake"
        export GCS_CATALOG="gcs_lake"
        
        gcloud storage buckets create "$GCS_BUCKET" \
          --project="$PROJECT_ID" \
          --location="$REGION"
        
        gcloud biglake iceberg catalogs create "$GCS_CATALOG" \
          --project="$PROJECT_ID" \
          --catalog-type=biglake \
          --primary-location="$REGION" \
          --default-location="$GCS_BUCKET"

2.  Save the following Python script as `load_gcs.py` to seed the tables:
    
        import subprocess, pyarrow as pa
        from pyiceberg.catalog.rest import RestCatalog
        from pyiceberg.schema import Schema
        from pyiceberg.types import NestedField, StringType, LongType, DoubleType
        import os
        
        PROJECT = os.environ["PROJECT_ID"]
        CATALOG = os.environ["GCS_CATALOG"]
        TOKEN = subprocess.check_output(
            ["gcloud", "auth", "application-default", "print-access-token"], text=True
        ).strip()
        
        cat = RestCatalog(
            name=CATALOG,
            uri="https://biglake.googleapis.com/iceberg/v1/restcatalog",
            warehouse=f"bl://projects/{PROJECT}/catalogs/{CATALOG}",
            token=TOKEN,
            **{"header.x-goog-user-project": PROJECT,
               "header.X-Iceberg-Access-Delegation": "vended-credentials"},
        )
        
        cat.create_namespace_if_not_exists("retail")
        
        def mk(name, schema, table):
            ident = ("retail", name)
            try: cat.drop_table(ident)
            except Exception: pass
            t = cat.create_table(ident, schema=schema)
            t.append(table)
            print(f"  {name}: {table.num_rows} rows")
        
        # customers
        mk("customers",
           Schema(NestedField(1, "customer_id", StringType()),
                  NestedField(2, "name", StringType()),
                  NestedField(3, "region", StringType())),
           pa.table({
               "customer_id": ["C1", "C2", "C3", "C4", "C5", "C6"],
               "name": ["Ana", "Ben", "Cara", "Dan", "Eve", "Finn"],
               "region": ["west", "west", "east", "east", "west", "south"],
           }))
        
        # orders
        mk("orders",
           Schema(NestedField(1, "order_id", StringType()),
                  NestedField(2, "customer_id", StringType()),
                  NestedField(3, "status", StringType()),
                  NestedField(4, "amount", DoubleType())),
           pa.table({
               "order_id": ["O1","O2","O3","O4","O5","O6","O7","O8","O9","O10"],
               "customer_id": ["C1","C1","C2","C3","C3","C4","C5","C5","C6","C2"],
               "status": ["shipped"]*8 + ["pending","shipped"],
               "amount": [156.0,89.0,120.0,147.0,89.0,199.0,25.0,88.0,80.0,224.0],
           }))
        
        # order_items
        mk("order_items",
           Schema(NestedField(1, "order_item_id", StringType()),
                  NestedField(2, "order_id", StringType()),
                  NestedField(3, "product_id", StringType()),
                  NestedField(4, "quantity", LongType()),
                  NestedField(5, "amount", DoubleType())),
           pa.table({
               "order_item_id": [f"OI{i}" for i in range(1, 16)],
               "order_id":  ["O1","O1","O2","O3","O3","O4","O5","O6","O6","O7","O8","O9","O10","O10","O2"],
               "product_id": ["P1","P2","P3","P1","P5","P4","P3","P6","P8","P7","P1","P2","P4","P5","P6"],
               "quantity":  [1,2,1,1,3,1,1,1,4,2,1,1,1,2,1],
               "amount":    [120.0,36.0,89.0,120.0,27.0,199.0,89.0,25.0,88.0,80.0,120.0,18.0,199.0,18.0,25.0],
           }))
        
        print("tables:", cat.list_tables("retail"))

3.  Run the script to load the tables:
    
        python load_gcs.py

4.  Verify the tables from BigQuery:
    
        bq --location="$REGION" query --use_legacy_sql=false \
          'SELECT customer_id, name, region
           FROM `'"$PROJECT_ID"'.gcs_lake.retail.customers`
           ORDER BY customer_id'

## Create the AWS spoke

Surface a Databricks Unity Catalog into BigQuery through an open borderless Lakehouse.

1.  In your Databricks SQL editor, create the products and suppliers tables:
    
        CREATE SCHEMA IF NOT EXISTS `<CATALOG>`.retail;
        
        CREATE OR REPLACE TABLE `<CATALOG>`.retail.suppliers (
          supplier_id STRING, name STRING, country STRING
        ) USING ICEBERG;
        
        INSERT INTO `<CATALOG>`.retail.suppliers VALUES
          ('S1','Acme','USA'), ('S2','Globex','Germany'),
          ('S3','Initech','Japan'), ('S4','Umbrella','UK');
        
        CREATE OR REPLACE TABLE `<CATALOG>`.retail.products (
          product_id STRING, name STRING, category STRING,
          supplier_id STRING, price DOUBLE
        ) USING ICEBERG;
        
        INSERT INTO `<CATALOG>`.retail.products VALUES
          ('P1','Widget','Gadgets',  'S1',120.0),
          ('P2','Gizmo','Gadgets',   'S1', 18.0),
          ('P3','Sprocket','Parts',  'S2', 89.0),
          ('P4','Cog','Parts',       'S2',199.0),
          ('P5','Bolt','Parts',      'S3',  9.0),
          ('P6','Nut','Parts',       'S3', 25.0),
          ('P7','Gear','Machinery',  'S4', 40.0),
          ('P8','Axle','Machinery',  'S4', 22.0);

2.  Grant read access to your service principal:
    
        GRANT USE CATALOG ON CATALOG `<CATALOG>` TO `<SP_APPLICATION_ID>`;
        GRANT USE SCHEMA, SELECT, EXTERNAL USE SCHEMA
          ON SCHEMA `<CATALOG>`.retail
          TO `<SP_APPLICATION_ID>`;

3.  Store the credentials in Secret Manager:
    
        export CLOUDSDK_API_ENDPOINT_OVERRIDES_SECRETMANAGER="https://secretmanager.${REGION}.rep.googleapis.com/"
        
        printf '{"client_id":"<SP_CLIENT_ID>","client_secret":"<SP_CLIENT_SECRET>"}' \
          | gcloud secrets create dbx-fed-sp \
              --project="$PROJECT_ID" \
              --location="$REGION" \
              --data-file=-

4.  Create the federated catalog:
    
        export DBX_HOST="<your-workspace-host-without-https>"
        export UC_CATALOG="<CATALOG>"
        
        gcloud alpha biglake iceberg catalogs create dbx_fed_catalog \
          --project="$PROJECT_ID" \
          --catalog-type=federated \
          --federated-catalog-type=unity \
          --unity-instance-name="$DBX_HOST" \
          --unity-catalog-name="$UC_CATALOG" \
          --secret-name="projects/${PROJECT_ID}/locations/${REGION}/secrets/dbx-fed-sp" \
          --primary-location="$REGION" \
          --refresh-interval=330s

5.  Grant the BigLake service account access to the secret:
    
        export BLIRC_SA="<paste-the-blirc-...-service-account-from-the-output>"
        export CLOUDSDK_API_ENDPOINT_OVERRIDES_SECRETMANAGER="https://secretmanager.${REGION}.rep.googleapis.com/"
        
        gcloud secrets add-iam-policy-binding dbx-fed-sp \
          --project="$PROJECT_ID" \
          --location="$REGION" \
          --member="serviceAccount:${BLIRC_SA}" \
          --role="roles/secretmanager.secretAccessor"

6.  Verify the sync:
    
        bq --location="$REGION" ls dbx_fed_catalog.retail
        
        bq --location="$REGION" query --use_legacy_sql=false \
          'SELECT product_id, name, category, supplier_id, price
           FROM `'"$PROJECT_ID"'.dbx_fed_catalog.retail.products`
           ORDER BY product_id'

## Create the cross-cloud property graph

Create a graph whose node and edge tables span both clouds.

1.  Create a dataset in your region:
    
        bq --location="$REGION" mk --dataset "${PROJECT_ID}:xcloud_graph"

2.  Create the graph:
    
        CREATE OR REPLACE PROPERTY GRAPH `PROJECT_ID.xcloud_graph.retail_xcloud`
        NODE TABLES (
          `PROJECT_ID.gcs_lake.retail.customers` AS Customer
            KEY (customer_id)
            LABEL Customer PROPERTIES (customer_id, name, region),
          `PROJECT_ID.gcs_lake.retail.orders` AS Orders
            KEY (order_id)
            LABEL OrderNode PROPERTIES (order_id, status, amount),
          `PROJECT_ID.gcs_lake.retail.order_items` AS OrderItems
            KEY (order_item_id)
            LABEL OrderItem PROPERTIES (order_item_id, quantity, amount),
          `PROJECT_ID.dbx_fed_catalog.retail.products` AS Products
            KEY (product_id)
            LABEL Product PROPERTIES (product_id, name, category, price),
          `PROJECT_ID.dbx_fed_catalog.retail.suppliers` AS Suppliers
            KEY (supplier_id)
            LABEL Supplier PROPERTIES (supplier_id, name, country)
        )
        EDGE TABLES (
          `PROJECT_ID.gcs_lake.retail.orders` AS Placed
            KEY (order_id)
            SOURCE KEY (customer_id) REFERENCES Customer (customer_id)
            DESTINATION KEY (order_id) REFERENCES Orders (order_id)
            LABEL PLACED,
          `PROJECT_ID.gcs_lake.retail.order_items` AS Contains_Item
            KEY (order_item_id)
            SOURCE KEY (order_id) REFERENCES Orders (order_id)
            DESTINATION KEY (order_item_id) REFERENCES OrderItems (order_item_id)
            LABEL CONTAINS_ITEM,
          `PROJECT_ID.gcs_lake.retail.order_items` AS Is_Product
            KEY (order_item_id)
            SOURCE KEY (order_item_id) REFERENCES OrderItems (order_item_id)
            DESTINATION KEY (product_id) REFERENCES Products (product_id)
            LABEL IS_PRODUCT,
          `PROJECT_ID.dbx_fed_catalog.retail.products` AS Supplied_By
            KEY (product_id)
            SOURCE KEY (product_id) REFERENCES Products (product_id)
            DESTINATION KEY (supplier_id) REFERENCES Suppliers (supplier_id)
            LABEL SUPPLIED_BY
        )

## Query the cross-cloud graph

Traverse the graph to query relationships across both clouds.

1.  Run a query that traverses relationships living on both clouds:
    
        GRAPH `PROJECT_ID.xcloud_graph.retail_xcloud`
        MATCH (c:Customer)-[:PLACED]->
              (o:OrderNode)-[:CONTAINS_ITEM]->
              (li:OrderItem)-[:IS_PRODUCT]->
              (p:Product)-[:SUPPLIED_BY]->
              (s:Supplier)
        RETURN
          c.name AS customer,
          o.order_id AS order_id,
          p.name AS product,
          p.category AS category,
          s.name AS supplier,
          s.country AS supplier_country,
          li.quantity AS qty
        ORDER BY customer, order_id
        LIMIT 50;

2.  Run a query to find which countries supply each customer:
    
        GRAPH `PROJECT_ID.xcloud_graph.retail_xcloud`
        MATCH (c:Customer)-[:PLACED]->
              (:OrderNode)-[:CONTAINS_ITEM]->
              (:OrderItem)-[:IS_PRODUCT]->
              (:Product)-[:SUPPLIED_BY]->
              (s:Supplier)
        RETURN DISTINCT c.name AS customer, s.country AS supplier_country
        ORDER BY customer, supplier_country;

## Clean up

To avoid incurring charges to your Google Cloud account for the resources used on this page, follow these steps.

To avoid ongoing charges, remove the resources that you created.

1.  Delete the graph dataset:
    
        bq rm -r -f -d "${PROJECT_ID}:xcloud_graph"

2.  Delete the federated catalog:
    
        gcloud alpha biglake iceberg catalogs delete dbx_fed_catalog --project="$PROJECT_ID"

3.  Save the following script as `drop_gcs.py` to drop the GCS tables and namespace:
    
        import subprocess, os
        from pyiceberg.catalog.rest import RestCatalog
        
        PROJECT = os.environ["PROJECT_ID"]
        CATALOG = os.environ["GCS_CATALOG"]
        TOKEN = subprocess.check_output(
            ["gcloud", "auth", "application-default", "print-access-token"], text=True
        ).strip()
        
        cat = RestCatalog(
            name=CATALOG,
            uri="https://biglake.googleapis.com/iceberg/v1/restcatalog",
            warehouse=f"bl://projects/{PROJECT}/catalogs/{CATALOG}",
            token=TOKEN,
            **{"header.x-goog-user-project": PROJECT},
        )
        for tbl in cat.list_tables("retail"):
            cat.drop_table(tbl)
        cat.drop_namespace("retail")
        print("emptied", CATALOG)

4.  Run the script:
    
        python drop_gcs.py

5.  Delete the Cloud Storage catalog:
    
        gcloud biglake iceberg catalogs delete "$GCS_CATALOG" --project="$PROJECT_ID"

6.  Delete the secret:
    
        export CLOUDSDK_API_ENDPOINT_OVERRIDES_SECRETMANAGER="https://secretmanager.${REGION}.rep.googleapis.com/"
        gcloud secrets delete dbx-fed-sp --project="$PROJECT_ID" --location="$REGION"

7.  Delete the bucket:
    
        gcloud storage rm -r "$GCS_BUCKET"

## What's next

  - Learn more about [BigQuery Graph](https://docs.cloud.google.com/bigquery/docs/graph-overview) .
  - Learn more about [borderless Lakehouse concepts](https://docs.cloud.google.com/lakehouse/docs/about-borderless-lakehouse) .
  - Learn how to [use borderless Lakehouse](https://docs.cloud.google.com/lakehouse/docs/use-borderless-lakehouse) .
  - Refer to the [GQL query statements](https://docs.cloud.google.com/bigquery/docs/reference/standard-sql/graph-query-statements) .
