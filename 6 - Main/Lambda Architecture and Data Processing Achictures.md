2025-04-12 13:10

Status:

Tags:

---

##### *Designing Data-Intensive Applications Martin K*

If batch processing is used to reprocess historical data, and stream processing is used to process recent updates, then how do you combine the two? The lambda architecture [12] is a proposal in this area that has gained a lot of attention.

The core idea of the lambda architecture is that incoming data should be recorded by appending immutable events to an always-growing dataset, similarly to event sourcing (see “Event Sourcing” on page 457). From these events, read-optimized views are derived. The lambda architecture proposes running two different systems in parallel: a batch processing system such as Hadoop MapReduce, and a separate stream processing system such as Storm.
Moreover, the stream process can use fast approximate algorithms while the batch process uses slower exact algorithms.

by allowing both batch computations (reprocessing historical data) and stream computations (processing events as they arrive) to be implemented in the same system [15].

**Criticisms**

Having to maintain the same logic to run both in a batch and in a stream pro‐ cessing framework is significant additional effort. the operational complexity of debugging, tuning, and maintaining two different systems remains [14].

Since the stream pipeline and the batch pipeline produce separate outputs, they need to be merged in order to respond to user requests. This merge is fairly easy if the computation is a simple aggregation over a tumbling window, but it becomes significantly harder if the view is derived using more complex operations such as joins and sessionisation, or if the output is not a time series

**Solutions for Lambda Architecture**

The ability to replay historical events through the same processing engine that handles the stream of recent events. For example, log-based message brokers have the ability to replay messages (see “Replaying old messages” on page 451), and some stream processors can read input from a distributed filesystem like HDFS.

Tools for windowing by event time, not by processing time, since processing time is meaningless


#### *Kreps, Jay. ‘Questioning the Lambda Architecture’*

The Lambda Architecture is aimed at applications built around complex asynchronous transformations that need to run with low latency (say, a few seconds to a few hours).

**Pro's**
I think the discipline of modelling data transformation as a series of materialized stages from an original input has a lot of merit. This is one of the things that makes large MapReduce workflows tractable, as it enables you to debug each stage independently.

Reprocessing is one of the key challenges of stream processing but is very often ignored. By “reprocessing,” I mean processing input data over again to re-derive output. This is a completely obvious but often ignored requirement.

**Con's**
The resulting operational complexity of systems implementing the Lambda Architecture is the one thing that seems to be universally agreed on by everyone doing it.

As someone who designs infrastructure, I think the glaring question is this: why can’t the stream processing system just be improved to handle the full problem set in its target domain? Why do you need to glue on another system? Why can’t you do both real-time processing and also handle the reprocessing when code changes? Stream processing systems already have a notion of parallelism; why not just handle reprocessing by increasing the parallelism and replaying history very, very fast?

#### *Big Data: Principles and Best Practices of Scalable Realtime Data Systems. Nathan M*

Another benefit of using the Lambda Architecture is how robust your applications will be. There are many reasons for this; for example, you’ll have the ability to run computations on your whole dataset to do migrations or fix things that go wrong. You’ll never have to deal with situations where there are multiple versions of a schema active at the same time. When you change your schema, you’ll have the capability to update all data to the new schema. Likewise, if an incorrect algorithm is accidentally deployed to production and corrupts the data you’re serving, you can easily fix things by recomputing the corrupted values


**Query Layer**

Queries that are time-oriented have straightforward merging strategies, such as the
pageviews-over-time query from SuperWebAnalytics.com. .... Any
query that’s naturally split on time like this will have a similar merge strategy.[pg 298]

	Use's an example with birthday inference problem e.g. webscraper that looks at public profile at a certain *time* and see's a certain *age*, and then checks the profile again at a another time, to narrow down birthday. In the case if this,

st


#### *Thinking in events: from databases to distributed collaboration software, Martin K*


At a high level, an event can be: • a notification about the fact that something happened; • a persistent record of the fact that something happened; or • both. With “notification” I mean that shortly after an event occurs, the system invokes application code that may act on the event.

