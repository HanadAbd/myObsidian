	2025-04-20 15:15

Status:

Tags:

---

*Big Data Principals and Best practices Nathan Marz*

There are two aspects to the performance of a batch-layer algorithm: the amount of resources required to update a batch view with new data, and the size of the batch views produced.(*pg 89*)

But the size of the batch view for an incremental algorithm can be significantly larger than the corresponding batch view for a Recomputation algorithm. This is because the view needs to be formulated in such a way that it can be incrementally updated. (*pg 89*)

Scalability is the ability of a system to maintain performance under increased load by adding more resources. Load in a Big Data context is a combination of the total amount of data you have, how much new data you receive every day, how many requests per second your application serves, and so forth. (*pg 92*)

When designing these indexes, you must consider two main performance metrics: throughput and latency. In this context, latency is the time required to answer a single query, whereas throughput is the number of queries that can be served within a given period of time. The relationship between the structure of the serving layer indexes and these metrics is best explained via an example. (**pg 181**)

There are a number of properties you’re concerned about with your queries: ■ Latency—The time it takes to run a query. In many cases, your latency requirements will be very low—on the order of milliseconds. Other times it’s okay for a query to take a few seconds. When doing ad hoc analysis, your latency requirements are often very lax, even on the order of hours. ■ Timeliness—How up-to-date the query results are. A completely timely query takes into account all data ever seen in the past, whereas a less timely query may not include results from the recent minutes or hours. ■ Accuracy—In many cases, in order to make queries performant or scalable, you must make approximations in your query implementations.[pg 285]

*Designing Data-Intensive Applications Marin Kep*

Load can be described with a few numbers which we call load parameters. The best choice of parameters depends on the architecture of your system: it may be requests per second to a web server, the ratio of reads to writes in a database, the number of simultaneously active users in a chat room, the hit rate on a cache, or something else. Perhaps the average case is what matters for you, or perhaps your bottleneck is dominated by a small number of extreme cases. (*pg 11*)

Once you have described the load on your system, you can investigate what happens when the load increases. You can look at it in two ways: • When you increase a load parameter and keep the system resources (CPU, mem‐ ory, network bandwidth, etc.) unchanged, how is the performance of your system affected? • When you increase a load parameter, how much do you need to increase the resources if you want to keep performance unchanged? (*pg13*)


In a batch processing system such as Hadoop, we usually care about throughput—the number of records we can process per second, or the total time it takes to run a job on a dataset of a certain size.iii In online systems, what’s usually more important is the service’s response time—that is, the time between a client sending a request and receiving a response.

Usually it is better to use percentiles. If you take your list of response times and sort it from fastest to slowest, then the median is the halfway point: for example, if your [pg44]

the client will see a slow overall response time due to the time waiting for the prior request to complete. Due to this effect, it is important to measure response times on the client side. 

An SLA may state that the service is considered to be up if it has a median response time of less than 200 ms and a 99th percentile under 1 s (if the response time is longer, it might as well be down), and the service may be required to be up at least 99.9% of the time


*A categorization scheme for SLA metrics, Schnappinger-Gerull*

Service Level Agreements (SLAs) defining the quality attributes (QoS - Quality of Service) and guarantees a service is required to process, are of growing commercial interest with a deep impact on the strategic and organisational processes, as many research studies and intensified interest in accepted management standards like ITIL1 or the new BS150002 show

No Description Object Unit
1 Availability Storage Time hour, percent
2 Maximum down-time Storage Hours or percent
33
3 Failure frequency Storage Number
4 Response time Storage Duration in minutes/seconds
5 Periods of operation Storage Time
6 Service times Storage Time
7 Accessibility in the case of problem Storage Yes/no
8 Backup Storage Time
9 Bytes per second Storage Number per second
10 Memory size Storage Number in bytes

# Write Up
---

- [ ] *What are the performance metrics used for such a system?*


Measurements used for testing come from standard Service LEvel Agreements (SLA) *A categorization scheme for SLA metrics, Schnappinger-Gerull* used to track not only big data applications and web servers, but software systems in general. Gerull catagorizes various measurments used in relation to our application, is helped defined in the table below.
Common systems peerformance metrics include CPU, memory, network bandwidth etc *Designing Data-Intensive Applications Marin Kep [pg 13]* with a greater focus on throughput. This includes latency or time taken to run a query, Timeliness or how up to date queries are and hugely, accuracy. This is mainly due to functionalities such as  incremental processing, speed layer or simply, inaccurate data can affect performance, although ideally as little as possible. To this end, it  is necessary to track the accuracy in comparison to the data actually created.



| Measurement | Unit | How it's calculated |
| ----------- | ---- | ------------------- |
| Throughput  |      |                     |



- [ ] What about metrics relating to web applications and servers?



Testing 

##### References
----
