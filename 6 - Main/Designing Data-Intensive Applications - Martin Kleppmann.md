2025-01-16 14:45

Status: #baby

Tags:[[Reading For Big Data]]

---
*6*
3 Key factors for an effective data dependent web application are:
- Reliability: Working to high degree even in adversity, hardware, software or even human error.
- Scalability: System should handle grows in data volume, traffic volume, complexity, it should be able to handle that
- Maintainability: Should be able to added on to effectively without issue (unnecessary for us)

Main principles of reliability:
- Faults are components of a system that fall out of spec with failures being total failure to meet demand for user. Ideally should minimise the chance of a fault causing failure, even more then stopping faults themselves.
- We can use testing to intentionally increase faults to see if the system can handle that without failure.
- Need to be able to safety handle faults and errors with causing failure
- If a component relies on some guarantee for it to function, it can constantly check itself and raise an error for any issues found.
- When handling human error, minimise inputs as much as possible whilst still providing desired functionality. Have unit tests and system wide integration tests. Allow quick, easy recovery from human errors like rolling back, stopping ongoing processes, Version control and git for pushing small amounts of code

Scalability:

First requires actual measurement values that will be used e.g. queries per second, data per request, failure's per hour, read/writes to database per second. After getting the measurement, we can track load across times and system usage to get an indicator of performance.

Percentiles are more commonly used then mean with technology companies holding themselves to a high stand of wanting results in the 99 percentile, so even if request times on average or great, if the 99th percentile are waiting 4 seconds, so 1 in 100 are waiting for 4 seconds, that give's us a standard of we handle at worst.

Measurements of performance should be tracked done both on client side and server side.


*90 (117)*
Difference between OLAP (Online Analytical Processing) and OLTP (Online Transaction Processing) is that OLTP is the raw transaction data in high volumes with OLAP being the grouping and aggregation of this data for analysis. So multiple OLTPs for an OLAP.
Data warehouses which are the type of databases OLAP's are stored are designed specifically for, are designed for analysed as much as the hearts content for read only analytical data. OLAP give's archive and live data, use bulk imports via ETL or streaming events, and manage large amounts of data.

Advantages being, not needing to query live used OLTP databases that are more critical and in use, and have a separate non-critical designed for analytics, database just for business analysts.

Typically stored via the "**star schema**" where you have 1 central "**facts**" table e.g. "**facts_sale**" that contains as much information for given events as needed e.g. time of event, what it is, transaction number etc. 
![[Pasted image 20250301122716.webp]]

Can have 100s of columns. The "star" comes from also having "**dimension**" tables like "**dim_product_table**" that contains the list of some value e.g. list of types of products, and passes the foreign key of that product to the facts table. So more information can be got from the dimension tables. So visually looks like a star. "**Snowflake schema**" is similar but breaks it down even further by having sub dimensions and referencing them in the dimension tables with FK.  More normalised, but less common due to being harder to query.

Typically Data warehouses have 4-5 facts table at time with trillions of rows and petabytes of data. 

*101 (123) Data Warehouses and Materialised Views*
Can be column oriented which is a lot more efficient for querying and works better for event column compression, but traditional row oriented processes can also be used.
For read-heavy row oriented data warehouses, it can be efficient to use data warehouses **materialised views** that store the results of queries on disk for faster read access. Helpful when lot's of queries use aggregate functions aggregate functions (COUNT, SUM, AVG, MIN, or MAX in SQL).

You can also use **data cubes**, grids of aggregates grouped by different dimensions. Makes certain queries very fast since they have efficetively been pre-computed, but very inflexible for specific data.
![[Pasted image 20250120142331.webp]]

*Most data warehouses therefore try to keep as much raw data as possible, and use aggregates such as data cubes only as a performance boost for certain queries - 103 (125)* 

*389(411) Different Types of Systems*

Book argues there are 3 different types of system:

- **Services (online Systems):** When a service receives a request or query, the server tries to respond to that request correctly as soon as possible
- **Batch Processing Systems (offline Systems):** Usually automatic jobs that a few minutes to days to handle large amounts of input data to produce some result.
- **Stream Processing Systems:** Inputs and produces outputs at timely intervals but operates on events as soon as they happen allowing for low latency.

*439(461) Speed Layer*

Essentially like batch processing, so using some input of data to produce some result, but they typically worked on large fixed and known sized data, which may not be ideal. You may want data hourly for however many came in during that time or even better, handling each **record/event** as they come in. Hence the **Stream Processing**

**Streams** refers to data made incrementally available over time. Typically related groups of data are grouped in to Topics or a stream. Producers produce these events and push events to consumers subscribed to this topic. 

