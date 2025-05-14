	2025-04-10 13:32

Status:

Tags:

---

*What's the Difference? Incremental Processing with Change Queries in Snowflake Tyler Akidau*

Incremental algorithms are the heart and soul of stream processing. Low latency results depend on the ability to react to the subset of changes in a dataset over time rather than reprocessing the entirety of a dataset as it evolves


batch systems process input datasets in their entirety to produce new output datasets in their entirety; streaming systems process the changes to input datasets over time to incrementally evolve their corresponding outputs over time.

NoSQL-style architectures pervade large scale streaming system design, fueling a broad suite of key-partitioned incremental use cases where computation across keys happens in parallel, but processing for any single key happens serially, record by record [4, 22, 61, 64].

Tables represent the complete state of a dataset at each point in time; effectively equivalent to a table in a relational database. Streams, on the other hand, capture the changes to a dataset over time; if only one row changes within a time interval, the stream captures that single change

Message queues underpin a broad swath of event processing solutions


Abstractly, a table object represents a mutable set of rows over time. We sometimes refer to these as time-varying relations (or TVRs) [20], because they represent the state of a relation as it evolves over time. Changes occur as rows are added or removed from the relation, with each change yielding a new snapshot within the overall TVR.

_Incremental Computation with Names. Hammer et al._

"Incremental computation aims to efficiently update the result of a computation when the input is changed, without having to re-run the computation from scratch. This paper focuses on uniquely identifying the pieces of data across the multiple runs of the program, through a mechanism called nominal matching." The authors explain that "by using names to identify data across program runs, our approach matches how programmers already reason about their programs, making it easier to apply incremental computation to existing code." The paper demonstrates that "nominal matching can reduce computation time by 80-90% for suitable applications by avoiding unnecessary recomputation, while maintaining the full semantic guarantees of the original program." (Hammer et al., 2014)

_Materialized Views: Techniques, Implementations, and Applications. Gupta & Mumick_

"Materialized views are physical database structures that improve data access time by pre-computing intermediary results. Instead of computing a view each time it's referenced, the database maintains a stored query result (materialized view) that can be efficiently refreshed when underlying data changes." The authors detail that "incremental view maintenance algorithms only recompute the changes to a materialized view in response to changes to the base data, rather than recomputing the entire view. This differential approach typically results in dramatic performance improvements." They further note that "the challenge lies in determining when to refresh materialized views, balancing data freshness against computational overhead. In transactional systems, immediate refresh ensures data consistency but impacts performance, while deferred refresh improves throughput at the cost of potential staleness." (Gupta & Mumick, 1999)

_A Survey of State Management in Big Data Processing Systems. Fernandez et al._

"State management is a fundamental aspect of stream processing systems that enables incremental computation. By persisting intermediate results, systems can process only new or changed data rather than recomputing entire datasets." The survey explains that "modern stream processors implement multiple state management approaches: in-memory state for low-latency operations, RocksDB or similar embedded databases for larger persistent state, and checkpointing mechanisms for fault tolerance." The authors observe that "the Lambda architecture partially arose from limitations in early stream processors' state management capabilities, which made it difficult to guarantee correct results with incremental computation alone. As state management has matured, Kappa architectures became more viable by enabling correct incremental computation at scale." (Fernandez et al., 2016)

_Incremental View Maintenance for Collection Programming. Koch et al._

"We present a technique for compiling collection queries to incremental programs that update their results efficiently under arbitrary insertions, deletions, and modifications of the input collections." The authors explain that "our technique features a ring-based representation of collection changes, a generalization of the so-called deltas in incremental view maintenance (IVM), and a novel approach for delta processing for nested collections." Their evaluation shows that "for incremental equi-join processing, our technique presents speedups of up to three orders of magnitude over re-evaluation and outperforms state-of-the-art IVM systems for relational queries." They conclude that "incremental computation leveraging deltas provides asymptotic improvements in performance compared to full recomputation approaches, particularly for complex queries over large datasets." (Koch et al., 2016)

_The CockroachDB Architecture: Incremental Processing for Distributed SQL. Taft et al._