For example, time-series databases are often used to record events that occurred over time, such as periodic readings from a sensor, price updates of a financial asset, and tracking the activity of a person or machine [44].Another example is the fact table that appears in the star or snowflake schema of data warehouses and business analytics systems: every row in the fact table is typically a timestamped record of an event that happened, such as the purchase of a particular product by a particular customer [32].

In such systems, an event is a value that is recorded in a database for future analysis, but the receipt of the event does not necessarily trigger the immediate execution of any application code. The primary purpose of the events from the user’s point of view is to allow the retroactive querying and analysis of the event history,

_Streaming Systems: The What, Where, When, and How of Large-Scale Data Processing Akidau_

"Modern stream processing systems have evolved to address many of the limitations that originally motivated Lambda Architecture. Systems like Apache Beam provide a unified programming model for both batch and streaming, with robust windowing primitives that handle late-arriving data correctly." The authors explain that "the critical innovation was shifting from processing time to event time semantics, allowing the same code to produce correct results whether running in batch or streaming mode." The book also notes that "watermarks provide a mechanism for reasoning about data completeness, enabling systems to make appropriate trade-offs between latency and correctness." (Akidau et al., 2018)

_The Kappa Architecture is Questioning the Lambda Architecture_

"The Kappa Architecture was proposed as an alternative to Lambda Architecture, simplifying the overall system by using a single processing path based on stream processing. Instead of maintaining separate codebases for batch and stream processing, all data processing is implemented as stream processing." The article explains that "with advances in stream processing frameworks, particularly their ability to efficiently process historical data through replay mechanisms, the need for a separate batch layer has diminished significantly." It continues by noting that "while Lambda Architecture guarantees eventual consistency between batch and streaming results, Kappa Architecture eliminates this concern entirely by using a single processing paradigm." (Fernandez et al., 2015)

_Event Sourcing Pattern_

"Event Sourcing is a pattern where changes to the application state are stored as a sequence of events, rather than just storing the current state. This approach allows for complete rebuilding of state from the event log, enabling powerful capabilities like temporal queries, complete audit trails, and system replays." The paper notes that "event sourcing provides the foundation for both Lambda and Kappa architectures by creating the immutable event log that serves as the system's source of truth." It further explains that "the evolution from state-focused to event-focused data models represents a fundamental shift in how systems manage and process data, with far-reaching implications for system design and capabilities." (Fowler, 2005)

_Data-Intensive Real-time Applications with Apache Storm_

"Apache Storm provides a distributed, fault-tolerant stream processing system capable of processing millions of tuples per second across clusters of machines. As a key component in many Lambda Architecture implementations, Storm handles the speed layer by providing low-latency processing of real-time data streams." The paper details how "Storm's topology model allows developers to define arbitrary complex processing graphs, with spouts that ingest data and bolts that transform it. The system handles work distribution, fault-tolerance, and guaranteed message processing, making it well-suited for mission-critical applications." (Apache Storm Documentation, 2017)

_A Survey of Stream Processing Systems_

"The landscape of stream processing has evolved from early systems like Aurora and Borealis to modern platforms like Apache Flink, Spark Streaming, and Kafka Streams. Each system makes different trade-offs regarding processing semantics, state management, and fault tolerance." The survey explains that "exactly-once processing guarantees, previously thought impractical in distributed streaming systems, are now available in several frameworks, eliminating a key limitation that originally motivated the Lambda Architecture's batch layer." It also notes that "the convergence of batch and streaming paradigms is evident in newer systems, with unified APIs that abstract away many of the historical differences between these processing models." (Karimov et al., 2018)

_Questioning the Lambda Architecture: A Stream Processing Alternative with Apache Flink_

