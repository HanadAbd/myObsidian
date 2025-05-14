2025-04-10 13:48

Status:

Tags:

---
*What's the Difference? Incremental Processing with Change Queries in Snowflake Tyler Akidau*

In the 2010s, a multitude of open-source stream processing frameworks emerged and made stream processing accessible to a wider audience. Prominent representatives are Storm [60], Spark Streaming [64], Flink [22], Samza [50], Beam [21], and Kafka Streams [61], all projects governed by the Apache Software Foundation

Many of these projects later added declarative APIs to define stream processing logic. Spark introduced Structured Streaming [19] which is built on top of Spark SQL.Confluent published KSQL [37], a wrapper around Kafka Streams that enables users to express logic in a SQL dialect.

Storm, Flink, Samza, and Beam added SQL parsers and compilers based on Calcite [21] to translate queries written in their SQL dialects into data flows [8, 9, 15, 16].

Members of some of these communities published an approach to define SQL queries over streaming and static data with common semantics [20]

These frameworks largely preferred low-latency and scale over ease-of-use and efficiency

Many DBMSs support temporal tables as standardized in SQL:2011 [39], including Oracle Database [52], Microsoft SQL Server [47], IBM DB2 [35], SAP HANA [54], and MariaDB [40].

Today, structured data is often stored in immutable files on cloud storage using table formats such as Delta Lake, Apache Iceberg, and Apache Hudi.


*Using Data Analytics to Derive Business Intelligence: A Case Study Ugochukwu Orji*


*Making Sense of Big Data in Intelligent Transportation Systems: Current Trends, Challenges and Future Directions Mian Ahmad Jan, *

Various AI-enabled approaches, such as ML, DL, and natural language processing, are utilized for analysis to identify patterns that predict future insights [15].

*A Comprehensive Survey on Big Data Analytics: Characteristics, Tools and Techniques Mohammed*

Goes over the different Apache tools, models and frameworks used to define big data tools.

— Hadoop: Hadoop is an open-source big data framework for distributed storage and batch processing, primarily using HDFS and MapReduce [6, 168]. — Apache Spark: Spark is a fast, flexible in-memory data processing engine designed for largescale analytics [151]. — Apache Kafka: Kafka is a distributed platform for real-time data ingestion and streaming, commonly used with Flink and Storm for real-time data processing [91]. — Storm: Storm is a fault-tolerant, real-time processing system often paired with Kafka and Cassandra for fast diagnostic analytics [50]. — Flink: Flink is a powerful tool for efficient streaming and batch data processing, optimized for network and storage efficiency [117]. — Hive and Pig: Hive and Pig are data processing frameworks built for Hadoop. Hive is used for SQL-based querying of large datasets, while Pig is used for data transformation and processing [15, 156]. — Mahout: Mahout is an open-source tool for scalable ML, offering algorithms for clustering, classification, and regression using Hadoop [50]. — Presto: Presto is a high-performance distributed SQL query engine, suitable for ad-hoc queries, but lacks built-in security or transaction features [163].


*dbt*

dbt is a transformation workflow that helps you get more work done while producing higher quality results. You can use dbt to modularize and centralize your analytics code, while also providing your data team with guardrails typically found in software engineering workflows. Collaborate on data models, version them, and test and document your queries before safely deploying them to production, with monitoring and visibility.

- Avoid writing boilerplate DML and DDL by managing transactions, dropping tables, and managing schema changes. Write business logic with just a SQL `select` statement, or a Python DataFrame, that returns the dataset you need, and dbt takes care of materialization.


# WRITE UP
----

- [ ] *What are the differences between the Apache tools and how they work?*

Due to big data processing, and the requirements necessary in order to succesffuly implement it, various tools, algorithms and designed patterns have emergeregd. Beyond the stream processing and batch processing apache frameworks such as Apache Hadoop
for distributed storage with HDFS, Apache kafka with it's real-time data ingestion, or flink with it's powefull tools, there exists various implementaiotns and advances.
*A Comprehensive Survey on Big Data Analytics: Characteristics, Tools and Techniques Mohammed*  Many of these tools, don't natively use SQL but various extensions such as KSQL wrapper over Kafka streams, or SQL parsers that exist on Apache storm and flink, allow for translation of SQL into interactions and design of their data flows. *What's the Difference? Incremental Processing with Change Queries in Snowflake Tyler Akidau*




- [ ] *Where are the different tools used for report visualization? (Grafana, Power BI, Tableau?)*




- [ ] What is defined/done in analytic stages/ what is done?

- [ ] *What does confluence, Amazon Redshift, S3, Big Query, etc. relate to data processing?*

dbt is a tool that helps with data transformation work flows, by allowing to build data models or simply SQL or python data frames that are converted into stable, materialized tables and configurations on the data ware house,. Not only helping to reduce boiler plate, and testing, helping to reduce debugging, via managing data models and there dependecies for you, even to texte extent of having incremental models built in. *dbt*

Modern data storage has evolved dramatically with cloud technologies reshaping implementation approaches. Cloud data warehouses like Snowflake, Amazon Redshift, Google BigQuery, and Azure Synapse Analytics have become predominant, offering scalable resources without physical infrastructure management. These platforms separate storage from compute, allowing independent scaling of each component.


- [ ] *What are the different types of data processes? Both real-time, server-side etc.?*




##### References
----
