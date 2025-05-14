	2025-01-02 11:59

Status:

Tags: [[Final Year Project|Final Year Project]]


---
- How are queries written
- How does it handle old data
- How does it handle live data
- How does it handle both types of data

![[Pasted image 20250102122631.webp]]

Current Plan:
--

Full extraction from each data source listed into the raw.schema of the prod database. And then each query get's it's data directly from the raw equivalent with sql by querying the raw database directly. It also adds parameters for inputs where necessary to be used in the front end. For live data, there will be a websocket connection that live data would be added that would "show" that live data. Data from this live source would be uploaded in batch to the raw database. If extra external data is needed like having a count of occurences etc. it would be stored in the database and incremented on the server, before being updated again. For queries that require a mix of data from before and after the last refresh time, it can just query those sources directly to get those results.

Problems with this:
- Prod database must be bigger then all sources combined.
- How would you "Query" this live data or speed layer? 
- How exactly do you "combine" data from the live view and old view?
- 1 group refresh time instead being based on the actual query or page necessity? The PowerBI approach of having a list of queries associated with a page and refreshing them at interval times is probably better
- Inputs and outputs should have clearly defined types so it can be explicitly used in the front end
- Only 1 live data connection to the main server, and web sockets from the server, sending that live data + any additional calculations used for that page 

Second Plan:
--

Intial full extraction of all data sources into staging area, that is cleaned, indexed ,timestamped and versioned before moved to the raw schema. After that any batch refresh, will only add new or updated data. When it comes to live streams of data, they are going to be added to a fast redis database on the server and prod database for easy access with time stamp and index. So new data is added to the redis database and calculations are done from mixture of both. Since it has fields and types, it can be quried like normal with the results of these queries being streamed to the user.

There will be a query engine to see if it should take from the real-time view or batch-view and in the case the data is from the batch view but hasn't been refreshed yet, the data will be directly quieried from the database, and stored in the realtime view for future use.

Problems
- relies on learning third party query engine to work with my application to differentiate the difference between speed layer
- Still doesn't answer how exactly data is transformed, just has 1 gigantic table or tables representing each data source

So in our case, full extraction of each data source into the staging area of our database


Queries:
--

Intial idea: Just write the query against the data in the batch view via pure sql using $1, $2 to specify parameters.

When you run the query you can see the input parameters against the output values. You will need to specify the type of each field before saving

When running the query, the query engine will look at the time field if available to view if data needs to directly queried or not.

---

Example situation

2 Inputs, 3 outputs
3 data sources

Inputs:
- All Machines
- All Shifts
Outputs:
- CARD - Count Per Minute
- CARD - Total Amount of parts Produced
- CARD - Amount produced THIS shift
- BAR GRAPH - Amounts produced per machine.
- TABLE - Production data with class faults above 2. Machine, Class Faults, Production data

Data sources:
- Excel file for shift handover, saying what the shift is currently and it's name.
- Postgres database for production_data, stating what products a machine has made at a certain time
- Apache Kafka stream - Live sensor data giving each product, a class fault and measurement values associated with it.


- There are 3 layers.
- Batch Layer- which is responsible for historical data and complex queries
- Speed Layer - Responsible for real time data
- Serving Layer - A layer of abstraction that takes queries and get's data from the relevant layer
  
- Connect to every data source and initialise ETL Process
- Write a insert query in batches- Fully extract each data source into the staging area to be typed, cleaned, versioned and timestamped before moving to raw schema in the database
- Only new data is added with each refresh (around 30 minutes) to aid efficiency
- Live data is also connected to the server and batch uploaded the database at regular intervals.
- Data outside of refresh time is uploaded to a redis database instead for fast easier use. This can be CDC data or just live streams of data.
- User creates queries against these raw tables using sql, providing input and output schemas for front end use
- A query engine looks at the time filters of the query, compares it against the refresh time of the data sources and determines whether there is enough data for the time range, or if it needs to be directly queried, and data in the table needs to updated.
- On the front end, users can pass API requests against these queries to receive data

Test data script should on initialisation:
- Restart all data sources, so Delete all their data, and populate them with the last 2 weeks of data.
- Then have the slowly insert data new data.
- Also have an apache Kafka stream that uploads sensor data in accordance to products being made
- Delete data older then a certain amount of entries so It doesn't become too large or a burden.

Post Request:
api/add-datasource?raw
```
{
    "data_source_cred": {
        "name": "string",
        "creation_date": "timestamp",
        "created_by": "string"
    },
    "source_type": "string",
    "connection_details": [
        {
            "host": "string",
            "port": "int",
            "username": "string",
            "password": "string",
            "ssl_mode": "boolean"
        },
        {
            "broker": "string",
            "topic": "string",
            "API_KEY": "string"
        },
        {
            "URL": "string"
        }
    ],
    "data_parameters": {
        "table_name": "string",
        "columns": [
            {
                "name": "string",
                "type": "string"
            }
        ],
        "query": "string"
    }
}
```

api/add-datasource?staging

```
{
    "dataSource":{
        "id": 1,
        "steps": [
                {"query": "SELECT * FROM table1"},
                {"query": "SELECT * FROM table2"}
            ],
        "refreshTime": "2019-01-01T00:00:00Z",
        "lastRefreshTime": "2019-01-01T00:00:00Z",
        "FullRefreshTime": "2019-01-01T00:00:00Z",
        "incrementalRefreshTime": "2019-01-01T00:00:00Z"
    }
}
```

api/config/datasource

```
{
    "name": "string",
    "fullRefreshTime": "string",
    "incrementalRefreshTime": "string",
    "data_source_cred": {
        "source_type": "string",
        "connection_details": [
            {
                "host": "string",
                "port": "int",
                "username": "string",
                "password": "string",
                "ssl_mode": "boolean"
            },
            {
                "broker": "string",
                "topic": "string",
                "API_KEY": "string"
            },
            {
                "URL": "string"
            }
        ]
    },
    "data_parameters": {
        "table_name": "string",
        "columns": [
            {
                "name": "string",
                "type": "string"
            }
        ],
        "query": "string"
    }
}
```
``

##### References


----
