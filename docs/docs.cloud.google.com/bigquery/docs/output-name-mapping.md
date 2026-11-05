---
name: documents/docs.cloud.google.com/bigquery/docs/output-name-mapping
uri: https://docs.cloud.google.com/bigquery/docs/output-name-mapping
title: Map SQL object names for translation
description: Describes how to specify output name mapping rules for use in SQL translation.
data_source: docs.cloud.google.com
---

# Map SQL object names for translation

> **Preview**
>
> This product is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

Name mapping lets you map SQL object names in your source files to target names in BigQuery by using a [configuration YAML](https://docs.cloud.google.com/bigquery/docs/config-yaml-translation#output_name_mapping) file. During SQL translation, all references to each source name across your SQL statements update to the target name in the translated output.

You can use some or all of the following components to configure name mapping for an object:

- A name mapping rule, composed of:
  - Source [name parts](https://docs.cloud.google.com/bigquery/docs/output-name-mapping#name_parts) that provide the fully qualified name of the object in the source system.
  - Target name parts that provide the name of the object in BigQuery.
- A [default database](https://docs.cloud.google.com/bigquery/docs/output-name-mapping#default_database) name to use with any source objects that don't specify one.
- A [default schema](https://docs.cloud.google.com/bigquery/docs/output-name-mapping#default_schema) name to use with any source objects that don't specify one.

### Name parts

You provide the values for the source and target object names in a name mapping rule by using a combination of the following name parts:

- `Database` : A top-level object in the object hierarchy, for example **`database`** `.schema.relation.attribute` . Your source platform might use an alternative term for this, for example *project* .
- `Schema` : A second-level object in the object hierarchy. Your source platform might use an alternative term for this, for example *dataset* .
- `Relation` : A third-level object in the object hierarchy. Your source platform might use an alternative term for this, for example *table* or *view* .
- `Function` : A third-level object in the object hierarchy representing a user-defined function or stored procedure, for example `create procedure db.test.function1(a int)` .
- `Attribute` : A fourth-level object in the object hierarchy. Your source platform might use an alternative term for this, for example *column* .

When configuring name mapping rules in a [configuration YAML file](https://docs.cloud.google.com/bigquery/docs/config-yaml-translation#output_name_mapping) , you only need to include the target name parts that you want to change. Any omitted target name parts remain unchanged.

### Default database

If you want to append a BigQuery project name to all translated objects, the easiest thing to do is to specify a default database name in a [configuration YAML file](https://docs.cloud.google.com/bigquery/docs/config-yaml-translation#specifying_default_database_and_schema_search_path) . This works for source files where three-part naming is used, or where four-part naming is used but the highest level object name isn't specified.

For example, if you specify the default database name `myproject` , then a source statement like `SELECT * FROM database.table` is translated to `SELECT * FROM myproject.database.table` . If you have objects that already use a database name part, like `SELECT * FROM database.schema.table` , then you have to use a name mapping rule to rename `database.schema.table` to `myproject.schema.table` .

### Default schema

If you want to fully qualify all object names in the source files that don't use four-part naming, you can provide both a [default database name](https://docs.cloud.google.com/bigquery/docs/output-name-mapping#default_database) and a default schema name in a [configuration YAML file](https://docs.cloud.google.com/bigquery/docs/config-yaml-translation#specifying_default_database_and_schema_search_path) . The default schema name is provided as the first schema name in the schema search path option.

For example, if you specify the default database name `myproject` and the default schema name `myschema` , then the following source statements:

- `SELECT * FROM database.table`
- `SELECT * FROM table1`

Are translated to:

- `SELECT * FROM myproject.database.table` .
- `SELECT * FROM myproject.myschema.table1`

## Name mapping rule behavior

The following sections describe how name mapping rules behave.

### Rule inheritance flows down the object hierarchy

A name change that affects a higher-level object affects the target object, and also all of its child objects in the same hierarchy.

For example, if you specify the following name mapping rule with an object type of `schema` :

| **Name part** | **Source**  | **Target** |
|---------------|-------------|------------|
| Database      | `sales_db`  | `sales`    |
| Schema        | `cust_mgmt` | `cms`      |
| Relation      |             |            |
| Attribute     |             |            |

When it is applied, the database and schema name parts of all `relation` and `attribute` objects under the `sales_db.cust_mgmt` schema are also changed. For instance, a `relation` object named `sales_db.cust_mgmt.history` becomes `sales.cms.history` .

Conversely, name changes that target lower-level objects don't affect higher- or same-level objects in the object hierarchy.

For example, if you specify the following name mapping rule with an object type of `relation` :

| **Name part** | **Source**  | **Target** |
|---------------|-------------|------------|
| Database      | `sales_db`  | `sales`    |
| Schema        | `cust_mgmt` | `cms`      |
| Relation      | `clients`   | `accounts` |
| Attribute     |             |            |

When it is applied, no other objects at the `sales_db` or `sales_db.cust_mgmt` level of the object hierarchy have their name changed.

### The most specific rule is applied

Only one name mapping rule is applied to an object. If multiple rules could affect a single object, the rule that affects the lowest level name part is applied. For example, if a `database` type name mapping rule and a `schema` type name mapping rule could both affect the name of a `relation` object, the `schema` type name mapping rule is applied.

### Use a unique combination of type and source values

You can't specify more than one name mapping rule with the same type and source values. For example, you can't specify both of the following name mapping rules:

|               | **Rule 1, type `attribute`** | **Rule 2, type `attribute`** |            |            |
|---------------|------------------------------|------------------------------|------------|------------|
| **Name part** | **Source**                   | **Target**                   | **Source** | **Target** |
| Database      | `project`                    |                              | `project`  |            |
| Schema        | `dataset1`                   |                              | `dataset1` |            |
| Relation      | `table1`                     |                              | `table1`   |            |
| Attribute     | `lname`                      | `last_name`                  | `lname`    | `lastname` |

### Name changes don't cascade

Name changes don't cascade across name rules. For example, if you created a name mapping rule that renames `database1` to `project1` , and another that renames `project1` to `project2` , the translator doesn't map `database1` to `project2` .

## Handle source objects that don't have four-part names

Some source systems, like Teradata, use three name parts to fully qualify object names. Many source systems also allow you to use partially qualified names in their SQL dialects, for example using `database1.schema1.table1` , `schema1.table1` , and `table1` to refer to the same object in different contexts. If your source files contain objects that don't use four-part object names, you can use name mapping in combination with specifying a [default database name](https://docs.cloud.google.com/bigquery/docs/output-name-mapping#default_database) and a [default schema name](https://docs.cloud.google.com/bigquery/docs/output-name-mapping#default_schema) to achieve the name mapping that you want.

For examples of using name mapping rules with a default database name or a default schema name, see [Change the database name part for objects with varying levels of name completion](https://docs.cloud.google.com/bigquery/docs/output-name-mapping#partial-database) and [Change a partially qualified relation object name](https://docs.cloud.google.com/bigquery/docs/output-name-mapping#partial-relation) .

## Name mapping examples

Use the examples in this section to see how name mapping rules work for common use cases. For YAML configuration syntax and examples, see [Output name mapping](https://docs.cloud.google.com/bigquery/docs/config-yaml-translation#output_name_mapping) .

### Change the database name part for fully qualified objects

The following example renames the database name part from `td_project` to `bq_project` for all `database` , `schema` , `relation` , and `function` objects that have fully qualified names.

**Source and target name parts**

| **Name part** | **Source**   | **Target**   |
|---------------|--------------|--------------|
| Database      | `td_project` | `bq_project` |
| Schema        |              |              |
| Relation      |              |              |
| Attribute     |              |              |

**Type**

- `database`

**Example input**

- `SELECT * FROM td_project.schema.table;`
- `SELECT * FROM td_project.schema1.table1;`

**Example output**

- `SELECT * FROM bq_project.schema.table;`
- `SELECT * FROM bq_project.schema1.table1`

### Change the database name part for objects with varying levels of name completion

The following example renames database name part `project` to `bq_project` for all object types, and also adds `bq_project` as the database name part for objects that don't specify one.

To do this, you must specify a default database value in addition to specifying name mapping rules. For more information on specifying a default database name, see [Specifying default database and schema search path](https://docs.cloud.google.com/bigquery/docs/config-yaml-translation#specifying_default_database_and_schema_search_path) .

**Default database value**

- `project`

**Source and target name parts**

| **Name part** | **Source** | **Target**   |
|---------------|------------|--------------|
| Database      | `project`  | `bq_project` |
| Schema        |            |              |
| Relation      |            |              |
| Attribute     |            |              |

**Type**

- `database`

**Example input**

- `SELECT * FROM project.schema.table;`
- `SELECT * FROM schema1.table1;`

**Example output**

- `SELECT * FROM bq_project.schema.table;`
- `SELECT * FROM bq_project.schema1.table1`

### Change the database name part and the schema name part for fully qualified objects

The following example changes the database name part `warehouse1` to `myproject` , and also changes the `database1` schema name part to `mydataset` .

You can also change the parts of a `relation` object name in the same manner, by using a `relation` type and specifying source and target values for the relation name part.

**Source and target name parts**

| **Name part** | **Source**   | **Target**  |
|---------------|--------------|-------------|
| Database      | `warehouse1` | `myproject` |
| Schema        | `database1`  | `mydataset` |
| Relation      |              |             |
| Attribute     |              |             |

**Type**

- `schema`

**Example input**

- `SELECT * FROM warehouse1.database1.table1;`
- `SELECT * FROM database2.table2;`

**Example output**

- `SELECT * FROM myproject.mydataset.table1;`
- `SELECT * FROM __DEFAULT_DATABASE__.database2.table2;`

### Change a fully qualified `relation` object name

The following example renames `mydb.myschema.mytable` to `mydb.myschema.table1` .

**Source and target name parts**

| **Name part** | **Source** | **Target** |
|---------------|------------|------------|
| Database      | `mydb`     | `mydb`     |
| Schema        | `myschema` | `myschema` |
| Relation      | `mytable`  | `table1`   |
| Attribute     |            |            |

**Type**

- `relation`

**Example input**

- `CREATE table mydb.myschema.mytable(id int, name varchar(64));`

**Example output**

- `CREATE table mydb.myschema.table1(id integer, name string(64));`

### Change a partially qualified `relation` object name

The following example renames `myschema.mytable` to `mydb.myschema.table1` .

**Default database value**

- `mydb`

**Source and target name parts**

| **Name part** | **Source** | **Target** |
|---------------|------------|------------|
| Database      | `mydb`     | `mydb`     |
| Schema        | `myschema` | `myschema` |
| Relation      | `mytable`  | `table1`   |
| Attribute     |            |            |

**Type**

- `relation`

**Example input**

- `CREATE table myschema.mytable(id int, name varchar(64));`

**Example output**

- `CREATE table mydb.myschema.table1(id integer, name string(64));`

### Change a `function` object name

The following example renames `mydb.myschema.myprocedure` to `mydb.myschema.procedure1` .

**Source and target name parts**

| **Name part** | **Source**    | **Target**   |
|---------------|---------------|--------------|
| Database      | `mydb`        | `mydb`       |
| Schema        | `myschema`    | `myschema`   |
| Function      | `myprocedure` | `procedure1` |
| Attribute     |               |              |

**Type**

- `function`

**Example input**

- `CREATE PROCEDURE mydb.myschema.myprocedure(a int) BEGIN declare i int; SET i = a + 1; END;`
- `CALL mydb.myschema.myprocedure(7)`

**Example output**

- `CREATE PROCEDURE mydb.myschema.procedure1(a int) BEGIN declare i int; SET i = a + 1; END;`
- `CALL mydb.myschema.procedure1(7);`

### Change an `attribute` object name

The following example renames `mydb.myschema.mytable.myfield` to `mydb.myschema.mytable.field1` . Because `attribute` objects are at the lowest level of the object hierarchy, this name mapping does not change the name of any other object.

**Source and target name parts**

| **Name part** | **Source** | **Target** |
|---------------|------------|------------|
| Database      | `mydb`     |            |
| Schema        | `myschema` |            |
| Relation      | `mytable`  |            |
| Attribute     | `myfield`  | `field1`   |

**Type**

- `attribute`

**Example input**

- `CREATE table mydb.myschema.mytable(myfield int, name varchar(64), revenue int);`
- `SELECT myfield, name FROM mydb.myschema.mytable;`

**Example output**

- `CREATE table mydb.myschema.mytable(field1 int, name varchar(64), revenue int);`
- `SELECT field1, name FROM mydb.myschema.mytable;`
