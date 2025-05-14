- Post request that takes the query for those tables + the values from the inputs and returns the actual relevant data
- Get request that gets and example first 100 rows from each data source or query
- Get request that gets every query.

IF Just before last batch refresh

- All data sources and their credentials are stored securely in the main database.
- At regular increments (e.g. every 30 minutes), the data ware house is refreshed by loading all of these data sources in to the database e.g. a postgres database. (So we keep both the raw data and the "Transformed" data)
  We can divide each layer into different schemas
- The user creates queries that are stored in the database. And these directly query the main database equivalent of the data sources.
- Each "area" of the page corresponds to a query so multiple inputs and output components, as well as saying how they are interacted e.g. this input page element's value corresponds to this WHERE statement, or this table contains these columns from the resulted queries etc.
- Have all those queries occur at page load/submit which are then passed on to each of the relevant "areas"


Products Per Minute - 
Total Amount Produced - 
Amount Produced This Shift-
Products Against Machine
Product data against Class Fault-