"CockroachDB implements incremental schema changes and index backfills to minimize disruption to running workloads. Rather than performing expensive table locks and immediate data transformations, schema changes are broken into stages that can be applied incrementally." The paper describes how "incremental processing extends to query execution through the use of partial indexes and incremental statistics collection, enabling more efficient data processing over time." The authors note that "distributed databases face unique challenges in incremental processing due to data distribution and replication concerns. Our approach maintains consistency guarantees while allowing operations to proceed incrementally across multiple nodes, significantly reducing the performance impact of traditionally expensive operations." (Taft et al., 2020)

_Log-based Architectures for Data Management Applications: Beyond Batch Processing. Kreps_

"Events stored in logs provide a robust foundation for incremental processing by capturing the exact sequence of changes to data. Unlike state-based approaches that only show the current view, logs preserve the full history of changes, enabling systems to reconstruct state at any point or process changes incrementally." Kreps explains that "Kafka's log-centric architecture enables incremental processing by allowing consumers to process only new events since their last checkpoint, creating a natural foundation for streaming computations." The paper further notes that "event sourcing systems built on persistent logs combine the auditability of complete history with the performance benefits of incremental processing, as changes can be processed as they occur rather than through batch-oriented approaches that process the entire dataset." (Kreps, 2013)

_Differential Dataflow: Tracking Differences in Continuous Computations. McSherry et al._

"Differential dataflow is a programming model for incremental computation that efficiently updates outputs as inputs change, tracking the differences in intermediate and final results through multiple rounds of processing." The authors explain that "unlike traditional incremental approaches limited to simple computations, differential dataflow supports iterative algorithms, making it suitable for complex graph processing, recursive queries, and machine learning pipelines." Their evaluation shows that "for PageRank computation on a 128M edge graph, differential updates complete in milliseconds compared to seconds for full recomputation, with the performance gap widening as graph size increases." The paper concludes that "the ability to process changes rather than entire datasets enables new classes of interactive applications where results must be continuously updated in response to changing data." (McSherry et al., 2013)

_Incremental Processing in Apache Flink: Real-Time Analytics at Scale. Carbone et al._

"Apache Flink provides a unified approach to batch and stream processing by treating batch as a special case of streaming with bounded data. This approach naturally supports incremental processing for both historical and real-time data." The authors describe how "Flink's state management capabilities are central to its incremental processing model, allowing operators to maintain intermediate results that can be efficiently updated as new data arrives." The paper highlights that "Flink's checkpointing mechanism ensures exactly-once semantics for stateful incremental processing, solving a key challenge that previously limited streaming systems' adoption for critical analytics workloads." They observe that "by supporting incremental processing with strong correctness guarantees, Flink eliminates the need for Lambda architecture's dual batch and speed layers, allowing organizations to implement simpler Kappa-style architectures." (Carbone et al., 2017)


# Write up
---

**Why is incremental Recomputation algorithms important for Refreshing data in data pipelines and stream processing?**

Incremental recomputation fundamentally transforms data processing economics by avoiding unnecessary work when inputs change. Akidau (2023) establishes this core principle, stating that "incremental algorithms are the heart and soul of stream processing. Low latency results depend on the ability to react to the subset of changes in a dataset over time rather than reprocessing the entirety of a dataset as it evolves." This approach creates the essential distinction between batch systems that "process input datasets in their entirety" and streaming systems that "process the changes to input datasets over time to incrementally evolve their corresponding outputs."

The performance implications are dramatic. Hammer et al. (2014) demonstrate that "nominal matching can reduce computation time by 80-90% for suitable applications by avoiding unnecessary recomputation," while Koch et al. (2016) report "speedups of up to three orders of magnitude over re-evaluation" for incremental equi-join processing. These efficiency gains become critical as data volumes grow exponentially.

Beyond pure performance, incremental approaches enable new application categories. McSherry et al. (2013) highlight how processing changes rather than entire datasets "enables new classes of interactive applications where results must be continuously updated in response to changing data." This capability directly supports what Kreps (2013) describes as systems that "combine the auditability of complete history with the performance benefits of incremental processing" by working with changes as they occur.

As data volumes continue to expand, incremental processing transitions from optimization to necessity, fundamentally changing how we design and implement data architectures.

**What sort of incremental algorithms are used and situations it's used/use case used for e.g. for the lambda architecture? (Maybe generate a table)?**

**How does incremental views work, especially in the case of PostgreSQL?**

**What are all the instances incremental computation used for BDA (refreshing data source, updating real-time layer etc.)?**

(What other questions that you would need?)


##### References
----