**Message brokers** (message queue) are used as an intermediary message database, optimised for handling message streams, as opposed directly sending messages from producer to consumer. Producers and Consumers join as clients, and the broker redirects messages to where they need to go, message brokers typically delete the data once sent to consumer. So, **acknowledging** a message is inherently destructive

To avoid this destructiveness, and make consumers and their readings more independent, we can use logs, append only sequence of records on disks, so messages are appended to logs, and consumers reads log sequentially until reaches the end and is notified their is a new record added. These logs can be partitioned and shared across multiple machines, with a topic being group of logs carrying messages of the same type. Since logs aren't deleted, and are essentially just read only files, they can be stored indefinitely and loaded in again later to query historical data 

*452(*474) Database and streams and keeping in sync*

Since data in a non-trivial application can appear multiple times in multiple locations, and in the case of data warehouses, full refresh takes too long, we can use "*dual write*" or writing to each system concurrently when data changes. This causes some issues with race conditions or if a thread fails, causing data to be inconsistent

Similar to **logs** like systems used in stream processing (e.g. Apache Kafka), we can use databases' **replication logs** (logs of all changes made to a database, which we can use to replicate an entire database). Technically you could just store these logs without the database, and end up with a log-based file system which is how streaming platforms work anyhow.

So, not only can we uses logs and the order they appear in to effectively synchronise every subsystem, but also, get live data by reading these logs in accordance to an offset of the previous batch process. Most database have replication logs and **CDC (Change Data Capture) tools** in order to do this but for files since they don't have logs, it can be a bit harder:

| **Data Source**                              | **Native Change Tracking?**                 | **Can Track Appended Data?** | **Common Techniques**                   |
| -------------------------------------------- | ------------------------------------------- | ---------------------------- | --------------------------------------- |
| **Databases (SQL, NoSQL)**                   | ✅ Replication Logs (CDC, WAL, Binlog, etc.) | ✅ Yes                        | CDC, Binlogs, WAL, Triggers             |
| **CSV / Text Files**                         | ❌ No built-in tracking                      | ⚠️ Only if appending         | File size checks, Line offsets, Hashing |
| **Excel Files (XLSX, CSV)**                  | ❌ No built-in tracking                      | ⚠️ Appending possible        | Versioning, Metadata timestamps         |
| **XML / JSON Files**                         | ❌ No built-in tracking                      | ⚠️ Appending possible        | Diffing, Last Modified Time             |
| **Parquet / Avro** (Big Data Formats)        | ✅ Some support for metadata                 | ✅ Yes                        | Partitioning, Append-Only Logs          |
| **Message Queues (Kafka, Pulsar, RabbitMQ)** | ✅ Built-in offset tracking                  | ✅ Yes                        | Kafka Offsets, Consumer State           |
|                                              |                                             |                              |                                         |

*497(519) Lambda Architecture, Pro's, Con's and benefits*

Books describes the lambda architecture as a popular way to manage batch processing for fixed historical data as the **Batch Layer** and unbounded event based real-time data handling known as the **Speed Layer** that would approximately add it's results to final views generated by the batch layer in order to give a semi-accurate depiction of real-time data.

The batch layer would be the more secure, simple and reliable, with the speed layer being almost an addition on top of it, to make their view's more accurate.

Con's:
- **2 Separate layers** that have to be maintained and despite being almost identical, subtle differences and nuances has to be considered with handling a log based storage system against typical data system approach. Debugging becomes exceptionally harder and changes must be made on both layers. Need's some sort of abstraction to work for both systems
- **Incremental Batch Refresh**: Full refresh of batch layer every hour or so would take too long and be too demanding, so incremental refreshes are done instead which increases the chance of faults, typically requiring a secure refresh eventually when there's less demand. Regardless, batch layer becomes more complicated
- **Combining Layers**: Combing the speed layer with the views made by the batch layer can be quite difficult when it's more then just handling counts, other types of aggregates and joins
- **Speed Layer Out of Order**: Because the Speed layer does not guarantee being in order or preventing duplicates (if a late event is a duplicate, but it's previous value wasn't remembered since it was hours ago, you now have accepted a duplicate) 

Solutions:
- Using the same processing engine, so just use a log based system for storing all data, and then for historical data, just loading historical logs. So the same process of querying recent data against.
- 
- Using **event time** instead of **process time** so using the time these events actually occurred and ignoring how they are processed time.  
##### References
----
[Designing Data intensive Applications](file:///C:/Users/Asus/Downloads/Designing%20Data-Intensive%20Applications%20The%20Big%20Ideas%20Behind%20Reliable,%20Scalable,%20and%20Maintainable%20Systems%20(%20PDFDrive%20).pdf)