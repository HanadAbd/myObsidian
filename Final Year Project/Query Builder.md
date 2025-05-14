
The issues needed to solve for this:

- Extracting data from these data sources
- Building queries
- Make queries for Live data



Two Approaches

Dynamic SQL Query Builder
==

Literally just loading the results of each query for each data source and just combining them together to be altered in the front end. Could just start simply by only considering the JOIN statements for now, or passing Where filters from 1 database to another, but everything else can be done in after being loaded with an API request

So for a query like:

SELECT COUNTROWS 
FROM postgres.nodes
INNER JOIN mssql.nodes where mssql.nodes.id = postgres.nodes.id


Rather manually parse it, in order of instructions, or use a JDBC driver like # UnityJDBC or some sort of application to do it separately

Could also use a third party application and send the query them to handle that

##### Make more efficient
- Could be made faster with appropriate caching of final result, so just sending that instead of repeating the process. Could be done very smart by considering the actual API call being done by the user for the given thingamajig.
- Made faster with better splitting of the queries, and only keeping data on the server that will either be necessary for another query, or sent to the user
- Could have persistent connections for each user based on session, or if we're querying multiple data sources.



Data Warehouse
==

Sort of like a giant materialized view. At regular intervals we pass data from a data source into a larger data source where all queries will come from.

Using ETL, Extract, Transform and Load, we can only get the data absolutely necessary that's already been calculated and filtered on their end. (So instead of everything from the database, if we just need the Total count of distinct nodes, we'll get that instead or load that to the data warehouse)

Very efficient in terms of performance (especially when it comes to pagination or only getting really small amounts of data), but harder to set up, and causes issues with caching and getting live data.

### Make more efficient

- Data that needs to be live, can just be taken directly from that corresponding data source if need be, or could call for those relevant data sources to sync there data with the data warehouse before giving it to you.
- Caching requests made to the data warehouse is still possible and that side of it, is much easier to do and set up efficiently.

Leaning towards the data warehouse but with using PostgreSQL as the data warehouse and designing the queries based on that.

This is a bit dependent on how this is going to be deployed. Cloud data could be easier and more easier to set up. Could just have both options be available but only do PostgreSQL for now?

PostgreSQL would be setup using a starschema