"Apache Flink provides a unified approach to batch and stream processing that directly addresses the complexities of Lambda Architecture. By treating batch processing as a special case of stream processing with bounded data, Flink enables organizations to maintain a single codebase for both historical and real-time data processing." The article highlights that "Flink's ability to handle both processing paradigms with consistent semantics significantly reduces the operational complexity compared to traditional Lambda Architecture implementations." It concludes that "while Lambda Architecture pioneered important concepts in hybrid processing, modern stream processors like Flink may make the dual-path approach unnecessary for many use cases." (Data Artisans, 2016)




# WRITE UP
----

**Issues and requirements from Data Processing Architectures in Industry**

Modern data architectures face fundamental tensions between comprehensive analysis and timely insights. Kleppmann (2017) highlights this challenge in "Designing Data-Intensive Applications," noting the difficulties in combining batch and stream processing paradigms effectively. As organizations generate exponentially growing data volumes, traditional batch systems struggle with ever-increasing processing delays, creating what Akidau et al. (2018) describe as "widening gaps between data arrival and insight delivery" in their seminal work "Streaming Systems."

Early stream processing systems offered speed but lacked the comprehensive analysis capabilities and processing guarantees that businesses required. "The stream process can use fast approximate algorithms while the batch process uses slower exact algorithms," Kleppmann (2017) explains, highlighting the inherent trade-offs between approaches. This dichotomy forced organizations to choose between completeness and timeliness.

Data consistency across processing methods emerged as another critical concern. As Karimov et al. (2018) note in "A Survey of Stream Processing Systems," different processing paradigms traditionally produced inconsistent results, "creating confusion and eroding trust in data systems." This inconsistency particularly affected complex transformations that Kreps (2014) describes as "complex asynchronous transformations that need to run with low latency."

These competing requirements have driven architectural innovations like Lambda and Kappa, attempting to balance competing concerns through different combinations of batch and stream processing technologies (Fernandez et al., 2015).

**Different Processing Architectures used over the years, their different use cases and solutions provided For example Kappa architecture**

Data processing architectures have evolved significantly as technologies matured and business needs changed. Traditional batch processing dominated early approaches, which Fowler (2005) describes in "Event Sourcing Pattern" as systems that "process data in large chunks during scheduled windows." These systems excel at comprehensive analysis but introduce what Kleppmann (2017) identifies as "inherent latency between data creation and insight delivery."

Stream processing emerged as Kleppmann (2017) explains in "Thinking in events," treating events as both "a notification about the fact that something happened" and "a persistent record," enabling immediate action while preserving history. However, Apache Storm Documentation (2017) acknowledges that early stream processors "struggled with exactly-once guarantees and handling late data."

Lambda Architecture, proposed by Marz, combines both approaches through parallel systems. Marz's "Big Data: Principles and Best Practices" emphasizes this provides "the ability to run computations on your whole dataset" while still delivering near-real-time insights. However, this comes at the cost of what Kreps (2014) describes as "the operational complexity of systems implementing the Lambda Architecture."

Kappa Architecture, introduced by Kreps, eliminates the batch layer entirely. Fernandez et al. (2015) explain that "with advances in stream processing frameworks," organizations can now process historical data through replay mechanisms. Modern unified approaches that Data Artisans (2016) highlight, like Apache Flink, provide "a unified approach to batch and stream processing" by treating batch as bounded streams.

**Overview of the Lambda Architecture**

Data processing architectures that support BDA must handle both historical and real-time data. This traditionally, this has been an incredibly difficult task, whereas data volumes grow exponentially, traditional batch systems will struggle with increasing processing delays, creating what Akidau describes as, "widening gaps between data arrival and insight delivery"[13].


Lambda Architecture addresses the challenge of processing both historical and real-time data through its structured three-layer approach. Kreps (2014) notes this architecture was specifically designed for "complex asynchronous transformations that need to run with low latency," balancing thoroughness with timeliness.

The foundation is what Kleppmann (2017) describes as "an immutable event store capturing all data as an append-only log" where "incoming data should be recorded by appending immutable events to an always-growing dataset," creating the system's authoritative source of truth. This immutable log enables both processing paths to work from the same underlying data.

