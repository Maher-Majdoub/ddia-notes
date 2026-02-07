# Chapter 2: Data Models and Query Languages

There are many types of data models; each one is built based on assumptions about how it will be used. Some usages are easy and others are not possible. Some operations are fast while others perform badly, so it’s important to choose the model that is appropriate for our application.

1. **Reltional Model**  

The relational model is well known nowadays (thanks to SQL), where data is organized into relations (tables in SQL). Each relation is an unordered collection of tuples (rows in SQL).

The data is represented in a simple structure (no nested or tree-like structure), so there are no complicated access paths to follow to retrieve the desired data. It also features a query optimizer that decides which part of the query will be executed first to achieve optimal runtime, and this is handled automatically by the database.

#### The Object-Relational Mismatch 

Most programming languages are object-oriented, so there is a mismatch between the structure of data used in application code and the structure of data stored in a relational data model. Object-Relational Mapping (ORM) tools reduce the amount of code needed to translate between these two representations.


2. **Document Model**

Document databases reverted back to the hierarchical model, so things like one-to-many relationships are stored as nested records inside the parent record. They are good for schema flexibility, better throughput, and are usually closer to the application’s data structures.

In some cases, certain values are used in many different places in the database. For example, schools where users studied: many users can study at the same school. For normalization purposes, we should store schools in one place so users can reference them. This is straightforward in the relational model, but document models do not support joins. To achieve this, we must handle it in application code, which adds more complexity.

It is also usually hard to represent many-to-many relationships with JSON-like data models.

#### Data locality 

A document is stored as a continuous string, encoded as JSON (or XML, etc.). If the application needs to access the entire document, this has a performance advantage. However, when modifying a single attribute, the whole document must be loaded. For this reason, it’s usually better to keep document sizes fairly small.

-> Relational databases enforce schema-on-write, while document stores often use schema-on-read, shifting validation to application code.

3. Graph like Data Models

If an application has a lot of complex many-to-many relationships, this model is a beast. A graph consists of vertices connected by edges, and it’s not limited to homogeneous data — it can store different types of objects in a single data store.

Graphs are great for flexible data modeling and evolvability, since we can add new features without modifying the overall graph representation.

#### Cypher Query Language
Cypher is a declarative query language for property graphs, created for the Neo4j graph database.

#### Graph Queries in SQL
It’s possible to query graph-like data stored in SQL tables, but it’s complex and inconvenient compared to graph query languages. For example, in Cypher we can write WITHIN *0.. to follow edges zero or more times. In SQL, achieving the same logic requires recursive common table expressions (CTEs), which are harder to write and reason about.

## Query Languages for data

We have two types of languages:

- Imperative:

Most programming languages are imperative. To achieve the desired output, we must implement an algorithm that tells the computer which operations to run and in what order.

- Declarative: 

In declarative languages, we specify the pattern of data we want as output and apply conditions, without describing how to execute the query. It’s up to the query optimizer to decide the execution order (examples: SQL, CSS).

Declarative languages are easier to work with because they hide implementation details, and parts of the query can be executed in parallel. Imperative languages are usually harder to parallelize across multiple cores or machines.

#### Map-Reduce Querying 
MapReduce is a programming model for processing huge volumes of data in bulk across many machines. It is neither a fully declarative query language nor a fully imperative API — it sits somewhere in between.

Query logic is expressed using snippets of code that are repeatedly called by the processing framework:
- **Map** -> Collect
- **Reduce** -> Aggregate

The map and reduce functions are restricted: they cannot run additional queries and must not have side effects. This makes them easy to rerun on failure and allows execution in any order.

They are powerful because they can express complex logic on large datasets. These features are not unique to MapReduce; some SQL databases can also be extended with programming languages.


