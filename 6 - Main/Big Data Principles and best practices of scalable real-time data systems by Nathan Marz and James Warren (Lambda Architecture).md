2025-01-16 14:49

Status: #baby 

Tags: [[Reading For Big Data]]

---
## Synopsis
---
Book made by the creator of the Lambda Architecture in order to ensure real-time data flow and query archive older data in a clear defined manner with minimal performance and ideal flexibility.


*7(28) Requirements of a big data system*
- **Robustness and Fault Tolerance**: Need to behave correctly despite machine's going down and regardless of human, by insuring immutability where possible
- **Low Latency Read/Writes**:
- **Scalability**: Maintaining performance despite increase in data and usage:
- **Extensibility**: Making it simple to add more features or changes to the systems
- **Ad hoc queries**: Should be able to handle sudden queries to compare data in a dataset
- **Minimal Maintenance**: Should be a simple to possible
- **Debuggability**: When something goes wrong, should be able to trace the error to view what caused that error


*14(35) Lambda architecture overview*

Comprised of 3 distinct Layers that are decoupled enough to not interfere with each other:
- **Batch Layer:** This stores the master dataset or the appending of all data and never deletes, with updates simply being logs that change earlier data. It also at fix intervals
- **Serving Layer:** Dataset where the batch views are uploaded too later. So a read only data store that at routine increments, asks the batch layer to update each of it's batch views in order to get the latest data. So queries use these batch layer views to append data.
- **Speed Layer:** Technically the last 2 Layers do everything but latency but that is a big issue. So this layer store's real-time views and does incremental update to those real-time views. So it isn't actually storing the appended data, on the real-time view. Since it doesn't have full context to the whole dataset, it's more of an approximation until the more reliable serving Layer. So if anything goes wrong, you can discard the real-time view, and regardless it will update correctly in a few hours with the next refresh.
![[Pasted image 20250301113222.webp]]


*88 (109) Recomputation algorithms vs. incremental algorithms*

So either full refresh by looking at the dataset and recomputing the views (I'm talking about both speed and batch layer), or incremental so ignoring the original dataset, and just appending new data according to the requirements of the view.

Incremental is much more efficient, especially in the case of the speed layer, since querying a small database every few ms to update the real-time view would be incredibly difficult. Also means we can have less data stored on the server which is helpful

In any case, Recomputation can be used, weekly or monthly to reset all data sources and metadata but in general unless there's a fault, incremental is used. Recomputation should be supported simply because of how fail-safe and fault-tolerant it is.

![[Pasted image 20250301144241.webp]]


*140(161) Creating Batch Views*

The main difficulty with batch views balancing the amount of read only data in the serving layer, against having as much data as possible for data analysis to use. This is incredibly dependent on use case.

Since it's between AllData -> Batch View -> Actual Query. So it's for the most part decided on by developers. That's why it's important to know Count of rows, time taken to create view, amount of storage taken and anything else that tells us the effectiveness of the batch view.

Batch views work on a pipeline of cleaning data, normalising any values, defining types , indexes etc. as well as removing duplicate events, and then generating the batch view you would need for other related queries.

At this point you can add any functionality you would need in order to make it effective such as creates graphs, star schemas, data cubes, etc.
Tips for making batch views include:

- Compute helpful aggregates instead of
- Apply indexes if possible
- Denormalization if possible.

*Note: The batch views in the serving layer are the ones that will be queried and potentially change by users. So the master dataset can be normalised, denormalisied or anything really, but the serving layer is under no obligation to match*'

*208(229) Speed Layer explanation*

Main features of speed layer is that it's Incremental computation only, only works on recent data so data past the last refresh, and automatically refreshed by the batch layer.

So essentially just updating the Realtime-view as data comes in and then refreshing after the batch layer refresh.

Since batch processing takes a while, and is still out of date even when completing (since it works on event time and only processes data before the event time of the batch starting), meaning the speed layer is typically 2 refresh cycles ahead.
![[Pasted image 20250301154541.webp]]

Typical solution used is having 2 real-time views that you alternate clearing and loading in
![[Pasted image 20250301154757.webp]]



*Requirements of data to be added into Lambda architecture*

✔ **Event Timestamps** → Needed for proper ordering & windowing.  
✔ **Immutable Data** → No updates or deletes; changes are new records.  
✔ **Partitioning** → Data must be split for parallel processing.  
✔ **Schema Definition** → Clear structure for Batch & Speed layers.  
✔ **Batch + Speed Layer Compatibility** → Store data in optimal formats.  
✔ **Deduplication & Idempotency** → Prevent duplicate events.  
✔ **Fault Tolerance** → Must recover from failures.

*37(57) Batch Layer and Master Dataset*

The key properties of a master dataset is:
- **rawness**: Data stored is as raw as possible as long as it's still effective and useful
- **immutability**: Data can not be changed or deleted, and is therefore Append only. Updates are also appended. Drastically reduces the chance of failure and total error loss.
- **perpetuity**: Data is eternally true, so at a given **time** and **situation**, this event was true e.g. This product left this machine at timestamp, which always be true. Doesn't necessarily have to be timestamp, but every fact added to the master dataset must be eternally true and timestamping, is a helpful way to achieve that, even if it's the timestamp of the data being pulled.

Uses a fact based model so each **event** is atomic (entirely self contained useful information), immutable and true with timestamps,
and needs an identifiable feature so it can tell a part duplicates. Whether that's an id or composite Key. This makes it as easy to query as possible, fault tolerant (simple to delete no longer used facts)

There also needs to be a schema for each fact in order to be enforce types and reduce errors as well as types of values accepted. So needs to define what facts are optional/required, structure of the expected data


##### References
----
[Big Data ](file:///C:/Users/Asus/Downloads/Book-7Nathan%20Marz,%20James%20Warren%20Big%20Data%20Principles%20and%20best%20practices%20of%20scalable%20realtime%20data%20systems.pdf)