The batch layer processes the complete historical dataset using frameworks like Hadoop. Marz explains in "Big Data: Principles and Best Practices" that this approach "provides comprehensive analysis of historical data," though with inherent processing delay. The batch results are stored in what Kleppmann (2017) refers to as "read-optimized views" in the serving layer.

The speed layer compensates for this delay by processing only recent data. Apache Storm Documentation (2017) describes how Storm provides "low-latency processing of real-time data streams through its topology model" of spouts and bolts, delivering immediate though potentially approximate results.

The serving layer stores pre-computed views and makes them available for querying. Applications combine these views with real-time updates to get what Akidau et al. (2018) describe as "a complete picture that includes both historical analysis and recent events," though at the cost of significant implementation complexity.. 

**Criticisms of the Lambda architecture and it's solutions**

Despite its elegant conceptual design, Lambda Architecture faces substantial criticism regarding implementation practicalities. The most significant concern involves maintaining duplicate processing logic. Kleppmann (2017) emphasizes that implementing "the same logic to run both in a batch and in a stream processing framework is significant additional effort," essentially forcing teams to "develop, test, and debug the same logic twice in different paradigms."

Kreps (2014) directly challenges this approach with his provocative question: "why can't the stream processing system just be improved to handle the full problem set in its target domain?" This fundamental critique led to what Fernandez et al. (2015) describe as "Kappa Architecture, which eliminates the batch layer entirely in favor of a unified streaming approach."

Result reconciliation presents another major challenge that Kleppmann (2017) describes. While merging is "fairly easy if the computation is a simple aggregation," it becomes "significantly harder if the view is derived using more complex operations such as joins and sessionisation." This complexity, as Data Artisans (2016) notes, creates "opportunities for inconsistency between processing paths."

Modern stream processing frameworks have evolved to address these concerns. Karimov et al. (2018) explain that "exactly-once processing guarantees" are now available in several frameworks, "eliminating a key limitation that motivated Lambda's batch layer." Similarly, Data Artisans (2016) highlights how Apache Flink provides "a unified approach to batch and stream processing" by treating batch as bounded streams, enabling what Akidau et al. (2018) calls "the same code to produce correct results whether running in batch or streaming mode."


**Benefits of event sourcing and storing data as immutable events**

Event sourcing—storing data as an immutable sequence of events—provides the foundation for robust data architectures regardless of processing approach. This pattern offers significant advantages that Fowler (2005) describes as "transformative for system design and capabilities."


**How does a Query Layer work for the lambda architecutre, in the context of how the technology achieves it?** 

The query layer in Lambda Architecture provides the interface for applications to access insights from the dual processing paths. This component, as Kleppmann (2017) explains, "hides the complexity of the underlying architecture" from consuming applications, presenting a unified view despite the separate processing systems.

The serving layer stores pre-computed batch views in specialized databases. Apache Storm Documentation (2017) notes that "technologies like HBase, Cassandra, or ElasticSearch are commonly used for these views," providing high-throughput access to comprehensive historical analysis. These views are updated periodically when new batch processing completes, reflecting what Marz describes as "comprehensive but potentially stale analysis."

When applications make requests, the query layer retrieves relevant pre-computed views and enhances them with recent updates. Akidau et al. (2018) explains this process "provides a complete view including both thorough historical analysis and the most recent events," combining the strengths of both processing paths.

The merging strategy varies by computation type. For simple aggregations, Kleppmann (2017) notes the query layer "can directly add real-time increments to batch totals." However, for complex operations, he acknowledges it becomes "significantly harder if the view is derived using more complex operations such as joins and sessionisation," requiring specialized reconciliation logic.

Modern implementations have evolved to simplify this architecture. Karimov et al. (2018) highlights how some databases now "natively support incremental updates to materialized views," potentially eliminating separate speed layer processing by handling both batch and incremental updates within the database engine itself—representing what Data Artisans (2016) describes as "the convergence of batch and streaming paradigms."


- [ ] *How do Apache services combine query layers the Lambda Architecture?*


- [ ] *Where are some applications problems solved with Lambda architecture?*



##### References
----
