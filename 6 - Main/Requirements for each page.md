2025-03-01 22:10

Status:

Tags:

---
**Dashboard**

- The components for the graphical elements
- Toggle button to view data for that component
- Able to see all the data sources for that component, including frequency, type, last refresh, how it was gotten(incremental, speed layer, computational refresh)
- Able to view the queries and columns related to the query
- Able to view the performance (amount of space taken, time to get response,  accuracy rate compared to actual)
- Able to see the raw data for the component
- Able to compare the assumed value against the actual value

- Able to view preliminary data by hovering over the toggle button 
- Able to filter the data on the page with input elements
- Able to view data changing on the time in accordance to changes on the speed layer


**Query Page**

(This could be the same page as the data sources page, but specifically adding or writing queries)
- Should be able to view all the previous queries, views, tables and other data in the prod table. 
- Should be able to write queries and test them out and save them once happy, and giving a name to this query along side some meta data.
- Should be able to view the output of each query, as a table and also able to see the data type in the column name e.g. Station(string)
- Able to view the input elements for each query, as well as the required type.
- Able to view the required meta data to allow for incremental counting for the speed layer, this metadata can either come from the batch views used or the actual query itself.
- Can either be a materialized view or regular view/query. If materialised view, edit when it should be after the refresh of each data source to either be immediately after it.

##### Requirements
- [x] Should be able to run a query and view the results
- [ ] Should be able to save the query
- [ ] Should be able to view the metadata associated with that query

**ETL**

- Timeline of the 3 stages for the ETL process (which represents both the speed layer and batch layer) as well as an expandable 4 layer that shows all the queries in relation to the loaded section.
- Should be able to click on each element and view it works. so viewing the query or process associated with it for that step, as well as data for that
- Be able to view performance data regarding the ETL Process, This includes, different measurements of throughput, latency, error rate, resource utilisation (amount of servers used), time taken for each process, load time, log of any and all issues with the pipeline.
- For the timeline, should be able to click each node and view metrics for that such as time taken to reach process, time of that process and more
- Should be able to view the pipeline for each data source 
- Should be able to view the refresh log of all pipelines, are a filtered look regarding the node selected. So log of all refreshes, average time taken to reach final query. As well as a log for all failures at every node
- Should be able to view error data generated during Pipeline, in order to state
  
- 
##### Requirements
- [ ] Should be able to see the steps for each query. contents of query and also change or delete them if necessary
- [ ] Should be able to add a step easily
- [ ] Should be able to view data be loaded in and out for batch views

**Test Data**

- Be able to view all the machines
- Be able to hover over machines to view their names and performance details
- Be able to hover over a report on the side of the page and view the relevant data along side the side
- Be able to update the performance of any node or machine.
- View the performance of the machine so able to see what machines are running e.g. Amount of back up data, rate of data added, amount of sources, amount of nodes, overview amount of parts per hour added
- Able to view the log of data being appended to the page.

##### References
----
